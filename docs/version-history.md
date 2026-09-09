---
layout: default
title: Version History
nav_order: 8
permalink: /docs/version-history/
---

# Version History & Changelog

Complete record of version releases, core features, and architectural updates.

---

### v1.4.0 (Current Version)
* **Inventory View Overhaul**: Implemented unified header bar, sortable inventory columns, and fixed header rows.
* **Database Maintenance Tools**: Added automated smart repot recalculations, bloom status validation sweeps, SQLite VACUUM optimization, and PRAGMA integrity diagnostics.
* **Schema Expansion**: Enforced primary key alignment (`id`), added auto-migrations for vendor tracking and rest periods, and unified historical archive fields.
* **CTk Glass Palette**: Fine-tuned dark glass aesthetic constants across all views and system modals.

---

### v1.3.0
* Updated user interface to CustomTkinter dark theme.
* Standardized spacing, typography, and contrast across forms and modal dialogs.

---

### v1.2.0
* Introduced Bulk Operations view with range parser (`id_parser.py`) supporting multi-plant watering and repotting routines.

---

### v1.1.0
* Introduced Specimen Passport modal cards displaying acquisition metrics, bloom logs, and care notes.
* Added relational database tables for bloom tracking and repotting logs.

---

### v1.0.0
* Initial working release featuring core specimen inventory logging, CustomTkinter window setup, and local SQLite database engine.
