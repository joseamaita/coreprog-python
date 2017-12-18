# Python Recipe for Files and I/O

## Printing to a file

### Problem

You want to redirect the output of the `print()` function to a file.

### Solution

**Version A**

Use the `file` keyword argument to `print()`, like this:

```python
>>> with open('hello-world.txt', 'wt') as f:
...     print("Hello, World!", file=f)
...
```

If you want to see the contents of the `hello-world.txt` file, you do 
this:

```python
>>> with open('hello-world.txt', 'rt') as f:
...     f.read()
...
'Hello, World!\n'
```

### Discussion

There's not much more to printing to a file other than this. However, 
make sure that the file is opened in text mode. Printing will fail if 
the underlying file is in binary mode.
