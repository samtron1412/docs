[TOC]

# Overview

## Introduction

- **General-purpose, high level programming language**
- **Multi-paradigm:** object-oriented, imperative, functional,
  procedural, reflective
- **Typing:** duck, dunamic, strong
- First release: 1991

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

- `pydoc`: a Linux/UNIX command
    + `pydoc sys`: showing help page for `sys` module
- Showing built-in methods for an built-in datatype in the Python
  interpreter:
    + `dir('abc')`: showing built-in methods for a string
- Learn about the built-in function using `help()` in the Python
  interpreter:
    + `help('ab'.find)`: showing the help for the find method


# Usage of the Interpreter

- Access the history commands
    + `Ctrl+p` (previous), `Ctrl+n` (next)
- Exit a session
    + `Ctrl+d`
- Doctest
    + `python3 -m doctest <python_file>`
    + doctests are surrounded by `"""`
    + Or add the following code in python file and run: `python file.py
      -v`

```python
if __name__ == "__main__":
    import doctest
    doctest.testmod()
```
- Run the script and then open an interactive session
    + `python3 -i <script_file>`


# The Python Standard Library

## Build-in Data Types

### List


### Dict


### Set

- https://realpython.com/python-sets/

## Counter

- https://pymotw.com/2/collections/counter.html

# Extra Data Structures

## heapq (min heap)

- if want max heap, negate all items
- `heapq.heappush(heap, item)`
- `heapq.heappop(heap)`
- `heapq.heapify(list)`

```python
import heapq
heap = []
heapq.heappush(heap, (1, 'abc'))
heapq.heappush(heap, (5, 'cde'))
```

## queue

- `queue.Queue()`
- `queue.PriorityQueue()`

```python
q = queue.PriorityQueue()
q.put((1, 'abc'))
q.put((2, 'cde'))
x = q.get()
```

## Monotone Stack

- https://helloacm.com/the-monotone-stack-implementation-in-python/#:~:text=The%20Monotone%20Stack%20in%20Python&text=At%20anytime%2C%20the%20monotone%20stack,or%2Dequal%20number%20is%203.

# Conda

- Conda vs. Pip
    + https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/
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
- `conda list`: show a list of all packages
- `conda install`
- `conda package`
- `conda search`
- `conda remove`
- `conda update`

## Tasks

- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/index.html

### Managing Channels

- Install a package from a non-default channel:
    + `conda install --channel conda-forge opencv`
- Add a new channel
    + `conda config --append channels conda-forge`
    + Or you can modify `~/.condarc`: the order of channels is matter,
    conda looks at these channel in order

```.condarc
channels:
  - defaults
  - conda-forge
channel_priority: strict
```

### Managing environments

- Activate an environment: `conda activate env_name`
- Deactivate: `conda deactivate`
- List all environments: `conda list --envs`
    + `conda env list`
- `conda init`: add some code to shellrc (.zshrc, etc.) to modify PATH
  when run conda activate
- Remove an environment: `conda env remove --name myenv`
- Create a new environment: `conda create --name myenv`
- Specify python version: `conda create -n myenv python=3.4`
- Specify default packages: `conda create -n myenv scipy`
- Specify version of a package: `conda create -n myenv scipy=0.15.0`
- Specify python and multiple packages
    + `conda create -n myenv python=3.4 scipy=0.15.0 astroid babel`
- No default packages: `conda create --no-default-packages -n myenv python`
- Building an identical environment using spec-file (usually is the same
  computer not for sharing)
    + `conda list --explicit > spec-file.txt`
    + `conda create --name myenv --file spec-file.txt`
- Sharing environments:
    + Export the active environment with all packages
        * `conda env export > environment.yml`
        * This way may not work across platforms because some of
        dependencies are different in different platforms.
    + Export only packages that you specifically install not all of its
    dependencies. The dependencies will be installed on the new platform
    later by conda.
        * `conda env export --from-history > environment.yml`
        * https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#exporting-an-environment-file-across-platforms
    + Creating an environment from an environment.yml file:
        * `conda env create -f environment.yml`

```environment.yml
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

- Restore an environment:
    + List the history of changes: `conda list --revisions`
    + Restore: `conda install --rev REVNUM`
        * `conda install --rev 8`
- Specify location for the environment:
    + `conda create --prefix /path/to/myenv jupyterlab=0.35 matplotlib=3.1 numpy=1.16`
    + Activate by name: `conda activate /path/to/myenv`
- Update an environment by modifying .yml file and run:
    + `conda env update -n conda-env -f /path/to/environment.yml`
    + `conda env update --prefix ./env --file environment.yml  --prune`
- Cloning an environment: `conda create --name myclone --clone myenv`


### Managing packages

- Activate an environment before installing a package
- Search a package: `conda search scipy`
- Install a package: `conda install scipy`
- Specific version: `conda install scipy=0.15.0`
- Update a package: `conda update scipy`
- View list of packages: `conda list`

### Managing python

- List all python versions: `conda search python`
    + `conda search --full-name python`
- Update python: `conda update python`




# Packages

## jupyter

Looking at `jupyter.md`

## sphinx

Generate Documentation for Python software

## pylint

- looking for bugs and poor quality code

## requests

A HTTP library, written in Python, for human beings.

## csv file

http://softwarerecs.stackexchange.com/questions/7463/fastest-python-library-to-read-a-csv-file


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
- `[]`: Used to define mutable data types - lists, list comprehensions
  and for indexing/lookup/slicing.
- `()`: Define tuples, order of operations, generator expressions,
  function calls and other syntax.
- `{}`: The two hash table types - dictionaries and sets.


# Tips and Tricks

## Caching in Python

- https://realpython.com/lru-cache-python/
- `lru_cache` decorator
    + `@lru_cache(maxsize=None)`: the size is unlimited, no need to
      evict anything, but it can grow indefinitely (will crash)
    + `@lru_cache(maxsize=128)`: maxsize is set to 128 as default

```python
from functools import lru_cache

@lru_cache
def steps_to(stair):
    ...
```

## `*args` and `**kwargs`, unpacking and packing values

- https://realpython.com/python-kwargs-and-args/
- `*args` and `**kwargs` are used to pass multiple arguments to a
  function
    + `*args` is used for iterable arguments
    + `**kwargs` is used for keyword arguments
- `*` is a operator that can use to unpack iterables
    + it can unpack a list into numbers
- `**` can unpack or pack keyword values
- order is important: `*args` should be before `**kwargs` in function
  signature: `def func(*args, **kwargs)`

```python
# sum_integers_args_2.py
def my_sum(*integers):
    result = 0
    for x in integers:
        result += x
    return result

print(my_sum(1, 2, 3))

# concatenate.py
def concatenate(**kwargs):
    result = ""
    # Iterating over the Python kwargs dictionary
    for arg in kwargs.values():
        result += arg
    return result

print(concatenate(a="Real", b="Python", c="Is", d="Great", e="!"))
```

## List Comprehensions and If/Else

- If and else: `[f(x) if condition else g(x) for x in sequence]`
- If only: `[f(x) for x in sequence if condition]`

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



## Get the class name as a string of an instance

- `instance.__class__.__name__`
- `self.__class__.__name__`: current class name

## Check for NaN (not a number)

- IEEE 754 standards
- Using `math.isnan(x)`: new in version >= 2.6
- version less than 2.6: using `numpy.isnan()`

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


# Troubleshoots


# The Python Language Specification

- https://docs.python.org/3/reference/index.html


# References

[threading]: https://docs.python.org/2/library/threading.html
[tut-threading]: https://www.tutorialspoint.com/python/python_multithreading.htm
