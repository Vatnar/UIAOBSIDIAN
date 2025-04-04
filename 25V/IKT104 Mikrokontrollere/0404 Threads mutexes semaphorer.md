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
		- Semaphores for synchronisation, waiting, signaling
	- IPC: inter process / thread / task communication
	- We'll go through these later in the next lecture.
	-

