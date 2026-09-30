# Changelog

All notable changes to Brainyte Fortress are recorded here.

Status vocabulary used throughout: `PLANNED` → `IN DEVELOPMENT` → `IMPLEMENTED`
→ `TESTED` → `VERIFIED`.

## Unreleased

### Added — repository foundation (placeholders only, no implementation)

- `shared/` platform contract placeholders: `types/`, `errors/`, `contracts/`,
  `security/`, `logging/`, `events/`, `validation/`.
- `backend/fortress-identity/` — Fortress Identity (Zaqen) placeholder structure
  (`crates/`, `apps/`, `migrations/`, `docs/`).
- `backend/fortress-enterprise/` — Fortress Enterprise placeholder.
- `tests/unit/` — the unit-test category required by the testing strategy.
- `docs/decisions/` with `ADR-001` … `ADR-004` placeholders and the ADR template.
- `docs/security/` and `docs/protocols/` documentation indexes.
- `docs/architecture/REPOSITORY_STRUCTURE.md` — the authoritative layout, the
  mapping to the Fortress ecosystem, and the structural rules.
- Component READMEs with responsibility, boundaries and honest status for
  Fortress Cloud, Fortress Identity, Fortress Enterprise, Fortress Mobile,
  Fortress Admin, Fortress Mail, shared, database, infrastructure, scripts and
  tests.
- `.gitattributes` and `.editorconfig`.

### Changed

- `.gitignore` rewritten. It previously excluded first-party source and
  documentation (`/docs`, `/mail`, `/database`, `/infrastructure`, `/admin`,
  `/android`, `/packages`), which left the majority of the platform untracked.
  It now excludes only secrets, dependencies, build output, logs, editor and
  machine-specific files.
- `.gitignore` duplicate entries and a machine-specific absolute path removed.

### Removed

- `packages/` — redundant with the mandated `shared/` directory; it contained
  only empty placeholders and no functionality.
- `..gitignore.swp` — stray editor swap file.

### Notes

- No source code, build tooling, database schema, or tests exist yet.
- AfOS Android remains a separate repository; this repository defines
  integration interfaces only.
