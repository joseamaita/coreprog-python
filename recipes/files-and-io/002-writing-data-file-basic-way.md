# Python Recipe for Files and I/O

## Writing a data file in a basic way

### Problem

You need a basic way of writing a data file.

### Solution

**Version A**

This program makes the output of a program go to a file. Here, you can 
supply a file to the `print` statement:

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

After running the script, if you open `datafile-02`, the output is:

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

**Version B**

This program makes the output of a program go to a file. Here, you use 
the `write()` method from the file object, which can be used to write 
raw data.

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
