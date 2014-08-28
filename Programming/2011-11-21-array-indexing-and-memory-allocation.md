title: Array Indexing and Memory Allocation in Programming Languages
date: 2011-11-21
slug: array-indexing-and-memory-allocation
tags: Arrays, Programming, C++, Python, Fortran, Scilab


Demystifying array indexing and memory storage schemes used by programming languages.<!-- PELICAN_END_SUMMARY -->

When it comes to arrays, there are two things to wrap your brain around:

1. Internal storage allocated for the array
2. Indexing the elements of the array so that we can read from or write to those elements.

All programming languages agree on the first: Memory for an array is allocated in a contiguous block. All elements of an array are assumed to be of the same data type. This makes it possible to access any element of the array if we know the location in memory of the initial element. This applies to an array with any dimension, one-dimensioned, two-dimensoned or multi-dimensioned.

Different programming languages differ on the second: Index of the initial element (element for one-dimensioned arrays, row or column for two-dimensioned arrays and so on for multi-dimensioned arrays) is:

1. Zero in C/C++, Python, PHP and cannot be changed (at least for static arrays).
2. One by default in Fortran, but can be changed to any integer value, positive or negative if need be.
3. One by default in Scilab, GNU Octave, Matlab(R) and cannot be changed.

(Note: I am not sure about Pascal, but I remember it is similar to Fortran)

Thus, while the programmer may wish to view the array as one-, two- or multi-dimensioned, memory allocation (addressing) is always one-dimensioned. What I intend to do in this post is to show how elements are mapped from a n-dimensioned array yo a one-dimensioned array in different languages. It will be assumed that the index of the initial element of the array in memory is consistent with the convention used by the respective languages.

Mapping an element of an one-dimensioned array to memory is straight forward because both the array and memory are one-dimensioned. Whatever is the index of the element is also the location of the element in memory as long as you use the initial index consistently.

Indexes of an element of a two-dimensioned array is (i,j) where 'i' is the row index and 'j' is the column index. In Fortran/Scilab/GNU Octave, the initial row is indexed as 1 (although it can be changed to any value in Fortran). In C/C++/Python/PHP the initial row is indexed as 0. Same goes for columns. Thus, an element with index (i,j) is mapped to the element in memory as follows:

1. Fortran/Scilab/GNU Octave: Element (i,j) of the matrix is mapped to the element (j-1)*m+i in storage, counting initial row and column as 1 and initial element in storage as 1. Indexing is column-wise, or left most index varies fastest. In order to use this mapping function, it is necessary that we know the number of rows in each column (because we are going column-wise).
2. C/C++, Python, PHP: Element (i,j) of the matrix is mapped to the element (i*n+j) in storage, counting initial row and column as 0 and initial element in storage as 0. Indexing is row-wise, or right most index varies fastest. In order to use this mapping function, it is necessary to know the number of columns in each row (because we are going row-wise).

Extending the same logic to 3-dimensioned or in general n-dimensioned array requires you to stop thinking in terms of rows and columns because it becomes over-whelming once you cross 3-dimensioned. For example, a 3-dimensioned array could be thought of as a deck of cards, with each card having the same number of rows and columns. A 4-dimensioned array could be thought of as boxes of sets of cards (with each box containing the same number of cards), with each card consisting of same number of rows and columns. Whew! An easier approach is to say that an element in an n-dimensioned array requires n-indexes. These elements are stored contiguous in memory. Elements of the array are mapped to the memory location by one of the following schemes:

1. **Left-most Index Varies Fastest Scheme (Fortran, Scilab, GNU Octave):** Left most index varies fastest. In order to map an element of array to memory, we will need the sizes of all indexes except the right most. The mapping formula for the element (i, j, k) of a 3-dimensioned array of size n1 x n2 x n3 is (i-1)*n2*n3
2. **Right-most Index Varies Fastest  Scheme (C/C++, Python):** Right most index varies fastest. In order to map an element of the array to memory, we will need the sizes of all indexes except the left most.

Here is an example illustrating the above points for a 2-dimensioned array. Consider a 2-dimensioned array of size 3x4 (3 rows and 4 columns). The diagram below shows the programmer's view of the array and the memory storage for the array using the two different schemes described above:


It is possible to write a C/C++ program to show that this is correct by printing out the addresses of the elements of an array. Other programming languages do not permit printing addresses thereby making it difficult to verify this. However, when initializing data in named DATA statements in BLOCKDATA SUBPROGRAMS in Fortran requires the elements to be entered column-wise, hinting at the way the array is stored in memory.

Any corrections and/or improvements to the above discussion are welcome and will be incorporated either directly in the post as corrections or left as comments at the end of the post.