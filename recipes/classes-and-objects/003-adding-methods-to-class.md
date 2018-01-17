# Python Recipe for Classes and Objects

## Adding methods to a class

### Problem

You need to know how to add methods to a class.

### Solution

**Version A**

A *method* is a function associated with a particular class. Remember 
the special `__init__` method, which is called on a new instance when 
that instance is first created. In the following example, we define 
another method, `area`, for the `Circle` class, which can be used to 
calculate and return the area for any `Circle` instance. Like most 
user-defined methods, `area` is called with a *method invocation syntax* 
that resembles instance variable access:

```python
>>> class Circle:
...     def __init__(self):
...         self.radius = 1
...     def area(self):
...         return self.radius * self.radius * 3.141592
...
>>> c = Circle()
>>> c
<__main__.Circle object at 0x7f399618c3c8>
>>> c.area()
3.141592
>>> c.radius = 4
>>> c.area()
50.265472
```

Method invocation syntax consists of an instance, followed by a period, 
followed by the method to be invoked on the instance. This syntax is 
sometimes called *bound* method invocation.

Like `__init__`, the `area` method is defined as a function within the 
body of the class definition. The first argument of any method is the 
instance it was invoked by or on, named `self` by convention.

Methods can be invoked with arguments, if the method definitions accept 
those arguments. This version of `Circle` adds an argument to 
the `__init__` method, so that we can create circles of a given radius 
without needing to set the radius after a circle is created:

```python
>>> class Circle:
...     def __init__(self, radius):
...         self.radius = radius
...     def area(self):
...         return self.radius * self.radius * 3.141592
...
```

Note the two uses of `radius` here. `self.radius` is the instance 
variable called `radius`. `radius` by itself is the local function 
variable called `radius`. The two aren't the same! In practice, we'd 
probably call the local function variable something like `r` or `rad`, 
to avoid any possibility of confusion.

Using this definition of `Circle`, we can create circles of any radius 
with one call on the `Circle` class. The following creates a `Circle` of 
radius 5:

```python
>>> c = Circle(5)
>>> c
<__main__.Circle object at 0x7f43a6b67b00>
>>> c.radius
5
```

All the standard Python function features, like default argument values, 
extra arguments, keyword arguments, and so forth, can be used with 
methods. For example, we could have defined the first line of `__init__` 
to be:

```python
def __init__(self, radius=1):
```

Now, let's rewrite the `Circle` class definition:

```python
>>> class Circle:
...     def __init__(self, r=1):
...         self.radius = r
...     def area(self):
...         return self.radius * self.radius * 3.141592
...
```

Then, calls to `Circle` would work with or without an extra argument. 
The `Circle()` call would return a circle of radius 1, and `Circle(3)` 
would return a circle of radius 3. Let's see:

```python
>>> c1 = Circle()
>>> c1.radius
1
>>> c3 = Circle(3)
>>> c3.radius
3
```
