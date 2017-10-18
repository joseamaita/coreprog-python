# Python Recipe for Testing, Debugging, and Exceptions

## Using Unittest to Develop Simple and Basic Unit Tests

### Small calculator program

One of the classic examples for demonstrating unit testing is a small 
calculator program. Let's see the first version of the application:

```python
#!/usr/bin/env python3
# calculate.py

class Calculate(object):

    def add(self, x, y):
        return x + y

if __name__ == '__main__':
    calc = Calculate()
    result = calc.add(2, 2)
    print(result)
```

After running the script, the output is:

```
4
```

Now, you have some working code, so why not write the tests to prove it 
and look into what could go wrong if the code is used in ways you didn't 
foresee? Try writing a test that checks to see that if you pass in the 
two numbers as 2, then you get the result as 4. Using the standard 
Python library, you can import the `unittest` package. This provides 
useful methods to make different kinds of assertions (for instance, 
checking whether something meets some condition) on your method. One of 
those assertions you can use is the `assertEqual` method. This method 
allows you to pass in two values and check whether they are equal.

Create a test file called `calculate_test.py`, following the standard 
naming conventions of using the class name under test and appending 
with `_test` (within the same folder). Let's see:

```python
#!/usr/bin/env python3
# calculate_test.py
import unittest
from calculate import Calculate

class TestCalculate(unittest.TestCase):

    def setUp(self):
        self.calc = Calculate()

    def test_add_method_returns_correct_result(self):
        self.assertEqual(4, self.calc.add(2, 2))

if __name__ == '__main__':
    unittest.main()
```

Notice the following things:

* First imports the functionality you need from Python's `unittest` 
module.
* Import your own class, `Calculate`, so that you can test its methods.
* Create a test class `CalculateTest` that 
subclasses `unittest.TestCase`.
* Create an instance of the class under test. You do this in the `setUp` 
method, which is executed before each test, so that you need to define 
your instance only once and have it created before each test.
* Write your test and again the standard is to append your test name 
with `test_*` and explain what the test is doing briefly in the rest of 
the name. Here, you are checking if the add method returns the correct 
result.
* Within the test, you make use of the `assertEqual` method provided by 
the imported `unittest` module. This checks if the first argument is 
equal to the second. Here, you are checking whether 4 is equal to the
result of calling your `add` method on 2 and 2.

After running the test, it passes. The output is:

```python
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

This shows you that your test ran okay, and you ran only the one test. 
What if things go wrong? You can simulate that by breaking the test. 
Change `test_add_method_returns_correct_result` to assert that 2 add 3 
equals 4, then you should see a failing test:

```python
#!/usr/bin/env python3
# calculate_test.py
import unittest
from calculate import Calculate

class TestCalculate(unittest.TestCase):

    def setUp(self):
        self.calc = Calculate()

    def test_add_method_returns_correct_result(self):
        self.assertEqual(4, self.calc.add(2, 3))

if __name__ == '__main__':
    unittest.main()
```

After running the test, it fails. The output is:

```python
F
======================================================================
FAIL: test_add_method_returns_correct_result (__main__.TestCalculate)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "./calculate_test.py", line 12, in test_add_method_returns_correct_result
    self.assertEqual(4, self.calc.add(2, 3))
AssertionError: 4 != 5

----------------------------------------------------------------------
Ran 1 test in 0.000s

FAILED (failures=1)
```

You can see that the `unittest` module provides great feedback as to 
what went wrong and where. You can easily go back and fix the test. Of 
course, a real failure would usually be caused by your code not meeting 
your expectation and producing the wrong result. In that case, you would 
need to go in and fix your code. There you have it. You've written your 
first, simple unit test.
