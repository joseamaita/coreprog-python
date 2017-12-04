# Python Recipe for Iterators and Generators

## Knowing origin of an iterator

### Problem

You want to know how an iterator is defined.

### Solution

**Version A**

An *iterable* is an object capable of returning its members one at a 
time. An iterable can be used to feed a `for` loop. The built-in 
function `iter()` takes an iterable object and returns an iterator. A 
call to the `next()` function on the iterator gives us the next element 
if any, and raises a `StopIteration` exception otherwise:

```python
>>> z = iter("Marianne")
>>> z
<str_iterator object at 0x7f2575b42358>
>>> next(z)
'M'
>>> next(z)
'a'
>>> next(z)
'r'
>>> next(z)
'i'
>>> next(z)
'a'
>>> next(z)
'n'
>>> next(z)
'n'
>>> next(z)
'e'
>>> next(z)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```
