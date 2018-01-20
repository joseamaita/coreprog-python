# Python Application focusing Classes and Objects

## Simple shapes module for a drawing program

### Version A

Here, we present an example that might be the start of a simple shapes 
module for a drawing program:

```python
#!/usr/bin/env python3
# sh.py
# Simple shapes module for a drawing program

# Most of the code were taken from Naomi Ceder's "The Quick Python Book"

"""sh module. Contains classes Shape, Square and Circle"""

import math

class Shape:
    """Shape class: has method move"""

    def __init__(self, x, y):
        self.x = x
        self.y = y

    def move(self, deltaX, deltaY):
        self.x = self.x + deltaX
        self.y = self.y + deltaY

class Square(Shape):
    """Square class: inherits from Shape and has method area"""

    def __init__(self, side=1, x=0, y=0):
        Shape.__init__(self, x, y)
        self.side = side

    def area(self):
        """Square area method: returns the area of the square."""
        return pow(self.side, 2)

    def __str__(self):
        return f"Square of side {self.side} at coordinates "\
               f"({self.x}, {self.y})"

class Circle(Shape):
    """Circle class: inherits from Shape and has method area"""
    π = math.pi

    def __init__(self, r=1, x=0, y=0):
        Shape.__init__(self, x, y)
        self.radius = r

    def area(self):
        """Circle area method: returns the area of the circle."""
        return self.π * pow(self.radius, 2)

    def __str__(self):
        return f"Circle of radius {self.radius} at coordinates "\
               f"({self.x}, {self.y})"

def main():
    print('--------------------------------------------------')
    print('   Simple shapes module for a drawing program')
    print('--------------------------------------------------')
    print()
    print("sh module. Contains classes Shape, Square and Circle")
    print(f"Shape docstring -> {Shape.__doc__}")
    print(f"Square docstring -> {Square.__doc__}")
    print(f"Circle docstring -> {Circle.__doc__}")
    print(f"Square.area docstring -> {Square.area.__doc__}")
    print(f"Circle.area docstring -> {Circle.area.__doc__}")
    print("Creating Square instances ...")
    sq1 = Square()
    sq3 = Square(3, 4, 8)
    print("Creating Circle instances ...")
    c1 = Circle()
    c5 = Circle(5, 15, 20)
    print("Shapes:")
    print(f"sq1 -> {sq1}")
    print(f"sq3 -> {sq3}")
    print(f"c1 -> {c1}")
    print(f"c5 -> {c5}")
    print()
    print(f"Area of sq1 is: {sq1.area()}")
    print(f"Area of sq3 is: {sq3.area()}")
    print(f"Area of c1 is: {c1.area()}")
    print(f"Area of c5 is: {c5.area()}")
    print()
    print("Moving Square instances -> x=+7, y=+14")
    sq1.move(7, 14)
    sq3.move(7, 14)
    print("Moving Circle instances -> x=+5, y=+6")
    c1.move(5, 6)
    c5.move(5, 6)
    print()
    print("Shapes:")
    print(f"sq1 -> {sq1}")
    print(f"sq3 -> {sq3}")
    print(f"c1 -> {c1}")
    print(f"c5 -> {c5}")

if __name__ == '__main__':
    main()
```

Import the `sh` module to make all classes available:

```python
>>> import sh
```

Display the module's docstring:

```python
>>> sh.__doc__
'sh module. Contains classes Shape, Square and Circle'
```

Display the `Shape`, `Square` and `Circle` classes docstrings:

```python
>>> sh.Shape.__doc__
'Shape class: has method move'
>>> sh.Square.__doc__
'Square class: inherits from Shape and has method area'
>>> sh.Circle.__doc__
'Circle class: inherits from Shape and has method area'
```

Display the docstring for the `area` method of the `Square` and `Circle` 
classes:

```python
>>> sh.Square.area.__doc__
'Square area method: returns the area of the square.'
>>> sh.Circle.area.__doc__
'Circle area method: returns the area of the circle.'
```

Create two `Square` instances with the following features:

* Default side (side=1) and default position (0, 0)
* Side 3 (side=3) and position (4, 8)

```python
>>> sq1 = sh.Square()
>>> sq1.side
1
>>> print(sq1)
Square of side 1 at coordinates (0, 0)
>>> sq3 = sh.Square(3, 4, 8)
>>> sq3.side
3
>>> print(sq3)
Square of side 3 at coordinates (4, 8)
```

Create two `Circle` instances with the following features:

* Default radius (r=1) and default position (0, 0)
* Radius 5 (r=5) and position (15, 20)

```python
>>> c1 = sh.Circle()
>>> c1.radius
1
>>> print(c1)
Circle of radius 1 at coordinates (0, 0)
>>> c5= sh.Circle(5, 15, 20)
>>> c5.radius
5
>>> print(c5)
Circle of radius 5 at coordinates (15, 20)
```

Now, calculate the areas of the `Square` and `Circle` instances:

```python
>>> sq1.area()
1
>>> sq3.area()
9
>>> c1.area()
3.141592653589793
>>> c5.area()
78.53981633974483
```

Move 7 spaces in `x` and 14 spaces in `y` for `Square` instances:

```python
>>> sq1.move(7, 14)
>>> print(sq1)
Square of side 1 at coordinates (7, 14)
>>> sq3.move(7, 14)
>>> print(sq3)
Square of side 3 at coordinates (11, 22)
```

Move 5 spaces in `x` and 6 spaces in `y` for `Circle` instances:

```python
>>> c1.move(5, 6)
>>> print(c1)
Circle of radius 1 at coordinates (5, 6)
>>> c5.move(5, 6)
>>> print(c5)
Circle of radius 5 at coordinates (20, 26)
```
