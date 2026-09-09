---
layout: default
title: Appendices
nav_order: 9
permalink: /docs/appendices/
---

# Appendices & Reference Materials

Supplementary reference data, color palette specifications, and system configuration constants.

---

## Appendix A: Theme Palette Constants (`config.py`)

```python
COLOR_BG_DARK = "#020617"       # Main background tone
COLOR_PANEL_DARK = "#0F172A"    # Primary dark container panel
COLOR_PANEL_LIGHT = "#111827"   # Secondary panel contrast tone

COLOR_TEXT_PRIMARY = "#FFFFFF"  # High-contrast primary text
COLOR_TEXT_MUTED = "#9CA3AF"    # Secondary/muted labels

COLOR_ACCENT_GREEN = "#4ADE80"  # Success / In Bloom indicators
COLOR_DANGER_RED = "#EF4444"    # Alerts / Errors / Destructive actions
COLOR_STATUS_BLUE = "#60A5FA"   # Info / Primary action accents
```
## Appendix B: Master Database Field Descriptions (`orchids` Table)

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `id` | `INTEGER` | Primary Key (Specimen Accession #) |
| `orchid_name` | `TEXT` | Primary name or clone title |
| `genus` | `TEXT` | Taxonomic genus (e.g., *Phalaenopsis*, *Cattleya*) |
| `species_hybrid_lineage` | `TEXT` | Species status or hybrid parentage lineage |
| `growth_habitat` | `TEXT` | Growth habit (Epiphyte, Lithophyte, Terrestrial) |
| `vendor_source` | `TEXT` | Nursery or vendor source |
| `in_bloom` | `TEXT` | Bloom state status (`In Bloom`, `Not in Bloom`, `Check File ⚠️`) |
| `foot_candles` | `TEXT` | Target light levels (e.g., `500–1,000 fc`) |
| `repotting_schedule` | `TEXT` | Required repotting interval (e.g., `24 months`) |
| `next_repot_due` | `TEXT` | Calculated target date for repotting |

---

## Appendix C: Relational Child Log Schemas

### `bloom_log`

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `log_id` | `INTEGER` | `PRIMARY KEY AUTOINCREMENT` | Log entry unique ID |
| `orchid_id` | `INTEGER` | `FOREIGN KEY -> orchids(id)` | Parent specimen reference ID |
| `in_bloom_date` | `TEXT` | — | Date bloom cycle initiated |
| `out_of_bloom_date` | `TEXT` | — | Date flowers dropped or faded |
| `duration` | `TEXT` | — | Calculated or logged bloom duration |
| `notes` | `TEXT` | — | Observational bloom notes |

### `repotting_log`

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `log_id` | `INTEGER` | `PRIMARY KEY AUTOINCREMENT` | Log entry unique ID |
| `orchid_id` | `INTEGER` | `FOREIGN KEY -> orchids(id)` | Parent specimen reference ID |
| `repot_date` | `TEXT` | — | Date repotting was performed |
| `notes` | `TEXT` | — | Substrate blend, pot size, or root notes |

### `watering_logs`

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `INTEGER` | `PRIMARY KEY AUTOINCREMENT` | Log entry unique ID |
| `orchid_id` | `INTEGER` | `FOREIGN KEY -> orchids(id)` | Parent specimen reference ID |
| `water_date` | `TEXT` | — | Timestamp of hydration event |
| `method` | `TEXT` | — | Application method (Pour, Soak, Flush) |
| `notes` | `TEXT` | — | Fertilizer additives or water quality notes |

### `observation_notes`

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `id` | `INTEGER` | `PRIMARY KEY AUTOINCREMENT` | Log entry unique ID |
| `orchid_id` | `INTEGER` | `FOREIGN KEY -> orchids(id)` | Parent specimen reference ID |
| `log_date` | `TEXT` | — | Observation record date |
| `observation` | `TEXT` | — | Detailed health or growth notes |

## Appendix D: Legacy Excel Column Mapping (`orchid_importer_inventory.py`)

| Excel Sheet Column (`Inventory`) | Target SQLite Field | Target Table |
| :--- | :--- | :--- |
| `ID #` | `id` / `orchid_id` | `orchids` / `care_profile` |
| `Orchid Name` | `orchid_name` | `orchids` |
| `Genus` | `genus` | `orchids` |
| `Species/Hybrid Lineage` | `species_hybrid_lineage` | `orchids` |
| `Alliance` | `alliance` | `orchids` |
| `Endemic To` | `endemic_to` | `orchids` |
| `Acquisition date` | `acquisition_date` | `orchids` |
| `Source` | `vendor_source` | `orchids` |
| `In Bloom` | `in_bloom` | `orchids` |
| `Last Bloom Date` | `last_bloom_date` | `orchids` |
| `Fragrance` | `fragrance` | `orchids` |
| `Repot Every` | `repotting_schedule` | `orchids` |
| `Next Repot Due` | `next_repot_due` | `orchids` |
| `Potting Media` | `potting_media` | `orchids` |
| `Fertilizer Routine` | `fertilizer_routine` | `orchids` |
| `Growth Habitat` | `growth_habitat` | `care_profile` |
| `Leaf Behaviour` | `leaf_behaviour` | `care_profile` |
| `Light Needs` | `light_needs` | `care_profile` |
| `Approximate Foot Candles` | `foot_candles` | `care_profile` |
| `Watering Needs` | `watering_needs` | `care_profile` |
| `Humidity` | `humidity` | `care_profile` |

---

## Appendix E: Application Metadata & System Paths (`config.py`)

| Constant | Value / Default Path | Description |
| :--- | :--- | :--- |
| `APP_VERSION` | `"1.4.0"` | Current release version identifier |
| `CURRENT_DATABASE_FILE` | `os.path.join(BASE_DIR, "orchids.db")` | Active SQLite database path |
| `APP_ICON_FILE` | `os.path.join(BASE_DIR, "orchid_icon.ico")` | Application taskbar icon file path |
| `TIME_FORMAT` | `"%Y-%m-%d %H:%M:%S"` | Standard ISO database timestamp string format |
| `DISPLAY_TIME_FORMAT` | `"%b %d, %Y — %I:%M %p"` | Human-readable UI display timestamp format |

---

## Appendix F: System Requirements & Dependencies

| Dependency / Component | Minimum Version | Module Reference | Purpose |
| :--- | :--- | :--- | :--- |
| **Python** | `3.10+` | Application Runtime | Core programming language environment |
| **CustomTkinter** | `5.2+` | `ui/` views and modals | Modern dark-themed GUI component framework |
| **SQLite3** | `3.35+` | `database.py` | Embedded relational database engine supporting UPSERT syntax |
| **Pandas** | `2.0+` | `orchid_importer_*.py` | Dataframe manipulation for Excel sheet ingestion and manifest printing |
| **openpyxl** | `3.1+` | Importer Utilities | Excel workbook parsing backend for `.xlsx` formats |

---

## Appendix G: Error Codes & Exception Catalog

| Exception Context | Error Message / Pattern | Trigger Condition | System Recovery Action |
| :--- | :--- | :--- | :--- |
| **Database Connection** | `Database Initialization Warning` | SQLite file lock or invalid path permission | Catches error gracefully, launches UI shell, prompts for DB path switch |
| **Range Parsing** | `Invalid ID range format` | Malformed string in bulk operations input | Aborts operation execution and updates status bar with danger accent |
| **Excel Ingestion** | `No Inventory sheet found` | Missing target tab in workbook during import | Raises `RuntimeError` and terminates process without DB commit |
| **Taskbar Registration** | `ctypes.windll` exception | Non-Windows OS or restricted privilege execution | Ignores registration error quietly via fallback pass block |

---

## Appendix H: UI Color Code Quick-Reference

| Element Category | Hex Code | UI Component Usage |
| :--- | :--- | :--- |
| **Main Background** | `#020617` | Root application window background |
| **Primary Panel** | `#0F172A` | Main container frame and status bar |
| **Secondary Panel** | `#111827` | Content card frames and tab backgrounds |
| **Primary Text** | `#FFFFFF` | Headers, active values, and primary labels |
| **Muted Text** | `#9CA3AF` | Subtitles, field descriptions, and inactive states |
| **In Bloom / Success** | `#4ADE80` | Blooming status indicators and success alerts |
| **Alert / Danger** | `#EF4444` | Out of bloom flags, deletion warnings, and error messages |
| **Primary Action** | `#60A5FA` | Buttons, navigation selection, and active menu items |

---

## Appendix I: CustomTkinter Component Hierarchy

| UI Layer / Class | Source Module | Base Class / Framework | Key Child Widgets & Responsibilities |
| :--- | :--- | :--- | :--- |
| `OrchidTrackerGlassApp` | `main.py` | `ctk.CTk` | Root window shell, native menu bar, global status bar, view switcher |
| `InventoryView` | `ui/views/inventory_view.py` | `ctk.CTkFrame` | Master table ledger, search/filter inputs, overview metric cards |
| `AccessionView` | `ui/views/accession_view.py` | `ctk.CTkFrame` | New specimen form inputs, genus selectors, cost/media entries |
| `BulkOpsView` | `ui/views/bulk_ops_view.py` | `ctk.CTkFrame` | ID range input parser interface, bulk action trigger shortcuts |
| `SpecimenPassportDialog` | `ui/dialogs/specimen_passport_dialog.py` | `ctk.CTkToplevel` | Multi-tab specimen card (Acquisition, Care, Bloom, Repot logs) |
| `BulkActionModal` | `ui/modals/bulk_action_modals.py` | `ctk.CTkToplevel` | Input validation modal for batch watering/repotting operations |
| `SystemModals` | `ui/modals/system_modals.py` | `ctk.CTkToplevel` | Historical archive viewer, genus care guides, system documentation |

## Appendix J: CLI Utilities & Execution Reference

| Script Name | Command Line Usage | Primary Function | Output / Result |
| :--- | :--- | :--- | :--- |
| `main.py` | `python main.py` | Launches the primary CustomTkinter application | GUI desktop window |
| `orchid_importer_inventory.py` | `python orchid_importer_inventory.py <manifest.xlsx>` | Ingests master `Inventory` worksheet into SQLite | Upserts `orchids` & `care_profile` tables |
| `orchid_importer_passport.py` | `python orchid_importer_passport.py <manifest.xlsx>` | Ingests per-orchid passport tabs (`1`, `2`, `3`...) | Populates child log tables |
| `patch_bloom_data.py` | `python patch_bloom_data.py` | Executes targeted historical bloom log repairs | Updates `bloom_log` table for target ID |

---

## Appendix K: Directory Map & File Artifacts

| Path / File Artifact | File Type | System Access | Purpose & Contents |
| :--- | :--- | :--- | :--- |
| `config.py` | Python Script | Read / Write | Defines color constants, time formats, version string, and runtime database file path |
| `database.py` | Python Script | Read / Write | Executes `CREATE TABLE IF NOT EXISTS` statements and handles schema auto-migrations |
| `main.py` | Python Script | Execution Entrypoint | Initializes `OrchidTrackerGlassApp`, builds native Tkinter menus, manages view routing |
| `orchids.db` | SQLite Database | Read / Write | Primary local relational data store containing active collection and archive tables |
| `orchid_icon.ico` | Application Icon | Read Only | Embedded window and Windows taskbar branding icon |
| `utils/id_parser.py` | Python Module | Read Only | Utility functions for parsing user-entered ID strings and range lists for bulk operations |
| `ui/widgets.py` | Python Module | UI Component | Shared custom widgets, status dot indicators, and reusable frame containers |
| `ui/dialogs/specimen_passport_dialog.py` | Python Module | Modal Overlay | Formats individual plant records, historical bloom logs, and repotting histories |
| `ui/modals/bulk_action_modals.py` | Python Module | Modal Overlay | Input validation dialogs for batch watering routines and bulk substrate changes |
| `ui/modals/passport_modal.py` | Python Module | Modal Overlay | Primary passport modal interface displaying specimen acquisition and care profile data |
| `ui/modals/system_modals.py` | Python Module | Modal Overlay | System dialogs for historical archive catalog, genus care guides, changelog, and help docs |
| `ui/views/inventory_view.py` | Python View | Primary View | Master specimen table with sortable columns, live search filtering, and overview metrics |
| `ui/views/accession_view.py` | Python View | Primary View | Data entry form for logging new orchids, vendor sources, costs, and care requirements |
| `ui/views/bulk_ops_view.py` | Python View | Primary View | Workspace for executing multi-plant watering and repotting maintenance routines |
