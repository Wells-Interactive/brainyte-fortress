# Fortress Enterprise

**Status: PLANNED** — placeholder only.

Fortress Enterprise provides organization-level (tenant) capabilities: device
enrollment, user provisioning, organizational roles, hierarchical policy
inheritance, and tenant-scoped audit.

## Boundaries

- Owns tenant scoping rules. Tenant data must **never** be exposed across
  organizational boundaries.
- Depends on Fortress Identity for authentication and subject resolution.
- Policy evaluation itself is shared with Fortress Cloud's policy engine; the
  Enterprise component owns the *hierarchy and inheritance model*, not the
  client-side enforcement.
- Consumes `shared/` contracts. Contains no business logic belonging to
  Identity, Cloud, Admin, Mail or Mobile.

## Enforcement note

Enterprise capabilities on standard Android are limited to Android Enterprise /
Device Owner APIs. Stronger system-level enforcement belongs to AfOS Android
and is out of scope for this repository.

