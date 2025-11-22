[TOC]

# Overview

## Introduction

- **General-purpose, high level programming language**
- **Multi-paradigm:** object-oriented, imperative, functional,
  procedural, reflective
- **Typing:** duck, dynamic, strong
- First release: 1991

## Resources

- Books:
    + https://realpython.com/best-python-books/#best-books-for-learning-python
    + https://hackr.io/blog/best-python-books-for-beginners-and-advanced-programmers
    + https://www.amazon.com/Fluent-Python-Concise-Effective-Programming/dp/1492056359/ref=pd_lpo_d_sccl_1/144-2146829-3357530
        * Fluent Python: Clear, Concise, and Effective Programming
- Best resources for Python OOP
    + https://aspp.school/python-summerschool-2013/_media/wiki/oop/oo_design_2013.pdf
    + https://www.programiz.com/python-programming/object-oriented-programming
    + https://dbader.org/img/oop-in-python-best-resources.pdf
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
- Design pattern
    + https://github.com/faif/python-patterns
- Courses
    + https://try.codecademy.com/learn-python-3?g_network=g&g_productchannel=&g_adid=699378988048&g_locinterest=&g_keyword=python%20lessons&g_acctid=243-039-7011&g_adtype=search&g_keywordid=kwd-297326765641&g_ifcreative=&g_campaign=account&g_locphysical=9033253&g_adgroupid=165097891369&g_productid=&g_source=%7Bsourceid%7D&g_merchantid=&g_placement=&g_partition=&g_campaignid=21287608736&g_ifproduct=&utm_id=t_kwd-297326765641:ag_165097891369:cp_21287608736:n_g:d_c&utm_source=google&utm_medium=paid-search&utm_term=python%20lessons&utm_campaign=US_-_Exact&utm_content=699378988048&gad_campaignid=21287608736

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

## Built-in Functions

## Built-in Constants

## Built-in Data Types

### List


### Dict


### Set

- https://realpython.com/python-sets/

## Built-in Exceptions

## Extra Data Structures

### collections

#### namedtuple() - factory function for creating tuple subclasses with named fields

- Creating a tuple subclass with named fields

```python
from collections import namedtuple

Student = namedtuple('Student', 'fname, lname, age')
first  = Student('Son', 'Tran', '29')
print(first.fname)
print(first.lname)
print(first.age)
```

#### Counter

- A dictionary subclass for counting hashable objects.
- https://pymotw.com/2/collections/counter.html

#### OrderedDict

- A dictionary subclass that remembers the order entries were added
- Linkedlist and hash map

#### defaultdict

- A dictionary subclass that calls a factory function to supply missing
  values.

```python
from collections import defaultdict
d = defaultdict(int)
print(d[1])
```

#### deque

- A list-like container with fast appends and pops on either ends

```python
>>> from collections import deque
>>> d = deque('ghi')                 # make a new deque with three items
>>> for elem in d:                   # iterate over the deque's elements
...     print(elem.upper())
G
H
I

>>> d.append('j')                    # add a new entry to the right side
>>> d.appendleft('f')                # add a new entry to the left side
>>> d                                # show the representation of the deque
deque(['f', 'g', 'h', 'i', 'j'])

>>> d.pop()                          # return and remove the rightmost item
'j'
>>> d.popleft()                      # return and remove the leftmost item
'f'
>>> list(d)                          # list the contents of the deque
['g', 'h', 'i']
>>> d[0]                             # peek at leftmost item
'g'
>>> d[-1]                            # peek at rightmost item
'i'

>>> list(reversed(d))                # list the contents of a deque in reverse
['i', 'h', 'g']
>>> 'h' in d                         # search the deque
True
>>> d.extend('jkl')                  # add multiple elements at once
>>> d
deque(['g', 'h', 'i', 'j', 'k', 'l'])
>>> d.rotate(1)                      # right rotation
>>> d
deque(['l', 'g', 'h', 'i', 'j', 'k'])
>>> d.rotate(-1)                     # left rotation
>>> d
deque(['g', 'h', 'i', 'j', 'k', 'l'])

>>> deque(reversed(d))               # make a new deque in reverse order
deque(['l', 'k', 'j', 'i', 'h', 'g'])
>>> d.clear()                        # empty the deque
>>> d.pop()                          # cannot pop from an empty deque
Traceback (most recent call last):
    File "<pyshell#6>", line 1, in -toplevel-
        d.pop()
IndexError: pop from an empty deque

>>> d.extendleft('abc')              # extendleft() reverses the input order
>>> d
deque(['c', 'b', 'a'])
```

#### ChainMap

- A dict-like class for creating a single view of multiple mappings.
- https://florimond.dev/blog/articles/2018/07/a-practical-usage-of-chainmap-in-python/
- https://stackoverflow.com/questions/23392976/what-is-the-purpose-of-collections-chainmap

```python
# cli.py
import argparse
import os
from collections import ChainMap

defaults = {"debug": False}

parser = argparse.ArgumentParser()
parser.add_argument("--debug")
args = parser.parse_args()
cli_args = {key: value for key, value in vars(args).items() if value}

config = ChainMap(cli_args, os.environ, defaults)

print(config.get("debug"))
```

#### UserDict

- A wrapper around dictionary objects for easier dict subclassing

```python
from collections import UserDict


# Creating a Dictionary where
# deletion is not allowed
class MyDict(UserDict):

    # Function to stop deleltion
    # from dictionary
    def __del__(self):
        raise RuntimeError("Deletion not allowed")

    # Function to stop pop from
    # dictionary
    def pop(self, s = None):
        raise RuntimeError("Deletion not allowed")

    # Function to stop popitem
    # from Dictionary
    def popitem(self, s = None):
        raise RuntimeError("Deletion not allowed")

# Driver's code
d = MyDict({'a':1,
    'b': 2,
    'c': 3})

d.pop(1)
```

### heapq (min heap)

- if want max heap, negate all items
- `heapq.heappush(heap, item)`
- `heapq.heappop(heap)`
    + pop the top of the heap
    + peeking the top of the heap by using `heap[0]`
- `heapq.heapify(list)`
- `heapq.pushpop(heap, item)`
    + push the new item then pop the top
    + more efficient than doing push then pop
    + keep a fixed size heap
    + returns the smaller value between the new and old items
- `heapq.heapreplace(heap, item)`
    + pop then push the new item
    + more efficient than pop then push
    + keep a fixed size heap
    + it may return larger value between the new and old items
- `heapq.nlargest(n, iterable, key=None)`
- `heapq.nsmallest(n, iterable, key=None)`

```python
import heapq
heap = []
heapq.heappush(heap, (1, 'abc'))
heapq.heappush(heap, (5, 'cde'))
```

### queue

- Thread safe, using in concurrent programming
- `queue.Queue()`
- `queue.PriorityQueue()`

```python
q = queue.PriorityQueue()
q.put((1, 'abc'))
q.put((2, 'cde'))
x = q.get()
```

### bisect

- Array bisection algorithm: binary search

### array

- Similar list but the type of elements is constrained.

### enum



### Monotone Stack

- https://helloacm.com/the-monotone-stack-implementation-in-python/#:~:text=The%20Monotone%20Stack%20in%20Python&text=At%20anytime%2C%20the%20monotone%20stack,or%2Dequal%20number%20is%203.

# Object Oriented Programming (OOP)

- https://realpython.com/python3-object-oriented-programming/
- https://coreyms.com/development/python/python-oop-tutorials-complete-series
- https://www.udemy.com/course/object-oriented-python-programming/
- https://www.datacamp.com/community/tutorials/inner-classes-python
- super(): https://realpython.com/python-super/
- hashable objects: https://hynek.me/articles/hashes-and-equality/
    + using `id` of an object
- is __init__ always needed:
    + https://stackoverflow.com/questions/6854080/is-it-necessary-to-include-init-as-the-first-function-every-time-in-a-class
    + No


## Type Checking

- https://realpython.com/python-type-checking/

## Inheritance

- https://www.w3schools.com/python/python_inheritance.asp

# Development Environment Setup

## Python version and package management

- Only Python packages:
    + uv:
        * https://docs.astral.sh/uv/
        * If your system has `mise`, then make sure to not use it for
          Python
            - https://mise.jdx.dev/mise-cookbook/python.html
        * Using Jupyter from VS Code with uv
            - https://docs.astral.sh/uv/guides/integration/jupyter/#using-jupyter-from-vs-code
            - `uv add --dev ipykernel`
- You also need non-Python packages:
    + pixi
        * https://pixi.sh/latest/
    + miniforge (open-source minimal installer for conda and mamba)
        * https://conda-forge.org
        * https://github.com/conda-forge/miniforge

## Linter and Formatter

- Ruff
    + https://docs.astral.sh/ruff/

## Static Type Checker

- pyright
    + https://github.com/microsoft/pyright
- ty (same creator as uv and ruff; written in Rust)
    + https://github.com/astral-sh/ty
    + https://docs.astral.sh/ty

# Use Cases

## Data Analysis

- Single machine
    + Polars (Rust-based)
    + DuckDB
    + Dask
- Multiple machines / clusters
    + PySpark
    + Dask

## Read and Write Parquet files

- Polars
- DuckDB

## Read and Write Avro Files

- Avro to Polar DataFrame
    + https://pypi.org/project/polars-avro/
- Avro to Pandas DataFrame
    + https://github.com/ynqa/pandavro
- Official Python package: https://avro.apache.org/docs/1.11.1/getting-started-python/
- 2019 summary
    + https://www.perfectlyrandom.org/2019/11/29/handling-avro-files-in-python/

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

## Working with shell scripts

- https://www.geeksforgeeks.org/how-to-run-bash-script-in-python/
- https://www.google.com/search?q=python+tutorial+to+run+shell+script&rlz=1C5GCEM_enUS953US953&oq=python+tutorial+to+run+shell+script&aqs=chrome..69i57.6427j0j4&sourceid=chrome&ie=UTF-8

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

## Iterables and Iterator; Generator and Coroutines

- http://www.dabeaz.com/coroutines/
- https://www.python.org/dev/peps/pep-0342/
- https://www.python.org/dev/peps/pep-0380/
- Coroutines
    + If you use yield more generally, you get a coroutine.
    + These do more than just generate values.
    + Instead, functions can consume values sent to it.

# Tips and Tricks

## f-strings, Format Strings

- https://realpython.com/python-f-strings/
    + New way to format string since 3.6
    + Easier to read and faster

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

## `*args` and `**kwargs`, unpacking and packing values; Asterisk in Python

- https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/
- https://realpython.com/python-kwargs-and-args/
- In Python, `*args` and `**kwargs` are special syntaxes used in
  function definitions to allow a function to accept a variable number
  of arguments.
    + They are primarily used when the exact number of arguments a
      function will receive is unknown at the time of defining the
      function.
    + `*args`: arbitrary positional (non-keyworded) arguments
        * The unpacking operator (`*`) will collect arguments into a
          tuple (immutable list) `args` (you can use a different name if
          you like, not necessary to be `args`)
    + `**kwargs` is used for keyword arguments, so `kwargs` is a
      dictionary of all keyword arguments.
- `*` is a operator that can use to unpack iterables
- `**` can unpack or pack keyword values
- Order is important: standard arguments, and then `*args` should be
  before `**kwargs` in function
  Signature: `def func(a, b, *args, **kwargs)`

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


# The Python Language Reference / Specification

- https://docs.python.org/3/reference/index.html

## Introduction

## Lexical Analysis

## Data model

## Execution model

## The import system

## Expressions

## Simple statements

### Assignment Statement

- `left = right`
    + Evaluate all expressions in the right of = from left to right
    + Bind all names in the left of = to those resulting values in the
      current frame.
- Parallel assignment: `a, b = 1, 2`
- The assignment returns the values of the right side
- Double assignment: `a, b = c, d = 1, 2`
    + assign the right most values to other names

### del statement

- https://www.programiz.com/python-programming/del
- https://stackoverflow.com/questions/6146963/when-is-del-useful-in-python
- `del obj_name` statement can be to delete variables, user-defined
  objects, lists, items within lists, dictionaries, etc.

## Compound statements

## Top-level components

## Full grammar specification

- https://docs.python.org/3/reference/grammar.html

# References

[threading]: https://docs.python.org/2/library/threading.html
[tut-threading]: https://www.tutorialspoint.com/python/python_multithreading.htm
