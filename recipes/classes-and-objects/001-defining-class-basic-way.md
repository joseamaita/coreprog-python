# Python Recipe for Classes and Objects

## Defining a class in a basic way

### Problem

You need a basic way of creating a class.

### Solution

**Version A**

A *class* in Python is effectively a data type. All the data types built 
into Python are classes, and Python gives you powerful tools to 
manipulate every aspect of a class's behavior. You define a class with 
the `class` statement:

```python
class MyClass:
    body
```

The code block `body` is a list of Python statements, typically variable 
assignments and function definitions. No assignments or function 
definitions are required. The body can be just a single `pass` 
statement, like this:

```python
>>> class MyClass:
...     pass
...
```

By convention, class identifiers are in **CapCase**, that is, the first 
letter of each component word is capitalized, to make them stand out. 
After you define the class, a new object of the class type (an instance 
of the class) can be created by calling the class name as a function:

```python
>>> instance_class = MyClass()
>>> instance_class
<__main__.MyClass object at 0x7f687ad699b0>
```
