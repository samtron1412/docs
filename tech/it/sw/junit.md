# Overview

- https://howtodoinjava.com/series/junit/
- Creating a new test class for each `@Test` to isolate tests.

# JUnit 5

- Links
    + https://junit.org/junit5/docs/current/user-guide
    + https://www.baeldung.com/junit-5
    + https://www.baeldung.com/junit-assertions
- Parameterized tests
    + https://www.baeldung.com/parameterized-tests-junit-5
- `@TestInstance` annotation to manage class lifecycle
    + https://www.baeldung.com/junit-testinstance-annotation
    + https://stackoverflow.com/questions/52551718/what-use-is-testinstance-annotation-in-junit-5
- Repeated tests:
    + https://junit.org/junit5/docs/current/user-guide/#writing-tests-repeated-tests
- Parallel execution
    + https://junit.org/junit5/docs/current/user-guide/#writing-tests-parallel-execution
    + If tests use Lifecycle.PER_CLASS mode or a MethodOrderer, then we
      need to explicitly add `@Execution(CONCURRENT)`.
    + https://www.baeldung.com/junit-5-parallel-tests
        * `@ResourceLock(value = "resources")`

## Annotations

- https://www.softwaretestinghelp.com/junit-annotations-tutorial/


## Migrate from JUnit4

- https://www.parasoft.com/blog/reaping-the-benefits-of-junit-5/
- https://www.baeldung.com/junit-5-migration

# Tips and Tricks

## When to use @RunWith and when @ExtendWith

- https://stackoverflow.com/questions/55276555/when-to-use-runwith-and-when-extendwith
