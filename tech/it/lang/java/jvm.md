# Overview

Java Virtual Machine

- Resources
    + https://docs.oracle.com/en/java/javase/21/vm/
    + Garbage Collection Tuning
        * https://docs.oracle.com/en/java/javase/21/gctuning/
- HotSpot JVM Optimization
    + https://docs.oracle.com/en/java/javase/11/vm/java-hotspot-virtual-machine-performance-enhancements.html
    + https://www.oracle.com/java/technologies/whitepaper.html
    + https://en.wikipedia.org/wiki/HotSpot_(virtual_machine)

# JVM Tool Interface

- https://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html
    + a programming interface used by development and monitoring tools.
    + It provides both a way to inspect the state and to control the
      execution of applications running in JVM.
- https://docs.oracle.com/javase/8/docs/platform/jvmti/jvmti.html#tooloptions
    + JAVA_TOOL_OPTIONS
    + Since the command-line cannot always be accessed or modified, for
      example in embedded VMs or simply VMs launched deep within
      scripts, a JAVA_TOOL_OPTIONS variable is provided so that agents
      may be launched in these cases.
- In many environments the command line is not readily accessible to
  start the application with necessary command-line options.
    + This often arises with applications that use embedded VMs (meaning
      they use the Java Native Interface (JNI) Invocation API to start
      the VM), or where the startup is deeply nested in scripts.
    + In these environments the JAVA_TOOL_OPTIONS environment variable
      can be useful to augment a command line.
