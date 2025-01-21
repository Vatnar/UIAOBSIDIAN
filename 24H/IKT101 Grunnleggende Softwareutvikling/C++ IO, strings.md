- CPP multiparadigme språk basert på C.
	- Ulike måter å strukturere kode på
		- Procedural, Prosedyrisk, globale funksjoner som endrer data som i C.
		- Object oriented, hvor funksjoner og data er gruppert sammen. (nytt)
	- Hvordan man skriver koden sin. 
- C++ er mye større en C, med ett mye større standard bibliotek.
	- Gjør ting enklere, men vanskeligere å skrive?
- Java og C# låner mye fra C++. Mer enn i fra C.
- C -> C++ -> Java, C# 
**Bruk**
- C++ er brukt i større, komplekse systemer.
- Brukt i PC programmer, for desktop og server.
- Brukes også i embedded og microcontroller i moderne tid ARM Mbed
- Eksempler: Google Chrome, Firefox, Microsoft Word, Unreal Engine, Veldig mye AI.
"Level " rating
-  C++ is considered a higher "level" programming language than C. "More abstraction". 
	- I.e. dynamic arrays, std::vector's. Other common data structures. 
	- Low to high:
	Assembly -> C -> C++ -> C# / Java -> Python.
### C vs C++
**Exisiting functionality**
- Everything we have learned so far still works in C++ and **more**
- Variables, operators, arrays, functions, strings, etc.
- The C STD library is still available, but the headers have new names:
	- stdio.h -> csdtio
	- stdlib.h -> cstdlib
	- math.h -> cmath
	- And so on C++ library headers do not have a file extensions.
**New functionality**
- C++ adds supports for classes, inheritence, operator overloading, and more.
	- We'll discuss some of these in later lectures
- C++ adds the C++ Standard Library
	- Uses the new language features
- New ways of input and output, strings, and storing data etc.

```cpp
#include <iostream>
int main(){
	std::cout << "Hello, World!" << std::endl;
	return 0;
}
```
std er namespace, som grupperer funksjonalitet.
Namespaces skjuler funksjoner bak namespace navnet.
:: går fra namepsace til funksjon, eller datatype osv.
std::cout er et object, og du sender det inn med <<.  << Er overloadet. 
Skyver "hello world" inn i output stream, og deretter skyver en endl;
Bruker std::endl for å flushe output. \n flusher ikke.


std::cout printe ting, std::cin lese fra brukeren. brukes med >>. 

