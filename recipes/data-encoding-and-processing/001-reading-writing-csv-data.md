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

**Reading CSV data as namedtuples**

In the preceding code block, `row` will be a tuple. Thus, to access 
certain fields, you will need to use indexing, such as `row[0]` (Symbol) 
and `row[5]` (Volume).

Since such indexing can often be confusing, this is one place where you 
might want to consider the use of named tuples. For example:

```python
#!/usr/bin/env python3

import csv
from collections import namedtuple

filename = "stocks.csv"

print(f"\nReading CSV data from '{filename}' as namedtuples ...\n")
with open(filename) as f:
    f_csv = csv.reader(f)
    Row = namedtuple('Row', next(f_csv))
    for r in f_csv:
        row = Row(*r)
        # process row
        print(f"    {row}")
        # print(f"    {row.Symbol}")
        # print(f"    {row.Volume}")
```

After running the script, the output is:

```
Reading CSV data from 'stocks.csv' as namedtuples ...

    Row(Symbol='AA', Price='39.48', Date='6/11/2007', Time='9:36am', Change='-0.18', Volume='181800')
    Row(Symbol='AIG', Price='71.38', Date='6/11/2007', Time='9:36am', Change='-0.15', Volume='195500')
    Row(Symbol='AXP', Price='62.58', Date='6/11/2007', Time='9:36am', Change='-0.46', Volume='935000')
    Row(Symbol='BA', Price='98.31', Date='6/11/2007', Time='9:36am', Change='+0.12', Volume='104800')
    Row(Symbol='C', Price='53.08', Date='6/11/2007', Time='9:36am', Change='-0.25', Volume='360900')
    Row(Symbol='CAT', Price='78.29', Date='6/11/2007', Time='9:36am', Change='-0.23', Volume='225400')
```

This would allow you to use the column headers such as `row.Symbol` 
and `row.Volume` instead of indices. It should be noted that this only 
works if the column headers are valid Python identifiers. If not, you 
might have to massage the initial headings (e.g., replacing 
nonidentifier characters with underscores or similar).

**Reading CSV data as dictionaries**

Another alternative is to read the data as a sequence of dictionaries 
instead. To do that, use this code:

```python
#!/usr/bin/env python3

import csv

filename = "stocks.csv"

print(f"\nReading CSV data from '{filename}' as dictionaries ...\n")
with open(filename) as f:
    f_csv = csv.DictReader(f)
    for row in f_csv:
        # process row
        print(f"    {row}")
        # print(f"    {row['Symbol']}")
        # print(f"    {row['Volume']}")
```

In this version, you would access the elements of each row using the row 
headers. For example, `row['Symbol']` or `row['Volume']`.

After running the script, the output is:

```
Reading CSV data from 'stocks.csv' as dictionaries ...

    OrderedDict([('Symbol', 'AA'), ('Price', '39.48'), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', '-0.18'), ('Volume', '181800')])
    OrderedDict([('Symbol', 'AIG'), ('Price', '71.38'), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', '-0.15'), ('Volume', '195500')])
    OrderedDict([('Symbol', 'AXP'), ('Price', '62.58'), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', '-0.46'), ('Volume', '935000')])
    OrderedDict([('Symbol', 'BA'), ('Price', '98.31'), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', '+0.12'), ('Volume', '104800')])
    OrderedDict([('Symbol', 'C'), ('Price', '53.08'), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', '-0.25'), ('Volume', '360900')])
    OrderedDict([('Symbol', 'CAT'), ('Price', '78.29'), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', '-0.23'), ('Volume', '225400')])
```

**Writing CSV data from headers as list and rows as list of tuples**

To write CSV data, you also use the `csv` module but create a writer 
object. Notice that the headers are stored as a list and the rows are 
stored as list of tuples. For example:

```python
#!/usr/bin/env python3

import csv

headers = ['Symbol', 'Price', 'Date', 'Time', 'Change', 'Volume']
rows = [
('AA', 39.48, '6/11/2007', '9:36am', -0.18, 181800), 
('AIG', 71.38, '6/11/2007', '9:36am', -0.15, 195500), 
('AXP', 62.58, '6/11/2007', '9:36am', -0.46, 935000), 
]

filename = "stocks_b.csv"

print(f"\nWriting CSV data to '{filename}' ...\n")
with open(filename, 'w') as f:
    f_csv = csv.writer(f)
    f_csv.writerow(headers)
    f_csv.writerows(rows)
```

The generated output file is:

```
Symbol,Price,Date,Time,Change,Volume
AA,39.48,6/11/2007,9:36am,-0.18,181800
AIG,71.38,6/11/2007,9:36am,-0.15,195500
AXP,62.58,6/11/2007,9:36am,-0.46,935000
```
