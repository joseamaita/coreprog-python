# Python Recipe for Network and Web Programming

## Creating a TCP server

### Problem

You want to implement a server that communicates with clients using the 
TCP Internet protocol.

### Solution

An easy way to create a TCP server is to use the `socketserver` library.

**Creating a simple echo server with the socketserver library**

For example, here is a simple echo server:

```python
#!/usr/bin/env python3

from socketserver import BaseRequestHandler, TCPServer

class EchoHandler(BaseRequestHandler):

    def handle(self):
        print(f'Got connection from {self.client_address}')
        while True:
            msg = self.request.recv(8192)
            if not msg:
                break
            self.request.send(msg)

def main():
    try:
        serv = TCPServer(('', 20000), EchoHandler)
        print('Echo server running on port 20000')
        serv.serve_forever()

    except KeyboardInterrupt:
        print("\n\nLeaving.")
        raise SystemExit(1)

if __name__ == '__main__':
    main()
```

In this code, you define a special handler class that implements 
a `handle()` method for servicing client connections. The `request` 
attribute is the underlying client socket and `client_address` has 
client address.

To test the server, run it and then open a separate Python process that 
connects to it (client code):

```python
>>> from socket import socket, AF_INET, SOCK_STREAM
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
>>> s.send(b'Hello\n')
6
>>> resp = s.recv(8192)
>>> print(f'Response: {resp}')
Response: b'Hello\n'
>>> s.close()
```

The server script output is:

```
Echo server running on port 20000
Got connection from ('127.0.0.1', 46923)
^C

Leaving.
```
