[TOC]

# Overview

- **General-purpose, high level programming language**
- **Multi-paradigm:** object-oriented, imperative, functional, procedural, reflective
- **Typing:** duck, dunamic, strong

## Resources

- The Hitchhiker's Guide to Python:
    + http://docs.python-guide.org/en/latest/
- Google Python course
    + https://developers.google.com/edu/python/

## History

first release: 1991

## Typing

duck

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

# References

[doc]:https://docs.python.org/3.6/
[threading]: https://docs.python.org/2/library/threading.html
[tut-threading]: https://www.tutorialspoint.com/python/python_multithreading.htm
