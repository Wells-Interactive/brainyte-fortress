# Scripts

**Status: PLANNED** — no scripts exist yet.

| Directory      | Responsibility                                     |
| -------------- | -------------------------------------------------- |
| `setup/`       | First-run environment and dependency bootstrap       |
| `development/` | Local development helpers                           |
| `security/`    | Security checks: secret scanning, dependency audit  |
| `deployment/`  | Deployment and verification automation              |

## Rules

- Scripts are idempotent and safe to re-run.
- Scripts accept no production secrets as arguments; they read them from the
  environment.
- A script that touches a remote system states what it changes and how to
  reverse it, and defaults to dry-run.
- Formatting and linting entry points belong here so that CI and local
  development run identical commands.
