- Fil navngiving
- Fil struktur
- Fil typer
- Fil tilgang
- Fil attributter
- Fil operasjoner/system kall
- Memory Mapped files (look at later)
### Terminologi
- Field
	- Grunnleggende data element
	- Inneholder en verdi
	- Karakterisert ved lengde og datatype
Record
- Samling av relaterte fields.
- Behandlet som en enhet
File
- Samling av lignende records.
- Regnet som EN enhet
- Har filnavn
- Kan prohibit and permit accessGi og ta tilgang
Database
- Samling av relatert data
- Relasjoner i mellom elementer

Filer blir håndtert av opsys. HVordan de blir akksessert navnet, beskyttet implementert er et hovedområde innenfor opsys design.

**Objectives**
+ Dekke behovene og krav for data administrasjon fra brukeren
+ Garantere at data i en fil er gyldig
+ Optimalisere ytelse.
+ Tilby input output for mange ulike lagrings enheter og typer.
+ Minimere eller fjerne muligheten for tapt eller ødelagt data.
+ Gi et standardisert sett med input outputt grensesnitt rutiner.
+ Gi input output support for flere brukere.
**Krav**
- Each user can create, delete, read, write and modify files.
- Each user may have controlled access to other users' files.
- each user may control what type of accesses are allowed to the users' files.
- Heac user should be able to restructure the user's files in a form appropriate to the problem.
- Each user should be able to move data between files
- Each user should be able to back up and recover the user's files in case of damage
- Each user should be able to access the user's files by using symbolic name.
- ![[Pasted image 20241115153831.png]]
[[Files System Software Architecture]]
**Filnavngivning
+ Får navn ved skapelse av prosess
+ Når prosessen forsvinner kan filen bli gjenbrukt av andre prosesser ve å bruke navnet.
+ Regler for navngiving varier.
+ De fleste har filnavn og fil extension
+ Noen programmer bruker extensions, men for OS er det ikke krevet.
**Struktur 
+ Tre vanlige måter:
+ Byte sekvens
	+ En ustrukturert sekvens med bytes
	+ opsys ser vet ikke og bryr seg ikke om hva den inneholder 
	+ All mening må legges inn av brukerprogram
	+ Maks fleksibilitet.
	+ Blir brukt av både UNIX og Windows
- Record Sekvens
	- En sekvens av en bestemt lengde bytes med litt intern struktur.
	- Gammelt system som ble brukt for hullkort.
- Tre
	- Består av en tre-struktur der det ikke trenger å være av samme lengde, men de har et nøkkelfelt i en bestemt posisjon.
	- Operativsystemet bestemmer hvor filene skal palsserers.
	- Brukt på store mainframe datamaskiner fremdeles.
	- ![[Pasted image 20241115160625.png]]
**Fil Typer
+ Vi har flere forskjellige typer filer
	+ Vanlige filer (regular)
		+ Inneholder bruker informasjon
	- Karakter spesielle filer (character special)
		- Relkatert til IO enheter
		- Brukt til å vise IO enheter.
	+ Blokk spesial filer
		+ Brukt til å vise harddisker
		+ ![[Pasted image 20241115161230.png]]
**Fil tilgang
+ Sekvensiell aksess
	+ Brukt i de første tidene
	+ Leste filene på rekke og rad, men kan ikke lese filene i en tilfeldig rekkefølge
	+ Kunne bli spolt tilbake
+ tilfeldig (random access)
	+ Filene kan bli lest i hvilken som helst rekkefølge
	+ Essensielle for mange programmer
	+ alle moderne systemer bruker random access.
**Fil attributter
+ Alle filer har noe mer informasjon assosiert ved seg en bare filnavn og dataen i filen.
+ Kalles attributter. Attributter gir metadata om en fil.
+ Det er mange forskjellige attributter som kan leggest til en fil. 
+ ![[Pasted image 20241115161720.png]]
+ [[Systemkall for filer]]

**Mapper directories, filkataloger
+ En level single level
+ ![[Pasted image 20241115162208.png]]
	+ Enkleste form for mappe system
	+ En mappe med all efiler kalles ROOT (UNIX)
	+ Fordeler
		+ Enkelt
		+ Finner filer raskt
	- Ulempe
		- Mange filer i samme mappe
			- Flerbrukersystemer kan få problemer med overskriving av filer med bruk av samme navn.
	Kan bli brukt i små embedded systemer
+ To level two level
	+ ![[Pasted image 20241115162224.png]]
	+ Enkelt system for flerbruker
	+ Hver bruker har hver sin mappe 
	+ Slipper overskrivingsproblemer
	+ En bruker kan få tilgang til sine filer
	+ Krever en form for innloggingsprosedyre
	+ Kan utvides til å få tilgang til andre brukeres filer
	+ Kan brukes i flerbruker maskin eller små nettverk.
+ Hierarikisk mappesystemer
	+ ![[Pasted image 20241115162412.png]]
	+ Generelt tresturktur system
	+ Brukeren kan struktuere som den vil
	+ Hver bruker så mange mapper som den vil
	+ Filer kan bli gruppert i naturlige mapper.
	+ Nesten alle moderne filssystemer har denne måten.
	+ ![[Pasted image 20241115162514.png]]
	+ 
+ Path name
+ [[systemkall for mappe, operasjoner]]
+ For å holde orden på filene har man mapper
+ Mappene i mange systemer er selv filer
+ I mappene legger vi filer.

**Filsystem implementering**
De som lager er interresert i
- Hvordan filer og mapper lagret
- Hvordan er det med plass håndtering
- Hvordan få det til å være effektivt
- Og ikke minst hvordan få det til å være pålitelig
Fil system layout (Planlegging)
	Filsystemer på datamaskiner
	Delt opp i partisjoner
	Sector 0 er MBR Master boot record
	MBR blir brukt for å starte datamaskinen
	MBR laster den første blokken i den aktive partisjonen og eksekverer denne
	Den første blokken holder informasjonen som skal til for å starte opp OS.
	![[Pasted image 20241115163426.png]]
	
Implementering av filer
+ Contiguous allocation
	+ Enkleste metode
	+ Lagrer blokkende fortløpende etter hverandre
	+ Husker den første blokken og hvor mange blokker det er.
	+ Trenger kun ett søk for å lese iog finne en fil.
	+ Harddisken blir etterhvert fragmentert.
	+ Må gi beskjed på forhånd hvor stor en fil er.
	+ CD-ROM
	+ ![[Pasted image 20241115163652.png]]
+ Linked list allocation
	+ LInket liste med blokker
	+ Første ord i blokka er en peker til neste blokk
	+ Harddisken blir ikke delt opp fragmentert
	+ Man trenger kun og huske første blokk
	+ Tilfeldig lesing av en blokk er tregt
	+ BLokken er ikke 2x. Mange program leser og skriver blokker 2 og 2.
	+ ![[Pasted image 20241115163944.png]]
+ Linked list allocation using a table memory
	+ Tar peker ordet i begynnelsen av filen og plasserrer det i en minnetabell i plassen
	+ Tar bort begge ulempene med linket liste
	+ FAT (File Allocation Table) (MS-DOS)
	+ Hele tabellen må være i minnet
	+ 20GB harddisk, 1KB blokk størrelse => 60-80MB stor tabell i RAM.
	+ ![[Pasted image 20241115164052.png]]
+ I-nodes index nodes, knutepunkt
	+ Hver fil får en i-node som lister opp attributter og disk adresser
	+ Trenger bare å være i minnet mens den filen er åpen.
	+ Maks størrelse i minnet er lik maks antall filer som kan være åpnme på en gang.
	+ En I-njode har kun plass til X antall adresser
	+ hvis en fil er større en dette så blir den siste adressen en peker til en ny i-node med flere adresser.
	+ UNIX
	+ ![[Pasted image 20241115164201.png]]
	+ 
Implementering av mapper
- Samme som ved filer,
- Attributter lagret rett under mappen unntak Inode
- ![[Pasted image 20241115164236.png]]
- ![[Pasted image 20241115164256.png]]
- 
Delte filer
	Fordeler å kunne dele filer
	Det blir laget en link m,ellom filen som blir delt og den andres mappe
	Filssystemet bli r da en direct acyclic graph DAG. istedenfor tree.
	Hvis linka flilen blir oppdart så blir kun den filen i den ene mappen oppdatert.
	I-nodes
		Dataen er ikke lagret i mappen, men i i-nodes assosiert med filen
	Symbolisk linking
		Den linka filen inneholder bare referansen PEKER til den originale filen
		![[Pasted image 20241115164528.png]]
		
Harddisk plass administrasjon
	Kan lagres contiguous eller ikke.
	Nesten alle filsystemer deler filer opp i blokker med bestemt størrelse
	BLokkene trenger ikke nødvendigvis å være på rekke og rad.
	Ca 2-4KB
	![[Pasted image 20241115164635.png]]
	HOlde orden på fire blokker
		Lagre fri blokker i en liste.
		Bitmap
		![[Pasted image 20241115164716.png]]
		
Filsystemers pålitelighet
	Ødelagt filsystem er verre en ødelagt datamaskin.
	Backup
		Hele systemet, eller deler
		Bortkastet tid av filer som ikke har forandret seg
		Komrpimere data
		Vanskelig i et system som kjører
		Mange ikke tekniske problemer
		Physical dump
			Starter ved blokk 0 og skriver av hele ahrddisken
			Enkel
			Er ingen vits i å ta backup av ledige blokker
			Hvis en blokk er ødelagt blir også denne dumpet.
		Logical dump
			Starter på en spefisisert mappe og tar med seg de filene som har blitt forandret siden sist.
			Freeblokk liste er ikk en fil og blir ikke tat backup av
			Det er viktig at filer som er med i en link bare blir gnneopprettet en gang
			Mange systemer modifiserer filer og skriver dem til harddisken senere
	• Hvis det blir kræsj før de blir skrevet til harddisken kan det bli rot
	• Derfor er det som regel et program i alle operativsystemer som sjekker filsystemers konsistens
	• For eksempel UNIX: fsck Windows: scandisk
Filssystemers utførelse
	Caching
		Vanligste måten
		Man har noen blokker med dat ai minnet i plassen for haddisken der de egentlig skal være
		Det er mange forksjellie algoritmer
		Sjekker cache først om blokker er der, hvis ikke så kopieres den inn. Den forsvinner fra cachen igjen når den har blitt fylt opp.
		Når skal cachen skrives til disk?
		UNIX har sync: tvinger alt i cachen til disken (30s)
		MS-DOS skriver enhver blokk som blir modifisert til disken med en gang kalt write through caches
	Block Read Ahead
		I denne teknikken så leser man en blokk lenger frem.
		For eksempel hvis man leser blokk k så sjekker man om blokk k+1 er i cahchen,. Hvis den ikke er det blir den skrevet inn.
	Minske armbevegelsen
	Man putter blokker som det er sannsynlig at blir lest i rekkefølge nærme hverandre. Hels t i samme sylinder.
Eksempler
CD ROM
- ISO 9660
- Rock ridtge extensions
- joilet extensions
CP/M
MS-DOS
WINDOWS 98
UNIX v7
