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
