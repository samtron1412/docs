[TOC]

# Overview

- https://www.digitalocean.com/community/tutorials/log4j2-example-tutorial-configuration-levels-appenders
- https://logging.apache.org/log4j/2.x/manual/configuration.html

Log4j is a Reliable, Fast and flexible Logging Framework written in Java
which is distributed under the Apache Software License.

LoggerContext -> LogManager -> Logger -> LoggerConfig -> Appender -> Layout

Log4j has three main components:
- **loggers**: responsible for capturing logging information.
- **appenders**: responsible for publishing logging information to
  various preferred destinations.
- **layouts**: responsible to format logging information in different
  styles.

# Architecture

There are two type of objects available with Log4j framework.

- **Core Objects**: these are mandatory objects of the framework and
  required to use the framework.
- **Support Objects**: These are optional objects of the framework and
  support core objects to perform addition but important tasks.

## Core objects

### Logger object

Capturing logging information and they are stored in a namespace
hierarchy.

### Layout object

human readable and reusable.

### Appender object

publishing logging information to various preferred destinations such as
a **database**, **file**, **console**, UNIX Syslog etc.

![log4j-architecture](log4j/log4j-arch.jpg)

## Support objects

### Level object

The Level object defines the granularity and priority of any logging
information. There are seven levels of logging defined within the API:
OFF, DEBUG, INFO, ERROR, WARN, FATAL, and ALL.

### Filter object

The Filter object is used to analyze logging information and make
further decisions on whether that information should be logged or not.

### Object Renderer

The ObjectRenderer object is specialized in providing a String
representation of different objects passed to the logging framework.
This object is used by Layout objects to prepare the final logging
information.

### Log Manager

The LogManager object manages the logging framework. It is responsible
for reading the initial configuration parameters from a system-wide
configuration file or a configuration class.

# Configuration

- https://logging.apache.org/log4j/log4j-2.0/manual/configuration.html

## Introduction

Configuring log4j involves assigning the Level, defining Appender, and
specifying Layout objects in a configuration file.

The log4j.properties file is a log4j configuration file which keeps
properties in key-value pairs. By default, the LogManager looks for a
file named log4j.properties in the CLASSPATH.

You can specify a different location for the properties file using a JVM
option:

`-Dlog4j.configurationFile=file:///Users/sont/repo/postage-stamp-kstream/src/test/resources/log4j2-test.xml`

## Dynamically change logging level

The `Configurator.setAllLevels(String, Level)` method sets the level of
the given named logger and all child loggers. Recall that in Log4j,
loggers are hierachical. If you have the loggers com.foo.a, com.foo.b,
and com.foo.c, and you call setAllLevels("com.foo", Level.DEBUG) then
all the loggers I listed will be set to DEBUG as will "com.foo". A
logger "com.bar" will remain as is.

The method `Configurator.setLevel(Map<String, Level>)` will set each
named logger to its Level from the map. No child loggers will be
affected unlike setAllLevels(String, Level).

The method `Configurator.setLevel(String, Level)` sets the named logger
to the given level without affecting child loggers (unlike
setAllLevels(String, Level)).

Finally, `Configurator.setRootLevel(Level)` sets the level of the root
logger to the given level without affecting child loggers. The root
logger is the topmost logger with a name of "" (the empty string).

## `packages` attribute is deprecated

- https://logging.apache.org/log4j/2.x/manual/configuration.html#ConfigurationSyntax
    + Instead of using this attribute to discover the plugins.
    + The plugins should be processed with the Log4j annotation
      processor.

# Layouts

## JSON Template

- https://logging.apache.org/log4j/2.x/manual/json-template-layout.html

# References

[home]: https://logging.apache.org/log4j/2.x/
[log4j]: https://en.wikipedia.org/wiki/Log4j
[configuration]: https://logging.apache.org/log4j/2.x/manual/configuration.html
