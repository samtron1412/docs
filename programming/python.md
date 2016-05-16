[TOC]

# Overview
- **General-purpose, high level programming language**
- **Multi-paradigm:** object-oriented, imperative, functional, procedural, reflective
- **Typing:** duck, dunamic, strong

## History
first release: 1991

## Typing
duck

# Package Manager - [pip](https://pypi.python.org/pypi/pip)
- Install pip
	+ Use package manager of Linux distribution
		* Arch Linux
			- python3: `sudo pacman -S python-pip`
			- python2: `sudo pacman -S python2-pip`
	+ Use [get-pip.py](https://bootstrap.pypa.io/get-pip.py) script
		* `python get-pip.py`
- Use pip with multiple python versions: `pip<version> <command> ...`
	+ `pip install <sth>`
	+ `pip2 install <sth>`
	+ `pip2.5 install <sth>`
- Upgrade pip
	+ Linux: `pip install -U pip`
	+ Windows: `python -m pip install -U pip`
- Show list packages: `pip list`
- Show list packages use for requirementstxt to install in other system: `pip freeze`
- Show outdated packages: `pip list --outdated`
- Searching for packages: `pip search "query"`
- Install new package: `pip install <package name>`
- Uninstall package: `pip uninstall <package naem>`
- Update package: `pip install <package name> -U` or `pip install <package name> --upgrade`
- Update all packages: `pip install --outdated | awk '{print $1}' | xargs -n1 sudo pip install -U`

## Configuration


# Version Manager
- [pyenv](https://github.com/yyuu/pyenv)
- [pythonz](https://github.com/saghul/pythonz)

**Windows**
- Can use trick, copy file .exe and change name

## pyenv
### Installation
#### [pyenv-installer](https://github.com/yyuu/pyenv-installer)

`curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash`

**Update**: `pyenv update`

**Uninstall**: pyenv is installed within `$PYENV_ROOT` (default: `~/.pyenv`). To uninstall, just remove it: `rm -fr ~/.pyenv` and remove these three lines from `.bashrc` or from `your shell rc file`:

	export PATH="/root/.pyenv/bin:$PATH"
	eval "$(pyenv init -)"
	eval "$(pyenv virtualenv-init -)"

#### [Manually install - Basic GitHub Checkout](https://github.com/yyuu/pyenv#basic-github-checkout)

### User guide


# Packages
## [cryptography](https://github.com/pyca/cryptography)

## [pycrypto](https://github.com/dlitz/pycrypto)

## [virtualenv](https://pypi.python.org/pypi/virtualenv)

## [Console User interface library](https://github.com/urwid/urwid)
- [alot - Mail User Agent](https://github.com/pazz/alot)

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
#!/usr/bin/python
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

