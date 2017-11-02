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
