[TOC]

# Overview

- A software design pattern is a general, reusable solution to a
  commonly occurring problem within a given context in software design.
- It is not a finished design that can be transformed directly into
  source or machine code.
- Rather, it is a description or template for how to solve a problem
  that can be used in many different situations.
- Design patterns are formalized best practices that the programmer can
  use to solve common problems when designing an application or system.

# Design Principles

- SOLID
    + Single responsibility
    + Open to extension closed to modification
    + Liskov substitution
    + Interface segregation
    + Dependency Inversion

# Creational patterns

## Builder

## Dependency Injection

## Factory method

## Lazy initialization

## Singleton

# Structural patterns

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


## Facade Pattern

- https://en.wikipedia.org/wiki/Facade_pattern
- https://www.tutorialspoint.com/design_pattern/facade_pattern.htm

# Behavioral patterns


# Concurrency patterns

# References

[book]: https://en.wikipedia.org/wiki/Design_Patterns
[wiki]: https://en.wikipedia.org/wiki/Software_design_pattern
[five-principles]: https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)
[facade-pattern]: https://en.wikipedia.org/wiki/Facade_pattern
