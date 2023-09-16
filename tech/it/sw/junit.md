# Overview

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


## Migrate from JUnit4

- https://www.parasoft.com/blog/reaping-the-benefits-of-junit-5/
- https://www.baeldung.com/junit-5-migration
