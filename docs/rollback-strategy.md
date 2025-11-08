# Rollback Strategy

## Overview
This document explains how Liquibase rollbacks are handled in the Database DevOps Project.

Every changeset in `changelogs/v1.0/db.changelog-v1.0.yaml` includes a `<rollback>` section to safely reverse schema or data changes.

## Testing Procedure
1. Run `liquibase update` to apply changes.
2. Run `liquibase rollbackCount 1` to undo the last change.
3. Check MySQL tables and data to confirm rollback worked.
4. Run `liquibase update` again to reapply the change.

## Data Integrity Verification
- After rollback of `id=1`: `users` and `roles` tables are dropped.
- After rollback of `id=2`: foreign key `fk_users_roles` is removed.
- After rollback of `id=3`: index `idx_users_username` is removed.
- After rollback of `id=4`: reference rows ('Admin', 'User') are deleted from `roles`.
- After rollback of `id=5`: `phone` column is dropped from `users`.
- After rollback of `id=6`: datatype of `username` reverts from `VARCHAR(200)` to `VARCHAR(100)`.

## Rollback Safety Guidelines
- Do not modify old changesets once applied in production.
- Always test rollbacks on a staging database before deploying to production.
- Maintain changelog versioning for traceability.

## Example Rollback Commands
```bash
liquibase rollbackCount 1
liquibase rollbackToDate 2025-10-15
liquibase clearCheckSums

