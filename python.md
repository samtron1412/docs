[TOC]

# Overview
- **General-purpose, high level programming language**
- **Multi-paradigm:** object-oriented, imperative, functional, procedural, reflective
- **Typing:** duck, dunamic, strong

## History
first release: 1991

## Typing
duck

# Install
## Package Manager
### pip
- Show list packages: `pip list`
- Show list packages use for requirementstxt to install in other system: `pip freeze`
- Install new package: `pip install <package name>`
- Uninstall package: `pip uninstall <package naem>`
- Update package: `pip install <package name> -U` or `pip install <package name> --upgrade`


## Version Manager
- [pyenv](https://github.com/yyuu/pyenv)
- [pylauncher](https://bitbucket.org/vinay.sajip/pylauncher)
- [virtualenv](https://pypi.python.org/pypi/virtualenv)

Windows
- Can use trick, copy file .exe and change name

### pyenv
#### Installation
##### [pyenv-installer](https://github.com/yyuu/pyenv-installer)

`curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash`

Update: `pyenv update`

Uninstall: pyenv is installed within `$PYENV_ROOT` (default: `~/.pyenv`). To uninstall, just remove it: `rm -fr ~/.pyenv`

##### Manually install - Basic GitHub Checkout
This will get you going with the latest version of pyenv and make it easy to fork and contribute any changes back upstream.

1. Check out pyenv where you want it installed. A good place to choose is $HOME/.pyenv (but you can install it somewhere else).

		$ git clone https://github.com/yyuu/pyenv.git ~/.pyenv

2. Define environment variable PYENV_ROOT to point to the path where pyenv repo is cloned and add $PYENV_ROOT/bin to your $PATH for access to the pyenv command-line utility.

$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile

Zsh note: Modify your ~/.zshenv file instead of ~/.bash_profile. Ubuntu note: Modify your ~/.bashrc file instead of ~/.bash_profile.

3. Add pyenv init to your shell to enable shims and autocompletion. Please make sure eval "$(pyenv init -)" is placed toward the end of shell configuration file since it manipulates PATH during the initialization.

		$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile

Zsh note: Modify your ~/.zshenv file instead of ~/.bash_profile. Ubuntu note: Modify your ~/.bashrc file instead of ~/.bash_profile.

General warning: There are some systems, where the BASH_ENV variable is configured to point to .bashrc. On such systems you should almost certainly put the abovementioned line eval "$(pyenv init -) into .bash_profile, and not into .bashrc. Otherwise you may observe strange behaviour, such as pyenv getting into an infinite loop. See #264 for details.

4. Restart your shell so the path changes take effect. You can now begin using pyenv.

		$ exec $SHELL

5. Install Python versions into $PYENV_ROOT/versions. For example, to install Python 2.7.8, download and unpack the source, then run:

		$ pyenv install 2.7.8

NOTE: If you need to pass configure option to build, please use CONFIGURE_OPTS environment variable.

NOTE: If you are having trouble installing a python version, please visit the wiki page about Common Build Problems

6. Rebuild the shim binaries. You should do this any time you install a new Python binary. (Examples: installing a new Python version, or installing a package that provides a binary.)

		$ pyenv rehash

This can be automated for pip using pyenv-pip-rehash, which invokes pyenv rehash after (un)installing packages using pip.

**Upgrading**

If you've installed pyenv using the instructions above, you can upgrade your installation at any time using git.

To upgrade to the latest development version of pyenv, use git pull:

$ cd ~/.pyenv
$ git pull
To upgrade to a specific release of pyenv, check out the corresponding tag:

$ cd ~/.pyenv
$ git fetch
$ git tag
v0.1.0
$ git checkout v0.1.0


# Packages
## Django
## [SQLAlchemy](http://www.sqlalchemy.org/)
SQLAlchemy is the Python SQL toolkit and Object Relational Mapper that gives application developers the full power and flexibility of SQL.

[SourCode](https://bitbucket.org/zzzeek/sqlalchemy)

## [peewee](http://peewee.readthedocs.org/en/latest/index.html)
Peewee is a simple and small ORM. It has few (but expressive) concepts, making it easy to learn and intuitive to use.
- A small, expressive ORM
- Written in python with support for versions 2.6+ and 3.2+.
- built-in support for sqlite, mysql and postgresql
- tons of extensions available in the [Playhouse, a collection of addons](http://peewee.readthedocs.org/en/latest/peewee/playhouse.html#playhouse) (postgres hstore/json/arrays, sqlite full-text-search, schema migrations, and much more).

[SourCode](https://github.com/coleifer/peewee)

## requests
A HTTP library, written in Python, for human beings.

## [csv file](http://softwarerecs.stackexchange.com/questions/7463/fastest-python-library-to-read-a-csv-file)


# Tutorial
## Structure of a script

```python
import sth

def myfunction():
	sth...

def main():
	myfunction();
	sth...

if __name__ == '__main__':
	main()
else:
	sth...
```





## I/O
- [Redirect stdout to file](http://stackoverflow.com/questions/4675728/redirect-stdout-to-a-file-in-python)

## [Work with MySQL](http://stackoverflow.com/questions/372885/how-do-i-connect-to-a-mysql-database-in-python)
- [Python MySQL Database Access](http://www.tutorialspoint.com/python/python_database_access.htm)
- [MySQL Unicode and Encoding](http://stackoverflow.com/questions/8365660/python-mysql-unicode-and-encoding)

## Work with Encoding
- [Unicode reading and writing to files in python](http://stackoverflow.com/questions/491921/unicode-utf8-reading-and-writing-to-files-in-python?answertab=votes#tab-top) see the answer most votes below accepted answer (not see accepted answer)
- [codecs](https://docs.python.org/2/library/codecs.html) module

# Tips and Tricks
## Check python version by python code
```python
import sys

print sys.version_info
```

