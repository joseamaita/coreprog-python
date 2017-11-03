# Python Application focusing Data Structures and Algorithms

## Basic switcher

### Version A

The following program shows how to handle multiple-test cases by using
the `elif` statement:

```python
#!/usr/bin/env python3
import sys

def menuSelection(number):
    print(f"You selected option '{number}'!\n\n")

def main():
    print('-------------------------------------------')
    print('          Basic Switcher')
    print('-------------------------------------------')
    print()
    if len(sys.argv) != 2:
        print("Please supply a number only!\n\n")
        raise SystemExit(1)
    number = int(sys.argv[1])
    if number == 0 or number == 1:
        menuSelection(number)
    elif number == 2:
        print("That option is not available yet!\n\n")
    elif number == 3:
        print("That option is going to be available soon!\n\n")
    else:
        raise RuntimeError("Unknown input")

if __name__ == '__main__':
    main()
```

After running the script for the range of options, the output are:

```
$ ./script.py -> Please supply a number only!
$ ./script.py 0 -> You selected option '0'!
$ ./script.py 1 -> You selected option '1'!
$ ./script.py 2 -> That option is not available yet!
$ ./script.py 3 -> That option is going to be available soon!
$ ./script.py 4 -> RuntimeError: Unknown input
```

### Version B

It's possible to write workarounds of "switch/case" statements on 
Python. One of these would be the use of a **dictionary mapping**.

The following program shows how to handle multiple-test cases by using a 
switch/case with dictionary mapping:

```python
#!/usr/bin/env python3
import sys

def menuSelection(number):
    switcher = {0: "You selected option 'zero'!\n\n", 
                1: "You selected option 'one'!\n\n", 
                2: "That option is not available yet!\n\n", 
                3: "That option is going to be available soon!\n\n"}
    return switcher.get(number, "Unknown input\n\n")

def main():
    print('-------------------------------------------')
    print('          Basic Switcher')
    print('-------------------------------------------')
    print()
    if len(sys.argv) != 2:
        print("Please supply a number only!\n\n")
        raise SystemExit(1)
    number = int(sys.argv[1])
    print(menuSelection(number))

if __name__ == '__main__':
    main()
```

After running the script for the range of options, the output are:

```
$ ./script.py -> Please supply a number only!
$ ./script.py 0 -> You selected option 'zero'!
$ ./script.py 1 -> You selected option 'one'!
$ ./script.py 2 -> That option is not available yet!
$ ./script.py 3 -> That option is going to be available soon!
$ ./script.py 4 -> Unknown input
```

### Version C

Another approach of "switch/case" statements on Python would be the use 
of **dictionary mapping for functions**. In Python, we can also include 
functions or lambdas in our dictionary mapping:

```python
#!/usr/bin/env python3
import sys

def zero():
    return "You selected option 'zero'!\n\n"

def one():
    return "You selected option 'one'!\n\n"

def two():
    return "That option is not available yet!\n\n"

def menuSelection(number):
    switcher = {0: zero, 
                1: one, 
                2: two, 
                3: lambda: "That option is going to be "
                           "available soon!\n\n"}
    # Get the function from switcher dictionary
    func = switcher.get(number, lambda: "Unknown input\n\n")
    # Execute the function
    return func()

def main():
    print('-------------------------------------------')
    print('          Basic Switcher')
    print('-------------------------------------------')
    print()
    if len(sys.argv) != 2:
        print("Please supply a number only!\n\n")
        raise SystemExit(1)
    number = int(sys.argv[1])
    print(menuSelection(number))

if __name__ == '__main__':
    main()
```

After running the script for the range of options, the output are:

```
$ ./script.py -> Please supply a number only!
$ ./script.py 0 -> You selected option 'zero'!
$ ./script.py 1 -> You selected option 'one'!
$ ./script.py 2 -> That option is not available yet!
$ ./script.py 3 -> That option is going to be available soon!
$ ./script.py 4 -> Unknown input
```

While the code inside `zero()`, `one()` and `two()` are simple, many 
Python programs use dictionary mappings like this to dispatch complex 
procedures.
