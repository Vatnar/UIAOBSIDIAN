```table-of-contents
```

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

# Mbed
## Mbed OS features
**About Mbed OS**
+ Mbed OS has two main profiles - bare metal and OS
+ The bare metal profiles is suitable for small programs on limited devices
+ The OS profile is suitable for larger programs on more capable devices
**Features**
- OS features: Threads, mutexes, semaphores, mailboxes
- Comunication features:
a. Ethernet / Wi-Fi
b. Bluetooth (low energy) Zigbee (low energy on top)
c. LoRaWAN
d. Cellular
- Security features:
a. Encryption
b. NFC/RFID
## MBed OS Architecture
![[Pasted image 20250404104526.png]]
Our code use Mbed OS APIs, 

# Thread
- Piece of code that runs independent of other threads
- Threads are used to organize larger programs into smaller pieces
- They have their own stacks for local variables, 4KB.
- With for many threads on microC it can be a problem since they dont hav emuch memory
- They share the same memory space.
- They can use mutexes to protect shared resources.
- They can use semaphores to synchronize
**Using**
- Threads are declared using the class Thread
- Functions can be started with thread.start(function)
- Mbed OS switches the active thread automatically to let all threads run
- Thread can sleep to reduce CPU usage, ThisThread::sleep_for(5s);
- You can wait for a thread to finish with the join() function thread.join();
- Threads can have different prioriteies
## Preemptive vs cooperative multitasking
**Preemptive**
- The scheduler pauses and unpauses threads at will
- Threads can be paused an unpaused at any time
- Threads are gnerally unaware that this happens
- Mbed OS uses preemptive threads
**Cooperative**
- Threads must pause themselves to let other threads run
- Threads pause by calling sleep, or other function that wait for data
- The scheduler decides which thread is allowed to run
## Example: Thread
```cpp
#include "mbed.h"
DigitalOut led1(LED1);
DigitalOut led2(LED2);
Thread thread;

void led2_thread()
{
    while (true) {
        led2 = !led2;
        ThisThread::sleep_for(1000ms);
    }
}
  
int main()
{
    thread.start(led2_thread);
  
    while (true) {
        led1 = !led1;
        ThisThread::sleep_for(500ms);
    }
}
```
## Thread Switching
![[Pasted image 20250404113952.png|412x362]]
**Time** **slices**
- Mbed OS uses a timer internally to switch the active thread
- The minimum time a thread can run is called a time slice
- Each thread runs for this amount of time when it is active, at least
**Thread** **priority**
- The default priority is *osPriorityNormal*
- You can assign a different priority at wish
-  Finds the highest priority ready thread
- Runs thread until enter state *waiting* / inactive  
or the next thread switch

## Mutex (mutual exclusion)
![[image-15.png|476x264]]
**About mutexes**
- Mutex can be used to protect access to shared data
- Mutex ensures that only one thread access the data
**Using** **mutexes**
- Mutexes are available through the *Mutex* class
- This class has two main functions:
	- *Lock()*
	- *unlock()*

### Example: Mutex
```cpp
#include "mbed.h"
  
Mutex stdio_mutex;
Thread t2;
Thread t3;
  
void notify(const char *name, int state)
{
    stdio_mutex.lock(); // Use a mutex to lock access to printf()
    printf("%s: %d\n\r", name, state);
    stdio_mutex.unlock();
}
  
void test_thread(void const *args)
{
    while (true) {
        notify((const char *)args, 0);
        ThisThread::sleep_for(1000ms);
        notify((const char *)args, 1);
        ThisThread::sleep_for(1000ms);
    }
}
  
int main()
{
    t2.start(callback(test_thread, (void *)"Th 2")); // callback is used to give the thread a parameter
    t3.start(callback(test_thread, (void *)"Th 3"));
  
    test_thread((void *)"Th 1");
}
```
### Example: Shared Struct
**About**
- We can use structs to share data between threads
- This type of data must also be protected against simultaneous access
- The code is just like last year - except the struct now has a mutex
- Threads lock this mutex when they want to access shared data
```cpp
// Struct holding our data  
typedef struct  
{  
  // Mutex that protects this data struct  
  Mutex mutex;
  // Regular struct members (our data)  
  char message[200];  
} data_t;
```

## Semaphores
**About**
- Semaphores are very similar to mutexes
- You aqquire and realase a semaphore
	- Similar to lock and  unlock for mutexes
- A semaphore can be aqquired more than once
	- useful when moore than 1 shared resource is avaible
- Count is the amount currently availbable max count is the maximum
![[image-16.png]]
```cpp
#include "mbed.h"

Semaphore one_slot(1);
Thread t2;
Thread t3;
  
void test_thread(void const *name)
{
    while (true) {
        one_slot.acquire();
        printf("%s\n\r", (const char *)name);
        ThisThread::sleep_for(1000);
        one_slot.release();
    }
}
  
int main(void)
{
    t2.start(callback(test_thread, (void *)"Th 2"));
    t3.start(callback(test_thread, (void *)"Th 3"));
  
    test_thread((void *)"Th 1");
}
```

### Common errors
Stack Overflow
This error occurs when a function uses up all its stack space. You might see this when using complex libraries or allocating a lot of local variables. You can increase the stack size in mbed_app.json to compensate.

  
Heap Overflow
This error occurs if any thread tries to allocate dynamic memory and that allocation fails. This means the you have used up all the memory on the microcontroller. This error usually occurs because of memory leaks, meaning memory that has been allocated but not freed.

# Resources
- [Mbed OS threads](https://os.mbed.com/docs/mbed-os/v6.16/apis/thread.html)
- [Mbed OS mutexes](https://os.mbed.com/docs/mbed-os/v6.16/apis/mutex.html)    
- [Mbed OS semaphores](https://os.mbed.com/docs/mbed-os/v6.16/apis/semaphore.html)