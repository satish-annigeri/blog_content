Title: Object Oriented Numerics
Date: 2011-11-18
Tags: C++, OOP, Programming
---

Object oriented programming and scientific and numerical computing.<!-- PELICAN_END_SUMMARY -->

Some of my previous posts have dealt with arrays in C/C++, and some of the topics that have been discussed are:

1. Static arrays and dynamic arrays, both one- and two-dimensioned.
2. Dynamic arrays with user specified start index.

But some other issues remain. For example:
1. Attributes of the array, such as, the number of rows and columns must be stored separate from the array itself. That is, these attributes are not an integral part of the array.
2. Operations on arrays are not defined. Thus c = a + b, works if a, b and c are integer or real numbers but does not work if a, b and c are arrays.
3. The first issue could be addressed if we use the abstract data type struct. But this advantage is realizable only at the cost of added complexity (as is the case with most things in life!). The programmer now needs to have mastery over user defined data types (UDTs) and its associated semantics. Here is one possible UDT to represent a matrix:

~~~cpp
struct matrix {
  size_t nr, nc; /* Number of rows and columns */
  int r1, c1;    /* Start index of rows and columns */
  float **p;     /* Pointer for dynamic memory allocation */
}
~~~

But the second issue still remains. Since C does not permit a programmer to define operators for UDTs, we need to define suitable functions to perform operations on this UDT. For example, to add two given matrices `a` and `b`, and return the sum `c`, we can write a function `float** mat_add(float** a, float** b)`. This function would perform the necessary checks to see if it is possible to add the two given matrices and return the sum of the matrices if this operation is permissible or an error otherwise. There are a number of operations we would need, including, creating a new matrix, deleting an existing matrix, assigning values to a matrix, addition, subtraction and multiplication, transpose, inversion, determinant and the list could go on.

Here are some, as yet unresolved, issues:

1. We need to develop a library of functions exclusively for the purpose of performing operations on our user defined data type. But as far as the programming language is concerned, they are in no way related. In fact, the programmer is the one who knows the intimate relationship between the user defined data type and the library of functions to operate on this data type.
2. The UDT shown above is only for a matrix of float elements. If we wanted a matrix of any other data type, we would have to define a number of structs, one for each of the data types. This also applies to the functions. We need a separate library of functions for each data type.

Object oriented programming (OOP) could resolve these issues:

1. OOP lets the programmer define a class (similar to struct), but comes with a number of features (such as data hiding, member functions, constructors and destructors). Functions that are written to work exclusively with a specific class are made member function of the class. Thus, the relationship between the class and its methods are known to the compiler and can therefore raise triggers.
2. OOP in C++ allows the programmer to define a class template. Using this feature, it is  possible to define the matrix class in terms of an assumed data type and specify this data type at the time of instantiating an object. Thus, a class template can create as many classes as required in a specific program at compile time so that objects of the required type can be created at run time. Only that many classes are created as are required in the given program. All classes so created are identical except for the difference in the data type.
3. Operators can be created for the class template, but operation must be identical to all classes. That is, if you define the addition operator for a matrix of floats, the operation is identical for a matrix of int and double, but has no meaning for a matrix of `char`.

A post in the near future will focus on the implementation of such a class template. Doing so right now may be more than what one could digest in one go. Moreover, giving food for thought and letting one try their own ideas based on this concept could be a motivating factor for many. Until the next post, bye!

**References**

1. http://www.oonumerics.org

2. Stroustrup, B., *The C++ Programming Language*, 3ed., Addison Wesley, ISBN 0-201-88954-4 (Chapter 22. Numerics)