# Overview

- https://martinfowler.com/articles/injection.html
- https://en.wikipedia.org/wiki/Dependency_injection
- Dependency injection is a technique in which an object receives other
  objects that it depends on, called dependencies.
    + Typically, the receiving object is called a `client` and the
      passed-in (injected) object is called a `service`.
    + The code that passes the service to the client is called the
      `injector`
- The intent behind dependency injection is to achieve separation of
  concerns of construction and use of objects.
    + This can increase readability and code reuse.
- Dependency injection is one form of the broader technique of inversion
  of control.
    + A client who wants to call a service should not have to know how
      to construct it. Instead, the client delegates to external code
      (the injector).
    + This means that the client does not need to know about the
      injector, how to construct the services, or even which services it
      is actually using.
    + The client only needs to know the `interfaces` of the services.
- Types of dependency injection:
    + Constructor injection: the dependencies are provided through a
      client's class constructor
    + Setter injections: the client exposes a setter method that the
      injector uses to inject the dependency
    + Interface injection: the dependency's interface provides an
      injector method that will inject the dependency into any client
      passed to it.
