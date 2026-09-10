---
layout: default
title: Home
nav_order: 1
permalink: /
---

# Orchid Tracker Documentation

Welcome to the documentation for Botanical Archivist (Orchid Tracker).

If you’ve ever tried keeping track of a growing orchid collection across random notebooks, scattered spreadsheets, or phone apps that keep hiding features behind a monthly subscription, you know how frustrating it gets. Orchid Tracker was built to fix that—giving you a dedicated, offline space to manage your plants without the clutter or cloud dependencies.

At its core, Orchid Tracker is a lightweight desktop app built with Python and CustomTkinter. It pairs a dark-slate visual palette with a clear, straightforward layout so you can update care records or check environmental telemetry late at night without blinding yourself. Whether you are logging custom fertilizer ratios, keeping tabs on wet-dry watering cycles, tracking bloom durations, or noting when a specimen was last repotted into bark and sphagnum, everything is organized in one place.

Because it runs completely on your local machine using an isolated SQLite database, your records remain entirely under your control. There are no mandatory updates, no accounts to log into, and no risk of losing your collection's history if an external server goes down. When a plant gets re-homed, sold, or lost, its records are safely moved into a historical archive table—preserving your botanical notes and lineage data without cluttering your active inventory view.

---

## Core Features

* **Master Inventory Ledger:** Sort, filter, and search through active plants with custom tags, status indicators, and quick care updates.
* **Specimen Passports:** Detailed profile cards for individual orchids, covering taxonomy, substrate mixes, light needs, acquisition notes, and photo galleries.
* **Care Chronicles:** Tabbed event logging to keep clear records of watering routines, fertilizer formulas, repotting dates, and new flower spikes.
* **Historical Archive:** When a plant is re-homed, sold, or lost, its history moves to a dedicated archive table—keeping active lists clean without erasing past records.
* **Local SQLite Storage:** Everything stays on your machine. Your data, notes, and file paths remain strictly in a local database file under your control.

---

## Navigation & Core Topics

* **[Project Overview](docs/overview)**: Purpose, primary user workflows, dark palette aesthetics, and core collection features.
* **[System Architecture](docs/architecture)**: Python execution loop, CustomTkinter UI framework, and full SQLite3 schema specifications.
* **[Core Modules](docs/modules)**: In-depth breakdowns of `InventoryView`, `AccessionView`, `BulkOpsView`, and modal systems.
* **[Database Maintenance & Migration](docs/regeneration)**: Maintenance routines, SQLite VACUUM compression, integrity checks, and Excel migration scripts.
* **[Troubleshooting & Support](docs/help)**: Native menu bar actions, DB connection handling, diagnostic tools, and support options.
* **[Development Roadmap](docs/roadmap)**: Planned greenhouse dashboards, care forecasting, and telemetry features.
* **[Version History](docs/version-history)**: Release history spanning v1.0 through v1.4.0.
* **[Appendices](docs/appendices)**: Full database schema definition, color palette constants, and file tree index.
