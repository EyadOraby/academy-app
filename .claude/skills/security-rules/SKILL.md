---
name: security-rules
description: Security rules for auth, payments, secrets, access control and members' personal data. Use when writing or reviewing anything that touches those areas.
---

# Security rules

## Areas that always need Eyad's own review
Authentication and sessions, payments, access-control rules, role changes, and any code that reads or writes members' personal data. Mark these PRs `NEEDS EYAD'S REVIEW` and do not merge without it.

## Secrets
- No keys, tokens or passwords in the repo, in code, in tests or in commit messages.
- Client apps hold only public keys. Privileged keys stay on the server.
- If a secret is committed, treat it as leaked: rotate it, then remove it.

## Authentication
- Use the platform's auth; do not write custom password hashing or token schemes.
- Store tokens in secure storage on the device, never in plain preferences.
- Enforce authorisation on the server for every request. The mobile UI hiding a button is not security.

## Personal data
- Some members are minors. Collect only the fields a feature needs.
- Never log personal data, tokens or payment details.
- Each member can access only their own data; guardians only their linked members.

## Payments
- Never store card numbers or CVV. Use the payment provider's hosted flow.
- Confirm payment status on the server from the provider's webhook, never from the client's word.
- Verify webhook signatures. Make payment handlers idempotent.

## Input and output
- Validate all input on the server. Treat everything from the client as untrusted.
- Return generic error messages to clients; keep detail in server logs.

## Dependencies
- No new dependency without approval. Prefer well-maintained packages and pin versions.
