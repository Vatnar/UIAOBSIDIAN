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

- Unstable power can cause problems. Memory corruption.
- Watchdog has a sequence to turn on and off, so it is protected. e.g. cosmic rays. ecc. 
## MBed-os interrupts
#### External interrupts on inputs
- Useful for buttons and other triggers
- All inputs on our board support interrupts
- External interrupts are directly supported by the MBed OS library.
#### External interrupt types
- LOW / HIGH: Trigger as long as the input is LOW / HIGH.
- CHANGE: Trigger when it changes
- RISING: Trigger when it goes from LOW to HIGH
- Falling: Trigger when it goes from HIGH to LOW
![[Pasted image 20250228104813.png]]
```cpp
#include "mbed.h"
#define DISCO_BLUE_BUTTON PC_13 // UM2153: HIGH to LOW transition when pressed
volatile int state = 0; // Keyword volatile ensures variable is read from memory before evaluated

void button_interrupt_cb(void) {
  state = !state; // Toggle state; 0=>1 or 1=>0
}
int main() {
  DigitalOut led1(LED1);
  InterruptIn button(DISCO_BLUE_BUTTON, PullNone); // Blue button has pullup

  // Configure callback function for falling edge interrupt from blue button
  button.fall(&button_interrupt_cb);

  while (true) {
    led1.write(state);
    thread_sleep_for(100);
  }
```

