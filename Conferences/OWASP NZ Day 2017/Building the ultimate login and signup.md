---
speaker: Matt Cotterell
---

# Building the ultimate login and signup

## Registration

- Get a copy of user credentials, really
- Only ask/collect what you need
- Hash password with random salt and re-hash multiple times
- Encourage highly entropic password
  - [zxcvbn](https://github.com/dropbox/zxcvbn) is an entropy based password strengh meter
- Discourage automatic login/signup
  - Use re-captcha
- Be mindful of users with disabilities though.

## Before the Login

- Let users use a password manager
  - Don't do `<input type="password" onpaste="return false;">
- Password reset
  - Unique token via email
- Always use password type input for password
  - Browsers handle them differently
  - Autocomplete changes (OS might store a non-password type input)
  - Will be warn on HTTP

## During the Login

- HTTPS everywhere
- Expire session cookie after each login/logout
- Rate limit brutefore attack
- Block IPs not accounts
- Use 2 of: knowledge (password), possession (2FA), inheritence (fingerprint)

## After the Login

- Ensure user required redirect go to domain you control