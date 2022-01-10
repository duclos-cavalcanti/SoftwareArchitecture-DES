# Software Architecture for Distributed Embedded Systems
This is a summary and compilation of information provided by a Masters course at the
Technical University of Munich. This is offered by the 
[Embedded Systems and Internet of Things](https://www.ei.tum.de/en/esi/home/) chair and
was such a pleasure that I wished to transform the material into a repository for future
referral.

All the source code examples are taken from [this](https://sourcemaking.com/)
 amazing site and are not made by me. Please check them out and give them their props!

## Chapter 1: Introduction
### Patterns
A pattern is the reusable form of a solution to a problem.

`Architecture` patterns help us to understand on a high abstraction level, a complex
software system that can be composed of interacting components.

`Design` patterns help us to implement a software system on a more detailed level using
established approaches, where the mechanics of the implementation are broken down to a
components mechanics level.

### OOP
"A-PIE"
- Abstraction
- Polymorphism
- Inheritance
- Encapsulation

### UML
The unified modeling language is an effort to standardize the definition of a software and
system architectures.

Defines thirteen different types of diagrams. Four important ones that represent different
types of interactions:

- **Structure Diagrams**, which includes the **Class Diagram**
- **Behavior Diagrams**
- **Interaction Diagrams**, which includes the **Sequence Diagram**

## Chapter 2: GoF Patterns: Intro and Structural
### Design Pattern
A design pattern is a general repeatable solution to a commonly occurring problem in
software design.

According to the GoF, there are three types of Patterns:
- `Structural patterns`
    - These are Design Patterns that ease the design by identifying a simple way to
      realize relationships between entities. They are mostly concerned with providing interfaces in a
      suitable form.
- `Behavioral patterns`
    - These are design patterns that identify common communication patterns
      between objects and realize these patterns. By doing so, these patterns increase flexibility in
      carrying out this communication.
- `Creational patterns`
    - These are design patterns that deal with object
      creation mechanisms, trying to create objects in a manner suitable to the situation. The basic form
      of object creation could result in design problems or added complexity to the design. Creational
      design patterns solve this problem by controlling this object creation.

### Structural Patterns
Structural design patterns all deal with enhancing the use of interfaces to achieve certain
improvements in software architecture.

Chosen Examples: Adapter, Bridge and Proxy
#### 1. Adapter (AKA Wrapper) (~Handle-Body Idiom)
* **Summary**: Match interfaces of different classes.
* **Problem**: An "off the shelf" component offers compelling functionality that you
  would like to reuse, but its "view of the world" is not compatible with
  the philosophy and architecture of the system currently being
  developed.

* Consequences
    * `Object Adapter`: Lets a single Adapter work with many Adaptees
    * `Object Adapter`: Adapter may add functionalities to all Adaptees at once
    * `Object Adapter`: Makes it harder to override Adaptee behavior
    * `Class Adapter`: Adapts Adaptee to Target by committing to a concrete Adaptee class.
    * `Class Adapter`: Won't work when we want to adapt a class and all its subclasses.
    * `Class Adapter`: Lets Adapter override some of Adaptee's behavior.
    * `Class Adapter`: Introduces only one object, and no additional pointer indirection.

* **Intent**:
    * Convert the interface of a class into another interface clients expect. 
    * Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
    * Wrap an existing class with a new interface.
    * “Impedance match” an old component to a new system.

* **Types**: Object Adapters vs Class Adapters

See more [here](https://sourcemaking.com/design_patterns/adapter).

#### 2. Bridge
* **Summary**: Separates an object's interface from its implementation. (Handle-Body Idiom)
* **Problem**:
    * When an abstraction can have one of several possible implementations, the usual way to
      accommodate them is to use inheritance.
    * An abstract class defines the interface to the abstraction, and concrete subclasses implement it in
      different ways.
    * But this approach isn't always flexible enough: Inheritance binds an implementation to the abstraction
      permanently, which makes it difficult to modify, extend, and reuse abstractions and implementations
      independently.
    * Locks in compile-time binding between interface and implementation.
    * The abstraction and implementation cannot be independently extended or composed.

* **Intent**:
    * Decouple an abstraction from its implementation so that the two can vary independently.
    * Publish interface in an inheritance hierarchy, and bury implementation in its own inheritance hierarchy.
    * Beyond encapsulation, to insulation.

* **Relations to other Patterns**:
    * Adapter makes things work after they're designed; Bridge makes them work before they are.
    * Bridge is designed up-front to let the abstraction and the implementation vary independently while
      Adapter is retrofitted to make unrelated classes work together.

See more [here](https://sourcemaking.com/design_patterns/bridge).

#### 3. Proxy
* **Summary**: An object representing another object.
* **Problem**: You need to support resource-hungry objects, and you do not want to 
               instantiate such objects unless and until they are actually requested by the client.

* **Intent**:
    * Provide a surrogate or placeholder for another object to control access to it.
    * Use an extra level of indirection to support distributed, controlled, or intelligent access.
    * Add a wrapper and delegation to protect the real component from undue complexity

* **Types**: Virtual, Remote, Protective, Smart

* **Relations to other Patterns**:
    * An adapter provides a different interface to the object it adapts.
    * By contrast, a proxy provides the same interface as its subject.
    * However, a proxy used for access protection might refuse to perform an operation that the subject will
      perform, so its interface may be effectively a subset of the subject's.

See more [here](https://sourcemaking.com/design_patterns/proxy).

## Chapter 3: GoF Patterns: Behavioral
### Behavioral Patterns
Behavioral patterns are concerned with algorithms and the assignment of
responsibilities between objects.  They describe not just patterns of 
objects or classes but also the patterns of communication between them.

These patterns characterize complex control flow that's difficult to follow at run-time.
They shift your focus away from flow of control to let you concentrate just on the way
objects are interconnected.

Chosen Examples: Observer, Strategy and Memento

#### 1. Observer (AKA Dependants, Publish-Subscribe)
* **Summary**: A way of notifying change to a number of classes. (part of the Model-View Controller)
* **Problem**: A large monolithic design does not scale well as new graphing or 
               monitoring requirements are levied.

* **Intent**:
    * Define a one-to-many dependency between objects so that when one object changes state, all its
      dependents are notified and updated automatically.
    * Encapsulate the core (or common or engine) components in a Subject abstraction, and the variable
      (or optional or user interface) components in an Observer hierarchy.

* **Applicability**:
    * When an abstraction has two aspects, one dependent on the other.
    * Encapsulating these aspects in separate objects lets you vary and reuse them independently.
    * When a change to one object requires changing others, and you don't know how many objects need
      to be changed.
    * When an object should be able to notify other objects without making assumptions about who these
      objects are.
    * In other words, you don't want these objects tightly coupled.

* Consequences
    * needs event compression to be implemented
    * has a single Observer sometimes monitoring multiple Subjects
    * Observers may be blind to costs of changing/updating Subjects

* **Types**: Publish-Subscribe, Original GoF
* **Relations to other Patterns**:
    * Chain of Responsibility, Command, Mediator, and Observer address how you can decouple senders
      and receivers, but with different trade-offs
    * Chain of Responsibility passes a sender request along a chain of potential receivers.
    * Command normally specifies a sender-receiver connection with a subclass.
    * Mediator has senders and receivers reference each other indirectly.

See more [here](https://sourcemaking.com/design_patterns/observer).

#### 2. Memento (AKA Token)
* **Summary**: Capture and restore an object's internal state.
* **Problem**: The need to restore an object back to its previous state 
               (e.g. "undo" or "rollback" operations).

* **Intent**:
    * Without violating encapsulation, capture and externalize an object's internal state so that the object
      can be returned to this state later.
    * A magic cookie that encapsulates a "check point" capability.
    * Promote undo or rollback to full object status.

* **Applicability**:
    * Use the Memento pattern when
    * a snapshot of (some portion of) an object's state must be saved so that it can be restored to that
      state later, and
    * a direct interface to obtaining the state would expose implementation details and break the object's
      encapsulation.
    * Can implement undo and redo capabilities with use of a stack of Command objects and
      a stack of Memento objects.

* Consequences
    * Preserve encapsulation boundaries
    * Using mementos might be expensive
    * Defining narrow and wide interfaces
    * Hidden costs in caring for mementos

* **Relations to other Patterns**:
    * Command and Memento act as magic tokens to be passed around and invoked at a later time. 
    * Polymorphism is important to Command, but not to Memento because its interface is so narrow that a
      memento can only be passed as a value.
    * Command can use Memento to maintain the state required for an undo operation.
    * Memento is often used in conjunction with Iterator. 
      An Iterator can use a Memento to capture the state
      of an iteration. The Iterator stores the Memento internally.

See more [here](https://sourcemaking.com/design_patterns/memento).

#### 3. Strategy
* **Summary**: Encapsulates an algorithm inside a class.
* **Problem**: 
    * One of the dominant strategies of objectoriented design is the "open-closed
      principle".
    * Program to an interface, not an implementation!

* **Intent**:
    * Define a family of algorithms, encapsulate each one, and make them interchangeable.
    * Strategy lets the algorithm vary independently from the clients that use it.
    * Capture the abstraction in an interface, bury implementation details in derived classes.

* **Applicability**:
    * Use the Memento pattern when
    * a snapshot of (some portion of) an object's state must be saved so that it can be restored to that
      state later, and
    * a direct interface to obtaining the state would expose implementation details and break the object's
      encapsulation.
    * Can implement undo and redo capabilities with use of a stack of Command objects and
      a stack of Memento objects.

* Consequences
    * Preserve encapsulation boundaries
    * Using mementos might be expensive
    * Defining narrow and wide interfaces
    * Hidden costs in caring for mementos

* **Relations to other Patterns**:
    * Strategy is like Template Method except in its granularity.
    * State is like Strategy except in its intent.
    * Strategy lets you change the guts of an object. Decorator lets you change the skin.
    * State, Strategy, Bridge (and to some degree Adapter) have similar solution structures. They all share
      elements of the 'handle/body' idiom. They differ in intent - that is, they solve different problems.
    * Strategy has 2 different implementations, the first is similar to State. The difference is in binding times
      (Strategy is a bind-once pattern, whereas State is more dynamic).
    * Strategy objects often make good Flyweights.

See more [here](https://sourcemaking.com/design_patterns/strategy).
