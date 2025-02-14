- Serial vs parallel
- Everyday examples
- MIcrocontroller communication options
- What is a bus?
- UART
- i2c
- SPI

Serial
- One link
- Transmits one bit at a time
- LIke a single queue at the post office
- Clock decides when a new bit is sent
- Requires smaller PCB
- Cables can be thinner
- Baud rate, 
- 

Parallel 
- Transmits multiple at once
- Like multiple queues 
- Clock decides when a batch is sent (usually)
- Bigger PCB
- Thicker or more wires.
![[Pasted image 20250214082337.png]]
the sides need to agree on how long one byte is and so on. 
Need to setup speed.
Or you can use a clock, goes up and down every other time. Every time it changes, there is red a new bit from the data line
We need the clock to synchronize

Clock is often used, e.g RAM, 4GHz ddr4

For serial you can have less connections
Transmit receive Ground Clock standard. 

Parallel is similar, but we use more than one. 8x as fast on same clock frequency.
Its faster, but alot more connections.

High frequency means less distance. DDR5 RAM is 64 lines. 

*Serial*
USB, serial port.
Universal Serial Bus, 
Clock is part of data signasl. up to Usb 2.0
Usb 3.0 has 4 data signals usb c is more complex.

*Parallel*
Paralell port, or RAM.
Ack busy so on.

*Microcontroller communication options*
UART - Univerasal asynchronous receiver tranceiver
- WE have used this already with std:printf()
- Can connect two microcontroller together with the same setup on their UART speeds, start stop bit, parity bits, Parity, verify data, correct interference. RAID, replace disk death. Error Correction, for UART interference. 
- Minimum 2 lines for bidirectional transmit and receive.
- Connects 2 devices together, no more
I2C - Inter-iintegrated circuit bus / TWI - Two Wire Interface Bus
- often used by sensors (temperature, pressure etc, humidity)
- Only uses 2 lines independent of the number of devices (data, clock)
- All devices are connected to the same wires thus the name.
![[Pasted image 20250214085201.png]]
Serial data and serial clock.
mikrokontrollere er master og enhetene er slaver.

SPI - Serial Peripheral Interface Bus
- Used to connect to peripherals
- SD Cards support SPI
- Uses 3 lines minimum for bidirectional Transmit receive clock
- Clock
- Serial in
- Serial Out
- Slave select
![[Pasted image 20250214085440.png]]

*Bus*
Something that transmits data
- Connect more than two devices, if not its point to point
-  Most buses these days are digital
- Serial or parallel
- Internal connects system components
- An external bus connects peripherals
- Devices on a bus often have an address to tell them apart
- ![[Pasted image 20250214085846.png]]

Uart example
Ground to ground
Tx transmit
Rx receive,
Therefore tx to rx.
and opposite.
Buffered Serial, goes to a buffer first, can send faster than it should 
Unbuffered Seriaal, it goes directly
UART has no clock
![[Pasted image 20250214092559.png]]
They need a common ground
If the speeds are mismatched they will misinterprate bits and bytes.

Often speed is a multiple of 9600 bps, roughly 1000 Byte per sekund. 
9600, 38400, 57600, 115200, 230400, 460800, 921600
Buffered and unbuffered serial classes can be used with functions read and write functions, for simple commands you can send 0 and 1 for off.
Use a protocol for more complex commands.

---
```cpp
Master device
#define BLINKING_RATE 250
BufferedSerial serial_port(PA_0, PA_1, 115200);

int main() {
  DigitalOut led(LED1);

  while (true) {

    serial_port.write("on", 2);
    thread_sleep_for(BLINKING_RATE);

    serial_port.write("off", 3);
    thread_sleep_for(BLINKING_RATE);

    // Toggle "running" LED

    led = !led;
  }
}
Slave device
BufferedSerial serial_port(PA_0, PA_1, 115200);

int main() {

  DigitalOut led(LED3);

  while (true) {
    char cmd[10];
    serial_port.read(cmd, sizeof(cmd));

    if (strncmp(cmd, "on", 2) {
      led.write(1); // Shorthand led = 1;
    } else if (strncmp(cmd, "off", 3) == 0) {
      led.write(0); // Shorthand led = 0;
    }
  }
}
```

I2c
Low speed bus that uses 2 ios.
- SDA serial data line, used for data in both direciton
- SCL - serial clock line, data is transferred on change
- Sensors
- Slave select through data line
	- Each slave has an address 
	- Managed by NXP 
- Commands and results are written/read to / from register
	We will cover this later
Premade libraries to handle specific sensors
You can use i2c manually with mbed os i2c lib
![[Pasted image 20250214094659.png]]

*usage*
we will use
HTS221 temp humidy sensor
16x2 RGB LCD display
[https://developer.mbed.org/teams/ST/code/HTS221/](https://developer.mbed.org/teams/ST/code/HTS221/)
https://drive.google.com/file/d/1_pAloGqN2qxBgUnQEKW5XsiAl8n0NUxe/view
![[Pasted image 20250214094905.png]]
![[Pasted image 20250214094934.png]]
