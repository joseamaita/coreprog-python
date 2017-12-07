# Python Recipe for Iterators and Generators

## Consuming an iterator manually

### Problem

You need to process items in an iterable, but for whatever reason, you 
can't or don't want to use a `for` loop.

### Solution

**Version A**

To manually consume an iterable, use the `next()` function and write 
your code to catch the `StopIteration` exception. For example, this 
example manually reads lines from a file:

```python
with open('/etc/passwd') as f:
    try:
        while True:
            line = next(f)
            print(line, end='')
    except StopIteration:
        pass
```

Normally, `StopIteration` is used to signal the end of iteration. 
However, if you're using `next()` manually (as shown), you can also 
instruct it to return a terminating value, such as `None`, instead. For 
example:

```python
with open('/etc/passwd') as f:
    while True:
        line = next(f, None)
        if line is None:
            break
        print(line, end='')
```

### Discussion

In most cases, the `for` statement is used to consume an iterable. 
However, every now and then, a problem calls for more precise control 
over the underlying iteration mechanism. Thus, it is useful to know what 
actually happens.

The following interactive example illustrates the basic mechanics of 
what happens during iteration:

```python
>>> l = [1, 2, 3, 4, 5]
>>> # Get the iterator
...
>>> li = iter(l)    # Invokes l.__iter__()
>>> li
<list_iterator object at 0x7fd5c136d2e8>
>>> # Run the iterator
...
>>> next(li)        # Invokes li.__next__()
1
>>> next(li)
2
>>> next(li)
3
>>> next(li)
4
>>> next(li)
5
>>> next(li)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```
