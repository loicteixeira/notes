---
videos:
- https://youtu.be/0C-winjhYSE
speakers:
- Erica Anderson
---

# The Magical World of Cloud Security

Looking at *A7 - Insufficient Attack Protection*.

## Host-level Security

- Secrets
  - Don't commit these
  - Store in "vaults" instead: AWS Parameter Store, Azure Key Vault or Cloud Storages + Access Control + Encryption Key
- MFA for server access 
- TLS certificate:
  - Let's Encrypt
  - See OWASP TLS cheatsheet for private key size, strong protocol, stron cypher recommandation
  - Should you encrypt traffic between your own servers?
- Host based monitoring
  - Gateway inspection or manager + agent on each host: OSSEC open-source Host-based Intrusion Detection System (HIDS).

## Platform-level Security

- Access, User and Management
  - Cloudsploit, Analysis of security API activity
  - Bottom-Up permission model
  - Newer, trust-less architecture model
- System log monitoring
  - Be able to correlate from multiple sources (see Graylog, an open-source stack to collect, search and visualise)
- Ingress & Egress. Security monitoring alert
  - Tools to scan traffic as it comes in/out.
  - Requires decrypt/encrypt.
  - Start from the bottom with security rules and policies.

## Everything else (other people networks)

- CDN
  - Shared responsability, you trust them
  - stop from request to hit your infra

## Technical Debt

No tools or technologies will fix orphaned/outdated code.