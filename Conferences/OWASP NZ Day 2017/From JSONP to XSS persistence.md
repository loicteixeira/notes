---
url: https://youtu.be/VtFHxU_IYLA
speaker: Claudio Contin
---

# From JSONP to XSS persistence

Relies on JSONP, Servic Worker and XSS

- JSONP is allowing cross fetch with a callback inseeerted in your body (no Same Origin Policy)
- Service Worker run scripts in the background and cannot access DOM.
- Beef software.
- Fix XSS by only allowing word character for JSONP callback.