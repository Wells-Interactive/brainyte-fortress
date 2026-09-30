# Security Documentation

**Status: PLANNED** — no implemented security control is documented here yet.

The repository contains **no implemented security functionality**. Nothing in this
directory may be read as a claim that a security property has been achieved.

## Planned documents

| Document                 | Covers                                                        | Status   |
| ------------------------ | ------------------------------------------------------------- | -------- |
| `THREAT_MODEL.md`        | Primary threats and required mitigations                       | PLANNED  |
| `AUTHENTICATION.md`      | Authentication flows, assurance levels, failure handling       | PLANNED  |
| `AUTHORIZATION.md`       | Roles, scopes, policy evaluation, admin authorization          | PLANNED  |
| `SESSION_SECURITY.md`    | Token lifetime, rotation, revocation, concurrent sessions      | PLANNED  |
| `TENANT_ISOLATION.md`    | Cross-tenant boundaries and the tests that prove them          | PLANNED  |
| `SECRET_MANAGEMENT.md`   | How secrets are provisioned, rotated and never committed       | PLANNED  |
| `CRYPTOGRAPHY.md`        | Every cryptographic decision, with library and rationale       | PLANNED  |
| `DATA_PROTECTION.md`     | Sensitive data classes, purposes, retention, encryption       | PLANNED  |
| `INCIDENT_RESPONSE.md`   | Detection, containment, and audit-record use                   | PLANNED  |

## Mandatory rules that apply from the first commit

- No plaintext passwords, tokens, private keys, API keys or production
  certificates in source control.
- No hard-coded authentication secrets; secrets come from a secret manager.
- Input is validated at every trust boundary.
- Authentication precedes every privileged operation; authorization precedes
  every privileged operation.
- Security-relevant events are audited; secrets are never written to logs.
- Sensitive data is protected in transit and, where required, at rest.
- Tenant isolation, authentication failure paths and authorization failure paths
  are tested.

## Status vocabulary

```text
UNKNOWN  →  PLANNED  →  IN DEVELOPMENT  →  IMPLEMENTED  →  TESTED  →  VERIFIED
```

A property is not `VERIFIED` without evidence.
