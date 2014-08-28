title: Plot Graphs of Trigonometric Functions using Python
date: 2011-12-17
slug: plot-graphs-of-trigonometric-functions-using-python
tags: Programming, Python, NumPy, Matplotlib

Plotting graphs using Python. <!-- PELICAN_END_SUMMARY -->

Pylab, Python with NumPy, SciPy and Matplotlib aims to provide a viable alternative to Matlab. Here is an attempt to show how to plot sine and cosine interactively as well as through a script. I will leave it to you to decide whether it is easier or tougher than using Matlab, Scilab or GNU Octave.

First, the requirements. You must have installed, Python 2 along with the following modules - NumPy, SciPy and Matplotlib. I have a preference for IPython instead of the vanilla Python console. You will have to download and install it separately.

An alternative is Pylab, a bundle of IPython along with the above required libraries. A third possibility is to download Enthought Python Distribution (EPD Free). EPD Free is Pylab along with Enthought Tool Suite and other useful Python modules.

Once you have all required software installed, fire up IPython and type these commands interactively:

~~~python
In [1]:x = linspace(0, 2*pi, 101)
In [2]:y1 = sin(x)
In [3]:y2 = cos(x)
In [4]:plot(x, y1, x, y2)
In [5]:grid()
~~~

If you are not using IPython, you will need to import NumPy and Matplotlib modules. You will know this if you get error messages saying some functions are not available, import the required libraries before typing the above commands. The required lines are:

~~~python
from numpy import *
from matplotlib.pyplot import *
... [same lines as above] ...
show()
~~~

If you are not using IPython, you will also have to call the `show()` function to display the graph. Here is the graph that will be produced:

You could embellish the graph a little with the following commands:

~~~python
plot(x, y1, 'sin(x)')
plot(x, y2, 'cos(x)')
grid()
legend()
ylim(-1.2, 1.2)
xlabel('x')
ylabel('sin(x), cos(x)')
title('Harmonic Functions')
~~~

Here is the resulting graph:

You could position the legend at the bottom left corner with the command
`legend(loc=3)`. Refer the Matplotlib documentation for more details.

Here is a screencast of the above steps on YouTube or watch it right here on the post.

If you want to plot the same graph from a script, assume you are using the vanilla Python console and not IPython. That is, import all required modules and use the `show()` command to finally display the graph. Here is the Python script you will need. Save it as plotsincos.py and run it from the command line using the command prompt>python `plotsincos.py`.

~~~python
from numpy import *
from matplotlib.pyplot import *

plot(x, y1, 'sin(x)')
plot(x, y2, 'cos(x)')
grid()
legend(loc=3)
ylim(-1.2, 1.2)
xlabel('x')
ylabel('sin(x), cos(x)')
title('Harmonic Functions')
show()
~~~

I hope that was easy enough for you to complete. If not, refer to the interactive plotting tutorial on Spoken Tutorial website for the screencast.

{% youtube -9uJdRSkHQA?list=UUGORmgG8jw36m343nFsWFvw %}