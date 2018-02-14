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

**Making a POST request using requests library**

If your interaction with a service is more complicated than the code 
above, you should probably look at the `requests` library. For example, 
here is equivalent `requests` code for the preceding operations (make 
sure the `requests` module is already installed):

```python
>>> # A POST request using requests library
...
>>> import requests
>>> # Base URL being accessed
...
>>> url = 'http://httpbin.org/post'
>>> # Dictionary of query parameters (if any)
...
>>> parms = {
... 'name1': 'value1',
... 'name2': 'value2',
... }
>>> # Extra headers
...
>>> headers = {
... 'User-agent': 'none/ofyourbusiness',
... 'Spam': 'Eggs',
... }
>>> resp = requests.post(url, data=parms, headers=headers)
>>> resp
<Response [200]>
>>> # Decoded text returned by the request
...
>>> text = resp.text
>>> text
'{\n  "args": {}, \n  "data": "", \n  "files": {}, \n  "form": {\n    "name1": "value1", \n    "name2": "value2"\n  }, \n  "headers": {\n    "Accept": "*/*", \n    "Accept-Encoding": "gzip, deflate", \n    "Connection": "close", \n    "Content-Length": "25", \n    "Content-Type": "application/x-www-form-urlencoded", \n    "Host": "httpbin.org", \n    "Spam": "Eggs", \n    "User-Agent": "none/ofyourbusiness"\n  }, \n  "json": null, \n  "origin": "190.198.181.54", \n  "url": "http://httpbin.org/post"\n}\n'
>>> content = resp.content
>>> content
b'{\n  "args": {}, \n  "data": "", \n  "files": {}, \n  "form": {\n    "name1": "value1", \n    "name2": "value2"\n  }, \n  "headers": {\n    "Accept": "*/*", \n    "Accept-Encoding": "gzip, deflate", \n    "Connection": "close", \n    "Content-Length": "25", \n    "Content-Type": "application/x-www-form-urlencoded", \n    "Host": "httpbin.org", \n    "Spam": "Eggs", \n    "User-Agent": "none/ofyourbusiness"\n  }, \n  "json": null, \n  "origin": "190.198.181.54", \n  "url": "http://httpbin.org/post"\n}\n'
>>> from pprint import pprint
>>> pprint(resp.json(), indent=4)
{   'args': {},
    'data': '',
    'files': {},
    'form': {'name1': 'value1', 'name2': 'value2'},
    'headers': {   'Accept': '*/*',
                   'Accept-Encoding': 'gzip, deflate',
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

A notable feature of `requests` is how it returns the resulting response 
content from a request. As shown, the `resp.text` attribute gives you 
the Unicode decoded text of a request. However, if you 
access `resp.content`, you get the raw binary content instead. On the 
other hand, if you access `resp.json()`, then you get the response 
content interpreted as JSON.

**Making a HEAD request using requests library**

Here is an example of using `requests` to make a `HEAD` request and 
extract a few fields of header data from the response:

```python
>>> # A HEAD request using requests library
...
>>> import requests
>>> resp = requests.head('https://www.python.org/')
>>> resp
<Response [200]>
>>> status = resp.status_code
>>> status
200
>>> headers = resp.headers
>>> headers
{'Server': 'nginx', 'Content-Type': 'text/html; charset=utf-8', 'X-Frame-Options': 'SAMEORIGIN', 'x-xss-protection': '1; mode=block', 'X-Clacks-Overhead': 'GNU Terry Pratchett', 'Via': '1.1 varnish, 1.1 varnish', 'Fastly-Debug-Digest': 'a63ab819df3b185a89db37a59e39f0dd85cf8ee71f54bbb42fae41670ae56fd2', 'Content-Length': '48869', 'Accept-Ranges': 'bytes', 'Date': 'Fri, 09 Feb 2018 16:57:29 GMT', 'Age': '2916', 'Connection': 'keep-alive', 'X-Served-By': 'cache-iad2130-IAD, cache-mia17622-MIA', 'X-Cache': 'HIT, HIT', 'X-Cache-Hits': '6, 28', 'X-Timer': 'S1518195449.085108,VS0,VE0', 'Vary': 'Cookie', 'Strict-Transport-Security': 'max-age=63072000; includeSubDomains'}
>>> content_type = resp.headers['content-type']
>>> content_type
'text/html; charset=utf-8'
>>> content_length = resp.headers['content-length']
>>> content_length
'48869'
>>> server = resp.headers['server']
>>> server
'nginx'
```
