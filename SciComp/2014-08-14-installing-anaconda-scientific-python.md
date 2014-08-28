title: Installing Anaconda Scientific Python on Microsoft Windows
date: 2014-08-14
tags: Python
slug: installing-anaconda-scientific-python

Installing and managing Anaconda scientific Python distribution on Microsoft Windows<!-- PELICAN_END_SUMMARY -->

Python along with scientific computing modules NumPy, Matplotlib, SciPy, Pandas, SymPy and the rest is an excellent platform for numerical computation and data visualization. IPython Notebook has changed the way scientific computing is done, taught and shared. But installing and configuring the scientific computing Python stack is even now a non-trivial task. Distributions such as [Anaconda](http://www.continuum.io) and [Canopy](http://www.enthought.com) have addressed this problem, and to a great extent, have succeeded. This post describes installing and confuring Anaconda on Microsoft Windows.

Both Anaconda and Canopy bundle Python along with most of the scientific computing modules in a single installation file. They also include IPython and an IDE. Each also contains a package manager to add modules that are not bundled with the initial installation. The package manager can update or remove installed packages.

While both Python distributions have similar features, this post covers Anaconda as that is the one I use. Anaconda has a few features that I think are better:

1. Has both Python 2 and Python 3 versions.
2. The package manager `conda` can create and manage multiple virtual Python .
3. Create and manage multiple virtual environments, similar to `virtualenv`.
4. Package manager `conda` can be installed from [PyPi](http://pypi.python.org) and can then integrate with the Anaconda Python repository.
5. Install `miniconda`, a minimal Python environment and add only those packages you need.
6. Create conda compatible packages from your code.

###Downloading Anaconda
Anaconda Python can be downloaded from Continuum Analytics website at [http://continuum.io/downloads]. You can choose the install file appropriate for your operating systems. Versions are available for Microsoft Windows, GNU/Linux and Mac OS X. Both 32-bit and 64-bit versions are available.

Once downloaded, installation is straight forward. It is best to choose all default options during installation. Typically, Anaconda is installed on `C:\Anaconda`. This creates the default environment and has no name. Instead of Anaconda, you can download and install `miniconda` and you can then start with a minimal default environment and add only the modules you need.

###Managing the Anaconda Default Environment
You can list, add, update and remove packages with the Anaconda package manager `conda`. You can also search the Anaconda package repository by package name. You can install specific versions of packages instead of the most recent which is installed by default.

`conda` package manager is a command line tool and can be used from the MS-DOS Prompt. If you chose to add Anaconda to the `PATH` environment variable during install, it can be accessed from any directory.

You can display help about `conda` in multiple ways.
~~~bash
C:\>conda help

C:\>conda -h

C:\>conda help create

C:\>conda create -h
~~~

You can view information about the installed Anaconda Python.
~~~bash
C:\>conda info
Current conda install:

             platform : win-64
        conda version : 3.6.0
  conda-build version : 1.3.5
       python version : 2.7.7.final.0
     requests version : 2.3.0
     root environment : C:\Anaconda  (writable)
  default environment : C:\Anaconda
     envs directories : C:\Anaconda\envs
        package cache : C:\Anaconda\pkgs
         channel URLs : http://repo.continuum.io/pkgs/free/win-64/
                        http://repo.continuum.io/pkgs/pro/win-64/
          config file : None
    is foreign system : False
~~~

You can view the list of all installed packages. Packages installed by `pip` package manager are indicated with `<pip>` in the third column.
~~~bash
C:\>conda list
# packages in environment at C:\Anaconda:
#
_license                  1.1                      py27_0
alembic                   0.6.5                     <pip>
anaconda                  2.0.1                np18py27_0
...
xlwt                      0.7.5                    py27_0
yapsy                     1.10.423                  <pip>
zope.interface            4.1.1                     <pip>
~~~

You can search the Anaconda package reporitory for a package you are looking for by choosing a suitable search pattern. If there is a package in the repository matching your pattern, you are shown the complete list of all available versions, with the installed version indicated by an asterisk.
~~~bash
C:\>conda search 
Fetching package metadata: ..
matplotlib                   1.1.1                np16py27_2  defaults        
                             1.2.0                np16py27_0  defaults        
                             1.2.0                np17py33_1  defaults        
                             1.2.0                np17py27_1  defaults        
                             1.2.0                np16py27_1  defaults        
                             1.2.1                np17py33_0  defaults        
                             1.2.1                np17py27_0  defaults        
                             1.2.1                np17py33_1  defaults        
                             1.2.1                np17py27_1  defaults        
                             1.3.0                np17py33_0  defaults        
                             1.3.0                np17py27_0  defaults        
                             1.3.1                np17py33_0  defaults        
                             1.3.1                np17py27_0  defaults        
                             1.3.1                np18py33_1  defaults        
                             1.3.1                np18py27_1  defaults        
                             1.3.1                np17py33_1  defaults        
                             1.3.1                np17py27_1  defaults        
                          .  1.3.1                np18py34_2  defaults        
                             1.3.1                np18py33_2  defaults        
                          *  1.3.1                np18py27_2  defaults        
                             1.3.1                np18py26_2  defaults        
~~~

Installing a package requires you to know the name of the package, which you can find either from `conda search` or from information available from various sources on the Internet or books. Multiple packages can be installed at one go.
~~~bash
C:\>conda install numpy matplotlib scipy
~~~

Installing a version of a package older than the most recent can be done as follows:
~~~bash
C:\>conda install matplotlib=1.2.0
~~~

Updating an installed package is done by specifying the name of the package to be updated. The correct name of the installed package can be determined from the `conda list` command.
~~~bash
C:\>C:\>conda update matplotlib
~~~

Removing an installed package is done by specifying the name of the package to be removed.
~~~bash
C:\>conda remove matplotlib
~~~

### Virtual Environments
Traditinally, virtual Python environments are created and managed with `virtualenv`. A virtual environment is a sandbox with its own installation of Python and additional packages separate from others. This facilitates creation of custom Python installation along with only the required packages for the purpose of development, testing and any other use.

`conda`, in addition to managing packages, can also create and manage virtual environments. Each environment must be assigned a unique name which is used to activate it as well as manage it. Thus, it is possible to have a Python 2 environment alongside a Python 3 environment an duse one of them at an y given time. It is also posisble to specify the version of Python or the version of additionlal packages. When a new environment is created, unless specified otherwise, the version of Python installed for the new environment is the same as the one in the default environment. After creating an environment, packages can be added to it, and `conda` installes the versions appropriate to the version of Python for the specific environment.

Creating a new environment requires you to specify a name for the environment.
~~~bash
C:\>conda create -n flask
~~~

You can specify the packages to be installed into the environment after creating the environment.
~~~bash
C:\>conda create 0n flask python flask
~~~

You can specify the version of Python, if different from the default environment.
~~~bash
C:\>conda create -n py3flask python=3.4 flask
~~~

You can view the information about the newly created environment with the `conda info` command. Almost every command described above for the default environment works for a named virtual environment if you specify the environment by name on which the command is to be applied, but not all commands (for example `conda info -n py3flask` does not work).

As an example, to list all packages intalled in the `py3flask` environment, the command is `conda list -n py3flask`. It is possible to update, remove packages in a specific environment.
~~~bash
C:\>conda update -n py3flask flask
C:\>conda remove -n py3flask flask
~~~

There is no command to delete an existing environment. But deleting the directory where the environment is installed accomplishes the task. The installed directory can be found using the `conda info` command.

To use a specific environment, you have to activate it.
~~~bash
C:\>activate py3flask
~~~

The system prompt changes. the name of the environment appears to the left of the system prompt as a reminder of the environment in use. You have access to all system commands but only the active Python environment is available. To finish working in the environment, use the deactivate command
~~~bash
C:\>deactivate
~~~
You return to the normal system prompt.

###Installing Packages using `pip`
The popular package manager for Python, at least at present, is `pip`. `pip` has the same features that were described for `conda` above because, in my opinion, `conda` is consciously designed to resemble it. Thus, `pip help`, `pip list`, `pip install` all work. But, there are some differences too. Updating an installed package is `pip install -U flask`. Removing an installed package is `pip uninstall flask`. Since `pip` does not create and manage environments, the `-n` switch does not apply. Since Anaconda package repository is a subset of the Python Packahe Index (PyPI), you will have to use `pip` when you wish to install a package that is not in the Anaconda repository. But `conda` handles that gracefully, it even indicates which packages are installed from PyPI when you ask for the list of installed packages with `conda list`. You can thus have a mix of packages from both repositories.

###Other Features of `conda`
In addition to the features described above, `conda` can build packages that can be uploaded to the [Binstar](https://binstar.org/) service available from Continuum Analytics. Both free and paid plans are available. Another feature is the conversion of `conda` packages. There are a few more, but I am yet to use them and so will save it for another post, if at all.

###Anaconda on GNU/Linux
`conda` works almost identically on GNU/Linux as on Microsoft Windows. There are two differences, however. The commands to activate and deactivate are as follows:
~~~bash
$source activate py3flask
$source deactivate
~~~