[TOC]

# Overview

Something

# Core

- Future and promises
    + https://docs.scala-lang.org/overviews/core/futures.html

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
