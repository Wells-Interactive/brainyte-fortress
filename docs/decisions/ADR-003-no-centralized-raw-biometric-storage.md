# ADR-003 — No centralized raw biometric storage

**Status: PLANNED (PROPOSED)** — not ratified. No implementation exists.

## Scope

What Fortress Identity stores when a user authenticates with a face, fingerprint
or other biometric.

## Context

The Fortress Identity specification states the critical biometric rule:
Zaqen must not be built around collecting or centrally storing raw
fingerprints, raw Face ID data, or raw facial images. The intended flow is:

```text
biometric
  → trusted device secure hardware
  → private cryptographic key
  → WebAuthn/FIDO2 assertion
  → cryptographic authentication result
```

The platform rules additionally classify biometric and identity data as
sensitive by default, and requires that no unnecessary data be retained.

## Decision

*Unresolved — placeholder.* The direction is recorded as a current product
product decision ("raw centralized biometrics: not part of the normal
architecture").

## Consequences

- Identity verification that genuinely requires document or image capture (for
  example KYC liveness and face match) is a **separate** flow from sign-in, and
  must go through a provider abstraction rather than the authentication path.
- Any retained document or image requires private encrypted object storage,
  strict access control, a retention period, and audit logging.

## Security review

This is the platform's principal privacy boundary. It also constrains incident
response: a breach must not expose biometric data.
