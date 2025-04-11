![[10. Mbed OS - Event flags and mail.pdf]]

# Event flags, what are they?
Scenario
Imagine a thread that needs to wait for button ionput
The interrupt must notice the change
Interrupt handler is its own function
The thread does not know that the interrupt has happened.
- A semaphore cna be used to poke a thread. Semaphores knows something has happened, but not what.
### Event flags
- Ideal for signaling what has happened to a thread
- The thread can wait or check for one or more events
- Threads and interrupts can set/get events
- Each EventFlags object supports up to 31 flags.
- A flag is one specific thing that has happened.
- Example: 3 flags for 3 different buttons, 1 movment, 1 light, Eventflags would use 5 of 31 flags.
```cpp

```