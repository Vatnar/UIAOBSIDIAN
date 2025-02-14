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