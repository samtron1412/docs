[TOC]

# Overview

Sublime Text is a proprietary text editor with a Python application
programming interface.

# Basic Concepts

## Glossary

| Terms     | Description                                                                                                                                                                                                                                                                                                                                            |
| -         | -                                                                                                                                                                                                                                                                                                                                                      |
| buffer    | Data of a loaded file and additional metadata, associated with one or more views. The distinction between buffer and view is technical. Most of the time, both terms can be used interchangeably.                                                                                                                                                      |
| view      | Graphical display of a buffer. Multiple views can show the same buffer                                                                                                                                                                                                                                                                                 |
| plugin    | A feature implemented in Python, which can consist of a single command or multiple commands. It can be contained in one .py file or many .py files                                                                                                                                                                                                     |
| package   | This term is ambiguous in the context of Sublime Text, because it can refer to a Python package (unlikely), a folder inside `Packages` or a .sublime-package file. Most of the time, it means a folder inside `Packages` containing resources that belong together, which build a new feature or provide support for a programming or markup language. |
| panel     | An input/output widget, such as a search panel or the output panel.                                                                                                                                                                                                                                                                                    |
| overlay   | An input widget of a special kind. For example, Goto Anything is an overlay                                                                                                                                                                                                                                                                            |
| file type | In the context of Sublime Text, file type refers to the type of file as determined by the applicable `.tmLanguage` syntax definition. However, this is an ambiguous term, and in some instances it could also be used with the broader meaning it has in technical texts.                                                                              |

## The Data Directory

| Platform | Location                                       |
| -        | -                                              |
| Linux    | `~/.config/sublime-text-3`                     |
| Windows  | `%APPDATA%\Sublime Text 3`                     |
| OS X     | `~/Library/Application Support/Sublime Text 3` |

## The Packages Directory

- This is a key directory located under the data directory. All
resources for supported programming and markup languages are located
here.
- You can access the packages directory by means of an API cal
`sublime.packages_path()`.

## The User package

- `Packages/User` is a catch-all directory for custom plugins, snippets,
macros, etc.
- Consider it your personal area in the packages folder.
- It will contain most of your personal application or plugin settings.
- Updates to Sublime Text will never overwrite the contents of
`Packages/User`.

## Sublime Text is Programmable

- Sublime Text enables users with programming skills to add their own
features to the editor.
- Sublime Text exposes its internals via an Application Programming
Interface (API) that programmers can interact with using the Python
programming language.
- An embedded Python interpreter is included in the editor. The embedded
interpreter is useful to inspect the editor's setting and to quickly
test API calls while developing plugins.
- Sublime Text and plugins output information to a console. To open the
console, press **Ctrl+`**.

# Editing

The `Edit, Selection, Find and Goto` menus are good places to look for
handy editing tools.

## Multiple selections

- Use Multiple Selections to rename variables quickly.
    + Here `Ctrl+d` is used to select the next occurrence of the current
    word.
    + If you want to skip the current instance, press `Ctrl+k, Ctrl+d`.
    + If you go too far, press `Ctrl+u` to deselect the current
    instance.
- Make batch edits with Multiple Selections.
    + `Ctrl+l` expands the selections to the end of the line.
    + Here `Ctrl+Shift+l` is used to split a selection into lines, and
    each line is then edited simultaneously.
    + You can copu multiple selected lines to a separate buffer, edit
    them there, select the content again as multiple lines and then
    paste them back in the first buffer.
- Using with Vintageous:
    + From Insert mode:
        * Select by using the way of Sublime Text
        * `Ctrl+Shift+l` and keep editing
    + From Visual mode:
        * Type `gh` to go to Select mode of Vintageous
        * `Ctrl+Shift+l` to split the selection into lines
        * Type `i` to go to Insert mode

## Column Selection

- You can select a rectangular area of a file.

| OS      | Key binding                                      |
| -       | -                                                |
| Linux   | `Alt+Shift+k` and `Alt+Shift+j` (k: up, j: down) |
| Windows | `Ctrl+Alt+Up` and `Ctrl+Alt+Down`                |

## Other Ways of Selecting Text

All available options can be found under Selection menu.

- Select subwords : `Alt+Shift+<arrow>`
- Expand selecton to brackets: `Ctrl+Shift+m`
- Expand selection to indentation: `Ctrl+Shift+j`
- Expand selection to scope: `Ctrl+Shift+Space`

## Transposing things

- Put the cursor between two letters and use `Ctrl+t` to transpose them.
- Select two areas (words, lines, phrases, etc.) and use `Ctrl+t`

# Search and Replace

- Sublime Text uses the Perl Compatible Regular Expressions (PCRE)
engine from the Boost library to power regular expressions in search
panels. [Boost library documentation for regular expressions]
[boost-regex-doc]
- In search and replace box also supports special symbols called
`format strings` that look similar to regular expressions. [Boost
library documentation for format strings][boost-format-strings-doc]

## Single File

### General search

| Action                     | Key binding |
| -                          | -           |
| Open search panel          | Ctrl+f      |
| Toggle regular expressions | Alt+r       |
| Toggle case sensitivity    | Alt+c       |
| Toggle exact match         | Alt+w       |
| Find next                  | Enter       |
| Find previous              | Shift+Enter |
| Find all                   | Alt+Enter   |

### Incremental Search

| Action                        | Key binding                                                                                                        |
| -                             | -                                                                                                                  |
| Open incremental search panel | Ctrl+i                                                                                                             |
| Toggle regular expressions    | Alt+r                                                                                                              |
| Toggle case sensitivity       | Alt+c                                                                                                              |
| Toggle exact match            | Alt+w                                                                                                              |
| Find next                     | Enter (select the next match in the file and dismiss the search panel, so you cannot use `Shift+Enter` after this) |
| Find previous                 | Shift+Enter (it only has effect when the search panel is opened)                                                   |
| Find all                      | Alt+Enter                                                                                                          |

### Replacing text

| Action             | Key binding    |
| -                  | -              |
| Open replace panel | Ctrl+h         |
| Replace next       | Ctrl+Shift+h   |
| Replace all        | Ctrl+Alt+Enter |

### Goto Anything search

`Ctrl+p` -> type something to specify the file -> `#` -> type something
to search in the file.

### Search-related key bindings

These key bindings work when the search panel is hidden.

| Action                                       | Key binding |
| -                                            | -           |
| Search forward using most recent pattern     | f3          |
| Search backward using most recent pattern    | Shift+f3    |
| Select all matches using most recent pattern | Alt+f3      |

These key bindings effect `f3` and `shift+f3` key bindings.

| Action                          | Key binding  |
| -                               | -            |
| Search using current selection  | Ctrl+e       |
| Replace using current selection | Ctrl+Shift+e |

### Multiline search

You can type in multiline searjch patterns into search panels. To enter
newline character, press `Ctrl+Enter`

## Multiple Files

The search panel for searching multiple files is known as **Find in
Files**

### Searching

| Action                     | Key bindings |
| -                          | -            |
| Open Find in Files         | Ctrl+Shift+f |
| Toggle regular expressions | Alt+r        |
| Toggle case sensitivity    | Alt+c        |
| Toggle exact matches       | Alt+w        |
| Searching                  | Enter        |

### Search Filters

The **Where** field in Find in Files limits the search scope.

- Adding individual directories: `/home/abc/docs/`
- Adding/excluding files based on wildcards: `*.md` or `-*.md`
- Adding symbolic locations: `<open folders>`, `<open files>`,
`<current file>`.

It is also possible to combine filters using commas. You can combine
filters in any order.

### Results

- Show in separate view (Use Buffer)
- Show context

Navigating Results

| Action              | Key binding |
| -                   | -           |
| Next match          | f3          |
| Previous match      | Shift+f3    |
| Open next match     | f4          |
| Open previous match | Shift+f4    |

# File Navigation and File Management

## Goto Anything

Use Goto Anything to quickly navigate between files, even in the
largest projects.

| Action                                        | Key binding |
| -                                             | -           |
| Open Goto Anything                            | Ctrl+p      |
| Pin current item and close Goto Anything      | Enter       |
| Pin current item (do not close Goto Anything) | Right arrow |
| Close Goto Anything                           | Esc         |

- As you type into Goto Anything's input area, names of files in the
current project will be searched, and a preview of the best match will
be shown.
- This preview is `transient`; that is, it won't become the actual
active view until you perform some operation on it.
- You will find transient views in other situations, for example, after
clicking on a file in the sidebar.

### Operators

Goto Anything has several operators. All of them can be used on their
own or after the search term. If you use it by their own, it will apply
on the current view. If you use it after the search term, it will apply
on the active item in the transient.

- `@symbol`: searches the active file for the symbol named `symbol`.
    + Symbols usually include class and function names.
    + Symbol searches will only yield results if the active file type
    has symbols defined for it.
    + Symbol are defined in `.tmLanguage` files.
    + For more information about symbols, see [Symbols](#symbols)
- `#term`: performs a fuzzy search of the `term` search term and
highlights all matches.
- `:line_number`: goes to the specified `line_number`, or to the end of
the file if `line_number` is larger than the file's line count.

| Symbols | Key binding          |
| @       | Ctrl+r               |
| #       | Ctrl+, (not default) |
| :       | Ctrl+g               |

## Sidebar

- The sidebar provides an overview of the active project.
- Files and folders in the sidebar will be available in Goto Anything
and project-wide actions like project-wide searches.

| Action                         | Key binding    |
| -                              | -              |
| Toggle side bar                | Ctrl+k, Ctrl+b |
| Give the focus to the side bar | Ctrl+0 (zero)  |
| Return the focus to the view   | Esc            |
| Navigate side bar              | Arrow keys     |

Files opened from the sidebar create semi-transient views. Unlike
transient views, semi-transient views show up as a new tab. When a new
semi-transient view is opened, any other pre-existing semi-transient
view in the same pane gets automatically closed.

## Projects

- Project group sets of files and folders to keep your work organized.
- There is always an active project. If you haven't created one, an
implicit one is created by Sublime Text.
- Projects in Sublime Text are made up of two files: the sublime-project
file, `.sublime-project`, which contains the project definition, and the
sublime-workspace file, `.sublime-workspace`, which contains user
specific data, such as the open files and the modifications to each.
- As a general rule, the sublime-project file would be checked into
version control, while the sublime-workspace file would not, but always
be mindful of what you store in them.
- Projects can define settings applicable to that project only.
- You can open a project from the command line by passing the
`.sublime-project` file as an argument to the `subl` command line.
- You can add and remove folders to/from a project using the **Project**
menu or the sidebar's context menu.
- To save a project, go to **Project** -> **Save Project As...**
- You can switch projects by `Ctrl+Alt+p`

### The `.sublime-project` Format

Project metadata in `.sublime-project` files is split across three top
sections:

- `folders`: for the included folders
- `settings`: for project-specific settings
- `build_systems`: for project-specific build systems

```
{
    "folders":
    [
        {
            "path": "src",
            "folder_exclude_patterns": ["backup"]
        },
        {
            "path": "docs",
            "name": "Documentation",
            "file_exclude_patterns": ["*.css"]
        }
    ],
    "settings":
    {
        "tab_size": 8
    },
    "build_systems":
    [
        {
            "name": "List",
            "cmd": ["ls"]
        }
    ]
}
```

#### Folder options

| Option                  | Description                                                                                    |
| -                       | -                                                                                              |
| path                    | Required. The path may be relative to the project directory,                                   |
| name                    | Optional. If present, it will appear in the side bar                                           |
| folder_exclude_patterns | Optional. List of wildcards. folders matching the wildcards will be excluded from the project. |
| folder_include_patterns | Optional. List of wildcards. Folders matching the wildcards will be included in the project.   |
| file_exclude_patterns   | Optional. List of wildcards. Files matching the wildcards will be excluded from the project.   |
| file_include_patterns   | Optional. List of wildcards. File matching the wildcards will be included in the project.      |

#### Settings

- Project-specific settings override use settings, but not
syntax-specific settings.
    + Customization: [settings](#settings_1)
    + Reference: [settings](#settings_2)

#### Build Systems

Build systems included in a `.sublime-project` file will show up in the
`Tools -> Build Systems` menu. [Build Systems](#build-systems_1)

### Other settings related to the sidebar and projects

- `binary_file_patterns`: A list of wildcards. Files matching these
wildcards will show up in the side bar, but will be excluded from Goto
Anything and Find in Files.
    + These files are not indexed
    + Accept folder paths: `"binary_file_patterns": ["node_modules/"]`
- `index_exclude_patterns`
    + These files are not indexed
    + Does not accept folder paths, only file paths:
    `"index_exclude_patterns": ["*.log"]`
- `folder_exclude_patterns/file_exclude_patterns`: these files will not
show up in the side bar.

### Workspaces

- Workspaces can be seen as different views into the same project. For
example, you may want to have only a few selected files open while
working on some feature. Or perhaps you use a different pane layout when
you're writing tests, etc. Workspaces help in these situations.
- Workspaces behave very much like projects.
- To create a new workspace: `Project -> New Workspace for Project`.
- To save the active workspace: `Project -> Save Workplace As...`.
- To switch between workspaces: `Ctrl+Alt+p`, exactly as you do with
projects.

### Panes

- Panes are groups of views.
- Using [Origami][origami-pkg] package to work with panes.

# Build systems

Build systems let you run your files through external programs like
make, tidy, interpreters, etc without leaving Sublime Text, and see the
output they generate.

## Basics

### Parts of a Build System

- Simple build systems only require a `.sublime-build` file.
- Advanced build systems consist of up to three parts:
    + a `.sublime-build` file (configuration data in JSON format)
    + optionally, a custom Sublime Text command (Python code) driving
    the build process
    + optionally, an external executable file (script or binary file)

### File format of `.sublime-build` files

| Format   | JSON (with comments)            |
| -        | -                               |
| Location | Any under the `Packages` folder |

Each `.sublime-build` file is normally associated with a specific scope
corresponding to a file type (for example, `source.python`)

```
{
    "cmd": ["python", "-u", "$file"],
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "selector": "source.python"
}
```

### Flow of a build system

1. Run the build task (e.g. `Ctrl+b`)
2. A Sublime Text command receives the configuration data specified in
the `.sublime-build` file.
3. This command then builds the files. Often, it calls an external
program. By default, the command used in build systems is `exec`, but it
can be overriden.

### Overriding the default command for build systems

- The `exec` command implemented by `Packages/Default/exec.py`. This
command simply forwards configuration data to an external program and
runs it asynchronously.
- Using the `target` option in a `.build-system` file, it's possible to
override the `exec` command.

## Configuration

You can implement your own build system mechanism in two main ways:

1. As a custom `target` command (still using the default build system
framework)
2. As an entirely new plugin (skipping the build system framework)

### **Meta Options** in Build systems

This is a list of standard meta options that all build systems
understand.

- `target` (optional)
    + a `WindowCommand`. Defaults to `exec`
    (`Packages/Default/exec.py`). This command receives all the target
    command arguments specified in the `.sublime-build` file (as
    `**kwargs`)
    + Used to override the default build system command. Note that if
    you choose to override the default command for build systems, you
    can add any number of extra options to the `.sublime-build` file.
- `selector` (optional)
    + Used when `Tools -> Build System -> Automatic` is set to `true`.
    Sublime Text uses this scope selector to find the appropriate build
    system for the active view.
- `windows`, `osx` and `linux` (optional)
    + Used to selectively apply options by OS. OS-specific values
    override defaults. Each of the listed items accepts a dictionary of
    options.
- `variants` (optional)
    + A list of dictionaries of options. Variant names will appear in
    the Command Palette for easy access if the build system's selector
    matches for the active view.
    + Using variants, it's possible to specify multiple build system
    tasks in the same `.sublime-build` file.
- `name` (optional)
    + Only valid inside a variant.
    + Identifies a build system task.

### Target command arguments

- `target` setting will overrides the default `exec` command with any
other command of your choice, a build system may contain any number of
custom arguments that the new `target` command accepts.
- Examples:
    + [MarkdownBuildCommand][markdown-build-command]: `target:
    "markdown_build"`
    + [Golang sublime-build][golang-sublime-build]

### Platform-specific options

```
{
    "cmd": ["ant"],
    "file_regex": "^ *\\[javac\\] (.+):([0-9]+):() (.*)$",
    "working_dir": "${project_path:${folder}}",
    "selector": "source.java",

    "windows": {
        "cmd": ["ant.bat"]
    }
}
```

### Variants

```
{
    "selector": "source.python",
    "cmd": ["python2", "-u", "$file"],

    "variants": [
        { "name": "List Python Files",
          "cmd": ["ls -l *.py"],
          "shell": true
        },

        { "name": "Word Count (current file)",
          "cmd": ["wc", "$file"]
        },
    ]
}
```

### Capturing Build System Results

When build systems output text to a results view, it's possible to
capture results data in order to enable result navigation.

Set the following view settings in a result view if you want to enable
results navigation:

- `result_file_regex`: A Perl-style regular expression to capture up to
four fields of error information from a results view.
    + namely; **filename**, **line number**, **columns number** and
      **error message**.
    + Use groups in the pattern to capture this information.
    + The **filename** filed and the **line number** field are required.
-`result_line_regex`: If `result_file_regex` doesn't match but
`result_line_regex` exists and does match on the current line, walk
backwards through the buffer until a line matching `result_file_regex`
is found, and use the two matches to determine the file and line to go
to.
- `result_base_dir`: Used to find files where results occur.

In `exec` command the value of `file_regex`, `line_regex`, `working_dir`
will set for `result_file_regex`, `result_line_regex`, and
`result_base_dir`.

When result data is captured, you can navigate to results in your
project's files with `f4` and `shift+f4`. If available, the captured
error message will be displayed in the status bar.

### Build System Variables

Build system expand the following variables in `.sublime-build` files
(apply only to `cmd`, `shell_cmd`, and `working_dir`):

| `$file_path`         | The directory of the current file, e.g., C:\Files              |
| -                    | -                                                              |
| `$file`              | The full path to the current file, e.g., C:\Files\Chapter1.txt |
| `$file_name`         | The name portion of the current file, e.g., Chapter1.txt       |
| `$file_extension`    | e.g., txt                                                      |
| `$file_base_name`    | Name of file category, e.g., Document                          |
| `$folder`            | The path to the first folder opened in the current project     |
| `$project`           | The full path to the current project file.                     |
| `$project_path`      | The directory of the current project file                      |
| `$project_name`      |                                                                |
| `$project_extension` |                                                                |
| `$project_base_name` |                                                                |
| `$packages`          | The full path to the Packages folder.                          |

### Placeholders for variables

Features in [Snippets](#snippets) section can be used with build system
variables. For example:

- `${project_name:Default`: return the name of the current project if
there is one, otherwise return `Default`.
- `${file/\.php/\.txt/}`: return full path of the current file and
replacing .php with .txt

### Running build systems

| `Ctrl+b`       | Run build task            |
| -              | -                         |
| `Ctrl+Shift+b` | Show select build systems |
| `f7`           | Cancel running build task |

## `exec` Command Arguments

All the options that follow are related to the `exec` command. If you
change the `target` command, these options can no longer be relied on.

- `cmd`
    + Required if `shell_cmd` is empty.
    + Overriden by `shell_cmd`.
    + Array containing the command to run and its desired arguments. If
    you don't specify an absolute path, the external program will be
    searched in your `PATH`. Ultimately, `subprocess.Popen(cmd)` is
    called.
- `shell_cmd`
    + Required if `cmd` is empty.
    + Overrides `cmd` if used.
    + A string that specifies the command to be run and its arguments.
    Ultimately, `subprocess.Popen(shell_cmd, shell=True)` is called.
- `working_dir`
    + Optional
    + Directory to change the current directory to before running `cmd`.
    The original current directory is restored afterwards.
- `encoding`
    + Optional
    + Output encoding of `cmd`. Must be a valid Python encoding.
    Defaults to `UTF-8`.
- `env`
    + Optional
    + Dictionary of environment variables to be merged with the current
    process' before passing them to `cmd`.
    + Use this option, for example, to add or modify environment
    variables without modifying your system's settings.
    + Environmental variables with be expanded.
- `shell`
    + Optional
    + If true, `cmd` will be run through the shell (`cmd.exe`,
    `bash`...)
    + If `shell_cmd` is used, this option has no effect.
- `path`
    + Optional
    + `PATH` used by the `cmd` subprocess.
    + Use this option to add directories to `PATH` without having to
    modify your system's settings.
    + Environmental variables will be expanded.
- `file_regex`
    + Optional
    + Sets the `result_file_regex` for the results view.
- `line_regex`
    + Optional
    + Sets the `result_line_regex` for the results view.
- `syntax`
    + Optional
    + If provided, it will be used to colorize the build system's
    output.

# Customization

## Settings

- Sublime Text stores configuration data in `.sublime-settings` files.
- Always place your personal settings files under `Packages/User` to
guarantee they will overriden any other conflicting settings files.
- To check the value of a setting for a particular file being edited,
use `view.settings().get("setting_name")` from the console.
- The file type of settings is `.sublime-settings`

### The settings hierarchy

- `Packages/Default/Preferences.sublime-settings`
- `Packages/AnyOtherPackage/Preferences.sublime-settings`
- `Packages/User/Preferences.sublime-settings`
- Settings from the current project
- `Packages/Python/Python.sublime-settings`
- `Packages/User/Python.sublime-settings`
- Session data for the current file
    + Sublime Text maintains session data - settings for the particular
    set of files being currently edited.
- Auto-adjusted settings

# Extensibility and Automation

## Macro

Best solution for this is recording a macro on Sublime Text and then
assigning it to a keyboard key binding. Follow these steps:

1. Create a line such as `alert('hello')` and leave the cursor right
   after letter `o`.
2. Then go to Tools > Record a Macro to start recording.
3. Press `alt+left` to go to the end of line.
4. Press `;` and hit Enter
5. Stop recording the macro by going to Tools > Stop Recording Macro
6. You can now test your macro by Tools > Playback Macro (optional)
7. Save your macro by going to Tools > Save Macro (ex: EndOfLine
   .sublime-macro)
8. Create a key binding by adding this between the square brackets in
   your in your Preferences > Key Bindings - User file:

        {
        "keys": ["super+;"], "command": "run_macro_file", "args": {"file": "Packages/User/EndOfLine.sublime-macro"}
        }

9. Now, every time you hit `Command+;`, it will magically place the
   semicolon at the end of current line and move the cursor to the next
   line. Happy coding!

## Snippets

`Tools -> New Snippet...`

- Create new snippet for your definition.
- Improve your code speed.
- Add snippet manual or through package control.

# Command Line

# Advanced Users

## Settings

## Symbols

# Package Control

## End Users

### Usage

- Install Package
    + show a list of all available packages at default channel.
- Add Repository
    + add a repository that is not included in the default channel. This
      allows users to install and automatically update packages from
      GitHub and BitBucket.
    + To add a package hosted on GitHub, enter the URL in the form
      `https://github.com/username/repo`. Don’t include .git at the end!
      BitBucket repositories should use the format
      `https://bitbucket.org/username/repository`.
- Remove Package
    + This command will remove the package folder, and the package name
      from the `installed_packages` list in `Packages/User/Package
      Control.sublime-settings`.
    + The `installed_packages` list allow Package Control to
      automatically install packages for you if you copy your
      `Package/User/` folder to other machine.
- Add channel
- Create Package File
    + For package developers.
    + Takes a package folder and generates a `.sublime-package` file
      that can be uploaded onto the web and referenced in the
      `packages.json` file for a repository.
- Create Binary Package File
    + For package developers.
    + Creates a `.sublime-package` file that does not include the source
      `.py` files, but instead the `.pyc` bytecode files. This is useful
      to distribute commercial packages. Be sure to check the resulting
      `.sublime-package` file to ensure that at least one `.py` file is
      included so that Sublime Text will load the package.
- Disable Package
- Discover Package
    + Opens up a web browser to browse
- Enable Package
    + Re-enables a package that has been disabled.
- Upgrade/Overwrite All Packages
    + This will upgrade ALL Packages, including ones that were not
      installed via Package Control.
    + If you are developing a custom copy of a package, you may not want
      to use this command.
- Upgrade Package

### Settings

The default settings can be viewed by accessing the `Preferences >
Package Settings > Package Control > Settings – Default` menu. To ensure
settings are not lost when the package is upgraded, make sure all edits
are saved to `Settings – User`.

[References](https://packagecontrol.io/docs/settings)

### Customizing Packages

#### Packed vs Unpacked

Sublime Text 3 by default, packages will be installed by placing a
.sublime-package file in the `Install Packages/` folder. Then users may
override individual files in the package by creating a folder
`Packages/{Package Name}/` and placing edited files in there.

#### Editing Unpacked Files

Editing an unpacked package's files is not a good idea unless you've
cloned the package via `Git/Hg`. This is because, by default, Package
Control will automatically upgrade packages to the newest version. This
will cause any edits to files to be **overwritten**. If you experience
this, you may wish to check out the **Backups** section to learn how to
recover your customized version of a file.

- User Package
    + The `Packages/User/` folder is the User package. It is unique in
      that it is loaded **last** by Sublime Text.
    + This allows users to place changes to `.sublime-settings` and
      `.sublime-keymap` files in this folder.
    + Sublime Text loads these files by name. Thus if a package has a
      file named `Package Control.sublime-settings` in the package, a
      file with the same name in the User package will override any of
      the settings in the original file. The same is true for key
      bindings.
- Overrides
    + If a package for Sublime Text 3 is installed as a **packed
      package**, it should be possible to directly override **individual
      non-python files**. To do this, create a `Packages/{Package
      Name}/` folder and save customized versions of the files with
      **the same name they are in the .sublime-package file**.
- Git/Hg clone
    + For complete customization of a package, it will likely be
      necessary to using a version control program, such as Git or Hg to
      clone a copy of the original package repository into the
      `Packages/` folder.
    + The best way to make customizations would be to **fork the
      original repository and clone your fork of it**. If you think your
      customizations could be useful to others, consider sending a pull
      request to have your changes merged into the original version.
    + If you've cloned it from your own fork of the repository, no
      settings need to be changed. If you clone it from the original
      repository, you will likely want to set the `ignore_vcs_packages`
      setting.
- Backups
    + If you do ever find yourself in a situation where your edits to a
      package were overwritten by Package Control, you can find a backup
      copy in the `Backup/` folder. This folder can be located by
      selecting the `Preferences > Browse Packages…` menu and then
      browsing up a folder. Backups are stored in timestamped folders.

### Syncing

You should use Git or Dropbox like service to syncing `Packages/User/`
folder. When you go to new machine let override this `User` folder and
start Sublime with Package Control will reinstall all package for you
and all configuration of Sublime also applied.

When use Git you should ignore some things:
- Package Control.last-run
- Package Control.ca-list
- Package Control.ca-bundle
- Package Control.system-ca-bundle
- Package Control.cache/
- Package Control.ca-certs/
- etc. change frequently

#### Windows

- Make soft link to `User` directory: `cmd /c mklink /D User
  $env:userprofile\path\to\User`

### Troubleshooting

#### Purging and Reinstalling

1. Select the `Preferences > Settings – User` menu entry
2. Remove `"Package Control"` from the `"ignored_packages"` setting, if
   present
3. Select the `Preferences > Browse Packages…` menu entry
4. Delete the folder named `Package Control`
5. Browse up a folder and then into `Installed Packages`
6. Delete `Package Control.sublime-package` if it exists
7. Reinstall Package Control using the [installation instructions](https://packagecontrol.io/installation)

#### Enabling Debug Log

The debug log contains extensive information about what Package Control
is doing behind the scenes, and can help to diagnose why it isn't
working properly.

1. Click the `Preferences` menu
2. Select `Package Settings`
3. Choose `Package Control`
4. Click `Settings - User`
5. Add the setting `"debug": true`
6. Save the settings file

Now when performing actions with Package Control, debug information will
be printed to the Sublime Text console. The console can be opened by
pressing **ctrl+`** or using the View > Show Console menu entry.

### Issues

Are you having trouble using Package Control? Before opening an issue,
please take the time to perform the following few steps. Properly
following directions will improve the likelyhood of your issue be
quickly resolved.

1. Check to make sure you are using the latest version of Package
   Control: run the Package Control: List Packages command from the
   command palette
2. Look at the Sublime Text Console **ctrl+`** to see if any python
   errors are listed
3. Review the list of open GitHub issues to see if the problem you are
   experiencing has been reported
4. Please do not comment on a Closed issue, but feel free to reference
   it from a new one

To provide the info necessary to help solve the issue, please generate a
debug log. To do this:

1. Open `Preferences > Package Settings > Package Control > Settings -
   User`
2. Add "debug": true to enable the debug log
3. Restart Sublime Text
4. Perform the command or operation you are having trouble with
5. Copy the full contents of the Sublime Text Console
6. Comment on an existing Open issue, or create a new on

[Open issues on GitHub](https://github.com/wbond/package_control/issues?state=open)

## [Package Developers](https://packagecontrol.io/docs#Package_Developers)

### Submitting a Package

### Messaging

### Dependencies

### Creating Package Files

### Renaming a Package

### Channels and Repositories

### Events

### Code


# Sublime 3 Packages

## SmartMarkdown

### Move between headlines.

- Use `Ctrl+c Ctrl+n` to move to the next headline (any level); `Ctrl+c
  Ctrl+p` to the previous one, for Mac. (`Ctrl+; Ctrl+n` and `Ctrl+;
  Ctrl+p` for Windows and Linux)
- Use `Ctrl+c Ctrl+f` to move to the next headline (same level or higher
  level); `Ctrl+c Ctrl+b` to the previous one, for Mac. (`Ctrl+; Ctrlf`
  and `Ctrl+; Ctrl+b` for Windows and Linux)

### Adjust headline level Added by David Smith.

`Super+Shift+,` for decreasing and `Super+Shift+.` for increasing
headline levels.

## Vintageous

- Exit Insert mode: `ESC/j j`
- Visual mode:
    + visual normal mode `command mode -> v`
    + visual line mode `command mode -> V`

### Inserting text

- `i`   Insert before cursor
- `I`   Insert before line
- `a`   Append after cursor
- `A`   Append after line
- `o`   Open a new line after current line
- `O`   Open a new line before current line
- `r`   Replace one character
- `R`   Replace many characters

### Motion

- `h`   Move left
- `j`   Move down
- `k`   Move up
- `l`   Move right
- `w`   Move to next word
- `W`   Move to next blank delimited word
- `b`   Move to the beginning of the word
- `B`   Move to the beginning of blank delimted word
- `e`   Move to the end of the word
- `E`   Move to the end of Blank delimited word
- `{`   Move a paragraph back
- `}`   Move a paragraph forward
- `0`   Move to the begining of the line
- `$`   Move to the end of the line
- `gg/1G`   Move to the first line of the file
- `G`   Move to the last line of the file
- `nG`  Move to nth line of the file
- `H`   Move to top of screen
- `M`   Move to middle of screen
- `L`   Move to botton of screen
- `%`   Move to associated ( ), { }, [ ]

### Deleting text

Almost all deletion commands are performed by typing d followed by a
motion. For example, dw deletes a word. A few other deletes are:

- `x`   Delete character to the right of cursor
- `X`   Delete character to the left of cursor
- `D`   Delete to the end of the line
- `dd`  Delete current line

### Yanking text

Like deletion, almost all yank commands are performed by typing y
followed by a motion. For example, y$ yanks to the end of the line. Two
other yank commands are:

- `yy`  Yank the current line

### Putting text

- `p`   Put after the position or after the line
- `P`   Put before the position or before the line

### Changing text

The change command is a deletion command that leaves the editor in
insert mode. It is performed by typing c followed by a motion. For
example **cw** changes a word. A few other change commands are:

- `C`   Change from the cursor to the end of the line
- `cc`  Change the whole line

### Others

## Git

- [SublimeGit](https://github.com/SublimeGit/SublimeGit)
- [GitSavvy](https://github.com/divmain/GitSavvy)

## Packages for JavaScript programming

1. [Babel](https://packagecontrol.io/packages/Babel)
2. [JsHint](https://packagecontrol.io/packages/JSHint)
3. [JsFormat](https://packagecontrol.io/packages/JsFormat)
4. [DocBlockr](https://packagecontrol.io/packages/DocBlockr)
5. [AngularJS](https://packagecontrol.io/packages/AngularJS)
6. [TypeScript](https://packagecontrol.io/packages/TypeScript)
7. [HandleBar](https://packagecontrol.io/packages/Handlebars)
8. [Better CoffeeScript](https://packagecontrol.io/packages/Better%20CoffeeScript)
9. [jQuery](https://packagecontrol.io/packages/jQuery)

# Tips and Tricks

## Hiding folders or files in project, Workspace, Project

`Project -> Save project as...` after that edit path,
`folder_exclude_patterns`, `file_exclude_patterns`...

# Troubleshooting


# References

[1]: http://www.sublimetext.com/ "Homepage"
[2]: http://www.sublimetext.com/docs/3/ "Docs official"
[3]: http://docs.sublimetext.info/en/latest/intro.html "Docs unofficial"
[4]: https://courses.tutsplus.com/courses/perfect-workflow-in-sublime-text-2 "TutsPlus videos"
[boost-regex-doc]: http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html "Boost library documentation for regular expression"
[boost-format-strings-doc]: http://www.boost.org/doc/libs/1_44_0/libs/regex/doc/html/boost_regex/format/perl_format.html "Boost library documentation for format strings"
[origami-pkg]: https://github.com/SublimeText/Origami "Sublime Text Origami"
[markdown-build-command]: https://github.com/revolunet/sublimetext-markdown-preview/blob/master/MarkdownPreview.py#L1259 "Implementation of markdown_build target"
[golang-sublime-build]: https://github.com/golang/sublime-build "Golang Sublime Build system"
[sublime-packages-source]: https://github.com/sublimehq/Packages "Sublime Text Packages Source Code"
