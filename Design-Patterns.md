## Design Patterns
## Elements of Reusable Object-Oriented Software

# Table of Contents

- [Introduction](#introduction)

- <details>
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
    - [Iterator](#iterator)
    - [Mediator](#mediator)
    - [Memento](#memento)
    - [Observer](#observer)
    - [State](#state)
    - [Strategy](#strategy)
    - [Template Method](#template-method)
    - [Visitor](#visitor)
  </details>

## Introduction
The following table is how the patterns are classified and which scope they apply to. i.e. Classes or Objects.
![Design Pattern Table](assets/images/design-patterns/design-pattern-table.png)

Classes have relationships through inheritance, which are therefore static and fixed at compile-time.
Object relationships are more dynamic and can be changed during run-time.

Most patterns aren't found during early stages of design, and found over time as more apparant relationships emerge. The key is flexibility.

![Design Pattern Relationships](assets/images/design-patterns/design-pattern-relationships.png)

## Object Interfaces

Every operation in an object specifies the operation name, the objects it takes as params, and its return value. This is known as an operation's **signature**. A set of all signatures defined by an object's operations is called the interface.

### Dynamic Binding

> Dynamic-binding refers to the run-time assocation of a request to an object that executes different implemetatations of operations depending on the receiving object. Also known as late-binding.

By dynamic binding, we can subsitute objects with similar interfaces for each other during runtime, known as polymorphism.

### Abstract Class

> Abstract classes define a common interface for subclasses and defer some or all of its implementation to subclasses. This means abstract classes can't be instantiated.

> Non-abstract classes are called concrete classes.

## Inheritance versus Composition

Class inheritance is defined statically at compile-time and is supported in most languages. This makes it easier to modify the implementation being reused. When a subclass overrides some but not all operations, it can affect the operations it inherits as well. But it comes with disadvantages, such as being unable to change implementations inherited from parent classes at run-time, as the inheritance is defined at compile-time. Another downside is that parent classes often define at least part of their subclass's physical representation.

Because inheritance exposes a subclass to details of its parent's implementation, it's often said that "inheritance breaks encapsulation". 

Object composition is defined dynamically at run-time through objects acquiring refer- ences to other objects. Composition requires objects to respect each others' interfaces, which in turn requires carefully designed interfaces that don't stop you from using one object with many others. But there is a payoff. Because objects are accessed solely through their interfaces, we don't break encapsulation. 

Object composition has another effect on system design. Favoring object composition over class inheritance helps you keep each class encapsulated and focused on one task. Your classes and class hierarchies will remain small and will be less likely to grow into unmanageable monsters. On the other hand, a design based on object composition will have more objects (if fewer classes), and the system's behavior will depend on their interrelationships instead of being defined in one class.  

> Favor object composition over class inheritance.

## Delegation

Delegation are when a receiving object delegates a request operations to its **delegate**. This is similar to subclasses deferring requests to parent classes. E.g. Instead of a Window class inheriting Rectangle because they're similar in shape, we can keep an instance variable of Rectangle and *delegate* Rectangle-specific behavior to our Rectangle instance variable.

The Window class must forward requests explicitly instead of inheriting those operations.

## Inheritance versus Parameterized Types

Parameterized types give us a third way (in addition to class inheritance and object composition) to compose behavior in object-oriented systems.

Examples of Parameterized Types Patterns are the Template Method, Strategy, or an argument that specifies the name of the function to call and compare the elements.

Inheritance nor parameterized types are unable to change at run-time.

## Common Causes for Redesign

Design patterns are long term solutions on how systems are developed. Systems should take into account how it evolves over time.

1. Creating an object by specifying a class explicitly.
Applicable Patterns: Abstract Factory, Factory Method, Prototype.

2. Dependence on specific operations.
Applicable Patterns: Chain of Responsibility, Command

3. Dependence on hardware and software platform.
Applicable Patterns: Abstract Factory, Bridge.

4. Dependence on object representations or implementations.
Applicable Patterns: Abstract Factory, Bridge, Memento, Proxy.

5. Algorithmic dependencies.
Applicable Patterns: Builder, Iterator, Strategy, Template Method, Visitor.

6. Tight coupling.
Applicable Patterns: Abstract Factory, Bridge, Chain of Responsibility, Command, Facade, Mediator, Observer.

7. Extending functionality by subclassing.
Applicable Patterns: Bridge, Chain of Responsibility, Composite, Decorator, Observer, Strategy.

8. Inability to alter classes conveniently.
Applicable Patterns: Adapter, Decorator, Visitor.

> For indepth explanations on the causes, refer to Design Patterns, pg. 24.

### Classes of Software

1. Application Programs (E.g. Document or spreadsheet editor): 
   - Should prioritize *internal* reuse, maintainability, and extension. 

2. Toolkits: Set of related and reusable classes designed to provide general-purpose functionality. (E.g. Set of collection of classes for lists, associative tables, stacks, etc., like C++ I/O stream library).
   - These do not impose any design pattern, only provide functionality. Emphasizes code reuse.
   - They avoid assumptions and dependencies that could limit a toolkit's flexibility.

3. Frameworks: Dictates the archiecture of the application, and predefines design paramters.

The differences between design patterns and frameworks are as follows:
1. Design patterns are more abstract than frameworks.
2. Design patterns are smaller architectural elements than frameworks.
3. Design patterns are less specialized than frameworks.

## How to Select a Design Pattern
- Consider how design patterns solve design problems.
- Scan Intent sections.
- Study how patterns interrelate.
- Study patterns of like purpose.
- Examine a cause of redesign.
- Consider what should be variable in your design.

## How to Use a Design Pattern
1. Read the pattern once through for an overview.
2. Go back and study the Structure, Participants and Collaborations sections.
3. Look at the Sample Code section to see a concrete example of the pattern in code.
4. Choose names for pattern participants that are meaningful in the application context.
5. Define the classes. (Declare interfaces, establish their inheritance relationships and identity existing classes in your application that the pattern would affect and modify them accordingly)
6. Define application-specific names for operations in the pattern.
7. Implement the operations to carry out the responsibilities and collaborations in the pattern.

![Design Pattern Aspects](assets/images/design-patterns/design-pattern-aspects.png)

> Recursive Composition is a way to represent hierarchically structured information from building increasingly complex elements out of simpler ones.

---------------------------------------------

# Creational Patterns
Following is a list of patterns for how objects are created. These patterns show how subclasses or other objects are used during creation of classes/objects.

## Abstract Factory
Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

Many designs start by using [Factory Method](#factory-method) (less complicated and more customizable via subclasses) and evolve toward Abstract Factory, [Prototype](#prototype), or [Builder](#builder) (more flexible, but more complicated).

![Abstract Factory](./assets/images/design-patterns/abstract-factory.png)

- **Abstract Products** declare interfaces for a set of distinct but related products which make up a product family.
- **Concrete Products** are various implementations of abstract products, grouped by variants. Each abstract product (chair/sofa) must be implemented in all given variants (Victorian/Modern).
- The **Abstract Factory** interface declares a set of methods for creating each of the abstract products.
- **Concrete Factories** implement creation methods of the abstract factory. Each concrete factory corresponds to a specific variant of products and creates only those product variants.
- Although concrete factories instantiate concrete products, signatures of their creation methods must return corresponding abstract products. This way the client code that uses a factory doesn’t get coupled to the specific variant of the product it gets from a factory. The Client can work with any concrete factory/product variant, as long as it communicates with their objects via abstract interfaces.

[Code Example](./assets/docs/code/abstract-factory.md)

## Builder
Separate the construction of a complex object from its representation so that the same construction process can create different representations.

Use the Builder pattern:
- To get rid of a “telescoping constructor”. 

E.g.
```js
class Pizza {
    Pizza(int size) { ... }
    Pizza(int size, boolean cheese) { ... }
    Pizza(int size, boolean cheese, boolean pepperoni) { ... }
    // ...
```

- When you want your code to be able to create different representations of some product (for example, stone and wooden houses).
- To construct [Composite](#composite) trees or other complex objects.

![Builder](./assets/images/design-patterns/builder.png)

- The **Builder** interface declares product construction steps that are common to all types of builders.
- **Concrete Builders** provide different implementations of the construction steps. Concrete builders may produce products that don’t follow the common interface.
- **Products** are resulting objects. Products constructed by different builders don’t have to belong to the same class hierarchy or interface.
- The **Director** class defines the order in which to call construction steps, so you can create and reuse specific configurations of products.
- The **Client** must associate one of the builder objects with the director. Usually, it’s done just once, via parameters of the director’s constructor. Then the director uses that builder object for all further construction. However, there’s an alternative approach for when the client passes the builder object to the production method of the director. In this case, you can use a different builder each time you produce something with the director.

[Code Example](./assets/docs/code/builder.md)

## Factory Method
Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

![Factory Method](./assets/images/design-patterns/factory-method.png)

- The **Product** declares the interface, which is common to all objects that can be produced by the creator and its subclasses.
- **Concrete Products** are different implementations of the product interface.
- The **Creator** class declares the factory method that returns new product objects. It’s important that the return type of this method matches the product interface. You can declare the factory method as abstract to force all subclasses to implement their own versions of the method. As an alternative, the base factory method can return some default product type.
- **Concrete Creators** override the base factory method so it returns a different type of product. Note that the factory method doesn’t have to create new instances all the time. It can also return existing objects from a cache, an object pool, or another source.

[Code Example](./assets/docs/code/factory-method.md)

## Prototype
Specify the knids of objects to create using a prototypical instance, and create new objects by copying this prototype.

![Prototype](./assets/images/design-patterns/prototype.png)

- The **Prototype** interface declares the cloning methods. In most cases, it’s a single clone method.
- The **Concrete Prototype** class implements the cloning method. In addition to copying the original object’s data to the clone, this method may also handle some edge cases of the cloning process related to cloning linked objects, untangling recursive dependencies, etc.
- The **Client** can produce a copy of any object that follows the prototype interface.

> Many designs start by using [Factory Method](#factory-method) (less complicated and more customizable via subclasses) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, but more complicated).

> Sometimes Prototype can be a simpler alternative to Memento. This works if the object, the state of which you want to store in the history, is fairly straightforward and doesn’t have links to external resources, or the links are easy to re-establish.

[Code Example](./assets/docs/code/prototype.md)

## Singleton
Ensure a class only has one instance, and provide a global point of access to it.

![Singleton](./assets/images/design-patterns/singleton.png)

- The **Singleton** class declares the static method getInstance that returns the same instance of its own class.
- The Singleton’s constructor should be hidden from the client code. Calling the getInstance method should be the only way of getting the Singleton object.

[Code Example](./assets/docs/code/singleton.md)


# Structural Patterns
Following is a list of patterns for how objects relate to each other. Structural class patterns uses inheritance to compose classes, while object patterns describe ways to assemble objects.

## Adapter
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

This implementation uses the object composition principle: the adapter implements the interface of one object and wraps the other one. It can be implemented in all popular programming languages.

![Object Adapter](./assets/images/design-patterns/object-adapter.png)

- The **Client** is a class that contains the existing business logic of the program.
- The **Client Interface** describes a protocol that other classes must follow to be able to collaborate with the client code.
- The **Service** is some useful class (usually 3rd-party or legacy). The client can’t use this class directly because it has an incompatible interface.
- The **Adapter** is a class that’s able to work with both the client and the service: it implements the client interface, while wrapping the service object. The adapter receives calls from the client via the adapter interface and translates them into calls to the wrapped service object in a format it can understand.
- The client code doesn’t get coupled to the concrete adapter class as long as it works with the adapter via the client interface. Thanks to this, you can introduce new types of adapters into the program without breaking the existing client code. This can be useful when the interface of the service class gets changed or replaced: you can just create a new adapter class without changing the client code.

This implementation uses inheritance: the adapter inherits interfaces from both objects at the same time. Note that this approach can only be implemented in programming languages that support multiple inheritance, such as C++.

![Class Adapter](./assets/images/design-patterns/class-adapter.png)

- The **Class Adapter** doesn’t need to wrap any objects because it inherits behaviors from both the client and the service. The adaptation happens within the overridden methods. The resulting adapter can be used in place of an existing client class.

[Code Example](./assets/docs/code/adapter.md)

## Bridge
Decouple an abstraction from its implementation so that the two can vary independantly.

Use the Bridge pattern when:
- You want to divide and organize a monolithic class that has several variants of some functionality (for example, if the class can work with various database servers).
- You need to extend a class in several orthogonal (independent) dimensions.
- You need to be able to switch implementations at runtime.

![Bridge](./assets/images/design-patterns/bridge.png)

- The **Abstraction** provides high-level control logic. It relies on the implementation object to do the actual low-level work.
- The **Implementation** declares the interface that’s common for all concrete implementations. An abstraction can only communicate with an implementation object via methods that are declared here. The abstraction may list the same methods as the implementation, but usually the abstraction declares some complex behaviors that rely on a wide variety of primitive operations declared by the implementation.
- **Concrete Implementations** contain platform-specific code.
- **Refined Abstractions** provide variants of control logic. Like their parent, they work with different implementations via the general implementation interface.
- Usually, the **Client** is only interested in working with the abstraction. However, it’s the client’s job to link the abstraction object with one of the implementation objects.

[Code Example](./assets/docs/code/bridge.md)

## Composite
Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and comopsitions of objects uniformly.

The composite pattern is only useful when the core model of your app can be represented as a tree.

Use the Factory Method when:
- You don't know beforehand the exact types and dependencies of the objects your code should work with.
- You want to provide users of your library or framework with a way to extend its internal components.
- You want to save system resources by reusing existing objects instead of rebuilding them each time.

![Composite](./assets/images/design-patterns/composite.png)

- The **Component** interface describe the common operations for all elements in the tree.
- The **Leaf** doesn't have sub-elements and usually do most of the real work as they don't delegate
- The **Container** (also known as **Composite**) is an element that has sub-elements (leaves). It works with all sub-elements only via the common interface. When it receives a request, it delegates to sub-elements, processes the results and returns the final result to the client.
- The **Client** works with all the elements in the tree via the component interface.

[Code Example](./assets/docs/code/composite.md)

## Decorator
Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

Use the Decorator pattern when:
- You need to be able to assign extra behaviors to objects at runtime without breaking the code that uses these objects.
- It’s awkward or not possible to extend an object’s behavior using inheritance.

![Decorator](./assets/images/design-patterns/decorator.png)

- The **Component** declares the common interface for both wrappers and wrapped objects.
- **Concrete Component** is a class of objects being wrapped. It defines the basic behavior, which can be altered by decorators.
- The **Base Decorator** class has a field for referencing a wrapped object. The field’s type should be declared as the component interface so it can contain both concrete components and decorators. The base decorator delegates all operations to the wrapped object.
- **Concrete Decorators** define extra behaviors that can be added to components dynamically. Concrete decorators override methods of the base decorator and execute their behavior either before or after calling the parent method.
- The **Client** can wrap components in multiple layers of decorators, as long as it works with all objects via the component interface.

[Code Example](./assets/docs/code/decorator.md)

## Facade
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

> Facade defines a new interface for existing objects, whereas Adapter tries to make the existing interface usable. Adapter usually wraps just one object, while Facade works with an entire subsystem of objects.

![Facade](./assets/images/design-patterns/facade.png)

- The **Facade** provides convenient access to a particular part of the subsystem’s functionality. It knows where to direct the client’s request and how to operate all the moving parts.
- An **Additional Facade** class can be created to prevent polluting a single facade with unrelated features that might make it yet another complex structure. Additional facades can be used by both clients and other facades.
- The **Complex Subsystem** consists of dozens of various objects. To make them all do something meaningful, you have to dive deep into the subsystem’s implementation details, such as initializing objects in the correct order and supplying them with data in the proper format. Subsystem classes aren’t aware of the facade’s existence. They operate within the system and work with each other directly.
- The **Client** uses the facade instead of calling the subsystem objects directly.

> Facade is similar to [Proxy](#proxy) in that both buffer a complex entity and initialize it on its own. Unlike Facade, Proxy has the same interface as its service object, which makes them interchangeable.

[Code Example](./assets/docs/code/facade.md)

## Flyweight
Use sharing to support large numbers of fine-grained objects efficiently.

> Use the Flyweight pattern only when your program must support a huge number of objects which barely fit into available RAM.

![Flyweight](./assets/images/design-patterns/flyweight.png)

- The **Flyweight** pattern is merely an optimization. Before applying it, make sure your program does have the RAM consumption problem related to having a massive number of similar objects in memory at the same time. Make sure that this problem can’t be solved in any other meaningful way.
- The **Flyweight** class contains the portion of the original object’s state that can be shared between multiple objects. The same flyweight object can be used in many different contexts. The state stored inside a flyweight is called intrinsic. The state passed to the flyweight’s methods is called extrinsic.
- The **Context** class contains the extrinsic state, unique across all original objects. When a context is paired with one of the flyweight objects, it represents the full state of the original object.
- Usually, the behavior of the original object remains in the flyweight class. In this case, whoever calls a flyweight’s method must also pass appropriate bits of the extrinsic state into the method’s parameters. On the other hand, the behavior can be moved to the context class, which would use the linked flyweight merely as a data object.
- The **Client** calculates or stores the extrinsic state of flyweights. From the client’s perspective, a flyweight is a template object which can be configured at runtime by passing some contextual data into parameters of its methods.
- The **Flyweight Factory** manages a pool of existing flyweights. With the factory, clients don’t create flyweights directly. Instead, they call the factory, passing it bits of the intrinsic state of the desired flyweight. The factory looks over previously created flyweights and either returns an existing one that matches search criteria or creates a new one if nothing is found.

[Code Example](./assets/docs/code/flyweight.md)

## Proxy
Provide a surrogate or placeholder for another object to control access to it.

![Proxy](./assets/images/design-patterns/proxy.png)

- The **Service Interface** declares the interface of the Service. The proxy must follow this interface to be able to disguise itself as a service object.
- The **Service** is a class that provides some useful business logic.
- The **Proxy** class has a reference field that points to a service object. After the proxy finishes its processing (e.g., lazy initialization, logging, access control, caching, etc.), it passes the request to the service object. Usually, proxies manage the full lifecycle of their service objects.
- The **Client** should work with both services and proxies via the same interface. This way you can pass a proxy into any code that expects a service object.

[Code Example](./assets/docs/code/proxy.md)


# Behavioral Patterns
Following is a list of patterns for how objects communicate with each other and distribute responsibility. Behavioral Class patterns use inheritance to describe algorithms and flow of control, while Behavioral object patterns describe how objects cooperate to perform tasks that aren't done by one object alone.

## Chain of Responsibility
Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

![Chain of Responsibility](./assets/images/design-patterns/chain-of-responsibility.png)

- The **Handler** declares the interface, common for all concrete handlers. It usually contains just a single method for handling requests, but sometimes it may also have another method for setting the next handler on the chain.
- The **Base Handler** is an optional class where you can put the boilerplate code that’s common to all handler classes. Usually, this class defines a field for storing a reference to the next handler. The clients can build a chain by passing a handler to the constructor or setter of the previous handler. The class may also implement the default handling behavior: it can pass execution to the next handler after checking for its existence.
- **Concrete Handlers** contain the actual code for processing requests. Upon receiving a request, each handler must decide whether to process it and, additionally, whether to pass it along the chain. Handlers are usually self-contained and immutable, accepting all necessary data just once via the constructor.
- The **Client** may compose chains just once or compose them dynamically, depending on the application’s logic. Note that a request can be sent to any handler in the chain—it doesn’t have to be the first one.

> Chain of Responsibility is often used in conjunction with Composite. In this case, when a leaf component gets a request, it may pass it through the chain of all of the parent components down to the root of the object tree.

[Code Example](./assets/docs/code/chain-of-responsibility.md)

## Command
Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

![Command](./assets/images/design-patterns/command.png)

- The **Sender** class (aka invoker) is responsible for initiating requests. This class must have a field for storing a reference to a command object. The sender triggers that command instead of sending the request directly to the receiver. Note that the sender isn’t responsible for creating the command object. Usually, it gets a pre-created command from the client via the constructor.
- The **Command** interface usually declares just a single method for executing the command.
- **Concrete Commands** implement various kinds of requests. A concrete command isn’t supposed to perform the work on its own, but rather to pass the call to one of the business logic objects. However, for the sake of simplifying the code, these classes can be merged. Parameters required to execute a method on a receiving object can be declared as fields in the concrete command. You can make command objects immutable by only allowing the initialization of these fields via the constructor.
- The **Receiver** class contains some business logic. Almost any object may act as a receiver. Most commands only handle the details of how a request is passed to the receiver, while the receiver itself does the actual work.
- The **Client** creates and configures concrete command objects. The client must pass all of the request parameters, including a receiver instance, into the command’s constructor. After that, the resulting command may be associated with one or multiple senders.

[Code Example](./assets/docs/code/command.md)

## Iterator
Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

![Iterator](./assets/images/design-patterns/iterator.png)

- The **Iterator** interface declares the operations required for traversing a collection: fetching the next element, retrieving the current position, restarting iteration, etc.
- **Concrete Iterators** implement specific algorithms for traversing a collection. The iterator object should track the traversal progress on its own. This allows several iterators to traverse the same collection independently of each other.
- The **Collection** interface declares one or multiple methods for getting iterators compatible with the collection. Note that the return type of the methods must be declared as the iterator interface so that the concrete collections can return various kinds of iterators.
- **Concrete Collections** return new instances of a particular concrete iterator class each time the client requests one. You might be wondering, where’s the rest of the collection’s code? Don’t worry, it should be in the same class. It’s just that these details aren’t crucial to the actual pattern, so we’re omitting them.
- The **Client** works with both collections and iterators via their interfaces. This way the client isn’t coupled to concrete classes, allowing you to use various collections and iterators with the same client code. Typically, clients don’t create iterators on their own, but instead get them from collections. Yet, in certain cases, the client can create one directly; for example, when the client defines its own special iterator.

[Code Example](./assets/docs/code/iterator.md)

## Mediator
Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

![Mediator](./assets/images/design-patterns/mediator.png)

- **Components** are various classes that contain some business logic. Each component has a reference to a mediator, declared with the type of the mediator interface. The component isn’t aware of the actual class of the mediator, so you can reuse the component in other programs by linking it to a different mediator.
- The **Mediator** interface declares methods of communication with components, which usually include just a single notification method. Components may pass any context as arguments of this method, including their own objects, but only in such a way that no coupling occurs between a receiving component and the sender’s class.
- **Concrete Mediators** encapsulate relations between various components. Concrete mediators often keep references to all components they manage and sometimes even manage their lifecycle.
- Components must not be aware of other components. If something important happens within or to a component, it must only notify the mediator. When the mediator receives the notification, it can easily identify the sender, which might be just enough to decide what component should be triggered in return. From a component’s perspective, it all looks like a total black box. The sender doesn’t know who’ll end up handling its request, and the receiver doesn’t know who sent the request in the first place.

[Code Example](./assets/docs/code/mediator.md)

## Memento
Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.

### Implementing based on nested classes

![Memento Nested Classes](./assets/images/design-patterns/memento-with-nested-classes.png)

- The **Originator** class can produce snapshots of its own state, as well as restore its state from snapshots when needed.
- The **Memento** is a value object that acts as a snapshot of the originator’s state. It’s a common practice to make the memento immutable and pass it the data only once, via the constructor.
- The **Caretaker** knows not only “when” and “why” to capture the originator’s state, but also when the state should be restored. A caretaker can keep track of the originator’s history by storing a stack of mementos. When the originator has to travel back in history, the caretaker fetches the topmost memento from the stack and passes it to the originator’s restoration method.
- In this implementation, the memento class is nested inside the originator. This lets the originator access the fields and methods of the memento, even though they’re declared private. On the other hand, the caretaker has very limited access to the memento’s fields and methods, which lets it store mementos in a stack but not tamper with their state.

### Implementing with strict encapsulation

![Memento Strict Encapsulation](./assets/images/design-patterns/memento-with-strict-encapsulation.png)

- This implementation allows having multiple types of originators and mementos. Each originator works with a corresponding memento class. Neither originators nor mementos expose their state to anyone.
- Caretakers are now explicitly restricted from changing the state stored in mementos. Moreover, the caretaker class becomes independent from the originator because the restoration method is now defined in the memento class.
- Each memento becomes linked to the originator that produced it. The originator passes itself to the memento’s constructor, along with the values of its state. Thanks to the close relationship between these classes, a memento can restore the state of its originator, given that the latter has defined the appropriate setters.

[Code Example](./assets/docs/code/memento.md)

## Observer
Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

![Observer](./assets/images/design-patterns/observer.png)

- The **Publisher** issues events of interest to other objects. These events occur when the publisher changes its state or executes some behaviors. Publishers contain a subscription infrastructure that lets new subscribers join and current subscribers leave the list.
- When a new event happens, the publisher goes over the subscription list and calls the notification method declared in the subscriber interface on each subscriber object.
- The **Subscriber** interface declares the notification interface. In most cases, it consists of a single update method. The method may have several parameters that let the publisher pass some event details along with the update.
- **Concrete Subscribers** perform some actions in response to notifications issued by the publisher. All of these classes must implement the same interface so the publisher isn’t coupled to concrete classes.
- Usually, subscribers need some contextual information to handle the update correctly. For this reason, publishers often pass some context data as arguments of the notification method. The publisher can pass itself as an argument, letting subscriber fetch any required data directly.
- The **Client** creates publisher and subscriber objects separately and then registers subscribers for publisher updates.

[Code Example](./assets/docs/code/observer.md)

## State
Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

![State](./assets/images/design-patterns/state.png)

- **Context** stores a reference to one of the concrete state objects and delegates to it all state-specific work. The context communicates with the state object via the state interface. The context exposes a setter for passing it a new state object.
- The **State** interface declares the state-specific methods. These methods should make sense for all concrete states because you don’t want some of your states to have useless methods that will never be called.
- **Concrete States** provide their own implementations for the state-specific methods. To avoid duplication of similar code across multiple states, you may provide intermediate abstract classes that encapsulate some common behavior. State objects may store a backreference to the context object. Through this reference, the state can fetch any required info from the context object, as well as initiate state transitions.
- Both context and concrete states can set the next state of the context and perform the actual state transition by replacing the state object linked to the context.

[Code Example](./assets/docs/code/state.md)

## Strategy
Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

Use the Strategy pattern when:
- You want to use different variants of an algorithm within an object and be able to switch from one algorithm to another during runtime.
- You have a lot of similar classes that only differ in the way they execute some behavior.
- To isolate the business logic of a class from the implementation details of algorithms that may not be as important in the context of that logic.
- Your class has a massive conditional operator that switches between different variants of the same algorithm.

![Strategy](./assets/images/design-patterns/strategy.png)

- The **Context** maintains a reference to one of the concrete strategies and communicates with this object only via the strategy interface.
- The **Strategy** interface is common to all concrete strategies. It declares a method the context uses to execute a strategy.
- **Concrete Strategies** implement different variations of an algorithm the context uses.
- The context calls the execution method on the linked strategy object each time it needs to run the algorithm. The context doesn’t know what type of strategy it works with or how the algorithm is executed.
- The **Client** creates a specific strategy object and passes it to the context. The context exposes a setter which lets clients replace the strategy associated with the context at runtime.

[Code Example](./assets/docs/code/strategy.md)

## Template Method
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

![Template Method](./assets/images/design-patterns/template-method.png)

- The **Abstract Class** declares methods that act as steps of an algorithm, as well as the actual template method which calls these methods in a specific order. The steps may either be declared abstract or have some default implementation.
- **Concrete Classes** can override all of the steps, but not the template method itself.

[Code Example](./assets/docs/code/template-method.md)

## Visitor
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

Use the Visitor pattern when:
- You need to perform an operation on all elements of a complex object structure, E.g. An object tree with different types of objects on each branch.
- To clean up business logic of auxiliary behaviors. The visitor pattern makes classes more focused on their roles and extract other behaviors into a set of visitor classes.
- A behavior makes sense only in some classes of a class hierarchy, but not in others. We can exxtract behavior into separate visitor classes and implement only those visiting methods that accept objects of relevant classes, leaving the rest empty.

![Visitor](./assets/images/design-patterns/visitor.png)

- The **Visitor** interface declares a set of visiting methods that can take concrete elements of an object structure as arguments. These methods may have the same names if the program is written in a language that supports overloading, but the type of their parameters must be different.
- Each **Concrete Visitor** implements several versions of the same behaviors, tailored for different concrete element classes.
- The **Element** interface declares a method for “accepting” visitors. This method should have one parameter declared with the type of the visitor interface.
- Each **Concrete Element** must implement the acceptance method. The purpose of this method is to redirect the call to the proper visitor’s method corresponding to the current element class. Be aware that even if a base element class implements this method, all subclasses must still override this method in their own classes and call the appropriate method on the visitor object.
- The **Client** usually represents a collection or some other complex object (for example, a [Composite](#composite) tree). Usually, clients aren’t aware of all the concrete element classes because they work with objects from that collection via some abstract interface.

[Code Example](./assets/docs/code/visitor.md)
