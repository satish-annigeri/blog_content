title: Installing a Python 3 Scientific Computing Environment
date: 2014-08-05
slug: installing-python3-scientific-computing-environment
tags: Python, Scientific Computing

Installing scientific Python software and a review of some popular scientific Python distributions.<!-- PELICAN_END_SUMMARY -->

Python is a versatile and complete scientific computing environment. With NumPy, SciPy and Matplotlib modules, it gets most of the capabilities that one finds in a barebones Matlab environment. After this, you can choose the modules appropriate to your applications. For example, Pandas adds data structures and analysis tools for data analysis. SymPy brings symbolic computing to Python. Then there are the development environments that aid exploratory computing - IPython, Spyder, IEP to name a few. And the game changer, **IPython Notebook** - a web notebook that combines easy documentation using Markdown and $\LaTeX$ with live code, output and graphs that can be easily shared or exported to a number of formats. You couldn't ask for more.

Setting up a simple scientific computing environment in Python is also a straight forward matter. Download Python, `setuptools`, `easy_install` and `pip`. Then use `pip` to download and install NumPy, SciPy, Matplotlib, IPython, IPython-notebook, Pandas, SymPy and any other module you wish to use. You can choose either Python 2 or Python 3. However, choosing Python 2 is the preferred choice at present, especially if some modules you wish to use may not yet be ported to Python 3 as yet.

Some modules such as Cython may require Python development libraries be installed and `gcc` compiler be available. While this may not pose a problem for GNU/Linux or Mac OS X users, it can be a pain for Windows users. Fortunately, pre-compiled 32-bit and 64-bit binary versions for Windows, for both Python 2 and Python 3, are available at [Christoph Gohlke's Python Windows binaries](http://www.lfd.uci.edu/~gohlke/pythonlibs/). However, if you end up with a situation where things do not work, it is best to try one of the ready to install scientific Python distributions, described below.

With Python gaining significant ground in scientific computing and data analysis, several scientific Python distributions are now available. Notable among them are:

1. [Anaconda by Continuum Analytics](http://store.continuum.io/cshop/anaconda)
2. [Enthought Canopy by Enthought](https://www.enthought.com/products/canopy/)

As of this writing, Anaconda has distributions with Python 2 and Python 3 in 32-bit and 64-bit for GNU/Linux, Windows and Mac OS X. Enthought has a Python 2 based distribution in 32-bit and 64-bit for GNU/Linux, Windows and Mac OS X. Both have their own package manager, similar to `pip`. Anaconda package manager `conda`, in addition to managing packages, can also create virtual Python environments similar to `virtualenv`.