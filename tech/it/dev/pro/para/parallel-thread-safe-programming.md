# Overview

# Design Patterns

## Singleton

### Lazy Initialization

- https://w.amazon.com/bin/view/Qingzh/DesignPattern/#HLazyInitialization

#### Bill Pugh Singleton (static holder singleton)

A Bill Pugh Singleton is based on the “initialization on demand holder”
idiom. This idiom uses inner classes and enables a safe, highly
concurrent lazy initialization of static fields with good performance.

The JVM defers initializing the LazyHolder class until it's actually
used by static getInstance method. Since the class initialization phase
(of LazyHolder)  is guaranteed by the JLS (Java Language Specification)
to be sequential, i.e., non-concurrent, no further synchronization is
required in the static getInstance method during loading and
initialization.


```java
// Usage: MySingleton singleton = MySingleton.getInstance();
public class MySingleton {
    private MySingleton() { ... }

    public static MySingleton getInstance() {
        return LazyHolder.INSTANCE;
    }

    private static class LazyHolder {
        private static final MySingleton INSTANCE = new MySingleton();
    }
}
```

#### Enum Singleton

> This approach is functionally equivalent to the public field approach,
> except that it is more concise, provides the serialization machinery
> for free, and provides an ironclad guarantee against multiple
> instantiation, even in the face of sophisticated serialization or
> reflection attacks. While this approach has yet to be widely adopted,
> a single-element enum type is the best way to implement a singleton.

```java
// Usage: MySingleton singleton = MySingleton.INSTANCE;
public enum MySingleton {
    INSTANCE;

    private MySingleton() { ... }
}

////

// The functionally equivalent to the public field approach: ENUM singleton is lazily initialized.
// Usage: MySingleton singleton = MySingleton.INSTANCE;
public final class MySingleton {
    public static final MySingleton INSTANCE = new MySingleton();

    private MySingleton() { ... }
}
```

#### Double checked locking

```java
// Usage: MySingleton singleton = MySingleton.getInstance();
public class MySingleton {
    private static volatile MySingleton INSTANCE;

    private MySingleton() { ... }

    public static MySingleton getInstance() {
        if (INSTANCE == null) {
            synchronized(MySingleton.class) {
                if (INSTANCE == null) {
                    INSTANCE = new MySingleton();
                }
            }
        }

        return INSTANCE;
    }
}
```
