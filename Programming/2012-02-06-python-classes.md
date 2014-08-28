title: Python Classes
date: 2012-02-06
slug: python-classes
tags: Programming, OOP, Python

This post demonstrates how to write a class in Python
<!-- PELICAN_END_SUMMARY -->

Python supports object orientation but does not impose it. Programmer can choose to write programs entirely as a set of functions and function calls (procedural approach), entirely as classes with not a single user defined function outside a class (object oriented approach) or a mix of the two with both classes and user defined functions outside class definitions. Python supports object orientation features such as inheritance.

In this post, I intend to reimplement the line length calculation as a class. See the previous post where I wrote a simple function to calculate the length of a line in 2D or 3D space.

~~~python
from numpy import array, sum, sqrt

class Line(object):
    def __init__(self, p1, p2):
        self.p1 = p1
        self.p2 = p2

    def Length(self):
        prj = self.p2 - self.p1
        L = sqrt(sum(prj**2))
        return L

    def dc(self):
        L = self.Length()
        prj = self.p2 - self.p1
        return prj / L

def main():
    p1 = array([0.0, 0.0])
    p2 = array([3.0, 4.0])
    L1 = Line(p1, p2)
    print "Length of line = %10.4f", % L1.Length()

if __name__ == '__main__':
    main()
~~~

Assuming the program is saved in a file named `line.py` and the python interpreter is on your `PATH` variable, you can run this program from the command line as follows:

~~~
prompt>python line.py
~~~

The output from the program should look as shown below:

~~~
Length of line =     5.0000
~~~

Here are some points worth noting (if yoy are new to Python):

1. Name of the class is Line. It is a subclass of `object`, the base class for all Python classes. You need not subclass `Line` from `object`. If you don't, the type of class is `<type 'instance'>`. If you do, the type of the class is `<type '__main__.Line'>`. To see this, just add a line `print type(L1)` at the end of the `main()` function. But, a beginner programmercould skip this detail at this point of time.

2. The `Line` class has a constructor `__init__()` and two methods `Length()` and `dc()`.

3. The `self` is the representation of an instance of the class at runtime, required to distinguish between different instances of the class that may be created at any given point of time at runtime. Every method of the class must begin with  `self` in order to access its own member data.

4. All member data must be accessed using `self`. Note that in the constructor  `__init__()`, `p1` is the input parameter and  `self.p1` is the member data. When you call a method in another method of the same class, you must refer to it using `self`. For example, to call the method `Length()` in the method `dc()`, the statement is `self.Line()`.

5. In the `main()` function (which is not a method of the class `Line`), we first create an instance of the `Line` class (`L1 = Line(p1, p2)`). We can access its data and methods by first writing the name of the instance (`L1`), then a dot (`.`) followed by the member data or method. For example, you can print the point `p1` with the statement `print L1.p1`. You can call the method `Length()` with the statement `L = L1,Length()`. Object orientation requires that data be private and methods public. Following that convention, we don't normally access member data in functions that are not methods of the class, but Python does not explicitly make member data private, unless the name (of either member data or method) begins with `__` (two underscores). In such case, they are treated as private, and cannot be accessed by non-member methods.

6. Note that when calling methods, there is no argument corresponding to the parameter `self`. It is the instance behind the dot (`.`) operator.

Here are some things you could try:

1. Create another line, this time in 3D space (3 coordinates for each end point) and calculate its length.
Calculate the direction cosines of the line using the method `dc()`.

2. Add more methods that you think are essential. Can you transform the coordinates of the endpoints of the line if it were to be scaled by a specified factor?

3. Write the special method `__str__(self)` that lets you print information about a `Line`. This function must return a string. If such a function is defined, then you could write a statement such as `print L1`. Then whatever is the string returned by the method `__str__()`, it will be printed out. This way you can avoid accessing member data in non-member functions. If you want the `__str__()` method to work irrespective of the dimension of the end points (2D, 3D or any D!), you may have to inquire the length of the array representing the point and go into a loop.