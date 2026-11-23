---
id: email-deliverability.spam-rate-monitoring
title: Spam rate thresholds and monitoring with Google Postmaster Tools
type: reference
domain: email-deliverability
tags: [postmaster-tools, spam-rate, reputation, open-rate, monitoring, safe-browsing]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.gmail-bulk-sender-requirements, email-deliverability.sending-volume-ramp]
supersedes:
---

## Summary
Google Postmaster Tools is the source of truth for Gmail deliverability. The user-reported spam rate is the main health metric: target below 0.10%, and never reach 0.30%.

## Details

### Spam rate thresholds (Postmaster Tools)
| Level | Spam rate | Meaning |
|---|---|---|
| Target | < 0.10% | Healthy; absorbs occasional complaint spikes |
| Hard limit | ≥ 0.30% | Violates sender requirements; increased spam classification |

- Recovery is slow: improvements in spam rate take time to show up in classification.

### What Postmaster Tools shows
- When recipients mark mail as spam.
- Why messages may not be delivered.
- Whether messages are authenticated.
- Domain and IP reputation and their effect on delivery.

### Open rates
- Google does not track open rates and cannot verify third-party open rates.
- Low open rates are NOT a reliable signal of deliverability or spam problems. Use spam rate and reputation instead.

### Other checks
- Check regularly that the sending domain and any linked domains are not flagged by Google Safe Browsing (Safe Browsing site status page).
- Use the Google Admin Toolbox to review domain DNS settings.

## Open questions
- Is Postmaster Tools already set up and verified for the sending domain(s)?
