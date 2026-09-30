# API Architecture

**Status: PLANNED** — no endpoint is implemented. The contract below defines the
rules that every future endpoint must satisfy.

Machine-readable contract: [`docs/api/openapi.yaml`](../api/openapi.yaml)
(`paths` is intentionally empty until endpoints are implemented).

## Versioning

- Base path: `/api/v1/`
- Versioning is part of the URL path, not a header, so that a version is visible
  in logs, traces and client configuration.
- Breaking changes require a new major version. An existing version is never
  altered in place.
- Additive, backward-compatible changes may be added to a minor version.
- Fortress Identity's own API families (`/v1/auth`, `/v1/users`, `/v1/devices`,
  `/v1/credentials`, `/v1/passkeys`, `/v1/sessions`, `/v1/recovery`,
  `/v1/oauth`, `/v1/oidc`, `/v1/clients`, `/v1/organizations`, `/v1/audit`,
  `/v1/risk`) are owned by `backend/fortress-identity/` and versioned
  independently.

## Response envelope

```json
{
  "success": true,
  "data": {},
  "error": null,
  "meta": { "request_id": "uuid", "timestamp": "ISO-8601" }
}
```

On failure:

```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "AUTHENTICATION_FAILED",
    "message": "Authentication could not be completed.",
    "details": []
  },
  "meta": { "request_id": "uuid", "timestamp": "ISO-8601" }
}
```

Rules:

- `error.code` is a **stable machine-readable** identifier. `error.message` is for
  humans and may change; clients branch on `code`, never on `message`.
- Error bodies never contain passwords, tokens, private keys, internal secrets,
  database details, stack traces or internal exception text.
- `meta.request_id` is present on **every** request, including errors, and is
  the correlation key between client reports, application logs and audit records.

## Mandatory properties of every public endpoint

Each endpoint must document and satisfy all of the following:

| Property              | Requirement                                                        |
| --------------------- | ------------------------------------------------------------------ |
| Endpoint / interface  | Declared path or interface, with no undocumented endpoints          |
| Request format        | Schema, with all fields validated                                  |
| Response format       | Envelope above, including the error case                           |
| Authentication        | Stated explicitly; unauthenticated endpoints are the exception      |
| Authorization         | Stated explicitly; every privileged operation is authorized         |
| Error behaviour       | Stable codes, correct HTTP status, no internal detail leaked       |
| Version               | Path version, with a stated compatibility policy                   |
| Rate / abuse          | Rate limit and abuse-control behaviour defined                     |
| Audit                 | Which audit events the operation emits                             |
| Idempotency           | Idempotency key required for commands and sensitive writes          |

## Additional rules

- HTTPS everywhere. TLS verification is never disabled in production.
- Bearer authentication for authenticated calls; short-lived access tokens with
  refresh-token rotation.
- Pagination on every list endpoint; no unbounded result sets.
- Explicit timeout behaviour on every outbound call.
- Webhooks are signed and validated for signature, timestamp and replay.
- Responses do not disclose whether an account exists where that would enable
  enumeration.
- No excessive data exposure: responses return only fields the caller needs.

## Planned API domains

`auth`, `users`, `identity`, `devices`, `device-sessions`, `device-status`,
`locations`, `security-events`, `tamper-events`, `calls`, `sms`, `ussd`,
`contacts`, `policies`, `commands`, `organizations`, `departments`, `admin`,
`mail`, `reports`, `audit`, `licensing`, `webhooks`.

These are **planned** domains. None is implemented or contracted.
