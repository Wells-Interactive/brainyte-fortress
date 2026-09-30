# ADR-004 — API-first architecture

**Status: PLANNED (PROPOSED)** — not ratified. No implementation exists.

## Scope

How services and third-party applications integrate with the Fortress platform.

## Context

An API-first platform is required: a third-party application must be
able to integrate without understanding the internal authentication
implementation. Every public API is required to have an explicit
contract covering endpoint, request format, response format, authentication,
authorization, error behaviour, version, rate/abuse considerations, and audit
requirements.

The integration model also requires that the third-party application retains its
own business data and permissions — Fortress supplies authentication and
identity infrastructure only, and never assumes control of a third-party account.

## Decision

*Unresolved — placeholder.* The direction is recorded as a
current product decision (architecture: API-first).

## Consequences

- Integration points are versioned and independently testable.
- Contracts live in `shared/contracts/` and are published as
  `docs/api/openapi.yaml`.
- Internal implementation may change without breaking an integrated client;
  breaking changes require an explicit versioning strategy.

## Security review

Must define tenant isolation, rate limiting, input validation, structured errors,
and what is deliberately *not* exposed in responses (no stack traces, no internal
exception detail, no account-existence disclosure where inappropriate).
