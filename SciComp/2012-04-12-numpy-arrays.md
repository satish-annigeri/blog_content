title: NumPy Arrays
date: 2012-04-12
slug: numpy-arrays
tags: Python, NumPy, Arrays, Scientific Computing

NumPy ndarray is a versatile n-dim array implementation and quite different compared to Scilab matrices. Let us examine how NumPy and Scilab define and use arrays.<!-- PELICAN_END_SUMMARY -->

In **Scilab**, all arrays are treated as two dimensional arrays. Therefore, size of a scalar in Scilab is reported as 1x1, that is 1 row and 1 column. So, there is no such thing as a vector or a one-dimensioned array. A row vector is a matrix with only one row while a column vector is a matrix with only one column. Of course, Scilab does support arrays with more than 2 dimensions. The size of an object in Scilab is reported by the function `size()` and number of elements is reported by the function `length()`.

~~~scilab
-->a = 10;
-->typeof(a)
ans  =
constant
-->size(a)
ans  =
   1.   1.
-->length(a)
ans  =
   1.
-->b = rand(3, 4);
-->typeof(b)
ans  =
constant
-->size(b)
ans  =
   3.   4.
-->length(b)
ans  =
   12.
-->c = rand(3, 4, 5);
-->typeof(c)
ans  =
hypermat
-->size(c)
ans  =
   3.   4.   5.
-->length(c)
ans  =
   3.
~~~

Observe that the three dimensioned array `c` is of type **hypermat** and not constant (like `a` and `b`).

Unlike Scilab, **NumPy** defines a generalized n-dimensioned (`numpy.ndarray`) array. Thus scalars, vectors, matrices and arrays with higher dimensions are all distinct. A vector has only one dimension, a matrix has two dimensions and it is possible to define arrays with arbitrarily any number of dimensions. The size of an array is reported by the object attribute `shape`, which returns a tuple containing the size of each dimension. Attribute `shape` is specific to `numpy.ndarray` and cannot be applied to non-NumPy objects. Therefore, scalars are distinct from arrays. Vector is an array with the least number of dimensions, namely, one. Matrices are arrays with two dimensions. There can be arrays with higher dimensions.

~~~ python
>>from numpy import *
>>a = array([10])
>>print a.shape, a.size, len(a), type(a)
(1L,) 1 1 <type 'numpy.ndarray'>
>>a = array([1, 2, 3])

>>print a.shape, a.size, len(a), type(a)
(3L,) 3 3 <type 'numpy.ndarray'>

>>b = array([ [1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12] ])

>>print b.shape, b.size, len(b), type(b)
(3L, 4L) 12 3 <type 'numpy.ndarray'>
>>c = random.rand(3, 4, 5)

>>print c.shape, c.size, len(c), type(c)
(3L, 4L, 5L) 60 3 <type 'numpy.ndarray'>
>>print size(c, 0), size(c, 1), size(c, 2)
3  4  5

>>print len(c), len(c[0]), len(c[0, 0])
3  4  5
~~~

So here is what the attribute shape, and functions `size()` and `len()` report:
1. `shape` returns a tuple. The elements of the tuple give the lengths of the corresponding array dimensions
2. `size()` returns the number of elements along a given axis. The axis along which the elements are counted is an optional second argument. If it is not given, by default, size returns the total number of elements
3. `len()` returns the number of items of a sequence or a mapping. Thus, `len(c)` is 3, `len(c[0])` is 4 and `len(c[0, 0])` is 5. Note that `c` is the entire 3-dimensioned ndarray, `c[0]` is the first item of the 3-dimensioned array, which is a 2-dimensioned array and `c[0, 0]` is the first item of `c[0]` and hence a 1-dimensioned array.

One advantage that NumPy `ndarray` has is that it can be reshaped (without changing the data) as long as the total number of elements remains unchanged. Therefore, a matrix of size 3x4 can be reshaped to 6x2 or 4x3 because they all have exactly 12 elements. In fact, it could be reshaped to a vector or to a 3 dimensioned array too.

~~~python
>>a = array([ [1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11,12] ])
>>a.shape
(3L, 4L)
>>reshape(a, (4, 3))
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
>>reshape(a, 12)
array([ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])
>>reshape(a, (6, -1))
array([[ 1],
       [ 2],
       [ 3],
       [ 4],
       ...
       [11],
       [12]])
>>reshape(a, (3, 2, 2))
array([[[ 1,  2],
        [ 3,  4]],

       [[ 5,  6],
        [ 7,  8]],

       [[ 9, 10],
        [11, 12]]])
~~~

This is what we did:
1. Created a 2-dim array of size 3x4
2. Reshaped it to a 1-dim array with 12 elements
3. Then reshaped it to a 2-dim array with 12 rows and 1 column
4. Finally reshaped it to a 3-dim array of size 3x2x2 (3 card with each card having 2 rows and 2 columns)

While reshaping arrays, it is possible to leave size of one of the dimensions unspecified and let Python work out the required size (as long as a size is possible). Thus, specifying the size of one of the dimensions as -1 indicates that the corresponding size must be computed by NumPy.

~~~python
>>reshape(b, (-1, 3))
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
>>reshape(b, (4, -1))
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
~~~

If it is not possible to have the specified shape, Python reports an error.

~~~python
>>reshape(b, (5, -1))
------------------------------------
ValueError
   except AttributeError:
   ...
ValueError: total size of new array must be unchanged
~~~

Python arrays, are by default, row-major arrays (similar to C arrays) wherein the elements are ordered row by row. But the concept of rows and columns breaks down for arrays with 3 or more dimensions. Hence, it is better to say that the elements are arranged in an order where the right most index varies fastest and left most index varies slowest when the elements are arranged in a 1-dim array. In contrast, column major arrays (similar to Fortran arrays) are arranged such that the left most index varies fastest and right most index varies slowest. It is possible to alter this arrangement of elements using the third optional argument to `reshape()`, namely, `order='C'` (row-major arrangement), `order='F'` (column-major arrangement) or `order='A'` (preserve existing arrangement).

Hint: Using IPython, you could learn all of this quickly using online help. To get help on `reshape`, type `reshape?` at the IPython prompt and press Enter key.
