[TOC]

# Introduction
## What is PHP?
PHP (recursive acronym for **PHP: Hypertext Preprocessor**) is a widely-used **open source general-purpose scripting language** that is especially suited for web development and can be embedded into HTML.

## What can PHP do?
There are three main areas where PHP scripts are used.

- **Server-side scripting**. This is the most traditional and main target field for PHP. You need three things to make this work. `The PHP parser` (CGI or server module), `a web server` and `a web browser`.
- **Command line scripting**. You can make a PHP script to run it without any server or browser. You only need the PHP parser to use it this way. This type of usage is ideal for scripts regularly executed using cron (on *nix or Linux) or Task Scheduler (on Windows).
- **Writing desktop applications**. PHP is probably not the very best language to create a desktop application with a graphical user interface, but if you know PHP very well, and would like to use some advanced PHP features in your client-side applications you can also use [PHP-GTK](http://gtk.php.net/) to write such programs. You also have the ability to write cross-platform applications this way.

# Installation and Configuration
## [Release](http://php.net/releases/)
- Should use Japan server: `http://jp2.php.net/distributions/php-5.4.42.tar.gz`

## Common Gateway Interface ([CGI](http://tools.ietf.org/html/rfc3875))
CGI, when implemented on a Web server, provides an interface between the Web server and programs that generate the Web content. These programs are known as CGI scripts or simply CGIs; they are usually written in a scripting language, but can be written in any programming language.

Web server responde static files and dynamic contents. Dynamic contents serve by CGI, Web server will executed CGI scripts and responde outputs to clients.

Parameters are passed to the script are stored in the `QUERY_STRING` variable.

[Books](http://www.oreilly.com/openbook/cgi/ch01_01.html)

## [FastCGI Process Manager](http://php-fpm.org/) ([FPM](http://php.net/manual/en/install.fpm.php))
FPM (FastCGI Process Manager) is an alternative PHP FastCGI implementation with some additional features (mostly) useful for **heavy-loaded sites**.

### [FastCGI](http://en.wikipedia.org/wiki/FastCGI)
FastCGI is a variation on the earlier Common Gateway Interface (CGI); FastCGI's main aim is to reduce the overhead associated with interfacing the web server and CGI programs, allowing a server to handle more web page requests at once.

The FastCGI approach, however, competed against other techniques which also aimed to speed and simplify server-subprogram communications. Apache modules such as `mod_perl` and `mod_php` appeared around the same time, and they also quickly gained popularity.

Instead of creating a new process for each request, FastCGI uses *persistent processes to handle a series of requests*. These processes are owned by the **FastCGI server**, not the web server.

To service an incoming request, the web server sends environment information and the page request itself to a FastCGI process over a *socket* (in the case of local FastCGI processes on the web server) or *TCP connection* (for remote FastCGI processes in a server farm).

The separation of web applications from the web server in FastCGI has many advantages over embedded interpreters (`mod_perl`, `mod_php`, etc.). This separation allows server and application processes to be *restarted independently* – an important consideration for busy web sites. It also enables the implementation of *per-application / hosting service security policies*, which is an important requirement for ISPs and web hosting companies. Different types of incoming requests can be distributed to specific FastCGI servers which have been equipped to handle those particular types of requests efficiently.




# Resources
## Books
### Online
- [PHP documentation](http://php.net/docs.php)
- [Practical PHP Programming](http://www.tuxradar.com/practicalphp)
- [PHP Security Cheat Sheet](https://www.owasp.org/index.php/PHP_Security_Cheat_Sheet)

# Language References
## List reserved words
### [List of keywords](http://php.net/manual/en/reserved.keywords.php)


### [Predefined classes](http://php.net/manual/en/reserved.classes.php)
`self`: current class

`static`: current class at runtime

`parent`: parent class (like `super` at Java)

- Use `::` for static elements (class) and `->` for instance elements (obj)
- Use `self` for current class and `$this` for current object

### [Predefined constants](http://php.net/manual/en/reserved.constants.php)





## OOP
### Visibility
Public, Private, Protected

### Static keyword
Static property of class, static method of class and static variable of method (in variable scope)


## Types
PHP supports eight primitive types.

Four scalar types:
- [boolean](#booleans)
- integer
- float
- string

Two compound types:
- array
- object

And finally two special types:
- resource
- NULL

Some pseudo-types for readability reasons:
- mixed
- number
- callback (aka callable)
- array | object
- void

And the pseudo-variable `$...`

### Booleans


## Variables
### Predefined variables
- `Superglobals` — Superglobals are built-in variables that are always available in all scopes
- `$GLOBALS` — References all variables available in global scope
- `$_SERVER` — Server and execution environment information
- `$_GET` — HTTP GET variables
- `$_POST` — HTTP POST variables
- `$_FILES` — HTTP File Upload variables
- `$_REQUEST` — HTTP Request variables
- `$_SESSION` — Session variables
- `$_ENV` — Environment variables
- `$_COOKIE` — HTTP Cookies
- `$php_errormsg` — The previous error message
- `$HTTP_RAW_POST_DATA` — Raw POST data
- `$http_response_header` — HTTP response headers
- `$argc` — The number of arguments passed to script
- `$argv` — Array of arguments passed to script

### Variables Scope
global keyword, static keyword ( A static variable exists only in a local function scope, but it does not lose its value when program execution leaves this scope.)



## Constants
A constant is an identifier (name) for a simple value. As the name suggests, that value cannot change during the execution of the script (except for magic constants, which aren't actually constants). A constant is case-sensitive by default. By convention, constant identifiers are always uppercase.

### Syntax
Use `define()` or `const` to declare constants.

>**note**: if use `const` must be declared at the top-level scope because they are defined at compile-time. This means that it cannot be declared inside function, loops, if statements or try/catch blocks.

  <?php
  define("CONSTANT", "Hello world.");
  echo CONSTANT; // outputs "Hello world."
  echo Constant; // outputs "Constant" and issues a notice.
  ?>

  <?php
  // Works as of PHP 5.3.0
  const CONSTANT = 'Hello World';

  echo CONSTANT;

  // Works as of PHP 5.6.0
  const ANOTHER_CONST = CONSTANT.'; Goodbye World';

  echo ANOTHER_CONST;
  ?>


### Magic constants
There are **eight magical constants that change depending on where they are used**. For example, the value of `__LINE__` depends on the line that it's used on in your script. These special constants are **case-insensitive** and are as follows:

| Name          | Description                                                                                                                                                                                                                            |
| -             | -                                                                                                                                                                                                                                      |
| `__LINE__`      | The current line number of the file.                                                                                                                                                                                                   |
| `__FILE__`      | The full path and filename of the file with symlinks resolved. If used inside an include, the name of the included file is returned.                                                                                                   |
| `__DIR__`       | The directory of the file. If used inside an include, the directory of the included file is returned. This is equivalent to dirname(`__FILE__`). This directory name does not have a trailing slash unless it is the root directory.     |
| `__FUNCTION__`  | The function name. (method name only)                                                                                                                                                                                                  |
| `__CLASS__`     | The class name. The class name includes the namespace it was declared in (e.g. Foo\Bar). Note that as of PHP 5.4 `__CLASS__` works also in traits. When used in a trait method, `__CLASS__` is the name of the class the trait is used in. |
| `__TRAIT__`     | The trait name. The trait name includes the namespace it was declared in (e.g. Foo\Bar).                                                                                                                                               |
| `__METHOD__`    | The class method name. (class::method)                                                                                                                                                                                                 |
| `__NAMESPACE__` | The name of the current namespace.                                                                                                                                                                                                     |

## Expressions


## Operators
### Assignment operators
[See the Arithmetic Operators page](http://www.php.net/manual/en/language.operators.arithmetic.php)

  Assignment    Same as:
  $a += $b     $a = $a + $b    Addition
  $a -= $b     $a = $a - $b     Subtraction
  $a *= $b     $a = $a * $b     Multiplication
  $a /= $b     $a = $a / $b    Division
  $a %= $b     $a = $a % $b    Modulus

[See the String Operators page](http://www.php.net/manual/en/language.operators.string.php)

  $a .= $b     $a = $a . $b       Concatenate

[See the Bitwise Operators page](http://www.php.net/manual/en/language.operators.bitwise.php)

  $a &= $b     $a = $a & $b     Bitwise And
  $a |= $b     $a = $a | $b      Bitwise Or
  $a ^= $b     $a = $a ^ $b       Bitwise Xor
  $a <<= $b     $a = $a << $b     Left shift
  $a >>= $b     $a = $a >> $b      Right shift

Assigning by reference

  <?php
  $a = 3;
  $b = &$a; // $b is a reference to $a

  print "$a\n"; // prints 3
  print "$b\n"; // prints 3

  $a = 4; // change $a

  print "$a\n"; // prints 4
  print "$b\n"; // prints 4 as well, since $b is a reference to $a, which has
                // been changed
  ?>

### Arithmetic operators
`$a ** $b`: $a power $b


### [Bitwise operators](http://php.net/manual/en/language.operators.bitwise.php)


### Error Control Operators
`@`: sftu operator (shut the fuck up)


### Comparison Operators
#### Ternary
`(condition) ? (value_if_true) : (value_if_false);`



## Control Structures

## Functions

## Classes and Objects
### Predefined Classes and Interfaces

## Namespaces

## Exceptions
### Predefined Exceptions

## Generators

## References Explained

## Context options and parameters

## Supported Protocols and Wrappers

# Security



# Features



# Function Reference



# PHP at the core: A Hacker's guide


# Tutorial
## Debug
- [8 best PHP debug tools](http://codecall.net/2014/02/21/best-php-debugging-tools/): kint, whoops, xdebug, phpdebugbar,

## Thread safe and Non Thread Safe
When integrated PHP with Apache, we have to choose right version of PHP module to work with Apache. Depend on the way Apache handle request to choose thread safe or non thread safe.

- Thread safe when Apache use model thread to handle request.
- Non thread safe when Apache use model non thread to handle request.

Best practice is use Thread safe when PHP use through mod_php of Apache, and Non Thread Safe when install standalone PHP parallel with Apache.

## Server Application Programming Interface (SAPI)
It is an interface to communicate between PHP and web server.



## Performance
- Use `$arr[] = value` fast than and convinient than `array_push($arr, value)`
- Use `for($i = 0; $i < size; $i++)` fast than `foreach($arr as $item)`
-


## Loop
- `foreach($arr as $item)` will copy $arr
- `foreach($arr as &$item)` will reference to $arr and you can change value of array while looping.
- `array_map("callback_function_name", $input)` call callback function and map on each item.
- `array_reduce("callback_function_name", $input)` call callback functin and reduce array to single value.
-



# Tips and Tricks
## [Best practices, coding standards](https://github.com/codeguy/php-the-right-way)

## [Disable xdebug](https://web.archive.org/web/20150208161308/http://frankmayer.me/blog/12-xdebug-disabling-vs-not-loading-it-at-all)
Comment this line in php.ini file:

`;zend_extension = "/usr/lib64/php/modules/xdebug.so"`

## include vs require
It is possible to insert the content of one PHP file into another PHP file (before the server executes it), with the include or require statement.

The include and require statements are identical, except upon failure:

- require will produce a fatal error (`E_COMPILE_ERROR`) and stop the script
- include will only produce a warning (`E_WARNING`) and the script will continue

## phpinfo from the command line
    echo "<?php phpinfo(); ?>" | php > phpinfo.txt
    php -i
    php -r "phpinfo();"

    php -a (interactive shell)
    php> phpinfo()

Find Loaded Configuration File

    php -i | grep "Configuration File"

List all modules loaded by PHP

    php -m


## Install PHP 5.2 from source
- Install required packages:

```bash
yum -y install gcc make httpd-devel libxml2-devel bzip2-devel openssl-devel libcurl-devel gd-devel libc-client-devel libmcrypt-devel mhash-devel aspell-devel libxslt-devel mysql-devel mysql
```

- Download source of php:

```bash
wget http://museum.php.net/php5/php-5.2.17.tar.gz
tar -zxvf php-5.2.17.tar.gz
cd php-5.2.17
```

- Configure source:

```bash
./configure --disable-posix --enable-zend-multibyte --enable-mbregex --enable-roxen-zts --enable-maintainer-zts --enable-bcmath --enable-calendar --enable-exif --enable-fastcgi --enable-ftp --enable-gd-native-ttf --enable-libxml --enable-magic-quotes --enable-mbstring --enable-pdo --enable-soap --enable-sockets --enable-wddx --enable-zip --with-libdir=lib64 --with-apxs2=/usr/sbin/apxs --with-config-file-path=/usr/local/lib --with-bz2 --with-curl --with-curlwrappers --with-freetype-dir --with-gd --with-gettext --with-imap --with-imap-ssl --with-jpeg-dir --with-kerberos --with-libexpat-dir --with-libxml-dir --with-libxml-dir --with-mcrypt --with-mhash --with-mime-magic --with-mysql --with-mysqli --with-openssl --with-openssl-dir --with-pcre-regex --with-pdo-mysql --with-pdo-sqlite --with-pic --with-png-dir --with-pspell --with-sqlite --with-ttf --with-xmlrpc --with-xpm-dir --with-xsl --with-zlib --with-zlib-dir --with-readline
```

- Compile and install php:

```shell
make
make install
```

### Explain configure opptions
- `--with-readline`: enable Interactive shell for PHP
-


# Packages manager
## PECL
PECL is a repository for PHP Extensions, providing a directory of all known extensions and hosting facilities for downloading and development of PHP extensions.

Install extention: `pecl install <package>`
- `pecl install xdebug` : install latest version
- `pecl install xdebug-2.2.7` : install specific version

### Upgrade ICU for intl package
icu4c
#### From source
```bash
wget http://download.icu-project.org/files/icu4c/51.2/icu4c-51_2-src.tgz
tar zxf icu4c-51_2-src.tgz
cd icu/source
./configure --prefix && make && make install
pecl install intl
```

#### From bin
```bash
wget http://download.icu-project.org/files/icu4c/52.1/icu4c-52_1-RHEL6-i386.tgz
tar zxf icu4c-52_1-RHEL6-i386.tgz
cp -r usr/local/* /usr/
cp -r usr/* /usr
/usr/bin/icu-config --prefix
pecl install intl
```



