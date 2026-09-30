# Fortress Mail

**Status: PLANNED — integration boundary only.***

Fortress Mail will be delivered by integrating **Mailcow** or **iRedMail**, not
by implementing mail protocols. This repository owns the integration boundary,
the service layer, domain configuration, policy, administration and audit — not
SMTP, IMAP, DKIM or malware scanning.

## Planned structure

```text
mail/
├── gateway/         # TLS-terminating mail gateway / proxy to the mail platform
├── smtp/            # inbound/outbound SMTP integration (handled by mail platform)
├── imap/            # mailbox access integration (handled by mail platform)
├── spam/            # spam and phishing filtering integration
├── malware/         # attachment malware scanning integration
├── dkim/            # DKIM signing/verification integration
├── storage/         # attachment object storage integration
└── administration/  # mailbox provisioning, quota and policy administration
```

No SMTP or IMAP protocol implementation is to be written here.

## Integration boundary (to be defined)

- A `MailProvider` interface abstracts the chosen platform, so the project is not
  locked to Mailcow or iRedMail.
- Fortress owns: domain and DNS records (SPF, DKIM, DMARC), mailbox
  provisioning, quotas, security policy, administrative actions, audit events.
- The mail platform owns: protocol handling, message store, filtering engines.

## Boundaries

- Mailbox and message content are private communications and are treated as
  sensitive.
- Mail administration is a privileged operation and requires authorization plus
  an audit event.
- Mail state exposed to Fortress Cloud is normalized result data, not raw message
  content.

## Not yet decided

- Mailcow vs iRedMail (the decision drives the provider adapter).
- Attachment storage location and retention.
- Mailbox retention and legal-hold policy.
