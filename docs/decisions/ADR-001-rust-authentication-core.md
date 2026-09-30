# ADR-001 — Rust as the authentication core

**Status: PLANNED (PROPOSED)** — not ratified. No implementation exists.

## Scope

The implementation language of the security-critical identity core
(Fortress Identity / Zaqen, see `backend/fortress-identity/`).

## Context

The Fortress Identity specification directs that Rust be used for the core
authentication and security-sensitive backend because of memory safety, strong
concurrency, control-level expressiveness and a mature cryptographic ecosystem.

A competing directive exists in the architecture document, which describes
Fortress Cloud as a Laravel/PHP API. The two are not necessarily in conflict,
but the boundary between them has not been drawn.

## Open decision required

Which responsibilities belong to the Rust identity core and which belong to the
Fortress Cloud services, and whether any service is implemented in both
languages. This must be settled before implementation begins; `ZAQEN.md`
requires that a materially architectural ambiguity be raised rather than
guessed.

## Decision

*Unresolved — placeholder.*

## Consequences

*Unresolved.*

## Security review

A decision here determines where authentication secrets are handled and which
toolchain is trusted for cryptographic operations. It must be reviewed as a
security decision, not a productivity decision.
