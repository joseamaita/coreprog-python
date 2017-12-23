# Python Application focusing Iterators and Generators

## Simple generator functions

### Version A

Here, we create a script that presents a group of simple generator 
functions and show each respective output. This version includes the 
following features:

* Integer numbers generated from a countdown
* Integer numbers from zero to a maximum number excluded (similar 
to `range`)
* Square numbers generated from 1 to 10

Anything that can be done with a generator can also be done with an 
iterator. However, generators are really nice to express certain ideas 
in a very clean and concise fashion.

Now, let's see the code for the application:

```python
#!/usr/bin/env python3

def countdown(n=1):
    print(f"Counting down from ... {n}")
    while n > 0:
        yield n
        n -= 1
    print("Done counting down!\n\n")

def range_m(maxi=5):
    print(f"Generating numbers from ... 0 to {maxi} (excluded)")
    index = 0
    while index < maxi:
        yield index
        index += 1
    print("Done with range-like function!\n\n")

def squares(n=10):
    print(f"Generating squares from ... 1 to {n ** 2}")
    for i in range(1, n + 1):
        yield i ** 2
    print("Done with square numbers!\n\n")

def main():
    print('-----------------------------------')
    print('    Simple generator functions')
    print('-----------------------------------')
    print()
    for i in countdown(10):
        print(i, end=' ')
    for r in range_m(8):
        print(r, end=' ')
    for x in squares():
        print(x, end=' ')

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-----------------------------------
    Simple generator functions
-----------------------------------

Counting down from ... 10
10 9 8 7 6 5 4 3 2 1 Done counting down!


Generating numbers from ... 0 to 8 (excluded)
0 1 2 3 4 5 6 7 Done with range-like function!


Generating squares from ... 1 to 100
1 4 9 16 25 36 49 64 81 100 Done with square numbers!


```
