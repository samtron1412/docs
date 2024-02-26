[TOC]

# [Overview](http://gulpjs.com/)

- [GitHub](https://github.com/gulpjs/gulp)
- Based on NodeJS, so look at `nodejs.md` for concepts such as: stream,
  pipe, etc.

# Concepts

- https://gulpjs.com/docs/en/api/concepts
- Vinyl
    + A metadata object that describes a file.
    + Main properties
        * `path` and `contents`
- Vinyl adapters
    + Ways to access files that represented by Vinyl objects.
    + Eac file source is accessed using a Vinyl adapter.
    + Methods
        * `src(globs, [options])`: returns a stream that produces Vinyl
          objects.
        * `dest(folder, [options])`: returns a stream that consumes
          Vinyl objects.
        * Others
- Tasks
    + Each gulp task is an asynchronous JavaScript function that either
      accepts an error-first callback or returns a stream, promise,
      event emitter, child process, or observable.
- Globs
    + A glob is a string of literal and/or wildcard characters (`*`,
      `**`, `!`) used to match filepaths.
    + Globbing is the act of locating files on a file system using one
      or more globs.
    + Glob base (glob parent) is the path segment before any special
      characters in a glob string.
        * Glob base of `/src/js/**.js` is `/src/js/`
- File system stats:
    + File metadata is provided as an instance of Node's `fs.Stats`.
    + It is available as the `stat` property on the Vinyl instances.
    + It is used internally to determine if a Vinyl object represent a
      directory or symbolic link.
    + When written to the file system, permissions and time values are
      synchronized from the Vinyl object's stat property.
- File system modes
    + File system modes determine what permissions exist for a
      file. Most files and directories on your file system will have a
      fairly permissive mode, allowing gulp to read/write/update files
      on your behalf. By default, gulp will create files with the same
      permissions as the running process, but you can configure the
      modes through options in src(), dest(), etc. If you're
      experiencing permission (EPERM) issues, check the modes on your
      files.

# Getting Started

## Creating Tasks

- https://gulpjs.com/docs/en/getting-started/creating-tasks
