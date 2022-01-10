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
#### 1. Adapter (AKA Wrapper)
* **Summary**: Match interfaces of different classes.
* **Problem**: An "off the shelf" component offers compelling functionality that you
  would like to reuse, but its "view of the world" is not compatible with
  the philosophy and architecture of the system currently being
  developed.

* **Intent**:
    * Convert the interface of a class into another interface clients expect. 
    * Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
    * Wrap an existing class with a new interface.
    * “Impedance match” an old component to a new system.

* **Types**: Object Adapters vs Class Adapters

See more [here](https://sourcemaking.com/design_patterns/adapter).

#### 2. Bridge
* **Summary**: Separates an object's interface from its implementation.
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
    * Adapter makes things work after they're designed; Bridge makes them work before they are.
    * Bridge is designed up-front to let the abstraction and the implementation vary independently while
      Adapter is retrofitted to make unrelated classes work together.

See more [here](https://sourcemaking.com/design_patterns/proxy).
