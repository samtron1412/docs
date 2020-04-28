[TOC]

# Overview

## Introduction

- **General-purpose, high level programming language**
- **Multi-paradigm:** object-oriented, imperative, functional,
  procedural, reflective
- **Typing:** duck, dunamic, strong

## Resources

- The Hitchhiker's Guide to Python:
    + http://docs.python-guide.org/en/latest/
- Python project workflows
    + part 1: https://gabhijit.github.io/python-project-workflows-1.html
    + part 2: https://gabhijit.github.io/python-project-workflows-2.html
    + part 3: https://gabhijit.github.io/python-project-workflows-3.html
- Open sourcing a python project the right way
    + https://jeffknupp.com/blog/2013/08/16/open-sourcing-a-python-project-the-right-way/
- Google Python course
    + https://developers.google.com/edu/python/

## Help

- Showing built-in methods for an built-in datatype
    + `dir('abc')`: showing built-in methods for a string
- Learn about the built-in function using `help()`
    + `help('ab'.find)`: showing the help for the find method

## History

first release: 1991

## Typing

duck

# Interpreter

- Access the history commands
    + `Ctrl+p` (previous), `Ctrl+n` (next)
- Exit a session
    + `Ctrl+d`
- Doctest
    + `python3 -m doctest <python_file>`
    + doctests are surrounded by `"""`
- Run the script and then open an interactive session
    + `python3 -i <script_file>`

# Conda

- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html
- conda
    + anaconda: a full distribution with a lot of binaries and libraries
    + miniconda: an empty conda environment, containing only Conda, its
    dependencies and python.

## Glossary

- `~/.condarc`: configure conda
    + run `conda config` to create one in the home directory
- Channels: the location of repositories where conda looks for packages

## General commands

- `conda <command> --help`
- `conda clean`: remove unused packages and cache
- `conda config`: modified values in .condarc
    + https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html
- `conda create`: create an environment
- `conda info`: show conda's information
- `conda list`
- `conda install`
- `conda package`
- `conda search`
- `conda remove`
- `conda update`

## Tasks

- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html

### Managing environments

- Create a new environment: `conda create --name myenv`
- Specific python: `conda create -n myenv python=3.4`
- Specific package: `conda create -n myenv scipy`
- Specific version of a package: `conda create -n myenv scipy=0.15.0`
- Specific python and multiple packages
    + `conda create -n myenv python=3.4 scipy=0.15.0 astroid babel`
- No default packages: `conda create --no-default-packages -n myenv python`
- Building an identical environment using spec-file
    + `conda list --explicit > spec-file.txt`
    + `conda create --name myenv --file spec-file.txt`
    + Export the active environment: `conda env export > environment.yml`
- Create an environment from a .yml file
    + `conda env create -f environment.yml`

```yml
name: stats2
channels:
  - javascript
dependencies:
  - python=3.4   # or 2.7
  - bokeh=0.9.2
  - numpy=1.9.*
  - nodejs=0.10.*
  - flask
  - pip:
    - Flask-Testing
```

- Specific location for the environment:
    + `conda create --prefix /path/to/myenv jupyterlab=0.35 matplotlib=3.1 numpy=1.16`
    + Activate by name: `conda activate /path/to/myenv`
- Update an environment by modifying .yml file and run:
    + `$ conda env update --prefix ./env --file environment.yml  --prune`
- Cloning an environment: `conda create --name myclone --clone myenv`
- List all environments: `conda list --envs`
    + `conda env list`
- `conda init`: add some code to shellrc (.zshrc, etc.) to modify PATH
  when run conda activate
- Remove an environment: `conda env remove --name myenv`


## Managing packages

- Activate an environment before installing a package
- Search a package: `conda search scipy`
- Install a package: `conda install scipy`
- Specific version: `conda install scipy=0.15.0`
- Update a package: `conda update scipy`
- View list of packages: `conda list`

## Managing python

- List all python versions: `conda search python`
    + `conda search --full-name python`
- Update python: `conda update python`

# Virtual Environment

## Introduction

- venv: official way for python >= 3.4
    + https://docs.python.org/3/library/venv.html
- virtualenv: 3rd-party way for older version
    + https://virtualenv.pypa.io/en/stable/
- https://realpython.com/python-virtual-environments-a-primer/

## Creation

```
python -m venv <DIR>
virtualenv <DIR>
```

## Activation

```
$ source <DIR>/bin/activate
```

## Usage

### Common

- Once inside the virtual environment, modules can be installed with pip
  and scripts can be run as normal.
- To exit the virtual environment, run the function provided by
  `bin/activate`
    + `$ deactivate`

### Mac OS

- Restricting Pip to virtual environments

`vim ~/Library/Application\ Support/pip/pip.conf`

```
[install]
require-virtualenv = true

[uninstall]
require-virtualenv = true
```

- Install or upgrade global packages:

```~/.bashrc
gpip(){
   PIP_REQUIRE_VIRTUALENV="0" pip3 "$@"
}

// alternative solution
env PIP_REQUIRE_VIRTUALENV="0" pip3 install --upgrade foobar
```

## Sharing the virtual environment

https://help.pythonanywhere.com/pages/RebuildingVirtualenvs/

- Backing up : `pip freeze > requirements.txt`
- Rebuild:
    + Using the appropriate Python version: `virtualenv --python=/usr/bin/pythonX.Y /home/myusername/path/to/virtualenv`
    + Reinstall packages: `pip install -r requirements.txt`

# Package Manager

## Introduction

- pip
- setuptools (easy_install)

## DON'T USE PIP SYSTEM-WIDE, JUST USE IT FOR VIRTUALENV AND SIMILAR TOOLS - [pip](https://pypi.python.org/pypi/pip)

- Install pip
	+ Use package manager of Linux distribution
		* Arch Linux
			- python3: `sudo pacman -S python-pip`
			- python2: `sudo pacman -S python2-pip`
	+ Use [get-pip.py](https://bootstrap.pypa.io/get-pip.py) script
		* `python get-pip.py`
- Use pip with multiple python versions: `pip<version> <command> ...`
	+ `pip install <sth>`
	+ `pip2 install <sth>`
	+ `pip2.5 install <sth>`
- Upgrade pip
	+ Linux: `pip install -U pip`
	+ Windows: `python -m pip install -U pip`
- Show list packages: `pip list`
- Show list packages use for requirementstxt to install in other system: `pip freeze`
- Show outdated packages: `pip list --outdated`
- Searching for packages: `pip search "query"`
- Install new package: `pip install <package name>`
- Uninstall package: `pip uninstall <package naem>`
- Update package: `pip install <package name> -U` or `pip install <package name> --upgrade`
- Update all packages: `pip install --outdated | awk '{print $1}' | xargs -n1 sudo pip install -U`

## Configuration


## Scientific Packages

- https://packaging.python.org/guides/installing-scientific-packages/

# Version Manager

## Introduction

- [pyenv](https://github.com/yyuu/pyenv)
- [pythonz](https://github.com/saghul/pythonz)

**Windows**
- Can use trick, copy file .exe and change name

## pyenv

### Installation

#### [pyenv-installer](https://github.com/yyuu/pyenv-installer)

`curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash`

**Update**: `pyenv update`

**Uninstall**: pyenv is installed within `$PYENV_ROOT` (default: `~/.pyenv`). To uninstall, just remove it: `rm -fr ~/.pyenv` and remove these three lines from `.bashrc` or from `your shell rc file`:

	export PATH="/root/.pyenv/bin:$PATH"
	eval "$(pyenv init -)"
	eval "$(pyenv virtualenv-init -)"

#### [Manually install - Basic GitHub Checkout](https://github.com/yyuu/pyenv#basic-github-checkout)

### User guide


# Packages

## jupyter

### Introduction

- `jupyter notebook`: a web-based interactive computational environment
  for multiple programming languages such as Python, etc.
- `jupyterlab`: next-generation of jupyter notebook

### Installation

- `conda install jupyter` or `pip install jupyter`
- `conda install -c conda-forge jupyterlab` or `pip install jupyterlab`

### Running

- Activate the conda environment if necessary
- `jupyter notebook`
- `jupyter lab`

### Securing a notebook server

- https://jupyter-notebook.readthedocs.io/en/stable/public_server.html
    + Set a password
    + etc.

### Usage

- Jupyter notebook: https://realpython.com/jupyter-notebook-introduction/
- Jupyter lab: https://towardsdatascience.com/jupyter-lab-evolution-of-the-jupyter-notebook-5297cacde6b

### Tips and Tricks for jupyter notebook

#### Export to PDF without section numbers

```nosecnum.tplx
((* extends 'article.tplx' *))

((* block commands *))
\setcounter{secnumdepth}{0} % Turns off numbering for sections
((( super() )))
((* endblock commands *))
```

`jupyter notebook --to=pdf --template=nosecnum.tplx file.ipynb`

#### Install nbextensions

#### Export to PDF with newpage break

- Add the following code to a raw NBConvert cell type:

```
%%latex
\newpage
```

#### Export to HTML without code blocks (hide all input blocks)

`jupyter nbconvert <yourFile>.ipynb --no-input --no-prompt`

## pylint

- looking for bugs and poor quality code

## [cryptography](https://github.com/pyca/cryptography)

## [pycrypto](https://github.com/dlitz/pycrypto)

## [virtualenv](https://pypi.python.org/pypi/virtualenv)

## [Console User interface library](https://github.com/urwid/urwid)

- [alot - Mail User Agent](https://github.com/pazz/alot)

## Django

## [SQLAlchemy](http://www.sqlalchemy.org/)

SQLAlchemy is the Python SQL toolkit and Object Relational Mapper that
gives application developers the full power and flexibility of SQL.

[SourCode](https://bitbucket.org/zzzeek/sqlalchemy)

## [peewee](http://peewee.readthedocs.org/en/latest/index.html)

Peewee is a simple and small ORM. It has few (but expressive) concepts,
making it easy to learn and intuitive to use.
- A small, expressive ORM
- Written in python with support for versions 2.6+ and 3.2+.
- built-in support for sqlite, mysql and postgresql
- tons of extensions available in the [Playhouse, a collection of addons](http://peewee.readthedocs.org/en/latest/peewee/playhouse.html#playhouse) (postgres hstore/json/arrays, sqlite full-text-search, schema migrations, and much more).

[SourCode](https://github.com/coleifer/peewee)

## requests

A HTTP library, written in Python, for human beings.

## [csv file](http://softwarerecs.stackexchange.com/questions/7463/fastest-python-library-to-read-a-csv-file)


# Tutorial

## Working with images

- Lowest level: PIL/Pillow (PIL is discontinued)
- Wrappers on top:
    + imageio:
        * less dependencies (numpy, Pillow)
        * for simple tasks
    + scikit-image
        * powerful
        * easy to integrate with scikit ecosystem
- Different system
    + cv2
        * the most powerful tool
        * the most complex system
        * faster than Pillow
    + pillow-simd
        * a fork of pillow
        * fastest

## Threading

- https://docs.python.org/2/library/threading.html
- https://www.tutorialspoint.com/python/python_multithreading.htm

## Python's slicing

   +---+---+---+---+---+---+
   | P | y | t | h | o | n |
   +---+---+---+---+---+---+
     0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1   0

    a[start:end] # items start through end-1
    a[start:]    # items start through the rest of the array
    a[:end]      # items from the beginning through end-1
    a[:]         # a copy of the whole array

There is also the `step` value, which can be used with any of the above:

    a[start:end:step] # start through not past end, by step

The key point to remember is that the `:end` value represents the first
value that is not in the selected slice. So, the difference between
`end` and `start` is the number of elements selected (if `step` is 1,
the default).

The other feature is that `start` or `end` may be a negative number,
which means it counts from the end of the array instead of the
beginning. So:

    a[-1]    # last item in the array
    a[-2:]   # last two items in the array
    a[:-2]   # everything except the last two items

Similarly, `step` may be a negative number:

    a[::-1]    # all items in the array, reversed
    a[1::-1]   # the first two items, reversed
    a[:-3:-1]  # the last two items, reversed
    a[-3::-1]  # everything except the last two items, reversed

Python is kind to the programmer if there are fewer items than you ask
for. For example, if you ask for `a[:-2]` and `a` only contains one
element, you get an empty list instead of an error. Sometimes you would
prefer the error, so you have to be aware that this may happen.

## Structure of a script

```python
#!/usr/bin/python
import sth

def myfunction():
	sth...

def main():
	myfunction();
	sth...

if __name__ == '__main__':
	main()
else:
	sth...
```





## I/O

- [Redirect stdout to file](http://stackoverflow.com/questions/4675728/redirect-stdout-to-a-file-in-python)

## [Work with MySQL](http://stackoverflow.com/questions/372885/how-do-i-connect-to-a-mysql-database-in-python)

- [Python MySQL Database Access](http://www.tutorialspoint.com/python/python_database_access.htm)
- [MySQL Unicode and Encoding](http://stackoverflow.com/questions/8365660/python-mysql-unicode-and-encoding)

## Work with Encoding

- [Unicode reading and writing to files in python](http://stackoverflow.com/questions/491921/unicode-utf8-reading-and-writing-to-files-in-python?answertab=votes#tab-top) see the answer most votes below accepted answer (not see accepted answer)
- [codecs](https://docs.python.org/2/library/codecs.html) module

# Glossary

- `inf`: is infinity - a value that is greater than any other value.
  `-inf` is therefore smaller than any other value.
- `nan`: stands for Not A Number
- `[]`: Used to define mutable data types - lists, list comprehensions and for indexing/lookup/slicing.
- `()`: Define tuples, order of operations, generator expressions, function calls and other syntax.
- `{}`: The two hash table types - dictionaries and sets.

# Tips and Tricks

## Reload the class source file after importing

- `>>> reload(shop)`

## Asterisk in Python

- https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/

## exit a Python script

- https://stackoverflow.com/questions/19747371/python-exit-commands-why-so-many-and-when-should-each-be-used
- sys.exit(): proper way (import sys)
- raise SystemExit

## Multiline string

- Concatenation
- Multi-line string syntax
- Tuple syntax

```
template = "This is the first line.\n" \
           "This is the second line.\n" \
           "This is the third line."

template = """This is the first line.
This is the second line.
This is the third line."""

template = ("This is the first line.\n"
            "This is the second line.\n"
            "This is the third line.")
```


## pipenv - work flow for a big project

### Introduction

- pipenv
    + separate development environment and production environment
    + combine virtualenv, pip, and Pipfile

### Usage

```
$ cd my_project

// create two new files, Pipfile and Pipfile.lock
// create a new virtual environment for the project
// pipenv install --two : use Python 2
// pipenv install --three : use Python 3
$ pipenv install

// install a new package
$ pipenv install beautifulsoup4

// uninstall a package
$ pipenv uninstall beautifulsoup4

// freeze the list of dependencies
$ pipenv lock

// Add Pipfiles to VCS


===
// Separate development environment
$ pipenv install --dev nose2

// Install packages in development environment
$ pipenv install --dev


===
// Running your code
// Activate the virtual environment
$ pipenv shell

// python run : invoke shell commands in your virtual environment
// without explicitly activating it first
$ pipenv run which python
$ pipenv run python my_project.py
```

## Get the class name as a string of an instance

- `instance.__class__.__name__`
- `self.__class__.__name__`: current class name

## Check for NaN (not a number)

- IEEE 754 standards
- Using `math.isnan(x)`: new in version >= 2.6
- version < 2.6: using `numpy.isnan()`

## File extensions

- .py - Regular scripts
- .py3 - (rarely used) Python3 script. Python3 scripts usually end with
  ".py" not ".py3", but I have seen that a few times
- .pyc - compiled script (Bytecode)
- .pyo - optimized pyc file (As of Python3.5, Python will only use pyc
  rather than pyo and pyc)
- .pyw - Python script for Windows. It is executed with pythonw.exe
- .pyx - Cython src to be converted to C/C++
- .pyd - Python script made as a Windows DLL
- .pxd - Cython script which is equivalent to a C/C++ header
- .pxi - MyPy stub
- .pyi - Stub file (PEP 484)
- .pyz - Python script archive (PEP 441); this is a script containing
  compressed Python scripts (ZIP) in binary form after the standard
  Python script header
- .pywz - Python script archive for MS-Windows (PEP 441); this is a
  script containing compressed Python scripts (ZIP) in binary form after
  the standard Python script header
- .py[cod] - wildcard notation in ".gitignore" that means the file may
  be ".pyc", ".pyo", or ".pyd".

A larger list of additional Python file-extensions (mostly rare and
unofficial) can be found at http://dcjtech.info/topic/python-file-
extensions/

## Check python version by python code

```python
import sys

print sys.version_info
```


# IPython

- An enhanced Python command line
- Jupiter: notebook can be used for a web interface to IPython
- bpython: a ncurses interface to the Python interpreter

# Troubleshoots

## Broken references in Virtualenvs

```
dyld: Library not loaded: @executable_path/../.Python
  Referenced from: /Users/[user]/.virtualenvs/modclass/bin/python
  Reason: image not found
Trace/BPT trap: 5
```

I found the solution to the problem
[here](https://web.archive.org/web/20150206132233/https://wirtel.be/posts/en/2014/07/29/fix_virtualenv_python_brew/),
so all credit goes to the author.

The gist is that when you create a virtualenv, many symlinks are created
to the Homebrew installed Python.

Here is one example:

    $ ls -la ~/.virtualenvs/my-virtual-env
    ...
    lrwxr-xr-x  1 ryan staff   78 Jun 25 13:21 .Python -> /usr/local/Cellar/python/2.7.7/Frameworks/Python.framework/Versions/2.7/Python
    ...

When you upgrade Python using Homebrew and then run ``brew cleanup``,
the symlinks in the virtualenv point to paths that no longer exist
(because Homebrew deleted them).

The symlinks needs to point to the newly installed Python:

    lrwxr-xr-x  1 ryan staff   78 Jun 25 13:21 .Python -> /usr/local/Cellar/python/2.7.8_1/Frameworks/Python.framework/Versions/2.7/Python

The solution is to remove the symlinks in the virtualenv and then
recreate them:

    find ~/.virtualenvs/my-virtual-env/ -type l -delete
    virtualenv ~/.virtualenvs/my-virtual-env

It's probably best to check what links will be deleted first before
deleting them:

    find ~/.virtualenvs/my-virtual-env/ -type l

In my opinion, it's even better to only delete broken symlinks. You can
do this using GNU `find`:

    gfind ~/.virtualenvs/my-virtual-env/ -type l -xtype l -delete

You can install GNU `find` with Homebrew if you don't already have it:

    brew install findutils

Notice that by default, GNU programs installed with Homebrew tend to be
prefixed with the letter `g`. This is to avoid shadowing the `find`
binary that ships with OS X.
# References

[doc]:https://docs.python.org/3.6/
[threading]: https://docs.python.org/2/library/threading.html
[tut-threading]: https://www.tutorialspoint.com/python/python_multithreading.htm
