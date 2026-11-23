---
id: email-deliverability.one-click-unsubscribe
title: One-click unsubscribe (RFC 8058) for bulk senders
type: procedure
domain: email-deliverability
tags: [unsubscribe, list-unsubscribe, rfc-8058, rfc-2369, bulk-sending]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.gmail-bulk-sender-requirements]
supersedes:
---

## Summary
Senders of more than 5,000 messages/day to Gmail must support one-click unsubscribe on marketing and subscribed messages, using two List-Unsubscribe headers, plus a visible unsubscribe link in the message body.

## Details

### Preconditions
- An HTTPS endpoint that accepts POST requests and unsubscribes the recipient without further confirmation.

### Steps
1. Add both headers to every marketing/subscribed message:
   ```
   List-Unsubscribe-Post: List-Unsubscribe=One-Click
   List-Unsubscribe: <https://yourdomain.com/unsubscribe/{token}>
   ```
2. Handle the POST that Gmail sends when a recipient clicks unsubscribe. The body is `List-Unsubscribe=One-Click`, content type `application/x-www-form-urlencoded`.
3. Remove the recipient from the list.
4. Also include a clearly visible unsubscribe link in the message body.

### Expected result
- Gmail shows an "Unsubscribe" option next to the sender; one click removes the recipient.

### Failure modes
- Endpoint requires login or a confirmation page → not one-click; non-compliant.

## Examples
- Most ESPs (including HubSpot marketing email) add these headers automatically (inferred; verify per ESP).

## Exceptions / Edge cases
- Preference centers (per-list unsubscribe, unsubscribe-all) and auto-unsubscribing hard bouncers are allowed as extras but NEVER replace one-click unsubscribe.
- Specs: RFC 2369 (List-Unsubscribe header), RFC 8058 (one-click).

## Open questions
- Which ESP(s) will send the high volume, and are their one-click headers verified on a live message?
