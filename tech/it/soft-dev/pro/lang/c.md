[TOC]

# Overview

- [Intro to c for the high-level programmer](https://github.com/charles-l/intro_to_c_slideshow)

# Basic structure

A C program basically consistes of the folowing parts:
- Preprocessor commands: for example, `#include <stdio.h>`
- Functions: `printf(...)`
- Variables
- Statements and Expressions
- Comments

```c
#include <stdio.h>

int main() {
  /* my first program in C */
  printf("Hello, World! \n");

  return 0;
}
```

# Basic syntax

## Tokens

Tokens: keywords, identifiers, constants, string literals, symbols

## Semicolons

In a C program, the semicolon is a statement terminator.

## Comments

- `//`: starting inline comments
- `/* */`: block comments

## Identifiers

- A C Identifiers is a name used to identify a variable, function, or
  any other user-defined item.
- An identifier starts with a letter or an underscore followed by zero
  or more letters, underscores, and digits.
- C does not allow punctuation character such as `@, $, %` within
  identifiers.
- C is a case-sensitive programming language. Thus, `Manpower` and
  `manpower` are two different identifiers in C.

## Keywords

List of the reserved words in C. These words cannot be used as constants
or variables or any other identifier names.

| auto     | else   | long     | switch   |
| break    | enum   | register | typedef  |
| case     | extern | return   | union    |
| char     | float  | short    | unsigned |
| const    | for    | signed   | void     |
| continue | goto   | sizeof   | volatile |
| default  | if     | static   | while    |
| do       | int    | struct   | _Packed  |
| double   |        |          |          |

## Whitespace in C

- A line containing only whitespace, possibly with a comment, is known
  as a blank line, and a C compiler totally ignores it.
- Whitespace is the term used in C to describe blanks, tabs, newline
  characters and comments.

# Data types

Data types in C refer to an extensive system used for declaring
variables or functions of different types. The type of a variable
determines how much space it occupies in storage and how the bit pattern
stored is interpreted.

| Type            | Description                                                                                                                                        |
| -                | -                                                                                                                                                  |
| Basic Types      | They are arithmetic types and are further classified into: (a) integer types and (b) floating-point types                                          |
| Enumerated types | They are again arithmetic types and they are used to define variables that can only assign certain discrete integer values throughout the program. |
| The type void    | The type specifier void indicates that no value is available                                                                                       |
| Derived types    | They include (a) Pointer types, (b) Array types, (c) Structure types, (d) Union types and (e) Function types.                                      |

## Basic Types

### Integer Types

| Type           | Storage sizes | Value range                                          |
| -              | -             | -                                                    |
| char           | 1 byte        | -128 to 127 or 0 to 255                              |
| unsigned char  | 1 byte        | 0 to 255                                             |
| signed char    | 1 byte        | -128 to 127                                          |
| int            | 2 or 4 bytes  | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647 |
| unsigned int   | 2 or 4 bytes  | 0 to 65,535 or 0 to 4,294,967,295                    |
| short          | 2 bytes       | -32,768 to 32,767                                    |
| unsigned short | 2 bytes       | 0 to 65,535                                          |
| long           | 4 bytes       | -2,147,483,648 to 2,147,483,647                      |
| unsigned long  | 4 bytes       | 0 to 4,294,967,295                                   |

To get the exact size of a type or a variable on a particular platform,
you can use the **sizeof** operator. The expressions **sizeof(type)**
yields the storage size of the object or type in bytes.

```c
#include <stdio.h>
#include <limits.h>

int main() {
  printf("Storage size for int: %d \n", sizeof(int));
  return 0;
}
```

### Floating-Point Types

| Type        | Storage size | Value range          | Precision         |
| -           | -            | -                    | -                 |
| float       | 4 bytes      | 1.2E-38 to 3.4E+38   | 6 decimal places  |
| double      | 8 bytes      | 2.3E-308 to 1.7E+308 | 15 decimal places |
| long double | 10 bytes     |                      |                   |

# Function

[ref](http://users.aber.ac.uk/auj/voidmain.cgi)

## Other function

`void func(void)` : return nothing and zero arg

`void func()` : return nothing and accept arbitrary args

`int func(void)` : return value int type, zero arg

`int func()` : return value int type, arbitrary args

## main function

always have return int

`int main(int argc, char* argv[])`

`int main(void)` : do not require access to the command line arguments.
>The return type of main() must always be an int, this allows a return
code to be passed to the invoker.

>Under C89, the return statement at the end of main() is required,
>whereas under C99 if no return statement is present, return 0 is
>implied. However, it is good programming practice to always use a
>return statement, even if you don't have to.

## Wrong practice

`void main(void)` : return type is void

When people ask why using a void is wrong, (since it seems to work), the
answer is usually one of the following:

1. Because the standard says so. (To which the answer is usually of the
   form "but it works for me!")
2. Because the startup routines that call *main* could be assuming that
   the return value will be pushed onto the stack. If *main()* does not
   do this, then this could lead to *stack corruption* in the program's
   exit sequence, and cause it to *crash*. (To which the answer is
   usually of the form "but it works for me!")
3. Because you are likely to return a random value to the invokation
   environment. This is bad, because if someone wants to check whether
   your program failed, or to call your program from a makefile, then
   they won't be able to guarantee that a non-zero return code implies
   failure. (To which the answer is usually of the form "that's their
   problem").

# Compile C source code to assembly

[online](http://assembly.ynh.io/)

## GCC

`gcc -O2 -S -c foo.c -masm=intel` will leave the generated assembly code
on the file `foo.s` with Intel syntax.

If you want to see the C code together with the assembly use a command
line like this:

`gcc -c -g -Wa,-a,-ad -masm=intel [other GCC options] foo.c > foo.lst`

which will output the combined C and assembly listing to the file
`foo.lst`

`gcc -O2 -S -masm=intel -fno-asynchronous-unwind-tables hello.c`

which will output assembly language with no macros.
