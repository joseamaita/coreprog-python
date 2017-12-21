# Python Recipe for Iterators and Generators

## Delegating iteration

### Problem

You have built a custom container object that internally holds a list, 
tuple, or some other iterable. You would like to make iteration work 
with your new container.

### Solution

**Version A**

Typically, all you need to do is define an `__iter__()` method that 
delegates iteration to the internally held container.

Now, let's see the code for the application example:

```python
#!/usr/bin/env python3

class Node:

    def __init__(self, value):
        self._value = value
        self._children = []

    def __repr__(self):
        return f"Node({self._value})"

    def add_child(self, node):
        self._children.append(node)

    def __iter__(self):
        return iter(self._children)

def main():
    print('--------------------------------')
    print('    Delegating iteration')
    print('--------------------------------')
    print()
    root = Node(0)
    child1 = Node(1)
    child2 = Node(2)
    root.add_child(child1)
    root.add_child(child2)
    for ch in root:
        print(ch)

if __name__ == '__main__':
    main()
```

After running the script, the output is:

```python
--------------------------------
    Delegating iteration
--------------------------------

Node(1)
Node(2)
```

In this code, the `__iter__()` method simply forwards the iteration 
request to the internally held `_children` attribute.

### Discussion

Python's iterator protocol requires `__iter__()` to return a special 
iterator object that implements a `__next__()` method to carry out the 
actual iteration. If all you are doing is iterating over the contents of 
another container, you don't really need to worry about the underlying 
details of how it works. All you need to do is to forward the iteration
request along.

The use of the `iter()` function here is a bit of a shortcut that cleans 
up the code. The statement `iter(s)` simply returns the underlying 
iterator by calling `s.__iter__()`, much in the same way that `len(s)` 
invokes `s.__len__()`.
