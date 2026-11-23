---
id: email-deliverability.smtp-error-playbook
title: Gmail SMTP rejection codes and responses
type: playbook
domain: email-deliverability
tags: [smtp-errors, bounces, troubleshooting, 4.7.28, 5.7.26, 5.7.1]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.sending-volume-ramp, email-deliverability.email-authentication]
supersedes:
---

## Summary
Common Gmail SMTP rejection codes, what causes them, and the first response to each.

## Details
- WHEN `4.7.28` (rate limit / quota exceeded) THEN pause at least 10 minutes and resume with a single connection, adding connections one at a time BECAUSE the domain (SPF/DKIM) or IP quota was exceeded. Full procedure: [[email-deliverability.sending-volume-ramp]].
- WHEN `5.7.26` THEN fix SPF/DKIM (and DMARC for bulk senders) BECAUSE the message failed authentication requirements.
- WHEN `550 5.7.1` (IP on suspended list) THEN check the IP's blocklist status and reputation; consider moving off a poor shared IP BECAUSE the sending IP has a poor reputation.
- WHEN `550-5.7.1 ... IPv6 sending guidelines regarding PTR records and authentication` THEN add an IPv6 PTR record (or confirm the ESP has one) BECAUSE the IPv6 sending server lacks valid reverse DNS.
- WHEN `421 4.7.0` THEN check the recipient domain's allowed-IP setup BECAUSE the sending IP is not on the recipient domain's allowed list.
- WHEN bounces or deferrals rise during a send THEN reduce volume until errors drop, then ramp slowly BECAUSE continued pressure deepens rate limiting.
- WHEN problems persist after following all guidelines THEN use Google's "Troubleshooting for senders with email delivery issues" tool.

## Open questions
- Google's full SMTP error reference has more codes; add them as they come up.
