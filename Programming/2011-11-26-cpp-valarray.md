title: C++ valarray
date: 2011-11-26
slug: cpp-valarray
tags: OOP, Programming, C++, Numerical Methods

C++ valarray is a class template to represent an array of numerical values. It is versatile and comes with all basic features required for a one-dimensioned array. <!-- PELICAN_END_SUMMARY -->

Arrays in C++ are identical to those in C. Consequently, operators, such as $+, -, *, /$ are not defined for arrays. C++ classes are a user defined data type (UDT) for which the programmer can define operators, thereby making the UDT similar to built-in data types. Therefore a program statement such as `c = a + b` can be written for a class representing a vector (one-dimensioned array) or a matrix (two-dimensioned array) provided the class defines the required method for the operator.

`valarray` is a class template in the C++ standard library to represent one-dimensioned arrays of numerical values. It is meant to represent arrays of non-numeric data types (such as char or bool) for which operators +, -, * would not have a meaning.

A `valarray` is much more than an array. Following are possible with a valarray:

1. You can create a valarray of any numeric type. For example `valarray<int> x(10)` creates `x` as a valarray with 10 integer elements. In the same way, `valarray<float> y(20)` creates `y` as a valarray with 20 float elements.
2. Selected operations on valarray are defined. Thus `c = a + b`, where `a`, `b` and `c` are valarrays of compatible types works. So do other operations such as `-` (subtraction), `*` (element wise multiplication), `=` (assignment), `[]` (subscripting and assignment).
3. No error checking is performed for subscripting or assignment. It is programmer's responsibility to ensure that the array bounds are not crossed while performing any operations. Error checking is sacrificed to achieve speed.

The strength of a valarray is that when used along with other classes such as `slice`, `gslice`, `slice_array`, `gslice_array`, it is possible to impose a two-dimensional or a multi-dimensional view on the one-dimensioned valarray. However, I have not been able to work out how to change the start index of the initial element, other than through use of pointers. But Chapter 22 Numerics from Stroustrup, B., *The C++ Programming Language* has an assignment question precisely for this solution. Does anyone know whether there is a solution manual for this book?

Here are a few selected problems from Exercise 22.9 from this book:

1. Prob. 6 (*2.5) Define and implement a three-dimensional matrix with suitable operations.
2. Prob. 7 (*2.5) Define and implement an n-dimensional matrix with suitable operations.
3. Prob. 9 *3) Implement a Fortran style array Fort_array where indices start from 1 rather than 0.
4. Prob. 10 (*3) Implement Matrix using a valarray member as the representation of the elements (rather than a pointer or a reference to a valarray).

**Reference:**

Stroustrup, B., *The C++ Programming Language*, Special Edition, Addison-Wesley, 2000 (There could be a more recent edition than the one I am referring)
