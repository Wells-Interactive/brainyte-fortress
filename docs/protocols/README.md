# Protocols

**Status: PLANNED** — no protocol is implemented yet.

This directory records the wire protocols and protocol-adjacent contracts the
Fortress platform depends on. Established standards are used; proprietary
protocols are not invented where a standard applies.

## Planned documents

| Document             | Protocol / contract                                | Status   |
| -------------------- | ------------------------------------------------- | -------- |
| `webauthn.md`        | WebAuthn / FIDO2 registration and assertion flows  | PLANNED  |
| `oauth2.md`          | OAuth 2.0 authorization code and token flows        | PLANNED  |
| `oidc.md`            | OpenID Connect federation                          | PLANNED  |
| `remote_commands.md` | Remote command envelope: id, expiry, signature, replay protection, single execution | PLANNED  |
| `webhooks.md`        | Webhook signature, timestamp and replay validation | PLANNED  |
| `api_envelope.md`    | `/api/v1/` request and response envelope           | PLANNED  |
| `afos_integration.md`| AfOS Android integration interface (boundary only) | PLANNED  |

## Rules

- Cryptographic operations use maintained libraries; primitives are never
  implemented manually.
- Tokens are generated with a cryptographically secure random source.
- Every protocol document must state its replay, downgrade and enumeration
  protections, and must have negative tests for each.
- Documented behaviour must match implemented behaviour. Where the two differ,
  the documentation is wrong and must be corrected before implementation.
