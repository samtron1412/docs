[TOC]

# Overview

# Tips and Tricks

## Render Whitespaces

- `Cmd + Shift + P` then type `Render Whitespace`

## Display a dynamically allocated array in the debugger

Yes, simple. say you have: `char *a = new char[10];`

writing in the watch window: `a,10`

would show you the content as if it were an array.
