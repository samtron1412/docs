[TOC]

# Overview

- Learning JavaScript
    + https://javascript.info/js
    + https://developer.mozilla.org/en-US/docs/Web/JavaScript
    + https://felix-kling.de/jsbasics/
    + https://github.com/getify/You-Dont-Know-JS
        * 1st edition: https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/README.md
- Execution and Interpretation: Microtasks vs. tasks
    + https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/
    + https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide
- Language Specification/Feature
    + Object and Prototype
        * https://levelup.gitconnected.com/the-javascript-object-paradigm-and-prototypes-explained-simply-e9cb9eaa49aa
        * https://stackoverflow.com/questions/53199341/object-vs-prototype-in-javascript
        * https://github.com/getify/You-Dont-Know-JS/tree/0cc17c53ff772e20dfd6a7072c965df2486116e8/this%20%26%20object%20prototypes
    + Function
    + Promise
        * https://github.com/kriskowal/uncommonjs/blob/master/promises/specification.md
        * https://promisesaplus.com/
        * https://github.com/kriskowal/q
    + Write a JavaScript framework or library
    + `window`
    + HTML DOM
        * HTML DOM Events: https://www.w3schools.com/jsref/dom_obj_event.asp
- Books
    + Javascript : The Definitive Guide (David Flanagan)
    + Javascript: The Good Parts by Douglas Crockford
    + Javascript Patterns by Stoyan Stefenov
    + https://felix-kling.de/jsbasics/

# Testing

## Automation

- Task runner: Grunt, Gulp, npm scripts, etc.
    + linting, minifying, adding CSS prefixes, transpilling, running
      tests, etc.
- Browser automation system: Selnium, Cypress, PlayWright, Nightwatch,
  etc.
    + run specific tests on installed browsers and return results

## Unit tests

- https://medium.com/welldone-software/an-overview-of-javascript-testing-7ce7298b9870
- https://medium.com/swlh/a-road-to-the-ultimate-testing-setup-with-jest-and-headless-chrome-browser-83f14e3799e3
- https://github.com/facebook/jest
- https://github.com/mochajs/mocha
- https://github.com/jasmine/jasmine
- https://github.com/jsdom/jsdom

## Integration/end-to-end tests

- https://www.selenium.dev/
- https://github.com/puppeteer/puppeteer
- https://webdriver.io/
- https://www.cypress.io/
- https://playwright.dev/
- Articles
    + https://www.reddit.com/r/QualityAssurance/comments/srhafv/cypress_vs_playwright/
    + Performance/Speed comparison: https://blog.checklyhq.com/cypress-vs-selenium-vs-playwright-vs-puppeteer-speed-comparison/

# Debugging

- Source map (sourcemap)
    + https://web.archive.org/web/20220125022251/html5rocks.com/en/tutorials/developertools/sourcemaps/
        * https://developer.chrome.com/blog/sourcemaps/
        * https://firefox-source-docs.mozilla.org/devtools-user/debugger/how_to/use_a_source_map/index.html
    + https://www.bugsnag.com/blog/source-maps
    + A file that contains a mapping to help the debugger reconstructs
      the original source code from transformed (compressed/combined)
      source. (local development)
- Source Map Revision 3
    + https://docs.google.com/document/d/1U1RGAehQwRypUTovF1KRlpiOFze0b-_2gc6fAH0KY0k/edit

# Expressions and operators

## Optional Chaining

- `?.`
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining

## Nullish coalescing

- `??`: double question marks
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator
    + where `||` returns the right side for all falsy left side values,
      `??` only return the right side if the left side is `null` or
      `undefined`.
- Examples:

```JavaScript
const foo = null ?? 'default string';
console.log(foo);
// Expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// Expected output: 0

const val = obj.x.y ?? 0;
```

# Code pattern

## Global objects / variables

- https://developer.mozilla.org/en-US/docs/Glossary/Global_object
- https://stackoverflow.com/questions/11938380/global-variables-in-angularjs
- https://2ality.com/2019/07/global-scope.html

## Prototype

Use to code plugin JavaScript

## OOP Coding

### The module

First we declare an JavaScript object

```js
var s, loginApp = {

};
```

### Settings

The settings function contains all significant elements (DOM nodes),
static variables and things need for global.

```js
$(document).ready(function(){
        var setting = {
                loginForm: $('#loginForm'),
                userId: $('input[name=userId]'),
                password: $('input[name=password'),
                errorMessage: $('span.errorMessage')
        };
});
```

### Init function

To "kick things off" we'll have just only one function be called. This
will be consistent across all modules, so you know exactly where to look
when you start reading the code and figuring out what happens when.

We will pass setting variables to initial function for get all DOM
nodes:

```js
var s, loginApp = {
        init: function(param){
                s = param;
        };
};
```

### Binding UI action

We would have a function just for binding the UI events. You never write
any code that "does stuff" when you bind, you just do the binding and
then call another appropriately named sub-function.

BindingUIAction will be called in initial function for "kick things off"

```js
var s, loginApp = {
        init: function(){
                s = this.setting;
                this.bindUIActions();
        },

        bindUIActions: function(){
                s.loginForm.validate();
        }
};
```

### Validation

#### I. Need add jquery plugin validate on page

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Login Page</title>
    <link rel="stylesheet" type="text/css" href="{{urlResource('assets/css/lib/bootstraps/bootstrap.css')}}">

    <!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
    <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
    <![endif]-->
    <script src="{{urlResource('assets/js/lib/jquery/jquery-1.11.2.js')}}"></script>
    <script src="{{urlResource('assets/js/lib/bootstraps/bootstrap.js')}}"></script>

    <script src="{{urlResource('assets/js/lib/jquery/jquery.validate.js')}}"></script>

</head>
```

#### II. Call validate function on form element need to validate.

```js
s.loginForm.validate({
        onfocusout: function(element){ $(element).valid(); }
});
```

The onfocusout function help to execute validate element on blur event.

#### III. Validate Properties

##### 1. `rules`: Read, add and remove rules for an form's child element.

Example:

```js
s.userId.rules("add", {
        required: true,
        maxlength: 20
});
```

**Rules properties**
- Makes the element required: `required: (true or false)`
- Request a remote resource to check the element for validity: `remote:
  {...}`
    + Example: Makes the email field required, is an email and does a
      remote request to check if the given email address is available or
      not.

```js
$( "#myform" ).validate({
  rules: {
    email: {
      required: true,
      email: true,
      remote: {
        url: "check-email.php",
        type: "post",
        data: {
          username: function() {
            return $( "#username" ).val();
          }
        }
      }
    }
  }
});
```
- Min length: `minlength: (number)`
- Max length: `maxlength: (number)`
- Range length: `rangelength: (array of range)`
- Valid email: `email: (true or false)`
- Valid url: `url: (true or false)`
- Date: `date: (true or false)`
- Decimal number: `number: (true or false)`
- Digits only: `digits: (true or false)`
- Credit card number: `creditcard: (true or false)`

#### Some Helper function

1. errorClass: "class name"
2. wrapper: "html element"
3. highlight: function(element, errorClass, validClass)
4. unhighlight: function(element, errorClass, validClass)

Example

```js
var validator = s.loginForm.validate({
        onfocusout: function(element) { $(element).valid(); },
        wrapper: "span",
        errorClass: "text-danger",
        highlight: function(element, errorClass, validClass) {
                $(element).closest('div').addClass('has-error');
        },
        unhighlight: function(element, errorClass, validClass){
                $(element).closest('div').removeClass('has-error');
        }
});
```

#### About Datatablles plugin

Use datatables: `$('#employeeTable').DataTable();`

Setting

```js
$('#employeeTable').DataTable({
        scrollY: 300,
        paging: false
});
```

Please visit here for full options: https://datatables.net/reference/option/

# JavaScript Modules

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules
- https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c
- JS programs started off pretty small
    + Isolated scripting tasks, providing a bit of interactivity to your
      web pages.
- Complex projects necessitate a mechanism for splitting JS programs
  into separate modules that can be imported when needed.
    + Libraries and frameworks that enable module usage:
        * CommonJS and AMD-based module systems: RequireJS
        * webpack
        * Babel
    + Node.js
- All modern browsers support module features natively without needing
  transpilation.
    + Browsers can optimize loading of modules, making it more efficient
      than having to use a library and do all of that extra client-side
      processing and extra round trips.
    + It does not obsolete bundlers like webpack
        * Bundlers still do a good job at partitioning code into
          reasonably sized chunks, and are able to do other
          optimizations like minification, dead code elimination, and
          tree-shaking.

# JavaScript engine

- A JavaScript engine is a computer program which interprets and executes
  JavaScript code.
    + Using just-in-time compilation to improve performance
- Although there are several uses for a JavaScript engine, it is most
  commonly used in web browsers
- Popular engines

## Active projects

- [Rhino](https://en.wikipedia.org/wiki/Rhino_(JavaScript_engine)):
  managed by the Mozilla Foundation, open source, developed entirely in
  Java
- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)): open
  source, developed by Google in Denmark, part of Google Chrome
- [JavaScriptCore](): open source, marketed as Nitro and developed by
  Alpple for Safari
- [Chakra](): for Microsoft Edge

# Node.js

Node.js is an **open source**, cross-platform runtime environment for
developing server-side Web applications. The runtime environment
interprets JavaScript using Google's **V8** JavaScript engine.

Node.js has an **event-driven architecture** capable of **asynchronous
I/O**. These design choices are meant to optimize **throughput** and
**scalability** in Web applications with many input/output operations,
as well as for real-time Web applications.

- 3 components
    + Callback stack
    + Asynch API
    + EventLoop
- Asynchronous APIs
    + `setTimeout(callback, interval);`
- Problem: callback hell
    + Fix: PROMISES

```javascript
const response = getAPIGet(); // response is a promise
response.then((response) => {
    console.log(response);
})
```
- Promises vs. Observables
    + Promises only give you data once, and it is JavaScript native
    + Observables can return data multiple times, and it is provided
      through `RxJS` library (reactive programming)
    + https://auth0.com/blog/javascript-promises-vs-rxjs-observables/
    + https://stackoverflow.com/q/50269671/1683888

## Tutorials

### Build a simple web server

- http://blog.modulus.io/build-your-first-http-server-in-nodejs

## Packages

### npm - node package manager

npm is the default package manager for the JavaScript runtime
environment Node.js.

- Install a package globally: `# npm install -g package-name`

### Bower

Bower is a package management system for **client-side programming** on
the World Wide Web. It depend on Node.js and npm.

#### [API](http://bower.io/docs/api/)

### http-server

http-server is a simple command-line http server.

- Install globally: `# npm install -g http-server`

Usage: `$ node /bin/http-server`

# [TypeScript vs JavaScript][typescript-js]

# [List of languages that compile to JavaScript][list]

# Linting and Formatting

- Requirements
    + Should be built into the build process to make sure it always run
      for everyone regardless of their IDEs and settings.
- ESLint vs Prettier
    + https://prettier.io/docs/en/comparison
    + Prettier: formating rules: max-len, no-mixed-spaces-and-tabs,
      comma-style, etc.
    + ESLint: code-quality rules: no-unused-vars, no-extra-bind,
      no-implicit-globals, etc.

# Tips and Tricks

## Fuzzy Search

- https://github.com/leeoniya/uFuzzy/tree/main
- https://github.com/farzher/fuzzysort/tree/master
- https://github.com/krisk/fuse
- https://github.com/bevacqua/fuzzysearch/tree/master
- https://github.com/bevacqua/horsey

## Dollar Sign

- `$` is usually assigned to the jQuery object itself
    + `window.jQuery = window.$ = jQuery;`
    + `$(params)`: passing `params` to the jQuery object.
- Template literal in ES6: `${..}`
- Usually it's related to jQuery or built-in feature that support by
  browsers
    + `$(function() {...});` is equivalent to
      `$(document).ready(function() {...});`
        * ensure that the function is called once after all the DOM
          elements of the page are ready to be used.
        * https://stackoverflow.com/questions/7642442/what-does-function-do
        * https://stackoverflow.com/questions/22244823/what-is-the-dollar-sign-in-javascript-if-not-jquery

## Memory Management

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management
- Mark and sweep algorithm
    + Traverse from roots (global objects), mark all reachable objects
      from roots.
    + Sweep all non-reachable objects

## clone

- https://medium.com/@tiagobertolo/which-is-the-best-method-for-deep-cloning-in-javascript-are-they-all-bad-101f32d620c5
- Avoid JSON cloning: `JSON.parse(JSON.stringify(obj))` due to data loss
- Lodash deepClone or other libraries
- Write your own clone method.

## lodash vs. built-ins

- https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore
- https://youmightnotneed.com/lodash/
- https://www.sitepoint.com/lodash-features-replace-es6/
- https://blog.bitsrc.io/you-dont-need-lodash-or-how-i-started-loving-javascript-functions-3f45791fa6cd
- https://stackoverflow.com/questions/13789618/differences-between-lodash-and-underscore-js

## Object to Array

- https://www.samanthaming.com/tidbits/76-converting-object-to-array/

## Currying

- Currying is a technique of converting a function that takes multiple
  arguments into a sequence of functions that each takes a single
  argument.
- It can be useful to avoid repeating yourself when you would have been
  calling the same JavaScript built-ins over and over with all the same
  values but one.
    + So we can use currying to fix known parameters.
- https://stackoverflow.com/questions/113780/javascript-curry-what-are-the-practical-applications
- https://javascript.info/currying-partials
- https://medium.com/coding-in-depth/curry-recipe-in-javascript-af236028c8f7
-

```javascript
function converter(toUnit, factor, offset, input) {
    offset = offset || 0;
    return [((offset + input) * factor).toFixed(2), toUnit].join(" ");
}

var milesToKm = converter.curry('km', 1.60936, undefined);
var poundsToKg = converter.curry('kg', 0.45460, undefined);
var farenheitToCelsius = converter.curry('degrees C', 0.5556, -32);

milesToKm(10);            // returns "16.09 km"
poundsToKg(2.5);          // returns "1.14 kg"
farenheitToCelsius(98);   // returns "36.67 degrees C"

Function.prototype.curry = function() {
    if (arguments.length < 1) {
        return this; //nothing to curry with - return function
    }
    var __method = this;
    var args = toArray(arguments);
    return function() {
        return __method.apply(this, args.concat([].slice.apply(null, arguments)));
    }
}
```

## `isFinite()` vs `Number.isFinite()` vs `_.isFinite()`

- Global function `isFinite()` convert the argument to Number before
  checking:
    + Return `true` if the coerced argument is a Number
    + Return `false` if it is `+Infinity`, `-Infinity`, or `NaN`
- Lodash `_.isFinite()` is the same as `Number.isFinite()`
    + They do not convert the argument to Number
    + So the only `true` value is Number and finite

## _ variable with arrow function in ES6

- https://stackoverflow.com/questions/41085189/using-underscore-variable-with-arrow-functions-in-es6-typescript
- Should avoid `_` variable (ignored variables)
- Should use `_unusedVar` instead for unused variable

## Double exclamation mark operator

- https://brianflove.com/2014-09-02/whats-the-double-exclamation-mark-for-in-javascript/
- Shortcut for cast a value to boolean
    + falseys: 0, empty string, null, undefined, NaN
    + truthys: object, array, non-empty string, number other than 0,
      Date

## Three dots operator

- Similar pack and unpacking operators in Python (`*` for list and `**`
  for dictionary)
- `...`: rest and spread operator
    + https://dev.to/sagar/three-dots---in-javascript-26ci
    + rest operator `...params` is used in function definitions
    + spread operator `...args` is used in function calls

# Troubleshooting

## await vs. return vs. return await

- https://jakearchibald.com/2017/await-vs-return-vs-return-await/
- `return await` is redundant outside of `try/catch` block
    + Use `return await` only inside `try` block

## Callback hell

- Nested callbacks
- Hard to maintain and errors handling
- Use Promise or Observable instead

# References

## Glossary

- Template literals
    + https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
    + Tagged templates and raw strings
- Polyfill
    + https://developer.mozilla.org/en-US/docs/Glossary/Polyfill
    + A polyfill is a piece of code (usually JavaScript on the Web) used
      to provide modern functionality on older browsers that do not
      natively support it.

## Built-in objects

### null vs undefined

- Use null when you want to explicitly represent "no value."
- Let JavaScript use undefined for uninitialized variables or missing properties.

### Promise

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
- https://javascript.info/async
- Promise reject vs. throw
    + https://stackoverflow.com/questions/33445415/javascript-promises-reject-vs-throw
- `await vs. return vs. return await`
    + https://jakearchibald.com/2017/await-vs-return-vs-return-await/
- Reject handler vs. catch
    + https://stackoverflow.com/questions/52656159/javascript-promise-reject-handler-vs-catch
    + Better to have if condition in catch to handle checked exception,
      rather than having a Reject handler since it simplifies the logic.
- Cancel promises or async functions
    + https://stackoverflow.com/questions/30233302/promise-is-it-possible-to-force-cancel-a-promise/30235261#30235261
    + https://stackoverflow.com/questions/25345701/how-to-cancel-timeout-inside-of-javascript-promise
    + https://stackoverflow.com/questions/29478751/cancel-a-vanilla-ecmascript-6-promise-chain
    + https://stackoverflow.com/questions/21781434/status-of-cancellable-promises
    + Using `AbortController`

### Reflect

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect

### Proxy

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy
- Create a proxy for another object, which can intercept and redefine
  fundamental operations for that object.

## Expressions and Operators

### await

- https://javascript.info/async-await
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await
- The await operator is used to wait for a Promise.
- It can only be used inside an async function within regular JavaScript
  code; however it can be used on its own with JavaScript modules.
- If no `await` for an `async` function, then the async function will be
  executed normally, but the JavaScript interpreter will not wait for it
  to be finished before executing the next line in the current function.
    + https://stackoverflow.com/questions/55019537/is-possible-to-call-async-function-without-await-keyword-and-what-happens-if-we


## Declarations vs Statements

- You can see declarations as "binding identifiers to values", and
  statements as "carrying out actions".
- The fact that var is a statement instead of a declaration is a special
  case, because it doesn't follow normal lexical scoping rules and may
  create side effects — in the form of creating global variables,
  mutating existing var-defined variables, and defining variables that
  are visible outside of its block (because var-defined variables aren't
  block-scoped).

### Declarations

- `let, const, function, function*, async function, async function*,
  class, export, import`

#### `export` declaration (statement)

+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export
+ export object: https://stackoverflow.com/questions/34619640/what-is-the-best-way-to-export-an-object-literal-with-es6-2015
    * Destructuring a default export object: https://stackoverflow.com/questions/43814830/destructuring-a-default-export-object
+ Why using default exports?
    * https://stackoverflow.com/questions/46913851/why-and-when-to-use-default-export-over-named-exports-in-es6-modules
+ PREFER NAMED EXPORTS INSTEAD OF DEFAULT EXPORTS
    * Can export many things
    * Import the same name (only change names with `as` if it's
      necessary)
    * Early errors if trying to import something does not exist

#### `import` declaration:

+ Declarative import (`import` statement): https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
+ Dynamically import (`import()` call): https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import
    * Lazily import modules

#### `async function`

+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
+ An async function is a function declared with the async keyword,
  and the await keyword is permitted within it.
    * Async functions can contain zero or more await expressions.
+ The async and await keywords enable asynchronous, promise-based
  behavior to be written in a cleaner style, avoiding the need to
  explicitly configure promise chains.
+ RETURN VALUE: a `Promise` which  will be resolved with the value
  returned by the async function, or rejected with an exception
  thrown from, or uncaught within, the async function.

### Statements

## Functions

### The arguments object

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments


[typescript-js]: http://stackoverflow.com/questions/12694530/what-is-typescript-and-why-would-i-use-it-in-place-of-JavaScript/35048303#35048303
[list]: https://github.com/jashkenas/coffeescript/wiki/List-of-languages-that-compile-to-JS
[coffee-type-dart]: https://www.quora.com/Should-I-learn-CoffeeScript-TypeScript-or-Dart
