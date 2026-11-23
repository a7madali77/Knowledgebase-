---
id: email-deliverability.high-volume-launch-checklist
title: Checklist before sending high email volume to Gmail
type: procedure
domain: email-deliverability
tags: [checklist, bulk-sending, launch, gmail]
status: draft
confidence: high
source: Compiled from Google "Email sender guidelines" (retrieved 2026-11-23); ordering is Claude's synthesis
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.gmail-bulk-sender-requirements, email-deliverability.email-authentication, email-deliverability.one-click-unsubscribe, email-deliverability.sending-volume-ramp, email-deliverability.sending-practices, email-deliverability.spam-rate-monitoring]
supersedes:
---

## Summary
Pre-flight checklist for sending a high volume of email a day (5,000+ to Gmail). Every item maps to a Gmail requirement or guideline. Complete it top to bottom before scaling volume.

## Details

### 1. Authentication and DNS
- [ ] SPF record published, listing every sending service
- [ ] DKIM on, key ≥ 1024 bits (2048 preferred)
- [ ] DMARC record published (`p=none` minimum) with `rua` reports
- [ ] From: domain aligned with SPF or DKIM domain
- [ ] Sending IP has PTR + matching A/AAAA record (or the ESP confirms this)
- [ ] TLS enabled

### 2. Message setup
- [ ] One-click unsubscribe headers + visible unsubscribe link in the body
- [ ] RFC 5322 compliant; valid Message-ID; no duplicate single-instance headers
- [ ] Display name = sender identity only
- [ ] Consistent From: address per message category; no mixed content types

### 3. List
- [ ] Only opted-in recipients; no purchased lists; no pre-checked boxes
- [ ] Hard bounces and long-term non-engagers removed

### 4. Infrastructure
- [ ] Separate IPs/subdomains or streams for transactional vs marketing (if using multiple)
- [ ] Shared IP (if any) checked against blocklists and in Postmaster Tools

### 5. Monitoring
- [ ] Google Postmaster Tools verified for the domain
- [ ] Safe Browsing status clean for the domain and linked domains

### 6. Ramp
- [ ] Start with engaged recipients, low volume, consistent rate
- [ ] Increase gradually; watch spam rate (< 0.10%), reputation, SMTP errors
- [ ] 4.7.28 response procedure known to whoever runs sends

## Open questions
- Target volume/day, ESP (HubSpot or other), and dedicated vs shared IP are needed to turn step 6 into a dated schedule.
