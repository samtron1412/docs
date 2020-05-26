[TOC]

# Overview

In computer programming, a data type or simply type is a classification
of data which tells the compiler or interpreter how the programmer
intends to use the data.

# Classes of data types

## Primitive data types

### Machine data types

- All data in computers based on digital electronics is represented as
  bits (alternatives 0 and 1) on the lowest level.
    + The smallest addressable unit of data is usually a group of bits
      called a byte (8 bits).
    + This unit processed by machine code instructions is called a word
      (32-64 bits).

### Boolean type

- The Boolean type represents the values true and false.
    + Although only two values are possible, they are rarely implemented
      as a single binary digit for efficiency reasons.
    + Many programming languages do not have an explicit Boolean type,
      instead interpreting 0 as false and other values as true.

### Numeric types

- Integer data types, or "whole numbers."
- Floating point data types, usually represent values as high-precision
fractional values (rational numbers mathematically), but are sometimes
misleadingly called reals (evocative of mathematical real numbers).
- Fixed point data types are convenient for representing monetary
values. They are often implemented internally as integers.

## Composite types

Composite types are derived from more than one primitive type. The ways
they are combined are called data structures.

- Bignum or arbitrary precision numeric types lack predefined limits.
- An array stores a number of elements of the same type in a specific
  order.
- A list
- Record (struct)
- Union
    + Tagged union
- A set is an abstract data type that can store certain values, without
  any particular order, and no repeated values.
- An object contains a number of data fields, like a record, and also a
  number of subroutines for accessing or modifying them, called methods.

### Enumerations

An enumerated type is a data type consisting of a set of named values
called elements, members or enumerators of the type. The enumerator
names are usually identifiers that behave as constants in the language.

### String and text types

Character and string types can store sequences of characters from a
character set such as ASCII.

## Other types

### Pointers and references

A pointer refer directly to another value stored elsewhere in the
computer memory using its address.
    + Pointers are often stored in a format similar to an integer;
      however, attempting to dereference or look up a pointer whose
      value was never a valid memory address would cause a program to
      crash.

### Function types

A function type (or arrow type or exponential) is the type of a variable
or parameter to which a function has or can be assigned, or an argument
or result type of a higher-order function taking or returning a
function.

## Abstract data types (ADT)

An abstract data type (ADT) is a theoretical concept in computer
science used in the design and analysis of algorithms, data structures,
and software systems, and do not correspond to specific features of
programming languages.

An ADT is a mathematical model for data types, where a data type is
defined by its behavior (semantics) from the point of view of a user of
the data:
    + specifically in terms of possible values,
    + possible operations on data of this type, and
    + the behavior of these operations.

This contrasts with data structures, which are concrete representations
of data, and are the point of view of an implementer, not a user.
    + Any data type that does not specify an implementation is an
      abstract data type.

Formally, an ADT may be defined as a "class of objects whose logical
behavior is defined by a set of values and a set of operations" without
the details of how the data type is implemented; this is analogous to an
algebraic structure in mathematics.

Examples include:
- A queue is a first-in first-out list.
    + Deque
    + Priority queue
- A set can store certain values, without any particular order, and with
no repeated values.
- A stack is a last-in, first-out data structure.
- A tree is a hierarchical structure.
- A graph
- A hash, dictionary, map or associate array is a more flexible
variation on a record, in which name-value pairs can be added and
deleted freely.
- A smart pointer is the abstract counterpart of a pointer.

## Utility types

For convenience, high-level languages may supply ready-made "real world"
data types, for instance times, dates and monetary values, and memory,
even where the language allows them to be built from primitive types.

# Abstract Data Type (ADT)


# Data Structure

A data structure is a particular way of organizing data in a computer so
that it can be used efficiently.

