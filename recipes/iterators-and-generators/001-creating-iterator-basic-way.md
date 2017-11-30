# Python Recipe for Iterators and Generators

## Creating an iterator in a basic way

### Problem

You need a basic way of creating an iterator.

### Solution

**Version A**

To simply loop over all the members of a sequence such as a string, 
tuple, dictionary, or list, just use the most common looping construct, 
which is the `for` statement. This allow us to iterate over a collection 
of items.

```python
>>> for s in "Python is fun!":
...     print(s)
...
P
y
t
h
o
n
 
i
s
 
f
u
n
!
>>> for t in (("David", 38), ("Mark", 21), ("John", 27)):
...     print(t)
...
('David', 38)
('Mark', 21)
('John', 27)
>>> d = {'GOOG': 490.10, 'IBM': 91.50, 'AAPL': 123.15}
>>> for i in d:
...     print(i, d[i])
...
GOOG 490.1
IBM 91.5
AAPL 123.15
>>> for n in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
...     print(f"2 to the {n} power is {2 ** n}")
...
2 to the 1 power is 2
2 to the 2 power is 4
2 to the 3 power is 8
2 to the 4 power is 16
2 to the 5 power is 32
2 to the 6 power is 64
2 to the 7 power is 128
2 to the 8 power is 256
2 to the 9 power is 512
```

In the last example, the variable `n` will be assigned successive items 
from the list `[1, 2, 3, 4, ..., 9]` on each iteration. Because looping 
over ranges of integers is quite common, the following shortcut is often 
used for that purpose:

```
>>> for n in range(1, 10):
...     print(f"2 to the {n} power is {2 ** n}")
...
2 to the 1 power is 2
2 to the 2 power is 4
2 to the 3 power is 8
2 to the 4 power is 16
2 to the 5 power is 32
2 to the 6 power is 64
2 to the 7 power is 128
2 to the 8 power is 256
2 to the 9 power is 512
```

The `range(i,j [,stride])` function creates an object that represents a 
range of integers with values *i* to *j-1*. If the starting value is 
omitted, it's taken to be zero. An optional stride can also be given as 
a third argument. Let's see:

```python
>>> a = range(5)
>>> a
range(0, 5)
>>> list(a)
[0, 1, 2, 3, 4]
>>> b = range(1, 8)
>>> b
range(1, 8)
>>> list(b)
[1, 2, 3, 4, 5, 6, 7]
>>> c = range(0, 14, 3)
>>> c
range(0, 14, 3)
>>> list(c)
[0, 3, 6, 9, 12]
>>> d = range(8, 1, -1)
>>> d
range(8, 1, -1)
>>> list(d)
[8, 7, 6, 5, 4, 3, 2]
```

The `for` loop is one of Python's most powerful language features 
because you can create custom iterator objects and generator functions 
that supply it with sequences of values.
