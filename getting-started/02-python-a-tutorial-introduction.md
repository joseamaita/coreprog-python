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

### Variables and Arithmetic Expressions

The following program shows the use of variables and expressions by 
performing a simple compound-interest calculation. Let's see the code:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('   Simple Compound-Interest Calculation')
    print('-------------------------------------------')
    print()
    year = 0
    principal = 1000    # Initial amount
    print(f"Year={year}, Amount={principal}")
    rate = 0.05         # Interest rate
    numyears = 5        # Number of years
    year = 1
    while year <= numyears:
        principal = principal * (1 + rate)
        print(f"Year={year}, Amount={principal}")
        year += 1

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-------------------------------------------
   Simple Compound-Interest Calculation
-------------------------------------------

Year=0, Amount=1000
Year=1, Amount=1050.0
Year=2, Amount=1102.5
Year=3, Amount=1157.625
Year=4, Amount=1215.5062500000001
Year=5, Amount=1276.2815625000003
```

Python is a dynamically typed language where variable names are bound to 
different values, possibly of varying types, during program execution. 
The assignment operator simply creates an association between a name and 
a value. Although each value has an associated type such as an integer 
or string, variable names are untyped and can be made to refer to any 
type of data during execution. This is different from C, for example, in 
which a name represents a fixed type, size, and location in memory into 
which a value is stored. This dynamic behavior can be seen in the above 
code with the `principal` variable. Initially, it's assigned to an 
integer value. However, later in the program it's reassigned as follows:

```python
principal = principal * (1 + rate)
```

This statement evaluates the expression and reassociates the 
name `principal` with the result. Although the original value 
of `principal` was an integer `1000`, the new value is now a 
floating-point number ( `rate` is defined as a float, so the value of 
the above expression is also a float). Thus, the apparent "type" 
of `principal` dynamically changes from an integer to a float in the 
middle of the program. However, to be precise, it's not the type 
of `principal` that has changed, but rather the value to which 
the `principal` name refers.

A newline terminates each statement. However, you can use a semicolon to 
separate statements on the same line, as shown here:

```python
principal = 1000; rate = 0.05; numyears = 5;
```

Also, Python doesn't specify the amount of required indentation, as long 
as it's consistent within a block. However, it is most common (and 
generally recommended) to use **four spaces per indentation level**.

If you look the above output, you notice it isn't very configurable. To 
improve the output, you could right-align the columns and limit the 
precision of `principal` to two digits. There are several ways to 
achieve this formatting. Let's see:

```python
print(f"Year={year:3d}, Amount={principal:15.2f}")
```

Now, let's update the code:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('   Simple Compound-Interest Calculation')
    print('-------------------------------------------')
    print()
    year = 0
    principal = 1000    # Initial amount
    print(f"Year={year:3d}, Amount={principal:15.2f}")
    rate = 0.05         # Interest rate
    numyears = 5        # Number of years
    year = 1
    while year <= numyears:
        principal = principal * (1 + rate)
        print(f"Year={year:3d}, Amount={principal:15.2f}")
        year += 1

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-------------------------------------------
   Simple Compound-Interest Calculation
-------------------------------------------

Year=  0, Amount=        1000.00
Year=  1, Amount=        1050.00
Year=  2, Amount=        1102.50
Year=  3, Amount=        1157.62
Year=  4, Amount=        1215.51
Year=  5, Amount=        1276.28
```

Format strings contain ordinary text and special formatting-character 
sequences such as `d`, `s`, and `f`. These sequences specify the 
formatting of a particular type of data such as an integer, string, or 
floating-point number, respectively. The special-character sequences can 
also contain modifiers that specify a width and precision. For example
, `3d` formats an integer right-aligned in a column of width 3, 
and `15.2f` formats a floating-point number in a column of width 15, so 
that only two digits appear after the decimal point.

### Conditionals

The `if` and `else` statements can perform simple tests. Here's an 
example:

```python
if a < b:
    print("Computer says Yes")
else:
    print("Computer says No")
```

The bodies of the `if` and `else` clauses are denoted by indentation. 
The `else` clause is optional.

To create an empty clause, use the `pass` statement, as follows:

```python
if a < b:
    pass    # Do nothing
else:
    print("Computer says No")
```

You can form Boolean expressions by using the `or`, `and`, and `not` 
keywords:

```python
if product == "game" and type == "pirate memory" \
                     and not (age < 4 or age > 8):
    print("I'll take it!")
```

Please, notice that writing complex test cases commonly results in 
statements that involve an annoyingly long line of code. To improve 
readability, you can continue any statement to the next line by using a 
backslash `\` at the end of a line as shown. If you do this, the normal 
indentation rules don't apply to the next line, so you are free to 
format the continued lines as you wish.

Keep in mind that Python does not have a special **switch** or **case** 
statement for testing values. To handle multiple-test cases, use 
the `elif` statement, like this:

```python
if suffix == ".htm":
    content = "text/html"
elif suffix == ".jpg":
    content = "image/jpeg"
elif suffix == ".png":
    content = "image/png"
else:
    raise RuntimeError("Unknown content type")
```

Also, other methods or workarounds are available to handle multiple-test 
cases such as:

* Switch/case with dictionary mapping.
* Switch/case with dictionary mapping for functions.
* Switch/case with dispatch methods for classes.

To denote truth values, use the Boolean values `True` and `False`. 
Here's an example:

```python
if 'spam' in s:
    has_spam = True
else:
    has_spam = False
```

All relational operators such as `<` and `>` return `True` or `False` as 
results. The `in` operator used in this example is commonly used to 
check whether a value is contained inside of another object such as a 
string, list, or dictionary. It also returns `True` or `False`, so the 
preceding example could be shortened to this:

```python
has_spam = 'spam' in s
```
