[TOC]

# Overview

## NumPy

### What is NumPy?

NumPy is a Python extension module that provides efficient operation on
arrays of homogeneous data. It allows Python to serve as a high-level
language for manipulating numerical data, much like for example IDL or
MATLAB.

### What is a NumPy array?

A NumPy array is a multidimensional array of objects all of the same
type. In memory, it is an object which points to a block of memory,
keeps track of the type of data stored in that memory, keeps track of
how many dimensions there are and how large each one is, and -
importantly - the spacing between elements along each axis.

For example, you might have a NumPy array that represents the numbers
from zero to nine, stored as 32-bit integers, one right after another,
in a single block of memory. (for comparison, each Python integer needs
to have some type information stored alongside it). You might also have
the array of even numbers from zero to eight, stored in the same block
of memory, but with a gap of four bytes (one 32-bit integer) between
elements. This is called striding, and it means that you can often
create a new array referring to a subset of the elements in an array
without copying any data. Such subsets are called views. This is an
efficiency gain, obviously, but it also allows modification of selected
elements of an array in various ways.

An important constraint on NumPy arrays is that for a given axis, all
the elements must be spaced by the same number of bytes in memory. NumPy
cannot use double-indirection to access array elements, so indexing
modes that would require this must produce copies. This constraint makes
it possible for all the inner loops in NumPy’s internals to be written
in efficient C code.

NumPy arrays offer a number of other possibilities, including using a
memory-mapped disk file as the storage space for an array, and record
arrays, where each element can have a custom, compound data type.

### What advantages do NumPy arrays offer over (nested) Python lists?

Python’s lists are efficient general-purpose containers. They support
(fairly) efficient insertion, deletion, appending, and concatenation,
and Python’s list comprehensions make them easy to construct and
manipulate. However, they have certain limitations: they don’t support
“vectorized” operations like elementwise addition and multiplication,
and the fact that they can contain objects of differing types mean that
Python must store type information for every element, and must execute
type dispatching code when operating on each element. This also means
that very few list operations can be carried out by efficient C loops –
each iteration would require type checks and other Python API
bookkeeping.

## SciPy

### What is SciPy?

SciPy is a set of open source (BSD licensed) scientific and numerical
tools for Python. It currently supports special functions, integration,
ordinary differential equation (ODE) solvers, gradient optimization,
parallel programming tools, an expression-to-C++ compiler for fast
execution, and others. A good rule of thumb is that if it’s covered in a
general textbook on numerical computing (for example, the well-known
Numerical Recipes series), it’s probably implemented in SciPy.

### What is the difference between NumPy and SciPy?

In an ideal world, NumPy would contain nothing but the array data type
and the most basic operations: indexing, sorting, reshaping, basic
elementwise functions, et cetera. All numerical code would reside in
SciPy. However, one of NumPy’s important goals is compatibility, so
NumPy tries to retain all features supported by either of its
predecessors. Thus NumPy contains some linear algebra functions and
Fourier transforms, even though these more properly belong in SciPy. In
any case, SciPy contains more fully-featured versions of the linear
algebra modules, as well as many other numerical algorithms. If you are
doing scientific computing with Python, you should probably install both
NumPy and SciPy. Most new features belong in SciPy rather than NumPy.

### Why both numpy.linalg and scipy.linalg? What’s the difference?

scipy.linalg is a more complete wrapping of Fortran LAPACK using f2py.

One of the design goals of NumPy was to make it buildable without a
Fortran compiler, and if you don’t have LAPACK available NumPy will use
its own implementation. SciPy requires a Fortran compiler to be built,
and heavily depends on wrapped Fortran code.

The linalg modules in NumPy and SciPy have some common functions but
with different docstrings, and scipy.linalg contains functions not found
in numpy.linalg, such as functions related to LU decomposition and the
Schur decomposition, multiple ways of calculating the pseudoinverse, and
matrix transcendentals like the matrix logarithm. Some functions that
exist in both have augmented functionality in scipy.linalg; for example
scipy.linalg.eig() can take a second matrix argument for solving
generalized eigenvalue problems.

# Basic Usage

## Axes

- `0`: (Oy axis) vertical axis
- `1`: (Ox axis) horizontal axis

## Shape

```python
>>>a = np.array([[1, 2], [3, 4], [5, 6]])
>>>a.shape
(3, 2)
>>>a.reshape(3, 2)
```

- numpy.reshape(a, newshape, order='C')
    + Gives a new shape to an array without changing its data
- numpy.size(a, axis=None)
    + Default: return total elements
    + axis = 0: # of rows
    + axis = 1: # of columns

## ndarray

- https://docs.scipy.org/doc/numpy/reference/arrays.ndarray.html


## What is the preferred way to check for an empty (zero element) array?

If you are certain a variable is an array, then use the size attribute.
If the variable may be a list or other sequence type, use len(). The
size attribute is preferable to len because:

```python
>>> a = numpy.zeros((1,0))
>>> a.size
0
>>> len(a)
1
```

## I want to load data from a text file. How do I make this code more efficient?

Use `numpy.loadtxt()`. Even if your text file has header and footer
lines or comments, loadtxt can almost certainly read it; it is
convenient and efficient.

If you find this still too slow, you can try Pandas (it has a faster csv
reader for example). If that doesn’t help, you should consider changing
to a more efficient file format than plain text. There are a large
number of alternatives, depending on your needs (and on which version of
NumPy/SciPy you are using):

- Text files: slow, huge, portable, human-readable; built into NumPy
- pickle: somewhat slow, somewhat portable (may be incompatible with
  different NumPy versions); built into NumPy
- HDF5: high-powered kitchen-sink format; both PyTables and h5py provide
  a NumPy friendly interface on top of the core HDF5 library written in
  C.
- FITS: standard kitchen-sink format in astronomy; the astropy library
  provides a convenient Python interface through its io.fits package.
- .npy: NumPy native binary data format, simple, efficient, portable;
  built into NumPy as of 1.0.5.

## What is the difference between matrices and arrays?

Note: NumPy matrices will be deprecated, do not use them for new code.

## How do I find the indices of an array where some condition is true?

The prefered idiom for doing this is to use the function numpy.nonzero()
, or the nonzero() method of an array. Given an array a, the condition
a>3 returns a boolean array and since False is interpreted as 0 in
Python and NumPy, np.nonzero(a > 3) yields the indices of a where the
condition is true.

## Repeat elements of an array

- numpy.repeat(a, repeats, axis=None)

https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.repeat.html

## Construct an array by repeating A the number of times given by reps

- numpy.tile(A, reps)

https://docs.scipy.org/doc/numpy/reference/generated/numpy.tile.html

# np.linalg

something

# scipy.linalg

something
