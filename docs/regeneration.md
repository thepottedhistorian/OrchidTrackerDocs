---
layout: default
title: Database Maintenance
nav_order: 5
permalink: /docs/regeneration/
---

# Database Maintenance & Migration

Orchid Tracker includes built-in maintenance operations and automated migration scripts to protect data integrity and import legacy spreadsheets.

---

## Automated System Routines

These maintenance functions are accessible directly from the application's native **Database** menu:

### 1. Smart Repot Recalculation
Recalculates `next_repot_due` milestone dates across all specimens. It parses interval strings (e.g., `"24 months"`) and calculates target due dates based on either the latest entry in `repotting_log` or the original `acquisition_date`.

### 2. Bloom Validation Sweep
Scans active records marked as `"In Bloom"`. If a blooming log entry exceeds 180 days without an `out_of_bloom_date`, the system flags the plant as `"Check File ⚠️"` to prevent stale records.

### 3. SQLite Vacuum & Compression
Executes the `VACUUM;` SQL command to defragment the SQLite database file on disk, clearing unused pages and minimizing storage overhead.

### 4. Schema Integrity Diagnostics
Runs `PRAGMA integrity_check;` against the connected `.db` file, validating index structure, table allocation, and cell integrity.

---

## Excel Import Pipeline

For bulk imports or legacy spreadsheet conversions, Orchid Tracker uses specialized Python import tools:

* **`orchid_importer_inventory.py`**: Reads the master `Inventory` worksheet, normalizes column headers, and upserts data into `orchids` and `care_profile` using `ON CONFLICT(id) DO UPDATE`.
* **`orchid_importer_passport.py`**: Ingests individual numbered passport tabs (e.g., `1`, `2`, `3`), extracting historical bloom cycles, observation logs, repotting events, and watering history into relational child tables.
