[TOC]

# Overview


# Test Doubles
>When we are writing a test in which we cannot (or chose not to) use a real depended-on component (DOC), we can replace it with a Test Double. The Test Double doesn't have to behave exactly like the real DOC; it merely has to provide the same API as the real one so that the SUT thinks it is the real one!

**Limitations**: `final`, `private` and `static` methods cannot be stubbed or mocked. They are ignored by PHPUnit's test double functionality and retain their original behavior.

# Command line test runner
`phpunit` : run all tests

`phpunit --filter UnitTestClass` : run tests of UnitTestClass

`phpunit --filter UnitTestClass::testMethod` : run testMethod of UnitTestClass

`phpunit --testsuite suiteName` : run the tests of suiteName test suite



