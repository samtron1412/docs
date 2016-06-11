[TOC]

# Introduction
Java is a computer programming language that is **concurrent**, **class-based**, **object-oriented**, and specifically designed to have *as few implementation dependencies as possible*. It is intended to let application developers "**write once, run anywhere**" (WORA), meaning that code that runs on one platform does not need to be recompiled to run on another. Java applications are typically compiled to [bytecode](http://en.wikipedia.org/wiki/Java_bytecode) (class file) that can run on any [Java virtual machine](http://en.wikipedia.org/wiki/Java_virtual_machine) (JVM) regardless of computer architecture.

Released in 1995, implement by C and C++. The original and *reference implementation* Java **compilers**, **virtual machines**, and **class libraries** were developed by Sun. As of May 2007, in compliance with the specifications of the [Java Community Process](https://www.jcp.org), Sun relicensed most of its Java technologies under the [GNU General Public License](http://en.wikipedia.org/wiki/GNU_General_Public_License).

## History
Java named from [Java coffee](http://en.wikipedia.org/wiki/Java_coffee).

**Java 2** (released initially as J2SE 1.2 in December *1998 – 1999*), new versions had multiple configurations built for different types of platforms. For example, *J2EE* targeted enterprise applications and the greatly stripped-down version *J2ME* for mobile applications (Mobile Java). *J2SE* designated the Standard Edition. In *2006*, for marketing purposes, Sun renamed new J2 versions as *Java EE, Java ME, and Java SE*, respectively.

[Java Version History](http://en.wikipedia.org/wiki/Java_version_history):

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
Java.net is a large community of Java developers and their projects. We welcome anyone interested in Java, related **JVM** technologies, and education to our discussions and projects.

### Java Community Process ([JCP](https://www.jcp.org))
The JCP is the mechanism for developing standard technical specifications for Java technology.


# Installation
## From repository
Use packages manager to install packages.


## From Oracle bin file
- Download bin file from [this](http://ftp.cc.uoc.gr/Java/Linux-x86_64/)
- chmod +x <file>
- Run file

```bash
update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.6.0_45/bin/java" 1
update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.6.0_45/bin/javac" 1
update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.6.0_45/bin/javaws" 1
```

1. Open the profile file with your favorite editor. I used nano
`sudo nano /etc/profile`
2. In the /usr/profile file, type the following lines.
`JAVA_HOME=/usr/java/jdk1.5.0_22; export JAVA_HOME;PATH=$JAVA_HOME/bin:$PATH; export PATH` **note**: JAVA_HOME location might be different for you.
3. Update the environment variables by typing
`source /etc/profile`


## From OpenJDK



# Practices
## [Platform](http://docs.oracle.com/javase/8/docs/index.html)
One characteristic of Java is **portability**, which means that computer programs written in the Java language must run similarly on any hardware/operating-system platform. This is achieved by compiling the Java language code to an intermediate representation called *Java bytecode*, instead of directly to platform-specific machine code. Java bytecode instructions are analogous to machine code, but they are intended to be interpreted by a virtual machine (VM) written specifically for the host hardware. End-users commonly use a *Java Runtime Environment* (JRE) installed on their own machine for standalone Java applications, or in a web browser for Java *applets*.

**Standardized libraries** provide a generic way to access host-specific features such as *graphics*, *threading*, and *networking*.

The **Java platform** is the name for *a bundle of related programs* from Sun that *allow for developing and running programs written in the Java programming language*. The platform is not specific to any one processor or operating system, but rather *an execution engine* (called a virtual machine) and *a compiler* with *a set of libraries* that are implemented for various hardware and operating systems so that Java programs can run identically on all of them. Each platform have:

- Java compiler: Java source code -> Java bytecode
- Java Runtime Environment (JRE - Java Virtual Machine): Java bytecode -> machine code
- The libraries (API)

Main platforms:

- [Java Card](http://en.wikipedia.org/wiki/Java_Card): A technology that allows small Java-based applications (*applets*) to be run securely on smart cards and similar small-memory devices.
- [Java ME](http://www.oracle.com/technetwork/java/javame/index.html) (Micro Edition): Specifies several different sets of libraries (known as profiles) for devices with limited storage, display, and power capacities. Often used to develop applications for *mobile devices, PDAs, TV set-top boxes, and printers*.
- [Java SE](http://www.oracle.com/technetwork/java/javase/index.html) (Standard Edition): For *general-purpose* use on desktop PCs, servers and similar devices.
- [Java EE](http://www.oracle.com/technetwork/java/javaee/index.html) (Enterprise Edition): Java SE plus various APIs useful for *multi-tier client–server enterprise applications*.

### Implementations
[Oracle Corporation](http://en.wikipedia.org/wiki/Oracle_Corporation) is the current owner of the official implementation of the Java SE platform, following their acquisition of [Sun Microsystems](http://en.wikipedia.org/wiki/Sun_Microsystems) on January 27, 2010.

Because Java lacks any formal standardization recognized by *Ecma International, ISO/IEC, ANSI, or other third-party standards organization*, the Oracle implementation is the [de facto standard](http://en.wikipedia.org/wiki/De_facto_standard).

The Oracle implementation is packaged into two different distributions:

- **The Java Runtime Environment** (JRE) which contains the parts of the Java SE platform required to run Java programs and is intended for end-users.
- **The Java Development Kit** (JDK), which is intended for software developers and includes development tools such as the [Java compiler](http://en.wikipedia.org/wiki/Java_compiler), [Javadoc](http://en.wikipedia.org/wiki/Javadoc), [Jar](http://en.wikipedia.org/wiki/JAR_(file_format)), and a **debugger**.

[OpenJDK](http://en.wikipedia.org/wiki/OpenJDK) is another notable Java SE implementation that is licensed under the GPL. The implementation started when Sun began releasing the Java source code under the GPL. As of Java SE 7, OpenJDK is the official Java reference implementation.

### Performance
Programs written in Java have a reputation for being slower and requiring more memory than those written in C++. However, Java programs' execution speed improved significantly with the introduction of Just-in-time compilation in 1997/1998 for Java 1.1

Some platforms offer direct hardware support for Java; there are microcontrollers that can run Java in hardware instead of a software Java virtual machine, and ARM based processors can have hardware support for executing Java bytecode through their [Jazelle](http://en.wikipedia.org/wiki/Jazelle) option.

### Java Bytecode
Java bytecode is the [instruction set](http://en.wikipedia.org/wiki/Instruction_set) of the [Java virtual machine](http://en.wikipedia.org/wiki/Java_virtual_machine).

Each bytecode is composed by one, or in some cases two, bytes that represent the instruction ([opcode](http://en.wikipedia.org/wiki/Opcode)), along with zero or more bytes for passing parameters. Of the 256 possible byte-long opcodes, 198 are currently in use, 51 are reserved for future use, and 3 are set aside as permanently unimplemented.

"Understanding bytecode and what bytecode is likely to be generated by a Java compiler helps the Java programmer in the same way that knowledge of assembly helps the C or C++ programmer."

#### Instructions

#### Model of computation

### Java Virtual Machine ([JVM](http://en.wikipedia.org/wiki/Java_virtual_machine))
A **Java virtual machine** (JVM) is a [process virtual machine](http://en.wikipedia.org/wiki/Virtual_machine#Process_virtual_machines) that can execute [Java bytecode](http://en.wikipedia.org/wiki/Java_bytecode). It is the code execution component of the [Java platform](http://en.wikipedia.org/wiki/Java_platform).

JVMs use [JIT](http://en.wikipedia.org/wiki/Just-in-time_compilation) compiling, not interpreting, to achieve greater speed.

<figure>
  <figcaption style="text-align:center;">Overview of a Java virtual machine (JVM) architecture. Source code is compiled to Java bytecode, which is verified, interpreted or JIT-compiled for the native architecture. The Java APIs and JVM together make up the Java Runtime Environment (JRE).</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="javaFigures/Java_virtual_machine_architecture.svg" alt="jvm" title="jvm">
</figure>

### Java Runtime Environment ([JRE](http://www.java.com/))
JRE = JIT compiler + JVM

Java Bytecode -> JRE -> Machine code

### Java Standard Edition ([Java SE](http://www.oracle.com/technetwork/java/javase/index.html))
Java Platform, Standard Edition or Java SE is a widely used platform for development and deployment of portable applications for desktop and server environments.[1] Java SE uses the object-oriented Java programming language. Strictly speaking, Java SE is a platform specification. It defines a wide range of general purpose APIs—such as Java APIs for the Java Class Library[citation needed]—and also includes the Java Language Specification and the Java Virtual Machine Specification.[2] One of the most well-known implementations of Java SE is Oracle Corporation's Java Development Kit (JDK).

- [JDK Oracle implementation of Java SE](http://www.oracle.com/technetwork/java/javase/overview/index.html)
- [Open source implementation of Java SE](http://openjdk.java.net/)
- [Documentation](http://docs.oracle.com/javase/8/)

### Java Enterprise Edition ([Java EE](http://www.oracle.com/technetwork/java/javaee/index.html))
Java Platform, Enterprise Edition or Java EE is Oracle's enterprise Java computing platform. The platform provides an API and runtime environment for developing and running enterprise software, including network and web services, and other large-scale, multi-tiered, scalable, reliable, and secure network applications. Java EE extends the Java Platform, Standard Edition (Java SE),[1] providing an API for object-relational mapping, distributed and multi-tier architectures, and web services. The platform incorporates a design based largely on modular components running on an application server. Software for Java EE is primarily developed in the Java programming language. The platform emphasizes Convention over configuration[2] and annotations for configuration. Optionally XML can be used to override annotations or to deviate from the platform defaults.

- [Documentation](http://docs.oracle.com/javaee/)

### Java Embedded
#### Java Micro Edition ([Java ME](http://www.oracle.com/technetwork/java/javame/index.html))
Java Platform, Micro Edition, or Java ME, is a Java platform designed for embedded systems (mobile devices are one kind of such systems). Target devices range from industrial controls to mobile phones (especially feature phones) and set-top boxes. Java ME was formerly known as Java 2 Platform, Micro Edition (J2ME).

- [Documentation](http://docs.oracle.com/javame/)

#### [Java Card](http://en.wikipedia.org/wiki/Java_Card)
Java Card refers to a software technology that allows Java-based applications (applets) to be run securely on smart cards and similar small memory footprint devices. Java Card is the tiniest of Java platforms targeted for embedded devices. Java Card gives the user the ability to program the devices and make them application specific. It is widely used in SIM cards (used in GSM mobile phones) and ATM cards.


## Automatic memory management
Java uses an automatic garbage collector to manage memory in the object lifecycle. The programmer determines when objects are created, and the Java runtime is responsible for recovering the memory once objects are no longer in use.

## What can Java technology can do?
- **Development Tools**: The development tools provide everything you'll need for compiling, running, monitoring, debugging, and documenting your applications. As a new developer, the main tools you'll be using are the *javac* compiler, the *java* launcher, and the *javadoc* documentation tool.

- **Application Programming Interface (API)**: The API provides the core functionality of the Java programming language. It offers a wide array of useful classes ready for use in your own applications. It spans everything from basic objects, to networking and security, to XML generation and database access, and more.

- **Deployment Technologies**: The JDK software provides standard mechanisms such as the Java Web Start software and Java Plug-In software for deploying your applications to end users.

- **User Interface Toolkits**: The *JavaFX*, *Swing*, and *Java 2D* toolkits make it possible to create sophisticated Graphical User Interfaces (GUIs).

- **Integration Libraries**: Integration libraries such as the Java IDL API, JDBC API, Java Naming and Directory Interface (JNDI) API, Java RMI, and Java Remote Method Invocation over Internet Inter-ORB Protocol Technology (Java RMI-IIOP Technology) enable database access and manipulation of remote objects.

# Syntax
## Object Oriented Programming (OOP)

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

One of the limitations of this approach is that it doesn't work if you have two optional parameters of the same type and any of them can be omitted.

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

The main drawback of this approach is that if optional parameters are of different types you lose static type checking. Furthermore, if each parameter has different meaning you need some way to distinguish them.


3. Nulls. To address the limitations of the previous approaches you can allow null values and then analyse each parameter in a method body:

		void foo(String a, Integer b, Integer c) {
		    b = b != null ? b : 0;
		    c = c != null ? c : 0;
		    //...
		}

		foo("a", null, 2);

Now all arguments values must be provided, but the default ones may be null.

4. Optional class. This approach is similar to nulls, but uses guava Optional class for parameters that have a default value:

		void foo(String a, Optional<Integer> bOpt) {
		    Integer b = bOpt.isPresent() ? bOpt.get() : 0;
		    //...
		}

		foo("a", Optional.of(2));
		foo("a", Optional.<Integer>absent());

Optional makes a method contract explicit for a caller, however, one may find such signature too verbose.

5. Builder pattern. The builder pattern is used for constructors and is implemented by introducing a separate Builder class:

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

6. Maps. When the number of parameters is too large and for most of them default values are usually used, you can pass method arguments as a map of their names/values:

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

Please note that you can combine any of these approaches to achieve a desirable result.


# Special classes
## [Abstract class](http://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)

# Class libraries

# Basic knowledge
## [Servlet](https://en.wikipedia.org/wiki/Java_servlet)
Java programming language program running on server, receive requests and can respond them.

## [JSP](https://en.wikipedia.org/wiki/JavaServer_Pages)
Create dynamically generated web pages based on HTML, XML.

To deploy and run JSP, a compatible web server with a servlet container, such as [Apache Tomcat](http://tomcat.apache.org/) or [Jetty](http://www.eclipse.org/jetty/).

![Life of a JSP file](http://upload.wikimedia.org/wikipedia/commons/0/03/JSPLife.svg "Life of a JSP file")

## Build Java project
The "Build" is a process that covers all the steps required to create a "deliverable" of your software. In the Java world, this typically includes:

1. Generating sources (sometimes).
2. Compiling sources.
3. Compiling test sources.
4. Executing tests (unit tests, integration tests, etc).
5. Packaging (into jar, war, ejb-jar, ear).
6. Running health checks (static analyzers like Checkstyle, Findbugs, PMD, test coverage, etc).
7. Generating reports.

So as you can see, compiling is only a (small) part of the build (and the best practice is to fully automate all the steps with tools like **Maven** or Ant and to run the build continuously which is known as **Continuous Integration**).

# Development Tools
## IDE
- [Eclipse](https://www.eclipse.org/)
- [Netbean](https://netbeans.org/)

## Frameworks
### [Playframework](https://www.playframework.com/)
Make your changes and simply hit refresh!

Inspired by Rails. A drawback is that it is not idiomatic when using Java, since it was written in Scala and that is its native language. It is not compatible with [Servlets](https://en.wikipedia.org/wiki/Java_servlet) Framework, so it can't be used with **Tomcat** or for "enterprise" deployments where an **application server** is needed.

### [Dropwizard](http://www.dropwizard.io/)
Developing ops-friendly, high-performance, RESTful web services.

> Looks good for a pure REST API backend solution.

### [Spark](http://sparkjava.com/)
A tiny Sinatra inspired framework for creating web applications in Java 8 with minimal effort.

### Spring
MVC is popular and is compatible with the **Servlets Framework**. [JHipster](https://jhipster.github.io/) combines it with **AngularJS** and its command line stack of Bower etc. Or it can be used with the traditional [JSP](https://en.wikipedia.org/wiki/JavaServer_Pages) (which is becoming less popular and doesn't work well with emedded web servers), or with Springs's new recommendation [Thymeleaf](http://www.thymeleaf.org/).

### Struts


### MyBatis
SQL Mapping Framework for Java

### Hibernate



## Testing
- Unit test: JUnit, TestNG
- Simulation user's interaction: Selenium
- Code coverage: Cobertura (calculates the percentage of code accessed by tests. It can be used to identify which parts of your Java program are lacking test coverage.)
- Continuous integration: Jenkins, Hudson

# Tutorial
## Reflection
- [Using reflection to set attribute](http://stackoverflow.com/questions/14374878/using-reflection-to-set-an-object-property)

## Debug
- [List of debug tools](http://blog.takipi.com/java-debugger-the-definitive-list-of-tools/)

# Tips & Tricks
## [Send mail](https://cloud.google.com/appengine/docs/java/mail/usingjavamail)

## Convert int to String
- String.valueOf(number)
- Integer.toString(number) : check null before
- Concat string: "" + number

## [Java Built-in Exceptions](http://www.tutorialspoint.com/java/java_builtin_exceptions.htm)
- Difference between `e.printStackTrace()` and `e.toString()`: printStackTrace will print the whole stack trace of an exception.

## Decompile Java class files, jar files
### Available decompilers - Listing follow popular

1. [Procyon](https://bitbucket.org/mstrobel/procyon): 2014. JDK 5, partly 6. Written in Java. Worth trying.

2. CFR - 2014. JDK 6, 7, 8 support. Written in Java 6.

“CFR by Lee Benfield is well on its way to becoming the premier Java Decompiler. Lee and I actually work for the same company and share regression tests. We're engaged in a friendly competition to see who can deliver a better decompiler. Based on his progress thus far, there's a very good chance he will win--at least on decompiling obfuscated code :)”

3. Candle - 2013. Written in Java. By Brad Davis @ RH. “only decompiles a subset of the JVM operations”.

4. Krakatau - 2014.  JDK 7 support? Written in Python.

“Includes a robust verifier. Focuses on translating arbitrary bytecode into valid Java code, as opposed to reconstructing the original code.”

5. JBVD - 2013. Academic Free License (AFL). Javassist approach. Unknown quality.

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
