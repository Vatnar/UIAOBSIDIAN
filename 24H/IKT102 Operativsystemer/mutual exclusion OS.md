Passe på at kun en av prosessene kan lese og skrive til den delte daten samtidig

Property of [[process synchronization]] "no two processes can exist in the critical section at any given point of time"
The need for mutual exclusion comes with concurrency. There are several kinds of concurrent execution:

- Interrupt handlers
- Interleaved, preemptively scheduled processes/threads
- Multiprocessor clusters, with shared memory
- Distributed systems
[Mutual exclusion](https://www.geeksforgeeks.org/mutual-exclusion-in-synchronization/) methods are used in concurrent programming to avoid the simultaneous use of a common resource, such as a global variable, by pieces of computer code called critical sections.

[[Lock - Mutex]] is a mutual exclusion flag