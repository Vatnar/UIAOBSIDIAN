#### Main UML specification 
 - Superstructure
	 - Defines the UML elements (diagram, etc.)
- Infrastructure
	- Defines the UML core metamodel
- OCL (Object constraint language):
	- Formal language for writing predicates, constraints, and formulas inside diagrams
- XMI (XML Metadata Interchange):
	- DTD for UML models
- UML Diagram Interchange: XMI + graphic info
### Structure and behaviour
- UML focuses on two aspects of object oriented models: structure and behaviour.
- It aims at visualizing both.

#### Describing the structure of software
- The description of structure offers an account of what a system is made of, in terms of both its parts and the relationship among htem.
- A structure may be a hierarchy featuring one to many relationships, a network featuring many to many, or a lattice featuring connections between components that are neighbours in space.

**Module vs component**
- Module - detailed implementation description. Focusing on inner structure and "use" structure
- Component, high level description, used early in design phase.
Module static structure
Component runtime structure

##### Three model axis 
Functional interaction model 
Dynamic dynamic model state chart
Static object model made by functional and dynamic

Example:
Chess program, alone, client server, agent based.
Different rules?
What is the goal?
- To play and win a chess game against an opponent

- Could it be used to learn to play chess?
	- Responsibility of program, write chess notation

- Each responsibility corresponds to at least a use case

##### Use cases
- A use case is a description of the possible sequences of interaction between the system under discussion and its external actors, related to a particular goal.
- The idea of a use case is to show how the systems responds to the outside word, the responsibilities and behaviour of the system without revealing how the internal parts are constructed.
- We want to write as little as possible, as clear as possible

*Use Case Diagram*
- It describes the externally observable behaviour of a system, as related to requirements
- It describes the main interactions between the system and external entities, including users and other systems.
- It is a summary of the main scenarios where the system will be used.
- It describes the main user roles

- Very important - external properties and entities, e.g. black box view

##### Elements of a use case diagram
- Actor
	- Represents a role played by external entities
	- Humans, external systems, that interacts with the system or the system to be interacts with, important -<span style="color:rgb(192, 0, 0)"> time is an actor</span>
- Use case:
	- Describes what the system to be shall do
	- Scenario: sequence of interactions between the actors and the system to be
- Relationships:
	- Relations between actors, use cases and other use cases

Hierarchy of actors, cause if not we get supporting actors.