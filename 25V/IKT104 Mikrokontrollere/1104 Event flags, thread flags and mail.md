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
// Each flag is one bit. Use bit 0 for the button event
#define EVENT_FLAG_BUTTON_PRESSED (1 << 0)
// Each EventFlags supports 31 flags (1 bit per flag)
EventFlags event_flags;
static void button_interrupt_cb(void)
{
	// Set event flag EVENT_FLAG_BUTTON_PRESSED
	event_flags.set(EVENT_FLAG_BUTTON_PRESSED);
}
// Thread that handles events from event_flags
void main()
{
	// Setup interrupts etc. here
	while (true) {
		printf("Waiting for button flag event...\n");
		// This thread will be blocked until the flag is set elsewhere
		event_flags.wait_all(EVENT_FLAG_BUTTON_PRESSED);
		printf("Got button flag!\n");
	}
}
```