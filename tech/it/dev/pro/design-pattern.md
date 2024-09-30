[TOC]

# Overview

- https://refactoring.guru/design-patterns
- A software design pattern is a general, reusable solution to a
  commonly occurring problem within a given context in software design.
- It is not a finished design that can be transformed directly into
  source or machine code.
- Rather, it is a description or template for how to solve a problem
  that can be used in many different situations.
- Design patterns are formalized best practices that the programmer can
  use to solve common problems when designing an application or system.

# Design Principles

```
There is a tradeoff between design patterns/principles and code
complexity, and that was what I was inviting the team to discuss on my
CR. I think Java developers tend to get carried away with these kinds of
things, which ends up making code more complicated than necessary and
results in bugs (for example, when I made the Holder a top-level class
instead of an inner class).
```

- SOLID
    + Single responsibility
        * https://en.wikipedia.org/wiki/Single_responsibility_principle
    + Open to extension closed to modification
        * https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle
    + Liskov substitution
        * https://stackoverflow.com/questions/56860/what-is-an-example-of-the-liskov-substitution-principle
    + Interface segregation
    + Dependency Inversion
- YAGNI (You Aren't Gonna Need It)
    + https://softwareengineering.stackexchange.com/questions/401797/is-there-a-conflict-between-yagni-and-srp
    + https://martinfowler.com/bliki/Yagni.html

## Working effectively with legacy code

## Clean Code

# Creational patterns

## Factory Method

## Abstract Factory

## Builder

## Prototype

## Singleton

- Serializable, reflection and cloneable may break singleton(except enum
  singleton).
- Multi-threaded programming consideration
    + Eager initialization
        * Private static field
        * Static block
    + Lazy initialization
        * Enum with single value (Enum singleton) (similar as Public
          static field but safer)
        * Static holder singleton (Bill Pugh singleton)
            - https://en.wikipedia.org/wiki/Initialization-on-demand_holder_idiom
        * Double checked locking
            - https://en.wikipedia.org/wiki/Double-checked_locking


# Structural patterns

## Adapter

## Bridge

## Composition / Composite

- https://en.wikipedia.org/wiki/Composite_pattern
- https://en.wikipedia.org/wiki/Composition_over_inheritance
- https://softwareengineering.stackexchange.com/questions/371707/why-the-industry-prefer-use-composition-over-inheritance
    + The argument is between inheritance and composition: Should you say
      that the "Rectangle has a Shape"? Refer to the Liskov substitution
      principle, if Rectangle is meant to be used where Shape is used, use
      inheritance.
- https://softwareengineering.stackexchange.com/questions/134097/why-should-i-prefer-composition-over-inheritance
- https://softwareengineering.stackexchange.com/questions/65179/where-does-this-concept-of-favor-composition-over-inheritance-come-from
- https://www.thoughtworks.com/en-us/insights/blog/composition-vs-inheritance-how-choose
- https://neethack.com/2017/04/Why-inheritance-is-bad/
- https://www.artima.com/articles/design-principles-from-design-patterns

```
Composition versus inheritance
Bill Venners: The other principle of object-oriented design that you
offer in the GoF introduction is, "Favor object composition over class
inheritance." What does that mean, and why is it a good thing to do?

Erich Gamma: I still think it's true even after ten years. Inheritance
is a cool way to change behavior. But we know that it's brittle, because
the subclass can easily make assumptions about the context in which a
method it overrides is getting called. There's a tight coupling between
the base class and the subclass, because of the implicit context in
which the subclass code I plug in will be called. Composition has a
nicer property. The coupling is reduced by just having some smaller
things you plug into something bigger, and the bigger object just calls
the smaller object back. From an API point of view defining that a
method can be overridden is a stronger commitment than defining that a
method can be called.

In a subclass you can make assumptions about the internal state of the
superclass when the method you override is getting called. When you just
plug in some behavior, then it's simpler. That's why you should favor
composition. A common misunderstanding is that composition doesn't use
inheritance at all. Composition is using inheritance, but typically you
just implement a small interface and you do not inherit from a big
class. The Java listener idiom is a good example for composition. With
listeners you implement a listener interface or inherit from what is
called an adapter. You create a listener object and register it with a
Button widget, for example. There is no need to subclass Button to react
to events.

Bill Venners: When I talk about the GoF book in my design seminar, I
mention that what shows up over and over is mostly using composition
with interface inheritance for different reasons. By interface
inheritance I mean, for example, inheriting from pure virtual base
classes in C++, or code font interface inheritance in Java. The Listener
example you mention, for instance, has inheritance going on. I implement
MouseListener to make MyMouseListener. When I pass an instance to a
JPanel via addMouseListener, now I'm using composition because the
front-end JPanel that's holding onto that MouseListener will call its
mouseClicked method.

Erich Gamma: Yes, you have reduced the coupling. In addition you now
have a separate listener object and you might even be able to connect it
with other objects.

Bill Venners: That extra flexibility of composition over inheritance is
what I've observed, and it's something I've always had difficulty
explaining. That's what I was hoping you could capture in words. Why?
What is really going on? Where does the increased flexibility really
come from?

Erich Gamma: We call this black box reuse. You have a container, and you
plug in some smaller objects. These smaller objects configure the
container and customize the behavior of the container. This is possible
since the container delegates some behavior to the smaller thing. In the
end you get customization by configuration. This provides you with both
flexibility and reuse opportunities for the smaller things. That's
powerful. Rather than giving you a lengthy explanation, let me just
point you to the Strategy pattern. It is my prototypical example for the
flexibility of composition over inheritance. The increased flexibility
comes from the fact that you can plug-in different strategy objects and,
moreovers, that you can even change the strategy objects dynamically at
run-time.

Bill Venners: So if I were to use inheritance...

Erich Gamma: You can't do this mix and match of strategy objects. In
particular you cannot do it dynamically at run-time.
```


## Decorator

## Facade Pattern

- https://en.wikipedia.org/wiki/Facade_pattern
- https://www.tutorialspoint.com/design_pattern/facade_pattern.htm

## Flyweight

## Proxy


# Behavioral patterns

## Chain of Responsibility

## Command

## Iterator

## Mediator

## Memonto

## Observer

## State

## Strategy

## Template Method

## Visitor

- What
    + https://en.wikipedia.org/wiki/Visitor_pattern
    + SOLID: Also good to follow open/closed principle and single
      responsibility principle when implementing this pattern.
- When
    + https://stackoverflow.com/a/478672
    + Having a relatively fix set of class hierarchy, but the set of
      methods for the class hierarchy can grow over time or not
      determined at this moment.
    + The team develops the class hierarchy (and initial set of
      supported methods) are different from the team that develops other
      supported methods.
        * Third-party libraries!
    + Works really well for "recursive" structures like directory tress,
      XML structures, or document outlines.
        * Hierarchical visitor pattern: more flexible than the classic
          visitor pattern.
            - Track the depth of traversal and decide which branch to
              traverse or stop traversing all together. The classic
              visitor pattern will visit all nodes.
        * https://stackoverflow.com/a/255437
    + Other use cases:
        * https://stackoverflow.com/a/47968789
- Examples
    + https://en.wikipedia.org/wiki/Visitor_pattern#Java_example
    + https://docs.oracle.com/javase%2Ftutorial%2F/essential/io/walk.html
    + http://www.artima.com/cppsource/top_cpp_aha_moments.html

```
In my opinion, the open/closed principle is most important for
frameworks that are vended to external customers. For example, the JDK
uses the visitor pattern for traversing a file system tree
(https://docs.oracle.com/javase%2Ftutorial%2F/essential/io/walk.html).

This is so people can implement whatever operations they want as they
traverse the tree rather than requiring the JDK to provide all
implementations (recursively print, delete, etc.) If it is your own
codebase, it is much easier to simply modify the library to add the
functionality you need.
```

# Concurrency patterns

# Enterprise Integration Pattern

- https://martinfowler.com/books/eip.html
- https://en.wikipedia.org/wiki/Enterprise_Integration_Patterns
- http://www.enterpriseintegrationpatterns.com/
    + Up-to-date patterns with current technologies and tools
- https://www.youtube.com/watch?v=QmaNucXFYd8
- https://www.amazon.com/Enterprise-Integration-Patterns-Designing-Deploying/dp/0321200683

# Domain Driven Design

- https://en.wikipedia.org/wiki/Domain-driven_design
- https://martinfowler.com/bliki/DomainDrivenDesign.html
- https://www.amazon.com/gp/product/0321125215/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0321125215&linkCode=as2&tag=martinfowlerc-20
- https://www.amazon.com/dp/0321834577
- https://www.amazon.com/dp/1118714709
- Command Query Responsibility Segregation (CQRS) and Event Sourcing
    + https://learn.microsoft.com/en-us/previous-versions/msp-n-p/jj554200(v=pandp.10)?redirectedfrom=MSDN

# Cloud-based Design

- https://learn.microsoft.com/en-us/azure/architecture/
- https://wa.aws.amazon.com/index.en.html
    + https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html
    + https://aws.amazon.com/architecture/well-architected

# Other patterns

## Lazy initialization


## Inversion of Control

- https://martinfowler.com/bliki/InversionOfControl.html
- https://en.wikipedia.org/wiki/Inversion_of_control
- Inversion of Control is a defining characteristic of a framework.
    + In procedural programming, the main custom code will be in control of the
      flow, and it'll call framework/subroutines to accomplish tasks.
    + With inversion of control, the framework is in control, and the
      framework will call your custom code when it's needed.
- IoC is used in GUI environments, web server application frameworks,
  event-driven programming.

### Dependency Injection

- More details in `dependency-injection.md`
- Instead of inverting the control flow, it inverts the control over
  implementations of dependencies.

# Other related topics

## Polyglot Programming and Polyglot Persistence

- https://martinfowler.com/bliki/PolyglotPersistence.html

# References

[book]: https://en.wikipedia.org/wiki/Design_Patterns
[wiki]: https://en.wikipedia.org/wiki/Software_design_pattern
[five-principles]: https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)
[facade-pattern]: https://en.wikipedia.org/wiki/Facade_pattern
