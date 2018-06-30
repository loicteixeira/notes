---
url: https://youtu.be/6x1uoakCAlU
---

# More testing with fewer tests

`hypothesis` is well known for **Property based testing** but also do **State based testing**.

If a test fails, it writes the input that caused the fail to disk to re-run it laterm because with the random nature of the input, you wouldn't end-up on the same test otherwise. *CI and dev machine sync?!*

It has `Django` integration to populate models.

```python
>>> from hypothesis.extra.django.models import models
>>> from toystore.models import Customer
>>> c = models(Customer).example()
>>> c
<Customer: Customer object>
>>> c.email
'jaime.urbina@gmail.com'
>>> c.name
'\U00109d3d\U000e07be\U000165f8\U0003fabf\U000c12cd\U000f1910\U00059f12\U000519b0\U0003fabf\U000f1910\U000423fb\U000423fb\U00059f12\U000e07be\U000c12cd\U000e07be\U000519b0\U000165f8\U0003fabf\U0007bc31'
>>> c.age
-873375803
>>> from hypothesis.strategies import integers
>>> c = models(Customer, age=integers(min_value=0, max_value=120)).example()
>>> c
<Customer: Customer object>
>>> c.age
5
```

# Property based testing

Decorate the test function and use strategies for data types.

```python
@given(floats())
def test_something(f):
	assert

@given(list(floats(), min_length=1))
def test_something_else(l):
	assert
```

Strategies are useful because they test inputs that are known to have weird behaviours (or just inputs you might not think of)

```python
>>> 9007199254740993 == 9007199254740993.0
False
>>> float(9007199254740993) == 9007199254740993.0
True
>>> 9007199254740993 == int(9007199254740993.0)
False
>>> 9007199254740992 == 9007199254740993.0
True
```

Because you will exclude some values from the strategies, you still need additional tests to check that the validation happens properly (or know that the app will crash in such circumstances).

# State based testing

Generates app that fails instead of random inputs.

```python
from hypothesis.stateful import RuleBaseStateMachine, Bundle, rule
from hypothesis import strategies

from tree import Tree

class TreeRules(RuleBasedStateMachine):
	trees = Bundle('BinaryTree')
	
	@rule(target=trees)
	def leaf(self):
		return Tree()
		
	@rule(target=trees, tree=trees, number=strategies.integers())
	def node(self, tree, number):
		return tree.insert(number)
		
	@rule(tree=trees)
	def check_sorted(self, tree):
		assert list(tree) == sorted(list(tree))
```

Rules with target can be run in any order, any number of times, they build the object (but can still fail obviously).  
Rules without a target test the object and are run anytime during its lifetime.

```python
from hypothesis.control import assume

@rule(target=trees, tree=trees, number=strategies.integers())
def delete(self, tree, number):
	assume(number in list(tree))
	return tree.delete(number)
```

More is coming. Using `assume` statement to ensure the strategy returned a valid number and throw the test away if it doesn't. It produce a lot of waste. Will be integrated to the strategy somehow.