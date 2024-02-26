# Overview

AngularJS framework (note: this is not Angular framework, this is the
older version). End of life December 31, 2021.
- A client-side JavaScript framework.
- AngularJS extends HTML attributes with **Directives**, and binds data
  to HTML with **Expressions**.
- AngularJS is distributed as a JavaScript file, and can be added to a
  web page with a script tag:

```html
<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
```

- It is used in Single Page Application (SPA) projects.
- Philosophy
    + Is built around the belief that **declarative programming** should
      be used for building **user interfaces and connecting software
      components**, while **imperative programming** is better suited to
      defining an **application's business logic**.

- Developer Guide
    + https://docs.angularjs.org/guide
- API
    + https://docs.angularjs.org/api

- Testing
    + `scope.$digest`: flushes/evaluates all the promises
        * This is needed in testing to run all the code in the function
        * One way to test that the test is hitting all the code is that
          using `console.log` to see whether that piece of code is
          executed

- Improve unit tests by replace headless Chrome with Node + Jest + JSDOM
    - Jest: https://github.com/facebook/jest
    - https://freecontent.manning.com/testing-with-node-jest-and-jsdom/
    - JSDOM: https://github.com/jsdom/jsdom
- Testing framework
    - Mocha: https://www.npmjs.com/package/mocha (BDD test definitions)
    - Chai: https://www.npmjs.com/package/chai (assertion library)
    - Sinon: https://www.npmjs.com/package/sinon (test doubles, spies, fakes)
    - angular-mocks: https://docs.angularjs.org/guide/unit-testing
    - https://www.codementor.io/@codementorteam/javascript-testing-framework-comparison-jasmine-vs-mocha-8s9k27za3
    - https://raygun.com/blog/mocha-vs-jasmine-chai-sinon-cucumber/
- Testing strategy
    - TDD vs. BDD vs. something else
- End-to-end testing (E2E)
    - Protractor: https://www.protractortest.org/
    - TestCafe: https://github.com/DevExpress/testcafe
    - https://www.testim.io/blog/end-to-end-testing-vs-integration-testing/
    - https://www.testim.io/blog/e2e-testing
- https://gulpjs.com/
- Improve linter with internal styles

# Component

- https://docs.angularjs.org/guide/component
- An application is a tree of components.
- Components only control their own View and Data.
- Public API
    + Inputs:
        * `<`: one-way binding, the bound properties in the component
          scope is not watched, which means if you assign a new value to
          the property in the component scope, it will not update the
          parent scope
            - Note however, that both parent and component scope
              reference the same object, so if you are changing object
              properties or array elements in the component, the parent
              will still reflect that change
            - The general rule should therefore be to never change an
              object or array property in the component scope
        * `@`: it can be used when the input is a string, especially
          when the value of the binding doesn't change
    + Outputs:
        * `&`: which function as callbacks to component events
    + Instead of manipulating Input Data, the component calls the
      correct Output Event with the changed data.
        * That way, the parent component can decide what to do with the
          event (e.g. delete an item or update the properties)
- Lifecycle hooks
    + `$onInit()`: called after construction and bindings
    + `$onChanges(changesObj)`:
    + `$doCheck()`
    + `$onDestroy()`

# Modules

- https://docs.angularjs.org/guide/module
- https://docs.angularjs.org/api/ng/type/angular.Module

# Logging

- https://docs.angularjs.org/api/ng/service/$log
