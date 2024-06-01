# Overview

- Git
    + https://github.com/google/guava
    + Wiki: https://github.com/google/guava/wiki
- API
    + https://guava.dev/releases/snapshot-jre/api/docs/
- https://www.baeldung.com/guava-preconditions

# com.google.common.collect

- https://guava.dev/releases/snapshot-jre/api/docs/com/google/common/collect/package-summary.html
- This package contains generic collection interfaces and
  implementations, and other utilities for working with collections.

# com.google.common.base

- https://guava.dev/releases/snapshot-jre/api/docs/com/google/common/base/package-summary.html

# com.google.common.io

- https://guava.dev/releases/snapshot-jre/api/docs/com/google/common/io/package-summary.html

# com.google.common.util.concurrent

- https://guava.dev/releases/snapshot-jre/api/docs/com/google/common/util/concurrent/package-summary.html

## RateLimiter

- https://github.com/google/guava/blob/master/guava/src/com/google/common/util/concurrent/RateLimiter.java
- https://www.baeldung.com/guava-rate-limiter

# Tips and Tricks

## Check a string is not null, not empty, and not blank

```java
!Strings.nullToEmpty(stringVar).trim().isEmpty()
```
