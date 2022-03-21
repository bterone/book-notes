## Design Patterns
## Elements of Reusable Object-Oriented Software

# Table of Contents

<details>
  <summary>Creational Patterns</summary>

  - [Abstract Factory](#abstract-factory)
  - [Builder](#builder)
  - [Factory Method](#factory-method)
  - [Prototype](#prototype)
  - [Singleton](#singleton)
</details>
<details>
  <summary>Structural Patterns</summary>

  - [Adapter](#adapter)
  - [Bridge](#bridge)
  - [Composite](#composite)
  - [Decorator](#decorator)
  - [Facade](#facade)
  - [Flyweight](#flyweight)
  - [Proxy](#proxy)
</details>
<details>
  <summary>Behavioral Patterns</summary>

  - [Chain of Responsibility](#chain-of-responsibility)
  - [Command](#command)
  - [Interpreter](#interpreter)
  - [Iterator](#iterator)
  - [Mediator](#mediator)
  - [Memento](#memento)
  - [Observer](#observer)
  - [State](#state)
  - [Strategy](#strategy)
  - [Template Method](#template-method)
  - [Visitor](#visitor)
</details>

The following table is how the patterns are classified and which scope they apply to. i.e. Classes or Objects.
![Design Pattern Table](assets/images/design-patterns/design-pattern-table.png)


# Creational Patterns
Following is a list of patterns for how objects are created.

## Abstract Factory
Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

## Builder
Separate the construction of a complex object from its representation so that the same construction process can create different representations.

## Factory Method
Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

## Prototype
Specify the knids of objects to create using a prototypical instance, and create new objects by copying this prototype.

## Singleton
Ensure a class only has one instance, and provide a global point of access to it.


# Structural Patterns
Following is a list of patterns for how objects relate to each other

## Adapter
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

## Bridge
Decouple an abstraction from its implementation so that the two can vary independantly

## Composite
Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and comopsitions of objects uniformly.

## Decorator
Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

## Facade
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

## Flyweight
Use sharing to support large numbers of fine-grained objects efficiently.

## Proxy
Provide a surrogate or placeholder for another object to control access to it.


# Behavioral Patterns
Following is a list of patterns for how objects communicate with each other

## Chain of Responsibility
Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

## Command
Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

## Interpreter
Given a language, define a represention for its grammar along with an interpreter that uses the representation to interpret sentences in the language.

## Iterator
Provide a way to access the elements of an aggregate object sequentially withoutexposingitsunderlying representation.

## Mediator
Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

## Memento
Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.

## Observer
Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

## State
Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

## Strategy
Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

## Template Method
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

## Visitor
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.
