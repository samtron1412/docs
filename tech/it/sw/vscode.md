[TOC]

# Overview

- live server
- html, css, JavaScript

# User Guide

## Debugging

- https://code.visualstudio.com/docs/editor/debugging

## Tasks

- https://code.visualstudio.com/docs/editor/tasks
- Integrate with external tools via Tasks.

## Keyboard shortcuts (key bindings/mappings)

### macOS

- Open the keyboard shortcuts view
    + `Cmd+Shift+P` and search for keyboard shortcuts
    + `Cmd+K,Cmd+S`
- `Option+Cmd+K` to record keys or type the search phrase: `"cmd+b"`

#### Useful shortcuts or feature to know

- Toggle side bar/panel view: `Cmd+b`
- Toggle bottom bar/panel view: `Cmd+j`
- `shift + cmd + p`: search commands
    + Toggle minimap
- Open file structure view: `Cmd+Shift+E`
- Open Cline AI-agent view: `Cmd+Shift+'`
    + Toggle between Plan and Act mode: `Cmd+Shift+A`
- `cmd + p`: search files, `:` go to line, `@` go to symbols
- `shift + cmd + .`: dropdown for the last breadcrumb
- `shift + cmd + ;`: select the last breadcrumb without dropdrown
- `shift + cmd + o`: navigate between symbols inside a file
- `cmd + t`: open symbols by names across files
- `cmd + f12`: jumping to the implementation of the symbol

## Zen mode with less distraction

- To toggle Zen mode: `Cmd + K, Z`
- Zen mode can be configured in Preferences
    + `Cmd + ,`, search for `zen mode`
    + Good setting: center layout, full screen, hide activity bar (side
      bar), show line numbers, show status bar, restore, show tabs: none

## Render Whitespaces

- `Cmd + Shift + P` then type `Render Whitespace`

# Tips and tricks

## Change File Type / Language Mode

- Set a file type or language to a file
    + `shift + cmd + p` to search `Change Language Mode` command

## Linters

- Only add folders of the same project to a workspace
    - Multiple projects in a workspace can interfere with linters and
      other error checking tools

# Troubleshooting

## Configure Java Runtime (JDK version)

- https://code.visualstudio.com/docs/java/java-project#_configure-runtime-for-projects
- Command Palette (`Cmd+Shift+P`), then type `Java configure runtime`

## bin folder is generated for Gradle packages

- Edit `.classpath` in that project and change `bin`  to `build`
- Or using command palette (`Cmd+Shift+P`) and then type: `Java
  configure classpath` and then change the classpath.

## Stuck / Slow at Java Initialize Workspace

- Disable `java.gradle.buildServer.enabled` setting
    + https://github.com/redhat-developer/vscode-java/issues/3357#issuecomment-1778443064
    + Note that this setting can be configured in multiple places: User,
      Remote, Workspace, etc. so try to disable all of them.

# References

[homepage]: https://code.visualstudio.com/?wt.mc_id=DX_841432
[wiki]: https://en.wikipedia.org/wiki/Visual_Studio_Code
