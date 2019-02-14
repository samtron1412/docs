[TOC]

# Overview

- It starts with a `/**`
- Then you describe the method's purpose.
- Then, for each argument, you supply a line that starts with `@param`,
  followed by the name of the variable that holds the argument. Supply a
  short explanation for each argument after the variable name.
- Supply a line that starts with `@return`, describing the return value.

The `javadoc` utility copies the first sentence to each comment to a
summary table. Therefore, it is best to write that first sentence with
some care.
- It should start with an uppercase and end with a period.
- It does not have to be a grammatically complete sentence, but it
  should be meaningful when it is pulled out of the comment and
  displayed in a summary.

```java
/**
 * Withdraws money from the bank account.
 * @param amount the amount to withdraw
 */
public void withdraw(double amount)
{
    // TODO
}

/**
 * Gets the current balance of the bank account.
 * @return the current balance
 */
public double getBalance()
{
    // TODO
}
```

>According to the standard Java documentation style, every class, every
method, every parameter, and every return value should have a comment.

# Overall Guidelines and Principles

- Using javadoc for anything that you want to comment, even it is
  private or protected. Avoid using normal comments (block or line),
  instead try to keep your code self-documenting.
- Document *What* code does as well as *why* it was developed.
    + For example, you can look at a piece of code, or class and figure
      out what it does internally. However, it may not clear what
      requirements, or other systems this class supports or, why the
      code is trapping for and throwing certain exceptions.
- Document difficult or complex functionality
- Document dependencies, if methods call other methods internally it is
  important to note that in the method description
- Document members of the Domain Object Model (real-world object) that
  your class is based on, or inspired by
- Methods that implement an interface should not provide javadoc
  comments, since the javadoc comments are included in the interface and
  will be referenced when javadoc executes.

# Terminology

API docs vs. API specs

# Source Files

Source files
-

# javadoc command

- Document one file: `javadoc MyClass.java`
- Document multiple files: `javadoc *.java`
- `javadoc` automatically provides hyperlinks to other classes and
  methods.
- You can run `javadoc` before implementing any methods.

>`javadoc` allows you to put the documentation together with your code.
That way, when you update your programs, you can see right away which
documentation needs to be updated.

# Format of a Doc Comment

format

# Block tags

## Method Documentation

Each method should include `@exception`, `@param`, `@return`,
`@deprecated` where appropriate

```java
/**
* Method to check if proscribed operation is allowed for this object.
* This method is needed to provided some level of security on operations.
*
* @param action must be an operation that has registered itself with the object
* @return boolean true if the operation is allowed, false otherwise.
* @exception UnknownOperation exception is thrown when an operation that has not
* registered with the object is passed as a parameter.
* @deprecated No longer used, SecurityAccessor class in com.iwombat.security replaces functionality
* @see com.iwombat.security
*/
public boolean operationIsAllowed(Operation action)
throws UnknownOperation
{

}
```

# References

[javadoc]: https://www.oracle.com/technetwork/java/javase/tech/index-137868.html
