# Python Recipe for Files and I/O

## Reading a data file in a basic way

### Problem

You need a basic way of reading a data file.

### Solution

**Version A**

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

This program opens a data file, reads its contents line by line and 
prints the contents:

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

**Version B**

This program opens a data file, reads and prints its contents line by 
line, but using the `for` statement:

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

**Version C**

This program opens a data file, reads and prints its contents line by 
line, but using the `with` keyword:

```python
#!/usr/bin/env python3

def main():
    print('-------------------------------------------')
    print('          Read Data File')
    print('-------------------------------------------')
    print()
    with open("datafile") as f:
        print(f.read(), end='')

if __name__ == '__main__':
    main()
```
