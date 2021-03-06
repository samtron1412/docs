[TOC]

# Overview

# User Guide

## Build

`mvn clean package`

## plugins vs pluginManagement

- https://stackoverflow.com/questions/10483180/maven-what-is-pluginmanagement
- pluginManagement: will be inherited in child modules

# Tips and Tricks

## Add version tag for plugins


## Specify the source version of Java

By default, Maven assumes the code using JDK 1.5. You need to add the
maven-compiler-plugin to your build plugins, to tell it to use 1.8

```java
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

# References

[home]: https://maven.apache.org/
[tutorial]: https://www.tutorialspoint.com/maven/index.htm
