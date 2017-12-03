[TOC]

# Overview

Java is a general-purpose computer programming language that is
**concurrent**, **class- based**, **object-oriented**, and specifically
designed to have *as few implementation dependencies as possible*.
- It is intended to let application developers "**write once, run
  anywhere**" (WORA), meaning that code that runs on one platform does
  not need to be recompiled to run on another.
- Java applications are typically compiled to bytecode (class file) that
  can run on any Java Virtual Machine (JVM) regardless of computer
  architecture.

## History

James Gosling, Mike Sheridan, and Patrick Naughton initiated the Java
language project in June 1991.
- Java was originally designed for interactive television, but it was
  too advanced for the digital cable television industry at the time.
- The language was initially called Oak after an oak tree that stood
  outside Gosling's office.
- Later the project went by the name Green and was finally renamed Java,
  from Java coffee.
- Gosling designed Java with a C/C++ style syntax that system and
  application programmers would find familiar

Released in 1995, implement by C and C++. The original and reference
implementation Java **compilers**, **virtual machines**, and class
libraries were developed by Sun.
- Major web browsers soon incorporated the ability to run Java applets
  within web pages, and Java quickly became popular.
- Java 2 had multiple configurations built for different types of
  platforms
    + J2EE included technologies and APIs for enterprise applications
      typically run in server environments.
    + J2ME featured APIs optimized for mobile applications.
    + J2SE is the desktop version.
    + In 2006, J2 versions renamed as Java EE, Java ME, and Java SE.
- As of May 2007, in compliance with the specifications of the [Java
  Community Process](https://www.jcp.org), Sun relicensed most of its
  Java technologies under the GNU General Public License.
- On April 2, 2010, James Gosling resigned from Oracle.
- In January 2016, Oracle announced that Java runtime environments based
  on JDK 9 will discontinue the browser plugin.

### Versions

- JDK 1.0 (January 21, 1996)
- JDK 1.1 (February 19, 1997)
- J2SE 1.2 (December 8, 1998)
- J2SE 1.3 (May 8, 2000)
- J2SE 1.4 (February 6, 2002)
- J2SE 5.0 (September 30, 2004)
- Java SE 6 (December 11, 2006)
- Java SE 7 (July 28, 2011)
- Java SE 8 (March 18, 2014)

## Principles

There were five primary goals in the creation of the Java language:

1. It should be "**simple, object-oriented and familiar**"
2. It should be "**robust and secure**"
3. It should be "**architecture-neutral and portable**"
4. It should execute with "**high performance**"
5. It should be "**interpreted, threaded, and dynamic**"

## Community

### [Java Community](https://www.java.net/)

Java.net is a large community of Java developers and their projects. We
welcome anyone interested in Java, related **JVM** technologies, and
education to our discussions and projects.

### Java Community Process ([JCP](https://www.jcp.org))

The JCP is the mechanism for developing standard technical
specifications for Java technology.


# Practices

## Documentation

Using javadoc utility:
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

### javadoc utility

- Document one file: `javadoc MyClass.java`
- Document multiple files: `javadoc *.java`
- `javadoc` automatically provides hyperlinks to other classes and
  methods.
- You can run `javadoc` before implementing any methods.

>`javadoc` allows you to put the documentation together with your code.
That way, when you update your programs, you can see right away which
documentation needs to be updated.

## Unit Testing

A unit test verifies that a class works correctly in isolation, outside
a complete program.

A tester class is a class with a main method that contains statements to
run methods of another class.
- Construct one or more objects of the class that is being tested.
- Invoke one or more methods.
- Print out one or more results.
- Print the expected results.

## [Platform](http://docs.oracle.com/javase/8/docs/index.html)

One characteristic of Java is **portability**, which means that computer
programs written in the Java language must run similarly on any hardware
/operating-system platform. This is achieved by compiling the Java
language code to an intermediate representation called *Java bytecode*,
instead of directly to platform-specific machine code. Java bytecode
instructions are analogous to machine code, but they are intended to be
interpreted by a virtual machine (VM) written specifically for the host
hardware. End-users commonly use a *Java Runtime Environment* (JRE)
installed on their own machine for standalone Java applications, or in a
web browser for Java *applets*.

**Standardized libraries** provide a generic way to access host-specific
features such as *graphics*, *threading*, and *networking*.

The **Java platform** is the name for *a bundle of related programs*
from Sun that *allow for developing and running programs written in the
Java programming language*. The platform is not specific to any one
processor or operating system, but rather *an execution engine* (called
a virtual machine) and *a compiler* with *a set of libraries* that are
implemented for various hardware and operating systems so that Java
programs can run identically on all of them. Each platform have:

- Java compiler: Java source code -> Java bytecode
- Java Runtime Environment (JRE - Java Virtual Machine): Java bytecode -> machine code
- The libraries (API)

Main platforms:

- [Java Card](http://en.wikipedia.org/wiki/Java_Card): A technology that
  allows small Java-based applications (*applets*) to be run securely on
  smart cards and similar small-memory devices.
- [Java ME](http://www.oracle.com/technetwork/java/javame/index.html)
  (Micro Edition): Specifies several different sets of libraries (known
  as profiles) for devices with limited storage, display, and power
  capacities. Often used to develop applications for *mobile devices,
  PDAs, TV set-top boxes, and printers*.
- [Java SE](http://www.oracle.com/technetwork/java/javase/index.html)
  (Standard Edition): For *general-purpose* use on desktop PCs, servers
  and similar devices.
- [Java EE](http://www.oracle.com/technetwork/java/javaee/index.html)
  (Enterprise Edition): Java SE plus various APIs useful for *multi-tier
  client–server enterprise applications*.

### Implementations

[Oracle Corporation](http://en.wikipedia.org/wiki/Oracle_Corporation) is
the current owner of the official implementation of the Java SE
platform, following their acquisition of [Sun
Microsystems](http://en.wikipedia.org/wiki/Sun_Microsystems) on January
27, 2010.

Because Java lacks any formal standardization recognized by *Ecma
International, ISO/IEC, ANSI, or other third-party standards
organization*, the Oracle implementation is the [de facto
standard](http://en.wikipedia.org/wiki/De_facto_standard).

The Oracle implementation is packaged into two different distributions:

- **The Java Runtime Environment** (JRE) which contains the parts of the
  Java SE platform required to run Java programs and is intended for
  end-users.
- **The Java Development Kit** (JDK), which is intended for software
  developers and includes development tools such as the [Java
  compiler](http://en.wikipedia.org/wiki/Java_compiler),
  [Javadoc](http://en.wikipedia.org/wiki/Javadoc),
  [Jar](http://en.wikipedia.org/wiki/JAR_(file_format)), and a
  **debugger**.

[OpenJDK](http://en.wikipedia.org/wiki/OpenJDK) is another notable Java
SE implementation that is licensed under the GPL. The implementation
started when Sun began releasing the Java source code under the GPL. As
of Java SE 7, OpenJDK is the official Java reference implementation.

### Performance

Programs written in Java have a reputation for being slower and
requiring more memory than those written in C++. However, Java programs'
execution speed improved significantly with the introduction of Just-in-
time compilation in 1997/1998 for Java 1.1

Some platforms offer direct hardware support for Java; there are
microcontrollers that can run Java in hardware instead of a software
Java virtual machine, and ARM based processors can have hardware support
for executing Java bytecode through their
[Jazelle](http://en.wikipedia.org/wiki/Jazelle) option.

### Java Bytecode

Java bytecode is the [instruction
set](http://en.wikipedia.org/wiki/Instruction_set) of the [Java virtual
machine](http://en.wikipedia.org/wiki/Java_virtual_machine).

Each bytecode is composed by one, or in some cases two, bytes that
represent the instruction
([opcode](http://en.wikipedia.org/wiki/Opcode)), along with zero or more
bytes for passing parameters. Of the 256 possible byte-long opcodes, 198
are currently in use, 51 are reserved for future use, and 3 are set
aside as permanently unimplemented.

"Understanding bytecode and what bytecode is likely to be generated by a
Java compiler helps the Java programmer in the same way that knowledge
of assembly helps the C or C++ programmer."

#### Instructions

#### Model of computation

### Java Virtual Machine ([JVM](http://en.wikipedia.org/wiki/Java_virtual_machine))

A **Java virtual machine** (JVM) is a [process virtual machine](http://e
n.wikipedia.org/wiki/Virtual_machine#Process_virtual_machines) that can
execute [Java bytecode](http://en.wikipedia.org/wiki/Java_bytecode). It
is the code execution component of the [Java
platform](http://en.wikipedia.org/wiki/Java_platform).

JVMs use [JIT](http://en.wikipedia.org/wiki/Just-in-time_compilation)
compiling, not interpreting, to achieve greater speed.

<figure>
  <figcaption style="text-align:center;">Overview of a Java virtual machine (JVM) architecture. Source code is compiled to Java bytecode, which is verified, interpreted or JIT-compiled for the native architecture. The Java APIs and JVM together make up the Java Runtime Environment (JRE).</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="javaFigures/Java_virtual_machine_architecture.svg" alt="jvm" title="jvm">
</figure>

### Java Runtime Environment ([JRE](http://www.java.com/))

JRE = JIT compiler + JVM

Java Bytecode -> JRE -> Machine code

### Java Standard Edition ([Java SE](http://www.oracle.com/technetwork/java/javase/index.html))

Java Platform, Standard Edition or Java SE is a widely used platform for
development and deployment of portable applications for desktop and
server environments.[1] Java SE uses the object-oriented Java
programming language. Strictly speaking, Java SE is a platform
specification. It defines a wide range of general purpose APIs—such as
Java APIs for the Java Class Library[citation needed]—and also includes
the Java Language Specification and the Java Virtual Machine
Specification.[2] One of the most well-known implementations of Java SE
is Oracle Corporation's Java Development Kit (JDK).

- [JDK Oracle implementation of Java SE](http://www.oracle.com/technetwork/java/javase/overview/index.html)
- [Open source implementation of Java SE](http://openjdk.java.net/)
- [Documentation](http://docs.oracle.com/javase/8/)

### Java Enterprise Edition ([Java EE](http://www.oracle.com/technetwork/java/javaee/index.html))

Java Platform, Enterprise Edition or Java EE is Oracle's enterprise Java
computing platform. The platform provides an API and runtime environment
for developing and running enterprise software, including network and
web services, and other large-scale, multi-tiered, scalable, reliable,
and secure network applications. Java EE extends the Java Platform,
Standard Edition (Java SE),[1] providing an API for object-relational
mapping, distributed and multi-tier architectures, and web services. The
platform incorporates a design based largely on modular components
running on an application server. Software for Java EE is primarily
developed in the Java programming language. The platform emphasizes
Convention over configuration[2] and annotations for configuration.
Optionally XML can be used to override annotations or to deviate from
the platform defaults.

- [Documentation](http://docs.oracle.com/javaee/)

### Java Embedded

#### Java Micro Edition ([Java ME](http://www.oracle.com/technetwork/java/javame/index.html))

Java Platform, Micro Edition, or Java ME, is a Java platform designed
for embedded systems (mobile devices are one kind of such systems).
Target devices range from industrial controls to mobile phones
(especially feature phones) and set-top boxes. Java ME was formerly
known as Java 2 Platform, Micro Edition (J2ME).

- [Documentation](http://docs.oracle.com/javame/)

#### [Java Card](http://en.wikipedia.org/wiki/Java_Card)

Java Card refers to a software technology that allows Java-based
applications (applets) to be run securely on smart cards and similar
small memory footprint devices. Java Card is the tiniest of Java
platforms targeted for embedded devices. Java Card gives the user the
ability to program the devices and make them application specific. It is
widely used in SIM cards (used in GSM mobile phones) and ATM cards.


## Automatic memory management

Java uses an automatic garbage collector to manage memory in the object
lifecycle. The programmer determines when objects are created, and the
Java runtime is responsible for recovering the memory once objects are
no longer in use.

## What can Java technology can do?

- **Development Tools**: The development tools provide everything you'll
  need for compiling, running, monitoring, debugging, and documenting
  your applications. As a new developer, the main tools you'll be using
  are the *javac* compiler, the *java* launcher, and the *javadoc*
  documentation tool.

- **Application Programming Interface (API)**: The API provides the core
  functionality of the Java programming language. It offers a wide array
  of useful classes ready for use in your own applications. It spans
  everything from basic objects, to networking and security, to XML
  generation and database access, and more.

- **Deployment Technologies**: The JDK software provides standard
  mechanisms such as the Java Web Start software and Java Plug-In
  software for deploying your applications to end users.

- **User Interface Toolkits**: The *JavaFX*, *Swing*, and *Java 2D*
  toolkits make it possible to create sophisticated Graphical User
  Interfaces (GUIs).

- **Integration Libraries**: Integration libraries such as the Java IDL
  API, JDBC API, Java Naming and Directory Interface (JNDI) API, Java
  RMI, and Java Remote Method Invocation over Internet Inter-ORB
  Protocol Technology (Java RMI-IIOP Technology) enable database access
  and manipulation of remote objects.

# Syntax and Rules

## static

When you declare a variable or a method as static, it belongs to the
class, rather than to a specific instance.
- This means that only one instance of a static member exists, even if
  you create multiple objects of the class, or if you don't create any.
  It will be shared by all objects.
- It's a common practice to use upper case when naming a static
  variable, although not mandatory.

## final

Use the final keyword to mark a variable constant, so that it can be
assigned only once.
- Methods and classes can also be marked final.
    + So the methods can't be overridden.
    + And the classes can't be made subclasses.

## Packages

Packages are used to avoid name conflicts and to control access to
classes.
- A package can be defined as a group made up of similar types of
  classes, along with sub-packages.
- The following code will appear at the top of the classes:
    + `package <pkg_name>;`
- Import the classes
    + `import pkg.Vehicle;`
    + `import pkg.*`
- Two major results occur when a class is placed in a package.
    + First, the name of the package becomes a part of the name of the
      class.
    + Second, the name of the package must match the directory structure
      where the corresponding class file resides.

## Default parameter values

There are several ways to simulate default parameters in Java:

1. Method overloading.

		void foo(String a, Integer b) {
		    //...
		}

		void foo(String a) {
		    foo(a, 0); // here, 0 is a default value for b
		}

		foo("a", 2);
		foo("a");

One of the limitations of this approach is that it doesn't work if you
have two optional parameters of the same type and any of them can be
omitted.

2. Varargs.

a) All optional parameters are of the same type:

		void foo(String a, Integer... b) {
		    Integer b1 = b.length > 0 ? b[0] : 0;
		    Integer b2 = b.length > 1 ? b[1] : 0;
		    //...
		}

		foo("a");
		foo("a", 1, 2);

b) Types of optional parameters may be different:

		void foo(String a, Object... b) {
		    Integer b1 = 0;
		    String b2 = "";
		    if (b.length > 0) {
		      if (!(b[0] instanceof Integer)) {
		          throw new IllegalArgumentException("...");
		      }
		      b1 = (Integer)b[0];
		    }
		    if (b.length > 1) {
		        if (!(b[1] instanceof String)) {
		            throw new IllegalArgumentException("...");
		        }
		        b2 = (String)b[1];
		        //...
		    }
		    //...
		}

		foo("a");
		foo("a", 1);
		foo("a", 1, "b2");

The main drawback of this approach is that if optional parameters are of
different types you lose static type checking. Furthermore, if each
parameter has different meaning you need some way to distinguish them.


3. Nulls. To address the limitations of the previous approaches you can
   allow null values and then analyse each parameter in a method body:

		void foo(String a, Integer b, Integer c) {
		    b = b != null ? b : 0;
		    c = c != null ? c : 0;
		    //...
		}

		foo("a", null, 2);

Now all arguments values must be provided, but the default ones may be
null.

4. Optional class. This approach is similar to nulls, but uses guava
   Optional class for parameters that have a default value:

		void foo(String a, Optional<Integer> bOpt) {
		    Integer b = bOpt.isPresent() ? bOpt.get() : 0;
		    //...
		}

		foo("a", Optional.of(2));
		foo("a", Optional.<Integer>absent());

Optional makes a method contract explicit for a caller, however, one may
find such signature too verbose.

5. Builder pattern. The builder pattern is used for constructors and is
   implemented by introducing a separate Builder class:

		 class Foo {
		     private final String a;
		     private final Integer b;

		     Foo(String a, Integer b) {
		       this.a = a;
		       this.b = b;
		     }

		     //...
		 }

		 class FooBuilder {
		   private String a = "";
		   private Integer b = 0;

		   FooBuilder setA(String a) {
		     this.a = a;
		     return this;
		   }

		   FooBuilder setB(Integer b) {
		     this.b = b;
		     return this;
		   }

		   Foo build() {
		     return new Foo(a, b);
		   }
		 }

		 Foo foo = new FooBuilder().setA("a").build();

6. Maps. When the number of parameters is too large and for most of them
   default values are usually used, you can pass method arguments as a
   map of their names/values:

		void foo(Map<String, Object> parameters) {
		    String a = "";
		    Integer b = 0;
		    if (parameters.containsKey("a")) {
		        if (!(parameters.get("a") instanceof Integer)) {
		            throw new IllegalArgumentException("...");
		        }
		        a = (String)parameters.get("a");
		    }
		    if (parameters.containsKey("b")) {
		        //...
		    }
		    //...
		}

		foo(ImmutableMap.<String, Object>of(
		    "a", "a",
		    "b", 2,
		    "d", "value"));

Please note that you can combine any of these approaches to achieve a
desirable result.


## Exception Handling

A `try` and `catch` block is placed around the code that might generate
an exception.

```java
try {
    //some code
} catch (Exception e) {
    //some code to handle errors
}
```

`Exception` type is used to catch all possible exceptions.

### `throw` keyword

The `throw` keyword allows you to manually generate exceptions from your
methods.

```java
int div(int a, int b) throws ArithmeticException {
    if (b == 0) {
        throw new ArithmeticException("Division by Zero");
    } else {
        return a/b;
    }
}
```

The `throws` statement in the method definition defines the type of
Exception(s) the method can throw.
- Next, the `throw` keyword throws the corresponding exception, along
  with a custom message.
- Multiple exceptions can be defined in the throws statement using a
  comma-separated list.

A single try block can contain multiple catch blocks that handle
different exceptions separately.
- All catch blocks should be ordered from most specific to most general.
- You can use the `Exception` type to handle all other exceptions as the
  last catch.

```java
try {
    //some code
} catch (ExceptionType1 e1) {
    //Catch block
} catch (ExceptionType2 e2) {
    //Catch block
} catch (ExceptionType3 e3) {
    //Catch block
}
```

### Types of Exceptions

There are two exception types, checked and unchecked (also called
runtime).
- The main difference is that checked exceptions are checked when
  compiled, while unchecked exceptions are checked at runtime.
- Thread.sleep() throws an InterruptedException. this is an example
  checked exception. Your code will not compile until you've handled the
  exception.
- Unchecked exceptions: dividing by 0.

## Threads

Java is a multi-threaded programming language.
- The following diagram shows the life-cycle of a thread.

New Thread() -> New --Start()--> Runnable --run()--> Running
                 |                                       |
                 |----> Dead <--End of execution---------|
                          ^                              |
                          |- Waiting <--Sleep(), wait()--|

There are two ways to create a thread.

### 1. Extend the Thread class

Inherit from the Thread class, override its `run()` method, and write
the functionality of the thread in the run() method.
- Then you create a new object of your class and call its `start()`
  method to run the thread.

```java
class Loader extends Thread {
    public void run() {
        System.out.println("Hello");
    }
}

class MyClass {
    public static void main (String[] args) {
        Loader obj = new Loader();
        obj.start();
    }
}
```

>Every Java thread is prioritized to help the operating system determine
the order in which to schedule threads. The priorities range from 1 to
10, with each thread defaulting to priority 5. You can set the thread
priority with the `setPriority()` method.

### 2. Implementing the Runnable interface

Implements the run() method. Then, create a new thread object, pass the
Runnable class to its constructor, and start the Thread by calling the
start() method.
- Thread.sleep() method pauses a Thread for a specified period of time.
  For example, calling Thread.sleep(1000); pause the thread for one
  second.
    + Thread.sleep() throws an InterruptedException, so be sure to
      surround it with a try/catch block.

```java
class Loader implements Runnable {
    public void run() {
        System.out.println("HEllo");
    }
}

class MyClass {
    public static void main(String[] args) {
        Thread t = new Thread(new Loader());
        t.start();
    }
}
```

>It may seem that implementing the Runnable interface is a bit more
complex than extending from the Thread class. However, implementing the
Runnable interface is the preferred way to start a Thread because it
enables you to extend from another class, as well.

# Technologies

## [Servlet](https://en.wikipedia.org/wiki/Java_servlet)

Java programming language program running on server, receive requests
and can respond them.

## [JSP](https://en.wikipedia.org/wiki/JavaServer_Pages)

Create dynamically generated web pages based on HTML, XML.

To deploy and run JSP, a compatible web server with a servlet container,
such as [Apache Tomcat](http://tomcat.apache.org/) or
[Jetty](http://www.eclipse.org/jetty/).

![Life of a JSP file](http://upload.wikimedia.org/wikipedia/commons/0/03/JSPLife.svg "Life of a JSP file")

## Java API

The Java API is a collection of classes and interfaces that have been
written for you to use.
- Once you locate the package you want to use, you need to import it
into your code.

## Data Structures

### ArrayList

ArrayList are created with an initial size, but when this size is
exceeded, the collection is automatically enlarged.
- When objects are removed, the ArrayList may shrink in size. Note that
  the ArrayList class is in the java.util package, so it's necessary to
  import it before using it.

```java
import java.util.ArrayList;

ArrayList colors = new ArrayList();
// You can optionally specify a capacity and type of objects
ArrayList<String> colors = new ArrayList<String>(10);
```

>ArrayLists store objects. Thus, the type specified must be a class
type. You cannot pass, for example, `int` as the objects' type. Instead,
use the special class types that correspond to the desired value type,
such as `Integer` for int, `Double` for double, and so on.

```java
import java.util.ArrayList;

public class MyClass {
    public static void main(String[] args) {
        ArrayList<String> colors = new ArrayList<String>();
        colors.add("Red");
        colors.add("Blue");
        colors.add("Green");
        colors.add("Orange");
        colors.Remove("Green");

        System.out.println(colors);
    }
}
// Output: [Red, Blue, Orange]
```

Useful methods:

| Name           | Description                                               |
| -              | -                                                         |
| add(obj)       | Add a new object to the ArrayList                         |
| remove(obj)    | Remove an object from the ArrayList                       |
| contains()     | Returns true if the list contains the specified element   |
| get(int index) | Returns the element at the specified position in the list |
| size()         | Returns the number of elements in the list                |
| clear()        | Removes all the elements from the list                    |

### LinkedList

```java
import java.util.LinkedList;

public class MyClass {
    public static void main(String[] args) {
        LinkedList<String> c = new LinkedList<String>();
        c.add("Red");
        c.add("Blue");
        c.add("Green");
        c.add("Orange");
        c.remove("Green");

        System.out.println(c);
    }
}
//Outputs: [Red, Blue, Orange]
```

Summary:
- Use an ArrayList when you need rapid access to your data.
- Use a LinkedList when you need to make a large number of inserts
  and/or deletes.

### HashMap

Arrays and Lists store elements as ordered collections, with each
elements given an integer index.
- HashMap is used for storing data collections as key and value pairs.
- One object is used as a key (index) to another object (the value).
- The `put`, `remove`, and `get` methods are used to add, delete, and
  access values in the HashMap.

```java
import java.util.HashMap;

public class MyClass {
    public static void main(String[] args) {
        HashMap<String, Integer> points = new HashMap<String, Integer>();
        points.put("Amy", 154);
        points.put("Dave", 42);
        points.put("Rob", 733);
        System.out.println(points.get("Dave"));
    }
}
//Outputs 42
```

A HashMap cannot contain duplicate keys. Adding a new item with a key
that already exists overwrites the old element.
- The `containsKey` and `containsValue` methods that determine the
  presence of a specified key or value.
- It you try to get a value that is not present in you map, it returns
  the value of null.

### Sets

A Set is a collection that cannot contain duplicate elements. It models
the mathematical set abstraction.
- One of the implementations of the Set is the HashSet class.

```java
import java.util.HashSet;

public class MyClass {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<String>();
        set.add("A");
        set.add("B");
        set.add("C");
        System.out.println(set);
    }
}
//Outputs: [A, B, C]
```

The HashSet class does not automatically retain the order of the
elements as they are added. To order the elements, use a LinkedHashSet,
which maintains a linked list of the set's elements in the order in
which they were inserted.

### Collection class

```java
import java.util.Collections;

public class MyClass {
    public static void main(String[] args) {
        ArrayList<Integer> nums = new ArrayList<Integer>();
        nums.add(3);
        nums.add(36);
        nums.add(73);

        Collections.sort(nums);
        System.out.println(nums);
    }
}
```

- sort, max, min, reverse, shuffle

### Iterators

An Iterator is an object that enables to cycle through a collection,
obtain or remove elements.

```java
import java.util.Iterator;
import java.util.LinkedList;

public class MyClass {
    public static void main(String[] args) {
        LinkedList<String> animals = new LinkedList<String>();
        animals.add("fox");
        animals.add("cat");
        animals.add("dog");
        animals.add("rabbit");

        Iterator<String> it = animals.iterator();
        while (it.hasNext()) {
            String value = it.next();
            System.out.println(value);
        }
    }
}
//Outputs: fox
```

## Build Java project

The "Build" is a process that covers all the steps required to create a
"deliverable" of your software. In the Java world, this typically
includes:

1. Generating sources (sometimes).
2. Compiling sources.
3. Compiling test sources.
4. Executing tests (unit tests, integration tests, etc).
5. Packaging (into jar, war, ejb-jar, ear).
6. Running health checks (static analyzers like Checkstyle, Findbugs, PMD, test coverage, etc).
7. Generating reports.

So as you can see, compiling is only a (small) part of the build (and
the best practice is to fully automate all the steps with tools like
**Maven** or Ant and to run the build continuously which is known as
**Continuous Integration**).

## Variables

### Local variables

A local variables is a variable that is declared in the body of a
method.
- Parameter variables are similar to local variables, but they are
  declared in method headers.
- Local and parameter variables belong to methods. When a method runs,
  its local and parameter variables come to life. When the method exits,
  they are removed immediately.
- In contrast, instance variables belong to objects, not methods. When
  an object is constructed, its instance variables are created. The
  instance variables stay alive until no method uses the object any
  longer. (The Java virtual machine contains an garbage collector that
  periodically reclaims objects when  they are no longer used.)
- You must initialize all local variables
- Instance variables are initialized with a default value before a
  constructor is invoked.

# Development Tools

## IDE

- [Eclipse](https://www.eclipse.org/)
- [Netbean](https://netbeans.org/)

## Frameworks

### [Playframework](https://www.playframework.com/)

Make your changes and simply hit refresh!

Inspired by Rails. A drawback is that it is not idiomatic when using
Java, since it was written in Scala and that is its native language. It
is not compatible with
[Servlets](https://en.wikipedia.org/wiki/Java_servlet) Framework, so it
can't be used with **Tomcat** or for "enterprise" deployments where an
**application server** is needed.

### [Dropwizard](http://www.dropwizard.io/)

Developing ops-friendly, high-performance, RESTful web services.

> Looks good for a pure REST API backend solution.

### [Spark](http://sparkjava.com/)

A tiny Sinatra inspired framework for creating web applications in Java
8 with minimal effort.

### Spring

MVC is popular and is compatible with the **Servlets Framework**.
[JHipster](https://jhipster.github.io/) combines it with **AngularJS**
and its command line stack of Bower etc. Or it can be used with the
traditional [JSP](https://en.wikipedia.org/wiki/JavaServer_Pages) (which
is becoming less popular and doesn't work well with emedded web
servers), or with Springs's new recommendation
[Thymeleaf](http://www.thymeleaf.org/).

### Struts


### MyBatis

SQL Mapping Framework for Java

### Hibernate



## Testing

- Unit test: JUnit, TestNG
- Simulation user's interaction: Selenium
- Code coverage: Cobertura (calculates the percentage of code accessed
  by tests. It can be used to identify which parts of your Java program
  are lacking test coverage.)
- Continuous integration: Jenkins, Hudson

## Build Tools

### Ant

### Maven

### Gradle

# Tutorial

## Input and Output

### Input

```java
import java.util.Scanner;
...
Scanner in = newScanner(System.in);
...
System.out.print("Please enter the number of bottles: ");
int bottles = in.nextInt();

System.out.print("Enter price: ");
double price = in.nextDouble();

System.out.print("Enter your name: ");
String name = in.next(); // Get a word without spaces
String name = in.nextLine(); // Get the whole line with spaces
```

### Formatted Output

```java
System.out.printf("%10.2f", price);
System.out.printf("Quantity: %d Total: %10.2f", quantity, total);
```

| Format String  | Sample Output  | Comments                                                                              |
| -              | -              | -                                                                                     |
| "%d"           | 24             | Use d with an integer                                                                 |
| "%5d"          | ___24          | Spaces are added so that the field width is 5                                         |
| "Quantity:%5d" | Quantity:   24 | Characters inside a format string but outside a format specifier appear in the output |
| "%f"           | 1.21997        | Use f with a floating-point number                                                    |
| "%.2f"         | 1.22           | Prints two digits after the decimal point                                             |
| "%7.2f"        | ___1.22        | Spaces are added so that the field width is 7                                         |
| "%s"           | Hello          | Use s with a string                                                                   |
| "%d %.2f"      | 24 1.22        | You can format multiple values at once                                                |

### Using Dialog Boxes

```java
// This method returns a String object
String input = JOptionPane.showInputDialog("Enter price:");

// Use the Integer.parseInt and Double.parseDouble to convert the string
// to a number
double price = Double.parseDouble(input);

// Display output in a dialog box
JOptionPane.showMessageDialog(null, "Price: " + price);
```

## Working with Files

The `java.io` package includes a File class that allows you to work with
files.

```java
import java.io.File;

public class MyClass {
    public static void main(String[] args) {
        File x = new File("/tmp/test.txt");
        if (x.exists()) {
            System.out.println(x.getName() + "exists!");
        } else {
            System.out.println("The file does not exist");
        }
    }
}
```

### Reading a File

```java
import java.util.Scanner;

try {
    File x = new File("/tmp/test.txt");
    Scanner sc = new Scanner(x);
    while(sc.hasNext()) {
        System.out.println(sc.next());
    }
    sc.close();
} catch (FileNotFoundException e){
    e.printStackTrace();
}
```

The file's contents are output word by word because the next() method
returns each word separately.

### Creating & Writing Files

```java
import java.util.Formatter;

public class MyClass {
    public static void main(String[] args) {
        try {
            Formatter f = new Formatter("/tmp/test.txt");
            f.format("%s %s %s", "1", "John", "Smith \r\n");
            f.format("%s %s %s", "2", "Amy", "Brown");
            f.close();
        } catch (Exception e) {
            System.out.println("Error");
        }
    }
}
```

This creates an empty  file at the specified path. If the file already
exists, this will overwrite it.

## Reflection

- [Using reflection to set attribute](http://stackoverflow.com/questions/14374878/using-reflection-to-set-an-object-property)

## Debug

- [List of debug tools](http://blog.takipi.com/java-debugger-the-definitive-list-of-tools/)

# Object-Oriented Programming

## Instance Variables and Encapsulation

An instance is an object of the class.
- Each object of a class has its own set of instance variables.

A black box is any device whose inner workings are hidden.
- Its interface with the outside world is well-defined.
- The process of hiding implementation details while publishing an
  interface is called encapsulation.

Benefits of encapsulation:
- Simplify the process of making complicated things from other simple
  components.
- encapsulation also helps with diagnosing errors.

## Public Interface

What methods should you provide?
- What information should you give the programmers who use this class?

Mutators: modify the values and don't return a value.
- Accessors: return a value

```java
public double getBalance()
{
    // TODO: fill in implementation
    return 0;
}
```

## Class Implementation

### Instance Variables

### Constructor

A constructor has a simple job: to initialize the instance variables of
an object.

>When you implement constructors, be sure that each constructor
initializes all instance variables, and that you make use of all
parameter variables.

### Methods

When you implement a method, ask yourself whether it is an accessor or
mutator method.

## The `this` reference

When you call a method, you pass two kinds of inputs to the method:
- The object on which you invoke the method
- The method arguments

When you implement the method, you provide a parameter variable for each
argument. But you don't need to provide a parameter variable for the
object on which the method is being invoked.
- That object is called the **implicit parameter**.
- All other parameter variables are called **explicit parameters**.

The `this` reference denotes the implicit parameter.
- The `this` reference can also be used to distinguish between instance
  variables and local or parameter variables.

A method call without an implicit parameter is applied to the same
object.

```java
public class BankAccount
{
    ...
    public void monthlyFee()
    {
        withdraw(10);
        // this.withdraw(10);
    }
}
```

## Calling one constructor from another

```java
public class BankAccount
{
    public BankAccount(double initialBalance)
    {
        balance = initialBalance;
    }

    public BankAccount()
    {
        this(0);
    }
}
```

## Access Modifiers - Encapsulation

| Modifiers | Description                                                                                                                                              |
| -         | -                                                                                                                                                        |
| public    | Accessible from any other class                                                                                                                          |
| default   | A variable or method declared with no access control modifier is available to any other class in the same package.                                       |
| protected | Provides the same access as the default access modifier, with the addition that subclasses can access protected methods and variables of the superclass. |
| private   | Accessible only within the declared class itself                                                                                                         |

## Inheritance

Use the `extends` keyword.

```java
class Dog extends Animal {
    // some code
}
```

Here, Dog is the subclass, and animal is the superclass.

You can access the superclass from the subclass using the `super`
keyword. For example, `super.var` accesses the var member of the
superclass.

#### Anonymous classes

Anonymous classes are a way to extend the existing classes on the fly.
- The modification is applicable only to the current object, and not the
  class itself. So if we create another object of that class, the object
  will use the method is defined in the class.

For example, consider having a class Machine:

```java
class Machine() {
    public void start() {
        System.out.println("Starting...");
    }
}

public static void main(String[] args) {
    Machine m = new Machine() {
        @Override public void start() {
            System.out.println("Wooooo");
        }
    };

    m.start();
}
```

The `@Override` annotation is used to make your code easier to
understand, because it makes it more obvious when methods are
overridden.

## Polymorphism

One method with multiple implementations.

Here is an example in Java: Dog and Cat are classes that inherit from
the Animal class. Each class has its own implementation of the makeSound
() method.

```java
class Animal {
    public void makeSound() {
        System.out.println("Grr...");
    }
}

class Cat extends Animal {
    public void makeSound() {
        System.out.println("Meow");
    }
}

class Dog extends Animal {
    public void makeSound() {
        System.out.println("Woof");
    }
}
```

As all Cat and Dog objects are Animal objects, we can do the following
in main:

```java
public static void main(String[] args) {
    Animal a = new Dog();
    Animal b = new Cat();
    a.makeSound();  //Outputs "Woof"
    b.makeSound();  //Outputs "Meow"
}
```

This demonstrate that you can use the Animal variable  without actually
knowing that it contains an object of the subclass. This is very useful
when you have multiple subclasses of the superclass.

#### Method overriding

A subclass can define a behavior that's specific to the subclass type,
meaning that a subclass can implement a parent class method based on its
requirements. This feature is known as method overriding.

Rules for Method Overriding:
- Should have the same return type and arguments
- The access level cannot be more restrictive than the overriden
  method's access level.
    + Example: if the superclass method is declared public, the
      overriding mthod in the subclass can be neither private nor
      protected.
- A method declared final or static cannot be overridden
- If a method cannot be inherited, it cannot be overridden
- Constructors cannot be overridden

#### Method overloading

When methods have the same name, but different parameters, it is known
as method overloading.

## Abstraction

In Java, abstraction is achieved using abstract classes and interfaces.

#### Abstract classes

An abstract class is defined using the `abstract` keyword.
- If a class is declared abstract it cannot be instantiated (you cannot
  create objects of that type).
- To use a abstract class, you have to inherit it from another class.
- Any class that contains an abstract method should be defined as
  abstract.
    + An abstract method is a method that is declared without an
      implementation (without braces, and followed by a semicolon):
      `abstract void walk();`

```java
abstract class Animal {
    int legs = 0;
    abstract void makeSound();
}

class Cat extends Animal {
    public void makeSound() {
        System.out.println("Meow");
    }
}
```

Different animals make different sounds, that's why we define an
abstract class Animal, and leave the implementation of how they make
sounds to the subclasses.
- This is used when there is no meaningful for the method in the
  superclass.

#### Interfaces

An interface is a completely abstract class that contains only abstract
methods.

Specifications for interfaces:
- Defined using the `interface` keyword.
- May contain only `static` final variables.
- Cannot contain a constructor because interfaces cannot be instantiated
- Interfaces can extend other interfaces
- A class can implement any number of interfaces

```java
interface Animal {
    public void eat();
    public void makeSound();
}

class Cat implements Animal {
    public void makeSound() {
        System.out.println("Meow");
    }

    public void eat() {
        System.out.println("omnomnom");
    }
}
```

Properties of interfaces
- An interface is implicitly abstract. You do not need to use the
  abstract keyword while declaring an interface.
- Each method in an interface is also implicitly abstract, so the
  abstract keyword is not needed.
- Methods in an interface are implicitly public.

>A class can inherit from just one superclass, but can implement multiple
interfaces!

>When you implement an interface, you need to override all of its
methods.

## Nesting classes - Inner classes

Java supports nesting classes; a class can be a member of another class.
- Inner classes can be private.

## The equals() method

Each object has a predefined `equals()` method that is used for
semantic equality testing.
- But, to make it work for our classes, we need to override it and check
  the conditions we need.
- It can be auto-generated by the IDE.

```java
class Animal {
  String name;
  Animal(String n) {
    name = n;
  }
  @Override
  public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + ((name == null) ? 0 : name.hashCode());
    return result;
  }
  @Override
  public boolean equals(Object obj) {
    if (this == obj)
      return true;
    if (obj == null)
      return false;
    if (getClass() != obj.getClass())
      return false;
    Animal other = (Animal) obj;
    if (name == null) {
      if (other.name != null)
        return false;
    } else if (!name.equals(other.name))
      return false;
    return true;
  }
}
```

The automatically generated hashCode() method is used to determine where
to store the object internally.
- Whenever you implement equals, you MUST also implement hashCode.

# Data Structures

## Primitive types

In Java, every value is either a reference to an object, or it belongs
to one of the eight primitive types.

### Number types

| Type    | Description                                                                | Size    | Example      |
| -       | -                                                                          | -       | -            |
| int     | The integer type, range Integer.MIN_VALUE to Integer.MAX_VALUE             | 4 bytes | 1, 2, 3      |
| byte    | The type describing a single byte, range -128 ... 127                      | 1 byte  |              |
| short   | The short integer type, range -32,768 ... 32,767                           | 2 bytes |              |
| long    | The long integer type                                                      | 8 bytes |              |
| double  | The double-precision floating-point type                                   | 8 bytes | 0.1          |
| float   | The single-precision floating-point type                                   | 4 bytes | 1E6, 2.96E-2 |
| char    | The character type, representing code units in the Unicode encoding scheme | 2 bytes |              |
| boolean | THe type with the two truth values false and true                          | 1 bit   |              |

When a value such as 6 or 0.335 occurs in a Java program, it is called a
**number literal**.

A numeric computation overflows if the result falls outside the range
for the number type.
- Using `BigInteger` type to prevent overflow errors.

**Rounding errors** occur when an exact representation of a floating-
point number is not possible.
- Using `BigDecimal` type to prevent rounding errors.

Constants:
- In a method: `final double NICKEL_VALUE = 0.05;`
- In a class: `public static final double LITERS_PER_GALLON = 3.785;`

Big Numbers:

```java
BigInteger n = new BigInteger("1000000");
BigInteger r = n.multiply(n);
System.out.println(r);

BigDecimal d = new BigDecimal("4.35");
BigDecimal e = new BigDecimal("100");
BigDecimal f = d.multiply(e);
System.out.println(f);
```

Any number that is not completely self-explanatory should be declared as
a named constant. Or write comments to explain its functions and why you
choose them.

Mathematical methods

| Method            | Returns                      | Method            | Returns                      |
| -                 | -                            | -                 | -                            |
| Math.sqrt(x)      | Square root of x             | Math .abs(x)      | Absolute value               |
| Math.pow(x, y)    | x to the y                   | Math.max(x, y)    | The larger                   |
| Math.sin(x)       | Sine of x (radian)           | Math.min(x, y)    | The smaller                  |
| Math.cos(x)       | Cosine                       | Math.exp(x)       | e to the x                   |
| Math.tan(x)       | Tangent                      | Math.log(x)       | Natural log                  |
| Math.round(x)     | Closest integer              | Math.log10(x)     | Decimal log                  |
| Math.ceil(x)      | Smallest integer >= x        | Math.floor(x)     | Largest integer <= x         |
| Math.toRadians(x) | Convert x degrees to radians | Math.toDegrees(x) | Convert x radians to degrees |

## String

### String operations

| Statement                                                | Result               | Comment                                                                                                                                |
| -                                                        | -                    | -                                                                                                                                      |
| String str = "Ja"; str = str + "va";                     | str is set to "Java" | When applied to strings, + denotes concatenation                                                                                       |
| String greeting = "H & S"; int n = greeting.length();    | n is set to 5        | Each space counts as one character                                                                                                     |
| str.charAt(1)                                            |                      |                                                                                                                                        |
| String str = "Sally"; String str2 = str.substring(1, 4); | str2 is set to "all" | Extracts the substring starting at position 1 and ending before position 4 (starting with first good data and end with first bad data) |

### Reading Exception Reports

1. The name of the exception, such as `StringIndexOutOfBoundsException`
2. The line number of the code that contained the statement that caused
   the exception, such as `Homework1.java:16`

The name of the exception is always in the first line of the report, and
it ends with `Exception`
- The first line of the stack trace is the method that actually
  generated the exception.
- THe last line of the stack trace is a line in `main`
- Often, the exception was thrown by a method that is in the standard
  library. Look for the first line in **your code** that appears in the
  exception report.

## Array

```java
// Have to "new" an array when we initialize it
double[] values = new double[10];

// An array of objects
BankAccount[] accounts = new BankAccount[10];
// We have to initialize the array manually
for (int i = 0; i < 10; i++)
{
    accounts[i] = new BankAccount();
}
```

### Methods with a variable number of arguments

```java
public void addScores(int... values)
{
    for (int i = 0; i < values.length; i++) // values is an int[]
    {
        totalScore = totalScore + values[i];
    }
}

fred.addScores(10, 7);
fred.addScores(1, 7, 2, 9);
```

# Loop

- while, do while, for

```java
// This for each loop cannot modify the array
// Use this for each loop to traverse the data
for (double element : values)
{
    sum = sum + element;
}
```

# Tips & Tricks

## Redirection of Input and Output

The command line interface of the operating system provides a way to
link a file to the input of a program, as if all the characters in the
file had actually been typed by a user.
- `java SentinelDemo < numbers.txt`
- Redirect output: `java SentinelDemo < numbers.txt > output.txt`

## Input Validation

```java
if  (in.hasNextInt())
{
    int floor = in.nextInt();
    // Process the input value
}
else
{
    System.out.println("Error: Not an integer.")
}
```

## Logging

Instead of using `System.out.println` to print out trace messages, use
the global logger object.

```java
Logger.getGlobal().info("status is SINGLE");
```

By default, the message is printed. But if you call `Logger.getGlobal
().setLevel(Level.OFF);` at the beginning of the main method of your
program, all log message printing is suppressed. Set the level to
Level.INFO to turn logging of info messages on again.

## Comparing Floating-Point Numbers, Strings, Objects

```java
final double EPSILON = 1E-14;
if (Math.abs(x-y) <= EPSILON)
{
    // x is approximately equal to y
}
```

```java
if (strin1.equals(string2))
{
    // ...
}
```

`string1.compareTo(string2)`: comparing strings using lexicographic
order.

`==`: compare the references refer to the objects

## [Send mail](https://cloud.google.com/appengine/docs/java/mail/usingjavamail)

## Convert int to String

- String.valueOf(number)
- Integer.toString(number) : check null before
- Concat string: "" + number

## [Java Built-in Exceptions](http://www.tutorialspoint.com/java/java_builtin_exceptions.htm)

- Difference between `e.printStackTrace()` and `e.toString()`:
  printStackTrace will print the whole stack trace of an exception.

## Decompile Java class files, jar files

### Available decompilers - Listing follow popular

1. [Procyon](https://bitbucket.org/mstrobel/procyon): 2014. JDK 5,
   partly 6. Written in Java. Worth trying.

2. CFR - 2014. JDK 6, 7, 8 support. Written in Java 6.

“CFR by Lee Benfield is well on its way to becoming the premier Java
Decompiler. Lee and I actually work for the same company and share
regression tests. We're engaged in a friendly competition to see who can
deliver a better decompiler. Based on his progress thus far, there's a
very good chance he will win--at least on decompiling obfuscated code
:)”

3. Candle - 2013. Written in Java. By Brad Davis @ RH. “only decompiles
   a subset of the JVM operations”.

4. Krakatau - 2014.  JDK 7 support? Written in Python.

“Includes a robust verifier. Focuses on translating arbitrary bytecode
into valid Java code, as opposed to reconstructing the original code.”

5. JBVD - 2013. Academic Free License (AFL). Javassist approach. Unknown
   quality.

6. EDJC - 2011. Written in Java.

7. JD - JD-Core and JD-GUI are written in C++.

### GUI Front Ends Interface base on these decompilers

[Jadx](https://github.com/skylot/jadx)

[Luyten](https://github.com/deathmarine/Luyten)

[Bytecode Viewer](https://github.com/Konloch/bytecode-viewer)

## Compare jar file content with source code

1. You export source code into jar file. (e.g: use Eclipse to export)
2. Use decompiler jar file tool to decompile two jar file into source code. (e.g: luyten, jadx, etc.)
3. Use compare tool to compare content of two source code folder is generated by step 2. (e.g: Beyond Compare tool)

# References

[wiki]: https://en.wikipedia.org/wiki/Java_(programming_language)
