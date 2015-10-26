[TOC]

# [Install](https://www.ruby-lang.org/en/installation)
- Linux
	+ [RVM - Ruby Version Manager](http://rvm.io/)
	+
- Windows
	+ [RubyInstaller](http://rubyinstaller.org/)
	+ [pik](https://github.com/vertiginous/pik)

# Philosophy - Design
Ruby was influenced by `Perl, Smalltalk, Eiffel, Ada, and Lisp`.

## No perfect language
Each person will find an language perfect with himself.

## Orthogonal versus Harmonious (Trực giao so với Hài hòa)
*Yukihiro Matsumoto*: An example of orthogonality is allowing any combination of small features or syntax. For example, C++ supports both default parameter values for functions and overloading of function names based on parameters. Both are good features to have in a language, but because they are orthogonal, you can apply both at the same time. The compiler knows how to apply both at the same time. If it's ambiguous, the compiler will flag an error. But if I look at the code, I need to apply the rule with my brain too. I need to guess how the compiler works. If I'm right, and I'm smart enough, it's no problem. But if I'm not smart enough, and I'm really not, it causes confusion. The result will be unexpected for an ordinary person. This is an example of how orthogonality is bad.

## One way versus Many ways
*Python* support one way to do something, and *Ruby* provide many ways to so something. Follow *Matz* it make freedom and comfort for developers.

## The Joy
*Ruby* code concise and succinct. Get your jobs done quickly and fun.

## The Human Factor
Focus on *human*. We are the masters. They are the slaves.

Focus on programming efficiency and productivity, not runtime efficiency.

Ruby interpreter is robust, but Ruby language design does not.

## Principle of least surprise
Principle least surprise after you learn Ruby very well. Minimize confusion for experienced developers. You can surprise with C++ after works on it 2 year, but with Ruby you does not.

## Design
Ruby is a language designed in the following steps:

- take a simple lisp language (like one prior to CL).
- remove macros, s-expression.
- add simple object system (much simpler than CLOS).
- add blocks, inspired by higher order functions.
- add methods found in Smalltalk.
- add functionality found in Perl (in OO way).


# Category
Written in C.

Ruby is a *dynamic*, *reflective*, *object-oriented*, *general-purpose* programming language.

It supports multiple programming paradigms, including *functional*, *object-oriented*, and *imperative*.

It also has a *dynamic type system* and *automatic memory management*.

## Object-oriented (OOP)
Object-oriented programming (OOP) is a *programming paradigm* that represents the concept of `Objects` (noun) that have *data fields* (state - attributes that describe the object) and associated procedures known as *methods* (behavior - code - verb). `Objects`, which are usually *instances* of *classes*, are used to interact with one another to design applications and computer programs.

Object-oriented programming is an approach to designing *modular*, *reusable* software systems.

Everything is Objects. Every Object has two Class, *regular* Class and *singleton* Class. Every Class is an object of first-class `Class`.

## Reflective (hit yourself)
`Reflection` is the ability of a computer program to *examine* (type introspection) and *modify* the structure and behavior (specifically the values, meta-data, properties and functions) of the program at runtime.

### Historical background
>The earliest computers were programmed in their native *assembly language*, which were *inherently reflective* as these *original architectures* could be programmed by defining instructions as data and using [self-modifying code](http://en.wikipedia.org/wiki/Self-modifying_code)(usually use in early age of computer programming, and now use to write virus, it have some purposes). As programming moved to higher level languages such as C, this reflective ability disappeared.

### Type introspection (Examine)
`Type introspection` is the ability of a program to examine the type or properties of an object at runtime.

In Ruby, the `Object` class (ancestor of every class) provides `Object#instance_of?` and `Object#kind_of?` methods for checking the instance's class.

```ruby
$ irb
irb(main):001:0> A=Class.new
=> A
irb(main):002:0> B=Class.new A
=> B
irb(main):003:0> a=A.new
=> #<A:0x2e44b78>
irb(main):004:0> b=B.new
=> #<B:0x2e431b0>
irb(main):005:0> a.instance_of? A
=> true
irb(main):006:0> b.instance_of? A
=> false
irb(main):007:0> b.kind_of? A
=> true
---
irb(main):008:0> A.instance_of? Class
=> true
irb(main):009:0> a.class
=> A
irb(main):010:0> a.class.class
=> Class
irb(main):011:0> A > B
=> true
irb(main):012:0> B <= A
=> true
```

### Uses
For example, consider an application that uses two different classes `X` and `Y` interchangeably to perform similar operations. Without reflection-oriented programming, the application might be hard-coded to call method names of class X and class Y. However, using the reflection-oriented programming paradigm, the application could be designed and written to utilize reflection in order to invoke methods in classes X and Y *without hard-coding* method names.

*Reflection* is often used as part of [software testing](http://en.wikipedia.org/wiki/Software_testing), such as for the runtime creation/instantiation of [mock objects](http://en.wikipedia.org/wiki/Mock_object)(fake object to replace with real complex object).

*Reflection* is also a key strategy for [metaprogramming](http://en.wikipedia.org/wiki/Metaprogramming).

### Implementation
First-class citizen is an entity which supports all the operations generally available to other entities.

# Features and Learn
## Object, Class, Module

## Block and Closure

## Data types
### Symbol
- Immutable object.
- Every :symbol refers to exactly one object => performance

## Pre-defined variables

## Regular expression

## Security problems

## Syntax

## Standard library




