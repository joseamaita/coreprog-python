# Python Recipe for Data Structures and Algorithms

## Merging two dictionaries in a basic way

### Problem

You need to know how to merge two dictionaries with a single expression.

### Solution

**Version A**

Suppose you have dictionaries `x` and `y`:

```python
>>> x = {'a': 1, 'b': 2}
>>> y = {'b': 3, 'c': 4}
```

Apply the double star `*` operator like this:

```python
>>> z = {**x, **y}
>>> z
{'a': 1, 'b': 3, 'c': 4}
>>> z = {**y, **x}
>>> z
{'b': 2, 'c': 4, 'a': 1}
```

Notice that in these examples, Python merges dictionary keys in the 
order listed in the expression, overwriting duplicates from left to 
right.
