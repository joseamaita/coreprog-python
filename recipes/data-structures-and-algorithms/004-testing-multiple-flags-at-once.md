# Python Recipe for Data Structures and Algorithms

## Testing multiple flags at once

### Problem

You need to know different ways to test multiple flags at once.

### Solution

**Version A**

Suppose you have these three flags `x`, `y` and `z`:

```python
>>> x, y, z = 0, 1, 0
>>> x
0
>>> y
1
>>> z
0
```

One way to test the flags would be this:

```python
>>> if x == 1 or y == 1 or z == 1:
...     print('Passed')
...
Passed
```

A different way would be this:

```python
>>> if 1 in (x, y, z):
...     print('Passed')
...
Passed
```

A more compact test would be:

```python
>>> if x or y or z:
...     print('Passed')
...
Passed
```

Another way to test would be this:

```python
>>> if any((x, y, z)):
...     print('Passed')
...
Passed
```
