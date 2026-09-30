# Fortress Identity (codename **Zaqen**)

**Status: PLANNED** — placeholder structure only.

Fortress Identity is the identity foundation of the Brainyte Fortress ecosystem.
It is the authority for *who a subject is*, *whether they proved it*, and *what
they may do*.

Authoritative specification: `ZAQEN.md` (repository root).

## Product boundary

- Standards-based, API-first authentication and identity infrastructure.
- Primary mechanism: WebAuthn / FIDO2 / passkeys.
- Cryptographic proof is received; **raw biometric data is not centrally stored**.
- Federation via OAuth 2.0 / OpenID Connect.
- Tenant and application boundaries are enforced server-side, never by the client.

## Structure (placeholder)

```text
backend/fortress-identity/
├── crates/      # Zaqen library crates (zaqen-core, zaqen-identity, zaqen-auth,
│                # zaqen-authorization, zaqen-federation, zaqen-sessions,
│                # zaqen-recovery, zaqen-risk, zaqen-audit, zaqen-db,
│                # zaqen-crypto, zaqen-api)
├── apps/        # zaqen-server, zaqen-worker
├── migrations/  # PostgreSQL schema migrations
└── docs/        # identity-specific design notes
```

Do not create a crate until it has a defined responsibility and an owner

## Boundaries

- Fortress Cloud and Fortress Admin consume Identity through API contracts only.
- No administrative authorization decisions are owned here; Identity supplies
  the subject and its claims.
- No AfOS code. AfOS is a separate repository and an integration boundary only.
- Secrets are never stored here and never committed.

## Language

- Rust
