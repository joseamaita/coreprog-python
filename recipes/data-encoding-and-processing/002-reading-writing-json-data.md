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
