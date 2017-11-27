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

### Tuples

To create simple data structures, you can pack a collection of values 
together into a single object using a *tuple*, a fixed-length, immutable 
sequence. You create a tuple in different ways:

* The easiest way is with a comma-separated sequence of values.
* By enclosing a group of values in parentheses `()`.
* By using the `tuple` type function.

```python
>>> names_a = "Peter", "Dalia", "Johnny", "Rick"
>>> names_a
('Peter', 'Dalia', 'Johnny', 'Rick')
>>> stock = ('CNTV', 100, 126.84)
>>> stock
('CNTV', 100, 126.84)
>>> address = tuple(['www.python.org', 80])
>>> address
('www.python.org', 80)
```

Notice that Python often recognizes that a tuple is intended even if the 
parentheses are missing:

```python
>>> stock = 'CNTV', 100, 126.84
>>> stock
('CNTV', 100, 126.84)
>>> address = 'www.python.org', 80
>>> address
('www.python.org', 80)
>>> person = "Bob", "Jones", "555-7698"
>>> person
('Bob', 'Jones', '555-7698')
```

Tuples of 0 (empty) and 1-element have to be defined like this:

```python
>>> a = ()
>>> a
()
>>> b
(71,)
>>> b = 71,
>>> b
(71,)
```

The values in a tuple can be extracted by numerical index just like a 
list. However, it is more common to unpack tuples into a set of 
variables:

```python
>>> stock = ('CNTV', 100, 126.84)
>>> name, shares, price = stock
>>> name
'CNTV'
>>> shares
100
>>> price
126.84
>>> address = ('www.python.org', 80)
>>> host, port = address
>>> host
'www.python.org'
>>> port
80
>>> person = "Bob", "Jones", "555-7698"
>>> first_name, last_name, phone = person
>>> first_name
'Bob'
>>> last_name
'Jones'
>>> phone
'555-7698'
```

Using this functionality you can easily swap variable names, a task 
which in many languages might look like:

```
tmp = a
a = b
b = tmp
```

But, in Python, the swap can be done like this:

```python
>>> a, b = ("foo", "bar")
>>> a
'foo'
>>> b
'bar'
>>> b, a = a, b
>>> a
'bar'
>>> b
'foo'
```

A common use of variable unpacking is iterating over sequences of tuples 
or lists:

```python
>>> seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
>>> seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
>>> for a, b, c in seq:
...     print(f"a={a}, b={b}, c={c}")
... 
a=1, b=2, c=3
a=4, b=5, c=6
a=7, b=8, c=9
```

A more advanced tuple unpacking would help with situations where you may 
want to "pluck" a few elements from the beginning of a tuple. This uses 
the special syntax `*rest`, which is also used in function signatures to 
capture an arbitrarily long list of positional arguments:

```python
>>> values = (1, 2, 3, 4, 5)
>>> a, b, *rest = values
>>> a
1
>>> b
2
>>> rest
[3, 4, 5]
```

This `rest` bit is sometimes something you want to discard; there is 
nothing special about the `rest` name. As a matter of convention, many 
Python programmers will use the underscore ( `_` ) for unwanted 
variables:

```python
>>> values = (1, 2, 3, 4, 5)
>>> a, b, *_ = values
>>> a
1
>>> b
2
>>> _
[3, 4, 5]
```

Another common use is returning multiple values from a function. Let's 
see:

```python
>>> a1 = 5
>>> x1 = 14
>>> def add_numbers(a, x):
...     return a, x, a + x
...
>>> add_numbers(a1, x1)
(5, 14, 19)
```

Although tuples support most of the same operations as lists (such as 
indexing, slicing, and concatenation), the contents of a tuple cannot be 
modified after creation (that is, you cannot replace, delete, or append 
new elements to an existing tuple). This reflects the fact that a tuple 
is best viewed as a single object consisting of several parts, not as a 
collection of distinct objects to which you might insert or remove 
items.

Let's see this on the interpreter:

```python
>>> tup = tuple(['foo', [1, 2], True])
>>> tup[2] = False
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

If an object inside a tuple is mutable, such as a list, you can modify 
it in-place:

```python
>>> tup[1].append(3)
>>> tup
('foo', [1, 2, 3], True)
```

You can concatenate tuples using the `+` operator to produce longer 
tuples:

```python
>>> (4, None, 'foo') + (6, 0) + ('bar',)
(4, None, 'foo', 6, 0, 'bar')
```

Multiplying a tuple by an integer, as with lists, has the effect of 
concatenating together that many copies of the tuple:

```python
>>> ('foo', 'bar') * 4
('foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'bar')
```

Note that the objects themselves are not copied, only the references to 
them.

Since the size and contents of a tuple cannot be modified, it is very 
light on instance methods. A particularly useful one (also available on 
lists) is `count`, which counts the number of occurrences of a value:

```python
>>> a = (1, 2, 2, 2, 3, 4, 2)
>>> a.count(4)
1
>>> a.count(2)
4
```

Because there is so much overlap between tuples and lists, some 
programmers are inclined to ignore tuples altogether and simply use 
lists because they seem to be more flexible. Although this works, it 
wastes memory if your program is going to create a large number of small 
lists (that is, each containing fewer than a dozen items). This is 
because lists slightly overallocate memory to optimize the performance 
of operations that add new items. Because tuples are immutable, they use 
a more compact representation where there is no extra space.

Tuples and lists are often used together to represent data. For example, 
this program shows how you might read a file consisting of different 
columns of data separated by commas. The datafile 
named `datafile-03.csv` has this structure:

```
CNTV,100,126.84
PLTR,250,321.78
PDVS,400,1007.87
SIDR,125,32.46
ALSA,110,15.45
```

The script is:

```python
#!/usr/bin/env python3
# File containing lines of the form "name,shares,price"
filename = "datafile-03.csv"
portfolio = []

def print_portfolio(portfolio):
    print(f"portfolio[0]: {portfolio[0]}")
    print(f"portfolio[1]: {portfolio[1]}")
    print(f"portfolio[2][1]: {portfolio[2][1]}")
    print(f"portfolio[3][2]: {portfolio[3][2]}")
    print(f"portfolio[4]: {portfolio[4]}")

def main():
    print('------------------------------------------------------')
    print(' Read a File with Columns of Data Separated by Commas ')
    print('------------------------------------------------------')
    print()
    with open(filename) as f:
        for line in f:
            fields = line.split(",")    # Split each line into a list
            name = fields[0]    # Extract and convert individual fields
            shares = int(fields[1])
            price = float(fields[2])
            stock = (name, shares, price)    # Create a tuple 
                                             # (name, shares, price)
            portfolio.append(stock)    # Append to list of records
        print_portfolio(portfolio)

if __name__ == '__main__':
    main()
```

The `split()` method of strings splits a string into a list of fields 
separated by the given delimiter character. The resulting `portfolio` 
data structure created by this program looks like a two-dimension array 
of rows and columns. Each row is represented by a tuple and individual 
items of data can be accessed too.

After running the script, the output is:

```
------------------------------------------------------
 Read a File with Columns of Data Separated by Commas 
------------------------------------------------------

portfolio[0]: ('CNTV', 100, 126.84)
portfolio[1]: ('PLTR', 250, 321.78)
portfolio[2][1]: 400
portfolio[3][2]: 32.46
portfolio[4]: ('ALSA', 110, 15.45)
```

Here's an easy way to loop over all of the records and expand fields 
into a set of variables:

```python
#!/usr/bin/env python3
# File containing lines of the form "name,shares,price"
filename = "datafile-03.csv"
portfolio = []

def print_portfolio(portfolio):
    print(f"portfolio[0]: {portfolio[0]}")
    print(f"portfolio[1]: {portfolio[1]}")
    print(f"portfolio[2][1]: {portfolio[2][1]}")
    print(f"portfolio[3][2]: {portfolio[3][2]}")
    print(f"portfolio[4]: {portfolio[4]}")

def main():
    print('------------------------------------------------------')
    print(' Read a File with Columns of Data Separated by Commas ')
    print('------------------------------------------------------')
    print()
    with open(filename) as f:
        for line in f:
            fields = line.split(",")    # Split each line into a list
            name = fields[0]    # Extract and convert individual fields
            shares = int(fields[1])
            price = float(fields[2])
            stock = (name, shares, price)    # Create a tuple 
                                             # (name, shares, price)
            portfolio.append(stock)    # Append to list of records
        print_portfolio(portfolio)
        total = 0.0
        for name, shares, price in portfolio:
            total += shares * price
        print(f"The total amount of money that you have is {total} $")

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
------------------------------------------------------
 Read a File with Columns of Data Separated by Commas 
------------------------------------------------------

portfolio[0]: ('CNTV', 100, 126.84)
portfolio[1]: ('PLTR', 250, 321.78)
portfolio[2][1]: 400
portfolio[3][2]: 32.46
portfolio[4]: ('ALSA', 110, 15.45)
The total amount of money that you have is 502034.0 $
```

### Built-In Sequence Functions

Python has a handful of useful sequence functions that you should 
familiarize yourself with and use at any opportunity.

**enumerate**

It's common when iterating over a sequence to want to keep track of the 
index of the current item. A do-it-yourself approach would look like:

```python
i = 0
for value in collection:
    # do something with value
    i += 1
```

Since this is so common, Python has a built-in function, `enumerate`, 
which returns a sequence of `(i, value)` tuples:

```python
for i, value in enumerate(collection):
    # do something with value
```

When you are indexing data, a helpful pattern that uses `enumerate` is 
computing a `dict` mapping the values of a sequence (which are assumed 
to be unique) to their locations in the sequence:

```python
>>> a_list = ['foo', 'bar', 'baz']
>>> mapping = {}
>>> for i, value in enumerate(a_list):
...     mapping[value] = i
... 
>>> mapping
{'foo': 0, 'bar': 1, 'baz': 2}
```

**sorted**

The `sorted` function returns a new sorted list from the elements of any 
sequence:

```python
>>> sorted([7, 1, 2, 6, 0, 3, 2])
[0, 1, 2, 2, 3, 6, 7]
>>> sorted('horse race')
[' ', 'a', 'c', 'e', 'e', 'h', 'o', 'r', 'r', 's']
```

The `sorted` function accepts the same arguments as the `sort` method on 
lists.

**zip**

The `zip` function "pairs" up the elements of a number of lists, tuples, 
or other sequences to create a list of tuples:

```python
>>> seq_1 = ['foo', 'bar', 'baz']
>>> seq_2 = ['one', 'two', 'three']
>>> zipped = zip(seq_1, seq_2)
>>> list(zipped)
[('foo', 'one'), ('bar', 'two'), ('baz', 'three')]
```

The `zip` function can take an arbitrary number of sequences, and the 
number of elements it produces is determined by the *shortest* sequence:

```python
>>> seq_3 = [False, True]
>>> list(zip(seq_1, seq_2, seq_3))
[('foo', 'one', False), ('bar', 'two', True)]
```

A very common use of `zip` is simultaneously iterating over multiple 
sequences, possibly also combined with `enumerate`:

```python
>>> for i, (a, b) in enumerate(zip(seq_1, seq_2)):
...     print(f"{i}: {a}, {b}")
... 
0: foo, one
1: bar, two
2: baz, three
```

Given a "zipped" sequence, `zip` can be applied in a clever way to 
"unzip" the sequence. Another way to think about this is converting a 
list of *rows* into a list of *columns*. The syntax, which looks a bit 
magical, is:

```python
>>> users = [('David', 'Jones'), ('Mike', 'Parker'), ('Trent', 'Bay')]
>>> first_names, last_names = zip(*users)
>>> first_names
('David', 'Mike', 'Trent')
>>> last_names
('Jones', 'Parker', 'Bay')
```

**reversed**

The `reversed` function iterates over the elements of a sequence in 
reverse order:

```python
>>> list(reversed(range(10)))
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

Keep in mind that `reversed` is a generator, so it does not create the 
reversed sequence until materialized (e.g., with `list` or a `for` 
loop).

### Sets

A *set* is used to contain an unordered collection of unique objects. To 
create a set, use the `set()` function and supply a sequence of items or 
via a *set literal* with curly braces `{}`:

```python
>>> set_1 = set([3, 5, 9, 10])
>>> set_1
{9, 10, 3, 5}
>>> set_2 = set([2, 2, 2, 1, 3, 3])
>>> set_2
{1, 2, 3}
>>> set_3 = set("Hello")
>>> set_3
{'H', 'l', 'e', 'o'}
>>> set_4 = {2, 2, 2, 1, 3, 3}
>>> set_4
{1, 2, 3}
```

Unlike lists and tuples, sets are unordered and cannot be indexed by 
numbers. Moreover, the elements of a set are never duplicated. Notice 
above that only one `'l'` appears.

Sets support mathematical *set operations*, including union, 
intersection, difference, and symmetric difference. Consider these two 
example sets:

```python
>>> a = {1, 2, 3, 4, 5}
>>> b = {3, 4, 5, 6, 7, 8}
```

The union of these two sets is the set of distinct elements occurring in 
either set. This can be computed with either the `union` method or 
the `|` binary operator:

```python
>>> a.union(b)
{1, 2, 3, 4, 5, 6, 7, 8}
>>> a | b
{1, 2, 3, 4, 5, 6, 7, 8}
```

The intersection contains the elements occurring in both sets. The `&` 
operator or the `intersection` method can be used:

```python
>>> a.intersection(b)
{3, 4, 5}
>>> a & b
{3, 4, 5}
```

The difference contains the elements in one set, but not the other. 
The `-` operator or the `difference` method can be used:

```python
>>> a.difference(b)
{1, 2}
>>> a - b
{1, 2}
```

The symmetric difference contains the elements in either set but not 
both. The `^` operator or the `symmetric_difference` method can be used:

```python
>>> a.symmetric_difference(b)
{1, 2, 6, 7, 8}
>>> a ^ b
{1, 2, 6, 7, 8}
```

New items can be added to a set using `add()` or `update()` methods:

```python
>>> a.add(9)
>>> a
{1, 2, 3, 4, 5, 9}
>>> b.update([10, 37, 42])
>>> b
{3, 4, 5, 6, 7, 8, 37, 10, 42}
```

An item can be removed using `remove()`:

```python
>>> b.remove(42)
>>> b
{3, 4, 5, 6, 7, 8, 37, 10}
```

All of the logical set operations have in-place counterparts, which 
enable you to replace the contents of the set on the left side of the 
operation with the result. For very large sets, this may be more 
efficient:

```python
>>> c = a.copy()
>>> c
{1, 2, 3, 4, 5, 9}
>>> c |= b
>>> c
{1, 2, 3, 4, 5, 6, 7, 8, 9, 37, 10}
>>> d = a.copy()
>>> d &= b
>>> d
{3, 4, 5}
```

Set elements generally must be immutable. To have list-like elements, 
you must convert it to a tuple:

```python
>>> data = [6, 7, 8, 9]
>>> set_1 = {tuple(data)}
>>> set_1
{(6, 7, 8, 9)}
```

You can also check if a set is a subset of (is contained in) or a 
superset of (contains all elements of) another set:

```python
>>> set_2 = {1, 2, 3, 4, 5}
>>> {1, 2, 3}.issubset(set_2)
True
>>> set_2.issuperset({1, 2, 3})
True
```

Sets are equal if and only if their contents are equal:

```python
>>> {1, 2, 3} == {3, 2, 1}
True
```

### Dictionaries

The `dict` object is likely the most important built-in Python data 
structure. Common names for it are *hash map*, *hash table* 
or *associative array*. A *dictionary* contains objects indexed by keys. 
Another definition could be that they contain a flexibly sized 
collection of *key-value* pairs, where *key* and *value* are Python 
objects.

To create a dictionary, use the `dict({})` function or use curly 
braces `{}` and colons `:` to separate keys and values, like this:

```python
>>> stock = {"name": "CNTV", "shares": 100, "price": 126.84}
>>> stock
{'name': 'CNTV', 'shares': 100, 'price': 126.84}
>>> dict_1 = dict({"a": "some value", "b": [1, 2, 3, 4]})
>>> dict_1
{'a': 'some value', 'b': [1, 2, 3, 4]}
```

An empty dictionary is created in one of two ways:

```python
>>> prices_1 = {}
>>> prices_1
{}
>>> prices_2 = dict()
>>> prices_2
{}
```

To access members of a dictionary, use the key-indexing operator:

```python
>>> stock['name']
'CNTV'
>>> stock['shares']
100
>>> stock['price']
126.84
>>> value = stock['shares'] * stock['price']
>>> value
12684.0
```

Modify or insert objects by doing this:

```python
>>> stock['shares'] = 125
>>> value = stock['shares'] * stock['price']
>>> stock['value'] = value
>>> stock['date'] = "February 4, 2014"
>>> stock
{'name': 'CNTV', 'shares': 125, 'price': 126.84, 'value': 15855.0, 'date': 'February 4, 2014'}
```

Although strings are the most common type of key, you can use many other 
Python objects, including numbers and tuples. Some objects, including 
lists and dictionaries, cannot be used as keys because their contents 
can change.

A dictionary is a useful way to define an object that consists of named 
fields as shown previously. However, dictionaries are also used as a 
container for performing fast lookups on unordered data. Let's see a 
dictionary of stock prices:

```python
>>> prices = {"CNTV": 126.84, "PLTR": 321.78, "PDVS": 1007.87, "SIDR": 32.46, "ALSA": 15.45}
>>> prices
{'CNTV': 126.84, 'PLTR': 321.78, 'PDVS': 1007.87, 'SIDR': 32.46, 'ALSA': 15.45}
```

Dictionary membership is tested with the `in` operator:

```python
if "VELM" in prices:
    p = prices["VELM"]
else:
    p = 0.0
```

This particular sequence of steps can also be performed more compactly 
like this:

```python
>>> p = prices.get("VELM", 0.0)
>>> p
0.0
>>> p = prices.get("PLTR", 0.0)
>>> p
321.78
```

You can delete values either using the `del` statement or the `pop` 
method (which simultaneously returns the value and deletes the key):

```python
>>> prices['FMO'] = 334.78
>>> prices
{'CNTV': 126.84, 'PLTR': 321.78, 'PDVS': 1007.87, 'SIDR': 32.46, 'ALSA': 15.45, 'FMO': 334.78}
>>> del prices['ALSA']
>>> prices
{'CNTV': 126.84, 'PLTR': 321.78, 'PDVS': 1007.87, 'SIDR': 32.46, 'FMO': 334.78}
>>> prices.pop('SIDR')
32.46
>>> prices
{'CNTV': 126.84, 'PLTR': 321.78, 'PDVS': 1007.87, 'FMO': 334.78}
```

To obtain a list of dictionary keys, convert a dictionary to a list:

```python
>>> syms = list(prices)
>>> syms
['CNTV', 'PLTR', 'PDVS', 'FMO']
```

The `keys` and `values` method give you iterators of the dictionary's 
keys and values, respectively. While the key-value pairs are not in any 
particular order, these functions output the keys and values in the same 
order:

```python
>>> list(prices.keys())
['CNTV', 'PLTR', 'PDVS', 'FMO']
>>> list(prices.values())
[126.84, 321.78, 1007.87, 334.78]
```

You can merge one dictionary into another using the `update` method:

```python
>>> prices.update({"BAUX": 44.98, "VENO": 227.51})
>>> prices
{'CNTV': 126.84, 'PLTR': 321.78, 'PDVS': 1007.87, 'FMO': 334.78, 'BAUX': 44.98, 'VENO': 227.51}
```

The `update` method changes dictionaries in-place, so any existing keys 
in the data passed to `update` will have their old values discarded.

**Creating dictionaries from sequences**

It's common to occasionally end up with two sequences that you want to 
pair up element-wise in a dictionary. As a first cut, you might write 
code like this:

```python
mapping = {}
for key, value in zip(key_list, value_list):
    mapping[key] = value
```

Since a dictionary is essentially a collection of 2-tuples, the `dict` 
function accepts a list of 2-tuples:

```python
>>> mapping = dict(zip(range(5), reversed(range(5))))
>>> mapping
{0: 4, 1: 3, 2: 2, 3: 1, 4: 0}
```

**Default values**

It's very common to have logic like:

```python
if key in some_dict:
    value = some_dict[key]
else:
    value = default_value
```

Thus, the dictionary methods `get` and `pop` can take a default value to 
be returned, so that the above `if-else` block can be written simply as:

```python
value = some_dict.get(key, default_value)
```

The `get` method by default will return `None` if the key is not 
present, while the `pop` method will raise an exception. With *setting* 
values, a common case is for the values in a dictionary to be other 
collections, like lists. For example, you could imagine categorizing a 
list of words by their first letters as a dictionary of lists:

```python
>>> words = ['apple', 'bat', 'bar', 'atom', 'book']
>>> by_letter = {}
>>> for word in words:
...     letter = word[0]
...     if letter not in by_letter:
...         by_letter[letter] = [word]
...     else:
...         by_letter[letter].append(word)
>>> by_letter
{'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}
```

The `setdefault` dictionary method is for precisely this purpose. The 
preceding `for` loop can be rewritten as:

```python
>>> for word in words:
...     letter = word[0]
...     by_letter.setdefault(letter, []).append(word)
... 
>>> by_letter
{'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}
```

The built-in `collections` module has a useful class, `defaultdict`, 
which makes this even easier. To create one, you pass a type or function 
for generating the default value for each slot in the dictionary:

```python
>>> from collections import defaultdict
>>> by_letter = defaultdict(list)
>>> for word in words:
...     by_letter[word[0]].append(word)
... 
>>> by_letter
defaultdict(<class 'list'>, {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']})
>>> by_letter['a']
['apple', 'atom']
>>> by_letter['b']
['bat', 'bar', 'book']
```

**Valid dictionary key types**

While the values of a dictionary can be any Python object, the keys 
generally have to be immutable objects like scalar types (int, float, 
string) or tuples (all the objects in the tuple need to be immutable, 
too). The technical term here is *hashability*. You can check whether an 
object is hashable (can be used as a key in a dictionary) with 
the `hash` function:

```python
>>> hash('string')
-889191027928915186
>>> hash((1, 2, (2, 3)))
1097636502276347782
>>> hash((1, 2, [2, 3]))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

To use a list as a key, one option is to convert it to a tuple, which 
can be hashed as long as its elements also can:

```python
>>> d = {}
>>> d[tuple([1, 2, 3])] = 5
>>> d
{(1, 2, 3): 5}
```

Dictionaries are probably the most finely tuned data type in the Python 
interpreter. So, if you are merely trying to store and work with data in 
your program, you are almost always better off using a dictionary than 
trying to come up with some kind of custom data structure on your own.

### Iteration and Looping

The most widely used looping construct is the `for` statement, which is 
used to iterate over a collection of items. Iteration is one of Python's 
richest features. However, the most common form of iteration is to 
simply loop over all the members of a sequence such as a string, list, 
or tuple. Let's see:

```python
>>> for n in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
...     print(f"2 to the {n} power is {2**n}")
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

In this example, the variable `n` will be assigned successive items from 
the list `[1, 2, 3, 4, ..., 9]` on each iteration. Because looping over 
ranges of integers is quite common, the following shortcut is often used 
for that purpose:

```python
>> for n in range(1, 10):
...     print(f"2 to the {n} power is {2**n}")
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

You can advance a `for` loop to the next iteration, skipping the 
remainder of the block, using the `continue` keyword. Consider the below 
code, which sums up integers in a list and skips `None` values:

```python
>>> seq = [1, 2, None, 4, None, 5]
>>> total = 0
>>> for value in seq:
...     if value is None:
...         continue
...     total += value
...
>>> total
12
```

A `for` loop can be exited altogether with the `break` keyword. This 
code sums elements of the list until a 5 is reached:

```python
>>> seq = [1, 2, 0, 4, 6, 5, 2, 1]
>>> total_until_5 = 0
>>> for value in seq:
...     if value == 5:
...         break
...     total_until_5 += value
...
>>> total_until_5
13
```

The `break` keyword only terminates the innermost `for` loop. Any 
outer `for` loops will continue to run:

```python
>>> for i in range(4):
...     for j in range(4):
...         if j > i:
...             break
...         print((i, j))
...
(0, 0)
(1, 0)
(1, 1)
(2, 0)
(2, 1)
(2, 2)
(3, 0)
(3, 1)
(3, 2)
(3, 3)
```

The `for` loop is one of Python's most powerful language features 
because you can create custom iterator objects and generator functions 
that supply it with sequences of values.

A different looping statement is the `while` loop. It specifies a 
condition and a block of code that is to be executed until the condition 
evaluates to `False` or the loop is explicitly ended with `break`:

```python
>>> x = 256
>>> total = 0
>>> while x > 0:
...     if total > 500:
...         break
...     total += x
...     x = x // 2
...
>>> x
4
>>> total
504
```

### List, Set, and Dictionary Comprehensions

*List comprehensions* are one of the most-loved Python language 
features. They allow you to concisely form a new list by filtering the 
elements of a collection, transforming the elements passing the filter 
in one concise expression. They take the basic form:

```python
[expr for val in collection if condition]
```

This is equivalent to the following `for` loop:

```python
result = []
for val in collection:
    if condition:
        result.append(expr)
```

The filter condition can be omitted, leaving only the expression. For 
example, given a list of strings, we could filter out strings with 
length 2 or less and also convert them to uppercase like this:

```python
>>> strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
>>> [x.upper() for x in strings if len(x) > 2]
['BAT', 'CAR', 'DOVE', 'PYTHON']
```

Set and dictionary comprehensions are a natural extension, producing 
sets and dictionaries in an idiomatically similar way instead of lists. 
A dictionary comprehension looks like this:

```python
{key-expr: value-expr for val in collection if condition}
```

Let's see an example:

```python
>>> {x.upper(): list(range(3)) for x in ['a', 'b', 'c'] if type(x) is str}
{'A': [0, 1, 2], 'B': [0, 1, 2], 'C': [0, 1, 2]}
```

In a similar way, a set comprehension looks like this:

```python
{expr for val in collection if condition}
```

Let's see an example:

```python
>>> {x.upper() for x in ['d', 'e', 'f', 1, 2, 3] if type(x) is str}  
{'E', 'D', 'F'}
```

Like list comprehensions, set and dictionary comprehensions are mostly 
conveniences, but they similarly can make code both easier to write and 
read. Consider the list of 
strings `['a', 'as', 'bat', 'car', 'dove', 'python']` and suppose we 
wanted a set containing just the lengths of the strings contained in the 
collection. We could easily compute this using a set comprehension:

```python
>>> strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
>>> {len(x) for x in strings}
{1, 2, 3, 4, 6}
```

We could also express this more functionally using the `map` function:

```python
>>> set(map(len, strings))
{1, 2, 3, 4, 6}
```

As a simple dictionary comprehension example, we could create a lookup 
map of these strings to their locations in the list:

```python
>>> {val: index for index, val in enumerate(strings)}
{'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}
```

**Nested list comprehensions**

Suppose we have a list of lists containing some English and Spanish 
names:

```python
>>> data = [['John', 'Emily', 'Michael', 'Mary', 'Peter'], 
...         ['Maria', 'Juan', 'Miguel', 'Emilia', 'Pablo']]
```

You might have gotten these names from a couple of files and decided to 
organize them by language. Now, suppose we wanted to get a single list 
containing all names with two or more `e`s in them. We could certainly 
do this with a simple `for` loop:

```python
>>> for names in data:
...     enough_es = [name for name in names if name.count('e') >= 2]
...     names_of_interest.extend(enough_es)
...
>>> names_of_interest
['Peter']
```

You can actually wrap this whole operation up in a 
single *nested list comprehension*, which will look like:

```python
>>> names_of_interest = [name for names in data for name in names if name.count('e') >= 2]
>>> names_of_interest
['Peter']
```

At first, nested list comprehensions are a bit hard to wrap your head 
around. The `for` parts of the list comprehension are arranged according 
to the order of nesting, and any filter condition is put at the end as 
before. Here is another example where we "flatten" a list of tuples of 
integers into a simple list of integers:

```python
>>> tuple_a = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
>>> [x for tup in tuple_a for x in tup]
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Keep in mind that the order of the `for` expressions would be the same 
if you wrote a nested `for` loop instead of a list comprehension:

```python
flattened = []
for tup in tuple_a:
    for x in tup:
        flattened.append(x)
```

You can have arbitrarily many levels of nesting, though if you have more 
than two or three levels of nesting you should probably start to 
question whether this makes sense from a code readability standpoint. 
It's important to distinguish the syntax just shown from a list 
comprehension inside a list comprehension, which is also perfectly 
valid:

```python
>>> [[x for x in tup] for tup in tuple_a]
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

This produces a list of lists, rather than a flattened list of all of 
the inner elements.

### Functions

Functions are the primary and most important method of code organization 
and reuse in Python. As a rule of thumb, if you anticipate needing to 
repeat the same or very similar code more than once, it may be worth 
writing a reusable function. Functions can also help make your code more 
readable by giving a name to a group of Python statements.

Functions are declared with the `def` keyword and returned from with 
the `return` keyword. Let's see a first example:

```python
>>> def remainder(a, b):
...     q = a // b
...     r = a - q * b
...     return r
...
```

A second example would be:

```python
>>> def my_function(x, y, z=1.5):
...     if z > 1:
...         return z * (x + y)
...     else:
...         return z / (x + y)
...
```

To invoke a function, simply use the name of the function followed by 
its arguments enclosed in parentheses:

```python
>>> result_1 = remainder(37, 15)
>>> result_1
7
>>> result_2 = my_function(12, 25)
>>> result_2
55.5
```

There is no issue with having multiple `return` statements. If Python 
reaches the end of a function without encountering a `return` statement
, `None` is returned automatically.

Each function can have *positional* arguments and *keyword* arguments. 
Keyword arguments are most commonly used to specify default values or 
optional arguments. In the first preceding function, `a` and `b` are 
positional arguments. In the second preceding function, `x` and `y` are 
positional arguments, while `z` is a keyword argument. This means that 
those functions can be called in any of these ways:

```python
>>> result_11 = remainder(26, 8)
>>> result_11
2
>>> result_12 = remainder(b=8, a=26)
>>> result_12
2
>>> result_21 = my_function(5, 6, z=0.7)
>>> result_21
0.06363636363636363
>>> result_22 = my_function(3.141592, 7, 3.5)
>>> result_22
35.495571999999996
>>> result_23 = my_function(10, 20)
>>> result_23
45.0
```

The main restriction on function arguments is that the keyword 
arguments *must* follow the positional arguments (if any). You can 
specify keyword arguments in any order; this frees you from having to 
remember which order the function arguments were specified in and only 
what their names are.

It is possible to use keywords for passing positional arguments as well. 
In the second preceding example, we could also have written:

```python
my_function(x=5, y=6, z=7)
my_function(y=6, x=5, z=7)
```

In some cases this can help with readability.

**Namespaces, Scope, and Local Functions**

Functions can access variables in two different scopes: *global* 
and *local*. An alternative and more descriptive name describing a 
variable scope in Python is a *namespace*. Any variables that are 
assigned within a function by default are assigned to the local 
namespace. That is, the variable is only defined inside the body of the 
function and is destroyed when the function returns. The local namespace 
is created when the function is called and immediately populated by the 
function's arguments. After the function is finished, the local 
namespace is destroyed (with some exceptions). Consider the following 
function:

```python
>>> def func():
...     a = []
...     for i in range(5):
...         a.append(i)
...
```

When `func()` is called, the empty list `a` is created, five elements 
are appended, and then `a` is destroyed when the function exits. Suppose 
instead we had declared `a` as follows:

```python
>>> a = []
>>> def func():
...     for i in range(5):
...         a.append(i)
...
```

Assigning variables outside of the function's scope is possible, but 
those variables must be declared as global via the `global` keyword:

```python
>>> a = 1
>>> a
1
>>> def bind_a_variable():
...     global a
...     a = []
...
>>> bind_a_variable()
>>> a
[]
```

Notice this: it is generally discouraged to use the `global` keyword. 
Typically global variables are used to store some kind of state in a 
system. If you find yourself using a lot of them, it may indicate a need 
for object-oriented programming (using classes).

**Returning Multiple Values**

You can use a tuple to return multiple values from a function:

```python
>>> def divide(a, b):
...     q = a // b
...     r = a - q * b
...     return q, r
...
```

When returning multiple values in a tuple, you can easily unpack the 
result into separate variables like this:

```python
>>> quotient, remainder = divide(1456, 33)
>>> quotient
44
>>> remainder
4
```

A different approach is this:

```python
>>> return_value = divide(1456, 33)
>>> return_value
(44, 4)
```

Here, `return_value` would be a 2-tuple with the two returned variables. 
A potentially attractive alternative to returning multiple values like 
before might be to return a `dict` instead:

```python
>>> def divide(a, b):
...     q = a // b
...     r = a - q * b
...     return {'q': q, 'r': r}
...
```

Then:

```python
>>> return_value = divide(1456, 33)
>>> return_value
{'q': 44, 'r': 4}
```

**Functions Are Objects**

Since Python functions are objects, many constructs can be easily 
expressed that are difficult to do in other languages. Suppose we were 
doing some data cleaning and needed to apply a bunch of transformations 
to the following list of strings:

```python
>>> states = ['Alabama ', 'Georgia!', 'Georgia', 'georgia', 'FlOrIda', 
...           'south   carolina##', 'West virginia?']
```

Anyone who has ever worked with user-submitted survey data has seen 
messy results like these. Lots of things need to happen to make this 
list of strings uniform and ready for analysis: stripping whitespace, 
removing punctuation symbols, and standardizing on proper 
capitalization. One way to do this is to use built-in string methods 
along with the `re` standard library module for regular expressions:

```python
>>> import re
>>> def clean_strings(strings):
...     result = []
...     for value in strings:
...         value = value.strip()
...         value = re.sub('[!#?]', '', value)
...         value = value.title()
...         result.append(value)
...     return result
...
```

The result looks like this:

```python
>>> clean_strings(states)
['Alabama', 'Georgia', 'Georgia', 'Georgia', 'Florida', 'South   
Carolina', 'West Virginia']
```

An alternative approach that you may find useful is to make a list of 
the operations you want to apply to a particular set of strings:

```python
>>> def remove_punctuation(value):
...     return re.sub('[!#?]', '', value)
...
>>> clean_ops = [str.strip, remove_punctuation, str.title]
>>> def clean_strings(strings, ops):
...     result = []
...     for value in strings:
...         for function in ops:
...             value = function(value)
...         result.append(value)
...     return result
...
```

Then we have the following:

```python
>>> clean_strings(states, clean_ops)
['Alabama', 'Georgia', 'Georgia', 'Georgia', 'Florida', 'South   
Carolina', 'West Virginia']
```

A more *functional* pattern like this enables you to easily modify how 
the strings are transformed at a very high level. The `clean_strings` 
function is also now more reusable and generic.

You can use functions as arguments to other functions like the 
built-in `map` function, which applies a function to a sequence of some 
kind:

```python
>>> for x in map(remove_punctuation, states):
...     print(x)
...
Alabama
Georgia
Georgia
georgia
FlOrIda
south   carolina
West virginia
```

**Anonymous (Lambda) Functions**

Python has support for so-called *anonymous* or *lambda* functions, 
which are a way of writing functions consisting of a single statement, 
the result of which is the return value. They are defined with 
the `lambda` keyword, which has no meaning other than "we are declaring 
an anonymous function":

```python
>>> def short_function(x):
...     return x * 2
...
>>> short_function(10)
20
>>> equiv_anon = lambda x: x * 2
>>> equiv_anon(10)
20
```

These functions are especially convenient in data analysis because there 
are many cases where data transformation functions will take functions 
as arguments. It's often less typing (and clearer) to pass a lambda 
function as opposed to writing a full-out function declaration or even 
assigning the lambda function to a local variable. For example, consider 
this silly example:

```python
>>> def apply_to_list(some_list, f):
...     return [f(x) for x in some_list]
...
>>> ints = [4, 0, 1, 5, 6]
>>> apply_to_list(ints, lambda x: x * 2)
[8, 0, 2, 10, 12]
```

You could also have written `[x * 2 for x in ints]`, but here we were 
able to succinctly pass a custom operator to the `apply_to_list` 
function.

As another example, suppose you wanted to sort a collection of strings 
by the number of distinct letters in each string:

```python
>>> strings = ['foo', 'card', 'bar', 'aaaa', 'abab']
```

Here we could pass a lambda function to the list's `sort` method:

```python
>>> strings.sort(key=lambda x: len(set(list(x))))
>>> strings
['aaaa', 'foo', 'abab', 'bar', 'card']
```

Notice this: one reason lambda functions are called anonymous functions 
is that, unlike functions declared with the `def` keyword, the function 
object itself is never given an explicit `__name__` attribute.

**Currying: Partial Argument Application**

*Currying* is computer science jargon (named after the mathematician 
Haskell Curry) that means deriving new functions from existing ones 
by *partial argument application*. For example, suppose we had a trivial 
function that adds two numbers together:

```python
>>> def add_numbers(x, y):
...     return x + y
...
```

Using this function, we could derive a new function of one variable
, `add_five`, that adds 5 to its argument:

```python
>>> add_five = lambda y: add_numbers(5, y)
>>> add_five(10)
15
```

The second argument to `add_numbers` is said to be *curried*. There's 
nothing very fancy here, as all we've really done is define a new 
function that calls an existing function. The built-in `functools` 
module can simplify this process using the `partial` function:

```python
>>> from functools import partial
>>> add_five = partial(add_numbers, 5)
>>> add_five(10)
15
```
