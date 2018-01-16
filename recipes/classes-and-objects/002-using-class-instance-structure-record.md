# Python Recipe for Classes and Objects

## Using a class instance as a structure or record

### Problem

You need to know how to use a class instance as a structure or record.

### Solution

**Version A**

Class instances can be used as structures or records. Unlike C 
structures, the fields of an instance don't need to be declared ahead of 
time but can be created on the fly. The following short example defines 
a class called `Circle`, creates a `Circle` instance, assigns to 
the `radius` field of the circle, and then uses that field to calculate 
the circumference of the circle:

```python
>>> class Circle:
...     pass
...
>>> a_circle = Circle()
>>> a_circle.radius = 4
>>> print(2 * 3.141592 * a_circle.radius)
25.132736
```

Like Java and many other languages, the fields of an instance/structure 
are accessed and assigned to by using dot notation.

You can initialize fields of an instance automatically by including 
an `__init__` initialization method in the class body. This function is 
run every time an instance of the class is created, with that new 
instance as its first argument. The `__init__` method is similar to a 
constructor in Java, but it doesn't really *construct* anything, 
it *initializes* fields of the class. This example creates circles with 
a radius of `1` by default:

```python
>>> class Circle:
...     def __init__(self):
...         self.radius = 1
...
>>> a_circle = Circle()
>>> a_circle
<__main__.Circle object at 0x7f9840741a20>
>>> a_circle.radius
1
>>> print(2 * a_circle.radius * 3.141592)
6.283184
>>> a_circle.radius = 4
>>> print(2 * a_circle.radius * 3.141592)
25.132736
```

By convention, `self` is always the name of the first argument 
of `__init__`. The keyword `self` is set to the newly created circle 
instance when `__init__` is run.
