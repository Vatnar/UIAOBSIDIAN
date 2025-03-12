Før du kan løse må du forstå.
Da må du gjøre en analyse
<span style="color:rgb(255, 0, 0)">Object Oriented Analysis/Design</span>
<span style="color:rgb(255, 0, 0)">OOA, OOD, OOA, OOAD.</span>
Analyse er å forstå. Design å løse.
<span style="color:rgb(255, 0, 0)">Ikke trekke inn løsning i problemet.</span>

## Object Oriented analysis
- Modelling real world objects based on their description
- produce object analysis modelling
- pays primary attention to the objects with which the problem is concerned.
- Ignore other objects.
Specification is the "drawing" which is the base of the program.

*Hvorfor har vi OOP*
- Modellere den virkelige verden
	- Statiske strukturen
		- Hvordan ting henger sammen
		- En pasient tilhører ett sykehus
	- Dynamiske strukturen
		- Kan en pasient være pasient på to sykehus samtidig
		- Forflyttelse
- Er det poeng å snakke om pasient hvis man ikke gjør det i kontekst av et sykehus?
- Forstå domenet. kan ikke designe universitet som et sykehus med mange små rom.

- En relasjon mellom en pasient og et sykehus.
- Abstraksjonsnivå, Level of granularity
```plantuml
@startuml
Pasient -- Sykehus
```
Klikker nivå
USB, HHE nivå.
IR.
OSV.

<span style="color:rgb(255, 0, 0)">Abstraction</span> gjør at vi kan lage overordnede prinsipper.

# Hvordan
Vi bruker OOA.
+ Finne Klasser
+ Beskrive relasjoner mellom klasser
+ Beskrive ansvarsområdene til hver klasse
+ Entity klasser lærer vi.


Klasser
- Entitet
	- tenk databasetabell
- Kontrollerklasser

Tasklist
1. Obtain or prepare a textual desscription
2. Underline the nouns
3. Organize the nouns into groups to become candidate classes.
4. Underline all the adjectives
5. Assign the adjectives as attributes ot the candidate classes
6. Underline the verb, differentiate action from stative verb.
7. Assign the action verbs to operation of classes.
8. Assign the stative verbs as attributes of classes or relationship.

Proper noun - Object instantiation - alice
Common noun - class Customer
Doing verb - Association - creates, drives, submits
being verb - special form, inheritence, specialization - is kind of 
Havin/owrning verb - aggregation, com But some tools are better than others. position, has, includes
adjective  - atrtributes.

UML
Unified Modeling Language

Modeling syntax aimed primarily at creating models of software-based systems.

- UML Defines rules, not what diagrams to create.
- Comprehensive - it can be used to model anything. It is deisgned to be user extended.
- Language-independent. Doesnt matter what hi leel language is to be used in the code. Mapping into  code is a matter of the tool you use.
- Process-independent, Seperate from the process.
- Can be defined in xml, tool independent.
- Well documented - the UML notatioon guide is available.
- ITs application is not well understood - the UML notation guide is not sufficient to use the language. 
- Originally for jsystem, but is used for other sthings too.

# UML diagrams
- structure diagrams:
	- Describes static structure and relations
		- Class diagram
		- package diagram
		- component diagram
		- deployment diagram
- behavioral diagrams
	- describers dynamic behavoir or change over time.
		- Usercase diagram
		- Interaction diagram
			- Sequence diagram

Notation for UML classes
![[Class-Notation.webp]]
<span style="color:rgb(255, 0, 0)">Information hiding</span> 
Sett alt til private, vurder om noe skal være public.
Private gir modifiability
