External and watchdog

Polling vs interrupts
Polling
- Continousluy read input waiting for a value
- Used in all sorts of system but very applicable in mC
- Can be clunky in a program cause a lot of loops.
- Can be less responsive
- Small program in small programs, big problem in big programs

Interrupts
- Function that runs when a condition occurs.
- You set the interrupt -e.g. when input 0 goes high
- Interrupts allow you to more easily handle urgent events
- Whatever code is running is paused when an interrupt occurs, exceot ongoing handling of higher priority interrupt
- The paused code resumes when interrupt ends.

## Types of interrupt
#### External Interrupt
- Can be used for passive (button) or active (microcontroller) components. 
- Triggers on an external signal, e.g. digital input.