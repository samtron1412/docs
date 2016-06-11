[TOC]

# Overview
Log4j is a Reliable, Fast and flexible Logging Framework written in Java which is distributed under the Apache Software License.

Log4j has three main components:
- **loggers**: responsible for capturing logging information.
- **appenders**: responsible for publishing logging information to various preferred destinations.
- **layouts**: responsible to format logging information in different styles.

# Architecture
There are two type of objects available with Log4j framework.
- **Core Objects**: these are mandatory objects of the framework and required to use the framework.
- **Support Objects**: These are optional objects of the framework and support core objects to perform addition but important tasks.

## Core objects
### Logger object
Capturing logging information and they are stored in a namespace hierarchy.

### Layout object
human readable and reusable.

### Appender object
publishing logging information to various preferred destinations such as a **database**, **file**, **console**, UNIX Syslog etc.

<figure>
  <figcaption style="text-align:center;">log4j Architecture</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="log4j/log4j-arch.jpg" alt="log4j" title="log4j">
</figure>

## Support objects
### Level object
The Level object defines the granularity and priority of any logging information. There are seven levels of logging defined within the API: OFF, DEBUG, INFO, ERROR, WARN, FATAL, and ALL.

### Filter object
The Filter object is used to analyze logging information and make further decisions on whether that information should be logged or not.

### Object Renderer
The ObjectRenderer object is specialized in providing a String representation of different objects passed to the logging framework. This object is used by Layout objects to prepare the final logging information.

### Log Manager
The LogManager object manages the logging framework. It is responsible for reading the initial configuration parameters from a system-wide configuration file or a configuration class.

# Configuration
Configuring log4j involves assigning the Level, defining Appender, and specifying Layout objects in a configuration file.

The log4j.properties file is a log4j configuration file which keeps properties in key-value pairs. By default, the LogManager looks for a file named log4j.properties in the CLASSPATH.


