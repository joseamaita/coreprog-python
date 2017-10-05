# Getting Started with Python

## Initial setup

### Install Python from source

The following procedure was applied on a Debian-based box and for the 
version 3.6.0:

* First, make sure to have these libraries to build Python in your 
system already installed: `build-essential`, `libreadline-dev`, `tk-dev`
, `libsqlite3-dev`, `libc6-dev`, `libssl-dev`, `libbz2-dev`
, `libgdbm-dev`, `libz-dev`, `libncursesw5-dev`, `libdb-dev`
, `liblzma-dev`, `zlib1g-dev`, `blt-dev`, `python-dev`
, `libncurses5-dev`, and `libexpat1-dev`.
* Go to the [Python's download page](https://www.python.org/downloads/).
* There, download 
the [latest source release](https://www.python.org/ftp/python/3.6.0/Python-3.6.0.tar.xz) 
(in this case, the selected version was 3.6.0).
* Extract the compressed file to a desired folder. For example, you 
could use `~/Python-3.6.0`.
* Open a terminal prompt as root.
* Change directories as needed and enter the designated folder.
* There, run the **configure** script by 
typing `sh configure --enable-optimizations`. Wait until the process is 
completed.
* Then, continue the build process by typing `make`. Wait until the 
process is completed (tests also have to be performed).
* Install the Python version, which live side-by-side with the other 
versions, by typing `make altinstall`. Wait until the process is 
completed (tests also have to be performed again).
* Make sure the Python version is installed by typing `python3.6`. The 
interpreter has to be shown with the following message:

```
Python 3.6.0 (default, Jan 25 2017, 23:55:25) 
[GCC 4.9.2] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

### Create virtual environment

```
$ python3.6 -m venv /home/jose-alberto/.virtualenvs/py360core
```

### Activate virtual environment

```
$ workon py360core
```

### Check the Python version

```
(py360core) $ python -V
Python 3.6.0
```

### Test a Python application

```
(py360core) $ python name_of_python_application.py
```

### Run a Python script from the console

```
-> (within name_of_python_application.py), add this line at the top:
#!/usr/bin/env python3

(py360core) $ chmod +x name_of_python_application.py
(py360core) $ ./name_of_python_application.py
```

### Create very basic programs

**Hello, World!**

```python
#!/usr/bin/env python3

def main():
    print("Hello, World!")

if __name__ == '__main__':
    main()
```

**Custom Hello (A)**

```python
#!/usr/bin/env python3

def main():
    name = input("Enter your name: \n")
    print(f"\nHello, {name}!\n")

if __name__ == '__main__':
    main()
```

**Custom Hello (B)**

```python
#!/usr/bin/env python3
import sys

def main():
    print(f"Hello, {sys.argv[1]}!")

if __name__ == '__main__':
    main()
```

**Custom Hello (C)**

```python
#!/usr/bin/env python3
import sys

def main():
    if len(sys.argv) != 2:
        print("Please supply a first name only!")
        raise SystemExit(1)
    print(f"Hello, {sys.argv[1]}!")

if __name__ == '__main__':
    main()
```

**Custom Hello (D)**

```python
#!/usr/bin/env python3

def main():
    print('---------------------------------')
    print('      HELLO APP')
    print('---------------------------------')
    print()
    user_text = input('What is your name? ')
    print(f"Nice to meet you, {user_text}!\n")

if __name__ == '__main__':
    main()
```

### Deactivate virtual environment

```
(py360core) $ deactivate
```
