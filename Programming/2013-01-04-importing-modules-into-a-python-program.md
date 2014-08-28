title: Importing Modules into a Python Program
date: 2013-01-04
slug: importing-module-into-a-python-program
tags: Programming, Python

In Python, a module introduces a new namespace and adds functions, classes and variables into your programs, enabling them to do things which they would not be able to without the capabilities imported from the module. <!-- PELICAN_END_SUMMARY -->

"Modules" in Python are what other programming languages call "libraries". You import a module with the import statement. Modules typically contain valid lines of Python code, which get included into your Python program, at the line where the import statement appears, verbatim. Hence a module can import variables, functions, classes or executable statements.

In addition to importing lines of code, a module also introduces a new namespace into your program, which is the same as the name of the module. A namespace isolates code imported from a module from the code in your own program. Consequently, to call a function named `func` defined in a module named `mod`, the function call is `mod.func()`. For example, to call the function `sqrt()` in the module `math`, first import the `math` module and then call it as `math.sqrt(4)`. The program snippet to this is shown below:

~~~python
import math

x = math.sqrt(4.0)
print x
~~~

The output from the above lines is 2.0. The advantage of creating a separate namespace is that, if you so wish for whatever reason, you can define your own function with the name `sqrt()`, same as the one in the `math` module.

If you find this method of calling functions from a module cumbersome, it is possible to merge the code from the module into the default namespace in which your own program exists. Then you could call the imported function directly without having to refer to its module name. But then you would lose the ability to define your own function having the same name as the one imported from the module. The following lines of code demonstrate how to accomplish this:

~~~python
from math import *
x = sqrt(4)
~~~

The above import statement imports everything from the math module and merges it with your own program. Sometimes, you may wish to import only the function `sqrt()` from the math module instead of importing everything. This is accomplished as follows:

~~~python
from math import sqrt
x = sqrt(4)
~~~

There is another way to import a module. Suppose you wish to import a module into its own namespace but want to assign a shorter alternative name to the module so that you can save on some typing. For example, it is standard practice to import the NumPy module and assign the name `np` to it. From then on, you can refer to the module by the alternate alias that you assigned to it. Here is an example.

~~~python
import numpy as np
x = np.linspace(0, 2*np.pi, 501)
y = np.sin(x)
~~~

You can do the same to a function name instead of to a module, that is, assign an alternative name to a function imported from a module.

~~~python
import numpy.sqrt as npsqrt
x = np.linspace(0, 2*np.pi, 501)
y = npsqrt(x)
~~~

Whatever I described with reference to a function can be extended to a class or a variable imported from a module.

It is possible that a module is organized into submodules, especially if a module is large and contains many functions. For example, Matplotlib and SciPy modules contain a number of submodles. It is then necessary to address functions contained in submodules using the full path to the function. For example

~~~python
import scipy.linalg
print scipy.linalg
print scipy.linalg.solve
~~~

This imports `scipy.linalg` submodule, which can be demonstrated with the two print statements that print out information about the `scipy.linalg` module and the `solve` function in the `scipy.linalg` module.

You must note that importing a module or a submodule creates a new namespace and imports the functions, classes and variables present in the submodule that is imported. However, importing a module does not automatically import its submodules and the contents of the submodules. Each submodule must be imported separately. Therefore the following lines result in an error:

~~~python
import scipy
print scipy.linalg
~~~

It is possible to write your own modules so that you or others who have access to your modules can import them into programs. If you wish to do so, remember that the name of the file (without the ".py" filename extension is automatically the name of the module.

Typically, the Python interpreter searches for modules at predefined directories. To import a module, it must be in one of the pre-defined directories that Python interpreter searches in or in the same directory where the file containing your program resides. If the module file is in a different directory, then you must define an environment variable called `PYTHONPATH` whose value is a string containing the list of directories that the Python interpreter will search for modules. Multiple directory name must be separated by a colon (Linux/Unixes) or a semicolon (Windows). The directory name separator is, in fact, defined by os.pathsep.

If there is a section (or sections) of your module file that you do not wish to be executed when the file is imported as a module but that you wish to execute if the file is executed as a script, put that section of the code within a if `__name__ == '__main__'` conditional block. Here is an example:

~~~python
def myfunc(x):
  statement1
  statement2
  return y

if __name__ == '__main__':
  x = 10
  y = myfinc(x)
  print x, y
~~~

Python interpreter assigns a name to each module it interprets and executes, and the name of a module is available in the built-in variable `__name__`. Thus the statements in such a block are to be executed only if the name of the module from where the file is being executed happens to be `'__main__'`, a string constant. The lines will not be executed if the name of the module from where the file is executed is anything other than `'__main__'`. If the file is imported, the name of the module is the name of the Python file containing the code and lines in this block will not be executed. If on the other hand, the file is being executed by the Python interpreter as a script, the name of the main module is `'__main__'` and consequently, lines in such a block are executed.