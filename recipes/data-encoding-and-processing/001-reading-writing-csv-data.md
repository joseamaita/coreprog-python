# Python Recipe for Data Encoding and Processing

## Reading and writing CSV data

### Problem

You want to read or write data encoded as a CSV file.

### Solution

For most kinds of CSV data, use the `csv` library. For example, suppose 
you have some stock market data in a file named *stocks.csv* like this:

```csv
Symbol,Price,Date,Time,Change,Volume
"AA",39.48,"6/11/2007","9:36am",-0.18,181800
"AIG",71.38,"6/11/2007","9:36am",-0.15,195500
"AXP",62.58,"6/11/2007","9:36am",-0.46,935000
"BA",98.31,"6/11/2007","9:36am",+0.12,104800
"C",53.08,"6/11/2007","9:36am",-0.25,360900
"CAT",78.29,"6/11/2007","9:36am",-0.23,225400
```

**Reading CSV data as lists**

Here's how you would read the data as a sequence of lists:

```python
#!/usr/bin/env python3

import csv

filename = "stocks.csv"

print(f"\nReading CSV data from '{filename}' as lists ...\n")
with open(filename) as f:
    f_csv = csv.reader(f)
    headers = next(f_csv)
    print(f"    {headers}")
    for row in f_csv:
        # process row
        print(f"    {row}")
```

After running the script, the output is:

```
Reading CSV data from 'stocks.csv' as lists ...

    ['Symbol', 'Price', 'Date', 'Time', 'Change', 'Volume']
    ['AA', '39.48', '6/11/2007', '9:36am', '-0.18', '181800']
    ['AIG', '71.38', '6/11/2007', '9:36am', '-0.15', '195500']
    ['AXP', '62.58', '6/11/2007', '9:36am', '-0.46', '935000']
    ['BA', '98.31', '6/11/2007', '9:36am', '+0.12', '104800']
    ['C', '53.08', '6/11/2007', '9:36am', '-0.25', '360900']
    ['CAT', '78.29', '6/11/2007', '9:36am', '-0.23', '225400']
```

**Reading CSV data as tuples**

Here's how you would read the data as a sequence of tuples:

```python
#!/usr/bin/env python3

import csv

filename = "stocks.csv"

print(f"\nReading CSV data from '{filename}' as tuples ...\n")
with open(filename) as f:
    f_csv = csv.reader(f)
    headers_l = next(f_csv)
    headers = tuple(headers_l)
    print(f"    {headers}")
    for row_l in f_csv:
        # process row
        row = tuple(row_l)
        print(f"    {row}")
```

After running the script, the output is:

```
Reading CSV data from 'stocks.csv' as tuples ...

    ('Symbol', 'Price', 'Date', 'Time', 'Change', 'Volume')
    ('AA', '39.48', '6/11/2007', '9:36am', '-0.18', '181800')
    ('AIG', '71.38', '6/11/2007', '9:36am', '-0.15', '195500')
    ('AXP', '62.58', '6/11/2007', '9:36am', '-0.46', '935000')
    ('BA', '98.31', '6/11/2007', '9:36am', '+0.12', '104800')
    ('C', '53.08', '6/11/2007', '9:36am', '-0.25', '360900')
    ('CAT', '78.29', '6/11/2007', '9:36am', '-0.23', '225400')
```
