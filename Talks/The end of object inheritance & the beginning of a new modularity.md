---
url: https://youtu.be/3MNVP9-hglc
---

# The End Of Object Inheritance & The Beginning Of A New Modularity

## Premises

1. We use types for nouns
  - Can be formerly declared as types in statically typed languages, or expected properties/attributes/methods on subsystems
2. We express ourselves structurally
  - In code, not comments or docstring
  - Use folder structures
  - Methods might have different visibility
  - Use control flow
3. Most programming is parametric programming
  - Programs take input that changes the output in some valuable way.

Those premises aren't only true but are virtuous.

## The problem

We're asked to implement an abstract type with 2 know/concrete steps and 1 unknown/abstract intermediary step. In ortodox inheritence, an abstract class is created with 2 implemented methods and one abstract (which the client/subclass will implement, tell us how to do).

```python
class MyAbstractClass:
  def orange_method(self):
    pass
    
  def green_method(self):
    """Do not call orange_method in your implementation"""
    raise NotImplementedError()
    
  def blue_method(self):
    pass
```

When implementing the intermediary step, the client is encouraged to call the first step method but not the third. This is done via documentation (which violates premise #2) and while visibility of the method could help, the client still needs to know about those methods. In addition, it's not using type to organise (premise #1).

## Composition to the rescue

Instead of inheriting, pass one layer into another. It's an explicit one way relationship unlike the original solution, where green might depend on blue via self attributes (which is described as a one way relationship in English but a two ways relationship in code).

With composition, a module defines interfaces, nouns now have types (premise #1)

```python
class Blue:
  def blue_method(self):
    raise NotImplementedError()
    
class Green:
  def green_method(self):
    raise NotImplementedError()
    
class Orange:
  def orange_method(self):
    raise NotImplementedError()
```

The module also implements two concrete types.

```python
class ImplementedBlue(Blue):
  def blue_method(self):
    pass
    
class ImplementedOrange(Orange):
  def __init__(self, green):
    self._green = green
  
  def orange_method(self):
    pass
```

The client only implement the third class.

```python
class ImplementedGreen(Green):
  def __init__(self, blue):
    self._blue = blue

  def green_method(self):
    pass
```

Unlike classic inheritance, dependencies are explicit (you don't have to follow MRO to know what is being called). You can also use delegation (green proxying an attribute from blue).

Both solutions are right, but in the latter, there is no need to explain.

## Fault (in)Tolerance

It is desired to call immediate attention to errors and not allow the error to pass silently.

Classic inheritance will not prevent you from calling methods you should, or method the module reserves the right to call later but doesn't do yet. The code will work just fine then, until you update the library. With composition, it's impossible for the higher level of the stack to reference the lower levels. It's making illegal states unrepresentable.