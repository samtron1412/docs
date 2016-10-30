[TOC]

- [Docs official](http://www.sublimetext.com/docs/3/)
- [Docs unofficial](http://docs.sublimetext.info/en/latest/intro.html)
- [TutsPlus](https://courses.tutsplus.com/courses/perfect-workflow-in-sublime-text-2)

# Sublime 3 Packages

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

# Snippets
`Tools -> New Snippet...`

- Create new snippet for your definition.
- Improve your code speed.
- Add snippet manual or through package control.

# Build system
`Tools -> Build System -> New build system`

- Create new build system of you to build. Example, PHP, coffee script.

# Hiding folders or files in project, Workspace, Project
`Project -> Save project as...` after that edit path, `folder_exclude_patterns`, `file_exclude_patterns`...

# Macro
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

# Plugin



# Configuration file
## Key binding

```
[
	{ "keys": ["alt+l"], "command": "move", "args": {"by": "subword_ends", "forward": true} },
	{ "keys": ["alt+;"], "command": "run_macro_file", "args": {"file": "Packages/User/End_Of_Line_With_Semicolon.sublime-macro"} },
	{ "keys": ["ctrl+shift+w"], "command": "close_all" },
	{ "keys" : ["ctrl+shift+b"], "command" : "show_panel" , "args" : {"panel": "output.exec"} },
	{ "keys": ["ctrl+alt+b"], "command": "exec", "args": {"kill": true} },
	{ "keys": ["ctrl+enter"], "command": "insert", "args": {"characters": "\n"} },
	{ "keys": ["shift+enter"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Add Line.sublime-macro"} },
	{
	"keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"}
	},
	{ "keys": ["ctrl+shift+."], "command": "erb", "context":
		[
			{ "key": "selector", "operator": "equal", "operand": "text.html.ruby, text.haml, source.yaml, source.css, source.scss, source.js, source.coffee" }
		]
	},
	{
		"keys": ["alt+shift+h"],
		"command": "set_layout",
		"args":
	{
		"cols": [0.0, 0.33, 1.0],
		"rows": [0.0, 1.0],
		"cells": [[0, 0, 1, 1], [1, 0, 2, 1]]
	}
	},
	{
		"keys": ["alt+shift+l"],
		"command": "set_layout",
		"args":
	{
		"cols": [0.0, 0.66, 1.0],
		"rows": [0.0, 1.0],
		"cells": [[0, 0, 1, 1], [1, 0, 2, 1]]
	}
	},
	// {
	// 	"keys" : ["j", "j"],
	// 	"command": "exit_insert_mode",
	// 	"context":
	// 	[
	// 		{ "key" : "setting.command_mode", "operand": false },
	// 		{ "key" : "setting.is_widget", "operand": false }
	// 	]
	// },
	{ "keys": ["j", "j"], "command": "_enter_normal_mode", "args": {"mode": "mode_insert"}, "context": [{"key": "vi_insert_mode_aware"}] },
	{ "keys": ["ctrl+alt+1"], "command": "focus_group", "args": { "group": 0 } },
	{ "keys": ["ctrl+alt+2"], "command": "focus_group", "args": { "group": 1 } },
	{ "keys": ["ctrl+alt+3"], "command": "focus_group", "args": { "group": 2 } },
	{ "keys": ["ctrl+alt+4"], "command": "focus_group", "args": { "group": 3 } },
	{ "keys": ["ctrl+alt+5"], "command": "focus_group", "args": { "group": 4 } },
	{ "keys": ["ctrl+alt+6"], "command": "focus_group", "args": { "group": 5 } },
	{ "keys": ["ctrl+alt+7"], "command": "focus_group", "args": { "group": 6 } },
	{ "keys": ["ctrl+alt+8"], "command": "focus_group", "args": { "group": 7 } },
	{ "keys": ["ctrl+alt+9"], "command": "focus_group", "args": { "group": 8 } }

]
]
```

## Setting

```
{
	"added_words":
	[
		"virtualization",
		"libcontainer",
		"namespaces",
		"cgroups",
		"systemd",
		"nspawn",
		"libvirt",
		"ps",
		"Hykes",
		"virtualizers",
		"filesystem",
		"stderr",
		"stdout",
		"config",
		"Vagrantfile",
		"provisioners",
		"gitconfig",
		"gitattibutes",
		"gitattributes",
		"autocrlf",
		"whitespace"
	],
	"bold_folder_labels": true,
	"caret_style": "phase",
	"color_scheme": "Packages/Monokai Extended/Monokai Extended.tmTheme",
	"default_line_ending": "unix",
	"dictionary": "Packages/User/English(US)_custom/English(American).dic",
	"draw_white_space": "all",
	"fade_fold_buttons": false,
	"font_size": 10,
	"ignored_packages":
	[
		"Markdown"
	],
	"tab_size": 2,
	"vintage_start_in_command_mode": true
}
```



# User guide
## General
- Duplicate line: `Ctrl + Shift + D`
- Quicker reference assert: `Ctrl + Shift + P` and type `Copy` to copy path, file name, etc.
- Insert one line after: `Ctrl + Enter` -> very userful when want to new line
- Insert one line before: `Ctrl + Enter`
- Delete/Cut line: `Ctrl + X`
- To Uppercase: `Ctrl + KU`
- To Lowercase: `Ctrl + KL`
- Find: `Ctrl + F`
- Replace: `Ctrl + H`
- Indentation text: `Ctrl + [` or `Ctrl + ]` - very useful in markdown
- Comment: `Ctrl + /` and you want uncomment use undo
- Spell check: `F6`
- New file: `Ctrl + N`
- Open file: `Ctrl + O`
- Undo: `Ctrl + Z`
- Redo: `Ctrl + Y`
- Column select: `Shift + Right mouse`
- Use Multiple Selections to rename variables quickly. Here `Ctrl+D` is used to select the next occurrence of the current word.
- Make batch edits with Multiple Selections. Here `Ctrl+Shift+L` is used to split a selection into lines, and each line is then edited simultaneously.
- The Command Palette gives fast access to functionality. Here `Ctrl+Shift+P` is used to show the Command Palette, "sspy" (short for Set Syntax: Python) is used set the syntax of the current file to Python.
- Use Goto Anything to quickly navigate between files, even in the largest projects. `Ctrl+P` shows Goto Anything, and typing then filters on file and directory names.
	+ Type part of a file name to open it.
	+ Type `@` to jump to symbols, `#` to search within the file, and `:` to go to a line number.
- `Ctrl + Alt + j`: go to matching tag of emmet

## Search and Replace
### Single file
- Search single file: `Ctrl + F`
	+ Toggle RegEx: `Alt + R`
	+ Toggle Case sensitivity: `Alt + C`
	+ Toggle Exact match: `Alt + W`
	+ Find next: `Enter`
	+ Find Previous: `Shift + Enter`
	+ Find All: `Alt + Enter`
- Incremental search: `Ctrl + I`
	+ Find and select first result
- Replace: `Ctrl + H`
	+ Replce next: `Ctrl + Shift + H`
	+ Replace all: `Ctrl + Alt + Enter`
- Other way to search file:
	+ Go to anything and type `#` to search, or use `@` to search layout of file

### Multiple files
- Search multiple files: `Ctrl + Shift + F`
	+ Key binding same the single file
- Search scope: `Where` field
- Navigatinf result:
	+ Next match: `F4`
	+ Previous match: `Shift + F4`

## Vintage mode
- Exit Insert mode: `ESC/j j`
- Visual mode:
	+ visual normal mode `command mode -> v`
	+ visual line mode `command mode -> V`

### Inserting text

- `i`	Insert before cursor
- `I`	Insert before line
- `a`	Append after cursor
- `A`	Append after line
- `o`	Open a new line after current line
- `O`	Open a new line before current line
- `r`	Replace one character
- `R`	Replace many characters

### Motion

- `h`	Move left
- `j`	Move down
- `k`	Move up
- `l`	Move right
- `w`	Move to next word
- `W`	Move to next blank delimited word
- `b`	Move to the beginning of the word
- `B`	Move to the beginning of blank delimted word
- `e`	Move to the end of the word
- `E`	Move to the end of Blank delimited word
- `{`	Move a paragraph back
- `}`	Move a paragraph forward
- `0`	Move to the begining of the line
- `$`	Move to the end of the line
- `gg/1G`	Move to the first line of the file
- `G`	Move to the last line of the file
- `nG`	Move to nth line of the file
- `H`	Move to top of screen
- `M`	Move to middle of screen
- `L`	Move to botton of screen
- `%`	Move to associated ( ), { }, [ ]

### Deleting text

Almost all deletion commands are performed by typing d followed by a motion. For example, dw deletes a word. A few other deletes are:

- `x`	Delete character to the right of cursor
- `X`	Delete character to the left of cursor
- `D`	Delete to the end of the line
- `dd`	Delete current line

### Yanking text

Like deletion, almost all yank commands are performed by typing y followed by a motion. For example, y$ yanks to the end of the line. Two other yank commands are:

- `yy`	Yank the current line

### Putting text

- `p`	Put after the position or after the line
- `P`	Put before the position or before the line

### Changing text

The change command is a deletion command that leaves the editor in insert mode. It is performed by typing c followed by a motion. For example **cw** changes a word. A few other change commands are:

- `C`	Change from the cursor to the end of the line
- `cc`	Change the whole line

### Others

## SmartMarkdown
### Move between headlines.
Use `Ctrl+c Ctrl+n` to move to the next headline (any level); `Ctrl+c Ctrl+p` to the previous one, for Mac. (`Ctrl+; Ctrl+n` and `Ctrl+; Ctrl+p` for Windows and Linux)
Use `Ctrl+c Ctrl+f` to move to the next headline (same level or higher level); `Ctrl+c Ctrl+b` to the previous one, for Mac. (`Ctrl+; Ctrlf` and `Ctrl+; Ctrl+b` for Windows and Linux)

### Adjust headline level Added by David Smith.
`Super+Shift+,` for decreasing and `Super+Shift+.` for increasing headline levels.

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

