# Liquibase Version Tagging Guide

## Current Tags
- v1.0 → Initial users and roles tables, phone column added
- v1.1 → Security updates and data type refinements

## Commands
- Apply all changes: `liquibase update`
- Tag database version: `liquibase tag v1.2`
- Rollback to version: `liquibase rollbackToTag v1.0`
- Show history: `liquibase history`
- Validate changelog: `liquibase validate`

## Rollback Strategy
Each changeset includes rollback logic, allowing safe reversion to any tagged version.