Agenda
- What is a real time operating system
- Mbed OS features
- Mbed OS architecture
- Creating threads
- Thread switching
- Protecting data with mutexes
- Sharing data between threads
- Common errors
![[09. Threads, mutexes and semaphores.pdf]]
# Real time operating system
**About**
- An RTOS is a small OS for embedded systems
- Mbed OS is one such Real time operating system
	- Zephyr, FreeRTOS
- An RTOS has features similar to a full desktop OS:
	- Process / thread / task switching
		-  In Mbed process dont really exists, threads only.
	- Mutexes / semaphores
		- Synchronize data access, solve race conditions
		- Semaphores for synchronisation, waiting, signalling
	- IPC: inter process / thread / task communication
		- Send data between threads, 1 thread reads buttons, 1 thread executes what happens
	- We'll go through these later in the next lecture.
	-
## Realtime vs traditional OS 
- Lower latency overall (thread switching, interrupt handling etc.)
- Lower OS overhead (no drivers, or lightweight drivers), drivers that exists are sensor drivers
	- No preinstalled programs, made to solve problems when developing.
- Predictability (important for embedded where timing matters)
	- Block interrupts and so on
- Usually no Memory Management Unit support (bare metal)
- Using an RTOS is useful in larger projects