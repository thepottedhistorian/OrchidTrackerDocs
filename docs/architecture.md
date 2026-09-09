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

```text
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
