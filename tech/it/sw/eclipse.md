[TOC]

# Overview


# Plugins

- StartExplorer
- Eclipse Color theme
- Moonrise theme
- EditBox of Nodeclipse
- Vrapper
- Eclipse Quicksearch

# Keyboard Shortcuts

## Eclipse Shortcut for Quick Navigation

In this section we will see some eclipse keyboard shortcut which helps
to quickly navigate within file and between file while reading and
writing code in Eclipse.

1) **Ctrl + Shift + T** for finding class even from jar

This keyboard shortcut in Eclipse is my most used and favorite shortcut.
While working with high speed trading system which has complex code I
often need to find classes with just blink of eye and this eclipse
keyboard shortcut is just made for that. No matter whether you have
class in your application or inside any JAR, this shortcut will find it.

2) **Ctrl + Shift + R** for finding any resource (file) including config
   xml files

This is similar to above Eclipse shortcut with only difference that it
can find out not only Java files but any files including xml, configs
and many others, but this eclipse shortcut only finds files from your
workspace and doesn’t dig at jar level.

7) **Ctrl + o** for quick outline going quickly to method
9) **Alt + right** and **Alt + left** for going back and forth while editing.
12) **Alt + Shift + W** for show in package explorer
13) **Ctrl + Shift + Up and down** for navigating from member to member (variables and methods)
15) **Ctrl + k** and **Ctrl + Shift +K** for find next/previous
24) Go to a type declaration: **F3**, This Eclipse shortcut is very useful to see function definition very quickly.
- **CTRL + SHIFT + >** : GO TO MATCHING TAG

## Eclipse Shortcut for Editing Code

These Eclipse shortcuts are very helpful for editing code in Eclipse.

3) **Ctrl + 1** for quick fix

This is another beautiful Eclipse shortcut which can fix up any error
for you in Eclipse. Whether it’s missing declaration, missing semi colon
or any import related error this eclipse shortcut will help you to
quickly short that out.

4) **Ctrl + Shift + o** for organize imports

Another Eclipse keyboard shortcut for fixing missing imports.
Particularly helpful if you copy some code from other file and what to
import all dependencies.

5) **Ctrl + /** for commenting, un commenting lines and blocks
6) **Ctrl + Shift + /** for commenting, un commenting lines with block comment
8) Selecting class and pressing **F4** to see its Type hierarchy
10) **Ctrl + F4** or **Ctrl + w** for closing current file
11) **Ctrl+Shirt+W** for closing all files.
14) **Ctrl + l** go to line
16) Select text and press **Ctrl + Shift + F** for formatting.
17) **Ctrl + F** for find, find/replace
18) **Ctrl + D** to delete a line
19) **Ctrl + Q** for going to last edited place

## Miscellaneous Eclipse Shortcuts

These are different Eclipse keyboard shortcuts which doesn’t fit on any category but quite helpful and make life very easy while working in Eclipse.

20) **Ctrl + T** for toggling between super type and subtype
21) Go to other open editors: **Ctrl + E**.
22) Move to one problem (i.e.: error, warning) to the next (or previous) in a file: **Ctrl +.** For next, and **Ctrl +,** for previous problem
23) Hop back and forth through the files you have visited: **Alt + ←** and **Alt + →**, respectively.
25) **CTRL+Shift+G**, which searches the workspace for references to the selected method or variable
26) Ctrl+Shift+L to view listing for all Eclipse keyboard shortcuts.
27) Alt + Shift + j to add javadoc at any place in java source file.
28) CTRL+SHIFT+P to find closing brace. Place the cursor at opening brace and use this.
29) Alt+Shift+X, Q to run Ant build file using keyboard shortcuts in Eclipse.
30) Ctrl + Shift +F for Autoformating.
31) Maximize active view or editor: Ctrl + M


# Project structure

```
repo
- src
    + pkg1
        * Main.java
        * Something.java
    + pkg2
        * Hey.java
- resources
    + icon.png
```

- Get resources
```java
URL url = Main.class.getResource("/resources/icon.png");
```

# Tips and Tricks

## Generate source code

- Source - Generate ...
- Generate Getters, Setters: alt + shift + s, r
    + Rename: alt + shift + r
    + Delete: alt + shift + q, o

## Different options of exporting runnable jar library handling

1. **Extract required libraries into JAR** - Extracts the actual .class
   files from the libraries your app uses and puts those .class files
   inside the runnable JAR. So, the runnable JAR will not only contain
   the .class files of your application, but also the .class files of
   all the libraries your application uses.
2. **Package required libraries into JAR** - Puts the actual JAR files
   of the libraries into your runnable JAR. Normally, a JAR file within
   a JAR file cannot be loaded by the JVM. But Eclipse adds special
   classes to the runnable JAR to make this possible.
3. **Copy required libraries into sub folder next to JAR** - Keeps the
   library JARs completely separate from the runnable JAR, so the
   runnable JAR will only contain the .class files of your application.

Option #2 is convenient because it packages everything neatly into a
single JAR, and keeps the library JARs separated from your application's
.class files.

However, a downside to packaging everything inside of a single JAR
(options #1 and #2) is that, if you update your application, then the
user will have to download more data to update the application. If the
JARs are kept separate, then the user would only have to download the
JAR that contains your application code, instead of a single, massive
JAR that contains your application code and all the library code.

# References

[source]: http://javarevisited.blogspot.com/2010/10/eclipse-tutorial-most-useful-eclipse.html#ixzz3El9zbjJu
