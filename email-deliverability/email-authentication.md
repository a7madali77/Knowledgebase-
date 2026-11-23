---
id: email-deliverability.email-authentication
title: Email authentication and sending infrastructure (SPF, DKIM, DMARC, PTR)
type: reference
domain: email-deliverability
tags: [spf, dkim, dmarc, ptr, dns, ip-reputation, shared-ip]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.gmail-bulk-sender-requirements, email-deliverability.sending-practices]
supersedes:
---

## Summary
SPF, DKIM, and DMARC prove that mail claiming to come from a domain is authorized by that domain. Gmail requires SPF or DKIM for all senders and all three for bulk senders. The sending IP must also have matching forward and reverse DNS.

## Details

| Method | What it does | Setup | Gmail requirement |
|---|---|---|---|
| SPF | Lists the servers allowed to send for the domain | Publish an SPF TXT record listing **every** sender (incl. ESPs like HubSpot) | All senders: SPF or DKIM. Bulk: required |
| DKIM | Cryptographic signature proving the domain owner sent the message | Turn on in the ESP / generate keys; publish the public key in DNS | Key length ≥ 1024 bits; 2048 bits recommended. Bulk: required |
| DMARC | Tells receivers what to do with mail failing SPF/DKIM; enables reports | Publish a DMARC TXT record (`_dmarc.domain`) | Bulk: required; `p=none` acceptable |

### DMARC pass condition
- The message passes SPF or DKIM (or both), AND
- The authenticating domain matches the domain in the From: header (alignment).
- Best practice: SPF and DKIM aligned with each other at the organizational domain level.

### Reverse/forward DNS (PTR)
- The sending server's public IP MUST have a PTR record resolving to a hostname (reverse lookup).
- That hostname MUST have an A (IPv4) or AAAA (IPv6) record resolving back to the same IP (forward lookup).
- IPv6 senders need an IPv6 PTR record; otherwise expect `550-5.7.1 ... IPv6 sending guidelines` errors.
- Check with the Google Admin Toolbox Dig tool.

### Shared IPs
- A shared IP's reputation is the combined reputation of every sender on it.
- On a shared IP: confirm it is not on any blocklist; check its reputation in Postmaster Tools.

## Examples
- SPF record covering Google Workspace and HubSpot: `v=spf1 include:_spf.google.com include:<hubspot-include> ~all` (inferred: exact HubSpot include value comes from HubSpot's domain settings).
- Starter DMARC record: `v=DMARC1; p=none; rua=mailto:dmarc@yourdomain.com`.

## Exceptions / Edge cases
- Third-party senders missing from SPF are more likely to land in spam.
- Forwarded mail can break SPF; follow Google's forwarding best practices.
- Authenticate the domain hosting the public website too, even if it does not send.

## Open questions
- DMARC policy progression plan (none → quarantine → reject) is not covered by the source.
