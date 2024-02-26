# Overview

- https://martinfowler.com/articles/injection.html
- https://en.wikipedia.org/wiki/Dependency_injection
- Dependency injection is a technique in which an object receives other
  objects that it depends on, called dependencies.
    + Typically, the receiving object is called a `client` and the
      passed-in (injected) object is called a `service`.
    + The code that passes the service to the client is called the
      `injector`
- Dependency injection is one form of the broader technique of inversion
  of control.
    + Where DI inverts `the control over the implementations of
      dependencies` rather than the `inversion of control flow`.
- The intent behind dependency injection is to achieve separation of
  concerns of `construction` and `use of objects` (loosely coupled).
    + This can increase `readability` and `code reuse`.
    + A client who wants to call a service should not have to know how
      to construct it. Instead, the client delegates to external code
      (the injector).
    + This means that the client does not need to know about the
      injector, how to construct the services, or even which services it
      is actually using.
    + The client only needs to know the `interfaces` of the services.
- Roles
    + `Service`: a service is any class which contains useful
      functionality.
    + `Client`: a client is any class which uses services.
    + `Interface`: services' APIs
    + `Injector`: (an assembler, container, provider or factory)
      injects/introduces services to the client.
- Types of dependency injection:
    + `Constructor injection`: the dependencies are provided through a
      client's class constructor
    + `Setter injections`: the client exposes a setter method that the
      injector uses to inject the dependency
    + `Interface injection`: the dependency's interface provides an
      injector method that will inject the dependency into any client
      passed to it.
- Dependency injection vs Service Locator
    + https://martinfowler.com/articles/injection.html#ServiceLocatorVsDependencyInjection
    + Criticism for Service Locator
        * https://blog.ploeh.dk/2010/02/03/ServiceLocatorisanAnti-Pattern/
    + https://stackoverflow.com/questions/1557781/whats-the-difference-between-the-dependency-injection-and-service-locator-patte
    + https://softwareengineering.stackexchange.com/questions/390755/whats-the-difference-between-using-dependency-injection-with-a-container-and-us
    + https://www.baeldung.com/cs/dependency-injection-vs-service-locator

