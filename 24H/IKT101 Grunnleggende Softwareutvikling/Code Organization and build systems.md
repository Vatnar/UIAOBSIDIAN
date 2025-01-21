- Agenda
- Organizing Code
- Command line programs
**Compilers**
- Purpose
- Source and target languages
- Basic usage
- Machine Code
**Linkers**
- Purpose
- Input and output
- Basic usage
**Build system examples**
![[Pasted image 20241104132120.png]]
## **CLion build order**
1. CLion calls (starts) CMake, CMake er en byggenerator. Leser CMakelists.txt. 
2. CMake generates build files for Ninja
3. CLion calls (starts) Ninja with intermediate files
4. Ninja uses GCC or Clang to compile .c files
5. Ninja uses GCC or Clang to link .o files
6. Final executable has been created

## **Organizing code**
- Ganske fri layout.
- You can split your code into multiple files to keep your porject organized
- Code outside of main live in one of these two types of files:
	- .h files header file / Struct definitions and function prototypes
	- .c/.cpp files source file / Function definition / implementations 
## **Command line programs**
**about**
- Every program we have made so far is a cli program
- You can run these outside of CLion by starting the program file.

### Compilers
**Purpose**
- A compiler is a program that reads code and turns it into another output format
	Noe nytt kan være forskjellige ting, ofte da binær fil. F.eks .obj, instruksjoner som prosessoren kan gjøre, helt grunnleggende atomiske operasjoner.
- The output is usually lower level, like assembly code or machine code (binary)
- There are many different compilers, supporting different languages for input and output.
- We are currently using GCC on Windows/linux and Clang on OSX
- Compilers output compiler errors: Typos, missing semicolons and so on.
	disse feilmeldingene kommer fra GCC eller Clang som sender det tilbake til Clion
**Compilers with C/Cpp**
- Translates each C file seperately, as seen on the previous figure.
- The output is usually an object file which contains the machine code for each C file
- These object files are then used as inputs for the linker.
**Relation to Clion**
- Clion is not a compiler, just a fancy text editor
- Clion uses the compiler installed on your machine to build code
	- On windows you manually install one (MinGW)
	- on osx you get a compiler when you install Homebrew
	- On linux (debian/ubuntu) you get compiler when you install build-essential
### Basic compiler commands
- These commands use Gnu Compiler Collection
- On windows you might have to be inside the MinGw-bin directory
- Compile main.c to main.o as binary code
```zsh
gcc -c -o main.o main.c
```
- Compile main.c to main.o as binary code with optimization level 2:
```zsh
gcc -c -o main.o -O2 main.c
```
- Compile main.c to main.o as binary code with:
	- optimization level 2
	- All warmings turned on
	- c99 as the input language
	```zsh
	gcc -c -o main.o -O2 -Wall -std=c99 main.c
```
- Compile main.c to main.o as binary code, allow includes from given path.
- This is often needed when using additional libbraries
```zsh
gcc -c -o main.o -IC:/dev/libs/auby/inculde main.c
```
### Machine code
**Why we need it**
- Processors CPU does not understand C code, or any code. Only basic operations
- The processor requires code in binary format made for that specific architecture
- There are many architectures (x86-64, ARM, MIPS...)
- Machine code is not compatible between architectures
- High level languages like C allows us to run the same code across  architectures.
**What does it look like**
- Assembly code is a text representation of machine code. Because of this assembly code is different for different architectures.
### Seeing compiler linker commands with Cmake
```zsh
set(CMAKE_VERBOSE_MAKEFILE on)
```
### Why build systems are needed
**Small vs medium/large software projects**
- As we saw in the previous lecture you can compile manually with the compiler
- This is fine for small projects
- As the project grows some problems will crop up:
	- The command line will be very long and you will have many files
	- Every file is compiled every time you build which can be slow
### Build systems
- CMake
	Generates build files for other build systems, using ninja in CLion
	Ninja is designed to be used with build generators like CMake
- Make
	Build system since the 70s
	MakeFile lists the targets what to build and how to build them
	File is read by the make command to build the project for you using th eavailable compiler
- Boost build
	Boos tbuild is the build system used by the popular CPP library Boost
	The boost library contains a lot of functionality not availble in CPP STD
	Mostly used for projecets that utilize the Boost library, since it is well integrated there.
	Boost has support for Clion