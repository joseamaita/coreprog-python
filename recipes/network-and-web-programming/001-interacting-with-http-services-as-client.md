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

**Executing a login into the PyPI using basic authentication**

Here is a `requests` example that executes a login into the Python 
Package Index using basic authentication:

```python
>>> # A login into the PyPI using basic authentication
...
>>> import os
>>> user = os.getenv('PYPI_USERNAME')
>>> password = os.getenv('PYPI_PASSWORD')
>>> import requests
>>> session = requests.Session()
>>> session.auth = (user, password)
>>> auth = session.post('https://pypi.python.org/pypi?:action=login')
>>> auth
<Response [200]>
>>> resp = session.get('https://pypi.python.org/pypi?:action=login')
>>> resp
<Response [200]>
>>> from pprint import pprint
>>> pprint(resp.text)
('<?xml version="1.0" encoding="utf-8"?>\n'
 '<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" '
 '"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">\n'
 '\n'
 '  <html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">\n'
 '    <head>\n'
 '      \n'
 '      <meta content="text/html; charset=utf-8" http-equiv="content-type"/>\n'
 '      <title>PyPI - the Python Package Index : Python Package Index</title>\n'
 '      <meta content="python programming language object oriented web free '
 'source package index download software"/>\n'
 '      <meta content="The Python Package Index is a repository of software '
 'for the Python programming language."/>\n'
 '       <link rel="alternate" type="application/rss+xml" title="RSS: 40 '
 'latest updates" href="https://pypi.python.org/pypi?:action=rss"/>\n'
 '       <link rel="alternate" type="application/rss+xml" title="RSS: 40 '
 'newest packages" href="https://pypi.python.org/pypi?:action=packages_rss"/>\n'
 '       <link rel="stylesheet" media="screen" '
 'href="/static/styles/screen-switcher-default.css" type="text/css"/>\n'
 '       <link media="screen" href="/static/styles/netscape4.css" '
 'type="text/css" rel="stylesheet"/>\n'
 '       <link media="print" href="/static/styles/print.css" type="text/css" '
 'rel="stylesheet"/>\n'
 '       <link media="screen" href="/static/styles/largestyles.css" '
 'type="text/css" rel="alternate stylesheet" title="large text"/>\n'
 '       <link media="screen" href="/static/styles/defaultfonts.css" '
 'type="text/css" rel="alternate stylesheet" title="default fonts"/>\n'
 '       <link rel="stylesheet" media="screen" href="/static/css/docutils.css" '
 'type="text/css"/>\n'
...
'            </li><li class=""><a href="http://www.python.org/community" '
 'class="" title="">Community</a>\n'
 '            </li><li class=""><a href="http://www.python.org/psf" class="" '
 'title="Python Software Foundation">Foundation</a>\n'
 '            </li><li class=""><a href="http://www.python.org/dev" class="" '
 'title="Python Core Language Development">Core Development</a>\n'
 '          </li>\n'
 '          </ul>\n'
 '        </div>\n'
 '\n'
 '      </div>\n'
 '      <div id="content-body">\n'
 '        <div id="body-main">\n'
 '          <div id="content">\n'
 '\n'
 '            <div id="breadcrumb">\n'
 '              <a href="/pypi">Package Index</a>\n'
 '              \n'
 '              \n'
 '\n'
 '            </div>\n'
 '\n'
 '            <div id="document-floating">\n'
 '\n'
 '            <div id="document-navigation" style="overflow-y: auto; '
 'max-height: 15em; overflow-x: hidden;">\n'
 '\t\t\n'
 '\n'
 '\t\t\n'
 '\n'
 '                  <h4>Welcome joseamaita</h4>\n'
 '                  <li>\n'
 '                    <a href="/pypi?%3Aaction=user_form">Your details</a>\n'
 '                    (<a href="/pypi?%3Aaction=logout">Logout</a>)\n'
 '                  </li>\n'
 '\n'
 '                  \n'
 '                    \n'
 '                  \n'
 '\n'
 '\t\t\n'
 '\n'
 '                <div id="statusdiv">\n'
 '                </div>\n'
 '            </div>\n'
 '        </div>\n'
 '        \n'
 '\n'
 '\n'
 '            <div class="section">\n'
 '              <h1>PyPI - the Python Package Index</h1>\n'
 '\n'
 '              \n'
 '<p>The Python Package Index is a repository of software for the Python\n'
 'programming language. There are currently\n'
 '<strong>129305</strong>\n'
 'packages here.\n'
 '<br/>\n'
...
```

**Persisting some cookies across requests**

The `Session` object allows you to persist certain parameters across 
requests. It also persists cookies across all requests made from 
the `Session` instance, and will use `urllib3`'s connection pooling. So, 
if you're making several requests to the same host, the underlying TCP 
connection will be reused, which can result in a significant performance 
increase (HTTP persistent connection).

```python
>>> # A persistent cookie across requests
...
>>> import requests
>>> session = requests.Session()
>>> resp1 = session.get('http://httpbin.org/cookies/set/sessioncookie/123456789')
>>> resp1
<Response [200]>
>>> resp2 = session.get('http://httpbin.org/cookies')
>>> resp2
<Response [200]>
>>> from pprint import pprint
>>> pprint(resp2.text)
'{\n  "cookies": {\n    "sessioncookie": "123456789"\n  }\n}\n'
>>> pprint(resp2.json())
{'cookies': {'sessioncookie': '123456789'}}
```

**Providing default data to the request methods**

Sessions can also be used to provide default data to the request 
methods. This is done by providing data to the properties on a `Session` 
object:

```python
>>> # Provide default data to headers
>>> import requests
>>> session = requests.Session()
>>> session.headers.update({'x-test': 'true'})
>>> session.headers
{'User-Agent': 'python-requests/2.18.4', 'Accept-Encoding': 'gzip, deflate', 'Accept': '*/*', 'Connection': 'keep-alive', 'x-test': 'true'}
>>> # both 'x-test' and 'x-test2' are sent
...
>>> resp = session.get('http://httpbin.org/headers', headers={'x-test2': 'true'})
>>> resp
<Response [200]>
>>> from pprint import pprint
>>> pprint(resp.text)
('{\n'
 '  "headers": {\n'
 '    "Accept": "*/*", \n'
 '    "Accept-Encoding": "gzip, deflate", \n'
 '    "Connection": "close", \n'
 '    "Host": "httpbin.org", \n'
 '    "User-Agent": "python-requests/2.18.4", \n'
 '    "X-Test": "true", \n'
 '    "X-Test2": "true"\n'
 '  }\n'
 '}\n')
>>> pprint(resp.json())
{'headers': {'Accept': '*/*',
             'Accept-Encoding': 'gzip, deflate',
             'Connection': 'close',
             'Host': 'httpbin.org',
             'User-Agent': 'python-requests/2.18.4',
             'X-Test': 'true',
             'X-Test2': 'true'}}
```

**Uploading a file using requests library**

Here is an example of using `requests` to upload content (JSON file):

```python
>>> # Upload a JSON file
...
>>> import requests
>>> url = 'http://httpbin.org/post'
>>> files = {'file': ('colors1.json', open('colors1.json', 'rb'))}
>>> resp = requests.post(url, files=files)
>>> resp
<Response [200]>
>>> from pprint import pprint
>>> pprint(resp.text)
('{\n'
 '  "args": {}, \n'
 '  "data": "", \n'
 '  "files": {\n'
 '    "file": "{\\n  \\"aliceblue\\": \\"#f0f8ff\\",\\n  \\"antiquewhite\\": '
 '\\"#faebd7\\",\\n  \\"aqua\\": \\"#00ffff\\",\\n  \\"aquamarine\\": '
 '\\"#7fffd4\\",\\n  \\"azure\\": \\"#f0ffff\\",\\n  \\"beige\\": '
 '\\"#f5f5dc\\",\\n  \\"bisque\\": \\"#ffe4c4\\",\\n  \\"black\\": '
 '\\"#000000\\",\\n  \\"blanchedalmond\\": \\"#ffebcd\\",\\n  \\"blue\\": '
 '\\"#0000ff\\",\\n  \\"blueviolet\\": \\"#8a2be2\\",\\n  \\"brown\\": '
 '\\"#a52a2a\\",\\n  \\"burlywood\\": \\"#deb887\\",\\n  \\"cadetblue\\": '
 '\\"#5f9ea0\\",\\n  \\"chartreuse\\": \\"#7fff00\\",\\n  \\"chocolate\\": '
 '\\"#d2691e\\",\\n  \\"coral\\": \\"#ff7f50\\",\\n  \\"cornflowerblue\\": '
 '\\"#6495ed\\",\\n  \\"cornsilk\\": \\"#fff8dc\\",\\n  \\"crimson\\": '
 '\\"#dc143c\\",\\n  \\"cyan\\": \\"#00ffff\\"\\n}\\n"\n'
 '  }, \n'
 '  "form": {}, \n'
 '  "headers": {\n'
 '    "Accept": "*/*", \n'
 '    "Accept-Encoding": "gzip, deflate", \n'
 '    "Connection": "close", \n'
 '    "Content-Length": "672", \n'
 '    "Content-Type": "multipart/form-data; '
 'boundary=a5de657581a6446b8f853bfec79eb921", \n'
 '    "Host": "httpbin.org", \n'
 '    "User-Agent": "python-requests/2.18.4"\n'
 '  }, \n'
 '  "json": null, \n'
 '  "origin": "190.198.181.54", \n'
 '  "url": "http://httpbin.org/post"\n'
 '}\n')
>>> pprint(resp.json())
{'args': {},
 'data': '',
 'files': {'file': '{\n'
                   '  "aliceblue": "#f0f8ff",\n'
                   '  "antiquewhite": "#faebd7",\n'
                   '  "aqua": "#00ffff",\n'
                   '  "aquamarine": "#7fffd4",\n'
                   '  "azure": "#f0ffff",\n'
                   '  "beige": "#f5f5dc",\n'
                   '  "bisque": "#ffe4c4",\n'
                   '  "black": "#000000",\n'
                   '  "blanchedalmond": "#ffebcd",\n'
                   '  "blue": "#0000ff",\n'
                   '  "blueviolet": "#8a2be2",\n'
                   '  "brown": "#a52a2a",\n'
                   '  "burlywood": "#deb887",\n'
                   '  "cadetblue": "#5f9ea0",\n'
                   '  "chartreuse": "#7fff00",\n'
                   '  "chocolate": "#d2691e",\n'
                   '  "coral": "#ff7f50",\n'
                   '  "cornflowerblue": "#6495ed",\n'
                   '  "cornsilk": "#fff8dc",\n'
                   '  "crimson": "#dc143c",\n'
                   '  "cyan": "#00ffff"\n'
                   '}\n'},
 'form': {},
 'headers': {'Accept': '*/*',
             'Accept-Encoding': 'gzip, deflate',
             'Connection': 'close',
             'Content-Length': '672',
             'Content-Type': 'multipart/form-data; '
                             'boundary=a5de657581a6446b8f853bfec79eb921',
             'Host': 'httpbin.org',
             'User-Agent': 'python-requests/2.18.4'},
 'json': None,
 'origin': '190.198.181.54',
 'url': 'http://httpbin.org/post'}
```
