---
videos:
- https://youtu.be/D80XFVNCGLM
---

# Making the web go fast with jelly snakes and raspberry twizzlers

Lots of stats thrown around.

> 40% of your users will leave if load time is greater than 3s. Average load time is 7s

> 70% of the browsers out there already support HTTP/2

When making the shift from HTTP/1.1 to HTTP/2, while some patterns are still useful (gzip compression, minification, CDN), some other become anti-pattern (concatenation, domain sharding).

HTTP/2 headers are binary, not plain text so you need tools. They are also compressed, which creates an attack vector of decompressing a simple header with simple symbols into a really big header but latest version of nginx should fix that.

WebSockets are still relevant, HTTP/2 is only about the initial request.

To get the CDN to `server push` your static files, use `rel="preload"` meta.

As you switch to HTTP/2, measure before, during and after: measure, Measure and MEASURE.