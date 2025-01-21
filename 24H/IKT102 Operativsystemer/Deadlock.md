Vranglås på norsk
Definition:
	A set of processes is deadlocked if each process in the set is waiting for an event that only another process in the set can cause.
		Potential deadlock, 4 biler møtes i kryss uten lys. Alle depender på hverandre.
		Faktisk deadlock, Halt til bil x er fri.

Deadlocks
	- Mange ressurser i et system kan kun brukes av en prosess om gangen
	- Enkelte prosesser trenger eksklusiv tilgang til mer enn en ressurs.
	- Kan også skje i nettverk
	- Kan skje både med hardware ressurser og software ressurser.
		- comport (communications port)
		- cdbrenner
		- Database, låser den ved skriving, kan bli deadlock

Ressurser
- Ressurs hardware printer og software informasjon i et databasesystem
- Preemtable og nonpreemtable ressurs.
- Det er nonpreemtable ressurser som er problematiske i forhold til deadlock.
- Sekvensen som man må følge for å rekvirere en ressurs
	- Rekvivere ressuren
	- Bruke
	- Frigi
- Hvis rekvirereringen bli nektet må prosessen vente.
	Ready running blocked.
Betingelser for deadlock
- Gjensidig utelukkelse tilstanden Mutual exclusion 
	Hver ressurs er tildelt en prosess eller er tilgjengelig
- Hold og vent tilstanden
	Prosesser som holder på en ressurs kan rekvivere flere.
- Ingen overtakelse
	Ressurser som har blitt gitt kan ikke bli tatt bort fra prosess.
- Sirkulær venteløkke.
	Må bestå av en sirkulær kjede med mer en 2 prosesser.
	Der hver prosess venter på en ressurs som blir holdt av det neste medlemmet i kjeden.

Deadlock modellering
- For  å finne og løse deadlock problemer kan man modellere. 

Fire strategier s167
- Ignorere problemet helt
- Oppdagelse og berging. La det skje, finne dem og løse dem.
- Dynamisk unnvikelse ved å forsiktig ressurs tildeling
- Forebyggelse ved å unngå en av de nødvendige betingelsene for at deadlock kan oppstå.

The ostrich algorithm
- Stikk hode i sanden og lat som om det ikke er noe problem. Fornuftig hvis deadlock skjer sjeldent, og kostnaden ved å unngå er høy.
- Tidligere windows versjoner og UNIX.

Deadlock detection and prevention
- Lar deadlocks oppstå og prøver å løse dem.
- Algoritme for å  oppdage deadlocks.
- Hvis en prosess har stått stille i x antall klokkeyskluser, så må sjekke hva som skjer.
- Not responding
- Berging av en deadlock
	Ta ressursen fra en prosess.
	Rollback man lagrer systematisk og kan gå tilbake for ånngå deadlock
	Drepe en prosess. 

Deadlock avoidance
- Mulig å unngå deadlock ved forsiktig tildeling, nesten umulig i praktisk
- Betingelser
	Må ha noe informasjon tilgjengelig
- Kan være mulig i mindre enklere systemer

Deadlock prevention
- Angriper de fire betingelsene for deadlock
- Gjensidig utelukkelse tilstanden [[mutual exclusion OS]], [[spooling]]. 
- Hold og vent tilstanden, kan gå i små systemer batch
- Ingeni overtakelse no preemption, ikke reelt
- Sirkulært venteløkke tilstanden, 
	prioritert ressursliste.
 Mutual exclusion Spool everything.
 hold and wait, trequast all resources initially.
