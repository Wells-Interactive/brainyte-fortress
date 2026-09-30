# Fortress Admin

**Status: PLANNED** — placeholder only. No implementation exists.

Fortress Admin is the administrative control surface for the Fortress ecosystem:
fleet management, identity review, security response, policy, reporting and
audit.

## Planned structure

```text
admin/fortress-admin/
├── dashboard/       # security overview
├── devices/         # device inventory and status
├── users/           # user management
├── organizations/   # organization management
├── departments/     # department hierarchy
├── policies/        # policy creation, versioning, assignment
├── identity/        # identity verification review
├── security/        # security alerts and tamper events
├── calls/           # call activity
├── sms/             # message activity
├── ussd/            # USSD activity
├── locations/       # device map and location history
├── mail/            # mail administration
├── reports/         # reporting
├── audit/           # audit trail
├── licensing/       # license and subscription administration
└── settings/        # administrative settings
```

## Authorization requirements (mandatory)

- Administrator roles and permission scopes must be defined before any screen is
  built.
- **Every privileged administrative operation must have an authorization check.**
- Administrative sessions are separately defined, separately secured, and
  separately audited.
- Every privileged action produces an audit event.
- Tenant scoping is enforced server-side for every administrative query.

## Boundaries

- Admin is a **client** of Fortress Cloud APIs. It does not own authentication,
  authorization policy, or audit storage.
- It never handles credentials, tokens or private keys.
- Administrative actions are administrative actions: no privileged operation may
  be performed purely client-side.

## Not yet decided

- Front-end framework and build tooling.
- Whether Admin is server-rendered or a client application.
- Break-glass administrator flow.
