---
layout: default
title: Database Regeneration
nav_order: 5
permalink: /docs/regeneration/
---

# Database Regeneration & Maintenance

Procedures for resetting, executing migrations, backing up, and restoring the application state.

## Schema Migrations
Instructions for executing SQLite schema migrations safely using upgrade scripts without risking data loss.

## Backup & Recovery
* **Manual Backups:** Locate and archive local `.db` files to secondary storage or cloud drives.
* **Restoration:** Steps to replace or restore application database state from a known stable snapshot.
