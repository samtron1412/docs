[TOC]

# Overview

Something

# Core

- Future and promises
    + https://docs.scala-lang.org/overviews/core/futures.html

# Basics

## Variables

- Define immutable value: `val name = "Son"`
    + Evaluate the right side to a value
    + Assign the value to the label
- Define mutable value: `var name = "Son"`
    + Evaluate the right side to a value
    + Assign the value to the label
- Assign a label to an immutable value whose evaluation is deferred for
  a later time: `def im_value = <label of immutable/mutable value>`
    + `def alias = name`
    + Similar like pointer

## Control flow

- if (cond) {} else {}
- while (cond) {}

## Collections

- The spirit of functional programming: immutable collections
    + `scala.collection.immutable`
    + import automatically
- Mutable collection: `scala.collection.mutable`
    + Need to explicitly import

### List (immutable)

- Create
    + `val names = List("Son", "Ryan")`
    + `val names = "Son" :: "Ryan" :: Nil`
- Access
    + names(0) => Son
    + names.head => the first element
    + names.tail => the rest of the list

### Set (immutable)

- Create
    + `val uniqueNames = Set("Son", "Ryan")`

# Tips and Tricks

## Operators

### `:`

- It is used for type ascription
    + forcing the compiler to see a value as some particular type

```scala
val b = 1: Byte
val f = 1: Float
```

### `:::` vs `++`

- `:::`: concatenation of two lists
    + `list1 ::: list2`
    + `1 :: 2 :: Nil` => a list
    + faster than `::` and type safe, only concatenate lists not other
      types
- `++`: to concatenate any two collections, even iterators

## Variable arguments (can be zero, one, or more arguments - varargs)

- the asterisk notation is used for declaring a varargs parameter
- `_*`: a variable of any type that subclasses `Seq[T]`

```scala
//varargs parameter, use as Array[String]
def f(args: String*) = ...
val list = List("a", "b", "c")
f(list: _*)
```


## Zip and zipWithIndex

- https://alvinalexander.com/scala/scala-zip-zipwithindex-stream-examples

## Scala fold, foldLeft, foldRight

- https://coderwall.com/p/4l73-a/scala-fold-foldleft-and-foldright

# References

[tour]: https://docs.scala-lang.org/tour/tour-of-scala.html
[docs]: https://docs.scala-lang.org/overviews/index.html
[api]: https://www.scala-lang.org/api/2.12.6/index.html
[specs]: https://scala-lang.org/files/archive/spec/2.12/
[cheatsheet]: https://docs.scala-lang.org/cheatsheets/index.html
[style]: https://docs.scala-lang.org/style/index.html
[faq]: https://docs.scala-lang.org/tutorials/FAQ/index.html
[scala-java]: https://docs.scala-lang.org/tutorials/scala-for-java-programmers.html
