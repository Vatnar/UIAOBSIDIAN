- Principles are used to diagnose problems with designs
- Patterns are used to address the problems

Software inevitably changes/evolves over time, maintenance upgrade.

**SOLID**
[[Single Responsibility Principle (SRP)]]
- Every class/module should only have one reason to be changed - the class/module should have only one responsibility.
- If class module A has two responsibilities, create new classes/module, to handle each responsibility.
[[Open Closed Principle (OCP)]] 
- Every class should be open for extension (derivative classes), but closed for modification (fixed interfaces).
- Put the system parts that are likely to change in the implementation (i.e. concrete classes) and define interfaces around the parts that are unlikely to change (e.g. abstract base classes)
[[Liskov Subsitution principle (LSP)]]
- Every implementation of an interface needs to fully comply with the requirements of this interface ( requirements determined by its clients)
- Any algorithm that works on the interface, should continue to work for any substitute implementation
- Every subclass or derived class should be substitute for base or parent
[[Interface segregation principle (ISP)]]
- A client should never be forced to implement an interface that it does not use, or client should not be forced to depend on methods they do not use -> segregate you interfaces.
- Keep interfaces as small as possible, to avoid unnecessary independents. Only keep coherent methods in an interface.
- Ideally,  it should be possible to understand any part of the code in isolation, without needing to look up the rest of the system code.
[[Dependency Inversion Principle (DIP)]]
- Instead of having concrete implementation communicate directly and depend on each other, decouple them by formalising their communication interface as an abstract interface based on the needs of the higher-level class.