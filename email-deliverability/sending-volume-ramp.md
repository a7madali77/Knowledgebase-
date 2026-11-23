---
id: email-deliverability.sending-volume-ramp
title: Ramping sending volume and handling Gmail rate limits (4.7.28)
type: procedure
domain: email-deliverability
tags: [warmup, ramp-up, rate-limiting, smtp-4.7.28, quotas, bulk-sending]
status: verified
confidence: high
source: Google, Gmail Help "Email sender guidelines" (retrieved 2026-11-23)
created: 2026-11-23
updated: 2026-11-23
related: [email-deliverability.spam-rate-monitoring, email-deliverability.smtp-error-playbook, email-deliverability.high-volume-launch-checklist]
supersedes:
---

## Summary
Gmail limits how much mail a domain and an IP can deliver in a given time. Volume must grow gradually, starting with engaged recipients. Sudden spikes cause rate limiting (SMTP 4.7.28) and reputation drops.

## Details

### How Gmail applies limits
- Gmail tracks volume, feedback, and limits per domain AND per IP.
- DKIM/SPF quotas belong to the domain: one domain hitting its limit does not block other domains on the same IP.
- The IP quota is shared: when an IP hits its quota, every domain sending from that IP is blocked.
- Limits are counted by the recipient's MX host, not the recipient's address domain. All domains whose MX is google.com (including Google Workspace customers) count toward the same Gmail limit.

### What sets the safe ramp speed
- Higher total volume → slower increase.
- Daily sending → can ramp faster than weekly sending.
- Recipient feedback: send only to subscribers; always offer unsubscribe.

### Ramp procedure
1. Start with low volume to the most engaged recipients.
2. Send at a consistent rate. Avoid bursts.
3. Increase gradually. NEVER suddenly double volume without a history of sending at that level.
4. Monitor at each step: SMTP responses, spam rate, domain reputation (Postmaster Tools).
5. When changing email format, infrastructure, or header structure, ramp the changed segment separately.
6. On bounces or deferrals: reduce volume until the error rate drops, then increase slowly again. If errors persist at low volume, test a blank message to isolate content issues.

### When Gmail returns 4.7.28 (quota exceeded)
1. Stop sending for at least 10 minutes.
2. Identify the cause. If the error does not name DKIM, SPF, or IP quota, assume all three are hit.
3. After 10 minutes, send from a single connection.
4. If that fails, wait another 10 minutes and retry.
5. If it succeeds, add connections one at a time up to the desired number.

## Exceptions / Edge cases
- Google Workspace/Gmail as the sender: hitting the limit throttles the sending IP.

## Open questions
- Target daily volume and current sending history are needed to build a concrete ramp schedule (numbers per day). The source gives no numeric schedule.
