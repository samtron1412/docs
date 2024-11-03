[TOC]

# Overview

- http://ant.apache.org/

Apache Ant is a Java based build tool from Apache Software Foundation.
- Apache Ant's build files are written in XML and they take advantage of
  being open standard, portable and eaasy to understand.
- ANT stands for Another Neat Tool.

Features
- Automate and simplify following tasks:
    + Compiling the code
    + Packaging the binaries
    + Deploying the binaries to the test server
    + Testing the changes
    + Copying the code from one location to another

## History

- Ant was created by James Duncan Davidson (the original author of
  Tomcat).
- It was originally used to build Tomcat, and was bundled as a part of
  Tomcat distribution.
- Ant was promoted as an independent project in Apache in the year 2000.

# User Manual and Tutorials

- https://ant.apache.org/manual/index.html
- Tutorials
    + https://jenkov.com/tutorials/ant/ant-tutorial.html
    + https://www.vogella.com/tutorials/ApacheAnt/article.html

# Build Files

Typically, Ant's build file, called `build.xml` should reside in the
base directory of the project.
- However, there is no restriction on the file name or its location.
- You are free to use other file names or save the build file in some
  other location.

```xml
<?xml version="1.0"?>
   <project name="Hello World Project" default="info">

   <target name="info">
      <echo>Hello World - Welcome to Apache Ant!</echo>
   </target>

</project>
```

## XML element `project`

```xml
<project name="Hello" default="default-target" basedir="root-folder">
```

It has three attributes

| Attributes | Description                                                                                                                                   |
| -          | -                                                                                                                                             |
| name       | (Optional) The name of the project.                                                                                                           |
| default    | (Mandatory) The default target. A project may contain many targets. This attribute pecifies which target should be considered as the default. |
| basedir    | (Optional) The base directory (or) the root folder for the project.                                                                           |

## A target

A target is a collection of tasks that you want to run as one unit.
- Targes can have dependency on other targets.

```xml

<target name="deploy" depends="package">
  ....
</target>

<target name="package" depends="clean,compile">
  ....
</target>

<target name="clean" >
  ....
</target>

<target name="compile" >
  ....
</target>
```

The target element has the following attributes:

| Attributes  | Description                                                                                                                                                    |
| -           | -                                                                                                                                                              |
| name        | (Required) The name of the target.                                                                                                                             |
| depends     | (Optional) Comma separated list of all targets that this target depends on.                                                                                    |
| description | (Optional) A sshort description of the target.                                                                                                                 |
| if          | (Optional) Allows the execution of a target based on the trueness of a conditional attribute.                                                                  |
| unless      | (Optional) Adds the target to the dependency list of the specified Extension Point. An Extension Point is similar to a target, but it does not have any tasks. |

## Property Task

Ant build files are written in XML, which does not allow declaring
variables. However, it would be useful if Ant allowed declaring
variables such as project name, project source directory, etc.
- Ant uses the `property` element which allows you to specify
  properties. This allows the properties to be changed from one build to
  another or from one environment to another.
- Properties are immutable in a build, when the property is set, it
  cannot modify after that in the same build. So the order of defining
  properties is important.
- By default, Ant provides the following pre-defined properties that can
  be used in the build file:

| Properties                  | Description                                                                                  |
| -                           | -                                                                                            |
| ant.file                    | The full location of the build file.                                                         |
| ant.version                 | The version of the Apache Ant                                                                |
| basedir                     | The base directory of the buld, as specified in the basedir attribute of the project element |
| ant.java.version            | The version of the JDK                                                                       |
| ant.project.name            | The name of the project, as specified in the name attribute of the project element           |
| ant.project.default-target  | The default target of the current project                                                    |
| ant.project.invoked-targets | Comma separated list of the targets that were invoked in the current project                 |
| ant.core.lib                | The full location of the Ant jar file                                                        |
| ant.home                    | The home directory of Ant installation                                                       |
| ant.library.dir             | The home directory for Ant library files - typically ANT_HOME/lib folder.                    |

Users can define additional properties using the `property` element.

```xml
<?xml version="1.0"?>
<project name="Hello World Project" default="info">

   <property name="sitename" value="www.tutorialspoint.com"/>
   <target name="info">
      <echo>Apache Ant version is ${ant.version} - You are at ${sitename} </echo>
   </target>

</project>
```

### Property Files

Setting properties directly in the build file is finie. However, for a
large project, it makes sense to store the properties in a separate
property file.
- It allows you to reuse the same build file, with different property
  settings for different execution environment. DEV, TEST, PROD
- It is useful when you do not know the values for a property up-front.
  This allows you to perform the build in other environments where the
  property value is known.

The property file usually is named `build.properties` and is placed
along-side the `build.xml` file.
- Multiple build properties files based on the deployment environemnts:
`build.properties.dev`, `build.properties.test`
- Example for `build.properties`

```xml
# The Site Name
sitename=www.tutorialspoint.com
buildversion=3.3.2
```

## Data Types

## Tasks

- https://ant.apache.org/manual/Tasks/

### taskdef and typedef

- https://ant.apache.org/manual/Tasks/taskdef.html
    + Refer to `typedef` for details
    + https://ant.apache.org/manual/Tasks/typedef.html
- Adds a task definition to the current project, such that this new task
  can be used in the current project.

### copy

- https://ant.apache.org/manual/Tasks/copy.html

### junit

- https://ant.apache.org/manual/Tasks/junit.html
