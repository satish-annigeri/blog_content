title: Object Oriented Programming Concepts (with a C++ Flavour)
date: 2011-11-29
slug: oop-concepts-with-a-cpp-flavor
tags: OOP, C++, Programming

A comparison of the two approaches, procedural and object oriented, to program design, development and maintenance.<!-- PELICAN_END_SUMMARY -->

The title of the book by Niklaus Wirth, Algorithms + Data Structures = Programs aptly captures the essence of computer programming. The two components of programs, algorithms and data structures, are intimately related to one another and each exists to serve the other. While algorithms define actions performed on data, data structures are meant so that actions can be performed on them.

In the traditional approach to program design, the procedural programming approach, procedure (algorithms) has the upper hand over data. In this approach, program design is based on the premise that the program is meant to perform a (large and possibly complex) task and the best way to accomplish this task is to break up this big task into manageable smaller tasks and sequence these tasks to accomplish the big task. Data is merely storage of information on which the tasks are to be performed. Thus the program design concerns itself with deciding the sequence of tasks and how data flows from one task to another. This is usually achieved by writing a function to perform the identified tasks. A complex task could be completed by writing a hierarchy of functions, beginning with the simplest functions and then going on to write more complex functions that in turn use the previously written simpler functions. The programmer ends up with a collection of a hierarchy of inter-related functions. This method of program design adopts concepts such as structured programming and modularity, so that it is possible to write complex programs. It adopts tools such as flow charts and documentation of functions and their inter-relationship in order to make it easy to debug and maintain complex programs developed using the procedural programming approach. Here, procedure is king, which is an indirect way of saying, data is slave to procedure.

Software engineering points out that it becomes difficult to design, develop and maintain programs developed using the procedural programming approach when the program crosses a certain size. Although it is difficult to specify this limit in terms of the number of lines of code, it is well accepted that such a limit exists. This is where the new approach to program design, development and maintenance comes in, the Object Oriented Programming (OOP) approach.

OOP is based on the premise that the natural way that humans use to solve problems is object oriented and not procedural. It is therefore open to question why we should use a procedural approach to problem solving when the natural way we solve problems everyday is object oriented. In this approach, program design is centered around identifying the data to represent the problem we want to solve and then look at the different actions we perform on this data. It is believed that any action that we perform has meaning only with reference to the data on which it acts and without it, the action would have no existence. Thus, actions are treated as an integral part of the data on which they act. This leads to the binding together of data and the actions performed on that data as single entity. This is the class in OOP terminology. The data become the attributes of the class and actions become the methods of the class. And, the two are inseparable. And not just that, the programming language knows they are inseparable and treats them as such. Therefore, you can call a method only with reference to an object of the class and never alone. In this approach, data is king, and consequently, procedure is slave to data.

The program design procedure now requires the programmer to identify the classes required to solve the problem at hand and for each class, the associated methods. Program execution is now a matter of creating the right objects, putting data in the objects and one object communication with another through message passing (in the form of invoking the appropriate methods) amongst the different objects. Program design tools now involve class diagrams, class hierarchy diagrams, state diagrams etc.

In many ways, it is true that it is possible to design, develop and maintain highly complex programs (as compared to the procedural programming approach), but this is achieved at a price. The price to pay is the added complexity of the process of program analysis, design and development. There is also the reduced run-time speed. So, it is not always true that OOP is the best approach to use. If the program is very complex, is to be maintained over a long period of time, by different developers then OOP is certainly the way to go. The additional time spent initially in understanding the problem to be solved and architecting an appropriate solution using the OOP approach will certainly pay back in terms of easier development, better communication amongst the team of developers and ease of maintenance of the code.

It would be appropriate to illustrate all that was said using a simple example that almost everyone would understand. So, let us assume that the problem is to calculate the roots of a quadratic equation

$$a x^2 + b x + c = 0$$

Using the procedural programming approach, this would be the way a solution is devised:

1. To find the roots of the quadratic equation, we must first find the discriminant $d = b2 - 4ac$.

2. If $d$ is positive, roots are real and unequal. They can be written as:
$$x_1 = \frac{-b + \sqrt{d}}{2s}$$
and
$$x_2 = \frac{-b - \sqrt{d}}{2a}$$

3. If $d$ is zero, roots are real and equal.  They can be written as:
$$x_1 = x_2 = \frac{-b}{2a}$$

4. If $d$ is negative, roots are complex conjugate. They can be written as:
$$x_1 = \frac{-b}{2a} + i \frac{\sqrt{d}}{2a}$$
and
$$x_2 = \frac{-b}{2a} - i \frac{\sqrt{d}}{2a}$$

5. We will need the following functions:
    1. `float disc(float a, float b, float c)` to compute the discriminant given the coefficients a, b and c.
    2. `void real_roots(float a, float b, float d, float& x1, float& x2)` to compute the real unequal roots in case $d >= 0$.
    3. `void cmplx_roots(float a, float b, float d, float& real, float& imag)` to compute the real and imaginary parts of the complex conjugate roots.
    4. `int calc_roots(float a, float b, float c, float& x1, float& x2)` to calculate the discriminant and the roots based on the value of the discriminant. The return value of the function is an integer and can be coded such that it is $-1$ if $d < 0$, $0$ if $d = 0$ and $+1$ if $d > 0$. Looking at this value would indicate the nature of the roots.

6. The algorithm for the program would be as follows:
    1. Input data: coefficients $a$, $b$ and $c$. Check that $a$ is not zero.
    2. Calculate the discriminant $d$ using the function `disc()`.
    3. If $d >= 0$, calculate the real roots using the function `real_roots()`, else calculate the real and imaginary parts of the complex conjugate roots using the function `cmplx_roots()`.
    4. Print the results.

Following the object oriented programming approach, program design would follow these steps:

1. The primary object in the program is the quadratic equation. The attributes of this object are the coefficients $a$, $b$ and $c$ of the quadratic equation. These become the attributes of the object. The class to create such an object would be `class quadeqn`.
2. The actions we perform on an object of this class are:
    1. Compute its discriminant. This would need a method `float disc()`.
    2. Compute the real roots. This would need a method `float real_roots(float& x1, float& x2)`.
    3. Compute the complex conjugate roots. This would require a method `float cmplx_roots(float& x1, float& x2)`.
    4. A master function `int calc_roots()` to compute the discriminant, calculate the roots depending on the value of the discriminant, along the lines described above.
    5. Read data and put it into the object. Print the roots
3. Program would follow this flow:
    1. Create an object of type `quadeqn`.
    2. Input data from the user and put it into the object.
    3. Invoke the method `calc_roots()`.
    4. Print the roots.

You will notice that the functions of the procedural approach and methods of the object oriented approach are quite similar. But there are a few differences. The methods of the OO approach have access to the attributes of the object and therefore need not be explicitly passed in as arguments. This is the advantage of binding data and methods together as a single composite package, the object.

Obviously, using OOAD (object oriented analysis and design) to develop a program to find the roots of a quadratic equation is overkill, but you can see its advantages if this is part of a bigger program that uses such a class. If all you wanted to do was to find the roots and be done with it, procedural approach would certainly be the way to go.

Of course, as with most things in life, the discussion above is not the whole picture. OOP and procedural approach use many more concepts than what is discussed. While it is true that OOP is better able to handle complex program architectures, it does not mean that complex programs cannot be written using the procedural approach. All you have to do is look at the existing large numerical libraries to understand this. There are also a number of non-numerical libraries and programs to support this statement. It is also true that merely adopting the OO approach does not automatically guarantee good programs. It is quite possible to write a messy program using the OO approach, as easily as you can using the procedural approach.

In the end, it can be summarised that each approach adopts its own conceptual tools and procedures and each has its strengths and weaknesses. It is best left to the programmer to decide the most appropriate approach to adopt for a given task.

