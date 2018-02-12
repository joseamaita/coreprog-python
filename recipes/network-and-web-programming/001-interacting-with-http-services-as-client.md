# Python Recipe for Network and Web Programming

## Interacting with HTTP services as a client

### Problem

You need to access various services via HTTP as a client. For example, 
downloading data or interacting with a REST-based API.

### Solution

For simple things, it's usually easy enough to use the `urllib.request` 
module.

**Making a basic GET request**

For example, to send a simple HTTP `GET` request to a remote 
service, do something like this:

```python
>>> # A basic GET request
...
>>> from urllib import request, parse
>>> # Base URL being accessed
...
>>> url = 'http://httpbin.org/get'
>>> # Dictionary of query parameters (if any)
...
>>> parms = {
... 'name1': 'value1',
... 'name2': 'value2',
... }
>>> # Encode the query string
...
>>> querystring = parse.urlencode(parms)
>>> querystring
'name1=value1&name2=value2'
>>> # Make a GET request and read the response
...
>>> u = request.urlopen(url+'?' + querystring)
>>> u
<http.client.HTTPResponse object at 0x7f67342e7550>
>>> resp = u.read()
>>> resp
b'{\n  "args": {\n    "name1": "value1", \n    "name2": "value2"\n  }, \n  "headers": {\n    "Accept-Encoding": "identity", \n    "Connection": "close", \n    "Host": "httpbin.org", \n    "User-Agent": "Python-urllib/3.6"\n  }, \n  "origin": "190.198.181.54", \n  "url": "http://httpbin.org/get?name1=value1&name2=value2"\n}\n'
>>> import json
>>> from pprint import pprint
>>> json_resp = json.loads(resp.decode('utf-8'))
>>> json_resp
{'args': {'name1': 'value1', 'name2': 'value2'}, 'headers': {'Accept-Encoding': 'identity', 'Connection': 'close', 'Host': 'httpbin.org', 'User-Agent': 'Python-urllib/3.6'}, 'origin': '190.198.181.54', 'url': 'http://httpbin.org/get?name1=value1&name2=value2'}
>>> pprint(json_resp, indent=4)
{   'args': {'name1': 'value1', 'name2': 'value2'},
    'headers': {   'Accept-Encoding': 'identity',
                   'Connection': 'close',
                   'Host': 'httpbin.org',
                   'User-Agent': 'Python-urllib/3.6'},
    'origin': '190.198.181.54',
    'url': 'http://httpbin.org/get?name1=value1&name2=value2'}
```

**Making a basic POST request**

If you need to send the query parameters in the request body using 
a `POST` method, encode them and supply them as an optional argument 
to `urlopen()` like this:

```python
>>> # A basic POST request
...
>>> from urllib import request, parse
>>> # Base URL being accessed
...
>>> url = 'http://httpbin.org/post'
>>> # Dictionary of query parameters (if any)
...
>>> parms = {
... 'name1': 'value1',
... 'name2': 'value2',
... }
>>> # Encode the query string
...
>>> querystring = parse.urlencode(parms)
>>> querystring
'name1=value1&name2=value2'
>>> # Make a POST request and read the response
...
>>> u = request.urlopen(url, querystring.encode('ascii'))
>>> u
<http.client.HTTPResponse object at 0x7ff7d5e1f710>
>>> resp = u.read()
>>> resp
b'{\n  "args": {}, \n  "data": "", \n  "files": {}, \n  "form": {\n    "name1": "value1", \n    "name2": "value2"\n  }, \n  "headers": {\n    "Accept-Encoding": "identity", \n    "Connection": "close", \n    "Content-Length": "25", \n    "Content-Type": "application/x-www-form-urlencoded", \n    "Host": "httpbin.org", \n    "User-Agent": "Python-urllib/3.6"\n  }, \n  "json": null, \n  "origin": "190.198.181.54", \n  "url": "http://httpbin.org/post"\n}\n'
>>> import json
>>> from pprint import pprint
>>> json_resp = json.loads(resp.decode('utf-8'))
>>> json_resp
{'args': {}, 'data': '', 'files': {}, 'form': {'name1': 'value1', 'name2': 'value2'}, 'headers': {'Accept-Encoding': 'identity', 'Connection': 'close', 'Content-Length': '25', 'Content-Type': 'application/x-www-form-urlencoded', 'Host': 'httpbin.org', 'User-Agent': 'Python-urllib/3.6'}, 'json': None, 'origin': '190.198.181.54', 'url': 'http://httpbin.org/post'}
>>> pprint(json_resp, indent=4)
{   'args': {},
    'data': '',
    'files': {},
    'form': {'name1': 'value1', 'name2': 'value2'},
    'headers': {   'Accept-Encoding': 'identity',
                   'Connection': 'close',
                   'Content-Length': '25',
                   'Content-Type': 'application/x-www-form-urlencoded',
                   'Host': 'httpbin.org',
                   'User-Agent': 'Python-urllib/3.6'},
    'json': None,
    'origin': '190.198.181.54',
    'url': 'http://httpbin.org/post'}
```

**Making a POST request with some custom HTTP headers**

If you need to supply some custom HTTP headers in the outgoing request 
such as a change to the user-agent field, make a dictionary containing 
their value and create a `Request` instance and pass it to `urlopen()` 
like this:

```python
>>> # A POST request with some custom HTTP headers
...
>>> from urllib import request, parse
>>> # Base URL being accessed
...
>>> url = 'http://httpbin.org/post'
>>> # Dictionary of query parameters (if any)
...
>>> parms = {
... 'name1': 'value1',
... 'name2': 'value2',
... }
>>> # Encode the query string
...
>>> querystring = parse.urlencode(parms)
>>> querystring
'name1=value1&name2=value2'
>>> # Extra headers
...
>>> headers = {
... 'User-agent': 'none/ofyourbusiness',
... 'Spam': 'Eggs',
... }
>>> req = request.Request(url, querystring.encode('ascii'), headers=headers)
>>> req
<urllib.request.Request object at 0x7fed36f14ba8>
>>> # Make a request and read the response
...
>>> u = request.urlopen(req)
>>> u
<http.client.HTTPResponse object at 0x7fed346b1780>
>>> resp = u.read()
>>> resp
b'{\n  "args": {}, \n  "data": "", \n  "files": {}, \n  "form": {\n    "name1": "value1", \n    "name2": "value2"\n  }, \n  "headers": {\n    "Accept-Encoding": "identity", \n    "Connection": "close", \n    "Content-Length": "25", \n    "Content-Type": "application/x-www-form-urlencoded", \n    "Host": "httpbin.org", \n    "Spam": "Eggs", \n    "User-Agent": "none/ofyourbusiness"\n  }, \n  "json": null, \n  "origin": "190.198.181.54", \n  "url": "http://httpbin.org/post"\n}\n'
>>> import json
>>> from pprint import pprint
>>> json_resp = json.loads(resp.decode('utf-8'))
>>> json_resp
{'args': {}, 'data': '', 'files': {}, 'form': {'name1': 'value1', 'name2': 'value2'}, 'headers': {'Accept-Encoding': 'identity', 'Connection': 'close', 'Content-Length': '25', 'Content-Type': 'application/x-www-form-urlencoded', 'Host': 'httpbin.org', 'Spam': 'Eggs', 'User-Agent': 'none/ofyourbusiness'}, 'json': None, 'origin': '190.198.181.54', 'url': 'http://httpbin.org/post'}
>>> pprint(json_resp, indent=4)
{   'args': {},
    'data': '',
    'files': {},
    'form': {'name1': 'value1', 'name2': 'value2'},
    'headers': {   'Accept-Encoding': 'identity',
                   'Connection': 'close',
                   'Content-Length': '25',
                   'Content-Type': 'application/x-www-form-urlencoded',
                   'Host': 'httpbin.org',
                   'Spam': 'Eggs',
                   'User-Agent': 'none/ofyourbusiness'},
    'json': None,
    'origin': '190.198.181.54',
    'url': 'http://httpbin.org/post'}
```
