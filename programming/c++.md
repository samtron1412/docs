[TOC]

# Introduction
C++ (pronounced cee plus plus) is a general purpose programming language. It has [imperative](http://en.wikipedia.org/wiki/Imperative_programming), [object-oriented](http://en.wikipedia.org/wiki/Object-oriented_programming) and [generic](http://en.wikipedia.org/wiki/Generic_programming) programming features, while also providing the facilities for low level memory manipulation.

It is designed with **a bias for systems programming** (e.g. embedded systems, operating system kernels), with performance, efficiency and flexibility of use as its design requirements. C++ has also been found useful in many other contexts, including *desktop applications*, *servers* (e.g. e-commerce, web search, SQL), *performance critical applications* (e.g. telephone switches, space probes) and *entertainment software*, such as video games.

C++ is standardised by the [International Organization for Standardization](http://en.wikipedia.org/wiki/International_Organization_for_Standardization) (ISO), which the latest (and current) having being ratified and published by ISO in September 2011 as [ISO/IEC 14882:2011](http://en.wikipedia.org/wiki/ISO/IEC_14882) (informally known as **C++11**). The C++ programming language was *initially standardised in 1998* as [ISO/IEC 14882:1998](http://en.wikipedia.org/wiki/ISO/IEC_14882), which was then amended by the **C++03**, *ISO/IEC 14882:2003*, standard. The current standard (C++11) supersedes these, with new features and an enlarged standard library.

Before standardization (1989 onwards), *C++ was developed by Bjarne Stroustrup at Bell Labs*, starting in *1979*, who wanted an efficient flexible language (like C) that also provided high level features for program organization.

It is a compiled language, with **implementations** of it available on many platforms. Various organizations provide them, including the [GCC](http://en.wikipedia.org/wiki/GNU_Compiler_Collection), [LLVM](http://en.wikipedia.org/wiki/Clang), [Microsoft](http://en.wikipedia.org/wiki/Microsoft_Visual_C%2B%2B) and [Intel](http://en.wikipedia.org/wiki/Intel_C%2B%2B_Compiler).

## History
**In 1983**, it was renamed from C with Classes to C++ (++ being the increment operator in C). New features were added including [virtual functions](http://en.wikipedia.org/wiki/Virtual_function), **function name** and [operator overloading](http://en.wikipedia.org/wiki/Operator_overloading), **references**, **constants**, **type-safe free-store memory allocation** (new/delete), **improved type checking**, and BCPL style single-line comments with two forward slashes (//), as well as the development of a proper compiler for C++, Cfront.

**In 1989** C++ 2.0 was released followed by the updated second edition of The C++ Programming Language in 1991. New features in 2.0 included **multiple inheritance**, **abstract classes**, **static member functions**, **const member functions**, and **protected members**.

**In 1990**, The Annotated C++ Reference Manual was published. This work became the basis for the future standard. Late feature additions included [templates](http://en.wikipedia.org/wiki/Template_(programming)), [exceptions](http://en.wikipedia.org/wiki/Exception_handling), [namespaces](http://en.wikipedia.org/wiki/Namespaces), new [casts](http://en.wikipedia.org/wiki/Cast_(computer_science)), and a **boolean type**.

**In 2011**, C++11 was released which added more features and enlarged the **standard library** further (compared to it in 1998), providing more facilities for C++ programmers to use, with more additions planned for 2014 and 2017.

## Philosophy
Throughout C++'s life, its development and evolution has been informally governed by a set of rules that its evolution should follow:

- It must be driven by actual problems and its features should be useful immediately in real world programs.
- Every feature should be implementable (with a reasonably obvious way to do so).
- Programmers should be free to pick their own programming style, and that style should be fully supported by C++.
- Allowing a useful feature is more important than preventing every possible misuse of C++.
- It should provide facilities for organising programs into well-defined separate parts, and provide facilities for combining separately developed parts.
- No implicit violations of the type system (but allow explicit violations that have been explicitly asked for by the programmer).
- Make user created types have equal support and performance to built in types.
- Any features that you do not use you do not pay for (e.g. in performance).
- There should be no language beneath C++ (except assembly language).
- C++ should work alongside other pre-existing programming languages, rather than being part of its own separate and incompatible programming environment.
- If what the programmer wants to do is unknown, allow the programmer to specify (provide manual control).

## Standardization
Year |	C++ Standard |	Informal name
-|-|-
1998 |	ISO/IEC 14882:1998 |	C++98
2003 |	ISO/IEC 14882:2003 |	[C++03](http://en.wikipedia.org/wiki/C%2B%2B03)
2007 |	ISO/IEC TR 19768:2007 |	[C++TR1](http://en.wikipedia.org/wiki/C%2B%2B_Technical_Report_1)
2011 |	ISO/IEC 14882:2011 |	[C++11](http://en.wikipedia.org/wiki/C%2B%2B11)
2014 |	N3690 (working draft C++14) |	[C++14](http://en.wikipedia.org/wiki/C%2B%2B14)

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
The purpose of a programming language is to help **express ideas in code**. In that, a programming language performs two related tasks:

1. it provides a vehicle for the programmer to specify actions to be executed by the machine, and
2. it provides a set of concepts for the programmer to use when thinking about what can be done.

The first purpose ideally requires a language that is "close to the machine" so that all important aspects of a machine are handled simply and efficiently in a way that is reasonably obvious to the programmer. The C language was primarily designed with this in mind.

The second purpose ideally requires a language that is "close to the problem to be solved" so that the concepts of a solution can be expressed directly and concisely. The facilities added to C to create C++, such as function argument checking, const, classes, constructors and destructors, exceptions, and templates, were primarily designed with this in mind.

Thus, C++ is based on the idea of providing both:
- **direct mappings of built-in operations and types to hardware** to provide efficient memory use and efficient low-level operations, and
- **affordable and flexible abstraction mechanisms** to provide user-defined types with the same notational support, range of uses, and performance as built-in types.

The design of C++ has focused on programming techniques dealing with fundamental notions such as *memory*, *mutability*, *abstraction*, *resource management*, *expression of algorithms*, *error handling*, and *modularity*. Those are the most important concerns of a systems programmer and more generally of programmers of resource-constrained and high-performance systems.

**What you don't use you don't pay for**: a language feature and a fundamental abstraction must be designed not to waste a single byte or a single processor cycle compared to equivalent alternatives.  This is known as **the zero-overhead principle**.

### Programming styles

### Type checking

### C Compatibility

### Language, Libraries, and Systems

## Advice



# Learning C++
## The early years

## The 1998 Standard

## The 2011 Standard

## What is C++ Used for?

## Programming in C++

## Suggestions for C++ Programmers

## Suggestions for C Programmers

## Suggestions for Java Programmers

## Standard library
The C++ standard consists of two parts: the **core language** and the [C++ Standard Library](http://en.wikipedia.org/wiki/C%2B%2B_Standard_Library); which C++ programmers expect on every major implementation of C++, it includes [vectors](http://en.wikipedia.org/wiki/Sequence_container_(C%2B%2B)#Vector), **lists**, **maps**, **algorithms** (find, for_each, binary_search, random_shuffle, etc.), **sets**, **queues**, **stacks**, **arrays**, **tuples**, **input/output facilities** (iostream; reading from the console input, reading/writing from files), **smart pointers for automatic memory management**, **regular expression** support, **multi-threading** library, **atomics** support (allowing a variable to be read or written to be at most one thread at a time without any external synchronisation), **time** utilities (measurement, getting current time, etc.), a system for converting error reporting that doesn't use C++ exceptions into C++ **exceptions**, a **random number generator** and a slightly modified version of the [C standard library](http://en.wikipedia.org/wiki/C_standard_library) (to make it comply with the C++ type system).

A large part of the C++ library is based on the [STL](http://en.wikipedia.org/wiki/Standard_Template_Library). This provides useful tools as [containers](http://en.wikipedia.org/wiki/Container_(data_structure)) (for example [vectors](http://en.wikipedia.org/wiki/Array_data_structure) and *lists*), [iterators](http://en.wikipedia.org/wiki/Iterator) to provide these containers with array-like access and [algorithms](http://en.wikipedia.org/wiki/Algorithm) to perform operations such as searching and sorting. Furthermore **(multi)maps** ([associative arrays](http://en.wikipedia.org/wiki/Associative_array)) and **(multi)sets** are provided, all of which export compatible interfaces. Therefore it is possible, using templates, to write generic algorithms that work with any container or on any sequence defined by iterators. As in C, the features of the library are accessed by using the `#include` [directive](http://en.wikipedia.org/wiki/Directive_(programming)) to include a standard header. C++ provides 105 [standard headers](http://en.wikipedia.org/wiki/C%2B%2B_standard_library#Standard_headers), of which 27 are deprecated.



