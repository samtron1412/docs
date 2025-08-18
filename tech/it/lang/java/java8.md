# Overview

- APIs
    + https://docs.oracle.com/javase/8/docs/api/

# Input and Output (IO)

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/io/package-summary.html
    + https://docs.oracle.com/javase/8/docs/api/java/nio/package-summary.html

# Math

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/math/package-summary.html

# Stream

- https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/package-summary.html
- Stream: an abstraction concept that differs from collections in
  several ways
    + No storage
        * A stream is not a data structure that stores elements;
          instead, it conveys elements from a source such as a data
          structure, an array, a generator function, or an I/O channel,
          through a pipeline of computational operations.
    + Functional in nature
        * An operation on a stream produces a result, but does not
          modify its source
    + Laziness-seeking
        * Stream operations are divided into intermediate
          (Stream-producing) and terminal (value- or
          side-effect-producing) operations.
        * Intermediate operations are always lazy.
    + Possibly unbounded
    + Consumable: elements of a stream are only visited once during the
      life of a stream.
        * Like an Iterator, a new stream must be generated to revisit
          the same elements of the source.

- map vs flatMap
    + https://stackoverflow.com/questions/26684562/whats-the-difference-between-map-and-flatmap-methods-in-java-8
    + map can produce `Stream<Stream<Item>>`
    + flatMap can produce `Stream<Item>`
- Exception handling in streams
    + https://dzone.com/articles/exception-handling-in-java-streams
    + Wrap exceptions in RuntimeException or Unchecked Exception
        * Stop processing the stream right away
    + `Either` or `Try` types
        * Continue processing the stream but store the Exception and the
          original value that causes the exception
    + Throw Checked Exceptions
        * https://javadevcentral.com/throw-checked-exceptions-in-java-streams
        * https://stackoverflow.com/questions/27644361
- Non-static method reference in stream
    + https://stackoverflow.com/questions/32619125/method-reference-cannot-make-a-static-reference-to-the-non-static-method
    + https://stackoverflow.com/questions/26168806/java-8-method-reference-to-non-static-method
    + Using `this::<non-static-method>` if want to use non-static method
      reference in the class.
    + You can use `<ClassInStream>::<non-static-method>`
    + Or `new MyClass()::<non-static-method>`

```java
//
var keyList = stringToSetMap.entrySet().stream()
        .map(Map.Entry::getKey) // Stream<Map.Entry>, the items in stream have the non-static getKey method
        .collect(toList());

```

- try-with-resources
    + https://stackoverflow.com/questions/25796118/java-8-streams-and-try-with-resources
    + Only streams whose source is an IO channel (Files.lines(), API,
      etc.) will require closing.
    + Streams are backed by collections, arrays, or generating functions
      do not required to be closed.

## Filter null from the stream

```java
Stream<String> language = Stream.of("java", "python", "node", null, "ruby", null, "php");
List<String> result = language.filter(x -> x!=null).collect(Collectors.toList());

// or
List<String> result = language.filter(Objects::nonNull).collect(Collectors.toList());
```

## Split stream into multiple streams

- https://www.baeldung.com/java-split-stream

# java.time

- https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html

## ISO 8601

- https://en.wikipedia.org/wiki/ISO_8601
- `2023-05-24T08:35:43Z`

## Instant


## LocalDate and LocalDateTime API

- LocalDate
- LocalTime
- LocalDateTime
    + `2007-12-03T10:15:30`

## OffsetDateTime

- OffsetTime
- OffsetDateTime
    + `2007-12-03T10:15:30+01:00`

## Zoned Date-Time API

- ZonedDateTime
    + `2007-12-03T10:15:30+01:00 Europe/Paris`

## Chrono Units Enum

- ChronoUnit
    + WEEKS, MONTHS, YEARS, ...

## Period and Duration

- Period
    + Date based amount of time
- Duration
    + Time based amount of time

## Temporal Adjusters

- Performs date mathematics
    + get the "second Saturday of the month"
    + get the next Tuesday


# Functional Programming

## Functional interfaces

- https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html
- https://docs.oracle.com/javase/8/docs/api/java/lang/FunctionalInterface.html

## Consumer interface

- https://aws.amazon.com/blogs/developer/consumer-builders-in-the-aws-sdk-for-java-v2/
- https://mkyong.com/java8/java-8-consumer-examples/
- https://dkbalachandar.wordpress.com/2017/08/31/java-8-builder-pattern-with-consumer-interface/

## Method references

- https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html
- https://www.devmedium.com/java-lambda-method-reference-and-local-variable/
- https://www.baeldung.com/java-method-references
- Negate a method reference
    + https://stackoverflow.com/questions/21488056/how-to-negate-a-method-reference-predicate

# Lambda Expressions

- Syntax
    + `parameter -> expression body`
    + *optional type declaration*: no need to declare the type of a
      parameter. The compiler can inference the same from the value of
      the parameter
    + *optional parenthesis around parameter*: for multiple parameters,
      parentheses are required
    + *optional curly braces*: no need to use curly braces in expression
      body if the body contains a single statement
    + *optional return keyword*: the compiler automatically returns the
      value if the body has a single expression to return the value
- Local variables used in Lambdas have to be final or `effectively final`
    + https://www.baeldung.com/java-lambda-effectively-final-local-variables
    + Effectively final
        * Static or Instance variables (on heap)
        * Non-final variables that are not changing.

# Optional: Null Pointer Exception

- Origin: it allows a method to return `Optional<T>`, i.e., it can
  return an object type T or nothing or null.
- https://nipafx.dev/design-java-optional/
- https://stackoverflow.com/questions/23454952/uses-for-optional
- https://www.oracle.com/technical-resources/articles/java/java8-optional.html
- https://www.baeldung.com/java-optional
- `map` method is broken for Optional
    + https://blog.developer.atlassian.com/optional-broken/
- Use optional to reveal intention
    + https://nipafx.dev/intention-revealing-code-java-8-optional/
- Guava's Optional vs. JDK Optional
    + https://medium.com/@edouard.kaiser/optional-guava-and-java-8-9d6e7d6147b0
- Good practices
    + https://forums.oracle.com/ords/apexds/post/optionals-patterns-and-good-practices-2540

# Monad - Monadic Java

- https://www.slideshare.net/mariofusco/monadic-java
- https://dzone.com/articles/what-is-a-monad-basic-theory-for-a-java-developer
- https://www.baeldung.com/java-monads
- https://medium.com/@afcastano/monads-for-java-developers-part-1-the-optional-monad-aa6e797b8a6e

# Networking Application (java.net)

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/net/package-summary.html

# Remote Method Invocation (RMI)

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/net/package-summary.html

# Security and Crypto (Certificates, etc.)

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/security/package-summary.html
    + https://docs.oracle.com/javase/8/docs/api/javax/crypto/package-summary.html

# SQL

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/sql/package-summary.html

# Text

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/text/package-summary.html
