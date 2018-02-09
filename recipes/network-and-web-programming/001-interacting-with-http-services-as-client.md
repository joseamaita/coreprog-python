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
