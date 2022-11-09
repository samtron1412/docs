# Overview

- Dependency injection library for Java
- https://dagger.dev
    + Dev guide: https://dagger.dev/dev-guide/
    + Tutorial: https://dagger.dev/tutorial
    + API: https://dagger.dev/api/latest
- Videos
    + Intro to Dagger 2: https://www.youtube.com/watch?v=oK_XtfXPkqw
    + Basic tutorial (good to have a basic overview how to use Dagger 2)
        * https://www.youtube.com/watch?v=plK0zyRLIP8

# Why?

- Dagger is a replacement for factory classes that implements the
  dependency injection design pattern without the burden of writing the
  boilerplate.
- DI helps testing
- It makes it easy to create reusable, interchangeable modules
    + You can share the same `AuthenticationModule` across all of your
      apps
    + You can run `DevLoggingModule` during development and
      `ProdLoggingModule` in production to get the right behavior in
      each situation.
- Dagger tries to generate code that mimics the code that a user might
  have hand-written to ensure that DI is as simple, traceable and
  performant ant as it can be.

# Using Dagger

- Coffee Application example
    + https://github.com/google/dagger/tree/master/examples/maven/coffee/src/main/java/example/dagger

## Declaring Dependencies

- Dagger constructs instances of your application classes and satisfies
  their dependencies.
- It uses the `javax.inject.Inject` annotations to identify which
  constructors and fields it is interested in.
- Use `@Inject` to annotate the constructor that Dagger should use to
  create instances of a class.
    + When a new instance is requested, Dagger will obtain the required
      parameters values and invoke this constructor.
    + Dagger can inject fields directly
- Classes that lack `@Inject` annotations cannot be constructed by
  Dagger.
    + At that point, you need to construct it and use `@Provides`
      annotation to declare dependencies.

## Satisfying Dependencies

- By default, Dagger satisfies each dependency by constructing an
  instance of the requested type as described above.
- `@Inject` doesn't work everywhere:
    + Interfaces can't be constructed
    + Third-party classes can't be annotated
    + Configurable objects must be configured
- For these cases, use an `@Provides` annotated method to satisfy a
  dependency.
    + The method's return type defines which dependency it satisfies.
    + For example, `provideHeater()` is invoked whenever a `Heater` is
      required

```java
@Provides static Heater provideHeater() {
    return new ElectricHeater();
}
```

- It's also possible for `@Provides` methods to have dependencies of
  their own.
    + For example, since `ElectricHeater` has an `@Inject` constructor,
      the above method could be written instead as:

```java
@Provides static Heater provideHeater(EletricHeater heater) {
    return heater;
}
```

- This way Dagger takes care of instantiating `ElectricHeater`, and the
  `@Provides` method is only used to alias it to the type `Heater`.
- In this particular case, we can simplify things further using an
  `@Binds` method to define the alias.
    + Unlike `@Provides`, an `@Binds` method is abstract, and has no
      implementation:

```java
@Binds Heater bindHeater(ElectricHeater heaterImpl);
```

- **NOTE**: Using `@Binds` is the preferred way to define an alias because
  Dagger only needs the module at compile time, and can avoid class
  loading the module at runtime
- All `@Provides` methods must belong to a module.
    + Modules are classes/interfaces that have an `@Module` annotation.

```java
@Module
interface HeaterModule {
    @Binds Heater bindHeater(ElectricHeater heaterImpl);
}
```

- Naming convention
    + `@Provides` methods: prefix `provide`
    + `@Binds` methods: prefix `bind`
    + `@Module` classes/interfaces: suffix `Module`

## Building the Graph

- The `@Inject` and `@Provides`-annotated classes form a graph of
  objects, linked by their dependencies.
    + Calling code accesses that dependency graph via a well-defined set
      of roots.
    + In Dagger 2, that set is defined by an interface with methods that
      have no arguments and return the desired type.
    + By applying the `@Component` annotation to such an interface and
      passing the module types to the modules parameter, Dagger 2 then
      fully *generates* an implementation of that contract.

```java
// multiple modules: @Component(modules = {DripCoffeeModule.class, ...})
// single module: @Component(modules = DripCoffeeModule.class)
@Component(modules = DripCoffeeModule.class)
interface CoffeeShop {
    CoffeeMaker maker();
}
```

- The generated implementation of the component has the same name as the
  interface prefixed with `Dagger`.
    + Obtain an instance by invoking the `builder()` method and use the
      returned builder to set dependencies and `build()` a new instance.

```java
CoffeeShop coffeeShop = DaggerCoffeeShop.builder()
    .dripCoffeeModule(new DripCoffeeModule())
    .build();
```

- **NOTE**: if your `@Component` is not a top-level type, the generated
  component's name will include its enclosing types' names, joined with
  an underscore.
    + For example, this code would generate a component named
      `DaggerFoo_Bar_BazComponent`.

```java
class Foo {
    static class Bar {
        @Component
        interface BazComponent {}
    }
}
```

- Any module with an accessible default constructor can be omitted
  without setting it because the builder will construct an instance
  automatically if none is set.
- For any module whose `@Provides` methods are all static, the
  implementation doesn't need an instance at all.
- If all dependencies can be constructed without the user creating a
  dependency instance, then the generated implementation will also have
  a `create()` method that can be used to get a new instance without
  having to deal with the builder.

```java
CoffeeShop coffeeShop = DaggerCoffeeShop.create();
```

## Bindings in the graph


## Singletons and Scoped Bindings

- Annotate an `@Provides` method or injectable class with `@Singleton`.
    + The graph will use a single instance of the value for all of its
      clients.

```java
@Provides @Singleton static Heater provideHeader() {
    return new EletricHeater();
}

@Singleton
class CoffeeMaker {
  ...
}
```

- Because Dagger 2 associates scoped instances in the graph with
  instances of component implementations, the components themselves need
  to declare which scope they intend to represent.
    + To declare that a component is associated with a given scope,
      simply apply the scope annotation to the component interface.
    + Components may have multiple scope annotations applied
        * This declares that they are aliases to the same scope, and so
          that component may include scoped bindings with any of the
          scopes it declares.

```java
@Component(modules = DripCoffeeModule.class)
@Singleton
interface CoffeeShop {
  CoffeeMaker maker();
}
```

## Reusable scope

- You want to limit the number of times an `@Inject`-constructed class is
  instantiated or a `@Provides` method is called, but you don't need to
  guarantee that the exact same instance issued during the lifetime of
  any particular component or sub-component.

```java
@Reusable // It doesn't matter how many scoopers we use, but don't waste them.
class CoffeeScooper {
  @Inject CoffeeScooper() {}
}

@Module
class CashRegisterModule {
  @Provides
  @Reusable // DON'T DO THIS! You do care which register you put your cash in.
            // Use a specific scope instead.
  static CashRegister badIdeaCashRegister() {
    return new CashRegister();
  }
}

@Reusable // DON'T DO THIS! You really do want a new filter each time, so this
          // should be unscoped.
class CoffeeFilter {
  @Inject CoffeeFilter() {}
}
```

- `@Reusable`-scoped bindings, unlike other scopes, are not associated
  with any single component; instead, each component that actually uses
  the binding will cache the returned or instantiated object.

## Lazy injections

- Sometimes you need an object to be instantiated lazily.
    + For any binding T, you can create a Lazy<T> which defers
      instantiation until the first call to Lazy<T>’s get() method.
- If T is a singleton, then Lazy<T> will be the same instance for all
  injections within the ObjectGraph.
    + Otherwise, each injection site will get its own Lazy<T> instance.

```java
class GrindingCoffeeMaker {
  @Inject Lazy<Grinder> lazyGrinder;

  public void brew() {
    while (needsGrinding()) {
      // Grinder created once on first call to .get() and cached.
      lazyGrinder.get().grind();
    }
  }
}
```

## Provider injections

## Qualifiers

## Optional bindings

## `@BindsInstance`

## Compile-time Validation

- The Dagger annotation processor is strict and will cause a compiler
  error if any bindings are invalid or incomplete.

## Compile-time Code Generation

- `Dagger<ComponentName>`: only need this in our code
- Other implementation details, just need it when debugging
    + `<...>_Factory.java`
    + `<...>_MembersInjector.java`

# Subcomponents

- Subcomponents are components that inherit and extend the object graph
  of a parent component.
- Use to partition application's object graph into subgraphs either to
  encapsulate diferent parts of your application from each other or to
  use more than one scope within a component.
- An object bound in a subcomponent can depend on any object that is
  bound in its parent component or any ancestor component, in addition
  to objects that are bound in its own modules.
    + On the other hand, objects bound in parent components can’t depend
      on those bound in subcomponents; nor can objects bound in one
      subcomponent depend on objects bound in sibling subcomponents.

## Declaring a subcomponent

- Just like for top-level components, you create a subcomponent by
  writing an abstract class or interface that declares abstract methods
  that return the types your application cares about.
    + Instead of annotating a subcomponent with @Component, you annotate
      it with @Subcomponent and install @Modules.
    + Similar to component builders, a @Subcomponent.Builder specifies
      an interface to supply necessary modules to construct the
      subcomponent.

```java
@Subcomponent(modules = RequestModule.class)
interface RequestComponent {
  RequestHandler requestHandler();

  @Subcomponent.Builder
  interface Builder {
    Builder requestModule(RequestModule module);
    RequestComponent build();
  }
}
```

## Adding a subcomponent to a parent component

- Add the subcomponent class to the subcomponents attribute of a @Module
  that the parent component installs.
    + Then the subcomponent’s builder can be requested from within the
      parent.

```java
@Module(subcomponents = RequestComponent.class)
class ServerModule {}

@Singleton
@Component(modules = ServerModule.class)
interface ServerComponent {
  RequestRouter requestRouter();
}

@Singleton
class RequestRouter {
  private final Provider<RequestComponent.Builder> requestComponentProvider;

  @Inject RequestRouter(
      Provider<RequestComponent.Builder> requestComponentProvider) {
    this.requestComponentProvider = requestComponentProvider;
  }

  void dataReceived(Data data) {
    RequestComponent requestComponent =
        requestComponentProvider.get()
            .requestModule(new RequestModule(data))
            .build();
    requestComponent.requestHandler()
        .writeResponse(200, "hello, world");
  }
}
```

# Multibindings

## Set Multibindings

## Map Multibindings

### Simple map keys

### Complex map keys

### Maps whose keys are not known at compile time

## Declaring multibindings

## Inherited subcomponent multibindings

# Best Practices


