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

# Monad - Monadic Java

- https://www.slideshare.net/mariofusco/monadic-java
- https://dzone.com/articles/what-is-a-monad-basic-theory-for-a-java-developer
- https://www.baeldung.com/java-monads
- https://medium.com/@afcastano/monads-for-java-developers-part-1-the-optional-monad-aa6e797b8a6e

# Concurrency (Concurrent)

- Concurrency vs.  Parallelism
    + https://jenkov.com/tutorials/java-concurrency/concurrency-vs-parallelism.html
- Concurrency Models
    + https://jenkov.com/tutorials/java-concurrency/concurrency-models.html
- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html
    + https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/package-summary.html
    + https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/package-summary.html
- Main ideas
    + There is a thread pool
        * Default thread pool = number of processors - 1.
        * Can create custom thread pools as well.
    + There are tasks that we want to execute and get back the results.
    + There is an executor that executes tasks.
- Fork-join framework
    + https://en.wikipedia.org/wiki/Work_stealing
    + https://www.baeldung.com/java-fork-join
    + https://stackoverflow.com/questions/7926864/how-is-the-fork-join-framework-better-than-a-thread-pool
    + https://www.youtube.com/watch?v=5wgZYyvIVJk
    + Common queue for external submission (main thread)
        + Each thread has its own queue to contain its original work as
          well as generated work (recursive tasks) from its tasks.
    + Use work-stealing algorithm
        + Idle threads steal work from busy threads: busy threads pick
          tasks from the top of the queue, idle threads pick tasks from
          the bottom of the queue.
- Parallel stream
    + https://www.baeldung.com/java-when-to-use-parallel-stream
    + Not always parallel processing is faster than sequential
      processing due to cost of splitting and merging the results.
    + NQ model: N (number of elements to process) * Q (the amount of
      computation performed per element), the larger N x Q, the more
      likely that we gain performance from parallel procesing.
    + Customer thread pool
        * https://stackoverflow.com/questions/21163108/custom-thread-pool-in-java-8-parallel-stream
- CompletableFuture
    + https://www.youtube.com/watch?v=-MBPQ7NIL_Y
- Structured Concurrency
    + https://openjdk.org/jeps/428

## Thread Safe and Multi-threaded Programming

- https://docs.oracle.com/javase/specs/jls/se8/html/jls-17.html
- https://www.baeldung.com/java-thread-safety
- Synchronization: a mechanism for communicating between threads
    + Implementation
        * Each object has an associated monitor which a thread can lock
          or unlock.
        * Only one thread at a time can hold a lock on a monitor.
        * A thread t may lock a particular monitor multiple times; each
          unlock reverses the effect of one lock operation.
    + A `synchronized` statement
        * https://docs.oracle.com/javase/specs/jls/se8/html/jls-14.html#jls-14.19
    + A `synchronized` method
        * https://docs.oracle.com/javase/specs/jls/se8/html/jls-8.html#jls-8.4.3.6
    + The Java programming language neither prevents nor requires
      detection of deadlock conditions.
        * You have to build your own high-level entities to prevent
          deadlocks.
- Other mechanism for communicating between threads
    + `volatile` variables
        * https://docs.oracle.com/javase/specs/jls/se8/html/jls-8.html#jls-8.3.1.4
        * https://jenkov.com/tutorials/java-concurrency/volatile.html
        * https://www.baeldung.com/java-volatile
        * https://ioflood.com/blog/java-volatile
        * field modifier, the Java Memory Model ensures that all threads
          see a consistent value for the variable by reading the value
          from main memory (heap) instead of Thread's local cache.
        * `volatile` and `synchronized` keywords
            - https://stackoverflow.com/questions/3519664/difference-between-volatile-and-synchronized-in-java
    + `java.util.concurrent` pacakges: ThreadLocal, etc.
- Wait Sets and Notification
    + https://docs.oracle.com/javase/specs/jls/se8/html/jls-17.html#jls-17.2
    + Every object, in addition to having an associated monitor, has an
      associated wait set. A wait set is a set of threads.
- Java programming language memory model (for shared variables)
    + https://docs.oracle.com/javase/specs/jls/se8/html/jls-17.html#jls-17.4
    + https://en.wikipedia.org/wiki/Java_memory_model
    + Implementation
        * https://jenkov.com/tutorials/java-concurrency/java-memory-model.html
        * https://www.digitalocean.com/community/tutorials/java-jvm-memory-model-memory-management-in-java
    + A memory model describes, given a program and an execution trace
      of that program, whether the execution trace is a legal execution
      of the program.
        * The Java programming language memory model works by examining
          each read in an execution trace and checking that the write
          observed by that read is valid according to certain rules.
    + The memory model describes possible behaviors of a program.
    + Shared variables
        * https://jenkov.com/tutorials/java-concurrency/thread-safety.html
        * Memory that can be shared between threads is called shared
          memory or heap memory.
        * All instance fields, static fields, and array elements are
          stored in heap memory.
        * Local variables (§14.4), formal method parameters (§8.4.1),
          and exception handler parameters (§14.20) are never shared
          between threads and are unaffected by the memory model.
            - However, local variables can point to objects on heap
              which are can be shared between threads.
        * Two accesses to (reads of or writes to) the same variable are
          said to be conflicting if at least one of the accesses is a
          write.
    + Happenned-before guarantee
        * https://en.wikipedia.org/wiki/Happened-before
        * https://jenkov.com/tutorials/java-concurrency/java-happens-before-guarantee.html

### java.util.concurrent

- ThreadLocal
    + https://docs.oracle.com/javase/8/docs/api/java/lang/ThreadLocal.html
    + https://www.baeldung.com/java-threadlocal
    + https://jenkov.com/tutorials/java-concurrency/threadlocal.html
    + Each thread has a local variable that only that thread can get and
      set.
    + https://stackoverflow.com/questions/817856/when-and-how-should-i-use-a-threadlocal-variable
    + Can potentially create memory leaks if forget to close/remove it.

# Java Language (java.lang)

- APIs
    + https://docs.oracle.com/javase/8/docs/api/java/lang/package-summary.html
    + Annotation: https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/package-summary.html
    + Reflection: https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/package-summary.html
    + Garbage collector: https://docs.oracle.com/javase/8/docs/api/java/lang/ref/package-summary.html
    + JVM/JRE management: https://docs.oracle.com/javase/8/docs/api/java/lang/management/package-summary.html
    + Dynamic language support: https://docs.oracle.com/javase/8/docs/api/java/lang/invoke/package-summary.html
    + Instrument programs running on the JVM: https://docs.oracle.com/javase/8/docs/api/java/lang/instrument/package-summary.html

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
