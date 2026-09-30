# Architecture Decision Records

**Status: PLANNED** — records are placeholders. No decision has been ratified.

Each ADR is immutable once accepted. Superseding a decision creates a new ADR
that references the one it replaces.

## Index

| ADR     | Title                                             | Status   |
| ------- | ------------------------------------------------- | -------- |
| ADR-001 | Rust as the authentication core                    | PLANNED  |
| ADR-002 | WebAuthn/FIDO2 as primary authentication mechanism  | PLANNED  |
| ADR-003 | No centralized raw biometric storage               | PLANNED  |
| ADR-004 | API-first architecture                             | PLANNED  |
| ADR-005 | OAuth 2.0 / OIDC federation                        | PLANNED  |
| ADR-006 | Hardware authenticator is optional                 | PLANNED  |

ADR-001 to ADR-004 are the initial required set. ADR-005 and
ADR-006 are listed there as well and are included for completeness.

## Template

```text
# ADR-NNN — Title

Status:      PROPOSED | ACCEPTED | SUPERSEDED BY ADR-NNN
Date:        YYYY-MM-DD
Deciders:    <names/roles>
Scope:       <what this decision covers>

## Context
<the forces and constraints>

## Decision
<what was decided>

## Consequences
<positive and negative consequences>

## Alternatives considered
<what was rejected and why>

## Security review
<security implications, threat model delta>
```

No ADR may claim a security property that has not been demonstrated
.
