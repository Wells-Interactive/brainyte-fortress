# Brainyte Fortress 

## 1. Project Identity

Project: Brainyte Fortress

Tagline: Your Phone. Your Fortress.

Operating system: **AfOS Android™ — Fortress Operating System**

Brainyte Fortress is a secure-device platform consisting of:

- Fortress Mobile — standard Android application
- Fortress Cloud — secure backend/API
- Fortress Admin — administration and fleet-management portal
- Fortress Mail — owned secure email service
- Fortress Identity — identity verification, liveness and face matching
- Fortress Enterprise — Android Device Owner / managed-device capabilities
- AfOS Android™ — hardened Android/AOSP operating system

Do not rename these components without explicit instruction.

The old generic term "Fortress OS" must not be used in new documentation. Use **AfOS Android™ — Fortress Operating System**.

---

## 2. Mission

Build a layered security platform that can begin on ordinary Android devices and progressively move enforcement into Android Enterprise and ultimately into AfOS Android™.

The implementation must never pretend that an ordinary Android application has privileges that Android does not provide.

The architecture must support:

1. Standard Android protection
2. Managed/Device Owner protection
3. AfOS Android™ system-level enforcement

---

## 3. Primary Repository

Repository:

    brainyte-fortress

Recommended package:

    com.wellsint.brainyte.fortress

Recommended API:

    https://api.fortress.wellsint.site

Recommended administration portal:

    https://portal.fortress.wellsint.site

Recommended database:

    brainyte_fortress

AfOS Android™ AOSP source should eventually live in a separate repository:

    brainyte-fortress-afos

Do NOT clone or vendor the complete AOSP source tree into this repository.

---

## 4. Core Architecture

The platform is divided into these major boundaries:

    brainyte-fortress/
    ├── android/fortress
    ├── backend/fortress-api
    ├── admin/fortress-admin
    ├── mail
    ├── infrastructure
    ├── database
    ├── packages
    ├── scripts
    ├── tests
    └── docs

AfOS Android™ is a separate system-level project.

The main repository contains the contracts, documentation, applications and services required to integrate with AfOS.

---

# 5. Non-Negotiable Security Rules

## 5.1 Never invent platform capabilities

Before implementing an Android security feature, verify whether Android exposes the required API.

If a feature cannot be guaranteed on standard Android:

- implement the strongest supported behavior;
- detect capability;
- show the limitation;
- record the security state;
- reserve stronger enforcement for Device Owner or AfOS.

Never describe a best-effort feature as guaranteed system-level blocking.

## 5.2 Never implement cryptography from scratch

Use:

- Android Keystore
- platform cryptographic APIs
- well-maintained audited libraries
- TLS
- established token standards

Never invent encryption algorithms, key derivation schemes or authentication protocols.

## 5.3 Never store production secrets in Git

Never commit:

- API keys
- database passwords
- JWT signing keys
- private keys
- certificates
- mail passwords
- identity-provider credentials
- FCM credentials
- cloud credentials

Use environment variables or a proper secret manager.

## 5.4 Least privilege

Every:

- Android permission
- backend role
- API scope
- service account
- system privilege

must have a documented reason.

Privileged Android/system applications must remain as small as practical.

## 5.5 Audit sensitive actions

The following must create auditable security events where applicable:

- authentication failures
- PIN changes
- biometric failures
- policy changes
- device enrollment
- device unenrollment
- remote commands
- remote lock
- remote wipe
- security-service changes
- SIM/security changes
- identity-verification decisions
- administrator actions
- sensitive identity-data access

---

# 6. Standard Android Capability Boundary

Fortress Mobile is NOT AfOS.

On ordinary Android, do not assume universal system-level control over:

- all outgoing calls
- all incoming calls
- all SMS
- all USSD
- SIM Toolkit
- arbitrary third-party application behavior
- uninstall prevention
- factory-reset prevention

Use Android's supported mechanisms, roles, permissions and managed-device APIs.

Where stronger guarantees are required, move the feature to:

    Device Owner / Enterprise

or ultimately:

    AfOS Android™

---

# 7. Android Technology Standards

Use:

- Kotlin
- Jetpack Compose
- AndroidX
- Room
- WorkManager
- CameraX
- BiometricPrompt
- Android Keystore
- DevicePolicyManager
- appropriate Telecom APIs
- appropriate SMS role/default-handler APIs
- FCM where appropriate

Architecture should favor:

    UI
      ↓
    ViewModel / Presentation
      ↓
    Application / Use Cases
      ↓
    Domain
      ↓
    Infrastructure
      ↓
    Android platform / API / local database

Do not put security policy decisions directly into UI components.

---

# 8. Fortress Mobile Modules

The Android project should eventually contain:

    android/fortress/
    ├── app/
    ├── core/
    ├── security/
    ├── authentication/
    ├── device/
    ├── calls/
    ├── sms/
    ├── ussd/
    ├── contacts/
    ├── identity/
    ├── liveness/
    ├── camera/
    ├── location/
    ├── intrusion/
    ├── tamper/
    ├── policy/
    ├── mail/
    ├── notifications/
    ├── remote/
    ├── database/
    └── ui/

Each module must have a clear responsibility.

Avoid giant service classes.

---

# 9. Fortress Authentication

Implement:

- Admin PIN
- configurable 4–12 digit PIN
- secure PIN storage
- biometric authentication
- authentication timeout
- failed-attempt tracking
- configurable lockout
- secure session state

Never store the raw PIN.

Prefer a strong password/PIN hashing approach suitable for the platform.

Use hardware-backed keys where possible.

---

# 10. Intruder Protection

After configurable failed authentication attempts:

1. Register a security event.
2. Capture an intruder image where technically and legally permitted.
3. Record timestamp.
4. Record device information.
5. Record location only if permitted and available.
6. Encrypt/store the evidence appropriately.
7. Queue an alert.
8. Synchronize with Fortress Cloud when online.

Do not capture camera data silently outside the product's disclosed security workflow.

---

# 11. Call Control

Required policy concepts:

- incoming allowed
- incoming restricted
- approved contacts
- blocked contacts
- outgoing authorization required
- outgoing blocked
- unknown number blocked
- international restriction
- premium-rate restriction where supported

All decisions must go through the policy layer.

Do not put hard-coded phone-number rules into UI code.

Call attempts should be auditable.

---

# 12. SMS Control

Support:

- incoming SMS protection
- protected message viewing
- hidden previews
- approved senders
- blocked senders
- outgoing authorization
- approved recipients
- outgoing blocking
- SMS audit events

Use Android SMS role/default-handler mechanisms where required.

AfOS may provide stronger system-level control.

---

# 13. USSD

USSD support must be capability-driven.

The application must:

- detect supported behavior;
- block/prevent where Android/device capabilities permit;
- restrict use through Fortress's controlled dialer where possible;
- log observable attempts.

AfOS is the target for stronger USSD/SIM Toolkit enforcement.

---

# 14. Contact Policy

Contacts support:

- create
- edit
- delete
- import
- search
- family category
- emergency category
- business category
- whitelist
- blacklist

Do not use raw phone numbers as public identifiers in logs.

Where appropriate, use normalized values and hashes/references.

---

# 15. Location

Support:

- current location
- last-known location
- history
- reporting interval
- battery state
- network state
- timestamp
- remote locate

Location is sensitive data.

Implement:

- explicit policy
- secure transport
- access control
- retention controls
- audit access

Do not collect location continuously without a valid product/security purpose.

---

# 16. Tamper Detection

Potential signals:

- repeated failed authentication
- SIM change/removal where available
- reboot/security events
- protection-stop attempts
- admin privilege changes
- Device Owner changes
- Developer Options changes
- USB debugging changes
- unknown APK installation
- factory-reset/bypass attempts where supported

Treat device signals as evidence, not assumptions.

---

# 17. Policy Engine

All security decisions should eventually flow through a normalized policy engine.

Example:

    {
      "incoming_calls": "allow",
      "outgoing_calls": "authorization_required",
      "incoming_sms": "allow",
      "outgoing_sms": "authorization_required",
      "ussd": "block",
      "unknown_contacts": "block",
      "gps": "required",
      "developer_options": "block",
      "usb_debugging": "block",
      "unknown_apps": "block"
    }

Policies require:

- unique ID
- version
- status
- created timestamp
- published timestamp
- audit record

Published versions should be immutable.

---

# 18. Remote Command Security

Remote commands must follow:

    Administrator
       ↓
    Authentication
       ↓
    Authorization/RBAC
       ↓
    Policy validation
       ↓
    Command creation
       ↓
    Unique command ID
       ↓
    Expiration
       ↓
    Authentication/signature
       ↓
    Device delivery
       ↓
    Device verification
       ↓
    Device policy check
       ↓
    Execute once
       ↓
    Result
       ↓
    Audit

Commands must be:

- authenticated
- authorized
- unique
- time-limited
- replay-protected
- idempotent where appropriate
- auditable

---

# 19. Fortress Cloud

Backend:

- PHP 8.3+
- Laravel
- PostgreSQL
- Redis
- queues
- object storage
- FCM integration where appropriate

Backend domains:

    Identity
    Devices
    Security
    Communications
    Policies
    Organizations
    Mail
    Licensing
    Audit

Use domain-oriented organization rather than putting everything into generic controllers.

---

# 20. API Standards

Base:

    /api/v1/

Response:

    {
      "success": true,
      "data": {},
      "error": null,
      "meta": {
        "request_id": "uuid",
        "timestamp": "ISO-8601"
      }
    }

Every API request should have a request ID.

Use:

- validation
- pagination
- rate limiting
- authorization
- structured errors
- idempotency for sensitive writes
- webhook verification
- API versioning

---

# 21. Database Standards

Primary database:

    PostgreSQL

Database name:

    brainyte_fortress

Major entities include:

    users
    user_profiles
    identity_verifications
    identity_documents
    liveness_checks
    face_matches
    verification_attempts
    verification_events

    devices
    device_installations
    device_sessions
    device_tokens
    device_policies
    device_status
    device_locations
    device_security_events
    device_tamper_events

    call_logs
    call_attempts
    sms_logs
    sms_attempts
    ussd_attempts

    contacts
    contact_whitelists
    contact_blacklists

    mail_accounts
    mailboxes
    email_messages
    email_threads
    email_attachments
    email_rules
    email_contacts
    email_security_events

    administrators
    roles
    permissions
    organizations
    departments
    organization_devices
    organization_users
    policies
    policy_assignments
    audit_logs

Use UUIDs where externally exposed identifiers are needed.

Use foreign keys, indexes, constraints and appropriate transaction boundaries.

---

# 22. Identity Verification

Create an internal interface such as:

    IdentityProvider

Provider adapters may include:

    DiditProvider
    SumsubProvider

The domain layer must not depend directly on vendor SDK classes.

Workflow:

    Registration
      ↓
    Email verification
      ↓
    Phone verification
      ↓
    Identity verification
      ↓
    Document verification
      ↓
    Selfie
      ↓
    Liveness
      ↓
    Face match
      ↓
    Provider decision
      ↓
    Fortress decision
      ↓
    Account activation

Do not build proprietary KYC/liveness AI in the first implementation.

Do not retain raw biometric data unless there is a documented reason.

---

# 23. Fortress Mail

Fortress Mail is an owned email service.

Example:

    user@fortress.brainyte.com

Use mature mail infrastructure:

- Postfix
- Dovecot
- Rspamd
- ClamAV
- DKIM
- SPF
- DMARC
- TLS

Never implement SMTP or IMAP from scratch.

Features:

- inbox
- sent
- drafts
- archive
- spam
- trash
- threads
- search
- contacts
- attachments
- mailbox settings
- security alerts
- administrative management

Mail infrastructure should be isolated from the main API/database network where practical.

---

# 24. Object Storage

Use private object storage for:

- identity documents
- verification evidence
- intruder images
- email attachments
- reports
- backups

Requirements:

- encryption at rest
- private buckets
- access controls
- signed URLs
- retention rules
- access logging

Do not expose raw object-storage URLs publicly.

---

# 25. Fortress Admin

Admin areas:

    Dashboard
    Devices
    Users
    Organizations
    Departments
    Policies
    Identity
    Security
    Calls
    SMS
    USSD
    Locations
    Mail
    Reports
    Audit
    Licensing
    Settings

Every administrative action must respect RBAC.

---

# 26. Roles

Initial roles may include:

- Super Administrator
- Organization Administrator
- Security Administrator
- Device Administrator
- Identity Administrator
- Mail Administrator
- Auditor
- Read-only Administrator

Do not assume every administrator can access identity documents or security evidence.

Sensitive permissions must be separate.

---

# 27. Organizations

Support:

- organizations
- departments
- users
- devices
- groups
- policies
- roles
- reports

An organization must not be able to access another organization's data.

Tenant isolation is mandatory.

---

# 28. Licensing

Support:

- device activation
- license validation
- subscription status
- device limits
- trials
- feature entitlements
- Personal
- Family
- Business
- Enterprise
- AfOS

Licensing must be designed so security-critical device state does not become permanently unusable because of a temporary network outage.

---

# 29. AfOS Android™

AfOS Android™ is the hardened Android/AOSP operating system.

Expected system layers:

    AOSP
      ↓
    AfOS Framework
      ↓
    Fortress Security Services
      ↓
    Fortress Policy Engine
      ↓
    Fortress System Applications
      ↓
    Hardware / Vendor / Modem

Expected privileged applications:

    FortressSecurity
    FortressDialer
    FortressMessages
    FortressMail
    FortressIdentity
    FortressSettings
    FortressManagement

AfOS may enforce:

- system-level authentication
- calls
- SMS
- USSD
- SIM Toolkit restrictions
- Settings restrictions
- Developer Options restrictions
- USB debugging restrictions
- APK installation restrictions
- kiosk
- remote management
- remote wipe
- application restrictions
- security auditing

Actual capabilities depend on target hardware, Android release, vendor components, modem and boot chain.

---

# 30. AfOS Security

Target:

- Android Verified Boot
- hardware-backed keys
- Android Keystore
- SELinux
- secure boot chain
- restricted recovery
- controlled bootloader
- controlled debugging
- hardened system settings
- signed system applications
- OTA update verification

Never claim bypass resistance without testing the complete boot chain on actual target hardware.

---

# 31. Preinstalled Apps

AfOS may ship with:

    Fortress Security
    Fortress Dialer
    Fortress Messages
    Fortress Mail
    Fortress Identity
    Fortress Management
    Fortress Settings

Optional approved applications:

    Browser
    Camera
    Gallery
    Files
    Clock
    Calculator

System apps must be signed and granted only the privileges they require.

---

# 32. Repository Structure

Maintain:

    docs/
    android/
    backend/
    admin/
    mail/
    infrastructure/
    database/
    packages/
    scripts/
    tests/

Do not place unrelated experimental code in production modules.

Use `docs/` for architecture and implementation decisions.

---

# 33. Documentation Requirements

Every major module should have:

- README
- architecture notes
- setup instructions
- security considerations
- API documentation where applicable
- test instructions

Architecture changes must update documentation.

---

# 34. Testing Requirements

Required test categories:

    Unit
    Integration
    API
    Android
    Security
    End-to-end

Security-sensitive features require negative tests.

Examples:

- wrong PIN
- repeated PIN failure
- expired session
- revoked device
- unauthorized command
- replayed command
- invalid webhook
- unauthorized organization access
- blocked call
- blocked SMS
- blocked USSD
- tamper event
- invalid identity result

---

# 35. CI/CD

CI should perform:

1. dependency installation
2. formatting
3. lint/static analysis
4. unit tests
5. integration tests
6. security checks
7. Android tests
8. backend tests
9. build artifacts
10. protected release signing

Production signing credentials must exist only in protected CI secrets.

Because development hardware may be limited, prefer CI for heavier Android builds.

---

# 36. Git Rules

Use small commits.

Recommended commit style:

    feat:
    fix:
    security:
    docs:
    refactor:
    test:
    chore:

Never commit generated secrets or local environment files.

Never force-push shared protected branches without explicit authorization.

---

# 37. Codex Workflow

Codex must work incrementally.

Before modifying code:

1. Inspect repository.
2. Read relevant documentation.
3. Identify existing implementation.
4. Determine platform limitations.
5. Plan the smallest safe change.
6. Implement.
7. Run relevant tests.
8. Review the diff.
9. Update documentation if architecture changed.
10. Report what was changed and what remains.

Do not rewrite the entire project merely to implement one feature.

Do not delete working functionality without explicit authorization.

---

# 38. Build Order

## Milestone 0 — Foundation

Create:

- repository structure
- AGENTS.md
- documentation
- CI baseline
- development configuration
- shared contracts

## Milestone 1 — Fortress Cloud

Build:

- Laravel
- PostgreSQL
- authentication
- users
- devices
- enrollment
- security events
- audit
- policies
- remote commands

## Milestone 2 — Fortress Mobile

Build:

- Android project
- authentication
- PIN
- biometric
- device registration
- local database
- policy sync
- security events
- location
- intrusion
- tamper

## Milestone 3 — Communication Controls

Build:

- secure dialer
- call policy
- SMS policy
- USSD handling
- contact whitelist
- logs

Respect Android capability limits.

## Milestone 4 — Fortress Admin

Build:

- dashboard
- device management
- policy management
- security alerts
- location
- users
- organizations
- audit

## Milestone 5 — Fortress Identity

Build:

- provider abstraction
- verification session
- provider adapter
- webhook processing
- liveness
- face match
- verification decision

## Milestone 6 — Fortress Mail

Build:

- mailbox provisioning
- mail infrastructure integration
- mailbox UI
- attachments
- spam/malware protection
- administration

## Milestone 7 — Fortress Enterprise

Build:

- Device Owner enrollment
- kiosk
- managed configuration
- application restrictions
- USB restrictions
- developer restrictions
- compliance

## Milestone 8 — AfOS Android™

Only after selecting target hardware:

- AOSP integration
- device tree
- kernel/vendor integration
- AfOS framework
- security services
- policy engine
- privileged apps
- SELinux
- Verified Boot
- OTA
- system-level controls

---

# 39. What Codex Must Not Do

Do NOT:

- invent unavailable Android APIs;
- claim universal call blocking on standard Android;
- claim universal SMS blocking without the required role/device control;
- claim universal USSD blocking;
- create custom cryptography;
- build SMTP/IMAP from scratch;
- build a KYC provider from scratch;
- commit secrets;
- expose private object storage;
- bypass platform security mechanisms;
- implement hidden surveillance functionality;
- silently collect sensitive information;
- disable Android security mechanisms simply to make a feature work;
- modify AOSP blindly without target-device requirements;
- place a full AOSP checkout into the main application repository;
- remove tests to make builds pass;
- suppress security warnings without documenting why.

---

# 40. Definition of Done

A feature is NOT complete merely because it compiles.

A feature is complete when:

- architecture is defined;
- implementation exists;
- security implications are reviewed;
- platform limitations are documented;
- authorization is enforced;
- errors are handled;
- logs/audits exist where required;
- tests exist;
- documentation is updated;
- CI passes;
- no secrets are committed;
- the implementation does not overclaim its security guarantee.

---

# 41. First Task for Codex

When starting from this repository, Codex should NOT immediately build all features.

First execute:

    1. Inspect the repository.
    2. Read AGENTS.md.
    3. Read README.md and architecture documentation.
    4. Verify the directory structure.
    5. Create the minimum development scaffolding.
    6. Create the first CI workflow.
    7. Create the backend skeleton.
    8. Create the Android skeleton.
    9. Create the admin skeleton.
    10. Create shared API/security contracts.
    11. Run validation/tests.
    12. Report the exact files created and the next recommended milestone.

Do not proceed to full feature implementation until the foundation builds successfully.

---

# 42. Product Principle

Brainyte Fortress must be designed around one central principle:

**Security must be enforceable at the lowest practical layer.**

Fortress Mobile protects what standard Android permits.

Fortress Enterprise controls managed devices.

AfOS Android™ controls the operating system itself.

Fortress Cloud provides centralized identity, policy, command, licensing and audit.

Together these form:

    Brainyte Fortress
    Your Phone. Your Fortress.
