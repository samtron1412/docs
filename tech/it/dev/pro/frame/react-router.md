# Overview

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
    + Others...

# React Router v7



# React Router v6

- Libraries
    + `react-router`: the core library
    + `react-router-dom`: a variant of the core library meant to be used
      for web applications
        * If you only need a library for a website, this is the library
          that you need.
    + `react-router-native`: a variant of the core library used with
      react native in the development of Android and iOS applications.

## Concepts

- https://reactrouter.com/en/main/getting-started/concepts

### URL

In React Router DOM (and general web applications), a URL is structured
into several parts that help define the location of a resource, the
parameters to use, and additional metadata. Here's a breakdown of a
typical URL and its components:

---

#### **General URL Structure**

```
protocol://hostname:port/pathname?query_string#fragment
```

---

#### **Parts of the URL**

1. **`protocol`**
   - Specifies the communication protocol (e.g., `http`, `https`, `ftp`).
   - Example: `https://`.

2. **`hostname`**
   - The domain or IP address of the server hosting the application.
   - Example: `www.example.com`.

3. **`port`** *(Optional)*
   - The server port for communication. If omitted, defaults are used (e.g., 80 for `http`, 443 for `https`).
   - Example: `:3000`.

4. **`pathname`**
   - Represents the hierarchical structure of the resource on the server. It is the part React Router DOM typically uses to match routes.
   - Example: `/users/profile`.

5. **`query_string`** *(Optional)*
   - A set of key-value pairs used to pass additional parameters.
   - Starts with `?` and is separated by `&` between key-value pairs.
   - Example: `?id=123&status=active`.

6. **`fragment`** *(Optional)*
   - An identifier pointing to a specific part of the resource.
   - Starts with `#`.
   - Example: `#section1`.

---

#### **Example URL in React Router DOM**

For the URL:
```
https://www.example.com:3000/users/profile?id=123&status=active#details
```

The parts are:
- **Protocol**: `https`
- **Hostname**: `www.example.com`
- **Port**: `3000`
- **Pathname**: `/users/profile`
- **Query String**: `?id=123&status=active`
  - Parameters:
    - `id=123`
    - `status=active`
- **Fragment**: `#details`

---

#### **React Router DOM and URL Parts**

1. **`pathname`**
   - React Router uses the `pathname` to match and render routes.
   - Example:
     ```jsx
     <Route path="/users/profile" element={<ProfilePage />} />
     ```

2. **`query_string`**
   - Query parameters are not directly handled by React Router DOM but can be accessed using `useLocation` or utility libraries like `URLSearchParams`.
   - Example:
     ```jsx
     import { useLocation } from 'react-router-dom';

     const Component = () => {
       const location = useLocation();
       const queryParams = new URLSearchParams(location.search);

       const id = queryParams.get('id');
       const status = queryParams.get('status');

       console.log(id, status); // Outputs: 123 active
       return <div>ID: {id}, Status: {status}</div>;
     };
     ```

3. **`fragment`**
   - Fragments (`#fragment`) are typically used for navigating within a single page and can be accessed using the `hash` property of `useLocation`.
   - Example:
     ```jsx
     const Component = () => {
       const location = useLocation();
       console.log(location.hash); // Outputs: #details
       return <div>Hash: {location.hash}</div>;
     };
     ```

---

#### **React Router and Dynamic Segments**
React Router allows dynamic segments in the `pathname` to build more flexible routes.

Example:
```jsx
<Route path="/users/:userId/profile" element={<ProfilePage />} />
```

For a URL like `/users/123/profile`, the `userId` parameter can be accessed using the `useParams` hook:

```jsx
import { useParams } from 'react-router-dom';

const ProfilePage = () => {
  const { userId } = useParams();
  console.log(userId); // Outputs: 123
  return <div>User ID: {userId}</div>;
};
```

## Tutorial

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

## Code splitting routers with React Lazy and Suspense

- https://linguinecode.com/post/code-splitting-react-router-with-react-lazy-and-react-suspense

# Tips and tricks

## Connect redux and router

+ https://github.com/supasate/connected-react-router
+ https://github.com/acdlite/redux-router
+ https://github.com/reactjs/react-router-redux

