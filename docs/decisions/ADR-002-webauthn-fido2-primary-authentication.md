# ADR-002 — WebAuthn/FIDO2 as the primary authentication mechanism

**Status: PLANNED (PROPOSED)** — not ratified. No implementation exists.

## Scope

The primary authentication mechanism for Fortress Identity and, by extension,
for Fortress Cloud sessions and Fortress Mobile sign-in.

## Context

Standards-first authentication is required, and inventing
proprietary authentication protocols where an established standard applies.
WebAuthn / FIDO2 / passkeys provide phishing-resistant, cryptographic
authentication using hardware-backed keys.

The Fortress Identity design constraint is that Identity receives
**cryptographic proof**, never raw biometric data.

## Decision

*Unresolved — placeholder.* The direction is stated as a
current product decision (primary authentication: WebAuthn/FIDO2/passkeys);
this ADR exists to record the reasoning and the rejected alternatives.

## Alternatives considered

- Password-only authentication — rejected: not phishing-resistant.
- Server-side biometric matching — rejected: requires centrally stored raw
  biometric data, forbidden by ADR-003.
- SMS or phone-number OTP — rejected: phone-number-based
  recovery as the foundation.

## Security review

Must address replay attacks, challenge reuse, origin and RP-ID validation,
credential substitution, and enumeration resistance.
