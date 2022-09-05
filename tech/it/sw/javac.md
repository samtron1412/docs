# Overview

- Java compiler
- Java 11
    + https://docs.oracle.com/en/java/javase/11/tools/javac.html#GUID-AEEC9F07-CB49-4E96-8BC7-BCC2C7F725C9

# Linting

- `Xlint`
- `@SuppressWarning`
    + https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html
    + `@SuppreWarning("unchecked")`
    + `@SuppreWarning({"unchecked", "deprecated"})`
    + Only use this in the deepest level / element. If you want to
      suppress the warning for a method, then use it on that method, not
      the class.
