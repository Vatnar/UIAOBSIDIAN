External and watchdog

Polling vs interrupts
Polling
- Continuously read input waiting for a value
- Used in all sorts of system but very applicable in mC
- Can be clunky in a program cause a lot of loops.
- Can be less responsive
- Small program in small programs, big problem in big programs

Interrupts
- Function that runs when a condition occurs.
- You set the interrupt -e.g. when input 0 goes high
- Interrupts allow you to more easily handle urgent events
- Whatever code is running is paused when an interrupt occurs, except ongoing handling of higher priority interrupt
- The paused code resumes when interrupt ends.

## Types of interrupt
#### External Interrupt
- Can be used for passive (button) or active (microcontroller) components. 
- Triggers on an external signal, e.g. digital input.
#### Timer Interrupt
- Used when accurate timing is important.
- Triggers at set intervals, e.g. every second

#### IO Interrupt
- Used to handle data transfer happening "in the background"
- Triggers when data arrives or has been sent on I2C/SPI/UART

#### DMA Interrupt
DMA is a method of copying memory quickly, direct memory access.
Triggers when data has been copied.

#### Watchdog Interrupt
- Used to handle code that hangs or crashes.
- Triggers when the system becomes unresponsive.
## Mbed
#### External interrupts on inputs

#### External interrupt types