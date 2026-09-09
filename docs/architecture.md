---
layout: default
title: Architecture
nav_order: 3
permalink: /docs/architecture/
---

# System Architecture

Orchid Tracker is constructed using a Python desktop application architecture backed by a local relational database engine.

## Key Architectural Components
* **User Interface:** Built with `CustomTkinter` for modern desktop UI components and responsive layouts.
* **Database Engine:** `SQLite3` database structure enforcing relational integrity across specimen, media, and telemetry tables.
* **Data Persistence:** Local flat-file storage ensuring full offline capabilities and seamless backup export routines.
