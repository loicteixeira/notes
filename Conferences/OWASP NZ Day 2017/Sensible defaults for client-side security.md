---
speaker: Jen Zajac
---

# Sensible defaults for client-side security

Aim for secure defaults. It removes the need for making choices.

## Dependencies Management

- Evaluate with npmcompare.com
- Don't want to break while upgrading but do want security updates?
  - Have automated regression testing
  - Use npm-update-checker
  - Use retire.js or nsp or snyk or advisories
- Action: Update, remove or ignore
- Verify CDN resources with [srihash.org](https://www.srihash.org/)

## CSP

- Roll it from the start
- Use it for dev and test as well
- Lock down first and open up later
- Send report of failures to log?

## Store locally

- Use the `HttpOnly` flag. The front-end should not be able to read your back-end cookies.
- Use the `Secure` flag.
- Set the cookie with `SameSite` to avoid CSRF.
- JWT
    - New and poorly understood.
    - Only use for token

## Escaping

- Don't roll your own
- Escape for the right coontext

## Misc

- Use `rel="noreferrer noopener"` if using target `target=_blank` on links.