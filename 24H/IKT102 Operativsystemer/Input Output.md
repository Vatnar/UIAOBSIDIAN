I/O - The Big Mess
- Innhold
	- Generelt IO
	- 3 VIktige teknikker
		- Memory Mapped, programmert IO
		- Interrupts
		- Direct Memory Access
	Viktig Enhet
	Harddisk
![[Pasted image 20241108123917.png]]
Veldig mange dingser man skal ha kontroll på.
Forventer at alt skal funke når du plugger inn.
Sånn var det ikke før.
Før
	Hver enhet hadde egne porter,, installer driver, Restart pc.
I/O OSX og Linux vs Windows
	OSX har fordel fordi de styrer hele arkitekturen. 
	Windows og Linux må ta hensyn til masse ulike arkitekturer på ulike enheter.
### Hovedfunksjonene for IO
- Kontrollere alle IO enheter
	- Gi ordrer
	- Fange interrupts
	- Behandle feil
- Gi et grensesnitt mellom enhetene og resten av systemet
#### Forskjellig syn på IO
- Elektroingeniør ser på fysiske komponenter som ledninger, chips, strømforsyninger osv.
- Programmerere ser på programvaren, hvilke kommandoer, funksjoner og hvilke feilmeldinger.
**IO devices**
Deles i to typer
- Blokk enheter
	- Lagrer informasjon i en bestemt blokk størrelse med hver sin adresse
- Karakter enheter
	- Leverer eller får en strøm av karakterer, uten hensyn på blokk struktur
- Noen passer ikke inn(klokker)
- 
**Device controllers**
Deler enheter opp i to froskjellige
- Mekanisk
- Elektronisk
- Elektronisk enheten blir kalt enhets kontroller eller adapter
- En disk kontrollerens oppgaver er å omforme bitstrømmer til blokker, sjekke for feil og så kopiere til minnet.\n
**Operating System Design Issues
- Efficiency
	- Most IO devices extremely slow compared to main memory
	- Use of multiprogramming allows for some processes to be waiting on IO while another process exectues
	- IO cannot keep up with processor speed
	- ISwapping is used to bring in additional Ready processes which is an IO operation.
**Goals of the IO Software**
- Utstyrsuavhengig
	- Programmer kan aksessere hvilket som helst IO utstyr
	- Uten å spesifisere utstyret på forhånd
		- Floppy, hard drive, CD-ROM
- Uniform navngiving
	- filnavn er en tekstreng
		- Bokstaver, tall tegn
	- Uavhengig av den enkelte maskin
- Feilhåndtering
	- Så nært mot hardware som mulig'
- Synkron vs asynkron overføring de fleste IO er asynkrone
	- Blokkoverføring vs. avbruddsstyrt
		Det er letterere å skrive brukerprogram dersom IO operasjonene er sykrone, dvs at programmet blir automatisk suspendert inntil dataene er tilgjengelig i bufferet.
		Løses ved å sende syste$all som blokkerer prosess fram til det er klart. For prosessen er det synkront, men asynkront for operativsystem. 
- BUffering
	- Data som kommer fra et utstyr kan ikke bli lagret på endelig bestemmelsessted - blir først sendt i en buffer.
- Delt utstyr vs. dedikert ustryt
	-Disker er delt type utstyr.
	Tape drivere r ikke det.

![[Pasted image 20241108131442.png]]
**Interrupt Handlers**
Makkverk
- Er best hidden
	- Have driver starting an IO operation block until interrupt notifies of completion.
- Interrupt procedure does its task
	- then unblocks driver that started it
	- Steps must be performed in software after
interrupt completed
![[Pasted image 20241108131553.png]]
**Device Drivers**
Driver ligger i kernel space sammen med operativsystem.![[Pasted image 20241108131617.png]]
Funker veldig bra stort sett.
- Hvorfor så integrert i kjernen?
	Mer effektivt
	Men, 
	Monolittisk, al t i kjernen
	Begynte å hive ut enkelte driver fra kjernen for å slippe å ha alle drivere ut av kjernen
	Får en mer microkernel. (Les opp på dette og monolitt.)
Kommunikasjjonen går gjennom drivere og enhet kontrollere går på bussen.

**Device independent IO software**
![[Pasted image 20241108132119.png]]
![[Pasted image 20241108132144.png]]
Standardisert driver interface gjør det enklere.
fysisk: USB. Universal Serial Bus.
gjør også i software.

![[Pasted image 20241108132246.png]]
**IO buffering**
Reasons:
	-Prosesser må vente på IO for å fortsette
	Noen pages må bli i memory under IO.
- Block oriented
	- Information is stored in a fixed sized blocks
	- Transfares are made a block at a time
	- used for disks and USB keys
- Stream oriented
	- Transfer information as a stream of bytes
	- Terminals, printers, mouse, keyboard so on.
![[Pasted image 20241108132452.png]]

Memorymapped IO
- KOntrollerne har noen få registere som brukes for å kommunisere med CPUen.
- Mange har også buffere som CPUen kan lese og skrive til.
**Tre måter
- Hver kontrollregister er tilegnet egne IO port
- Mapper kontrollregisterene inn i minnet
- Hybrid, der man har buffer i minnet og IO ports for registerne
- IRQ Spesifikke porter som blir brukt.
![[Pasted image 20241108134014.png]]
CPuen setter ut adressen på busen
Bus kontroll linjen får et signal om hva som skal gjøres read write
Egen linje som forteller om det er i IO space av minnet erll iei minnet selv
CPUEn busy waiter for svar på om den er ferdig.
Fordeler:
	Kan bruke C(CPP) for å programmere spesielle IO instruksjoner istedenfor assembly
	Beskytter IO fra brukere.
	Man kan refere til REgistre
ULemper:
- Caching kan være et problem
- Dedikert hiurtigbus til minne.
- ![[Pasted image 20241108134139.png]]
	Programmed IO, busy waiting. Ikke veldig effektivt.
	

****


Interrupts revistied
- Cpu starter en enhet og så begynner den å jobbe med noe annet
- Når enheten er ferdig med å jobben sier den ifra til CPUen dden gir en interrupt.
- Så må CPUen taseg av interrupten.
- ![[Pasted image 20241108134418.png]]
Interrupt handler bestemmer hvilken som går til CPU, andre blir ignorert for øyeblikket
Interrupt Vectoren peker på interruptprosedyren. Driver interrupprosedyre
Så blir interrupten bekreftet.
Cpuen må lagre noe infromasjon før den kan gjøre interrupt.
Minimu, lagre PC. Mange gange lagres registrene. Varierer.
![[Pasted image 20241108134614.png]]

**DMA**
Direct memory access
- Må veksle data mellom kontrollerne og CPU
- Cpuen kan gjøre dette ved hjelp av å ta en og en bit
- Som regel bruker man DMA
- Det kan være en DMA pr enhet eller en sentral DMA
- Dmaen har tilgang til Bus'en uavhengig av CPUen.
- DMA har flere registre som kan bli skrevet til og lest av CPU
		minneadresse
		byte teller
		kontrollregistre
![[Pasted image 20241108134842.png]]
Hvordan.
- Cuycle stealing
	- Overfører et og et ord mellom CPU bruken av busen
	- Stjeler en og anna cycle fra CPUen og forsinker den lik.
- Burst mode
	- Enheten rekvirerer busen og voerfører en burst
	- Kan blokkere cpuen over lengre tid.
- DMA bruker fysissk adresser og dermeed må CPUen sørge for at det er den fyssiske adressem som er skrevet inn med hjelp av MMU og ikke virtuaell.
Ulemper
	Dma er tregere en CPU hvis ikke IO er tregere
	Koster mer penger med DMA
	![[Pasted image 20241108135045.png]]
	![[Pasted image 20241108135051.png]]
	![[Pasted image 20241108135100.png]]
	Gevinsten ved bruk av DMA er å redusere antallet avbrudd fra et per tegn til et per buffer som blir printet.
	Må vurdere hva man skal bruke.
	![[Pasted image 20241108135143.png]]

## DIsks
- Hardisker brukes osm sekundert minne
- De lerser og skriver like raskt
- Magnetiske harddisker er delt opp i spor som igjen er delt opp i sektorer
- Hardisk organisasjon er skjult av driverer som tilbyr virtuell organisering.
![[Pasted image 20241108135705.png]]
Formatering
	Må formateres slik at man kan bruke
	Hver sektor har
		-Preamble
		Data 
		ECC Error correcting code.
		Spor og sektor
**Cylinder skew
- For å forbedre ytelsen benyttes cylinder skew
- For hvert sport er sektor 0 litt forskjøivet i forhold til sporet før.
- Dette fører til at vi ikke må gå en hel runde rundt uten å få lest noe.
Interleaving
- På samme måten kan det å lese en flere sketorer etter hverandre også by på problemer
- leser en ssektor og skal sjekke om det er feil
- bruker for mye tid på en lese en sektor.
- Derfor brukes interleaving.
**Disk arm scheduling algorithms**
- Time required to read or write a disk blcock determined by 
- 1. seek time
- rotational delay
- eactual transfer time.
- Seek time dominates
- Error checking is done by controllers.

- First come first serverved FCFS
	- Fram og tilbake med seeks, treg
- Shortest seek first SSF
	- Går til nærmeste, kan bli starvation.
- Elevator.
	-Opp og ned tar alle.

Error handling
- Når disker blir lagd er det noen Bad sectors.
- Hvis feilen er liten kan kanskje ECC rette den opp.
- Hvis den er alvorlig må enten controlleren eller operativsystemet ta seg av edn.
- ![[Pasted image 20241108140232.png]]
- Controlleren fysisk på disk
- Operativsystemet gjør det i software
	- Lager liste over sectorere som er bad som skjules for alt og alle slik at ingen bruker de sektorene.
