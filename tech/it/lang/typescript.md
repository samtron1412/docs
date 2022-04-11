[TOC]

# Overview

- TypeScript
    + A typed superset of JavaScript that is maintained by Microsoft
    + TypeScript can be compiled to JavaScript using TypeScript Compiler
      (TSC)
    + Features
        * Cross-platform: macOS, Windows, Linux
        * Static-type checking
        * OOP
        * Optional Static typing
        * DOM Manipulation
        * ES6 Features: can be converted to ES5
        * Type definitions:  auto-completion, suggestion for APIs
- Installing TypeScript
    + `npm install -g typescript`: globally install
    + `npm install typescript`: locally install
- Usage
    + `npx tsc <ars>`: if typescript is installed locally
    + `tsc -v`: check version
    + `tsc -h`: help
    + `tsc -w/--watch`: watch changes in file to re-run compiler
    + `tsc --pretty`
    + `tsc --all`
    + `tsc --init`: initialize a new typescript project with
      tsconfig.json
- Basic types for typescript
    + string, number, boolean, string[], undefined, void, any
    + enum: `enum Color {Red, Green, Blue};`
        * `let carColor: Color = Color.Red;`
    + union types:
        * `let isUserCreated: string|boolean;`
        * `isUserCreated = false;`
        * `isUserCreated = "alkdfj";`
    + array
        * `const accounts: number[] = [1,2,3];`
        * `const accounts: [number, string] = [1, "2"];`

# ESLint Rules

- `readonly`
    + https://typescript-eslint.io/rules/prefer-readonly/
    + https://typescript-eslint.io/rules/prefer-readonly-parameter-types

# Modules

- https://www.typescriptlang.org/docs/handbook/modules.html
- https://www.typescriptlang.org/tsconfig#module
- https://nodejs.org/api/esm.html
- https://nodejs.org/api/modules.html
- https://nodejs.org/api/packages.html

# Tips and tricks

## Using JS library for TypeScript

- https://medium.com/@steveruiz/using-a-javascript-library-without-type-declarations-in-a-typescript-project-3643490015f3
    - Definitely Typed repository: https://github.com/DefinitelyTyped/DefinitelyTyped
    - Create the declaration file by yourself

## interface vs. class

- https://ultimatecourses.com/blog/classes-vs-interfaces-in-typescript
- interfaces do not generate any JavaScript source code, and it
  represents a contract
    + Use it to type check anywhere you want
- only use class if you want to create some instances of it
    + it generate a lot of JavaScript code (prototypes)

# References

[wiki]: https://en.wikipedia.org/wiki/TypeScript
[why]: https://stackoverflow.com/questions/12694530/what-is-typescript-and-why-would-i-use-it-in-place-of-javascript
