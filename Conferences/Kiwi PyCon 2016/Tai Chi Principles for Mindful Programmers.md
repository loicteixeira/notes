---
videos:
- https://youtu.be/Skt6hRErR7c
---

# Tai Chi Principles for Mindful Programmers

## Do without doing

This is basically Python core. You don't have to think about all the internals, you just do it.

Showing examples of decorators, the with statement, list comprehensions.

## What is in the way is the way

Example of string interpolation for internationalisation.

`'%s is a member of %s' % (email, list_name)` goes the job until you realise that order of parameters can change.

`'%(email)s is a member of %(list_name)s' % {'email': email, 'list_name': list_name}` allow the order to change but add duplication, not to mention that translators might forgot the `s` at the end of a variable.

Relax and build your own parser `'$email is a member of $list_name'` to make it simpler.

But there is still duplication, use globals and locals instead:

```python
def _(original_text, **extras):
	translated = lookup(original_text)
	frame = sys._getframe()
	d = frame.f_globals.copy()
	d.update(frame.f_locals)
	d.update(extra)
	return translated.safe_substitude(d)
```

Seems evil. Developers at Springload generally agree that there must be a better way.

## Invest in loss, accept to lose to learn from your mistakes

What the title says, plus some analogy with Tai Chi push hands which I don't quite know how to explain on paper.

## Breathe

Because otherwise you die