# Database

**Status: PLANNED** — no schema, migration or seed data exists yet.

PostgreSQL is the architecture baseline: the data is highly relational, needs
flexible JSON metadata, policy versioning, and future geospatial workloads.

## Structure

| Directory     | Responsibility                                          |
| ------------- | ------------------------------------------------------- |
| `migrations/` | Versioned, forward-only schema migrations                |
| `seeders/`    | Non-production reference data only                        |
| `functions/`  | Stored functions / triggers                               |
| `policies/`   | Database-level access-control (row-level security) rules |

Identity-specific migrations live with the service that owns the data, under
`backend/fortress-identity/migrations/`. This directory holds migrations for
Fortress Cloud and shared platform concerns.

## Rules

- Never build SQL with string concatenation; use parameterized queries only.
- Use a database abstraction layer and least-privilege database accounts.
- Tenant isolation is enforced in the data layer (row-level security), never
  only in application code.
- Migrations are recorded and never silently destroy user data.
- Database credentials are never committed; development, test and production
  credentials are separate.
- Backups are encrypted, access-controlled, and restore-tested.
- Every sensitive field has a documented purpose and retention period.

## Ownership

Fortress Cloud owns its own tables. Fortress Identity owns identity tables.
A table has exactly one owning service; cross-service access goes through a
contract, not a shared schema.
