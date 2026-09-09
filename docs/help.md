---
layout: default
title: Help & Support
nav_order: 6
permalink: /docs/help/
---

# Help & Troubleshooting

Common troubleshooting workflows, menu shortcuts, and error recovery steps for Orchid Tracker.

---

## Native Menu Bar Overview

The native top menu bar (`main.py`) provides access to critical system actions:

* **File Menu**:
  * `New Database Repository`: Creates a clean SQLite `.db` file and initializes core tables.
  * `Switch Database Repository`: Switches application context to an existing `.db` file.
  * `Print Manifest Ledger`: Exports active collection inventory to a formatted temporary file and sends it to the default system printer.
* **Database Menu**: Runs recalculations, validation sweeps, SQLite VACUUM compression, and PRAGMA integrity checks.
* **Tools Menu**: Reloads active views and opens the Historical Archive Catalog.

---

## Common Issues & Resolutions

### Database Connection Warning on Startup
* **Symptom**: Application displays a `Database Initialization Warning` dialog upon launching.
* **Resolution**: Ensure write permissions exist in the application folder or use **File -> Switch Database Repository** to re-point the application to a valid `orchids.db` file.

### Missing Windows Taskbar Icon
* **Symptom**: Standard generic executable icon appears in the taskbar instead of the orchid seal icon.
* **Resolution**: `main.py` explicitly registers a custom Windows `AppUserModelID` (`thepottedhistorian.orchidtracker.archivist.1.4.0`). Ensure `orchid_icon.ico` remains in the root directory alongside `config.py`.

### Missing Columns After Version Upgrade
* **Symptom**: Error messages regarding missing database fields when opening older `.db` files.
* **Resolution**: The `database.py` module includes automatic schema migration checks on launch, adding missing columns (e.g., `vendor_source`, `rest_period`, `acquisition_cost`) without dropping existing plant records.
