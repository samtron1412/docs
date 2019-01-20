[TOC]

# Overview

Node.js® is a platform built on `Chrome's JavaScript runtime` for easily
building fast, scalable network applications. Node.js uses an
`event-driven`, `non-blocking I/O` model that makes it lightweight and
efficient, perfect for data-intensive real-time applications that run
across distributed devices.

Node.js allows the creation of `web servers, networking tools, and a
collection of "modules"`. Modules handle File system I/O, Networking,
Binary data, Cryptography functions, Data streams, etc.

Common framework: Express.js, Socket.io, etc.

Node.js applications can run on Windows, Unix, Mac OS X

Node.js applications can be written by any language that can compile to
JavaScript like CoffeScript, TypeScript.

The biggest difference between PHP and Node.js is that PHP is a blocking
language (commands execute only after the previous command has
completed), while Node.js is a **non-blocking** language(commands
execute in parallel, and use **callbacks to signal completion**).

Node.js brings **event-driven programming** to web servers, enabling
development of fast web servers in JavaScript. Developers can create
highly scalable servers without using threading, by using a simplified
model of event-driven programming that uses callbacks to signal the
completion of a task.

Node.js was created because concurrency is difficult in many server-side
programming languages, and often leads to poor performance. Node.js
connects the ease of a scripting language with the power of UNIX network
programming.

Node.js is built on the Google V8 JavaScript engine, because:
- V8 is open-source
- V8 us extremely fast
- V8 is focused on the web
- JavaScript is a well-known language within web development, making it
  accessible to many web developers

# History

2009: Node.js was invented by Ryan Dahl. The project received a standing
ovation.

2011: a package manager was introduced for NOde.js library, called
`npm`.

December 2014: Fedor Indutny started [io.js](https://iojs.org), a fork
of Node.js.  io.js was created as an open governance alternative with a
separate technical committee.

# Technical

## Threading

Node.js operates on a single thread, using non-blocking I/O calls. The
design of sharing a single thread between all the requests means it can
be used to build highly concurrent applications. The design goal of a
Node.js application is that any function performing I/O must use a
callback.

A downside of this approach is that Node.js doesn't allow scaling with
the number of CPU cores of the machine it is running on without using an
additional module such as
[cluster](https://nodejs.org/api/cluster.html), [StrongLoop Process
Manager](http://strong-pm.io/), or
[pm2](https://github.com/Unitech/pm2).

## V8

V8 compiles JavaScript source code to native machine code instead of
interpreting it in real time.

Node.js contains libuv to handle asynchronous events.


# Version Manager

## Node Version Manager - nvm



# Package management

## yarn



## npm

### npm cheat sheet

#### Install a package and also update package.json with the installed version and package name.

```
npm install <module-name> --save
```

#### Install a package and also update package.json with the installed version and package name, but into the devDependencies section.

```
npm install <module-name> --save-dev
```

#### Set --save as a default for ```npm install ```.

```
npm config set save true
```

#### Generate package.json in a module directory, based on npm parmaters.

```
npm init
```


#### List all npm configuration flags.

```
npm config ls -l
```


#### Install a version not from a git repository and not from the npm directory, for example:

```
npm install git://github.com/substack/node-browserify.git
```

#### Update the global npm version.

```
npm update npm -g
```

#### Display the readme.md / documentation / npmjs.orf page of a give library.

```
npm docs <module-name>
```

#### Run package test suite, based on setup in package.json in:

``` "scripts" : {"test" : "node testfile.js"} ```


```
npm test
```

#### Uninstall package (A nice thing about npm is you can always just ```rm -rf ./node_modules/<module_name>```).

```
npm uninstall <module_name>
```

#### Locally edit a dependency.

```
npm edit <module_name>
```

#### Setup editor for ```npm edit ``` :

```
npm config set editor "sublime"
```

#### Publish a package not under the default "latest" tag:

```
npm publish --tag beta
```

#### List outdated libraries compared to currently installe node_modules:

```
npm outdated
```

#### Lock down dependency versions:

```
npm shrinkwrap
```

#### Install a git specific release

```
npm install git://github.com/Marak/colors.js#v0.6.0
```

#### Easter Eggs

```
npm xmas
```

```
npm visnup
```

```
npm substack
```


# Tools

## Frameworks
- Server frameworks: Express.js, Socket.io, Koa.js, Hapi.js
- MVC frameworks: Meteor, Derby, Sails, Mean, Tower.js

