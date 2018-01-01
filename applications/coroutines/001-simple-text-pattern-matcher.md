# Python Application focusing Coroutines

## Simple text pattern matcher

### Version A

Here, we create a first simple example of a coroutine function. This 
function receives lines and prints out those that contain a substring.

Now, let's see the code for the application:

```python
#!/usr/bin/env python3
# grep.py
# Simple text pattern matcher
# A coroutine that matches a text pattern like Unix 'grep text'

# Most of the code were taken from David Beazley's web site at
# http://www.dabeaz.com/coroutines/grep.py

tp = "python"

tp_tomatch = ["Yeah, but no, but yeah, but no", 
              "A series of tubes", 
              "python generators rock!", 
              "python is easy and fun because ...", 
             ]

def grep(text_pattern):
    print(f"Looking for '{text_pattern}'\n\n")
    while True:
        line = (yield)    # Get a line of text
        if text_pattern in line:
            print(line)

def main():
    print('-----------------------------------')
    print('   Simple text pattern matcher')
    print('-----------------------------------')
    print()
    g = grep(tp)
    next(g)
    for tptm in tp_tomatch:
        g.send(tptm)

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```
-----------------------------------
   Simple text pattern matcher
-----------------------------------

Looking for 'python'


python generators rock!
python is easy and fun because ...
```
