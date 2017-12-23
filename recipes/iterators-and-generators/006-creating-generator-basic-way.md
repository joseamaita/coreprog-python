# Python Recipe for Iterators and Generators

## Creating a generator in a basic way

### Problem

You need a basic way of creating a generator.

### Solution

**Version A**

Instead of returning a single value, you want a basic function that can 
generate an entire sequence of results. To accomplish that, use the 
generation construct, which is the `yield` statement. Let's see a simple 
generator function definition:

```python
>>> def countdown(n):
...     print("Counting down!")
...     while n > 0:
...         yield n
...         n -= 1
...
```

A generator function does not return any values. When we call it, we get 
a `generator object`:

```python
>>> cu = countdown(3)
>>> cu
<generator object countdown at 0x7f99a34eb678>
```

Our generator object is indeed an iterator, as we can see, it implements 
the `__iter__` and the `__next__` methods:

```python
>>> print(hasattr(cu, '__iter__'))
True
>>> print(hasattr(cu, '__next__'))
True
```

Calling a generator function creates an object that produces a sequence 
of results through successive calls to a `__next__()` method. Let's see:

```python
>>> cu.__next__()
Counting down!
3
>>> cu.__next__()
2
>>> cu.__next__()
1
```

The `__next()__` call makes a generator function run until it reaches 
the next `yield` statement. At this point, the value passed to `yield` 
is returned by `__next__()`, and the function suspends execution. The 
function resumes execution on the statement following `yield` 
when `__next__()` is called again. This process continues until the 
function returns.

Normally you would not manually call `__next__()` as shown. Instead, you 
would use a `for` loop like this:

```python
>>> for i in countdown(8):
...     print(i, end=' ')
...
Counting down!
8 7 6 5 4 3 2 1
```

Generators are an extremely powerful way of writing programs based on 
processing pipelines, streams, or data flow.
