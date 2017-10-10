# Getting Started with Python

## A Tutorial Introduction

Quick introduction to Python and illustrate its most essential features.

### Running Python

Python programs are executed by an interpreter. Usually, the interpreter 
is started by simply typing `python`, `python3` or `python3.6` into a 
command shell. When the interpreter starts, a prompt appears at which 
you can start typing programs into a simple read-evaluation loop.

```
$ workon py360core
(py360core) $ python
Python 3.6.0 (default, Jan 25 2017, 23:55:25) 
[GCC 4.9.2] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello, World!")
Hello, World!
>>>
<Ctrl+D>
```

See this example of Python's interactive mode as a desktop calculator, 
which is one of its most useful features. For instance:

```python
>>> 6000 + 4523.50 + 134.12
10657.62
>>> _ + 8192.32
18849.940000000002
>>>
```

The special variable `_` holds the result of the last operation. This 
can be useful if you want to save or use the result of the last 
operation in subsequent statements.

If you want to create a program that you can run repeatedly, put 
statements in a file such as the following:

```python
# helloworld.py
print("Hello, World!")
```

To execute the `helloworld.py` file, you provide the filename to the 
interpreter as follows:

```
(py360core) $ python helloworld.py
Hello, World!
```

On UNIX, you can use `#!` on the first line of the program, like 
this `#!/usr/bin/env python3`.

The interpreter runs statements until it reaches the end of the input 
file. If it's running interactively, you can exit the interpreter by 
typing the EOF (end of file) character or by selecting **Exit** from 
pull-down menu of a Python IDE. On UNIX, EOF is **<Ctrl+D>**; on 
Windows, it's **<Ctrl+Z> (or F6)**. A program can request to exit by 
raising the **SystemExit** exception.

```python
>>> raise SystemExit
```
