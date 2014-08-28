title: Python function for Trapezoidal Rule
date: 2012-02-14
slug: python-function-for-trapezoidal-rule
tags: Programming, Python, Numerical Methods

Implementing a function for numerical integration using trapezoidal rule. <!-- PELICAN_END_SUMMARY -->

Here is the input I am assuming will be available:
A function of 'x' which we want to integrate. For illustration, let f(x) = 2x2 - x - 4. That is, the coefficients 2, -1 and -4.
The interval over which the function f(x) is to be integrated. In this illustration, say, from a=0 to b=5
The number of equal intervals into which the interval from a to b is to be divided. For this example, let us take n = 4
Then this is the hand calculation so that we can test our function when it is complete.

~~~
       x         y
   0.000    -4.000
   1.250    -2.125
   2.500     6.000
   3.750    20.375
   5.000    41.000
~~~

Using the trapezoidal rule, the value of the integral of $f(x)$ from $a=0$ to $b=5$ is given as:
$$ \int_0^5 f(x) = \frac{b - a}{n} \left[ y_0 + 2 (y_1 + y_2 + \cdots + y_{n-1}) + y_{n} \right]$$
where $h = \frac{(b - a)}{n}$ is the constant interval width and $n$ is the number of equal intervals.

Doing this calculation by hand, we get $I = 53.4375$. For the given function, finding the integral by hand is straight forward and we can calculate the value of the integral by hand, which turns out to be $50.8333$. Thus trapezoidal rule results in a value with an error of $5.12\%$ compared to the correct value.

Let us now implement a function in Python to do the same calculations.

~~~python
import numpy as np

def f(x):
    return 2.0*x**2 - x - 4.0

def trapezoidal(f, a, b, n, debug=False):
    x = np.linspace(a, b, n+1)
    y = f(x)

    if debug:     # printed only when debug == True
        for i in range(n+1):
            print "%5d %10.4f %10.4f" % (i, x[i], y[i])
    s = y[0] + 2.0 * sum(y[1:n]) + y[n]
    h = float(b - a) / n
    return s * h / 2.0

def main():     # Main function

    a = 0.0     # Setup input values
    b = 5.0
    n = 4
    s = trapezoidal(f, a, b, n, True) # call trapezoidal function
    print s                           # print result

if __name__ == '__main__':
    main()
~~~

Note the following:

1. The first function `f(x)` is the function to be integrated. This will need to be replaced if you wish to integrate a different function rather than the one used in this illustration.

2. Second function `trapezoidal(f, a, b, n, debug=False)` is our user defined function to perform integration by trapezoidal rule. It takes the function to be integrated as its first parameter. The limits of integration are the second and third parameters. The fourth parameter is the number of equal intervals into which the interval from a to b will be divided. The last parameter, which is set to False by default lets you tell the function whether you want it to print the calculated values of x and y.

3. Function `main()` sets up the input values, calls the function to calculate the integral and prints the result.

4. We ensure that the function `main()` is called only when this script is executed as the main program. It will not be executed if the script is imported as a module.

Running the script prints the result as 53.4375. Running the script by changing the value of `n` shows that the result improves if we divide into larger number of intervals. Here is the modified function `main()` to do this:

~~~python
def main():

    a = 0.0
    b = 5.0
    s = trapezoidal(f, a, b, 4)
    print "%5d %12.4f" % (4, s)

    s = trapezoidal(f, a, b, 10)
    
print "%5d %12.4f" % (10, s)

    s = trapezoidal(f, a, b, 20)
    
print "%5d %12.4f" % (20, s)
~~~

This will produce the output:

~~~
    4     53.4375

   10     51.2500

   20     50.9375
~~~

Here are somethings you can try:

1. Write a class to implement trapezoidal rule. What are the merits and demerits of writing classes instead of functions?

2. Write a function to evaluate the integral using Simpson's 1/3 rule and compare the results with the results of trapezoidal rule.

3. Write a function to evaluate the integral by the Simpson's 1/3 rule when the number of intervals is odd, by using Simpson's 1/3 rule up to last but one interval and trapezoidal rule for the last interval.
Write a function to evaluate the integral using Gauss Legndre quadrature and compare the results with those of trapezoidal rule ans Simpson's 1/3 rule

