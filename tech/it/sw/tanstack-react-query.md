# Overview

- https://tanstack.com/query/v4/
- Fetching, caching, synchronizing and updating server state (external
  data) in React applications.
- Tasks for server state
    + Caching
    + Deduping multiple requests for the same data into a single request
    + Updating "out of date" data in the background
    + Knowing when data is "out of date"
    + Reflecting updates to data as quickly as possible
    + Performance optimizations like pagaination and lazy loading data
    + Managing memory and garbage collection of server state
    + Memoizing query result with structural sharing

# Concepts

- Query
- InfiniteQuery
    + Pagination and lazy loading
- QueryClient
    + A client to access the cache
- QueryClientProvider
    + A provider to provide QueryClient to child components
- QueryCache
    + Storage mechanism for caching
- QueryErrorResetBoundary
    + When using suspense or useErrorBoundaries in your queries, you
      need a way to let queries know that you want to try again when
      re-rendering after some error occurred. With the
      QueryErrorResetBoundary component you can reset any query errors
      within the boundaries of the component.

# APIs

- C
