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
