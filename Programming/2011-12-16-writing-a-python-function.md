title: Writing a Python Function
date: 2011-12-16
slug: writing-a-python-function
tags: Python, Programming

Python has the reputation of being easy to learn. So here is a function in Python to calculate the length of a line in 3D space. Well, it looks almost similar to the one written in Scilab.<!-- PELICAN_END_SUMMARY -->

In a previous post, I discussed some aspects of designing functions and followed it up with implementing one in Scilab programming language. Well, functions in any programming language serve the same purpose, that of reusing code and making it possible to build large programs using functions as building blocks. They may vary in the way they are actually implemented, but the primary objective remains the same.

Let me implement a function to calculate the length of a line joining two points in 3D Cartesian space. This is the same example I used when implementing the function in Scilab. What you will realize when we finish implementing the function in Python is the striking similarity between the two programming languages.

As usual, we begin by choosing a name for the function (I am going to call it length), the list of input parameters (each point is an array of size 2 or 3 and there will be two points sent in as input to the function) and output parameter (length of the line joining the two points). Here is the function and the main function to call the function:

~~~python
from numpy import array, sum, sqrt
def length(p1, p2):
    prj = p2 - p1
    return sqrt(sum(prj**2))

if __name__ == '__main__':
    p1 = array([0.0, 0.0])
    p2 = array([3.0, 4.0])
    L = length(p1, p2)
    print 'Length of line =', L
~~~

Here are some points to remember:

1. Our functions uses several functions that are defined in the Python module `numpy`, namely, `array()`, `sum()` and `sqrt()`. The first line imports these functions from the `numpy` module into the current namespace.

2. The function will work irrespective of the size of the arrays p1 and p2. However, p1 and p2 must both have the same size.

3. The function could also be called without first defining the points, as follows:
`L = length(array([0.0, 0.0]), array([3.0, 4.0]))`

If you are new to Python, note the following about Python programs:

1. Indentation is not merely decorative, it is a requirement. Indentation decides the structure of the program.

2. There is no special function with the name `main()` (as is C/C++) that is executed first when program execution begins. However, you could write your own function named `main()` (or anything else, if you so wish) and make it the only executable statement outside the body of function definitions. Any executable statement(s) outside the body of a function definition are executed wherever they occur (and not merely those at the bottom of the program after all function definitions are complete).

The statements following the line `if __name__ == '__main__':` will be executed only when the program script is executed by Python, and will not be executed, for example, when the script is imported into another script. These same lines could be bundled into another user defined function, possibly called `main()` and called at the end of the program.

As with most things, Python functions have many more features than the ones demonstrated in the above example. For example:

1. It could return multiple return values instead of just one.

2. Input parameters could be assigned default values that can be used in case a matching argument is not furnished during function invocation.