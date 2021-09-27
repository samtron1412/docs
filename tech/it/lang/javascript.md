[TOC]

# Overview

- Learning JavaScript
    + https://javascript.info/js
    + https://developer.mozilla.org/en-US/docs/Web/JavaScript
    + https://felix-kling.de/jsbasics/
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

# Code pattern

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

# JavaScript engine

- A JavaScript engine is a computer program which interprets and executes
  JavaScript code.
    + Using just-in-time compilation to improve performance
- Although there are several uses for a JavaScript engine, it is most
  commonly used in web browsers
- Popular engines
    +

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

# Tips and Tricks

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

## Callback hell

- Nested callbacks
- Hard to maintain and errors handling
- Use Promise or Observable instead

# References

[typescript-js]: http://stackoverflow.com/questions/12694530/what-is-typescript-and-why-would-i-use-it-in-place-of-JavaScript/35048303#35048303
[list]: https://github.com/jashkenas/coffeescript/wiki/List-of-languages-that-compile-to-JS
[coffee-type-dart]: https://www.quora.com/Should-I-learn-CoffeeScript-TypeScript-or-Dart
