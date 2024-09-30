[TOC]

# Overview

# Troubleshooting

## Taking up so much memory and heap size

- https://intellij-support.jetbrains.com/hc/en-us/community/posts/6746377604498-The-IDE-is-really-taking-up-too-much-memory
- Solutions:
    + Change the boot Java runtime of the IDE
        * https://www.jetbrains.com/help/webstorm/switching-boot-jdk.html
        * Use vanilla/nomod version or custom version such as OpenJDK.
        * Remove `idea.jdk` file in `~/.config/JetBrains/.../idea.jdk`
          to use the default again.

# Tips and Tricks

## Remote development

- CodeWithMe is more stable than SSH development as of 2024-09.
- For CodeWithMe
    + IdeaVim plugin should only be installed in Client side, disable on
      the host side.

## Assign file types to file name patterns

- `Preferences - Editor - File Types`

## Useful Actions

- Search Actions `Cmd + Shift + A` or Search everything
- Override file type

## Add a new jar or directories to classpath

### Method 1 - Using Project Structure

- Open project structure (File -> Project Structure)
- Go to the "Modules" on the left
- Go to the "Dependencies" tab of that module
- Click "+" and choose "JARs or directories"
- In the dialog with "Choose Categories of Selected File", choose
  Classes (even if it's properties), press OK and OK again

### Method 2 - Using Run/Debug Configuration

- Run -> Edit Configurations
- Add VM options or add environment variables

# References
