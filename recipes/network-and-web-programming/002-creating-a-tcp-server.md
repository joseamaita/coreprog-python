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

**Creating an echo server that uses the StreamRequestHandler base class**

In many cases, it may be easier to define a slightly different kind of 
handler. Here is an example that uses the `StreamRequestHandler` base 
class to put a file-like interface on the underlying socket:

```python
#!/usr/bin/env python3

from socketserver import StreamRequestHandler, TCPServer

class EchoHandler(StreamRequestHandler):

    def handle(self):
        print(f'Got connection from {self.client_address}')
        # self.rfile is a file-like object for reading
        for line in self.rfile:
            # self.wfile is a file-like object for writing
            self.wfile.write(line)

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
Got connection from ('127.0.0.1', 56468)
^C

Leaving.
```

### Discussion

The `socketserver` library makes it relatively easy to create simple TCP 
servers. However, you should be aware that, by default, the servers are 
single threaded and can only serve one client at a time.

**Creating an echo server that handles multiple clients**

If you want to handle multiple clients, either instantiate 
a `ForkingTCPServer` or `ThreadingTCPServer` object instead. For 
example:

```python
#!/usr/bin/env python3

from socketserver import StreamRequestHandler, ThreadingTCPServer

class EchoHandler(StreamRequestHandler):

    def handle(self):
        print(f'Got connection from {self.client_address}')
        # self.rfile is a file-like object for reading
        for line in self.rfile:
            # self.wfile is a file-like object for writing
            self.wfile.write(line)

def main():
    try:
        serv = ThreadingTCPServer(('', 20000), EchoHandler)
        print('Echo server running on port 20000')
        serv.serve_forever()

    except KeyboardInterrupt:
        print("\n\nLeaving.")
        raise SystemExit(1)

if __name__ == '__main__':
    main()
```

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
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
>>> s.close()
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
```

The server script output is:

```
Echo server running on port 20000
Got connection from ('127.0.0.1', 56641)
Got connection from ('127.0.0.1', 56645)
Got connection from ('127.0.0.1', 56649)
^C

Leaving.
```

**Creating a pre-allocated pool of worker threads or processes**

One issue with forking and threaded servers is that they spawn a new 
process or thread on each client connection. There is no upper bound on 
the number of allowed clients, so a malicious hacker could potentially 
launch a large number of simultaneous connections in an effort to make 
your server explode.

If this is a concern, you can create a pre-allocated pool of worker 
threads or processes. To do this, you create an instance of a normal 
nonthreaded server, but then launch the `serve_forever()` method in a 
pool of multiple threads. For example:

```python
#!/usr/bin/env python3

from socketserver import StreamRequestHandler, TCPServer

class EchoHandler(StreamRequestHandler):

    def handle(self):
        print(f'Got connection from {self.client_address}')
        # self.rfile is a file-like object for reading
        for line in self.rfile:
            # self.wfile is a file-like object for writing
            self.wfile.write(line)

def main():
    try:
        from threading import Thread
        NWORKERS = 16
        serv = TCPServer(('', 20000), EchoHandler)
        for n in range(NWORKERS):
            t = Thread(target=serv.serve_forever)
            t.daemon = True
            t.start()
        print('Multithreaded server running on port 20000')
        serv.serve_forever()

    except KeyboardInterrupt:
        print("\n\nLeaving.")
        raise SystemExit(1)

if __name__ == '__main__':
    main()
```

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
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
>>> s.close()
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
```

The server script output is:

```
Multithreaded server running on port 20000
Got connection from ('127.0.0.1', 56661)
Got connection from ('127.0.0.1', 56665)
Got connection from ('127.0.0.1', 56667)
^C

Leaving.
```

**Adjusting the TCP server socket by setting options**

Normally, a `TCPServer` binds and activates the underlying socket upon 
instantiation. However, sometimes you might want to adjust the 
underlying socket by setting options. To do this, supply 
the `bind_and_activate=False` argument, like this:

```python
#!/usr/bin/env python3

from socketserver import StreamRequestHandler, TCPServer

class EchoHandler(StreamRequestHandler):

    def handle(self):
        print(f'Got connection from {self.client_address}')
        # self.rfile is a file-like object for reading
        for line in self.rfile:
            # self.wfile is a file-like object for writing
            self.wfile.write(line)

def main():
    try:
        import socket
        serv = TCPServer(('', 20000), EchoHandler, bind_and_activate=False)
        # Set up various socket options
        serv.socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, True)
        # Bind and activate
        serv.server_bind()
        serv.server_activate()
        print('Echo server running on port 20000')
        serv.serve_forever()

    except KeyboardInterrupt:
        print("\n\nLeaving.")
        raise SystemExit(1)

if __name__ == '__main__':
    main()
```

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
Got connection from ('127.0.0.1', 56668)
^C

Leaving.
```

**Setting the socket option on TCPServer**

The socket option shown above is actually a very common setting that 
allows the server to rebind to a previously used port number. It's 
actually so common that it's a class variable that can be set 
on `TCPServer`. Set it before instantiating the server, as shown in this
example:

```python
#!/usr/bin/env python3

from socketserver import StreamRequestHandler, TCPServer

class EchoHandler(StreamRequestHandler):

    def handle(self):
        print(f'Got connection from {self.client_address}')
        # self.rfile is a file-like object for reading
        for line in self.rfile:
            # self.wfile is a file-like object for writing
            self.wfile.write(line)

def main():
    try:
        TCPServer.allow_reuse_address = True
        serv = TCPServer(('', 20000), EchoHandler)
        print('Echo server running on port 20000')
        serv.serve_forever()

    except KeyboardInterrupt:
        print("\n\nLeaving.")
        raise SystemExit(1)

if __name__ == '__main__':
    main()
```

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
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
>>> s.close()
>>> s = socket(AF_INET, SOCK_STREAM)
>>> s.connect(('localhost', 20000))
>>> s.close()
```

The server script output is:

```
Echo server running on port 20000
Got connection from ('127.0.0.1', 56899)
Got connection from ('127.0.0.1', 56900)
Got connection from ('127.0.0.1', 56901)
^C

Leaving.
```
