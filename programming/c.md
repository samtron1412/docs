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
>The return type of main() must always be an int, this allows a return code to be passed to the invoker.

>Under C89, the return statement at the end of main() is required, whereas under C99 if no return statement is present, return 0 is implied. However, it is good programming practice to always use a return statement, even if you don't have to.

## Wrong practice
`void main(void)` : return type is void

When people ask why using a void is wrong, (since it seems to work), the answer is usually one of the following:

1. Because the standard says so. (To which the answer is usually of the form "but it works for me!")
2. Because the startup routines that call *main* could be assuming that the return value will be pushed onto the stack. If *main()* does not do this, then this could lead to *stack corruption* in the program's exit sequence, and cause it to *crash*. (To which the answer is usually of the form "but it works for me!")
3. Because you are likely to return a random value to the invokation environment. This is bad, because if someone wants to check whether your program failed, or to call your program from a makefile, then they won't be able to guarantee that a non-zero return code implies failure. (To which the answer is usually of the form "that's their problem").

# Compile C source code to assembly
[online](http://assembly.ynh.io/)

## GCC
`gcc -O2 -S -c foo.c -masm=intel` will leave the generated assembly code on the file `foo.s` with Intel syntax.

If you want to see the C code together with the assembly use a command line like this:

`gcc -c -g -Wa,-a,-ad -masm=intel [other GCC options] foo.c > foo.lst`

which will output the combined C and assembly listing to the file `foo.lst`

`gcc -O2 -S -masm=intel -fno-asynchronous-unwind-tables hello.c`

which will output assembly language with no macros.
