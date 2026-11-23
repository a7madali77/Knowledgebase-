# Glossary

| term | definition | entry |
|------|------------|-------|
| Bulk sender | Sends more than 5,000 messages/day to personal Gmail accounts | email-deliverability.gmail-bulk-sender-requirements |
| SPF | DNS record listing servers authorized to send for a domain | email-deliverability.email-authentication |
| DKIM | Cryptographic signature proving the domain owner sent a message | email-deliverability.email-authentication |
| DMARC | DNS policy telling receivers how to treat mail failing SPF/DKIM; requires From: alignment | email-deliverability.email-authentication |
| DMARC alignment | From: header domain matches the SPF or DKIM authenticating domain | email-deliverability.email-authentication |
| PTR record | Reverse DNS record mapping a sending IP to a hostname | email-deliverability.email-authentication |
| One-click unsubscribe | RFC 8058 List-Unsubscribe-Post mechanism letting recipients unsubscribe with one click | email-deliverability.one-click-unsubscribe |
| Postmaster Tools | Google's dashboard for Gmail spam rate, reputation and authentication data | email-deliverability.spam-rate-monitoring |
| Spam rate | Share of delivered mail that recipients report as spam, per Postmaster Tools | email-deliverability.spam-rate-monitoring |
| 4.7.28 | Gmail SMTP code for exceeding domain or IP sending quota | email-deliverability.smtp-error-playbook |
