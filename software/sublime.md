[TOC]

# Overview
Sublime Text is a proprietary text editor with a Python application
programming interface.

# Basic Concepts
## Glossary
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

| Action                     | Shortcut    |
| -                          | -           |
| Open search panel          | Ctrl+f      |
| Toggle regular expressions | Alt+r       |
| Toggle case sensitivity    | Alt+c       |
| Toggle exact match         | Alt+w       |
| Find next                  | Enter       |
| Find previous              | Shift+Enter |
| Find all                   | Alt+Enter   |

### Incremental Search

| Action                        | Shortcut                                                                                                           |
| -                             | -                                                                                                                  |
| Open incremental search panel | Ctrl+i                                                                                                             |
| Toggle regular expressions    | Alt+r                                                                                                              |
| Toggle case sensitivity       | Alt+c                                                                                                              |
| Toggle exact match            | Alt+w                                                                                                              |
| Find next                     | Enter (select the next match in the file and dismiss the search panel, so you cannot use `Shift+Enter` after this) |
| Find previous                 | Shift+Enter (it only has effect when the search panel is opened)                                                   |
| Find all                      | Alt+Enter                                                                                                          |

### Replacing text

| Action             | Shortcut       |
| -                  | -              |
| Open replace panel | Ctrl+h         |
| Replace next       | Ctrl+Shift+h   |
| Replace all        | Ctrl+Alt+Enter |

### Goto Anything search

`Ctrl+p` -> type something to specify the file -> `#` -> type something
to search in the file.

### Search-related key bindings

These key bindings work when the search panel is hidden.

| Action                                       | Shortcut |
| -                                            | -        |
| Search forward using most recent pattern     | f3       |
| Search backward using most recent pattern   | Shift+f3 |
| Select all matches using most recent pattern | Alt+f3   |

These key bindings effect `f3` and `shift+f3` key bindings.

| Search using current selection  | Ctrl+e       |
| Replace using current selection | Ctrl+Shift+e |


# File Navigation and File Management
## Goto Anything
Use Goto Anything to quickly navigate between files, even in the
largest projects. `Ctrl+p` shows Goto Anything, and typing then
filters on file and directory names.

- Type part of a file name to open it.
- Type `@` to jump to symbols, `#` to search within the file, and `:` to
go to a line number.


# Build systems
`Tools -> Build System -> New build system`

- Create new build system of you to build. Example, PHP, coffee script.


# Customization

# Extensibility and Automation
## Macro
Best solution for this is recording a macro on Sublime Text and then assigning it to a keyboard shortcut. Follow these steps:

1. Create a line such as `alert('hello')` and leave the cursor right after letter `o`.
2. Then go to Tools > Record a Macro to start recording.
3. Press `alt+left` to go to the end of line.
4. Press `;` and hit Enter
5. Stop recording the macro by going to Tools > Stop Recording Macro
6. You can now test your macro by Tools > Playback Macro (optional)
7. Save your macro by going to Tools > Save Macro (ex: EndOfLine.sublime-macro)
8. Create a shortcut by adding this between the square brackets in your in your Preferences > Key Bindings - User file:

        {
        "keys": ["super+;"], "command": "run_macro_file", "args": {"file": "Packages/User/EndOfLine.sublime-macro"}
        }

9. Now, every time you hit `Command+;`, it will magically place the semicolon at the end of current line and move the cursor to the next line.
Happy coding!

## Snippets
`Tools -> New Snippet...`

- Create new snippet for your definition.
- Improve your code speed.
- Add snippet manual or through package control.

# Command Line

# Advanced Users

# Package Control
## End Users
### Usage
- Install Package
    + show a list of all available packages at default channel.
- Add Repository
    + add a repository that is not included in the default channel. This allows users to install and automatically update packages from GitHub and BitBucket.
    + To add a package hosted on GitHub, enter the URL in the form `https://github.com/username/repo`. Don’t include .git at the end! BitBucket repositories should use the format `https://bitbucket.org/username/repository`.
- Remove Package
    + This command will remove the package folder, and the package name from the `installed_packages` list in `Packages/User/Package Control.sublime-settings`.
    + The `installed_packages` list allow Package Control to automatically install packages for you if you copy your `Package/User/` folder to other machine.
- Add channel
- Create Package File
    + For package developers.
    + Takes a package folder and generates a `.sublime-package` file that can be uploaded onto the web and referenced in the `packages.json` file for a repository.
- Create Binary Package File
    + For package developers.
    + Creates a `.sublime-package` file that does not include the source `.py` files, but instead the `.pyc` bytecode files. This is useful to distribute commercial packages. Be sure to check the resulting `.sublime-package` file to ensure that at least one `.py` file is included so that Sublime Text will load the package.
- Disable Package
- Discover Package
    + Opens up a web browser to browse
- Enable Package
    + Re-enables a package that has been disabled.
- Upgrade/Overwrite All Packages
    + This will upgrade ALL Packages, including ones that were not installed via Package Control.
    + If you are developing a custom copy of a package, you may not want to use this command.
- Upgrade Package

### Settings
The default settings can be viewed by accessing the `Preferences > Package Settings > Package Control > Settings – Default` menu. To ensure settings are not lost when the package is upgraded, make sure all edits are saved to `Settings – User`.

[References](https://packagecontrol.io/docs/settings)

### Customizing Packages
#### Packed vs Unpacked
Sublime Text 3 by default, packages will be installed by placing a .sublime-package file in the `Install Packages/` folder. Then users may override individual files in the package by creating a folder `Packages/{Package Name}/` and placing edited files in there.

#### Editing Unpacked Files
Editing an unpacked package's files is not a good idea unless you've cloned the package via `Git/Hg`. This is because, by default, Package Control will automatically upgrade packages to the newest version. This will cause any edits to files to be **overwritten**. If you experience this, you may wish to check out the **Backups** section to learn how to recover your customized version of a file.

- User Package
    + The `Packages/User/` folder is the User package. It is unique in that it is loaded **last** by Sublime Text.
    + This allows users to place changes to `.sublime-settings` and `.sublime-keymap` files in this folder.
    + Sublime Text loads these files by name. Thus if a package has a file named `Package Control.sublime-settings` in the package, a file with the same name in the User package will override any of the settings in the original file. The same is true for key bindings.
- Overrides
    + If a package for Sublime Text 3 is installed as a **packed package**, it should be possible to directly override **individual non-python files**. To do this, create a `Packages/{Package Name}/` folder and save customized versions of the files with **the same name they are in the .sublime-package file**.
- Git/Hg clone
    + For complete customization of a package, it will likely be necessary to using a version control program, such as Git or Hg to clone a copy of the original package repository into the `Packages/` folder.
    + The best way to make customizations would be to **fork the original repository and clone your fork of it**. If you think your customizations could be useful to others, consider sending a pull request to have your changes merged into the original version.
    + If you've cloned it from your own fork of the repository, no settings need to be changed. If you clone it from the original repository, you will likely want to set the `ignore_vcs_packages` setting.
- Backups
    + If you do ever find yourself in a situation where your edits to a package were overwritten by Package Control, you can find a backup copy in the `Backup/` folder. This folder can be located by selecting the `Preferences > Browse Packages…` menu and then browsing up a folder. Backups are stored in timestamped folders.


### Syncing
You should use Git or Dropbox like service to syncing `Packages/User/` folder. When you go to new machine let override this `User` folder and start Sublime with Package Control will reinstall all package for you and all configuration of Sublime also applied.

When use Git you should ignore some things:
- Package Control.last-run
- Package Control.ca-list
- Package Control.ca-bundle
- Package Control.system-ca-bundle
- Package Control.cache/
- Package Control.ca-certs/
- etc. change frequently

#### Windows
- Make soft link to `User` directory: `cmd /c mklink /D User $env:userprofile\path\to\User`

### Troubleshooting
#### Purging and Reinstalling
1. Select the `Preferences > Settings – User` menu entry
2. Remove `"Package Control"` from the `"ignored_packages"` setting, if present
3. Select the `Preferences > Browse Packages…` menu entry
4. Delete the folder named `Package Control`
5. Browse up a folder and then into `Installed Packages`
6. Delete `Package Control.sublime-package` if it exists
7. Reinstall Package Control using the [installation instructions](https://packagecontrol.io/installation)

#### Enabling Debug Log
The debug log contains extensive information about what Package Control is doing behind the scenes, and can help to diagnose why it isn't working properly.

1. Click the `Preferences` menu
2. Select `Package Settings`
3. Choose `Package Control`
4. Click `Settings - User`
5. Add the setting `"debug": true`
6. Save the settings file

Now when performing actions with Package Control, debug information will be printed to the Sublime Text console. The console can be opened by pressing **ctrl+`** or using the View > Show Console menu entry.

### Issues
Are you having trouble using Package Control? Before opening an issue, please take the time to perform the following few steps. Properly following directions will improve the likelyhood of your issue be quickly resolved.

1. Check to make sure you are using the latest version of Package Control: run the Package Control: List Packages command from the command palette
2. Look at the Sublime Text Console **ctrl+`** to see if any python errors are listed
3. Review the list of open GitHub issues to see if the problem you are experiencing has been reported
4. Please do not comment on a Closed issue, but feel free to reference it from a new one

To provide the info necessary to help solve the issue, please generate a debug log. To do this:

1. Open `Preferences > Package Settings > Package Control > Settings - User`
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
Use `Ctrl+c Ctrl+n` to move to the next headline (any level); `Ctrl+c Ctrl+p` to the previous one, for Mac. (`Ctrl+; Ctrl+n` and `Ctrl+; Ctrl+p` for Windows and Linux)
Use `Ctrl+c Ctrl+f` to move to the next headline (same level or higher level); `Ctrl+c Ctrl+b` to the previous one, for Mac. (`Ctrl+; Ctrlf` and `Ctrl+; Ctrl+b` for Windows and Linux)

### Adjust headline level Added by David Smith.
`Super+Shift+,` for decreasing and `Super+Shift+.` for increasing headline levels.

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

Almost all deletion commands are performed by typing d followed by a motion. For example, dw deletes a word. A few other deletes are:

- `x`   Delete character to the right of cursor
- `X`   Delete character to the left of cursor
- `D`   Delete to the end of the line
- `dd`  Delete current line

### Yanking text

Like deletion, almost all yank commands are performed by typing y followed by a motion. For example, y$ yanks to the end of the line. Two other yank commands are:

- `yy`  Yank the current line

### Putting text

- `p`   Put after the position or after the line
- `P`   Put before the position or before the line

### Changing text

The change command is a deletion command that leaves the editor in insert mode. It is performed by typing c followed by a motion. For example **cw** changes a word. A few other change commands are:

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
