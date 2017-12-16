# Python Recipe for Files and I/O

## Reading and writing text data

### Problem

You need to read or write text data, possibly in different text 
encodings such as ASCII, UTF-8, or UTF-16.

### Solution

**Version A**

Use the `open()` function with mode `rt` to read a text file. For 
example, here we read the entire file as a single string:

```python
>>> with open('datafile', 'rt') as f:
...     data = f.read()
...     print(data)
...
  1 1050.000000
  2 1102.500000
  3 1157.625000
  4 1215.506250
  5 1276.281563
  6 1340.095641
  7 1407.100423
  8 1477.455444
  9 1551.328216
 10 1628.894627
 11 1710.339358
 12 1795.856326
 13 1885.649142
 14 1979.931599
 15 2078.928179
 16 2182.874588
 17 2292.018318
 18 2406.619234
 19 2526.950195
 20 2653.297705
 21 2785.962590
 22 2925.260720
 23 3071.523756
 24 3225.099944
 25 3386.354941
```

Here, we iterate over the lines of the file and process each to strip 
the left whitespace:

```python
>>> with open('datafile', 'rt') as f:
...     for line in f:
...         print(line.lstrip(), end='')
...
1 1050.000000
2 1102.500000
3 1157.625000
4 1215.506250
5 1276.281563
6 1340.095641
7 1407.100423
8 1477.455444
9 1551.328216
10 1628.894627
11 1710.339358
12 1795.856326
13 1885.649142
14 1979.931599
15 2078.928179
16 2182.874588
17 2292.018318
18 2406.619234
19 2526.950195
20 2653.297705
21 2785.962590
22 2925.260720
23 3071.523756
24 3225.099944
25 3386.354941
```

Similarly, to write a text file, use `open()` with mode `wt` to write a 
file, clearing and overwriting the previous contents (if any). For 
example, here we write chunks of text data:

```python
>>> with open('datafile-copy', 'wt') as f:
...     f.write("Python is fun!\n")
...     f.write("Python is powerful!\n")
...     f.write("Python is good for you!\n")
...
15
20
24
>>> with open('datafile-copy', 'rt') as f:
...     data = f.read()
...     print(data)
...
Python is fun!
Python is powerful!
Python is good for you!
```

Here, we redirect the output using a `print` statement with a `file` 
argument:

```python
>>> with open('datafile-copy', 'wt') as f:
...     print("Python is fun!", file=f)
...     print("Python is powerful!", file=f)
...     print("Python is good for you!", file=f)
...
>>> with open('datafile-copy', 'rt') as f:
...     data = f.read()
...     print(data)
...
Python is fun!
Python is powerful!
Python is good for you!
```

Let's say you want to append text to the end of an existing file. In 
that case, you must use `open()` with mode `at`. Let's see:

```python
>>> with open('datafile-copy', 'at') as f:
...     print("Python is easy!", file=f)
...
>>> with open('datafile-copy', 'rt') as f:
...     data = f.read()
...     print(data)
...
Python is fun!
Python is powerful!
Python is good for you!
Python is easy!
```

By default, files are read/written using the system default text 
encoding, as can be found in `sys.getdefaultencoding()`. On most 
machines, this is set to `utf-8`. If you know that the text you are 
reading or writing is in a different encoding, supply the optional 
encoding parameter to `open()`. For example:

```python
>>> with open('datafile-copy', 'rt', encoding='latin-1') as f:
...
```

Python understands several hundred possible text encodings. However, 
some of the more common encodings are `ascii`, `latin-1`, `utf-8`, 
and `utf-16`. UTF-8 is usually a safe bet if working with web 
applications. ASCII corresponds to the 7-bit characters in the range 
U+0000 to U+007F. Latin-1 is a direct mapping of bytes 0-255 to Unicode 
characters U+0000 to U+00FF. Latin-1 encoding is notable in that it will 
never produce a decoding error when reading text of a possibly unknown 
encoding. Reading a file as `latin-1` might not produce a completely 
correct text decoding, but it still might be enough to extract useful 
data out of it. Also, if you later write the data back out, the original 
input data will be preserved.

### Discussion

Reading and writing text files is typically very straightforward. 
However, there are a number of subtle aspects to keep in mind. First, 
the use of the `with` statement in the examples establishes a context in 
which the file will be used. When control leaves the `with` block, the 
file will be closed automatically. You don't need to use the `with` 
statement, but if you don't use it, make sure you remember to close the 
file:

```python
>>> f = open('datafile', 'rt')
>>> data = f.read()
>>> print(data)
  1 1050.000000
  2 1102.500000
  3 1157.625000
  4 1215.506250
  5 1276.281563
  6 1340.095641
  7 1407.100423
  8 1477.455444
  9 1551.328216
 10 1628.894627
 11 1710.339358
 12 1795.856326
 13 1885.649142
 14 1979.931599
 15 2078.928179
 16 2182.874588
 17 2292.018318
 18 2406.619234
 19 2526.950195
 20 2653.297705
 21 2785.962590
 22 2925.260720
 23 3071.523756
 24 3225.099944
 25 3386.354941

>>> f.close()
```

Another minor complication concerns the recognition of newlines, which 
are different on Unix and Windows (i.e., `\n` versus `\r\n`). By 
default, Python operates in what's known as "universal newline" mode. In 
this mode, all common newline conventions are recognized, and newline 
characters are converted to a single `\n` character while reading. 
Similarly, the newline character `\n` is converted to the system default 
newline character on output. If you don't want this translation, supply 
the `newline=''` argument to `open()`.

As an example, let's take a Windows-encoded text file 
(*python-phrases.txt*) and play a little with it:

```
Python is fun!
Python is powerful!
Python is good for you!
Python is easy!
```

Let's read the file with a enabled newline translation (default):

```python
>>> with open('python-phrases.txt', 'rt') as f:
...     f.read()
...
'Python is fun!\nPython is powerful!\nPython is good for you!\nPython is easy!\n'
```

The last part is the output you will see on a Unix machine if you read 
the file *python-phrases.txt*.

Now, let's read the file with a disabled newline translation:

```python
>>> with open('python-phrases.txt', 'rt', newline='') as f:
...     f.read()
...
'Python is fun!\r\nPython is powerful!\r\nPython is good for you!\r\nPython is easy!\r\n'
```

The last part is the output you will see on a Windows machine if you 
read the file *python-phrases.txt*.

A final issue concerns possible encoding errors in text files. When 
reading or writing a text file, you might encounter an encoding or 
decoding error. For instance:

```python
>>> with open('python-phrases.txt', 'rt', encoding='utf-16') as f:
...     f.read()
...
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
  File "/usr/local/lib/python3.6/codecs.py", line 321, in decode
    (result, consumed) = self._buffer_decode(data, self.errors, final)
  File "/usr/local/lib/python3.6/encodings/utf_16.py", line 61, in _buffer_decode
    codecs.utf_16_ex_decode(input, errors, 0, final)
UnicodeDecodeError: 'utf-16-le' codec can't decode byte 0x0a in position 78: truncated data
```

If you get this error, it usually means that you're not reading the file 
in the correct encoding. You should carefully read the specification of 
whatever it is that you're reading and check that you're doing it right 
(e.g., reading data as UTF-8 instead of Latin-1 or whatever it needs to 
be). If encoding errors are still a possibility, you can supply an
optional `errors` argument to `open()` to deal with the errors.

As an example, let's take a Windows-encoded text file 
(*cooking-ingredients.txt*) and play a little with it:

```
Spicy Jalapeño!
```

The first sample of common error handling schemes is presented below. 
There, we replace bad characters with Unicode U+fffd replacement 
character:

```python
>>> with open('cooking-ingredients.txt', 'rt', encoding='ascii', errors='replace') as f:
...     f.read()
...
'Spicy Jalape��o!\n'
```

The second sample of common error handling schemes is presented below. 
There, we ignore bad characters entirely:

```python
>>> with open('cooking-ingredients.txt', 'rt', encoding='ascii', errors='ignore') as f:
...     f.read()
...
'Spicy Jalapeo!\n'
```

If you're constantly fiddling with the `encoding` and `errors` arguments 
to `open()` and doing lots of hacks, you're probably making life more 
difficult than it needs to be. The number one rule with text is that you 
simply need to make sure you're always using the proper text encoding. 
When in doubt, use the default setting (typically UTF-8).
