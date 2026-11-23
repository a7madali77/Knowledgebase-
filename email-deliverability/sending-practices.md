---
id: email-deliverability.sending-practices
title: Sending practices, list hygiene, message formatting and display names
type: rule
domain: email-deliverability
tags: [list-hygiene, opt-in, from-address, display-name, formatting, ip-strategy, affiliates]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.gmail-bulk-sender-requirements, email-deliverability.email-authentication]
supersedes:
---

## Summary
Beyond authentication, Gmail judges senders on consent, consistency, and honesty: who gets the mail, which address and IP it comes from, and whether headers, display names, and content are truthful.

## Details

### Infrastructure and identity
- SHOULD send all mail from one IP. If using several, MUST separate them by message type (e.g. notifications vs promotions). Why: one stream's reputation does not drag down another.
- SHOULD use one consistent From: address per message category (e.g. `sales@` receipts, `deals@` promotions, `alert@` notifications).
- NEVER mix content types in one message (e.g. promotions inside receipts).

### List and consent
- MUST send only to people who opted in. Why: non-subscribers report spam, which lowers domain reputation.
- SHOULD confirm each address before subscribing (double opt-in).
- SHOULD periodically reconfirm subscriptions and consider removing recipients who never open.
- SHOULD auto-unsubscribe addresses with repeated bounces.
- NEVER buy email lists.
- NEVER use pre-checked opt-in boxes; some regions restrict automatic opt-in.
- NEVER mark internal messages as spam.

### Message formatting
- MUST follow RFC 5322; HTML must follow HTML standards.
- MUST include a valid Message-ID.
- MUST include single-instance headers (From, To, Subject, Date) only once.
- From: header contains exactly one address.
- AVOID oversized headers.
- NEVER use "Re:" or "Fwd:" unless the message really is a reply or forward.
- NEVER hide content with HTML/CSS.
- Links MUST be visible and make clear where they go.
- International domains (authenticating, envelope-from, payload, reply-to, sender) MUST follow Unicode TS #39, section 5.2.

### Display names
- MUST identify only the sender (person and/or organization), consistently.
- NEVER put subject or offer text in it (e.g. "URGENT REQUEST", "Last Chance").
- NEVER include the recipient's name or thread markers like "User (2)".
- NEVER use emojis or symbols to imitate graphics or verification badges.
- NEVER use an @gmail.com address as the display name for bulk mail.

### Programs that affect reputation
- Affiliates: monitor them and remove any that spam; their spam is tied to the brand.
- NEVER send phishing tests or test campaigns from the production domain. Why: risk of reputation loss and blocklisting.
- ESPs: Google accepts no allowlist requests; an ESP cannot guarantee inbox placement.

## Examples
- Good display name: `Nuderm` or `Ahmad from Compound Labs`. Bad: `🔥 SALE ENDS TONIGHT`.

## Exceptions / Edge cases
- Mail from an address saved in the recipient's contacts is less likely to be marked as spam.
