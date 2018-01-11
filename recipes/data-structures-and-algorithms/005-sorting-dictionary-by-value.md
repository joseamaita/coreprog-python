# Python Recipe for Data Structures and Algorithms

## Sorting dictionary by value

### Problem

You need to know different ways to sort a dictionary by value.

### Solution

**Version A**

Suppose you have a dictionary `xs`:

```python
>>> xs = {'a': 4, 'b': 3, 'c': 2, 'd': 1}
>>> xs
{'a': 4, 'b': 3, 'c': 2, 'd': 1}
```

One way to sort the dictionary would be this:

```python
>>> sorted(xs.items(), key=lambda x: x[1])
[('d', 1), ('c', 2), ('b', 3), ('a', 4)]
```

A different way would be this:

```python
>>> import operator
>>> sorted(xs.items(), key=operator.itemgetter(1))
[('d', 1), ('c', 2), ('b', 3), ('a', 4)]
```
