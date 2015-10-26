# 1. Testing terminology

## 1.1. Unit tests and unit testing

A unit test is a piece of code written by a developer that executes a specific functionality in the code to be tested. The percentage of code which is tested by unit tests is typically called **test coverage**.

A unit test targets a small unit of code, e.g., **a method or a class**, (local tests).

Unit tests ensure that code works as intended. They are also very helpful to ensure that the code still works as intended in case you need to modify code for fixing a bug or extending functionality. Having a high test coverage of your code allows you to continue developing features without having to perform lots of manual tests.

## 1.2. Test fixture

The test fixture is **a fixed state of the software under test used as a baseline for running tests**.

Often use setUp() and tearDown() functions or beforeTest() and afterTest() functions or some similar method to prepare a state to test.

## 1.3. Functional and integration tests

An integration test has the target to **test the behavior of a component or the integration between a set of components**. The term functional test is sometimes used as synonym for integration test.

This kind of tests allow you to translate your user stories into a test suite, i.e., the test would resemble an expected **user interaction with the application**.

## 1.4. Performance tests

Performance tests are used to benchmark software components in a repeatable way.

## 1.5. Behavior vs. state testing

A test is an behavior test (also called interaction test) if it does not validate the result of a method call, but checks if **certain methods were called with the correct input parameters**.

State testing is about **validating the result**, while behavior testing is about testing the behavior of the application under test.

If you are testing algorithms or system functionality, you want to test in most cases state and not interactions. A typical test setup uses mocks or stubs of related classes to abstract the interactions with these other classes away and tests state in the object which is tested.

## Mocking
Simulate a real object and behavior of objects and verifies expectations.

## Stub
Is a simply dummy set of data that can be passed around to meet criteria.

# 2. Test organization

## 2.1. Test organization for Java projects

Typically unit tests are created in a separate project or separate source folder to avoid that the normal code and the test code is mixed.

## 2.2. What should you test?

What should be tested is a hot topic for discussion. Some developers believe every statement in your code should be tested.

In general it is safe to **ignore trivial code** as, for example, getter and setter methods which simply assign values to fields. Writing tests for these statements is time consuming and pointless, as you would be testing the Java virtual machine. The JVM itself already has test cases for this and you are safe to assume that field assignment works in Java if you are developing end user applications.

You should write software tests in any case for **the critical and complex parts of your application**. A solid test suite also protects you against **regression** in existing code if you introduce new features.

## 2.3. Introducing tests in legacy code

If you start developing tests for an existing code base without any tests, it is good practice to start writing tests for the parts of the application in which **most errors happened in the past**. This way you can focus on **the critical parts of your application**.


# 3. When use which test technique ?
| Goal                                                                                   | Strongest technique                                                                |
| -                                                                                      | -                                                                                  |
| **Finding bugs** (things that don't work as you want them to)                              | **Manual testing** (sometimes also automated integration tests)                        |
| **Detecting regressions** (things that used to work but have unexpectedly stopped working) | **Automated integration tests** (sometimes also manual testing, though time-consuming) |
| **Designing software components** robustly                                                 | **Unit testing** (within the TDD process)                                              |

(**Note**: there's one exception where unit tests do effectively detect bugs. It's when you're refactoring, i.e., restructuring a unit's code but without meaning to change its behavior has changed.)



# 4. Best Practices
## 4.1 Unit Tests
- [Writing Great Unit Tests: Best and Worst Practices](http://blog.stevensanderson.com/2009/08/24/writing-great-unit-tests-best-and-worst-practises/)