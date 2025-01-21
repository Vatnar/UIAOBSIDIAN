Hva er et operativsystem, hva er hovedfunksjonene og hvorfor er OS så viktig å ha i en PC:
	 Resource manager, extended machine.
	 Funksjoner: Process management, Memory management og file management og IO management. 

Dele opp i avsnitt.
kan skrive stikkord hvis man har dårlig tid.


Forklar grundig hva en prosess og tråd er og hva er forskjellen mellom dem er. Hvorfor er en prosess det viktigste konseptet innen for operativsystemer?
	stack, osv.

Hva er forskjellen mellom monolittisk og mikrokernel, Fordeler og ulemper.

HDD vs SSD
	Seek time rotation delay, trasnfer time, cylender skew, Virtual organization intearleaving.
Race conditions.
Mutex.
 minnehirerarkiet: nonVolatile og volatile
 
Multiprosessering: Multiprogrammering:
Paging vs segmentering:
- Programmerer må ikke være klar over paging, men må på segmentering.

### Spørsmål
FAT vs EXT:
	file allocation table, ikke om EXT siden vi ikke har vært inne om det.
Multiprogrammering vs multiplexing:
	Flere prosesser i minnet samtidig. Multiprogrammering er en multiplexing teknikk. 
Inline vs Heap I-nodes
	ikke tenke så mye på..
	Tenk heller inline og heap som konsept.
MBR 
	Aktuelt for eksamen, BIOS. kan være relevant å nevne UEFI. med GPT.
device independent OS
	Kjøre alle slags mulige enheter, ulike produsenter. Grensesnittet mellom OS og enhetene. Drivere er grensesnittet som gjør det device independent. CPU arkitektur er ikke device independent. men IO device drivere er det. Linux og windows, OSX litt mer tilpasset. 
Microkernel vs Monolittisk:
	Monolittisk, alt OS funksjon i kjernen, Mono en kjerne, micro minst mulig i kjernen, og heller ting i brukermodus. Systemprosesser med priviligierte rettigheter. MIcrokernel, scheduling funksjonalitet, og kommunikasjon.
Hva er forskjellen på lage i "layered kernerl"?
paging og segmentering samarbeid?
	Ulike segmenter i prosessene, samarbeidet. Segmenting må man vite om. 
	Kan bruke paging på segmentering for å løse med fast størrelse.
	Forskjell: 
	eller spesifikt. 
barriers
	Metode for å sørge for at prosesser stopper på et riktig tidspunkt. For å synkronisere.
	Matriseregning.
Hva er race conditions:
	Konkurranse, synkroniseringsutfordring. Jobber på samme delt ressurs uten at de er skilt i fra hverandre. Kritisk seksjon i kode. Plusse x begge to, annen skal gange x. Kommer an på når de leser og når de skriver. Endrer resultatet.
Interrupt handler
	forstyrre CPU, du må håndtere. 
	ofte IO enheter. Istedenfor at den hele tiden venter på en harddisk, så sier den til harddisk, finn blokken, interrupt meg når du er ferdig. Interrupt dreven IO.
	Har også DMA, direct memory access. Som CPU kan programmere for å hente så så mange blokker. osv. En interrupt istedenfor for f.eks 10.
Forskjellen på en tråd og en prosess:
	Gruppere ressurser. Prosess.
	Utføre kode, thread of execution. Tråd.
	Flere tråder som utfører kode på samme grupperte ressurser. Tråder har samme addresseområde. Ulik stack siden det er eksekveringen.
Bruk metaforer og eksempler. Pass på å ikke misforstå.
Vil en åpen fil være en delt ressurs eller en privat ressurs mellom trådene i en prosess?
	Prosess samler ressursene, dermed deler alle trådene samme fil. Synkroniseringsutfordringer.
Interrupt kontroller/prosedyrer
	 Får interruptsa fra IO, hver interrupt er koblet til en prosedyre. Da peker interrupt til en prosedyre. Så går den tilbake, eller en annen prosess basert på scheduleren.Interrupt Vector Table.
Mutex:
	Mutex er en binær semafor. Kun verdi 0 eller 1. Den tråden som låser mutexen 
	Betingelser
	1. Atomisk operasjon, ikke får race conditions. OS må skru av interrupts.
Minnehierarki:
	RAM random access. Er bare en liten del. Det misnste på toppen, jo mindre jo raskere,  er registre, så cache L1 L2 L3 L4, så kommer RAM, alt over er Volatile. Deretter kommer HDD, som kan bruke VRAM. SSD Magnetisk disk osv.
	Hele prosessen er ikke i registrene samtidig, bare en liten del. Større del på cachen, også resten i RAM, men hvis ikke nok, kan noe ligge på HDD. Paging og Swapping gjør dette.
PCB vs process table: M.2
	Prosess table er tabellen der alle PCB ligger.
RAM vs ROM:
	random access memory, standard minne. ROM er read only, kan brukes for oppstart osv. Ikke spørsmål.
data (bss), stack, text
	text er programkode, data er variabler, stack er eksekveringshistorikk.
Heap: 
	Haug,
	eller inline, Heap hiver på toppen og tar fra toppen.
IPC
	Intern process communication. Deadlock Race conditions, mutex, semafor osv.
PC
	Register på CPU som inneholder peker til neste instruksjon som skal utføres.
HDD vs SSD
	Søketid: alltid aktuelt, tar lengre tid på HDD. 
	Rotasjonsforsinkelse, skjer ikke på SSD, roterer ikke rundt. 
	Transfer time, tar litt tid å overføre. 
	Cylinder skew, nei. 
	Virtuell organisering av disk, alltid aktuelt,. 
	Interleaving, blokkene får mellomrom.
I-node
	Hvilken diskblokk fil er koblet til
	Hvis ikke nok, da er siste peker til en annen Inode, osv.
	Kun i minnet når den er i brok
	Inneholder metadata , filnavn skaper osv.
Drivere:
	koden som IO enheter må ha i OS for å kunne kommunisere med IOen. 
File descriptor:
	heltall som blir tilordnet en fil, 
Monitor vs mutex vs semafor? Tråder kjører på ressurser gjennom mutex og semfaroreer hva med monitor?
	Monitor er abstraksjon av det.
	Kjører gjennom monitor.
	Fordelen med monitor er at du kan kjøre flere betingelser på det.
Page page frame og page table.
	Prosessiden er page, page frame er fysisk, page table er liste over pages. OS har page table. Hver prosess har en page table, OS har en total page table for det som er i minnet.
Kommer
	Prosess, minne, fil og IO, 
Hvordan har tråder egen stack.
	Har egen eksekveringshistorikk.
MMu og page table
	Logiske minneoperasjoner, CPU må få oversatt adressene som prosess sender ut til fysisk. Så mmu må oversette. Page fault, da må pagen flyttes inn i RAM. CPUen kan aksessere RAM m
HOlde orden på blokker
	lenket liste og bitmaps.
Bruker character devices cycle stealing mens block devices bruker burst mode?
	Cycle stealing er når DMA lurer inn signaler inne i mellom CPU.
	Gir mening at man kan implementere det.
	Ikke tenk på det på eeksamen.
Interrupt
	Må skje modus bytte uansett, Så registrene må byttes. Men ikke context switch, men kan skje det.
Mapper inode
	Vanlig fil, mappe og fil er det samme.
	Ligger i preamble kode for å finne.
Monolittisk system er mest mulig effektivt, Mikrokernel er mer for at det skal være sikkert. Mer tid på mikrokernel, men sikrere. Monolittisk er raskere men sårbar.
