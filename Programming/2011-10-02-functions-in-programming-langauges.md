Title: Functions in Programming Languages
Date: 2011-10-02

Functions are modular blocks of code that help you build complex programs.
<!-- PELICAN_END_SUMMARY -->

### Sources of Functions

There are several sources for functions:

1. **Functions that are part of the standard library of the programming language:** For example the C standard library has a number of functions for a variety of uses, such as, scanf() to read input from the standard input device, sqrt() to calculate the square root of a number, toupper() to convert lower case characters in a string to upper case. This is true of all programming languages. The programmer needs to study the list of standard library functions for each language.
2. **Functions developed by the programmer for his/her own use:** A programmer can develop her own functions in case the standard library does not have one that is appropriate. It is common to develop one's own set of functions for a given application.
3. **Functions developed by others for application to specific specialized areas of application:** There are a number of free and open source as well as closed source libraries of applications for specialized areas of application such as mathematics (for example, LAPACK for linear algebra, Blitz++ for object oriented numerics and matrix computations), High performance graphics (OpenGL), Computer vision (OpenCV) and a host of others. Such libraries are developed by experts and may be too difficult for individual programmers to develop on their own.

### Function as a Black Box

A programmer who uses a function developed by others may or may not know how the function performs its intended task. This is the blackbox analogy, wherein the user of the function only knows how to use the function while its inner working details are either unknown to the user or of no concern. This is the basic concept that enables one to write complex software, otherwise each programmer would have to develop her own functions for each task.

### What You Should Know About a Function
A programmer must know the following information about the function in order to use it:

1. **Name of the function:** Name of the function is the handlw by which it can be invoked.
2. **Input arguments:** The input data that the programmer must pass on to the function.
3. **Output arguments:** The data that the function returns that the programmer must store for subsequent use.

Having a name for the function that reflect its purpose has multiple benefits:

1. The programmer will find it easy to associate the function with its purpose.
2. While reverse engineering a program, it helps other programmers quickly understand the purpose of the function.

A function exchanges data with its parent function. Parent function invokes the function, pumps in data from its scope into the function and waits for the function to finish its job. When the function completes its job, control returns to the parent function, and the function call is replaced by the value returned by the function.