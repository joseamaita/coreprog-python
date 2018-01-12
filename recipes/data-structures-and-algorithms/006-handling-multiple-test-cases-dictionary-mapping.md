# Python Recipe for Data Structures and Algorithms

## Handling multiple test cases with dictionary mapping

### Problem

You need to know how to handle multiple test cases with dictionary 
mapping.

### Solution

**Version A**

Suppose you have a dictionary `user_id_to_name`:

```python
>>> user_id_to_name = {
...     382: "Alice", 
...     590: "Bob", 
...     951: "Dilbert", 
... }
>>> user_id_to_name
{382: 'Alice', 590: 'Bob', 951: 'Dilbert'}
```

Next, write the core function that actually handles the test cases:

```python
>>> def greeting(user_id):
...     return f"Hi {user_id_to_name.get(user_id, 'there')}!"
...
```

Evaluate such function and notice the conversion from *id* to *name* 
(includes default value if no *id* is found):

```python
>>> print(greeting(382))
Hi Alice!
>>> print(greeting(590))
Hi Bob!
>>> print(greeting(951))
Hi Dilbert!
>>> print(greeting(99951))
Hi there!
```

The implementation shown above is known as one of the workarounds of 
"switch/case" statements on Python.
