# Repository Structure

**Status: PLANNED** — the structure below is a scaffold of placeholders. There
is no implementation, no build tooling, and no test suite in this repository yet.

Sources of truth for this layout: `INSTRUCTIONS.md`, `ZAQEN.md`, and
`Brainyte_Fortress_Complete_Architecture.odt`.

## Layout

```text
brainyte-fortress/
├── .env.example                  # configuration placeholders only, never secrets
├── .editorconfig
├── .gitattributes
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── INSTRUCTIONS.md               # development directives (owner-internal)
├── LICENSE.md
├── PRIVACY.md
├── README.md
├── SECURITY.md
├── THREAT_MODEL.md
├── ZAQEN.md                      # Fortress Identity specification (owner-internal)
├── Brainyte_Fortress_Complete_Architecture.odt
├── docker-compose.yml
│
├── assets/                       # repository assets (branding, media)
│
├── shared/                       # shared platform contracts
│   ├── types/                    #   shared data types
│   ├── errors/                   #   shared, stable error models
│   ├── contracts/                #   public API contracts
│   ├── security/                 #   security primitives
│   ├── logging/                  #   logging interfaces
│   ├── events/                   #   event structures
│   └── validation/               #   common validation
│
├── backend/                      # server-side Fortress services
│   ├── fortress-api/             #   Fortress Cloud — backend control plane
│   ├── fortress-identity/        #   Fortress Identity (Zaqen) — identity core
│   └── fortress-enterprise/      #   Fortress Enterprise — tenant capabilities
│
├── admin/
│   └── fortress-admin/           # Fortress Admin — administrative portal
│
├── android/
│   └── fortress/                 # Fortress Mobile — Android application
│
├── mail/                         # Fortress Mail — integration boundary only
│   ├── gateway/  smtp/  imap/  spam/  malware/  dkim/  storage/  administration/
│
├── database/                     # PostgreSQL migrations, seeders, functions, policies
│   ├── migrations/  seeders/  functions/  policies/
│
├── infrastructure/               # docker, nginx, firewall, monitoring, logging,
│                                 # secrets, backups, terraform
│
├── docs/
│   ├── architecture/             # system, api, identity, security, mail, AfOS
│   ├── api/                      # OpenAPI contract
│   ├── decisions/                # ADRs
│   ├── protocols/                # wire protocol contracts
│   ├── security/                 # security documentation
│   ├── android/                  # Android / AfOS integration notes
│   ├── deployment/               # deployment documentation
│   └── product/                  # PRD, features, flows, roadmap
│
├── scripts/                      # setup, development, security, deployment
│
└── tests/                        # unit, integration, security, API, Android, e2e
```

## Mapping to the Fortress ecosystem

| Fortress component    | Location                       | Notes                     |
| --------------------- | ------------------------------ | ------------------------- |
| Fortress Mobile       | `android/fortress/`            | Android application       |
| Fortress Cloud        | `backend/fortress-api/`        | Backend control plane     |
| Fortress Identity     | `backend/fortress-identity/`   | Identity core (Zaqen)     |
| Fortress Admin        | `admin/fortress-admin/`        | Administrative portal     |
| Fortress Mail         | `mail/`                        | Integration boundary only |
| Fortress Enterprise   | `backend/fortress-enterprise/` | Tenant capabilities       |
| Shared platform       | `shared/`                      | Platform-wide contracts   |
| AfOS Android          | *separate repository*          | Not part of this repository |

## AfOS boundary

AfOS Android is maintained in a separate repository
(`Wells-Interactive/brainyte-AfOS`). This repository defines **integration
interfaces only**. It contains no AOSP source, no duplicated AfOS
implementation, and no assumptions about undocumented AfOS internals.

```text
Brainyte Fortress  →  AfOS Integration Layer  →  AfOS Android
```

## Structural rules

1. A directory is created only when implementation requires it. Placeholder
   directories are not created for appearance.
2. `shared/` must not contain service-specific business logic.
3. Every service depends on `shared/`; `shared/` depends on no service.
4. A table, an event, and a contract each have exactly one owning service.
5. No service-to-service circular dependencies.
6. Cross-service access happens through contracts, not shared schemas.

## Change log

| Change                                                       | Reason                                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------------------------- |
| Added `shared/`                                              | The shared platform is a required top-level area; the previous `packages/` directory duplicated the same intent under a second name |
| Removed `packages/`                                          | Redundant with `shared/`; contained only empty placeholders             |
| Added `backend/fortress-identity/`                           | Fortress Identity previously had no location                            |
| Added `backend/fortress-enterprise/`                         | Fortress Enterprise previously had no location                          |
| Added `docs/decisions/`, `docs/security/`, `docs/protocols/` | Required for ADRs, security documentation and protocol contracts        |
| Added `tests/unit/`                                          | The testing strategy requires a unit-test category                      |
| Un-ignored `docs/`, `mail/`, `database/`, `infrastructure/`, `admin/`, `android/` | The previous `.gitignore` excluded first-party source and documentation |
