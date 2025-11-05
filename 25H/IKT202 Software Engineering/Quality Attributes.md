# Quality Attributes

- The architectures current technical environment is also an important factor.
	- Standard industry practices
	- Software engineering techniques prevalent in the architect's professional community.
- Today's information systems are web-based, object-oriented, service-oriented, mobility-aware, cloud-based, social-networking-friendly, AI-enabled
	- It wasn't always so
	- It wont be so ten years from now

### Architectural process
- All of these processes that involves software development include design among their obligations.
- Architecture is a special kind of design, so architecture finds a home in each one

### A definition of software architecture
- The software architecture of a system is the set of structures needed to reason about the system, which comprise software elements, relations among them, and properties of both.

**Constraints**: Design decision with zero degrees of freedom. That is a design decision that has already been made for you.
**Assumptions**: Very important to state our assumptions.

FReq: "When the user presses the green button the Options dialog appears":
- Performance QA (Quality Attribute) annotation might describe how quickly the dialog will appear.
- Availability QA annotation might describe how often this function will fail, and how quickly it will be repaired.
- Usability QA annotation might describe how easy it is to learn this function.

## Modules and Information Hiding
Loose coupling.
- Loosely coupled if interaction is only through interfaces
- Tightly coupled if the implementation of one module depends on the implementation of another
Message coupling
- Send messages through interfaces
Subclass coupling
- Inherit methods from superclass
Global coupling

Content coupling

Aim for High cohesion
- Degree to which the elements of a module belong together
- High cohesion of a module has one purpose and all element relate to the purpose.
- Low cohesion, module hase elemnts to be grouped together.
- jmultiple roles or elements that do not relate to a single purpose

Functional:
- Elements that relate to a single purpose
Sequential:
- Group elements based on processing steps
- Output of one process used in another
Data-cohesive:
- Grouped because they operate on the same data. 
- Rather, put functionality in correct module/functions
Temporal:
- Group elements based on ordering, may not be for related activities. 
Conincidental: No reason for elements to be grouped together