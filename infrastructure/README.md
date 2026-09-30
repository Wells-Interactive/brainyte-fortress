# Infrastructure

**Status: PLANNED** — placeholders only. Nothing here is deployable.

Reproducible, private-by-default infrastructure for Fortress Cloud, Fortress
Admin and Fortress Mail.

| Directory      | Responsibility                                              |
| -------------- | ----------------------------------------------------------- |
| `docker/`      | Reproducible local and CI service definitions               |
| `nginx/`       | Reverse proxy and TLS termination configuration             |
| `firewall/`    | Network segmentation and egress policy                      |
| `monitoring/`  | Uptime checks, metrics, alerting                            |
| `logging/`     | Centralized application and security log shipping            |
| `secrets/`     | Secret *references* only — never secret material            |
| `backups/`     | Encrypted backup jobs and restore verification              |
| `terraform/`   | Infrastructure-as-code for repeatable environments         |

## Rules

- HTTPS everywhere. The database is never exposed to the public internet.
- Secrets are injected from a secret manager at runtime. `secrets/` contains
  templates and references, never values; `.gitignore` blocks secret material.
- No infrastructure is introduced for appearance. Kubernetes is not used unless
  operational scale justifies it.
- Production configuration is never stored in this repository.

See also `docker-compose.yml` and `.env.example` at the repository root.
