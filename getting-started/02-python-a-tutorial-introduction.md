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

### File Input and Output

Suppose that you have a data file named `datafile` like this one:

```
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

This program opens a data file and reads its contents line by line:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('          Read Data File')
    print('-------------------------------------------')
    print()
    f = open("datafile")    # Returns a file object
    line = f.readline()    # Invokes readline() method on file
    while line:
        print(line, end='')
        line = f.readline()
    f.close()    # Close the file object

if __name__ == '__main__':
    main()
```

The `open()` function returns a new file object. By invoking methods on 
this object, you can perform various file operations. The `readline()` 
method reads a single line of input, including the terminating newline. 
The empty string is returned at the end of the file.

In the example, the program is simply looping over all the lines in the 
file `datafile`. Whenever a program loops over a collection of data like 
this (for instance input lines, numbers, strings, etc.), it is commonly 
known as *iteration*. Because iteration is such a common operation, 
Python provides a dedicated statement, `for`, that is used to iterate 
over items. For instance, the same program can be written much more 
succinctly as follows:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('          Read Data File')
    print('-------------------------------------------')
    print()
    f = open("datafile")
    for line in f:
        print(line, end='')
    f.close()

if __name__ == '__main__':
    main()
```

To make the output of a program go to a file named `datafile-02`, you 
can supply a file to the `print` statement, as shown in the following 
example:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('          Write Data File')
    print('-------------------------------------------')
    print()
    principal = 1000
    rate = 0.05
    numyears = 25
    year = 1
    f = open("datafile-02", "w")
    while year <= numyears:
        principal = principal * (1 + rate)
        print(f"{year:3d} {principal:0.2f}", file=f)
        year += 1
    f.close()

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
  1 1050.00
  2 1102.50
  3 1157.62
  4 1215.51
  5 1276.28
  6 1340.10
  7 1407.10
  8 1477.46
  9 1551.33
 10 1628.89
 11 1710.34
 12 1795.86
 13 1885.65
 14 1979.93
 15 2078.93
 16 2182.87
 17 2292.02
 18 2406.62
 19 2526.95
 20 2653.30
 21 2785.96
 22 2925.26
 23 3071.52
 24 3225.10
 25 3386.35
```

In addition, file objects support a `write()` method that can be used to 
write raw data. For example, the `print` statement in the previous 
example could have been written this way:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('          Write Data File')
    print('-------------------------------------------')
    print()
    principal = 1000
    rate = 0.05
    numyears = 25
    year = 1
    f = open("datafile-02", "w")
    while year <= numyears:
        principal = principal * (1 + rate)
        f.write(f"{year:3d} {principal:0.2f}\n")
        year += 1
    f.close()

if __name__ == '__main__':
    main()
```

Although these examples have worked with files, the same techniques 
apply to the standard output and input streams of the interpreter. For 
example, if you wanted to read user input interactively, you can read 
from the file `sys.stdin`. If you want to write data to the screen, you 
can write to `sys.stdout`, which is the same file used to output data 
produced by the `print` statement. For example:

```python
#!/usr/bin/env python3
import sys

def main():
    print('---------------------------------------------------')
    print('Read and Write from the Standard Input and Output')
    print('---------------------------------------------------')
    print()
    sys.stdout.write("Enter your name: \n")
    name = sys.stdin.readline().strip()
    print(f"\nHello, {name}!\n")

if __name__ == '__main__':
    main()
```

This code can also be shortened to the following:

```python
#!/usr/bin/env python3

def main():
    print('---------------------------------------------------')
    print('Read and Write from the Standard Input and Output')
    print('---------------------------------------------------')
    print()
    name = input("Enter your name: \n")
    print(f"\nHello, {name}!\n")

if __name__ == '__main__':
    main()
```

### Strings

Create strings like this:

```python
a = "Hello, World!"
b = 'Life is beautiful'
c = """The area of 'Data Structures and Algorithms in Python' is nice"""
```

The same type of quote used to start a string must be used to terminate 
it. The use of triple-quoted strings allow us to capture all the text 
that appears prior to the terminating triple quote, as opposed to single 
and double quoted strings, which must be specified on one logical line. 
Triple-quoted strings are useful when the contents of a string literal 
span multiple lines of text such as the following:

```python
print("""<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, 
        initial-scale=1.0">""")
```

Strings are immutable. The operators and functions that work with them 
return new strings derived from the original. The operators ( `in`, `+`, 
and `*` ) and built-in functions ( `len`, `max`, and `min` ) operate on 
strings as they do on lists and tuples. Index and slice notation works 
the same for obtaining elements or slices but can't be used to add, 
remove, or replace elements.

Strings are stored as sequences of characters indexed by integers, 
starting at zero (0). To extract a single character, use the indexing 
operator `s[i]` like this:

```python
>>> s = "Life is beatiful"
>>> s[0]
'L'
>>> s[1]
'i'
>>> s[2]
'f'
>>> s[3]
'e'
```

To extract a substring, use the slicing operator `s[i:j]`. This extracts 
all characters from `s` whose index `k` is in the range `i <= k < j`. If 
either index is omitted, the beginning or end of the string is assumed, 
respectively:

```python
>>> s = "Life is beatiful"
>>> s[:4]
'Life'
>>> s[5:]
'is beatiful'
>>> s[5:7]
'is'
```

If you want to concatenate strings, use the plus ( `+` ) operator:

```python
>>> s = "Life is beatiful"
>>> s + " and exciting"
'Life is beatiful and exciting'
```

Python never implicitly interprets the contents of a string as numerical 
data. For example, `+` always concatenates strings:

```python
>>> x = "49"
>>> y = "26"
>>> x + y
'4926'
```

To perform mathematical calculations, strings first have to be converted 
into a numeric value using a function such as `int()` or `float()`. For 
example:

```python
>>> x = "49"
>>> y = "26"
>>> int(x) + int(y)
75
>>> float(x) + float(y)
75.0
```

Non-string values can be converted into a string representation by using 
the `str()`, `repr()` or `f-strings` functions. See how this works:

```python
>>> x = 49
>>> "The value of x is " + str(x)
'The value of x is 49'
>>> "The value of x is " + repr(x)
'The value of x is 49'
>>> f"The value of x is {x}"
'The value of x is 49'
>>> f"The value of x is {x:5d}"
'The value of x is    49'
```

Although `str()` and `repr()` both create strings, their output is 
usually slightly different. `str()` produces the output that you get 
when you use the `print` statement, whereas `repr()` creates a string 
that you type into a program to exactly represent the value of an 
object.

The `f-string` function is used to convert a value to a string with a 
specific formatting applied. For example:

```python
>>> x = 49
>>> f"{x:0.6f}"
'49.000000'
```

### Lists

*Lists* are sequences of arbitrary objects. You create a list by 
enclosing values in square brackets `[]` or using the `list` type 
function:

```python
>>> names_a = ["Peter", "Dalia", "Johnny", "Rick"]
>>> names_a
['Peter', 'Dalia', 'Johnny', 'Rick']
>>> names_b = list(("Peter", "Dalia", "Johnny", "Rick"))
>>> names_b
['Peter', 'Dalia', 'Johnny', 'Rick']
```

Lists are indexed by integers, starting with zero. Use the indexing 
operator to access and modify individual items of the list:

```python
>>> n = names_a[2]
>>> n
'Johnny'
>>> names_a[0] = "Jeffrey"
>>> names_a
['Jeffrey', 'Dalia', 'Johnny', 'Rick']
```

The `list` function is frequently used in data processing as a way to 
materialize an iterator or generator expression:

```python
>>> gen = range(10)
>>> gen
range(0, 10)
>>> list(gen)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

To append new items to the end of a list, use the `append()` method:

```python
>>> names_a.append("Tristan")
>>> names_a
['Jeffrey', 'Dalia', 'Johnny', 'Rick', 'Tristan']
```

To insert an item into a specific position of a list, use the `insert()` 
method:

```python
>>> names_a.insert(1, "Sue")
>>> names_a
['Jeffrey', 'Sue', 'Dalia', 'Johnny', 'Rick', 'Tristan']
```

Notice this: the `insert` method is computationally expensive compared 
with `append`, because references to subsequent elements have to be 
shifted internally to make room for the new element. If you need to 
insert elements at both the beginning and end of a sequence, you may 
wish to explore `collections.deque`, a double-ended queue, for this 
purpose.

The inverse operation to `insert` is `pop`, which removes and returns an 
element at a particular index:

```python
>>> names_b
['Peter', 'Dalia', 'Johnny', 'Rick']
>>> names_b.pop(1)
'Dalia'
>>> names_b
['Peter', 'Johnny', 'Rick']
```

Elements can be removed by value with `remove`, which locates the first 
such value and removes it from the last:

```python
>>> names_b.remove("Peter")
>>> names_b
['Johnny', 'Rick']
```

If performance is not a concern, by using `append` and `remove`, you can 
use a Python list as a perfectly suitable "multiset" data structure.

Check if a list contains a value using the `in` keyword:

```python
>>> "Rick" in names_a
True
```

The keyword `not` can be used to negate `in`:

```python
>>> "Rick" not in names_a
False
```

Checking whether a list contains a value is a lot slower than doing so 
with dicts and sets, as Python makes a linear scan across the values of 
the list, whereas it can check the others (based on hash tables) in 
constant time.

To add two lists together, use the plus ( `+` ) operator:

```python
>>> [4, None, 'foo'] + [7, 8, (2, 3)]
[4, None, 'foo', 7, 8, (2, 3)]
```

If you have a list already defined, you can append multiple elements to 
it using the `extend` method:

```python
>>> x = [4, None, 'foo']
>>> x.extend([7, 8, (2, 3)])
>>> x
[4, None, 'foo', 7, 8, (2, 3)]
```

Note that list concatenation by addition is a comparatively expensive 
operation since a new list must be created and the objects copied over. 
Using `extend` to append elements to an existing list, especially if you 
are building up a large list, is usually preferable.

You can sort a list in-place (without creating a new object) by calling 
its `sort` function:

```python
>>> a = [7, 2, 5, 1, 3]
>>> a.sort()
>>> a
[1, 2, 3, 5, 7]
```

The `sort` function has a few options that will occasionally come in 
handy. One is the ability to pass a secondary *sort* key, that is, a 
function that produces a value to use to sort the objects. For example, 
we could sort a collection of strings by their lengths:

```python
>>> b = ['saw', 'small', 'He', 'foxes', 'six']
>>> b.sort(key=len)
>>> b
['He', 'saw', 'six', 'small', 'foxes']
```

You can extract or reassign a portion of a list by using the slicing 
operator:

```python
>>> names_a[:2]
['Jeffrey', 'Sue']
>>> names_a[2:]
['Dalia', 'Johnny', 'Rick', 'Tristan']
>>> names_a[-3:]
['Johnny', 'Rick', 'Tristan']
>>> names_a[1] = "Homer"
>>> names_a
['Jeffrey', 'Homer', 'Dalia', 'Johnny', 'Rick', 'Tristan']
>>> names_a[:2] = ["Keith", "Brandon", "Mark"]
>>> names_a
['Keith', 'Brandon', 'Mark', 'Dalia', 'Johnny', 'Rick', 'Tristan']
```

A step can also be used after a second colon to, say, take every other 
element:

```python
>>> names_a[::2]
['Keith', 'Mark', 'Johnny', 'Tristan']
```

A clever use of this is to pass `-1`, which has the useful effect of 
reversing a list or tuple:

```python
>>> names_a[::-1]
['Tristan', 'Rick', 'Johnny', 'Dalia', 'Mark', 'Brandon', 'Keith']
```

Create an empty list in these two ways:

```python
>>> names_c = []
>>> names_c
[]
>>> names_d = list()
>>> names_d
[]
```

Lists can contain any kind of Python object, including other lists:

```python
>>> a = [22, "Louie", 9.81, ["C.K.", 6, 8, [200, 300]], 29]
>>> a
[22, 'Louie', 9.81, ['C.K.', 6, 8, [200, 300]], 29]
```

Items contained in nested lists are accessed by applying more than one 
indexing operation:

```python
>>> a[2]
9.81
>>> a[3][0]
'C.K.'
>>> a[3][3][0]
200
```
