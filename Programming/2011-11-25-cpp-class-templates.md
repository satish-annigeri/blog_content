title: C++ Class Templates
date: 2011-11-25
slug: cpp-class-templates
tags: OOP, C++, Programming

A class template is a parameterized class definition.
<!-- PELICAN_END_SUMMARY -->

A class template in C++ is a parameterized class. That is, a class definition in terms of a placeholder for the data type that you intend to use when you want to instantiate an object of the class. If you think that is not a clear explanation, then here is an analogy. When you define a function, the input and output parameters are placeholders for the arguments you intend to supply when the function is to be invoked. During function definition, they are merely parameters. Their actual value is defined when you invoke the function. In fact, you can use different arguments each time you invoke the function. When this concept is extended to a class definition, you get a class template. A typical class template looks as follows:

~~~cpp
template class mymatrix<T> {
private:
  // private member data and methods go here

public:
  // public methods and member data if any, go here
};
~~~

Note the `T` within angle brackets `<>`, which is the parameter in this class template definition. The whole class definition is in terms of this data type. Once this class template is available, it is easy to instantiate a class of this type. When you do so, you will have to tell what you want replace `T` with. This is what you would do if you wanted to create a `class mymatrix` of integers, floats and chars:

~~~cpp
int main() {
  mymatrix<int> x;
  mymatrix<float> y;
  mymatrix<char> c;
}
~~~

Of course, you could add two matrices of type float (provided the operation is possible) by defining a method for the operator `+`. But, such an operator would be meaningless for a matrix of chars. It is therefore the responsibility of the programmer to convey to the users of the class how it must be used.

When you instantiate a class based on the class template, an entire class is created for the specified type. This is done at compile time so that the class is available when the program is executed. Only those classes based on the class template will be created that are instantiated in the given program. Thus, in the above example, three classes are created, one each for integers, floats and chars. But not for other data types, for example, doubles. Not because it can't be done, but because it is not required in this specific program.

The power of a class template is that it is everything that a class is, yet at the same time, it is a template for a number of related classes. This saves you development time and debugging time because you now have to test only one class template instead of a set of related classes. When you want to create a set of identical classes which differ only on the data type used in their definition, you can save a lot of effort and time by writing a class template, provided such a template is meaningful for the data types you are likely to use it with.