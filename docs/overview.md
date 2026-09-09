---
layout: default
title: Overview
nav_order: 2
permalink: /docs/overview/
---

# Project Overview

Orchid Tracker was created to eliminate spreadsheet clutter and provide a structured, calm environment for managing large orchid collections. It combines real-time collection metrics with specimen-level detail, allowing growers to track taxonomic lineage, microclimate requirements, vendor sources, and care routines.

---

## Core Operational Features

* **Master Inventory Ledger**: Features a sortable, filterable table display with fixed header rows and status indicators for active specimens.
* **Specimen Passport Modals**: Individual modal cards providing comprehensive details for each plant, including acquisition data, taxonomic lineage, bloom records, repotting history, and care notes.
* **Bulk Maintenance Engine**: Dedicated interface for executing multi-plant watering and repotting routines using range parsing (e.g., `1-10, 15`).
* **Historical Archive**: Retires deceased or re-homed specimens into a separate `archived_orchids` database table, preserving historical records without cluttering active inventory.

---

## Visual Design & Theme

Built on a **CTk Glass Dark Palette**, the visual architecture is designed to minimize visual fatigue during extended logging sessions:

* **Background Tone**: `#020617` (Deep dark slate)
* **Panel Tone**: `#0F172A` / `#111827` (Layered contrast frames)
* **Status Accents**: `#4ADE80` (In Bloom / Success), `#EF4444` (Alerts / Errors), and `#60A5FA` (Primary Action Accents)
