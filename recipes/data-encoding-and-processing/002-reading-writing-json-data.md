# Python Recipe for Data Encoding and Processing

## Reading and writing JSON data

### Problem

You want to read or write data encoded as JSON (JavaScript Object 
Notation)

### Solution

The `json` module provides an easy way to encode and decode data in 
JSON. The two main functions are `json.dumps()` and `json.loads()`, 
mirroring the interface used in other serialization libraries, such 
as `pickle`.

**Converting between Python data structure and JSON data**

Here is how you turn a Python data structure into JSON:

```python
>>> import json
>>> data = {
... 'name': 'ACME', 
... 'shares': 100, 
... 'price': 542.23, 
... }
>>> json_str = json.dumps(data)
>>> json_str
'{"name": "ACME", "shares": 100, "price": 542.23}'
```

Here is how you turn a JSON-encoded string back into a Python data 
structure:

```python
>>> data
{'name': 'ACME', 'shares': 100, 'price': 542.23}
>>> data_b = json.loads(json_str)
>>> data_b
{'name': 'ACME', 'shares': 100, 'price': 542.23}
```

**Reading JSON data from a file**

If you are working with files instead of strings, you can alternatively 
use `json.dump()` and `json.load()` to encode and decode JSON data. 
Let's see various examples of a *colors* JSON files. The name for the 
first one is *colors1.json*:

```json
{
  "aliceblue": "#f0f8ff",
  "antiquewhite": "#faebd7",
  "aqua": "#00ffff",
  "aquamarine": "#7fffd4",
  "azure": "#f0ffff",
  "beige": "#f5f5dc",
  "bisque": "#ffe4c4",
  "black": "#000000",
  "blanchedalmond": "#ffebcd",
  "blue": "#0000ff",
  "blueviolet": "#8a2be2",
  "brown": "#a52a2a",
  "burlywood": "#deb887",
  "cadetblue": "#5f9ea0",
  "chartreuse": "#7fff00",
  "chocolate": "#d2691e",
  "coral": "#ff7f50",
  "cornflowerblue": "#6495ed",
  "cornsilk": "#fff8dc",
  "crimson": "#dc143c",
  "cyan": "#00ffff"
}
```

The name of the second file is *colors2.json*:

```json
{
  "aliceblue": [240, 248, 255, 1],
  "antiquewhite": [250, 235, 215, 1],
  "aqua": [0, 255, 255, 1],
  "aquamarine": [127, 255, 212, 1],
  "azure": [240, 255, 255, 1],
  "beige": [245, 245, 220, 1],
  "bisque": [255, 228, 196, 1],
  "black": [0, 0, 0, 1],
  "blanchedalmond": [255, 235, 205, 1],
  "blue": [0, 0, 255, 1],
  "blueviolet": [138, 43, 226, 1],
  "brown": [165, 42, 42, 1],
  "burlywood": [222, 184, 135, 1],
  "cadetblue": [95, 158, 160, 1],
  "chartreuse": [127, 255, 0, 1],
  "chocolate": [210, 105, 30, 1],
  "coral": [255, 127, 80, 1],
  "cornflowerblue": [100, 149, 237, 1],
  "cornsilk": [255, 248, 220, 1],
  "crimson": [220, 20, 60, 1],
  "cyan": [0, 255, 255, 1]
}
```

Now, let's see an application that reads JSON data from a file:

```python
#!/usr/bin/env python3

import sys
import json

def main():
    filename = sys.argv[1]
    print(f"\nReading JSON data from '{filename}' ...\n")
    if len(sys.argv) != 2:
        print("Please supply a filename only!\n\n")
        raise SystemExit(1)
    try:
        with open(filename, 'r') as f:
            data = json.load(f)
            print(data)
    except FileNotFoundError:
        print("\nFile not found.\nLeaving.")
        raise SystemExit(1)

if __name__ == '__main__':
    main()
```

After running the script for *colors1.json*, the output is:

```
Reading JSON data from 'colors1.json' ...

{'aliceblue': '#f0f8ff', 'antiquewhite': '#faebd7', 'aqua': '#00ffff', 'aquamarine': '#7fffd4', 'azure': '#f0ffff', 'beige': '#f5f5dc', 'bisque': '#ffe4c4', 'black': '#000000', 'blanchedalmond': '#ffebcd', 'blue': '#0000ff', 'blueviolet': '#8a2be2', 'brown': '#a52a2a', 'burlywood': '#deb887', 'cadetblue': '#5f9ea0', 'chartreuse': '#7fff00', 'chocolate': '#d2691e', 'coral': '#ff7f50', 'cornflowerblue': '#6495ed', 'cornsilk': '#fff8dc', 'crimson': '#dc143c', 'cyan': '#00ffff'}
```

After running the script for *colors2.json*, the output is:

```
Reading JSON data from 'colors2.json' ...

{'aliceblue': [240, 248, 255, 1], 'antiquewhite': [250, 235, 215, 1], 'aqua': [0, 255, 255, 1], 'aquamarine': [127, 255, 212, 1], 'azure': [240, 255, 255, 1], 'beige': [245, 245, 220, 1], 'bisque': [255, 228, 196, 1], 'black': [0, 0, 0, 1], 'blanchedalmond': [255, 235, 205, 1], 'blue': [0, 0, 255, 1], 'blueviolet': [138, 43, 226, 1], 'brown': [165, 42, 42, 1], 'burlywood': [222, 184, 135, 1], 'cadetblue': [95, 158, 160, 1], 'chartreuse': [127, 255, 0, 1], 'chocolate': [210, 105, 30, 1], 'coral': [255, 127, 80, 1], 'cornflowerblue': [100, 149, 237, 1], 'cornsilk': [255, 248, 220, 1], 'crimson': [220, 20, 60, 1], 'cyan': [0, 255, 255, 1]}
```

**Writing JSON data to a file**

Next, let's see an application that writes JSON data to a file:

```python
#!/usr/bin/env python3
# Run it as -> ./script name_of_json_file (./script data)

import sys
import json

data = {
  "aliceblue": "#f0f8ff",
  "antiquewhite": "#faebd7",
  "aqua": "#00ffff",
  "aquamarine": "#7fffd4",
  "azure": "#f0ffff"
}

def main():
    filename = sys.argv[1] + ".json"
    print(f"\nWriting JSON data to '{filename}' ...\n")
    if len(sys.argv) != 2:
        print("Please supply a filename only!\n\n")
        raise SystemExit(1)
    with open(filename, 'w') as f:
        json.dump(data, f)

if __name__ == '__main__':
    main()
```

After running the script to *data.json*, the output is:

```json
{"aliceblue": "#f0f8ff", "antiquewhite": "#faebd7", "aqua": "#00ffff", "aquamarine": "#7fffd4", "azure": "#f0ffff"}
```
