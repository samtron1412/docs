[TOC]

# Overview

C++ (pronounced cee plus plus) is a general purpose programming
language. It has imperative, object-oriented and generic programming
features, while also providing the facilities for low level memory
manipulation. It is designed with **a bias for systems programming**
(e.g. embedded systems, operating system kernels), with performance,
efficiency and flexibility of use as its design requirements. C++ has
also been found useful in many other contexts, including *desktop
applications*, *servers* (e.g. e-commerce, web search, SQL),
*performance critical applications* (e.g. telephone switches, space
probes) and *entertainment software*, such as video games.

## History

**In 1983**, it was renamed from C with Classes to C++ (++ being the
increment operator in C). New features were added including **virtual
functions**, **function name** and **operator overloading**,
**references**, **constants**, **type-safe free-store memory
allocation** (new/delete), **improved type checking**, and BCPL style
single-line comments with two forward slashes (//), as well as the
development of a proper compiler for C++, Cfront.

**In 1989** C++ 2.0 was released followed by the updated second edition
of The C++ Programming Language in 1991. New features in 2.0 included
**multiple inheritance**, **abstract classes**, **static member
functions**, **const member functions**, and **protected members**.

**In 1990**, The Annotated C++ Reference Manual was published. This work
became the basis for the future standard. Late feature additions
included templates, exceptions, namespaces new casts and a **boolean
type**.

**In 2011**, C++11 was released which added more features and enlarged
the **standard library** further (compared to it in 1998), providing
more facilities for C++ programmers to use, with more additions planned
for 2014 and 2017.

## Philosophy

Throughout C++'s life, its development and evolution has been informally
governed by a set of rules that its evolution should follow:

- It must be driven by actual problems and its features should be useful
  immediately in real world programs.
- Every feature should be implementable (with a reasonably obvious way
  to do so).
- Programmers should be free to pick their own programming style, and
  that style should be fully supported by C++.
- Allowing a useful feature is more important than preventing every
  possible misuse of C++.
- It should provide facilities for organising programs into well-defined
  separate parts, and provide facilities for combining separately
  developed parts.
- No implicit violations of the type system (but allow explicit
  violations that have been explicitly asked for by the programmer).
- Make user created types have equal support and performance to built in
  types.
- Any features that you do not use you do not pay for (e.g. in
  performance).
- There should be no language beneath C++ (except assembly language).
- C++ should work alongside other pre-existing programming languages,
  rather than being part of its own separate and incompatible
  programming environment.
- If what the programmer wants to do is unknown, allow the programmer to
  specify (provide manual control).

## Standardization

The C++ standard consists of two parts:
- The core language
- The standard library:
    + vectors, lists, maps, sets, queues, stacks, arrays, tuples
    + i/o facilities (iostream, for reading from and writing to the
      console and files)
    + smart pointers for automatic memory management
    + regular expression support
    + multi-threading library
    + atomics support (allowing a vaiable to be read or written to by at
      most one thread at a time without any external synchronization)
    + time utilities (measurement, getting current time)
    + exceptions
    + a random number generator
    + and a modified version of the C standard library.
    + Standard Template Library (STL)

| Year | C++ Standard          | Informal name                                                     |
| -    | -                     | -                                                                 |
| 1998 | ISO/IEC 14882:1998    | C++98                                                             |
| 2003 | ISO/IEC 14882:2003    | [C++03](http://en.wikipedia.org/wiki/C%2B%2B03)                   |
| 2007 | ISO/IEC TR 19768:2007 | [C++TR1](http://en.wikipedia.org/wiki/C%2B%2B_Technical_Report_1) |
| 2011 | ISO/IEC 14882:2011    | [C++11](http://en.wikipedia.org/wiki/C%2B%2B11)                   |
| 2014 | ISO/IEC 14882:2014    | [C++14](http://en.wikipedia.org/wiki/C%2B%2B14)                   |

## Question

- What kinds of problems is it designed to help solve?
- What principles underlie the design?
- What are the fundamental limitations?
- What is its definition?

**C++11**

- How is it a better tool?
- What kings of programming styles and techniques does modern C++ support?
- What language and standard-library features support those techniques?
- What are the basic blocks of elegant, correct, maintainable and efficient C++ code?
- What features does C++11 offer over and above C++98?
	+ A machine model suitable for modern computers with a lots of **concurrency**. (standard-library, etc.)
	+ Regular expression handling.
	+ Resources management pointers.
	+ Random numbers.
	+ Improved containers (including, hash tables)
	+ General and uniform initialization, a simpler `for`-statement, move semantics, basic Unicode support, lambdas, general constant expressions, control over class defaults, variadic templates, user-defined literals, and more.

## The Design of C++

The purpose of a programming language is to help **express ideas in
code**. In that, a programming language performs two related tasks:

1. it provides a vehicle for the programmer to specify actions to be
   executed by the machine, and
2. it provides a set of concepts for the programmer to use when thinking
   about what can be done.

The first purpose ideally requires a language that is "close to the
machine" so that all important aspects of a machine are handled simply
and efficiently in a way that is reasonably obvious to the programmer.
The C language was primarily designed with this in mind.

The second purpose ideally requires a language that is "close to the
problem to be solved" so that the concepts of a solution can be
expressed directly and concisely. The facilities added to C to create
C++, such as function argument checking, const, classes, constructors
and destructors, exceptions, and templates, were primarily designed with
this in mind.

Thus, C++ is based on the idea of providing both:
- **direct mappings of built-in operations and types to hardware** to
  provide efficient memory use and efficient low-level operations, and
- **affordable and flexible abstraction mechanisms** to provide user-
  defined types with the same notational support, range of uses, and
  performance as built-in types.

The design of C++ has focused on programming techniques dealing with
fundamental notions such as *memory*, *mutability*, *abstraction*,
*resource management*, *expression of algorithms*, *error handling*, and
*modularity*. Those are the most important concerns of a systems
programmer and more generally of programmers of resource-constrained and
high-performance systems.

**What you don't use you don't pay for**: a language feature and a
fundamental abstraction must be designed not to waste a single byte or a
single processor cycle compared to equivalent alternatives.  This is
known as **the zero-overhead principle**.

### Programming styles

### Type checking

### C Compatibility

### Language, Libraries, and Systems

# Compilers

- GCC
    + g++ -std=c++11 test.cpp -o test
- Clang
    + clang++ -std=c++11 test.cpp -o test

# IDE

- Editors: vim, neovim, sublime text, emacs
- Eclipse
- Codeblock
- Codelite

# Standard library

| header     | description                                              |
| -          | -                                                        |
| iostream   | working with I/O stream                                  |
| iomanip    | I/O manipulators                                         |
| cmath      | mathematical library                                     |
| string     | string class, working with string                        |
| cstdlib    | using random generators                                  |
| ctime      | using time functions                                     |
| cctype     | functions determine the type contained in character data |
| fstream    | file input/output                                        |
| memory     | using smart pointers                                     |
| algorithm  |                                                          |
| functional | functional classes                                       |


# Important Concepts

## Smart Pointers

- [StackOverflow][so-smart-pointer]
- [StackOverflow][so-raw-smart-ptr]
- [Smart Pointer][smart-ptr]

## References vs. Pointers

- [StackOverflow][stack-ref-ptr]
- [cplusplus][c++-distinguish]
- https://www.geeksforgeeks.org/pointers-vs-references-cpp/

## Copy Constructors

## Operator Overloading

## Resource acquisition is initialization (RAII)

## Lambdas

- Added in the C++11 standard
- http://www.drdobbs.com/cpp/lambdas-in-c11/240168241

```
[ captures ] (parameters) -> returnTypesDeclaration { lambdaStatements; }
```

```cpp
#include <iostream>
using namespace std;

int main()
  {
      auto lambda = []() { cout << "Code within a lambda expression" << endl; };
      lambda();
  }
```

# Best practices

## Document and Organize C++ source code

- http://www.edparrish.net/common/cppdoc.html
- Naming conventions
- Comments
- Curly braces
- Whitespaces
- No magic numbers
- No global variables

## Code structure

```cpp
#include <...>
...
//using namespace std;

//global constants

typdef int arrayType[] [NUM_COLS];

//structures or classes

//function prototypes

//main constants
//main variables
//main input
//main processing
//main output
```

## Include guard vs #pragma once vs modules

- https://en.wikipedia.org/wiki/Pragma_once
- https://en.wikipedia.org/wiki/Include_guard
- https://stackoverflow.com/questions/1143936/pragma-once-vs-include-guards
- https://www.reddit.com/r/cpp/comments/4cjjwe/come_on_guys_put_pragma_once_in_the_standard/
- https://kennykerr.ca/2015/12/03/getting-started-with-modules-in-c/

## Choosing file extensions for C++ source files

- C++ headers only: `.hpp`
- C++ source code only: `.cpp`
- C/C++ compatible or pure C headers: `.h`
- C/C++ compatible or pure C source code: `.c`

## Working with references and for loop

- https://stackoverflow.com/questions/15176104/c11-range-based-loop-get-item-by-value-or-reference-to-const
- `auto x : collection`: working with copies
- If copy is an expensive operation
    + `auto &x : collection`: working with the original item and we can
      modify it
    + `auto const &x : collection`: working with the original item and
      we don't want to modify it

# References

[wiki]: https://en.wikipedia.org/wiki/C%2B%2B
[stack-ref-ptr]: https://stackoverflow.com/questions/57483/what-are-the-differences-between-a-pointer-variable-and-a-reference-variable-in
[c++-distinguish]: http://www.cplusplus.com/articles/ENywvCM9/
[so-smart-pointer]: https://stackoverflow.com/questions/8706192/which-kind-of-pointer-do-i-use-when
[so-raw-smart-ptr]: https://stackoverflow.com/questions/6675651/when-should-i-use-raw-pointers-over-smart-pointers
[smart-ptr]: http://ootips.org/yonat/4dev/smart-pointers.html
[document]: http://www.edparrish.net/common/cppdoc.html
