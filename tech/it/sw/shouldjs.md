# Overview

- `should` is an expressive, readable, framework-agnostic assertion
  library.
- By default `should` extends the `Object.prototype` with a single
  non-enumerable getter that allows you to express how that object
  should behave.
- API
    + `.not`: negates the current assertion
    + `.any`: allows for assertions with multiple parameters to assert
      any of the parameters (but not all). This is similar to the native
      JavaScript array.some.
    + Chaining assertions: every assertion will return a
      `should.js`-wrapped object, so assertions can be chained.
    + `.an`, `.of`, `.a`, `.and`, `.be`, `.have`, `.with`, `.is`,
      `.which`: use them for better readability, they do nothing
