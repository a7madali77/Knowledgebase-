---
id: email-deliverability.gmail-bulk-sender-requirements
title: Gmail bulk sender requirements (5,000+ messages/day)
type: rule
domain: email-deliverability
tags: [gmail, bulk-sending, compliance, spf, dkim, dmarc, unsubscribe]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.email-authentication, email-deliverability.one-click-unsubscribe, email-deliverability.spam-rate-monitoring, email-deliverability.high-volume-launch-checklist]
supersedes:
---

## Summary
Since 2024-02-01, Gmail enforces a mandatory set of requirements on anyone sending email to personal Gmail accounts (@gmail.com, @googlemail.com). Senders of more than 5,000 messages/day to Gmail ("bulk senders") face a stricter set. Missing them causes rejection, spam placement, or rate limiting.

## Details

### Scope
- Applies to mail sent to personal Gmail accounts: addresses ending in @gmail.com or @googlemail.com.
- Bulk threshold: more than 5,000 messages/day to Gmail accounts.

### All senders: MUST
- MUST authenticate sending domains with SPF **or** DKIM. Why: unauthenticated mail is marked as spam or rejected (error 5.7.26).
- MUST have valid forward and reverse DNS (PTR) for sending domains/IPs. Why: Gmail verifies the sending IP's identity.
- MUST transmit over TLS. Why: required since Dec 2023.
- MUST keep the Postmaster Tools spam rate below 0.3%.
- MUST format messages per RFC 5322 (Internet Message Format).
- NEVER impersonate Gmail in the From: header. Why: Gmail applies a DMARC quarantine policy to gmail.com.

### Bulk senders (>5,000/day): MUST, in addition
- MUST set up SPF **and** DKIM (both).
- MUST publish a DMARC record. A policy of `p=none` is acceptable.
- MUST align the From: header domain with the SPF domain or the DKIM domain (DMARC alignment).
- MUST support one-click unsubscribe on marketing and subscribed messages, AND show a visible unsubscribe link in the body.

## Examples
- A HubSpot marketing email blast of 20,000/day to a mixed list with ~40% Gmail addresses = ~8,000 Gmail messages/day → bulk sender rules apply.

## Exceptions / Edge cases
- Transactional mail is still bound by the "all senders" rules; the one-click unsubscribe rule targets marketing and subscribed messages.
- Requirements change over time; Google's "Email sender guidelines FAQ" holds the latest updates.

## Open questions
- Does this knowledge base also need Yahoo/Microsoft (Outlook) bulk sender rules? They introduced similar requirements.
