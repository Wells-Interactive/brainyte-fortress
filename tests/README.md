# Tests

**Status: PLANNED** — no test suites exist yet. The repository currently
contains no executable code and therefore no tests.

The testing foundation is part of the current mission. No
functionality may be marked complete because it merely compiles.

## Categories

Progression, from smallest to largest scope:

```text
Unit  →  Integration  →  Security  →  End-to-End
```

| Directory        | Scope                                                        |
| ---------------- | ------------------------------------------------------------ |
| `unit/`          | Pure functions: identity primitives, validation, error models |
| `integration/`   | Service boundaries, persistence, contract compatibility       |
| `security/`      | Authentication failure, authorization failure, tenant isolation, secret leakage |
| `api/`           | Public API contract conformance, versioning, error envelopes  |
| `android/`       | Fortress Mobile application logic and AfOS integration boundary |
| `end-to-end/`    | Cross-service flows                                           |

## Mandatory coverage for any new functionality

- normal behaviour;
- invalid input;
- authentication failure;
- authorization failure;
- missing data;
- malformed requests;
- service failure;
- boundary conditions;
- security-sensitive operations.

Security-sensitive code must include tests. Tenant isolation and
authentication/authorization failure paths are non-negotiable.

## Constraints

- Tests must never require real credentials, real devices, or production secrets.
- Tests must assert that secrets, tokens and personal data do not appear in
  errors or logs.
- No test may be marked passing without having actually been executed.
