title: IPython Notebook
date: 2012-03-14
slug: ipython-notebook
tags: IPython, Python, Notebook, Scientific Computing

Interactive Python in your browser.<!-- PELICAN_END_SUMMARY -->

IPython is a souped up Python shell with features such as inline help, tab completion, enhanced support for NumPy, SciPy and Matplotlib and a host of magic functions (IPython commands that begin with %).

But with version 0.12, IPython goes one step further. It now introduces a web based notebook. This means that you can access IPython running as a web server, either on your local machine or on a server on the network, and access the same interactive IPython shell through your browser.

An IPython Notebook typically has cells, which can b eeither **code cells** or **Markdown cells**. Code cells can contain Python code. Code cells have syntax highlighting. When you want to execute the code you have typed, click the **Run** button at the top. Output is inserted inline. If your code produces a graphical output using Matplotlib, the graph is shown in a separate window that pops up. You can show graphical input inline with the magic command `%matplotlib inline` at the beginning of your code.

Markdown cells can contain text in Markdown format and can include rich media. You can also embed $\LaTeX$ equations. IPython uses MathJax to display math, which is downloaded from the MathJac CDN when needed. It is possible to install and use a local copy MathJax if you want to display math when not connected to the Internet.

An IPython Notebook is a simple text file in JSON format. SO you can share a notebook with a friend and the friend can simply run the Notebook to see the code, your documentation and comments as well as output. Being a simple text file, it is easy to integrate with a version control system. The possibilities, especially for teaching and larning appear endless. You could run your own IPython notebook server and access it from anywhere through the network, to code, develop, test and/or run Python code.

Here are the dependencies:
1. IPython version 0.12 or higher. If you have an older version, do `easy_install -U ipython`. If you don't have `easy_install`, you can install it using `setuptools` either from your operating system package manager (GNU/Linux) or download and install (Microsoft Windows) from PyPI and install with the command `python setup.py`
2. Tornado version 2.2. Tornado is a Python web server. If you don't have Tornado installed, install it with the command easy_install tornado

You are now ready to run IPython notebook server. You can open a console (GNU/Linux) or an MS-DOS prompt (Microsoft Windows) and run the command

~~~
prompt>ipython notebook
~~~

This will run the Tornado web server and automatically open your browser showing you a web GUI. You can see the IPython prompt and start typing Python code. When done, press Shift+Enter to execute the code and see the results. To shutdown the IPython notebook server, go back to the console/MS-DOS Prompt and press Ctrl+C.

If you work with NumPy, SciPy and Matplotlib and don't want to bother with importing these modules each time. Simply start IPython notebook server as follows:

~~~
prompt>ipython notebook --pylab
~~~

To see inline graphs within the browser (instead of them popping up), use the following command to start IPython notebook server

~~~
prompt>ipython notebook --pylab inline
~~~

You can create a new notebook, save it for use in subsequent sessions, download notebooks to your local storage and upload notebooks from your computer to the notebook server. Here is a screencast (no audio on this one, sorry) to demonstrate basic features of IPython notebook server on Microsoft WIndows. I also tried it on Ubuntu 11.10 and it worked without a hitch.

### Update
IPython and IPython Notebook have undergone rapid development over the past year. IPython Notebook has become the de facto standard for presentations at most IPython conferences. IPython now has `nbconvert` built-in into itself and is no longer a separate command. IPython is now language agnostic and can run kernels of other dynamic interactive languages such as Julia, R and a few others. A new project has been hived off from IPython which is programming language agnostic, and is called [Jupyter](http://jupyter.org/). Integration of IPython Notebooks into Google Docs is already complete and is expected to be universally available shortly. Kudos to Fernando Perez and the IPython team for giving a software tool that is a game changer for education and open science.

Here are some changes as of IPython 2.1.0 that you must note:

1. To display graphics inline, the option `inline` is no longer available. Instead, use the magic statement `%matplotlib inline` at the very start of your notebook.
2. To convert your Notebook to several supported formats, use one of the following commands

~~~
ipython nbconvert --to html mynotebook.ipynb
ipython nbconvert mynotebook.ipynb --to latex
ipython nbconvert mynotebook.ipynb --to latex --post PDF
ipython nbconvert mynotebook.ipynb --to slides --post serve
~~~