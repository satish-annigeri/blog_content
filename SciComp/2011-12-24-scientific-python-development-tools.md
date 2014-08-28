title: Scientific Python Development Tools
date: 2011-12-24
slug: scientific-python-develeopment-tools
tags: Scientific Computing, Python

Identifying the tools needed to develop scientific and engineering applications using Python.<!-- PELICAN_END_SUMMARY -->

Developing scientific and engineering applications in Python requires the following features/tools, some of which are common to all applications and a few specific to scientific/engineering applications. A programming environment with these capabilities is most likely to result in an application that meets the requirements of the end user. Here is a list, in no particular order:

1. Strong support for both procedural and object oriented programming. The flexibility afforded by this hybrid approach frees the programmer from using a strictly laid down framework. Java is an example of a language that enforces a strict OOP approach with no option of choosing a procedural approach. Python doesn't enforce OOP.

2. Strong support for arrays and array operations. Scientific applications invariably involve data represented as vectors or matrices. A language that has native support for fast and efficient array storage, retrieval and operations is a necessary requirement for such applications.

3. Strong support for building GUI applications. Scientific applications necessarily involve interaction of the user with the application. This can be best achieved through a GUI. Availability of a good GUI application framework is essential.

3. Visualization of data. Scientific applications require representation of data in the form of 2D and 3D graphs. Ability to display 3D rendered images of geometry is a requirement in many engineering applications.

5. Generating formatted, print quality documents based on results computed by the application is an important requirement. Availability of a library to render documents in a portable format (such as PDF, PS etc.) is useful. Multi-format document generation through LaTeX are also a good option.

6. Database access is a useful feature in scientific applications. Such applications usually handle large amounts of data, represented in a custom format. Operations such as search, insert, delete are also frequently required. Availability of a library to connect to a database or any external datastore is a useful feature. Datastore could be server based (MySQL, PostgreSQL) or (file based (sqlite). If the library is datastore agnostic as well as able to represent data in the external datastore in software (as classes), the application becomes independent of the datastore as well as easy to program. The former technology goes by the name Database Abstraction Layer (DAL) and the latter by the name Object Relational Mapping (ORM).

7. Availability of a good IDE for development, debugging and testing is essential.
Ability to deploy the application either as a desktop application or as a web application would be an excellent feature. Future applications are more likely to be deployed on the web rather than on the device itself. Web applications enable easier collaboration amongst members of a team.

Based on these requirements, here is a list the available options for Python. First off, consider using one of several Scientific Python distributions that bundle many Python modules frequently required by scientific applications. This will avoid the problem of identifying, downloading and installing individual Python modules. Two such distributions (that I know of) are:

1. Enthought Python Distribution (EPD): EPD Free is open source whereas EPD is not. However, an academic version of EPD is available. EPD is available for Windows, Apple Mac OS X, GNU/Linux and Solaris in both 32-bit and 64-bit. One encouraging thing is the 64-bit version for Windows which is not usually available otherwise (at this point of time Dec 2011). There is support for both wxPython and PyQt, PySide.

2. Python(x,y): Python(x,y) is a scientific Python distribution with a PyQT tilt. It appears to have only 32-bit Windows version and no GNU/Linux versions (although I am not sure). It bundles Spyder, an interactive scientific development environment similar to Matlab(R).

Here are the individual components that are useful:

1. Arrays and array operations: NumPy, SciPy
2. GUI frameworks: wxPython, PyQt, PySide
3. Data visualization:
   1. 2D graphing: matplotlib, Enthought Chaco (in conjunction with Traits and TraitsUI)
   2. 3D visualization: Mayavi (Part of the open source Enthought Tool Suite)
4. Print document generation: ReportLab
5. Database access: SQLAlchemy
6. Integrated Development Environments:
7. Lightweight IDEs: Editra, Vim, IDLE
8. Industry strength IDEs: Eclipse with PyDev
9. Web application frameworks: Flask, CherryPy, Bottle, Django

Phew! The list is long and the learning curve steep, but who promised an easy path? All you need is the inner drive to persevere on the path to programming nirvana.

The above list is based on my limited exposure to and experience working with the Python programming language. I have only just begun on this path. Watch this blog to track my progress. Mean time, you could begin exploring Python and its capabilities with reference to your own applications.

Please add your comments to help improve this page by voicing your views and adding, modifying and/or correcting the information it contains.