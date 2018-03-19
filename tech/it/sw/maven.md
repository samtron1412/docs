[TOC]

# Overview

# Tips and Tricks

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
