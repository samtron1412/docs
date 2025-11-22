[TOC]

# Overview

- https://www.typescriptlang.org/
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

# Introduction

## What is JavaScript? A Brief History

- JavaScript (a.k.a. ECMAScript) staged its life as a simple scripting
  language for browsers.
- TypeScript: A static type checker
    + TypeScript is a **typed** superset of JavaScript.
    + You can configure how strictly TypeScript checks your code.
    + You can also bypass some restrictions.
    + Runtime Behavior: the same as JavaScript
    + Erased types when the code is compiled to JavaScript.
    + Objects with the same shape are considered to be the same type
      (duck/structural typing)

## Compared with Java/C#

- Java/C#: mandatory OOP with class is the basic unit of code
  organization

### TypeScript

- Free functions (not in class/struct) and data in JavaScript
- Static classes: singletons and static classes are unnecessary in
  TypeScript.
    + Static classes: no extending, no instantiating
    + Any function or object can fulfill this role
- Rethinking types
    + Nominal Reified type system: the types we wrote in the code
      are present at runtime, and the types are related via their
      declarations, not their structures.
    + Types as sets: in TypeScript, a type is a set of values that
      share something in common.
        * Because types are just sets, a particular value can belong to
          many sets at the same time.
    + Erased structural types: TypeScript's type system is structural,
      not nominal.
        * The relationships between types are determined by the
          properties they contain, not whether they were declared with
          some particular relationship.
        * TypeScript's  type system is also not reified: there's nothing
          at runtime that will tell us that `obj` is `Pointlike`. In
          fact, the `Pointlike` type is not present in `any form` at
          runtime.
- Consequences of Structural Typing
    + Empty Types: any object is belong Empty type set since that object
      contains all the properties of the Empty type.
    + Identical Types: different names, but the same structure. This is
      not common.
    + Reflection: cannot have type system information at runtime since
      the type system is fully erased when it's compiled.

## TypeScript for Functional Programmers

### Built-in types

- Primitives: number, string, bigint, boolean, symbol, null, undefined,
  object
- Others: unknown, never, object literal, void (subtype of undefined),
  T[] (mutable arrays, [T, T]: tuples, `(t: T) => U: functions`

### `readonly` and `const`

- `const`: reference is immutable, but referent is still mutable
- `readonly` modifier for properties
- `Radonly<T>` mapped type to makes all properties be constant
- `ReadonlyArray<T>`: mapped type to make an Array readonly
- Const-assertion for arrays and object literals
    + `let a = [1, 2, 3] as const;`

# Linting, Linter, ESLint Rules (husky, lint-staged)

- `readonly`
    + https://typescript-eslint.io/rules/prefer-readonly/
    + https://typescript-eslint.io/rules/prefer-readonly-parameter-types

## Naming convention

- https://typescript-eslint.io/rules/naming-convention
- https://makecode.com/extensions/naming-conventions
- https://ts.dev/style/
- https://google.github.io/styleguide/tsguide.html

## Git Hooks for enforcing linting, formatting (husky, lint-staged)

- `npm install --save-dev husky`
- Create
    + `.husky/pre-commit` file with content `npx lint-staged`
    + `.lintstagedrc` file with following content

```
{
  "*.{js,jsx,ts,tsx,html,css,scss,md,json,yaml,yml}": "prettier --write --cache",
  "{lib,test}/**/*.{js,jsx,ts,tsx}": "eslint --fix --cache"
}
```

- Rebuild the package to install husky, and then from now on, before git
  commit it will lint and format your committing code.

# Handbook

## The Basics

- https://www.typescriptlang.org/docs/handbook/2/basic-types.html

## Everyday Types

### Type Assertions

- https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions
- `as <type>`

### Function Types

- https://2ality.com/2020/04/typing-functions-typescript.html
- https://stackoverflow.com/questions/29689966/how-to-define-type-for-a-function-callback-as-any-function-type-not-universal

## Narrowing

- https://www.typescriptlang.org/docs/handbook/2/narrowing.html

## More on Functions

- https://www.typescriptlang.org/docs/handbook/2/functions.html

## Object Types

- https://www.typescriptlang.org/docs/handbook/2/objects.html

### Index Signatures

- https://www.typescriptlang.org/docs/handbook/2/objects.html#index-signatures
- Sometimes you don’t know all the names of a type’s properties ahead of
  time, but you do know the types of the possible values.
    + In those cases you can use an index signature to describe the
      types of possible values.
    + An index signature property type must be either ‘string’ or
      ‘number’.
- It is possible to support both types of indexers, but the type
  returned from a numeric indexer must be a subtype of the type returned
  from the string indexer.

## Type Manipulation

### Conditional Types

- https://www.typescriptlang.org/docs/handbook/2/conditional-types.html

## Classes

- https://www.typescriptlang.org/docs/handbook/2/classes.html

## Modules

- https://www.typescriptlang.org/docs/handbook/modules.html
- https://www.typescriptlang.org/tsconfig#module
- https://nodejs.org/api/esm.html
- https://nodejs.org/api/modules.html
- https://nodejs.org/api/packages.html

# Reference (Deeper explanation than Handbook)

## Utility Types

- Record type
    + https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type
    + Use `Object` as a map
    + https://howtodoinjava.com/typescript/difference-between-record-and-map/
    + Differences between `Object` and `Map` in JavaScript
        * https://stackoverflow.com/questions/18541940/map-vs-object-in-javascript
    + Good for configurations / static data
    + Use `Map` for dynamic data (update, modify the data) instead of
      `Record`

## Enums

- Enum vs `as const`
    + Prefer `const x = {} as const` instead due to some surprises from
      how enums are implemented in TypeScript.
        * Enum is not a native feature of JavaScript. `as const` object
          is a native feature of JavaScript.
        * https://www.typescriptlang.org/docs/handbook/enums.html#objects-vs-enums
    + https://www.youtube.com/watch?v=vBJF0cJ_3G0&t=1012s
    + https://www.youtube.com/watch?v=jjMbPt_H3RQ
- https://www.typescriptlang.org/docs/handbook/enums.html
- Numeric or string-based enums.

# Tutorials

# Declaration Files

# Project Configuration

# JavaScript


# Tips and tricks

## Get all possible key path of an object type

- https://dev.to/pffigueiredo/typescript-utility-keyof-nested-object-2pa3/comments

```typescript
type NestedKeyOf<T, K = keyof T> = K extends keyof T & (string | number)
  ? `${K}` | (T[K] extends object ? `${K}.${NestedKeyOf<T[K]>}` : never)
  : never;
```

OR

```typescript
type NestedKeyOf<ObjectType extends object> ={
    [Key in keyof ObjectType & (string | number)]: ObjectType[Key] extends object
        ? `${Key}` | `${Key}.${NestedKeyOf<ObjectType[Key]>}`
        : `${Key}`
}[keyof ObjectType & (string | number)];
```

- Infer the value type and update the field dynamically

```typescript
// Recursively building the key paths of a type T.
type KeyPath<T, K = keyof T> = K extends keyof T & (string | number)
  ? `${K}` | (T[K] extends object ? `${K}.${KeyPath<T[K]>}` : never)
  : never;

// Infer the value type from the key paths of a type T.
type ValueType<T, P extends string> = P extends `${infer Key}.${infer Rest}` // Split the key path
  ? Key extends keyof T // Check if the first segment is a valid key
    ? T[Key] extends Array<infer ElementType> // If it's an array
      ? Rest extends `${number}.${infer NestedRest}` // Handle array indexing and nested access
        ? ValueType<ElementType, NestedRest>
        : Rest extends `${number}` // Handle array indexing
          ? ElementType
          : ValueType<T[Key], Rest> // Handle non-array nested access
      : ValueType<T[Key], Rest> // Handle non-array objects
    : never // If the key doesn't exist, the path is invalid
  : P extends keyof T // If there are no dots, resolve directly
    ? T[P]
    : never;

type Action<T, R> = {
  type: R;
  keyPath: KeyPath<T>;
  value: ValueType<T, KeyPath<T>>;
}

function updateNestedProperty<T>(
  obj: T,
  path: KeyPath<T>,
  value: ValueType<T, typeof path>
): T {
  const keys = path.split('.');
  const [key, ...rest] = keys;

  if (!key) {
    return value as T; // Type assertion for the final value
  }

  return {
    ...obj,
    [key]: rest.length > 0
      ? updateNestedProperty(obj[key], rest.join('.') as KeyPath<T[keyof T]>, value as ValueType<T[keyof T], KeyPath<T[keyof T]>>)
      : value,
  };
}
```

## How to overload functions?

- https://bobbyhadz.com/blog/typescript-duplicate-function-implementation

## How to create a map in TypeScript

- https://timmousk.com/blog/typescript-map/
    + A JS indexed object with a mapped TypeSript type.
    + The built-in Map structure introduced in ES6.

## Cannot reassign to read only property such as `window.location.assign`

- Mainly, in testing we want to mock some readonly property
- Copy the object to a new object, then overwrite the property there:
    + `const location = Object.assign({}, window.location)`
    + `location.assign = ...`

## Delete a non optional property

- `// @ts-ignore`, then using `delete`
- `Reflect.deleteProperty(<object>, '<property>')`
    + `Reflect.deleteProperty(global.window, 'location')`
- `delete (window as any).location;`

## Alternatives to `any`

- https://betterprogramming.pub/4-ways-to-replace-any-in-typescript-5470b8d8357d
- Using `unknown`: `Record<string, unknown>`
    + the type-safe counterpart that forces the developer to add checks
      (type guards) or to cast the variable before usage.
    + Some typical checks include the instanceof and typeof operators
    + Type predicates: https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates
- Union types: `|`
- Generics

## Declaring global variables in TypeScript

- https://mariusschulz.com/blog/declaring-global-variables-in-typescript

```typescript
// Type Assertion
const initialData = (window as any).__INITIAL_DATA__;


// declare a global variable
export function someExportedFunction() {
  // ...
}

declare global {
  var __INITIAL_DATA__: InitialData;
}

const initialData = window.__INITIAL_DATA__;


// Augmenting the Window Interface
export function someExportedFunction() {
  // ...
}

declare global {
  interface Window {
    __INITIAL_DATA__: InitialData;
  }
}

const initialData = window.__INITIAL_DATA__;
```

## Dynamically set an object's property name from a variable

- https://bobbyhadz.com/blog/typescript-set-object-property-name-from-variable

```typescript
type Person = {
  name: string;
  country: string;
};

const myVar = 'name';

const obj: Person = {
  [myVar]: 'Tom',
  country: 'Chile',
};

console.log(obj); // 👉️ {name: 'Tom', country: 'Chile'}
```

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
