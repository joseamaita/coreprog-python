# Python Recipe for Files and I/O

## Reading and writing from the standard input and output

### Problem

You want to read user input interactively and write data to the screen 
using the standard input and output streams of the interpreter.

### Solution

**Version A**

If you want to read user input interactively, you can read it from the 
file `sys.stdin`. Also, if you want to write data to the screen, you can 
write it to `sys.stdout`, which is the same file used to output data 
produced by the `print` statement. Let's see an application sample:

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

A sample run would show you something like this:

```
---------------------------------------------------
Read and Write from the Standard Input and Output
---------------------------------------------------

Enter your name: 
José Alberto

Hello, José Alberto!
```
