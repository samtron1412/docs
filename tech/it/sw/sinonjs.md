# Overview

- https://sinonjs.org/
- https://www.npmjs.com/package/sinon

- Standalone test spies, stubs and mocks for JavaScript.
- Works with any unit testing framework.

- Install using `npm`
    + `npm install sinon`
- Setting up access
    + `var sinon = require("sinon");`

# General setup

- https://stackoverflow.com/questions/39244242/what-is-the-correct-way-of-using-sinon-spy-restore-or-reset
- If you're using the following initialization
    + `let someSpy = sinon.spy(obj, 'someFunction');`
    + This will replace `obj.someFunction` with the spy. If you ever
      want to go back to the original function, you use
      `someSpy.restore()`.
    + `restore` the default sandbox (`sinon`) after each test may help
      with memory leak problems. (Although JavaScript already has its
      own garbage collector  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)

```mocha
afterEach(() => {
    sinon.restore();
}
```

- If you're creating new spies, stubs, etc. for each test, in
  `beforeEach`, then you don't have to restore or reset anything in
  `afterEach`.
    + `mockAlerts.error = sinon.stub()` (new stub each test)

# Spies

## General Information

- A test spy is a function that records arguments, return value, the
  value of `this` (context) and exception thrown (if any) for all its
  calls.
- There are two types of spies
    + Anonymous functions: replaced the existing methods
        * `mockAlerts.error  = sinon.spy()`
    + Others wrap methods that already exist in the system under test
      (wrap around the existing methods, so we can restore the original
      if needed)
        * Spy a function: `sinon.spy(myFunc)`
        * Spy all object methods: `sinon.spy(obj)`
        * Spy an existing method: `sinon.spy(obj, 'method')`
        * Spy property getter and setter: `sinon.spy(obj, 'property',
          ['get', 'set'])`
        * You can use `sinon.restore()` or `spy.restore()` or
          `spy.get.restore()` to restore the original method.
- API
    + `spy.callCount`: the number of recorded calls.
    + `spy.called`: true if the spy was called at lest once
    + `spy.notCalled`:  true if the spy was not called
    + `spy.calledOnce/Twice/Thrice`: true if the spy was called exactly
      once/twice/thrice
    + `spy.first/second/third/lastCall`: the first/second/third/last spy
      call
    + `spy.callWith(arg1, ...)`
    + `spy.callWithExactly(arg1, ...)`
    + `spy.args`: array of arguments received
    + `spy.getCalls()`: returns an array of Spy Calls
    + `spy.resetHistory()`: resets the state of a spy
    + `spy.restore()`: replaces the spy with the original method. Only
      available if the spy replaced an existing method.
    + Others...

## Spy Call

- A spy call is an object representation of an individual call to a
  spied function, which could be a spy, stub, fake or mock method.
- API
    + Similar spy API

# Stubs

- Test stubs are functions (spies) with pre-programmed behavior.
- They support the full test spy API in addition to methods which can be
  used to alter the stub's behavior.
- As spied, stubs can be either anonymous, or wrap existing functions.
- When to use stubs?
    + Use a stub when you want to:
        * Control a method's behavior from a test to force the code
          down a specific path. Examples include forcing a method to
          throw an error in order to test error handling.
        * Prevent a specific method from being called directly (possibly
          because it triggers undesired behavior, such as a
          `XMLHttpRequest` or similar)
- API
    + `sinon.stub()`: anonymous stub function
    + `sinon.stub(obj)`: stubs all object methods (NOT RECOMMENDED)
    + `sinon.stub(obj, 'method')`
    + `sinon.stub(obj, 'method').callsFake(fn)`
    + `sinon.withArgs(arg1, ...)`
    + `sinon.onCall(num)`
    + `sinon.onFirst/Second/ThirdCall()`
    + `stub.reset()`: resets both behavior and history (spy)
    + `stub.resetBehavior()`
    + `stub.resetHistory()`
    + `stub.returns(obj)`
    + `stub.resolves(value)`
    + `stub.rejects()`
    + `stub.usingPromise(promiseLibrary)`: causes the stub to return
      promises using a specific Promise library instead of the global
      one when using `stub.rejects` or `stub.resolves`. Returns the stub
      to allow chaining.


# Fakes

- `fake`: a fake `Function` with the ability to set a default behavior.
- Immutable behaviors: fakes' behaviors cannot be changed after creation
    + Safer and less bugs compared to stubs and spies
- Fakes are intended to replace stubs and spies
    + However, I didn't see the replacement for custom promise libraries
      (`usingPromise` in stub API)

# Assertions

- Can be replaced by other assertion libraries (e.g., shouldjs)

# Matchers

- Can be passed as arguments to `spy.calledOn`, `spy.calledWith`,
  `spy.returned`
