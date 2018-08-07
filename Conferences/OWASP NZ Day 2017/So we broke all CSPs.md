---
speakers:
- Lukas Weichselbaum
- Michele Spagnuolo
---

# So we broke all CSPs... You won't guess what happened next!

- `strict-dynamic` to ease adoption of nonce space policies by allowing JS if parent had `nonce`
- `nonce`s to come in 2.0
- `report-uri`?
- Closure template
  - Context sensitive: It will escape the variable for the context it's used in.
  - Will propagate nonce token.
- Use `report-sample` to include script sample (first 40B)
- Usefullinks:
  - nico333fr/CSP-useful
  - CSP Mitigator chrome extension
  - [CSP Evaluator](https://csp-evaluator.withgoogle.com/)
  - CSP FrontEnd dedup reports
  - [CSP with Google](https://csp.withgoogle.com/docs/index.html)
  - [GitHub CSP's journey](https://githubengineering.com/githubs-csp-journey/)

## What could go wrong?

See [collection of CSP bypasses](http://sebastian-lekies.de/csp/bypasses.php).

- Rebasing nonce script with `<base>`
  - Fix with `base-uri: 'none';`
- Unclosed SVG set `href` on trusted script tag
- Steal existing nonces with CSS