---
speakers:
- Kevin Alcock
---

# OWASP Top Ten (2017 Draft)

OWASP is for attackers, defenders, developers and testers.

Attacks nowadays are 66% XSS, 20% CSRF, 3% SQL Injections, etc.

## A1 - Injection

Injection can happen anywhere: SQL, LDAP, NoSQL, Parsers, SMTP Headers, etc.

## A2 - Broken Authentication and Session Management 

- Use analytics to find right length for session validity.
- Validate password on sensitive operation.

## A3 - XSS

XSS comes in multiple forms: stored, reflected, server, client.

Remember to escape, *escape* and **escape**.

## A4 - Broken Access Control (Comeback)

Don't just hide features, check access.

## A5 - Security Misconfiguration

Using default settings? Don't. Even on dev.

Test that your policies actually do what they are supposed to.

## A6 - Sensitive Data Exposure

You can't be breached for the data you don't have. Only collect what you truly need.

Check legislation of country you're operating in.

## A7 - Insufficient Attack Protection (New)

Do you kno when you're under attack? WAFs, IDS, firewalls and honeypots aren't enough. Actively monitor and respond accordingly.

## A8 - CSRF

## A9 - Using components with known vulnerabilities

- Audit 3rd party dependencies and challenge the need for those.
- Regularly check vendors and Common Vulnerabilities and Exposures (CVE).

## A10 - Unprotected APIs (New)

Just because it's not "published" doesn't mean it's not discoverable.

Secure communications, credentials, tokens and keys. Harden parsers.