# Overview

- Jest testing framework for React

# API

- https://jestjs.io/docs/26.x/api

## Globals

- Any functions in globals, we don't need to import or require to use it
- Can add things to this in `setupTest.js` in the `setupFilesAfterEnv`
  setting

## Expect

- Jest matchers
- https://jestjs.io/docs/26.x/expect

## The Jest Object

- `jest` object help create mocks and let you control Jest's overall
  behavior
    + Mocks
        * Mock modules
        * Mock functions
        * Mock timers

## Mocks

### Mock Functions

- https://jestjs.io/docs/26.x/mock-function-api
- Known as "Spies"
    + spy on the behavior of a function that is called indirectly by
      some other code
    + determine the arguments are passed, number of calls to the mock
      function, etc.
- TypeScript
    + `jest.Mocked<Source>` (Source: typeof ...)
    + https://jestjs.io/docs/mock-function-api/#jestmockedsource

### Mock Modules

- https://jestjs.io/docs/26.x/jest-object#mock-modules


### Tips and Tricks

- Change mock implementation per test
    + https://stackoverflow.com/questions/48790927/how-to-change-mock-implementation-on-a-per-single-test-basis

## Configuring Jest

- https://jestjs.io/docs/26.x/configuration

## Environment variables

- https://jestjs.io/docs/26.x/environment-variables
- Set `NODE_ENV` to test if it's not set to something else.

# Documentation

## Using Matchers

- https://jestjs.io/docs/using-matchers

## Setup and Teardown

- https://jestjs.io/docs/setup-teardown

## Mocking

- https://jestjs.io/docs/mock-functions
- Manual mocks:
    + https://jestjs.io/docs/manual-mocks
- Bypassing module mocks
    + https://jestjs.io/docs/bypassing-module-mocks

## Jest Platform

- https://jestjs.io/docs/jest-platform

## Snapshot Testing (React components, etc.)

- https://jestjs.io/docs/snapshot-testing
- To update a snapshot
    + `jest --updateSnapshot`
    + If you'd like to limit which snapshot test cases get re-generated,
      you can pass an additional `--testNamePattern` flag to re-record
      snapshots only for those tests that match the pattern.
        * `jest --updateSnapshot --testNamePattern abc.test.js`
- "Obsolete" refers to snapshots or snapshot files, for which no
  .toMatchSnapshot() exists any more.
    + https://stackoverflow.com/a/58868037/1683888
- Image snapshot testing
    + https://dev.to/saniadsouza/test-for-visual-regression-with-jest-image-snapshot-4i54
    + https://stackoverflow.com/questions/54989595/how-do-i-image-snapshot-test-a-react-component-using-html5-canvas

## Timer Mocks

- https://jestjs.io/docs/timer-mocks


## Using with Webpack

- https://jestjs.io/docs/webpack

## Architecture

- https://jestjs.io/docs/architecture


# Framework Guides

## React

- https://jestjs.io/docs/tutorial-react

# Plugins

- jest-dom
    + Add more DOM matchers to Jest
    + eslint-plugin-jest-dom
- jest-extended
    + Add more general matchers to Jest
    + eslint-plugin-jest-extended
- babel-jest
    + Running TypeScript tests with Jest
- eslint-plugin-jest

# Tips and Tricks

## spyOn object and function exported by index files

- https://stackoverflow.com/a/72885576/1683888
- use `jest.mock` with `__esModule: true`, then `spyOn` normally

## Generate coverage for single test file

- https://stackoverflow.com/questions/66492412/how-to-run-jest-tests-with-coverage-for-one-file

- `npm run test -- <test-file> --collectCoverageFrom=<source-file>`
- `npm run test -- src/api/ApiHelper/__tests__/ApiHelper.test.ts --collectCoverageFrom=src/api/ApiHelper/ApiHelper.ts`

## Run a single test file

- `npm run test -- <file-path>`

## Test if a void async function was successful

- https://stackoverflow.com/a/60084003/1683888
    + `toBeUndefined()`

# Troubleshooting

## GENERAL STEPS TO TAKE WHEN SOME TESTS ARE FAILING

- https://jestjs.io/docs/troubleshooting
- Only run one test in a test file
    + Change `test/it` to `test.only/it.only`
- Each test file should be separated, so tests in different test files
  do not interfere each other.
    + Only tests in the same test files may interfere each other, so we
      should use `beforeEach/afterEach` to set up or clean up tests.
    + If multiple tests across test files are failing, then something is
      wrong with Jest configuration itself. Check mocking configuration
      if the failed tests are caused by mocks.

## toThrow does not work on custom Error or throw object

- https://stackoverflow.com/questions/48707111/asserting-against-thrown-error-objects-in-jest
    + Use `toEqual` object instead
- https://github.com/facebook/jest/issues/8279
    + Problem with extending Error class
