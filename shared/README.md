# Shared Platform

**Status: PLANNED** — placeholder structure only.

Reusable, service-independent platform functionality lives here. Every Fortress
service may depend on `shared/`; `shared/` must never depend on a service.

Required rule: **do not place service-specific business logic
in `shared/`.** If a contract is only meaningful to one service, it belongs with
that service.

| Directory        | Responsibility                                        |
| ---------------- | ----------------------------------------------------- |
| `types/`         | Shared data types and value objects                    |
| `errors/`        | Shared, stable, machine-readable error models         |
| `contracts/`     | Public API contracts (request/response/event schemas)  |
| `security/`      | Security primitives (hashing, token, redaction, ids)  |
| `logging/`       | Logging interfaces and structured log event shapes     |
| `events/`        | Event/message structures exchanged between services    |
| `validation/`    | Common input validation primitives                    |

## Boundaries

- No secrets, no credentials, no environment access in `shared/`.
- No network calls, no database access, no framework coupling.
- `shared/` is the only place cross-service primitives may be defined, so that
  duplicated security logic is prevented.
- Tests for `shared/` components live in `tests/unit/` and `tests/security/`.

## Not yet decided

- Language and packaging format for shared contracts.
- Whether contracts are schema-first (OpenAPI/JSON Schema) or code-first.
