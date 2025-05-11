# Overview

- An agnostic user interface library
    + `agnostic`: is used in many different environment such as browser
      (react-dom), computer OS, mobile OS, etc.
    + `user interface`: is used to create user interface components
    + `library`: lightweight compared to frameworks such as Angular
        * is used with other libraries to do the work

- Component architecture
    + The application is broken down to components.
    + Compose the application from components.
    + Each component is a JavaScript function that returns markup
      (HTML or other markup).
    + React component names must always start with a capital letter,
      while HTML tags must be lowercase.
- JSX (allows JavaScript and HTML to be mixed)
    + JSX is stricter than HTML. You have to close tags like `<br
      />`. Your component also can’t return multiple JSX tags. You have
      to wrap them into a shared parent, like a `<div>...</div>` or an
      empty `<>...</>` wrapper.
- Data flows down `one way` through a React app (component tree)
    + From the top to bottom (leaf) of the component tree
    + Component lifecycle
        * Mount - update - unmount
    + Avoid mutation, use react tools (hooks and APIs) to do the update
- State exists at a `component level` and is passed down.
    + Component state is immutable. Once set, the state of a component
      can’t be changed. State changes don’t change existing view
      state. Instead, they trigger a new view render with a new state.
- Conditional rendering
    + https://react.dev/learn#conditional-rendering
    + `<condition> ? <componentIf> : <componentElse>` for if else, and `
      <condition> && <component>` if else branch is not needed.
- Using hooks

# Best Practices

- Colocation code and assets
    + https://kentcdodds.com/blog/colocation

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

## Thinking In React

- Step 1: Start from the mockup and break the UI into a component
  hierarchy.
- Step 2: Build a static version in React
- Step 3: Find the minimal but complete representation of UI state.
- Step 4: Identify where (which component) your state should live
- Step 5: Add inverse data flow (passing set state functions down)

## Rules of React

- https://react.dev/reference/rules
- Components and Hooks must be pure.
- React calls Components and Hooks
- Rules of Hooks

## JSX (JavaScript Syntax Extension)

- An extension to JavaScript which allows you to write HTML markup
  inside JS code.
- Allow binding events to HTML elements

# Installation and Set up

## Frameworks

- Next.js
    + Including new full-stack architecture: Server Component and
      Suspense component.
    + https://github.com/reactjs/rfcs/blob/main/text/0188-server-components.md
        * Other frameworks (Angular and Vue.js) have partial hydration
          which might be similar to this feature? (NEED TO CONFIRM)
    + Server Component does not override the client-side
      state/components unlike Server-side rendering (SSR).
        * SSR render the pages on the server into HTML and send it back
          to client.
        * Server Component does not render into HTML but a special
          format to allow for preserving client-side states and
          components.
    + Server Components has zero effect on the bundle size, so your web
      app will be loaded faster.
    + Server Components let you access the backend resources directly
        * You can read the file system directly.
        * You can read from the database that is running on the server.
        * You can hit the API layer locally through: `localhost:<port>`
    + React IO Libraries:  react-fs,  react-db, react-fetch,  etc..
    + Server Components let you only load the code that is necessary.
        * Never need to download Server Components.
        * Conditional downloading Client Components.
    + Server Components let you decide the tradeoff for every concrete
      use case.
        * Client/Server/Shared Components
    + Server Components provide modern UX with a server-driven mental
      model.
        * The React web app as a single tree with both Server and Client
          Component Nodes.
        * For the Server Components, we can think of as server passes
          data to the Client Components as props.
- Remix
- Gatsby
- Expo (for native apps)

## React Compiler

- https://react.dev/learn/react-compiler
- A new compiler to optimize React apps.
    + Still in beta as of 2024-12-15
    + Should consider using this when it's stable to improve
      performance!

# Migration

## React 18 to 19

- https://react.dev/blog/2024/04/25/react-19-upgrade-guide
- Upgarde to `18.3.0` first to see warnings for incompatible issues for
  current code with React 19.
    + Fix the warnings before upgrading to React 19.

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
- Manipulating the DOM with a ref
    + https://react.dev/reference/react/useRef#manipulating-the-dom-with-a-ref
    + https://react.dev/learn/manipulating-the-dom-with-refs#best-practices-for-dom-manipulation-with-refs
    + Focusing a text input
    + Scrolling an image into view
    + Playing and pausing a video
    + Exposing a ref to your own component
- Create event listeners using ref
    + https://www.preciousorigho.com/articles/a-better-way-to-create-event-listeners-in-react

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
    + https://blog.testdouble.com/posts/2021-03-19-react-context-for-dependency-injection-not-state/
    + https://dev.to/dansolhan/simple-dependency-injection-functionality-for-react-518j
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

## Principles

- https://testing-library.com/docs/guiding-principles/
    + Tests should resemble the way your software is used.
    + Use DOM (role, text, etc.) rather than test IDs.
    + List of roles for HTMLELement
        * https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Guides/Techniques#roles
    + How to determine a role of an element on browser
        * Go to dev tool of that browser
        * Inspect the element and find the Accessibility tab/section
          (this will be different between Chrome and Firefox)
            - Chrome: Element tab, inside when select an element, it
              should display a nested Accessibility tab in the right
              side.
            - Firefox: Accessibility tab is separated
- Queries and priority of using them
    + https://testing-library.com/docs/queries/about/
    + https://testing-library.com/docs/queries/about/#priority
    + https://kentcdodds.com/blog/common-mistakes-with-react-testing-library#using-the-wrong-query
- Problems with using test-ids
    + https://stackoverflow.com/a/79218497

## Libraries

- `Jest`: general testing framework, can be used to test utilities,
  asynchronous functions, etc.
    + https://jestjs.io/docs/26.x/getting-started
- `React Testing Library`: build on top of DOM testing library, can be
  used to test components
    + https://testing-library.com/docs/react-testing-library/intro
    + It also has the capability to test Hooks as well.
- `jest-dom` matchers: add more custom matchers to jest
    + https://github.com/testing-library/jest-dom
- `jest-extended`: More matchers for jest
    + https://github.com/jest-community/jest-extended
- (LEGACY) React Hooks Testing Library: can be used to test React Hooks
    + SHOULD USE React Testing Library above instead.
    + https://react-hooks-testing-library.com/
    + React-use library of useful hooks: https://github.com/streamich/react-use

## Testing custom hooks

- Two approaches
    + Create a test component and tests for the test component
    + Using a library
- https://kentcdodds.com/blog/how-to-test-custom-react-hooks
- https://www.toptal.com/react/testing-react-hooks-tutorial
- https://react-hooks-testing-library.com/reference/api
- More resources
    + https://github.com/testing-library/react-testing-library/pull/991

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

## Troubleshooting / Debugging tests

### Log / Show the whole DOM when tests failed

- https://testing-library.com/docs/dom-testing-library/api-debugging
- Increase the `DEBUG_PRINT_LIMIT` environment variable (default is
  7000)
    + `DEBUG_PRINT_LIMIT=100000 npm test ...`

### test was not wrapped in act(...)

- Resources
    + https://www.reddit.com/r/reactjs/comments/tswa0p/test_was_not_wrapped_in_act_error_clear/
    + https://react.dev/reference/react/act
    + https://testing-library.com/docs/dom-testing-library/api-async/#waitfor
- Any thing that causes the state to update should go inside the `act`.
    + Using asynchronous act with await instead of synchronous version.
    + Don't wrap React testing library utilities such as `render` etc in
      `act` since they already wrapped in act.
- Also it's better to not use `act` but using `waitFor` or
  `waitForElementToBeRemoved` in react testing library to wait for React
  to complete all state updates before asserting. (`act` is built in for
  these utilities in React testing library)
    + https://testing-library.com/docs/dom-testing-library/api-async/#waitfor
    + https://egghead.io/lessons/jest-fix-the-not-wrapped-in-act-warning

```javascript
it('should ...', async () => {
    const var = await act(sync () => ...);
    ...
});
```

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

## Server State (fetching data from server)

- https://www.robinwieruch.de/react-hooks-fetch-data/

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

# React DOM

- https://react.dev/reference/react-dom
- The `react-dom` package contains methods that are only supported for
  the web applications (which run in the browser DOM
  environment). They are not supported for React Natives.

## Hooks

## Components

## APIs

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

## Build

- A JavaScript build toolchain typically consists of:
    + A `package manager`, such as `yarn` or `npm`. Install and update
      third party packages.
    + A `bundler`, such as `webpack` or `Parcel`. It lets you write
      modular code and bundle it together into small packages to
      optimize load time.
    + A `compiler` such as `Babel`. It lets you write modern JavaScript
      code that still works in older browsers.

## Development

### React Dev Tools

#### Settings

- General
    + Highlight updates when components render.
- Debugging
    + Hide logs during additional invocations in Strict Mode.
- Profiler
    + Record why each component rendered while profiling.
    + Hide commits below x ms

#### Components

- Can select components from the hierarchical list or vice versa (select
  the DOM element to show the component in the list)
- Can search the component by name
- Can view and edit components' props and hooks (states, etc.)
- Can view the rendered hierarchical (parent components)
- Can test React Suspense effect when components are loading.
- Can show associated DOM element of a component.
- Can log to console all the component details.
- Can show associated source code for the component.

#### Profiling

- In the settings for the tools, select the `Profiler` tab and select
  option: `Record why each component rendered while profiling.` to know
  the reason of a rerendering.

##### Basic

- Start profiling and then performing the actions on the web app.
- Stop the profiling.
- To profile on page load, click circular arrow `reload and start
  profiling` button.
- Look at the ranked view to find the slowest rendering to debug the
  issue.
    + There are component names and other information.
- Look at the flamegraph view to see the hierarchical structure of
  components.
    + After profiling is stopped, we can check all the renders at `xx /
      yy` at the top.
    + Components with colors are being rendered and taking time. Grey
      out components are not rendered.
    + Two numbers `x ms of y ms`: `x` is the time for that component to
      render and `y` is the total time to render that component and all
      of its child components.

##### Advanced

- Throttle network speed and performance (CPU, concurrency, etc.) to
  find slow down components.

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

## Grid/Table component

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
    + https://blog.testdouble.com/posts/2021-03-19-react-context-for-dependency-injection-not-state/
    + https://dev.to/dansolhan/simple-dependency-injection-functionality-for-react-518j

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

# TypeScript

- https://react.dev/learn/typescript
- `tsconfig.json`
    + `"lib"` should contains `dom`
    + `"jsx": "preserve"`
- Provide types for components' props.
    + Either through inline types or `interface` or `type` keywords.
- Example Hooks
    + https://react.dev/learn/typescript#example-hooks
    + `useState`: the type can be inferred from the initial state value
      or through explicit type  passing `useState<T>(value)`
    + `useReducer`: takes in a reducer function and an initial state
- Useful Types
    + DOM Events:
        * https://react.dev/learn/typescript#typing-dom-events
        * https://github.com/DefinitelyTyped/DefinitelyTyped/blob/b580df54c0819ec9df62b0835a315dd48b8594a9/types/react/index.d.ts#L1247C1-L1373
        * https://developer.mozilla.org/en-US/docs/Web/Events
    + React `children` with TypeScript
        * https://react.dev/learn/typescript#typing-children
        * `ReactNode`, `ReactChild`, `JSX.Element`
        * https://www.carlrippon.com/react-children-with-typescript/
    + Style Props
        * https://react.dev/learn/typescript#typing-style-props
        * `React.CSSProperties`
- React Context
    + https://kentcdodds.com/blog/how-to-use-react-context-effectively
    + https://felixgerschau.com/react-typescript-context/
    + https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/context/
