title: A Python Class for Numerical Integration
date: 2012-03-06
slug: python-class-for-numerical-integration
tags: Programming, OOP, Python, Numerical Methods

A Python class implementation of Trapezoidal and Simpson's 1/3 rules. <!-- PELICAN_END_SUMMARY -->

This is a continuation of my previous post where I implemented a function for Trapezoidal rule. This time around, I will implement a class and include Simpson's rule. Along the way, I will point out the key differences between the procedural and object oriented approaches to programming.

Let us use the same polynomial function that I used last time, namely,

$$y(x) = 2x^2 - x - 4 = 0$$

Here is a graph showing the function as well as values of the function at 5 equally spaced points from a=0 to b=5.

Summary of values and results of actual and numerical integration of the function by hand are given below:

~~~
  x       0.000    1.250    2.500     3.750     5.000
  y(x)   -4.000   -2.125    6.000    20.375    41.000
~~~

Actual Integration
$$ \int_0^5 y(x) dx = \left[ \frac{2}{3} x^3 - \frac{1}{2} x^2 - 4x \right]_0^5 = \frac{2}{3}(5^3 - 0) - \frac{1}{2} (5^2 - 0) - 4 (5 - 0) = \frac{305}{6} = 50.8333$$

Numerical Integration with 4 equal intervals using:

1. Trapezoidal Rule:
$$\frac{1.250}{2} \left[ y_0 + 2 (y_1 + y_2 + y_3) + y_4 \right] = 53.4375$$

2. Simpson's 1/3 Rule:
$$\frac{1.250}{3} \left[ y_0 + 4 (y_1 + y_3) + 2 (y_2) + y_4\right] = 50.8333$$

Since Simpson's 1/3 rule fits a parabola passing through 3 consecutive points, it is exact for polynomials of order 2.

Now for the key differences in the way you design a program by the procedural and the object oriented (OO) ways:
Procedural programming looks at program design as a matter of subdividing complex tasks into simpler ones and developing a function for each identified task or sub-task.

OO way considers program design as a matter of identifying objects in the program (actors in a play), identifying their attributes (characteristics of each role in the play) and orchestrating interaction amongst the objects.
Procedural programming (after identifying tasks and sub-tasks) requires the programmer to identify the input and output data for each function as well as data required in the main function and understand how data flows across the different functions and how data is modified by each function. A documentation of the program design using this approach requires a flowchart.

OO programming requires the programmer to identify attributes of each class in the program and the list of actions that need to be performed on it. Attributes become data fields of the class and tasks to be performed on an object become methods of the class. A documentation of the program using this approach requires class diagrams, class hierarchy diagrams and state diagrams. UML could be an ideal way to represent this information.
In the procedural approach, a program moves from one state to the next in a sequence of function calls, with each function modifying one or more pieces of data. When all function calls are complete, you have the results (hopefully!).

In the OO approach, a program begins by first creating objects of the required class, initializing their attributes and orchestrating message passing to objects by invoking their methods which alter the attributes. When this orchestration is complete, you have the results (once again, hopefully!).
In the procedural approach, the relationship that exists between the data and the functions which operate on the data is not known to the programming language (because it has no constructs to represent that relationship) and therefore is the responsibility of the programmer to be aware of this relationship and enforce it where necessary.

In the OO approach, the fact that an object is a bundle of both attributes and methods (which are simply functions that act on the attributes) means that the programming language is aware that the two are related (of course this relationship is initially programmed by the programmer, but once done, it is explicitly known to the language).
So let us design a class for Trapezoidal rule. The questions to ask are:
What are the attributes of the Trapezoidal rule? The answer is
The range over which integration is to be performed, that is, from a to b
Number of equal intervals into which the range is to be divided, that is, n
Either the function to be integrated or the x and y values of the function evaluated at the selected points over the chosen interval
What are the actions to be performed on the objects of the class? The answer is
Calculate the value of the integral using Trapezoidal rule
Being a simple class, it has only a few attributes and just one method. But we need at least one other method, a constructor, so that we can initialize the attributes with data when we create an object of this class. In Python, the constructor has the special name __init__(). It takes at least one parameter, self, the object on which to operate at run time. Additional parameters are the values required to initialize the attributes.

The formula for the Trapezoidal rule is:

$$I = \frac{h}{2} \left[ y_0 + 2 (y_1 + y_2 + \cdots + y_{n-1}) + y_n \right] $$

where $h = \frac{b - a}{n}$ or $h = x_{i+1} - x_i$

So here is the class to implement Trapezoidal rule:

~~~python
import numpy as np

class Trapezoidal(object):
    def __init__(self, a, b, x, y):
        self.a = a
        self.b = b
        self.x = x
        self.y = y

    def integrate(self):
        h = float(x[1] - x[0])
        s = y[0] + y[-1] + 2.0*sum(y[1:-1])
        return h * s / 2.0
~~~

Note the following points:
The above class assumes that the values of the points at which the function is evaluated are stored in the array x, and the values of the function are previously evaluated and stored in y. This needs to be done in the main function, which we will see later.
The sum required to calculate the integral is calculated using Python's indexing techniques. y[-1] is the last element of the array  y. Similarly,  y[1:-1]  is the range of values of y starting from  y[1]  up to (but not including) y[-1] which means up to but not including the last element.
We can use this class by writing the main script (in the same file as the above class, after the completion of the class definition), as follows:

~~~python
if __name__ == '__main__':
    a = 0.0
    b = 5.0
    n = 4
    x = np.linspace(a, b, n+1)
    y = 2.0*x**2 - x - 4.0
    T = Trapezoidal(a, b, x, y)
    print "Integral = %12.4f" % (T.integrate())
~~~

Note the following points:
1. We explicitly created the data points at which the function is to be evaluated. Note that $n$ is the number of **equal intervals** into which the range from $a$ to $b$ is divided as well as the index of the last element, because Python uses zero as the index of the start element.

2. Function `linspace(firstvalue, lastvalue, numpoints)` takes as arguments, the first value, last value and the number of equally spaced points, both the first and the last values included.

3. We created the object `T` and initialized it with the values $a=0, b=5, x \text{ and }  y$. In this case, it is not necessary to specify the number of intervals because this can be found from the number of elements in $x$ or $y$. The number of points in $x$ and $y$ is one more than the number of intervals.

4. The Trapezoidal class assumes that the values in $x$ and $y$ are at equal intervals. It does not explicitly test this, which it could easily do by testing the values in  $x$. In fact, if this is to be taken on trust, we could simply send in the number of equal intervals $n$ and $y$ values since $x$ values are not required to evaluate the integral. The interval width $h$ could then be calculated from $a$, $b$ and $n$.

Running this program should print out the following output:

~~~
Integral =      53.4375
~~~

Let us now implement Simpson's 1/3 rule along similar lines. In fact, the difference is very minor and is related to the formula for the sum.  The formula is:

$$I = \frac{h}{3} \left[ y_0 + 4 (y_1 + y_3 +...+ y_{n-1}) + 2 (y_2 + y_4 + \cdots + y_{n-2}) \right]$$

Let us add the following code below the Trapezoidal class and above the main script.

~~~python
class Simpson(object):
    def __init__(self, a, b, x, y):
        self.a = a
        self.b = b
        self.x = x
        self.y = y

    def integrate(self):
        h = float(x[1] - x[0])
        n = len(x) - 1
        if n % 2 == 1:
            n -= 1
        s = y[0] + y[n] + 4.0 * sum(y[1:-1:2]) + 2.0 * sum(y[2:-2:2])
        return h * s / 3.0
~~~

We will make a small change in the main script, as follows:

~~~python
if __name__ == '__main__':
    a = 0.0
    b = 5.0
    n = 4
    x = np.linspace(a, b, n+1)
    y = 2.0*x**2 - x - 4.0
    T = Trapezoidal(a, b, x, y)
    S = Simpson(a, b, x, y)
    print "Trapezoidal = %12.4f" % (T.integrate())
    print "  Simpson's = %12.4f" % (S.integrate())
~~~

This time, the output should be as follows:

~~~
Trapezoidal =      53.4375
  Simpson's =      50.8333
~~~

Here is some food for thought. When the two classes are so similar, can we have a class hierarchy? Can we define an abstract class for numerical integration and make the Trapezoidal and Simspon's rules its child classes? Do we gain from this exercise or is this a waste of effort? Is it possible to create a new child class to implement numerical equation by Gauss Legendre method? Would it make sense to have dissimilar approaches to numerical integration as children of one abstract class?

It doesn't matter what the final answer is. The very exercise of doing this thinking can teach you a great deal about programming. Well, try your hand at the above two classes before attempting the class hierarchy. Good luck.
