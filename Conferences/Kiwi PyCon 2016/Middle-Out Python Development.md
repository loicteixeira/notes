---
url: https://youtu.be/hXIAA8F8aPE
---

# Middle-Out Python Development

> Have you comited to X because you use Y?

You should decouple your business code from the framework you're using.

To achieve that you should write a consistent interface so you can test that interface in isolation and swap internals without affecting the rest of the code. Also, it becomes much easier to mock the interface to test other parts that use this interface.

```python
facade = settings.FACADE_CLASS()
facade.get_books()
facade.get_book(book_id)
```

Django ORM is an abstraction above SQL data stores but doesn't allow you to swap it for another type of data store.

Sensible argument but basically advocate not to use a framework.