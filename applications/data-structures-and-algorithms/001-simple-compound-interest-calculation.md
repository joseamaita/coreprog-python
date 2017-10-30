# Python Applications focusing Data Structures and Algorithms

## Simple compound-interest calculation

### Version A

The following program shows the use of variables and expressions by 
performing a simple compound-interest calculation. Let's see:

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

### Version B

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
