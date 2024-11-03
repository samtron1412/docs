# Overview

- Homepage: https://github.com/google/guice
- https://github.com/google/guice/wiki/GettingStarted
- https://justin.abrah.ms/misc/an-overview-of-guice-java-dependency-injection.html
- https://www.baeldung.com/guice
- https://www.tutorialspoint.com/guice/guice_linked_binding.htm

# APIs

- https://google.github.io/guice/api-docs/4.2/javadoc/overview-summary.html

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
