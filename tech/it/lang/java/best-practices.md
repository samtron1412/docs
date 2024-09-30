# Overview

# Common Misconception

## `final` modifier

### It is a best practice to make method arguments final as it will help in writing immutable/safe code

- It's a matter of taste rather than a best practice due to:
    + If the passing object is not immutable, we still can mutate it.
        * The `final` modifier only prevent us to reassign the passing
          parameter to a new value.
        * The references are passed to the method by value, and due to
          block scoping, reassigning passing parameter does not reassign
          the outer scope references.
    + Safe or correct code only can be guaranteed with high quality unit
      tests

### Adding final keyword on method parameters and local variable results in performance gains

- The performance gains only if the local variables are static
  constants.
    + If the variables are getting from a different source (database,
      API calls) then the compiler does not optimize it.

### But this is a widely accepted best practice to make parameters and local variables final.


- Code in Spring, Google Guava, JDK, and other industry standard
  libraries and projects do not use `final` for all local variables.
