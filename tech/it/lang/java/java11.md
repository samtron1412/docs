# Overview

- https://www.baeldung.com/java-11-new-features
- New Developer Features
    + New `String` methods
    + New `Files` methods
    + Collection to an Array
    + The `Predicate.not()`
    + Local-variable syntax `var`

# Working with Files

- Working with files in ClassPath
    + https://stackoverflow.com/questions/15713119/java-nio-file-path-for-a-classpath-resource
    + https://howtodoinjava.com/java/io/read-file-from-classpath/
- Working with files in general (disk storage)
    + https://www.marcobehler.com/guides/java-files

# Local Variable Type Inference

- `var` keyword
- Links
    + https://openjdk.java.net/projects/amber/guides/lvti-faq
    + https://medium.com/the-java-report/java-11-sneak-peek-local-variable-type-inference-var-extended-to-lambda-expression-parameters-e31e3338f1fe
- Benefits
    + It lowers the overhead of declaring a new local variable, and I
      believe this can help us avoid creating complex nested or chained
      expressions that impair readability.
    + Cleaner code

```java
// #1 - Pre Java 11
ITest op = (@NonNull SomeVeryObnioxiouslyLongClassName x, final SomeVeryObnioxiouslyLongClassName y, final SomeVeryObnioxiouslyLongClassName z,) -> .... ;

// #2 - Java 11+
ITest op = (@NonNull var x, final y, final z) -> .... ;
```
