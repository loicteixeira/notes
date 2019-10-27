---
videos:
- https://youtu.be/3afcBEz6CzA
---

# The Power ⚡️ and Responsibility 😓 of Unicode Adoption ✨

Really about emojis, not the whole unicode standard.

Use Python 3. If you need to use Python 2, use Python 3.

Python 3 ship with the `unicodedata` library which helps transforming from the emoji to its name and vice-versa (it follow RFC 3492). 

Representations of emoji vary by vendor implementation, when there is a representation (incomplete sets for example). Therefore use fallback or you will leave your users with �s.

Also test [vendors implementations](http://glasnt.com/unicode-test/), add [cross platform emoji support](https://github.com/twitter/twemoji) on the front-end or [convert the emojis server-side](https://github.com/glasnt/emojificate).