# Fortress Mobile

**Status: PLANNED** — placeholder only. No implementation exists.

Fortress Mobile is the user-facing Fortress experience for supported standard
Android devices.

> Fortress Mobile is **not** the operating system. It is **not** AfOS Android.
> No AfOS source is or will be present in this repository.

## Planned structure

```text
android/fortress/
├── app/             # application shell and navigation
├── core/            # platform-independent application logic
├── security/        # local protection, secure storage
├── authentication/  # sign-in flow and Identity integration
├── device/          # device registration and status reporting
├── calls/           # call control within platform capability limits
├── sms/             # SMS control within platform capability limits
├── ussd/            # USSD control within platform capability limits
├── contacts/        # contact management and policy-aware authorization
├── identity/        # identity verification client
├── liveness/        # liveness capture workflow
├── camera/          # camera integration
├── location/        # location and telemetry
├── intrusion/       # intruder protection workflow
├── tamper/          # tamper signals
├── policy/          # policy synchronization and local cache
├── mail/            # Fortress Mail client
├── notifications/   # notification integration
├── remote/          # remote command reception and execution
├── database/        # local persistence
└── ui/              # user interface
```

## Capability honesty (mandatory)

The platform must never claim capabilities the device or API does not provide:

- A normal third-party Android application **cannot** universally intercept
  every call, SMS or USSD operation.
- Enforcement strength differs by edition: standard Android → Device Owner /
  Android Enterprise → AfOS system-level enforcement.
- Unsupported enforcement must be reported explicitly, not silently faked.
- Integrity, root, debug and emulator checks are *signals*, never the sole
  security boundary.

## Boundaries

- Only platform-independent functionality is implemented here first.
- Where operating-system functionality is eventually required, a clean
  interface is created so AfOS can later integrate. That interface must depend
  on no undocumented AfOS internals.
- Application logic is testable without a physical device; heavy Android and
  AfOS build workloads run in CI.
