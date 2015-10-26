[TOC]

# Overview


# [All GNU packages](http://www.gnu.org/manual/blurbs.html)
[All manuals](http://www.gnu.org/manual/manual.html)

# [The GNU configure and build system](http://www.airs.com/ian/configure/)
[PDF](http://wwwcdf.pd.infn.it/localdoc/configure.pdf)

## Introduction
### Building
All `configure` scripts support a wide variety of options. The most interesting ones are `--with` and `--enable` options which are generally specific to particular tools. You can usually use the `--help` option to get a list of interesting options for a particular configure script.

The only generic options you are likely to use are the `--prefix` and `--exec-prefix` options. These options are used to specify the installation directory.

The directory named by the `--prefix` option will hold machine independent files such as info files.

The directory named by the `--exec-prefix` option, which is normally a subdirectory of the `--prefix` directory, will hold machine dependent files such as executables.

The default for `--prefix` is `/usr/local`. The default for `--exec-prefix` is the value used for `--prefix`.

### Uninstall
- If creator of package have uninstall rule for make, we will run: `make uninstall`
- If you specific different location at `--prefix` configure, example `--perfix=/usr/local/php52`. So, simple is delete this directory to uninstall.
- Use command: `find /use/local -type f -newermt <date install>` to find all files installed.
	+ `find /usr/local -type f -newermt '2015-04-02`
	+ Delete all files to uninstall, use command: `find /usr/local -type f -newermt '2015-04-02' -delete`
- If you're not lucky, you'll have to manually uninstall it. Running `make -n install` can be helpful, since it will show the steps that the software would take to install itself but won't actually do anything. You can then manually reverse those steps.