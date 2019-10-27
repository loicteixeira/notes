---
videos:
- https://youtu.be/TPR-Cke097U
speakers:
- Nick Malcolm
---

## How to spot and stop a wolf in sheep's clothing (a.k.a Account Takeover)

## Know

- Usernames amd password aren't enough to prove someone's identity.
- Localised account takeover
  - Malware
  - Fishing
  - XSS
  - Social Engineering
- Remtoe credential reuse
  - Find password from dictionaries
  - Check at haveibeenpowned.com

## Prevent

- Rate limiting
- Support 2FA
- IP Whitelist
- Do not use password policies beside minimum length
- Outsource authentication all together

## Detect

- What is normal? What browser, which location, etc.
- [AuthTables](https://github.com/magoo/AuthTables) is simple but has the drawback of having a hard pass or fail.
  - Only uses IP and cookies but there is a lot more you can look at.
- Machien learning would be better but is hard.
- Statistics: Smarter than AuthTables

## Respond

- Alert the users (email/slack)
- Block activity completely
- Guide the user through the scary journey