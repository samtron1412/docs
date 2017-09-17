[TOC]

# Overview

Object-oriented programming (OOP) is a programming paradigm based on the
concept of "objects," which may contain data, in the form of fields,
often known as attributes; and code, in the form of procedures, often
known as methods.
- A feature of objects is that an object's procedures can access adn
  often modify the data fields of the object with which they are
  associated (objects have a notion of "this" or "self").
- In OOP, computer programs are designed by making them out of objects
  that interact with one another.
- There is significant diversity of OOP languages, but the most popular
  ones are class-based, meaning that objects are instances of classes,
  which typically also determine their type.

# Core concepts

## Abstraction

Data abstraction provides the outside world with only essential
information, in a process of representing essential features without
including implementation details.
- The concept of abstraction is that we focus on essential qualities,
  rather than the specific characteristics of one particular example.

### Interfaces

An interface is a completely abstract class that contains only abstract
methods.
- Other classes implement the abstract methods of the interfaces.

## Encapsulation

The idea behind encapsulation is to ensure that implementation details
are not visible to users.
- The variables of one class will be hidden from the other classes,
accessible only through the methods of the current class.
- This is call data hiding.

Benefits:
- Control of the way data is accessed or modified.
- More flexible and easily changed code.
- Ability to change one part of the code without affecting other parts.

## Inheritance

Inheritance is the process that enables one class to acquire the
properties (methods and variables) of another.
- With inheritance, the information is placed in a more manageable,
  hierarchical order.
- The class inheriting the properties of another is the subclass (also
  derived class, or child class); the class whose properties are
  inherited is the superclass (base class, or parent class).
- When one class is inherited from another class, it inherits all of the
  superclass' non-private variables and methods.
- Constructors are not member methods, and so are not inherited by
  subclasses. However, the constructor of the superclass is called when
  the subclass is instantiated.

## Polymorphism

Polymorphism, which refers to the idea of "having many forms," occurs
when there is a hierarchy of classes related to each other through
inheritance.
- One method with multiple implementations.
- A call to a member method will cause a different implementation to be
  executed, depending on the type of the object invoking the method.

Here is an example in Java: Dog and Cat are classes that inherit from
the Animal class. Each class has its own implementation of the makeSound
() method.

```java
class Animal {
    public void makeSound() {
        System.out.println("Grr...");
    }
}

class Cat extends Animal {
    public void makeSound() {
        System.out.println("Meow");
    }
}

class Dog extends Animal {
    public void makeSound() {
        System.out.println("Woof");
    }
}
```

As all Cat and Dog objects are Animal objects, we can do the following
in main:

```java
public static void main(String[] args) {
    Animal a = new Dog();
    Animal b = new Cat();
    a.makeSound();  //Outputs "Woof"
    b.makeSound();  //Outputs "Meow"
}
```

This demonstrate that you can use the Animal variable  without actually
knowing that it contains an object of the subclass. This is very useful
when you have multiple subclasses of the superclass.

### Method overriding

A subclass can define a behavior that's specific to the subclass type,
meaning that a subclass can implement a parent class method based on its
requirements. This feature is known as method overriding.
- Run-time polymorphism

### Method overloading

When methods have the same name, but different parameters, it is known
as method overloading.
- Compile-time polymorphism

# References
