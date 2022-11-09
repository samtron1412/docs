# Overview

- An agnostic user interface library
    + `agnostic`: is used in many different environment such as browser
      (react-dom), server, ...
    + `user interface`: is used to create user interface components
    + `library`: lightweight compared to frameworks such as Angular
        * is used with other libraries to do the work
- Component architecture
    + The application is broken down to components.
    + Compose the application from components.
- Data flows down `one way` through a React app (component tree)
    + From the top to bottom (leaf) of the component tree
    + Component lifecycle
        * Mount - update - unmount
    + Avoid mutation, use react tools to do the update
- State exists at a `component level` and is passed down.
    + Component state is immutable. Once set, the state of a component
      can’t be changed. State changes don’t change existing view
      state. Instead, they trigger a new view render with a new state.

# Main Concepts

- A `function App()` represents an UI component `<App />`
- Virtual DOM (Document Object Model)
    + DOM is a web API that represents a document using a logical tree:
      each node contains objects
    + VDOM is a programming concept where a virtual/ideal representation
      of a UI is kept in memory and synced with the real DOM by a
      library such as ReactDOM (this process is called
      `reconcilication`).
    + This approach enables the `declarative API` of React: you tell
      React what state you want the UI to be in, and it makes sure the
      DOM matches the state.
        * This abstracts out the attribute manipulation, event handling,
          and manual DOM updating

## JSX

## Rendering Elements

## Components and Props

## Class Components: State and Lifecycle (Replaced by Hooks)

## Handling Events

## Conditional Rendering

## Lists and Keys

## Forms

## Lifting State Up

## Composition vs Inheritance

## Thinking In React


# Hooks

- https://reactjs.org/docs/hooks-intro.html
- https://nazrhan-mohcine.medium.com/react-hooks-why-what-and-pros-vs-cons-6d3fe18b8a0a
- Pros
    + https://kentcdodds.com/chats/01/03/realigning-your-model-of-react-after-hooks-with-dan-abramov
- Cons
    + https://hackernoon.com/update-react-request-for-comment-to-the-ugly-side-of-react-hooks-8l3b3eha

## Introducing Hooks

### Motivation

- It's hard to reuse stateful logic between components
    + Stateful logic: a service in Angular world
    + WRAPPER HELL: components surrounded by layers of providers,
      consumers, higher-order components, render props, and other
      abstractions.
    + With Hooks, you can extract stateful logic from a component, so it
      can be tested independently and reused.
    + Hooks allow you to reuse stateful logic without changing your
      component hierarchy. This makes it easy to share Hooks among many
      components or with the community.
- Complex components become hard to understand
    + Each lifecycle method often contains a mix of unrelated logic
    + Mutually related code that changes together gets split apart, but
      completely unrelated code ends up combined in a single method
    + In many cases it’s not possible to break these components into
      smaller ones because the stateful logic is all over the
      place. It’s also difficult to test them. This is one of the
      reasons many people prefer to combine React with a separate state
      management library. However, that often introduces too much
      abstraction, requires you to jump between different files, and
      makes reusing components more difficult.
    + Hooks let you split one component into smaller functions based on
      what pieces are related (such as setting up a subscription or
      fetching data), rather than forcing a split based on lifecycle
      methods.
- Problems with classes
    + Classes don’t minify very well, and they make hot reloading flaky
      and unreliable. We want to present an API that makes it more
      likely for code to stay on the optimizable path.

### Adoption plan

- DO NOT REWRITE (COMPLEX) EXISTING COMPONENTS
- JUST USE HOOKS FOR NEW COMPONENTS

## Hooks at a Glance

Hooks are functions that let you “hook into” React state and lifecycle
features from function components.

## Rules of Hooks

- Only call Hooks at the top level. Don’t call Hooks inside loops,
  conditions, or nested functions.
    + Instead, always use Hooks at the top level of your React
      function, before any early returns.
    + By following this rule, you ensure that Hooks are called in the
      same order each time a component renders. That’s what allows React
      to correctly preserve the state of Hooks between multiple useState
      and useEffect calls.
    + Put loops, conditions, or nested functions inside hooks.
- Only call Hooks from React function components. Don’t call Hooks from
  regular JavaScript functions. (There is just one other valid place to
  call Hooks — your own custom Hooks. We’ll learn about them in a
  moment.)
    + By following this rule, you ensure that all stateful logic in a
      component is clearly visible from its source code.

## Using the State Hook

- `useState(param)` hook
    + parameter: the initial state value
    + Return a pair: the current state value, and a function to update
      the state.

```typescript
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

- React assumes that if you call useState many times, you do it in the
  same order during every render.
- Reading state
    + Use the `stateVariable` directly
- Updating state
    + Use the `setX` function returned from `useState`


## Using the Effect Hook

- Side effects operations
    + data fetching, subscriptions, manually changing the DOM
    + these operations can affect other components and can't be done
      during rendering
    + There are two common kinds of side effects in React: those that
      don't require clean up, and those that do.
- `useEffect(...)` hook
    + it serves the same purpose as `componentDidMount`,
      `componentDidUpdate`, `componentWillUnmount`
    + When you call useEffect, you’re telling React to run your “effect”
      function after flushing changes to the DOM.
    + effects are declared inside the component so they have access to
      its props and state.
    + By default, React runs the effects after every render - including
      the first render.
    + Effects may also optionally specify how to “clean up” after them
      by returning a function.
    + Can use multiple `useEffect`

### Effects without cleanup

- run some additional code after React has updated the DOM.
    + Network requests, manual DOM mutations, and logging are common
      examples
    + we can run them and immediately forget about them

### Effects with cleanup

- For example, we might want to set up a subscription to some external
  data source. In that case, it is important to clean up so that we
  don’t introduce a memory leak
- `useEffect` returns a function to clean up the effect when the
  component unmounts.
    + React also cleans up effects from the previous render before
      running the effects next time.
    + You can tell React to skip applying an effect if certain values
      haven’t changed between re-renders. To do so, pass an array as an
      optional second argument to useEffect:
        * it must include all values that are used inside the callback
          and participate in the React data flow. That includes props,
          state, and anything derived from them.

```typescript
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes

useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // Only re-subscribe if props.friend.id changes
```


## Custom Hooks

- Custom Hooks are more of a convention than a feature. If a function’s
  name starts with ”use” and it calls other Hooks, we say it is a custom
  Hook. The useSomething naming convention is how our linter plugin is
  able to find bugs in the code using Hooks.

```typescript
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```


### Testing custom hooks

- Two approaches
    + Create a test component and tests for the test component
    + Using a library
- https://kentcdodds.com/blog/how-to-test-custom-react-hooks
- https://www.toptal.com/react/testing-react-hooks-tutorial
- https://react-hooks-testing-library.com/reference/api
- More resources
    + https://github.com/testing-library/react-testing-library/pull/991

## Hooks APIs

- https://reactjs.org/docs/hooks-reference.html
- `useContext`: lets you subscribe to React context without introducing
  nesting
- `useReducer`: lets yo manage local state of complex components with a
  reducer
- Others:
    + https://reactjs.org/docs/hooks-reference.html

```typescript
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
  // ...
}

function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);
  // ...
```

### useCallback and useMemo and React.memo()

- Avoid using `useCallback` for every function
- Do use `useCallback` for function that is passed as a prop to highly
  optimized child components. (React.memo(), React.useEffect(..,
  [callback]), etc.)
- https://kentcdodds.com/blog/usememo-and-usecallback

### useRef

- Optimize components with useCallback, useMemo and then useRef
    + https://stackoverflow.com/questions/64134566/should-we-use-usecallback-in-every-function-handler-in-react-functional-componen

# Advanced Guides

## Context

- https://reactjs.org/docs/context.html
- Best practices
    + https://kentcdodds.com/blog/how-to-use-react-context-effectively
    + https://kentcdodds.com/blog/how-to-optimize-your-context-value
- Context provides a way to pass data through the component tree without
  having to pass props down manually at every level.
- Context is designed to share data that can be considered “global” for
  a tree of React components, such as the current authenticated user,
  theme, or preferred language.
    + Can use Context to implement dependency injection for services
- Notes
    + All child components inside of a Provider are re-rendered if the
      value provided to it as a prop changes.
    + Because of the above issue, we should colocate Provider with child
      components, and make child components to be
      memoized. (`React.memo`)

## Error Boundaries

- https://reactjs.org/docs/error-boundaries.html

## Code-Splitting

- https://reactjs.org/docs/code-splitting.html

## Fragments

- https://reactjs.org/docs/fragments.html
    + Let you group a list of children without adding extra nodes
      (div/span) to the DOM.
    + This can be used for things to be rendered in a table, etc.

## Async React Components

- Handling async React component effects after unmount
    + https://www.benmvp.com/blog/handling-async-react-component-effects-after-unmount/
    + react-use library

# Testing

- Jest: general testing framework, can be used to test utilities,
  asynchronous functions, etc.
    + https://jestjs.io/docs/26.x/getting-started
- React Testing Library: build on top of DOM testing library, can be
  used to test components
    + https://testing-library.com/docs/react-testing-library/intro
- `jest-dom` matchers: add more custom matchers to jest
    + https://github.com/testing-library/jest-dom
- More matchers for jest
    + https://github.com/jest-community/jest-extended
- React Hooks Testing Library: can be used to test React Hooks
    + https://react-hooks-testing-library.com/
    + React-use library of useful hooks: https://github.com/streamich/react-use

## Snapshot testing

- https://kentcdodds.com/blog/effective-snapshot-testing
- https://kentcdodds.com/blog/why-i-never-use-shallow-rendering
- Order of priority
    + Using explicit assertions if as much as possible
    + Using only small, focused snapshots (less than 50 lines)
    + Using custom serializers to have cleaners snapshots
    + Using snapshot-diff to compare two states of the same component

## Testing environments

- https://reactjs.org/docs/testing-environments.html
- Test runners
    + Jest, Mocha
- Mocking a rendering surface
    + jsdom
    + mocha
    + cypress: end-to-end
- Mocking functions
    + jest, sinon
- Mocking modules
    + jest
- Mocking timers
    + jest, sinon

## Testing recipes

- https://reactjs.org/docs/testing-recipes.html
- Setup, act, assert

### Set up a server for fetch and axios

- https://testing-library.com/docs/react-testing-library/example-intro#full-example

# State Management

- react-query and useReducer + Context
    + if the app does not use redux
    + start fresh from beginning
    + speed development
- redux and RTK, RTK Query
    + app uses redux
    + complex application
    + large team

## Types of states

- https://kentcdodds.com/blog/application-state-management-with-react
    + https://kentcdodds.com/blog/state-colocation-will-make-your-react-app-faster
    + https://kentcdodds.com/blog/colocation
    + https://kentcdodds.com/blog/fix-the-slow-render-before-you-fix-the-re-render
- External data / Server cache
    + State that's actually stored on the server and we store in the
      client for quick-access (like user data)
    + REST APIs: *React query*, RTK Query, SWR
        * https://tanstack.com/query/v4/
        * Custom API fetch library is easier to use with `react-query`
          than RTK Query: https://www.reddit.com/r/reactjs/comments/q6lit4/comment/i0s3f27/?utm_source=share&utm_medium=web2x&context=3
        * Some reasons to use RTK Query instead of react-query: https://www.reddit.com/r/reactjs/comments/mggpr7/rtk_query_vs_react_query_which_to_use_in_what/
    + GraphQL: Apollo Client, urql
- App/UI State
    + State that's only useful in the UI for controlling the interactive
      parts of our app (like moal isOpen state)
    + Priority
        * Local state
        * Lift state + composition
        * Global state with useState/useReducer + Contexts
            - memo(Component)
            - Colocate providers and components for code splitting
        * Libraries: jotai, recoil, zustand, redux, mobx, etc.
            - https://github.com/pmndrs/jotai

## Server State

### react-query

- https://tanstack.com/query/v4/

## App/UI State

### useState/useReducer + Context

- Context vs. Redux
    + https://blog.isquaredsoftware.com/2021/01/context-redux-differences/

### Redux / Zustand

- https://blog.isquaredsoftware.com/2021/01/context-redux-differences/

### Recoil / Jotai

- Atomic state management

### Mobx

- https://github.com/mobxjs/mobx

# Router

- List of router libraries
    + React Router
        * https://reactrouter.com/
        * https://github.com/remix-run/react-router
    + TanStack Router
        * https://tanstack.com/router/v4
    + Wouter
        * https://github.com/molefrog/wouter
    + Hooks
        * https://blog.logrocket.com/how-react-hooks-can-replace-react-router/
        * https://github.com/Paratron/hookrouter

- Connect redux and router
    + https://github.com/supasate/connected-react-router
    + https://github.com/acdlite/redux-router
    + https://github.com/reactjs/react-router-redux

## React Router

- Libraries
    + `react-router`: the core library
    + `react-router-dom`: a variant of the core library meant to be used
      for web applications
        * If you only need a library for a website, this is the library
          that you need.
    + `react-router-native`: a variant of the core library used with
      react native in the development of Android and iOS applications.

### Tutorial

- List of Routers
    + BrowserRouter: is used for applications which have a dynamic
      server that knows how to handle any type of URL.
    + HashRouter: is used for static websites with a server that only
      responds to requests for files that it knows about.
    + MemoryRouter: (not needed for now)
- Any router expects to receive only one child.
- History
    + Each router creates a history object that it uses to keep track of
      the current location and re-renders the application whenever this
      location changes.
        * For this reason, the other React components rely on this
          history object being present; which is why they need to be
          rendered inside a router.
        * https://github.com/remix-run/history
    + The BrowserRouter uses the HTML5 history API to keep the user
      interface in sync with the URL in the browser address bar.
        *  https://developer.mozilla.org/en-US/docs/Web/API/History_API
    + The history object contains `location` property whose value is
      also an object.
        * location object = `{pathname, search, hash, state}`
- Routes
    + The `<Route/>` component renders the appropriate UI when the
      current location matches the route's `path` prop.
    + `<Route path=”/items”/>`: matches all paths start with `/items`
    + `<Route exact path=”/items” />` matches only for `/items`
- Restricting Routes and Links with Hooks
    + https://medium.com/craft-academy/how-to-restrict-your-routes-and-links-in-react-js-now-with-hooks-12b395c1a2fe

### Concepts

- https://reactrouter.com/en/main/getting-started/concepts

### Code splitting routers with React Lazy and Suspense

- https://linguinecode.com/post/code-splitting-react-router-with-react-lazy-and-react-suspense

# React Internal

## Design Principles

- https://reactjs.org/docs/design-principles.html
- Composition
    + Components written by different people should work well together.
    + Components describe any composable behavior

## Reconciliation

+ https://reactjs.org/docs/reconciliation.html
+ `render()` function creates a tree of React elements
+ On the next state or props update, `render()` will return a different
  tree of React elements. So React needs an efficient way to update the
  UI to match the most recent tree.
+ The algorithm is `tree edit distance`: https://grfia.dlsi.ua.es/ml/algorithms/references/editsurvey_bille.pdf
+ The state of the art algorithm is `O(n^3)`, so React chooses a
  heuristic approach to achieve `O(n)` complexity.
+ The heuristic algorithm based on two assumptions:
    * Two elements of different types will produce different trees.
    * The developer can hint at which child elements may be stable
      across different renders with a `key` prop.
+ First assumption means the algorithm will not try to match subtrees of
  different component types. If you see yourself alternating between two
  component types  with very similar output, you may want to make it the
  same type.
+ Keys should be stable, predictable, and unique. Unstable keys (like
  those produced by `Math.random()`) will cause many component instances
  and DOM nodes to be unnecessarily recreated

## Basic theoretical concepts

- https://github.com/reactjs/react-basic
- Transformation of representations of data
- Abstraction
- Composition
- State
- Memoization
- Lists
- Continuations
- State Map
- Memoization Map
- Algebraic Effects

## React Fiber Architecture

- https://github.com/acdlite/react-fiber-architecture

# Toolchain

- A JavaScript build toolchain typically consists of:
    + A `package manager`, such as `yarn` or `npm`. Install and update
      third party packages.
    + A `bundler`, such as `webpack` or `Parcel`. It lets you write
      modular code and bundle it together into small packages to
      optimize load time.
    + A `compiler` such as `Babel`. It lets you write modern JavaScript
      code that still works in older browsers.

# JSX (JavaScript Syntax Extension)

- An extension to JavaScript which allows you to declaratively create
  custom UI components.
- Use JS in HTML
- Allow binding events to HTML elements

# React UI Component Libraries

- Ant Design
    + https://ant.design/
    + https://github.com/ant-design/ant-design/
- Material UI
    + https://mui.com/
    + https://github.com/mui/material-ui
- React Bootstrap
    + https://react-bootstrap.github.io/
    + https://github.com/react-bootstrap/react-bootstrap
- Chakra UI
    + https://github.com/chakra-ui/chakra-ui
- Semantic UI
    + https://react.semantic-ui.com/
- Reactstrap
    + https://reactstrap.github.io/

# Grid/Table component

- ag-grid
    + https://www.ag-grid.com/
    + https://github.com/ag-grid/ag-grid
- handsontable
    + https://handsontable.com/
    + https://github.com/handsontable/handsontable

# Tips and Tricks

## Services in React (Similar Angular Services)

- Shared logic (without displaying code)
- Custom hooks to implement shared logic
    + Can use Higher-Order Components (but cumbersome and hard to
      manage)
- Context to implement dependency injection

## Error Handling

- Error Boundaries
    + https://reactjs.org/docs/error-boundaries.html
    + For declarative code such as rendering code of components
- For Hooks, use this library
    + https://www.npmjs.com/package/react-error-boundary
- For non-displaying / rendering code, use try/catch


## Type the Function Component (React.FC)

- DO NOT USE IT JUST WRITE NORMAL FUNCTION WITHOUT FUNCTION TYPE, ONLY
  TYPE INPUT AND OUTPUT.
- https://github.com/facebook/create-react-app/pull/8177
- https://fettblog.eu/typescript-react-why-i-dont-use-react-fc/
- https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/function_components/


# React Native

- https://reactnative.dev/
- It is used to develop applications for Android, Android TV, iOS,
  macOS, tvOS, Web, Windows and UWP by enabling developers to use the
  React framework along with native platform capabilities.

# TypeScript

- React `children` with TypeScript
    + https://www.carlrippon.com/react-children-with-typescript/
    + `ReactNode`, `ReactChild`, `JSX.Element`
- React Context
    + https://kentcdodds.com/blog/how-to-use-react-context-effectively
    + https://felixgerschau.com/react-typescript-context/
    + https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/context/
