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
