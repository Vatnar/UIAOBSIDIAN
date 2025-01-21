Hentet fra [Geeks for Geeks ](https://www.geeksforgeeks.org/memory-layout-of-c-program/)
1. Text Segment (i.e instructions)
> >2. Initialized data segment
> >3. Uninitialized data segment (BSS)
> >4. Heap
> >5. Stack
> ![[Pasted image 20241025144325.png]]

**Text Segment** A text segment,also known as code segment or just text. One of the sections of a program in a object file or in memory which contiains executabe instructions. The text segment is sharable so that only a single copy need sto be in memory for frequently executed programs, such as text editors, the c compiler, the shells, and so on. Also, the text segment is often read-only to prevent a program form accidently modifyin its instructions. 

**Initialized Data segment**: Usually called simply the Data Segment. A data segment is a portion of the virtual address space of a program, which contains the global variables and static variables that are initialized by the programmer.It is not read only since the values of the variables can be altered at run time. This segment can be further classified into the initialized read-only area and the initialized read-write area.For instance, the global string defined by char s[] = “hello world” in C and a C statement like int debug=1 outside the main (i.e. global) would be stored in the initialized read-write area. And a global C statement like const char* string = “hello world” makes the string literal “hello world” to be stored in the initialized read-only area and the character pointer variable string in the initialized read-write area.  
Ex: static int i = 10 will be stored in the data segment and global int i = 10 will also be stored in data segment

**Uninitialized Data segment / BSS** bss stood for "block started by symbol". Data in this is initialized by the compiler to arithmetic 0 bvefore th eprogram starts executing uniinitalized data starts at the end of the data segment and contains all global variables and static variables that are initialized to zero or od not have explicit initialization in the source code. For instance declared static int i; would be contained in the BSS segment. Or a global variable declared int j;.

**STACK** The stack area traditioanlly adjoined the heap area and grew in the sopposite direction; when the stack pointermet the heap pointer, free memory was exhausted. (With modern large address spaces and vitual memory techniques they may be placed almost anywhere, but they still typically grow in the opposite directions.) Stack, where automatic variables are stored, along with information that is saved each time a function is called. Each time a function is called, the address of where to return to and certain information about the caller’s environment, such as some of the machine registers, are saved on the stack. The newly called function then allocates room on the stack for its automatic variables. This is how recursive functions in C can work. Each time a recursive function calls itself, a new stack frame is used, so one set of variables doesn’t interfere with the variables from another instance of the function.

**HEAP** is the segment where dynamic memory allocation usually takes place. It begins at the end of the bss segment and grows to larger addresses from there. The heap area is managed by malloc realloc and free. Which may use the brk and sbrk system calls to adjust its size. The heap area is shared by all shared libraries and dyamically loaded modules in a process. 

```c
int main(void)
{
	return 0;
}
```
![[Pasted image 20241025145545.png]]
```c
#include <stdio.h>
int global;
int main(void)
{
	return 0;
}
```
![[Pasted image 20241025145615.png]]
4 bytes ekstra på bss siden den er unitianilzed eller 0;
```c
#include <stdio.h>
int main(void)
{
	static int i;
	return 0;
}
```
![[Pasted image 20241025145718.png]]
```c
#include <stdio.h>
int global;
int main()
{
	static int i = 100;
	return 0;
}
```
![[Pasted image 20241025145810.png]]
Her ser vi bss har fått fire ekstra bytes og data har fått fire extra bytes.
Dec is the size of the text data and bss size added together in decimal, and hex is the same in hexadecimal.