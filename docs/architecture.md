---
layout: default
title: Architecture
nav_order: 3
permalink: /docs/architecture/
---

# System Architecture

Orchid Tracker is constructed as a modular Python desktop application utilizing **CustomTkinter** for the user interface and **SQLite3** for offline relational data storage.

---

## Directory Architecture
```
orchid_archivist/
│
├── config.py             # Palette, theme settings, and system paths
├── database.py           # SQLite initialization & schema migrations
├── main.py               # Main window application controller & menus
│
├── utils/
│   └── id_parser.py      # Range parser for bulk operation IDs
│
└── ui/
    ├── widgets.py        # Reusable UI components & status dots
    ├── dialogs/
    │   └── specimen_passport_dialog.py
    ├── modals/
    │   ├── bulk_action_modals.py
    │   ├── passport_modal.py
    │   └── system_modals.py
    └── views/
        ├── accession_view.py
        ├── bulk_ops_view.py
        └── inventory_view.py
```
---

## Relational Database Schema

The SQLite database (orchids.db) relies on primary-foreign key relationships linking child logs to master orchid records.
```
-- Master Inventory Table
CREATE TABLE orchids (
    id INTEGER PRIMARY KEY,
    orchid_name TEXT NOT NULL,
    genus TEXT,
    species_hybrid_lineage TEXT,
    growth_habitat TEXT,
    leaf_behaviour TEXT,
    alliance TEXT,
    endemic_to TEXT,
    acquisition_date TEXT,
    vendor_source TEXT,
    in_bloom TEXT,
    last_bloom_date TEXT,
    bloom_duration TEXT,
    rest_period TEXT,
    last_watered_date TEXT,
    last_repotted_date TEXT,
    fragrance TEXT,
    light_needs TEXT,
    foot_candles TEXT,
    watering_needs TEXT,
    humidity TEXT,
    potting_media TEXT,
    fertilizer_routine TEXT,
    repotting_schedule TEXT,
    next_repot_due TEXT,
    general_notes TEXT,
    profile_photo TEXT,
    cost REAL
);

-- Relational Care Logs
CREATE TABLE bloom_log (
    log_id INTEGER PRIMARY KEY AUTOINCREMENT,
    orchid_id INTEGER,
    in_bloom_date TEXT,
    out_of_bloom_date TEXT,
    duration TEXT,
    notes TEXT,
    FOREIGN KEY(orchid_id) REFERENCES orchids(id)
);

CREATE TABLE repotting_log (
    log_id INTEGER PRIMARY KEY AUTOINCREMENT,
    orchid_id INTEGER,
    repot_date TEXT,
    notes TEXT,
    FOREIGN KEY(orchid_id) REFERENCES orchids(id)
);

CREATE TABLE watering_logs (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    orchid_id INTEGER,
    water_date TEXT,
    method TEXT,
    notes TEXT,
    FOREIGN KEY(orchid_id) REFERENCES orchids(id)
);

CREATE TABLE observation_notes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    orchid_id INTEGER,
    log_date TEXT,
    observation TEXT,
    FOREIGN KEY(orchid_id) REFERENCES orchids(id)
);
```
---

## Archive Database Table Schema

To preserve historical records without cluttering active inventory, retired or deceased specimens are transferred to the archived_orchids master table.
```
CREATE TABLE archived_orchids (
    archive_id INTEGER PRIMARY KEY AUTOINCREMENT,
    id INTEGER,
    original_id INTEGER,
    orchid_name TEXT,
    genus TEXT,
    species_hybrid_lineage TEXT,
    acquisition_date TEXT,
    archive_date TEXT,
    archived_date TEXT,
    final_status TEXT,
    disposition_status TEXT,
    disposition_notes TEXT,
    general_notes TEXT,
    acquisition_cost TEXT
);
```
---

## Schema Auto-Migration Guard Engine

The database.py initialization sequence contains an automated schema migration guard. On application startup, PRAGMA table_info() inspects active database tables and injects missing columns dynamically without requiring manual SQL scripts or dropping existing records.
```
-- Migration check for orchids table
PRAGMA table_info(orchids);
-- Conditionally executed if column is missing:
ALTER TABLE orchids ADD COLUMN vendor_source TEXT;
ALTER TABLE orchids ADD COLUMN rest_period TEXT;

-- Migration check for archived_orchids table
PRAGMA table_info(archived_orchids);
-- Conditionally executed if column is missing:
ALTER TABLE archived_orchids ADD COLUMN acquisition_cost TEXT;
ALTER TABLE archived_orchids ADD COLUMN species_hybrid_lineage TEXT;
```
---

## Application State & Memory Lifecycle
```
┌────────────────────────────────────────────────────────────────────────┐
│                        main.py (Application Root)                      │
│  - Registers Windows AppUserModelID                                    │
│  - Configures CustomTkinter CTk Base Frame & Theme                     │
│  - Builds Native Tkinter Menu Bar & System Status Bar                  │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
         ┌──────────────────────────┴──────────────────────────┐
         ▼                                                     ▼
┌─────────────────────────────────┐           ┌──────────────────────────────────┐
│      database.py Engine         │           │       View Manager Stack         │
│  - Connects to orchids.db       │           │  - InventoryView                 │
│  - Executes PRAGMA Auto-Guard   │           │  - AccessionView                 │
│  - Runs Integrity & VACUUM      │           │  - BulkOpsView                   │
└─────────────────────────────────┘           └──────────────────────────────────┘
```
1. **Initialization Phase**: main.py invokes init_database() from database.py, connecting to orchids.db and creating tables or running auto-migrations.
2. **OS & UI Registration**: Registers the process explicitly under thepottedhistorian.orchidtracker.archivist.1.0 via Windows ctypes.windll to ensure taskbar pinning and custom icon rendering.
3. **View Instantiation**: Initializes primary views (InventoryView, AccessionView, BulkOpsView) within content_frame and displays the default Inventory view.
4. **State Management**: Navigation switches views by invoking .pack_forget() on hidden frames and packing the selected view into the active layout frame.
