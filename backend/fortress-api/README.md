# Fortress Cloud

**Status: PLANNED** — placeholder only..

Fortress Cloud is the backend control plane used by Fortress clients and by
Fortress Admin. It owns policies, remote commands, device registration, and the
audit pipeline.

Reference: `Brainyte_Fortress_Complete_Architecture.odt`.

## Responsibilities (to be defined)

- Cloud service architecture and service-to-service interfaces.
- API versioning and the request/response envelope contract.
- Error handling and structured error behaviour.
- Event and message contracts.
- Persistence boundaries.
- Logging and audit boundaries.
- The first minimal service, then automated tests.

## Planned API surface

Versioned under `/api/v1/`. Domains listed in the architecture document:
`auth`, `users`, `identity`, `devices`, `device-sessions`, `device-status`,
`locations`, `security-events`, `tamper-events`, `calls`, `sms`, `ussd`,
`contacts`, `policies`, `commands`, `organizations`, `departments`, `admin`,
`mail`, `reports`, `audit`, `licensing`, `webhooks`.

Only the contract is defined here. **No endpoint is implemented.** The canonical
machine-readable contract is `docs/api/openapi.yaml`.

## Remote command security (design constraint, not yet implemented)

```text
admin authenticates
    → RBAC authorization
    → policy validation
    → command created with unique id, expiry and signature
    → device verifies authenticity and policy/state
    → execute exactly once (replay-protected)
    → result returned
    → audit event persisted
```

## Boundaries

- Authentication and session issuance are owned by Fortress Identity. Fortress
  Cloud consumes Identity's contracts; it does not re-implement authentication.
- Fortress Mobile and Fortress Admin are clients of this API, never peers.
- No AfOS code.
- Each service here must remain independently testable and must not grow into a
  monolith of unrelated functionality.

## Not yet decided

- Framework (the architecture document names Laravel/PHP; ZAQEN.md names Rust for
  the Identity core). The split of responsibilities between the two is recorded
  as an open decision and must be settled before implementation begins.
- Async/event transport.
- API gateway and rate-limiting implementation.
