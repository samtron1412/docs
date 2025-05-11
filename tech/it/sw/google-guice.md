# Overview

- Homepage: https://github.com/google/guice
    + Bob Lee's presentation: Big Modular Java with Guice
        * https://www.youtube.com/watch?v=hBVJbzAagfs
    + Motivation
        * https://github.com/google/guice/wiki/Motivation
- https://github.com/google/guice/wiki/GettingStarted
- https://justin.abrah.ms/misc/an-overview-of-guice-java-dependency-injection.html
- https://www.baeldung.com/guice
- https://www.tutorialspoint.com/guice/guice_linked_binding.htm

## What

- Guice is a dependency injection framework.
- Guice alleviates the need for factories and the use of `new` key word
  in your Java code.
    + Designed to manage dependencies between classes.

## Why

- It helps create a loosely coupled architecture by managing object
  creation and injection.
- It helps create more reusable code, more modular code, more testable
  code, and less code.
- Type safety (compared to Spring DI)
    + You get what you ask for without casting.
- Scopes
    + Singleton, etc.
- Aspect-oriented programming (AOP)

# How

- Guice injects dependencies at runtime.
- Guice is annotation-based rather than using configuration files
  such as Spring DI.

## Getting Started

- https://github.com/google/guice/wiki/GettingStarted

### `@Inject` annotation

- Java class constructors that are annotated with @Inject can be called
  by Guice through a process called constructor injection, during which
  the constructors' arguments will be created and provided by Guice.

```java
class Greeter {
  private final String message;
  private final int count;

  // Greeter declares that it needs a string message and an integer
  // representing the number of time the message to be printed.
  // The @Inject annotation marks this constructor as eligible to be used by
  // Guice.
  @Inject
  Greeter(@Message String message, @Count int count) {
    this.message = message;
    this.count = count;
  }

  void sayHello() {
    for (int i=0; i < count; i++) {
      System.out.println(message);
    }
  }
}
```

### Guice modules

- Applications contain objects that declare dependencies on other
  objects, and those dependencies form graphs.
- Guice modules allow applications to specify how to satisfy those
  dependencies.
- Later, with the mental model that Guice is a map, modules are the
  place that we putting records (Key-Provider pairs) into the Guice map.

```java
/**
 * Guice module that provides bindings for message and count used in
 * {@link Greeter}.
 */
import com.google.inject.Provides;

class DemoModule extends AbstractModule {
  @Provides
  @Count
  static Integer provideCount() {
    return 3;
  }

  @Provides
  @Message
  static String provideMessage() {
    return "hello world";
  }
}
```

### Guice injectors

- To bootstrap your application, you'll need to create a Guice Injector
  with one or more modules in it.
- The injector internally holds the dependency graphs described in your
  application. When you request an instance of a given type, the
  injector figures out what objects to construct, resolves their
  dependencies, and wires everything together.

```java
public final class MyWebServer {
  public void start() {
    ...
  }

  public static void main(String[] args) {
    // Creates an injector that has all the necessary dependencies needed to
    // build a functional server.
    Injector injector = Guice.createInjector(
        new RequestLoggingModule(),
        new RequestHandlerModule(),
        new AuthenticationModule(),
        new DatabaseModule(),
        ...);
    // Bootstrap the application by creating an instance of the server then
    // start the server to handle incoming requests.
    injector.getInstance(MyWebServer.class)
        .start();
  }
}
```

## Mental Model

- https://github.com/google/guice/wiki/MentalModel
- Guice is a map.
    + A map of `Guice key` to a `Provider`.
    + Your application code declares the dependencies it needs, and
      Guice fetches them for you from its map.
- `Guice key`: a key in the map which is used to fetch a particular
  value from the map.
- `Provider`: a value in the map which is used to create objects for
  your application.

## Bindings

- https://github.com/google/guice/wiki/Bindings
- Constructor bindings: to resolve a type, all its constructor
    * `bind(TwitterClient.class)`
    * Requires `@Inject` annotation on the constructor
        - Dependencies are passed in as parameters
- Provider methods: to resolve a type, call this method
    * Annotate a module method with `@Provides`
        - The return  type is bound.
        - Dependencies are passed in as parameters.
- Linked bindings: to resolve a type, use another binding
    * `bind(Tweeter.clas).to(SmsTweeter.class);`
    * Requires a binding for the target type.
    * If none exists, one will be created automatically.
- Binding annotations: uniquely identify a binding
    * `bind(String.class).annotatedWith(Username.class).toInstance("jesse")`

```java
@Inject
public SmsTweeter(@Username String username) {
    this.username  = username;
}
```

- Instance Bindings: always use the same value
    +  `bind(Integer.class).annotatedWith(Port.class).toInstance(8080);`

### Provider interface (injecting a Provider)

```java
public interface Provider<T> {
    T get();
}
```

- This looks like `Supplier` interface in java 8's functional
  interface??? YES!!!
    + This is was created before Java 8's functional interface!
- Why inject Providers?
    + to `load lazily`
    + to get `multiple instances`
        * e.g., to create multiple DatabaseConnections (call get() for
          each request/session)
    + to `mix scopes`
        * e.g., to access request-scoped objects from a singleton-scoped
          object.

## AOP

- https://github.com/google/guice/wiki/AOP
- You can apply method interceptors to injected objects
    + fantastic for cross-cutting concerns like transactions, security,
      and performance.

## Scopes

- https://github.com/google/guice/wiki/Scopes
- manage how many
- Scopes manage how instances are reused
    + because they're `stateful`
    + or `expensive`  to construct or lookup
    + or expensive to maintain
- Duration when the same instances are reused.
- Common scopes
    + `Unscoped`: one per use
        * create it, use it, and toss it
    + `@Singleton`: one per application
        * for heavyweight resources
        * and application state
    + `@RequestScoped`: one per web or RPC request
    + `@SessionScoped`: one per HTTP session
- Can apply scopes by:
    + Directly on the class definition
    + Adding annotations to bindings

## Injections

- https://github.com/google/guice/wiki/Injections
- Constructor injection
    + `@Inject` for constructors
- Method injection: setter injection
    + `@Inject` for setter methods
- Field injection
    + `@Inject` for fields / members. (Guice will use Reflection)
    + DON'T USE IT!!!
    + Difficult to test!


## Service Provider Inspection (SPI)

- Guice provides SPI, and we can use it to
    + create dependency graph
    + overrides some bindings of a module

## Compose modules from other modules

- `install(module)`

# APIs

- https://google.github.io/guice/api-docs/4.2/javadoc/overview-summary.html
- `@Inject`

## com.google.inject.Guice class

- https://google.github.io/guice/api-docs/7.0.0/javadoc/com/google/inject/Guice.html
- The entry point to the Guice framework. Creates Injectors from Modules.
- Guice supports a model of development that draws clear boundaries
  between APIs, Implementations of these APIs, Modules which configure
  these implementations, and finally Applications which consist of a
  collection of Modules. It is the Application, which typically defines
  your main() method, that bootstraps the Guice Injector using the Guice
  class, as in this example:

```java
 public class FooApplication {
   public static void main(String[] args) {
     Injector injector = Guice.createInjector(
         new ModuleA(),
         new ModuleB(),
         . . .
         new FooApplicationFlagsModule(args)
     );

     // Now just bootstrap the application and you're done
     FooStarter starter = injector.getInstance(FooStarter.class);
     starter.runApplication();
   }
 }
```

## Bindings

- Binder
    + https://google.github.io/guice/api-docs/4.2/javadoc/com/google/inject/Binder.html
    + https://google.github.io/guice/api-docs/4.2/javadoc/com/google/inject/binder/package-summary.html
    + Scoped bindings
        * Linked bindings
        * Annotated bindings
- Multibindings
    + https://google.github.io/guice/api-docs/4.2/javadoc/com/google/inject/multibindings/package-summary.html
    + https://github.com/google/guice/wiki/Multibindings
    + Including Optional bindings

# Best Practices

- https://github.com/google/guice/wiki/BestPractices
- Organize modules by feature, not by class type.
    + Organize module vertically, not horizontally.
- Minimize mutability: to gain immutability which is desired!
    + Use constructor injection as much as possible.
    + Only use method injection when it's necessary.
    + DO NOT USE field injection!
- Inject only direct dependencies (not indirect dependencies)
    + to have simpler code.
- Use the injector as little as possible (preferably only once at
  bootstrap)
    + DO NOT pass injectors into other injected objects through the
      constructor.
    + Injecting the injector makes it impossible for Guice to know
      ahead-of-time that your Dependency Graph is complete, because it
      lets folks get instances directly from the injector.
        * So long as nothing injects the injector, then Guice will 100%
          fail at Guice.createInjector time if any dependency isn't
          configured correctly.
        * However, if something injects the injector, then Guice might
          fail at runtime (when the code lazily calls
          injector.getInstance) with missing bindings error.
- Prefer `@Provides` methods over the binding DSL.
- Avoid calling `@Provider` methods and `@Inject` constructors directly
- Avoid circular dependencies
    + https://github.com/google/guice/wiki/CyclicDependencies
- Use `@Nullable`
    + Every injected parameter is non-null unless explicitly specified.
- Modules should be fast and side-effect free
    + DO NOT try to do heavy lifting in modules such as open a database
      connection, start up server, etc.
- Be careful about I/O in Providers
- Avoid conditional logic in modules
- Keep constructors as hidden as possible.
- Avoid binding Closable resources.
- Don't reuse binding annotations (aka `@Qualifiers`)
- Document the public bindings provided by modules

```java
/**
 * Provides {@link FooServiceClient} and derived bindings.
 *
 * [...]
 *
 * <p>The following bindings are provided:
 *
 * <ul>
 *   <li>{@link FooServiceClient}
 *   <li>{@link FooServiceClientAuthenticator}
 * </ul>
 */
public final class FooServiceClientModule extends AbstractModule {
  // ...
}
```

# Examples


# Override bindings and modules

Overriding bindings and modules in Google Guice can be useful for
testing, configuration, and modularity. Here are the various ways to
achieve this:

## 1. Using Child Injector

You can create a child injector from an existing injector and override
the bindings. This allows you to have a hierarchy of injectors, where
the child injector can override bindings from the parent.

Example:

```java
Injector parentInjector = Guice.createInjector(new ParentModule());

Injector childInjector = parentInjector.createChildInjector(new AbstractModule() {
    @Override
    protected void configure() {
        bind(Service.class).to(MockService.class);
    }
});

Service service = childInjector.getInstance(Service.class);
```

In this example, MockService overrides the Service binding from ParentModule.

## 2. Using Modules.override Method

Guice provides a Modules.override method to override bindings from one
or more modules with bindings from another module.

Example:

```java
Module originalModule = new AbstractModule() {
    @Override
    protected void configure() {
        bind(Service.class).to(RealService.class);
    }
};

Module overrideModule = new AbstractModule() {
    @Override
    protected void configure() {
        bind(Service.class).to(MockService.class);
    }
};

Injector injector = Guice.createInjector(Modules.override(originalModule).with(overrideModule));

Service service = injector.getInstance(Service.class);
```

Here, MockService overrides the binding of Service to RealService.

## 3. Using @Provides Method Override

You can also override @Provides methods in a module. The last bound
value will take precedence.

Example:

```java
class MyModule extends AbstractModule {
    @Provides
    Service provideService() {
        return new RealService();
    }
}

class TestModule extends AbstractModule {
    @Provides
    Service provideService() {
        return new MockService();
    }
}

Injector injector = Guice.createInjector(new MyModule(), new TestModule());

Service service = injector.getInstance(Service.class);
```

In this case, TestModule's provideService method will override MyModule's provideService method.

## 4. Using @Named Annotation for Qualifiers

Another approach is to use qualifiers such as @Named to distinguish
between different implementations. This way, you can provide specific
implementations where needed.

Example:

```java
class MyModule extends AbstractModule {
    @Override
    protected void configure() {
        bind(Service.class).annotatedWith(Names.named("real")).to(RealService.class);
        bind(Service.class).annotatedWith(Names.named("mock")).to(MockService.class);
    }
}

Injector injector = Guice.createInjector(new MyModule());

Service realService = injector.getInstance(Key.get(Service.class, Names.named("real")));
Service mockService = injector.getInstance(Key.get(Service.class, Names.named("mock")));
```

In this case, both RealService and MockService can coexist and be injected where appropriate using @Named annotation.

## 5. Custom Annotations as Qualifiers

Instead of using @Named, you can create custom annotations to qualify different bindings.

Example:

```java
@Retention(RUNTIME)
@Target({ FIELD, PARAMETER, METHOD })
@BindingAnnotation
@interface Real {}

@Retention(RUNTIME)
@Target({ FIELD, PARAMETER, METHOD })
@BindingAnnotation
@interface Mock {}

class MyModule extends AbstractModule {
    @Override
    protected void configure() {
        bind(Service.class).annotatedWith(Real.class).to(RealService.class);
        bind(Service.class).annotatedWith(Mock.class).to(MockService.class);
    }
}

Injector injector = Guice.createInjector(new MyModule());

Service realService = injector.getInstance(Key.get(Service.class, Real.class));
Service mockService = injector.getInstance(Key.get(Service.class, Mock.class));
```

Here, @Real and @Mock custom annotations are used to differentiate between different Service implementations.

## Detailed Explanation of Each Method:

### Child Injector:

Use Case: When you have a hierarchy of configurations, and you need to override some bindings for a specific part of your application.
Pros: Clean separation between parent and child configurations.
Cons: Managing multiple injectors can be complex.

### Modules.override:

Use Case: When you need to override bindings in a more straightforward manner, typically for testing.
Pros: Simple to use, especially for overriding multiple bindings at once.
Cons: Can become unwieldy with many overrides.

### @Provides Method Override:

Use Case: When overriding specific provider methods in testing or modular configurations.
Pros: Clear and method-specific.
Cons: Can lead to ambiguity if multiple modules provide the same method.

### @Named Annotation:

Use Case: When you have multiple implementations of the same type and need to distinguish between them.
Pros: Allows multiple implementations to coexist.
Cons: Using string names can lead to typos and is less type-safe.

### Custom Annotations:

Use Case: Similar to @Named, but with type safety and better readability.
Pros: Type-safe and more readable.
Cons: Requires more boilerplate code to define custom annotations.
Each method provides different ways to handle complex dependency injection scenarios, making Guice a versatile tool for various applications.

# Tips and Tricks

## javax.inject (JSR-330) vs. com.google.inject

- https://github.com/google/guice/wiki/JSR330
- Best Practices
    + Prefer JST-330's annotations and interfaces.
