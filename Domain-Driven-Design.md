# Introduction

- For most software projects, the primary focus should be on the domain and domain logic
- Complex domain designs should be based on a model

Xtreme Programming is was the most promiment agile process at the time, it rebelled against the burdens of projects with useless static documents and obsessive amount of upfront planning. It followed with the design philosphy to use "the simplest thing that can work"
Minimalism that was refreshing in the midst of all the domain driven designers

There are two key concepts to apply domain driven design

1. Development is iterative
2. Developers and domain experts have a close relationship

# Overview
  
Domain Driven Design offers an abstraction to the messiness of software design. It offers enough information to serve a particular purpose, much like a movie showing only the important scenes and cutting out the regular unedited real life.
  
## Ingredients for effective modeling
  
1. Binding the model and the implementation (and maintained through all subsequent iterations)
2. Cultivating a language based on the model
3. Developing a knowledge-rich model
4. Distilling the model
5. Brainstorming and experimenting

Use of diagrams must educate developers what's pertinent to the domain, without overloading it with technical jargon that would not appear in code.

> If the design, or some central part of it, does not map to the domain model, that model is of little value, and the correctness of the software is suspect. At the same time, complex mapings between models and design functions are difficult to understand and, in practice, impossible to maintain as the design changes.

> The model is the backbone of a language when tackling complex domains. Commiting to exercising that language in diagrams, writing and even speech.

# Modeling

> Any technical person contributing to the model must spend some time touching the code, whatever primary role he or she plays on the project. Anyone responsible for changing code must learn to express model through the code. Every developer must be involved in some level of discussion about the model and have contact with domain experts. Those who contribute in different ways must consciously engage those who touch the code in a dynamic exchange of model ideas through the UBIQUITOUS LANGUAGE.

Complex applications should be kept in a Layered Architecture.
Each layer must be cohesive and depends only on the layers below.

![Layered Architecture](assets/images/domain-driven-design/layered-architecture.png)

Most code related to the domain model is isolated to one layer and must be free from the UI, application or infrastructure code.  
This will alow the model to become rich and clear enough to capture essential business knowledge.

## Smart UI "Anti Pattern"

A common anti-pattern is known as Smart UI.  
This is done by putting all the business logic into the user interface. Chopping the application into small functions and implmenet them as separate user interfaces, and embedding business rules into them.  

This has some advantages such as higher productivity and has a much lower barrier to entry for the codebase, however developers would find difficulty of integrations of applications aside from the database.  

Another problem is that there is no reuse of behavior or abstraction of the business problem. Leading to dupliated rules in each operation in which they apply.

# Models Expressed in Software

There are three patterns of models;

1. Entities
2. Value Objects
3. Services

Entities represent objects with some form of continuity and identity, tracked through different states and even across implementations.  
Value Objects describes a state of some other object.  
Services offer a way to express as actions or operations to be done for a client on request.  

## Entities (Reference Objects)

Some objects are not defined primarily by their attributes. They represent a thread of identity that runs through time and often across distinct representations.   
Sometimes such an object must be matched with another object even though attributes differ. An object must be distinguished from other objects even though they might have the same attributes. Mistaken identity can lead to data corruption.

## Value Objects

Value objects represent a descriptive aspect of the domain with no conceptual identity.  
They are instantiated to represent elements of the design that we care about only for what they are, not who or which they are.  
(Basically anything that isn't pertinent to the application's domain, simply used and discarded or plain ol' objects)

> Treat Value Objects as immutable. Don't give it any identity and avoid the design complexity necessary to maintain Entities

There are considerations to making Value Objects mutable, such as if it changes frequently, or object creation or deletion is expensive. Then these values must not be shared to other entities in order to simplify implementations.  

When associating Value Objects and entities, try to keep assocations to the minimum as they can be hard to maintain. Another case is having bidirectional assocations between two Value Objects should never happen, and if it seems necessary, perhaps there is an identity that hasn't been explicity recognized yet.  

## Services  

A Service is an operation offered as an interface that stands alone in the model, without encapsulating state, as Entities and Value Objects do. They represent an activity or a verb, that would otherwise be an unnatural responsibility for an Entity or Value Object.  
E.g. A service that emails a user when their bank balance falls below a threshold.

A good service has three characteristics;  

1. The operation relates to a domain concept that is not a natural part of an Entity or Value Object.
2. The interface is defined in terms of other elements of the domain model.
3. The operation is stateless.

## Modules

Modules tell a story of the system and contain a choesive set of concepts.  
This often yields low coupling between Modules, but if it doesn't, look for a way to change the model to disentangle the concepts, or search for an overlooked concept that mightb e the basis of a Module that would bring the elements together in a meaningful way.  
Seek low coupling in the sense of concepts that can be understood and reasoned about independently of each other. Refine the model until partitions according to high-level domain concepts and the corresponding code is decoupled as well.  

## Agile Modules

Modules need to coevolve with the model. Early mistakes leads to high coupling and difficult refactors.  

## Pitfalls of Infrastructure Driven Packaging

Many frameworks come with their own methods of bundling packages, such as the enforcement of Layered Architecture. However, knowing to resist them is just as important if it will skew the meaning of the package.   
E.g: Each object broken into four tiers (Interface, persistence layer that handles mapping, application specific functionality layer, etc.).   
Some languages require importing all these modules separately, leading writers to believe they are separate when they are co-dependant. Finding the data and behavior that defined one class takes a lot of mental effort.

## Sticking With Model Driven Design When Mixing Paradigms

When mixing non-object elements (E.g. Model Paradigms) into a predominatly object-oriented system;

1. Don't fight the implementation paradigm; There's always another way to think about a domain. Find model concepts that fit the paradigm.
2. Lean on the ubiquitous language; Even when there is no rigorous connection between tools, very consistent use of langauge can keep parts of the design from diverging.
3. Don't get hung up on UML; Sometimes the fixation of a tool, like UML diagramming, leads people to distort the model to fit what can easily be drawn.
4. Be skeptical; Is the tool really pulling its weight? Just because you have some rules, that doesn't necessarily mean you need the overhead of a rules engine. Rules can be expressed as objects. perhaps a little less neatly; multiple paradigms complicate matters enourmously.

Before mixing a new paradigm, the dominant paradigm must be exhausted.

# Life Cycle of a Domain Object

## Aggregates

Aggregates are a collection of entites. There is one root entity that is called from the outside appilcation and acts as an interface, a global identity.
E.g. Car entity has wheel and tire entities. Car is the root entity and anything outside the aggregate boundry can't access the inside entities.
This acts as a way to define boundries.

## Factories

When creation of an aggregate becomes to complicated, Factories provide encapsulation.  

The two basic requirements for any good Factory are;

1 . Each creation method is atomic and enforces all invariants of the created object or Aggregate. A Factory should only be able to produce an object in a consistent state. For an Entity, this means the creation of the entire Aggregate, with all invariants satisfied, but probably with optional elements still to be added. For an immutable Value Object, this means that all attributes are initialized to their correct final state. If the interface makes it possible to request an object that can’t be created correctly, then an exception should be raised or some other mechanism should be invoked that will ensure that no improper return value is possible.
2. The Factory should be abstracted to the type desired, rather than the concrete class(es) created.

### When a Constructor Is All You Need

Avoid calling constructors within constructors of other classes. Constructors should be dead simple. Complex assemblies, especially of Aggregates, call for Factories. The threshold for choosing to use a little Factory method isn’t high.  

### Designing the Interface

Keep in mind these two points;

- Each operation must be atomic: You have to pass in everything needed to create a complete product in a single interaction with the Factory. You also have to decide what will happen if creation fails, in the event that some invariant isn’t satisfied. You could throw an exception or just return a null. To be consistent, consider adopting a coding standard for failures in Factories.

- The Factory will be coupled to its arguments: If you are not careful in your selection of input parameters, you can create a rat’s nest of dependencies. The degree of coupling will depend on what you do with the argument. If it is simply plugged into the product, you’ve created a modest dependency. If you are picking parts out of the argument to use in the construction, the coupling gets tighter.

## Repositories

A client needs a practical means of acquiring references to preexisting domain objects.  
If the infrastructure makes it easy to do so, the developers of the client may add more traversable associations, muddling the model.  
On the other hand, they may use queries to pull the exact data they need from the database, or to pull a few specific objects rather than navigating from Aggregate roots.  
Domain logic moves into queries and client code, and the Entities and Value Objects become mere data containers.  
The sheer technical complexity of applying most database access infrastructure quickly swamps the client code, which leads developers to dumb down the domain layer, which makes the model irrelevant.  

A Repository represents all objects of a certain type as a conceptual set (usually emulated).  
It acts like a collection, except with more elaborate querying capability. Objects of the appropriate type are added and removed, and the machinery behind the Repository inserts them or deletes them from the database.  
This definition gathers a cohesive set of responsibilities for providing access to the roots of Aggregate from early life cycle through the end.  

![Repository performing a search for client](assets/images/domain-driven-design/repository-search-for-client.png)

### Advantages of Repositories:

- They present clients with a simple model for obtaining persistent objects and managing their life cycle.
- They decouple application and domain design from persistence technology, multiple database strategies, or even multiple data sources.
- They communicate design decisions about object access.
- They allow easy substitution of a dummy implementation, for use in testing (typically using an in- memory collection).

# TODO: Research further into later. (Currently not relevant)

# Using the Language: An Extended Example

In order to implement a domain driven model to an existing application, we would do as follows;

## Isolate the Domain

To prevent responsibilties being mixed, we apply the layered archiecture to mark off a domain layer.
E.g. A cargo management system would have;

1. A Tracking Query that can access past and present handling of a particular Cargo
2. A Booking Application that allows a new Cargo to be registered and prepares the system for it
3. An Incident Logging Application that can record each handling of the Cargo (providing the information that is found by the Tracking Query)

## Distinguish Entities and Value Objects

Anything not interchangeable is an Entity

E.g. Customers, Cargo, Handling Events, Delivery History and Carrier Movement.

Otherwise they are treated as Value Objects;

E.g. Deliery Specificiation, Roles, etc.

Below is a distiction of problematic assocations;

![Cargo Assocation Example](assets/images/domain-driven-design/cargo-association-example.png)

## Aggregate Boundries

![Cargo Aggregate Boundries](assets/images/domain-driven-design/cargo-aggregate-boundries.png)

## Selecting Repositories

![Cargo Selecting Repositories](assets/images/domain-driven-design/cargo-repositories.png)

## Modules in the Shipping Model

The following diagram is a variation of an infrastructure-driven packaging problem when grouped in a pattern that doesn't convey the application story;

![Cargo Infrastructure Driven Diagram](assets/images/domain-driven-design/cargo-bad-diagram.png)

While a domain driven one is more straight-forward;

![Cargo Domain Driven Diagram](assets/images/domain-driven-design/cargo-good-diagram.png)

# TODO: Look into Anti Corruption Layer, and Enterprise Segments

# Refactoring Toward Deeper Insight

Developing useful models successfully has three points;

1. Sophisticated domain models are achievable and worth the trouble.
2. They are seldom developed except through an iterative process of refactoring, including close involvement of the domain experts with developers interested in learning about the domain.
3. They may call for sophisticated design skills to implement and to use effectively.

## Levels of Refactoring

Refactoring is making continuous, small design changes that do not change functionality.  
Technical refactoring focuses on mechanical changes to make code more readable, or enhance at a detailed level.  
Refactoring to patterns are opportunities to apply established design patterns.  

Refactoring based on domain is not only micro refactors, but toward an insightful model.

## Opportunties

When a breakthrough to a deeper model emerges, it has higher opportunity and risk, and may be at an inopportune time, but is important for progress.

## Focus on Basics

Rather than trying to bring a breakthrough, the possibility comes after many refactorings. Emerging after each successful refinement.

# Making Implicit Concepts Explicit

## Digging Out Concepts

> Listen to the language the domain experts use. Are there terms that succinctly state something complicated? Are they correcting your word choice (perhaps diplomatically)? Do the puzzled looks on their faces go away when you use a particular phrase? These are hints of a concept that might benefit the model.

These concepts may not always be `nouns as objects`. When the users or domain experts use vocabulary that is nowhere in the design, that is a warning sign. It is a doubly strong warning when both the developers and the domain experts are using terms that are not in the design.

## Scrutinize Awkwardness

Sometimes we may not find these concepts easily, so we need to dig in awkward parts of our design, procedures that do complicated things that are hard to explain, or where new requirements add complexity.  
Sometimes it can be hard to recognize that there even is a missing concept. You may have objects doing all the work but find some of the responsibilities awkward. Or, if you do realize something is missing, a model solution may elude you.  

## Contemplate Contradictions

Different domain experts see things different ways based on their experience and needs. Even the same person provides information that is logically inconsistent after careful analysis.  
Such pesky contradictions, which we encounter all the time when digging into program requirements, can be great clues to deeper models. Some are just variations in terminology or are based on misunderstanding. But there is a residue where two factual statements by experts seem to contradict.  

> Reading a book about the domain subject can help grasp fundamental concepts that can enrich your model.

>  Experimentation is the way to learn what works and doesn’t. Trying to avoid missteps in design will result in a lower quality result because it will be based on less experience. And it can easily take longer than a series of quick experiments.

## Modeling Less Obvious Concepts

The object-oriented paradigm leads us to look for and invent certain kinds of concepts. Things, even very abstract ones, are the meat of most object models, along with the actions those things take. These are the “nouns and verbs” that introductory object-oriented design books talk about. But other important categories of concepts can be made explicit in a model as well.

### Explicit Constraints

Concepts can appear implicitly. E.g A bucket can only handle up to its capacity.  
Expressing it explicitly can make this more obvious rather than being buried as classes get more complicated.  

```java
// Not explicit

class Bucket {
   private float capacity;
   private float contents;
   public void pourIn(float addedVolume) {
      if (contents + addedVolume > capacity) {
         contents = capacity;
      } else {
         contents = contents + addedVolume;
      }
} }

// Explicit
class Bucket {
   private float capacity;
   private float contents;
   public void pourIn(float addedVolume) {
      float volumePresent = contents + addedVolume;
      contents = constrainedToCapacity(volumePresent);
   }
   private float constrainedToCapacity(float volumePlacedIn) {
      if (volumePlacedIn > capacity) return capacity;
      return volumePlacedIn;
   } 
}
```

This separate method gives the constraint some room to grow, but there are lots of cases when a constraint just can’t fit comfortably in a single method.  
Or even if the method stays simple, it may call on information that the object doesn’t need for its primary responsibility.  

Here are some warning signs that a constraint is distorting the design of its host object.  
- Evaluating a constraint requires data that does not otherwise fit the object’s definition.
- Related rules appear in multiple objects, forcing duplication or inheritance between objects that are not otherwise a family.
- A lot of design and requirements conversation revolves around the constraints, but in the implementation, they are hidden away in procedural code.

> When the constraints are obscuring the object’s basic responsibility, or when the constraint is prominent in the domain yet not prominent in the model, you can factor it out into an explicit object or even model it as a set of objects and relationships.

### Processes as Domain Objects

Procedures should not be the prominent aspect of our models. Objects are meant to encapsulate the procedures and let us think about their goals or intentions instead.  
A Service is one way of expressing a process explicitly, while encapsulating complex algorithms.

When there is more than one way to carry out a process, another approach is to make the algorithm itself, or some key part of it, an object in its own right. The choice between processes becomes a choice between these objects, each of which represents a different Strategy.

### Specification

A Specification states a constraint on the state of another object, which may or may not be present. It has multiple uses, but one that conveys the most basic concept is that a Specification can test any object to see if it satisfies the specified criteria.

> Create explicit predicate-like VALUE OBJECTS for specialized purposes. A SPECIFICATION is a predicate that determines if an object does or does not satisfy some criteria.

Uses for Specification objects.
- To validate an object to see if it fulfills some need or is ready for some purpose
- To select an object from a collection (as in the case of querying for overdue invoices) 
- To specify the creation of a new object to fit some need

![Specification Pattern](assets/images/domain-driven-design/specification-pattern.png)

### More information on Applying and Implementing SPECIFICATION in Page 169 of DDD

# Supple Design
