# Python Recipe for Iterators and Generators

## Defining an iterator with a class

### Problem

You want to make your own definition of an iterator using a class.

### Solution

**Version A**

*Iterator* objects are required to support two methods, the `__iter__` 
method that returns the iterator object itself, used in `for` and `in` 
statements, and the `__next__` method that returns the next value from 
the iterator. If there is no more items to return, then the `__next__` 
method should raise a `StopIteration` exception. Let's see the class 
definition `range_5`:

```python
>>> class range_5:
...     def __init__(self):
...         self.i = 0
...     def __iter__(self):
...         return self
...     def __next__(self):
...         if self.i < 5:
...             i = self.i
...             self.i += 1
...             return i
...         else:
...             raise StopIteration()
...
```

Test the class with the interpreter like this:

```python
>>> y = range_5()
>>> y
<__main__.range_5 object at 0x7f7351f77a20>
>>> next(y)
0
>>> next(y)
1
>>> next(y)
2
>>> next(y)
3
>>> next(y)
4
>>> next(y)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 12, in __next__
StopIteration
```
