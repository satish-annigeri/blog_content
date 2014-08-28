title: Python Class for Quadratic Equations
date: 2012-02-07
slug: python-class-for-quadratic-equation
tags: Programming, OOP, Python, Numerical Methods

This posts implements a Python class to represent a quadratic equation, evaluate the equation, find its roots and a few special methods. <!-- PELICAN_END_SUMMARY -->

In continuation of the previous post where I implemented a Python class to represent a Line, this time I will dwell a little on its design and implement a few special functions.

A quadratic equation is of the form $f(x) = ax^2 + bx + c = 0$ and the things we normally do with such an equation are:

1. Evaluate the equation for a given value(s) of x
2. Find the roots of the equation, that is, determine the values of x such that f(x) = 0
3. Print out the equation

Obviously, to represent such an equation, we need to store the values of its attributes, namely, the coefficients a,  b and c. I will implement the following methods:

1. Find the roots of the quadratic equation. In this implementation, only real roots will be computed. Solving for complex roots will be left to you to implement.
2. Evaluate the equation for a given value of  x
3. Print a string representing the equation  f(x)

We will use NumPy because then we can then use array implementation of mathematical functions such as `sqrt()` instead of scalar implementation. Here is the class:

~~~python
import numpy as np

class Quad(object):
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c
    def __call__(self, x):
        return self.a * x**2 + self.b * x + self.c
    def roots(self):
        def disc(self):
            return self.b**2 - 4.0 * self.a * self.c
        d = disc(self)
        if d >= 0:
            x1 = (-self.b - np.sqrt(d)) / (2.0 * self.a)
            x2 = (-self.b + np.sqrt(d)) / (2.0 * self.a)
        else:
            x1 = 0.0 # change this to find complex roots
            x2 = 0.0 # change this to find complex roots
        return x1, x2
    def __str__(self):
        s = "f(x) = "
        if self.a:
            s += "%f x**2" % self.a
        if self.b:
            if self.b > 0:
                s += " + "
            else:
                s += " - "
            s += "%f x" % abs(self.b)
        if self.c:
            if self.c > 0:
                s += " + "
            else:
                s += " - "
            s += "%f" % abs(self.c)
        return s

def main():
    eq1 = Quad(1.25, 2.0, -1.0)  # calls __init__(3.0, 2.0, -2.0)
    print eq1                    # calls __str__()
    print "f(%f) = %f" % (1.5, eq1(1.5)) # calls __call__(1.5)
    x1, x2 = eq1.roots()
    print "Roots: %f, %f" % (x1, x2)
    return 0

if __name__ == '__main__':
    main()
~~~

Running this program (assuming it is saved in a file named quad.py and python directory is defined on your PATH environment variable) results in the following output:

~~~
prompt>python quad.py
f(x) = 1.250000 x**2 + 2.000000 x - 1.000000
f(1.500000) = 4.812500
Roots: -2.000000, 0.400000
~~~

Some points to note:
Methods `__init__()`, `__call__()` and `__str__()` cannot be called explicitly. They are implicitly called when required. `__init__()` is called to initialize an object when it is created, `__call__()` is called whenever we invoke an object as if it were a function and `__str__()` is called whenever we intend to print an object.

Function `disc()` is embedded within method `roots()` and is accessible only from inside `roots()`.
Method `__str__()` appears a little complicated because I am trying to print the signs of the coefficients correctly and not print it at all if it happens to be zero

Because we used NumPy, we can evaluate `f(x)` for an array `x` containing many values instead of just 1. Add the following line at the top of the program below the line where we import the NumPy module:

~~~python
from matplotlib import pyplot
~~~

Add the following lines at the end of the function `main()` just before the statement `return 0`.

~~~python
....
    x = np.linspace(0.5*x1, 1.5*x1, 11)
    y = eq1(x)
    pyplot.plot(x, y)
    pyplot.grid()
    pyplot.show()
    return 0
~~~

Then run the program. You can see a graph of the function, and you will notice that it is zero at $x = -2.0$.

