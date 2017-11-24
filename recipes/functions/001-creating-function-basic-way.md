# Python Recipe for Functions

## Creating a function in a basic way

### Problem

You need a basic way of creating a function.

### Solution

**Version A**

You use the `def` statement to create a function. You also need to 
return a value with the `return` keyword. Let's see the definition of 
the `remainder` function within an application:

```python
#!/usr/bin/env python3

def remainder(a, b):
    q = a // b
    r = a - q * b
    return r

def main():
    print('-------------------------------------------')
    print('      Create and Use Functions')
    print('-------------------------------------------')
    print()
    rem = remainder(37, 15)
    print(f"The remainder for 37/15 is {rem}")

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-------------------------------------------
      Create and Use Functions
-------------------------------------------

The remainder for 37/15 is 7
```

**Version B**

You can use a tuple to return multiple values from a function. Now, 
let's focus on the `divide` function definition:

```python
#!/usr/bin/env python3

def remainder(a, b):
    q = a // b
    r = a - q * b
    return r

def divide(a, b):
    q = a // b
    r = a - q * b
    return q, r

def main():
    print('-------------------------------------------')
    print('      Create and Use Functions')
    print('-------------------------------------------')
    print()
    a = 1456
    b = 33
    quotient, remainder = divide(a, b)
    print(f"If you divide {a}/{b}...")
    print(f"The remainder 'r' would be {remainder}")
    print(f"The quotient 'q' would be {quotient}")

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-------------------------------------------
      Create and Use Functions
-------------------------------------------

If you divide 1456/33...
The remainder 'r' would be 4
The quotient 'q' would be 44
```

**Version C**

Now, a different approach is shown, where a variable named `div` would 
be a 2-tuple with the two returned variables. Let's focus on 
the `divide` function definition:

```python
#!/usr/bin/env python3

def remainder(a, b):
    q = a // b
    r = a - q * b
    return r

def divide(a, b):
    q = a // b
    r = a - q * b
    return q, r

def main():
    print('-------------------------------------------')
    print('      Create and Use Functions')
    print('-------------------------------------------')
    print()
    a = 1456
    b = 33
    div = divide(a, b)
    print(f"If you divide {a}/{b}...")
    print(f"The remainder 'r' would be {div[1]}")
    print(f"The quotient 'q' would be {div[0]}")

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-------------------------------------------
      Create and Use Functions
-------------------------------------------

If you divide 1456/33...
The remainder 'r' would be 4
The quotient 'q' would be 44
```
