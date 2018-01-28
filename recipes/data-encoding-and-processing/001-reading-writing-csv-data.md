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

**Writing CSV data from headers as list and rows as list of dictionaries**

If you have the data as a sequence of dictionaries, do this:

```python
#!/usr/bin/env python3

import csv

headers = ['Symbol', 'Price', 'Date', 'Time', 'Change', 'Volume']
rows = [
{'Symbol': 'AA', 'Price': 39.48, 'Date': '6/11/2007', 'Time': '9:36am', 'Change': -0.18, 'Volume': 181800}, 
{'Symbol': 'AIG', 'Price': 71.38, 'Date': '6/11/2007', 'Time': '9:36am', 'Change': -0.15, 'Volume': 195500}, 
{'Symbol': 'AXP', 'Price': 62.58, 'Date': '6/11/2007', 'Time': '9:36am', 'Change': -0.46, 'Volume': 935000}, 
]

filename = "stocks_c.csv"

print(f"\nWriting CSV data to '{filename}' ...\n")
with open(filename, 'w') as f:
    f_csv = csv.DictWriter(f, headers)
    f_csv.writeheader()
    f_csv.writerows(rows)
```

The generated output file is:

```
Symbol,Price,Date,Time,Change,Volume
AA,39.48,6/11/2007,9:36am,-0.18,181800
AIG,71.38,6/11/2007,9:36am,-0.15,195500
AXP,62.58,6/11/2007,9:36am,-0.46,935000
```

### Discussion

You should almost always prefer the use of the `csv` module over 
manually trying to split and parse CSV data yourself. For instance, you 
might be inclined to just write some code like this:

```python
#!/usr/bin/env python3

filename = "stocks.csv"

print(f"\nParsing CSV file yourself without csv module from "\
      f"'{filename}' ...\n")
with open(filename) as f:
    for line in f:
        row = line.split(',')
        # process row
        print(f"    {row}")
        # print(f"    {row[0]}")
        # print(f"    {row[5]}")
```

After running the script, the output is:

```
Parsing CSV file yourself without csv module from 'stocks.csv' ...

    ['Symbol', 'Price', 'Date', 'Time', 'Change', 'Volume\n']
    ['"AA"', '39.48', '"6/11/2007"', '"9:36am"', '-0.18', '181800\n']
    ['"AIG"', '71.38', '"6/11/2007"', '"9:36am"', '-0.15', '195500\n']
    ['"AXP"', '62.58', '"6/11/2007"', '"9:36am"', '-0.46', '935000\n']
    ['"BA"', '98.31', '"6/11/2007"', '"9:36am"', '+0.12', '104800\n']
    ['"C"', '53.08', '"6/11/2007"', '"9:36am"', '-0.25', '360900\n']
    ['"CAT"', '78.29', '"6/11/2007"', '"9:36am"', '-0.23', '225400\n']
```

The problem with this approach is that you'll still need to deal with 
some nasty details. For example, if any of the fields are surrounded by 
quotes, you'll have to strip the quotes. In addition, if a quoted field 
happens to contain a comma, the code will break by producing a row with 
the wrong size.

By default, the `csv` library is programmed to understand CSV encoding 
rules used by Microsoft Excel. This is probably the most common variant, 
and will likely give you the best compatibility. However, if you consult 
the documentation for `csv`, you'll see a few ways to tweak the encoding 
to different formats (e.g., changing the separator character, etc.).

For example, let's consider the following tab-delimited file 
called *stocks.tsv*:

```tsv
Symbol	Price	Date	Time	Change	Volume
"AA"	39.48	"6/11/2007"	"9:36am"	-0.18	181800
"AIG"	71.38	"6/11/2007"	"9:36am"	-0.15	195500
"AXP"	62.58	"6/11/2007"	"9:36am"	-0.46	935000
"BA"	98.31	"6/11/2007"	"9:36am"	+0.12	104800
"C"	53.08	"6/11/2007"	"9:36am"	-0.25	360900
"CAT"	78.29	"6/11/2007"	"9:36am"	-0.23	225400
```

If you want to read tab-delimited data instead, use this:

```python
#!/usr/bin/env python3

import csv

filename = "stocks.tsv"

print(f"\nReading CSV file as tab-separated values from "\
      f"'{filename}' ...\n")
with open(filename) as f:
    f_tsv = csv.reader(f, delimiter='\t')
    for row in f_tsv:
        # Process row
        print(f"    {row}")
        # print(f"    {row[0]}")
        # print(f"    {row[5]}")
```

After running the script, the output is:

```
Reading CSV file as tab-separated values from 'stocks.tsv' ...

    ['Symbol', 'Price', 'Date', 'Time', 'Change', 'Volume']
    ['AA', '39.48', '6/11/2007', '9:36am', '-0.18', '181800']
    ['AIG', '71.38', '6/11/2007', '9:36am', '-0.15', '195500']
    ['AXP', '62.58', '6/11/2007', '9:36am', '-0.46', '935000']
    ['BA', '98.31', '6/11/2007', '9:36am', '+0.12', '104800']
    ['C', '53.08', '6/11/2007', '9:36am', '-0.25', '360900']
    ['CAT', '78.29', '6/11/2007', '9:36am', '-0.23', '225400']
```

If you're reading CSV data and converting it into named tuples, you need 
to be a little careful with validating column headers. For example, a 
CSV file named *locations.csv* could have a header line containing 
nonvalid identifier characters like this:

```
Street Address,Num-Premises,Latitude,Longitude
5412 N CLARK,10,41.980262,-87.668452
```

This will actually cause the creation of a `namedtuple` to fail with 
a `ValueError` exception. Try this:

```python
#!/usr/bin/env python3

import csv
from collections import namedtuple

filename = "locations.csv"

print(f"\nForce the 'ValueError' exception when reading "\
      f"'{filename}' ...\n")
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
Force the 'ValueError' exception when reading 'locations.csv' ...

Traceback (most recent call last):
  File "./script.py", line 12, in <module>
    Row = namedtuple('Row', next(f_csv))
  File "/usr/local/lib/python3.6/collections/__init__.py", line 400, in namedtuple
    'identifiers: %r' % name)
ValueError: Type names and field names must be valid identifiers: 'Street Address'
```

To work around this, you might have to scrub the headers first. For 
instance, carrying a regex substitution on nonvalid identifier 
characters like this:

```python
#!/usr/bin/env python3

import re
import csv
from collections import namedtuple

filename = "locations.csv"

print(f"\nChecking for headers as valid identifiers when reading "\
      f"'{filename}' ...\n")
with open(filename) as f:
    f_csv = csv.reader(f)
    headers = [ re.sub('[^a-zA-Z_]', '_', h) for h in next(f_csv) ]
    Row = namedtuple('Row', headers)
    for r in f_csv:
        row = Row(*r)
        # process row
        print(f"    {row}")
        # print(f"    {row.Street_Address}")
        # print(f"    {row.Longitude}")
        # print(f"    {row[0]}")
        # print(f"    {row[3]}")
```

After running the script, the output is:

```
Checking for headers as valid identifiers when reading 'locations.csv' ...

    Row(Street_Address='5412 N CLARK', Num_Premises='10', Latitude='41.980262', Longitude='-87.668452')
```

It's also important to emphasize that `csv` does not try to interpret 
the data or convert it to a type other than a string. If such 
conversions are important, that is something you'll need to do yourself. 
Here is one example of performing extra type conversions on CSV data:

```python
#!/usr/bin/env python3

import csv

filename = "stocks.csv"
col_types = [str, float, str, str, float, int]

print(f"\nReading into named tuples with type conversion from "\
      f"'{filename}' ...\n")
with open(filename) as f:
    f_csv = csv.reader(f)
    headers = next(f_csv)
    for row in f_csv:
        # Apply conversions to the row items
        row = tuple(convert(value) for convert, value in zip(col_types, row))
        print(f"    {row}")
        # print(f"    {row[0]}")
        # print(f"    {row[5]}")
```

After running the script, the output is:

```
Reading into named tuples with type conversion from 'stocks.csv' ...

    ('AA', 39.48, '6/11/2007', '9:36am', -0.18, 181800)
    ('AIG', 71.38, '6/11/2007', '9:36am', -0.15, 195500)
    ('AXP', 62.58, '6/11/2007', '9:36am', -0.46, 935000)
    ('BA', 98.31, '6/11/2007', '9:36am', 0.12, 104800)
    ('C', 53.08, '6/11/2007', '9:36am', -0.25, 360900)
    ('CAT', 78.29, '6/11/2007', '9:36am', -0.23, 225400)
```

Alternatively, here is an example of converting selected fields of 
dictionaries:

```python
#!/usr/bin/env python3

import csv

filename = "stocks.csv"
field_types = [
('Price', float), 
('Change', float), 
('Volume', int), 
]

print(f"\nReading as dictionaries with type conversion from "\
      f"'{filename}' ...\n")
with open(filename) as f:
    for row in csv.DictReader(f):
        row.update((key, conversion(row[key])) 
                    for key, conversion in field_types)
        print(f"    {row}")
        # print(f"    {row['Symbol']}")
        # print(f"    {row['Volume']}")
```

After running the script, the output is:

```
Reading as dictionaries with type conversion from 'stocks.csv' ...

    OrderedDict([('Symbol', 'AA'), ('Price', 39.48), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', -0.18), ('Volume', 181800)])
    OrderedDict([('Symbol', 'AIG'), ('Price', 71.38), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', -0.15), ('Volume', 195500)])
    OrderedDict([('Symbol', 'AXP'), ('Price', 62.58), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', -0.46), ('Volume', 935000)])
    OrderedDict([('Symbol', 'BA'), ('Price', 98.31), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', 0.12), ('Volume', 104800)])
    OrderedDict([('Symbol', 'C'), ('Price', 53.08), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', -0.25), ('Volume', 360900)])
    OrderedDict([('Symbol', 'CAT'), ('Price', 78.29), ('Date', '6/11/2007'), ('Time', '9:36am'), ('Change', -0.23), ('Volume', 225400)])
```

In general, you'll probably want to be a bit careful with such 
conversions, though. In the real world, it's common for CSV files to 
have missing values, corrupted data, and other issues that would break 
type conversions. So, unless your data is guaranteed to be error free, 
that's something you'll need to consider (you might need to add suitable 
exception handling).

Finally, if your goal in reading CSV data is to perform data analysis 
and statistics, you might want to look at 
the [Pandas package](http://pandas.pydata.org). Pandas includes a 
convenient `pandas.read_csv()` function that will load CSV data into 
a `DataFrame` object. From there, you can generate various summary 
statistics, filter the data, and perform other kinds of high-level 
operations. The recipe "Summarizing Data and Performing Statistics" will 
give you more information.
