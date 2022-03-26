# Overview

# `java.time`

- https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html

## ISO 8601

- https://en.wikipedia.org/wiki/ISO_8601

## Instant


## LocalDateTime API

- LocalDate/LocalTime
- LocalDateTime

## Zoned Date-Time API

- ZonedDateTime

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

# Optional: Null Pointer Exception

- https://stackoverflow.com/questions/23454952/uses-for-optional
- https://blogs.oracle.com/javamagazine/post/12-recipes-for-using-the-optional-class-as-its-meant-to-be-used
- https://www.oracle.com/technical-resources/articles/java/java8-optional.html
- https://www.baeldung.com/java-optional
