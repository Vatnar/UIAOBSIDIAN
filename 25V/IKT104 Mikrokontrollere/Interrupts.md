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

`volatile` tvinger kompilatoren til å ikke optimalisere ut variabelen.

For denne while loopen vil aldri state endre seg, siden det endres utenfor.
Kompilator prøver å lage rask kode. 

```cpp
int state = 0;
while (state == 0) { } // Wait until state is changed by an interrupt
```
I while loopen endres ikke state, så den vill erstatta state med 0.
`while (true) { }`

#### Do's and don'ts
<span style="color:rgb(0, 176, 80)">What to do</span>:
- Code in interrupt should be short and fast.
- Better to set some values that are handled in the loop
- Keep interrupt handlers simple
<span style="color:rgb(255, 0, 0)">What <span style="color:rgb(255, 0, 0)">not</span> to do</span>:
- A long interrupt can delay other interrupts and the loop
- Don't use code that relies on other interrupts like std::printf().
- Don't wait for something or block. No polling e.g.

## Watchdog Interrupts
What it is:
- A watchdog is a timer used to monitor your application or device
- It can detect if code is hanging (stuck forever)
- On a timeout an interrupt occurs.
- This interrupts resets the system usuallly. (because there can be alot of things causing it.)
- very high priority. 

Normal mode:
- Watchdog triggers if it hasn't been refreshed after a given period of time
- You can refresh it as often as you like
- How long it takes to trigger can be configured.

Window mode:
- The watchdog must be refreshed during a specific window of the configured period
- A *window* is a specific time range, that has an earliest and latest time.
- If the watchdog is refreshed outside the window it will trigger.
- This will also detect if the code is stuck clearing the watchdog continuously.
- How long it takes to trigger can be configured.
### Normal mode with system reset
1. Set which watchdog instance is being configured
2. Configure the prescaler value.  
    This sets how fast the internal timer runs
3. Set the reload value.  
    This is the value the watchdog starts counting down from on refresh
4. Init the watchdog
