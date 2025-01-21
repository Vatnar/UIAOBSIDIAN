**Relaterte temaer**
[[Deadlock]]

Program: En eksekverbar fil.
Proessess: En forekomst av et program under eksekvering

En datamaskin kan gjøre mange ting på en gang
 Men en CPU kan gjøre en ting om gangen (hvis vi ser bort fra dagens nyutvikling da)

Tidligere kunnskap
Computer platforms consist of a collection of hardware resources. Computer application are developed to perform some task. It is inefficient for applications to be written for just onne hardware.
OS provides an interface for applications to use. OS provides a representation of resources that can be requested and accessed by processes. 

#### Hva kan jeg om prosess
Et program er en prosess. En prosess har et formål som den prøver å oppnå. Bruker ressurser som den får tildelt fra OS. Når en prosess kjører må den være i RAM [[Minne fysisk]]. En prosess har et address space. Program Status Word. 

### Opsys
Program: En <span style="color:rgb(192, 0, 0)">eksekverbar</span> fil.
Prosess: En forekomst av et program under eksekvering
Brukerprogram kan manipulere prosesser gjennom systemkall til op.sys(kjernen)
- Starte nye prosesser
- Avslutte prosesser
- Synkronisere prosesser
- Kommunisere mellom prosesser. 
Alle program kjører ikke i kjernen. Men det er ett program som kjører i kjernen (opsys.)


Fordel med flere tråder, betyr at resten av trådene i prosessen kan fortsette selv om en stopper.

> [!IMPORTANT] ### <span style="color:rgb(192, 0, 0)">Viktige ting en prosess har</span>
> 
> - Address space
> 	Minne som prosessen kan lese og skrive til 
> 	Inneholder det eksekverende programmet, programdata og stack.
> Registre (Trådene har dette)
> - Program counter
> - Stack pointer
> - Andre registre

Trådene må holde seg innenfor prosessens adresseområde. Når den ikke jobber mot sitt eget adresseområde må den spørre operativsystemet om å gjøre det for han (SYSTEMKALL.)


Prossesens 3 segmenter.
Kode, Data, gap, Stack. Gap plasss til å vokse

Bake en kake
	Forskjellen mellom et program og en prosess kan illustreres best med et eksemepel
		Halvard bakrer kake
			Kake oppskrift - program
			Halvard - CPU
			Ingrediensene - Inputdata
			Aktiviteten med å hente ingredienser, mikse dem sammen osv er prosessen. 
	Prosess er en aktivitet, program er oppskriften.
	Husk at under prosessen kan det skje ting som ikke står i Programmet. 


> [!TIP] ##### <span style="color:rgb(0, 176, 80)">Viktigste elementet - Process Control Block [[PCB]]</span>
> 
> - Lagrer info om prosesser.
> En PCB per prosess som ligger lagret i en prosesstabell i Operativsystem adresseområdet.. Prosesstabellen lagrer PCB-er. 
> 	-Contains the process elements
> 	Created and manage by the operating system
> 	Allows support for multiple processes
> 	It defines the state of OS.
> 

**Multiprogramming**.
- CPUen bytter mellom forskjellige prosesser. Time slices. Prosessen får ikke kjøre så så lenge.
[[Scheduling]] og [[Context Switch]]



**OP sys prosessmodell**.
OS control tables, har en pcb for hver process.  Process image er adresse omrdåe som ligger i OS control tables. 
Kan være Process management, Memory management og file management.  

> [!NOTE] Modes of exectution..
>
> 
> MOst processers support at least two modes of exectuion.
> - User mode - Less privilieged mode. User programs typically execute in this mode. Their own varaibales.
> - System mode - more priviliged. Kernel of the operating systems.

When user mode processes needs to e.g expand their memory they request the opareting system for access to kernel mode (system mode). The transition is initialised by a system call. 
''

> [!important ] Switching Processes
> 
> - Serveral design issues are raised regarding process wtiching. 
> - When to switch
> - giving os controll.
> 
> Mechanisms. 
> Interrupts, External to the exectuion of the current instruction. Reaction to an asynchronous external event. Hard drive done, user input.
> 
> Trap. Assosiacted with the execution of the current instruction. Handling of an error or an exception condition. Skjer med den nåværende prosessen n/0. 
> 
> Superviosr call. Explicit request. Call to an operating system function. Prosessen spør om å bytte modus til OS gjennom system kall. 

>[!tip] Process Thread States
>- running
>- ready 
>- blocked

[[Is the OS a Process]]?


Processer har resurceownership og scheduling execution.
Disse to karakteristikkene er behandlet uavhengig av operativsystemet. 

- The unit of dispatching is referred to as a  
thread or lightweight process  
- The unit of resource ownership is referred  
to as a process or task
![[Pasted image 20240920131956.png]]
Må ha en oversikt på trådene sine i en slags trådtabell. 
Pending alarm, klokke, sender interrupt, og sier nå har det gått så lang tid. Nå ringer klokka.Tidsbasert interrupts. 

Tråd kan sees som en uavhenging program counter innenfor en prosess. Hver tråd har ikke sitt eget adresse område men innenfor  prosessen sitt adresseområde. 
![[Pasted image 20240920132306.png]]
Multithreading. Thread control block per tråd og user stack og kernel stack per. For å kunne bytte mellom trådene. Som i PID har man TID. THread iD.

Flere tråder brukes for å gjøre flere ting på en gang.
Kan sammenlignes direkte med en prosess.  Tråden deler ressursene som prosessen har. Prosessen deler ressurserne som datamaskinen har.
Tråder er ikke så uavhengige som prosesser
De deler samme adresseområde.
Kan det føre til problemer.
Synkronisering. Overskriving av variabler før lesing osv. 
- En tråd kan lese, skrive, eller slette en annens tråds stack.
- Det er ingen bneskyttelse mellom tråder
	Det er umullig
	det skulle være unødvendig (man skriver ikke et program som ødelegger for prgrammet.)
- Tårdene deler de samme åpne filene, child processes, alrams, signals, osv.
- Vi vil at vi kan ha flere tråder som kan eksekvere samtidig og kan dele ressurser. 
Hver tråd har sin egen stack. En stack er per tråd. Prosessen starter med en tråd, som kan lage nye tråder. veldig likt prosesser. OS har oversikt over prosesser, prosessen har oversikt over tråden.
Tråder har ingen klokke interrupt. Trådene må gi frivillig opp CPUen av og til for å gi andre sjansen til å kjøre. Kan også vente på andre tråder. 

![[Pasted image 20240920135026.png]]
![[Pasted image 20240920135040.png]]
![[Pasted image 20240920135114.png]]
 Kortere å bytte mellom tråder enn prosesser. Trenger ikke å lagre og bytte adresseområdet. Registrene må byttes, men du slipper å bytte hele adresseområdet. 

Eksempel på thread usage. ER word processsor med en tråd for keyboard, en for word processor og en for autosaving til disk. 

**Tråder i brukersmoud**
kan med letthet implementeres i alle systemer til og med de som ikke støtter tråder. 
Trådene må en egen trådtabell.
Lik prosesstabellen med programcounter stack pointer osv.
Ingen trap, ingen context switch. Tar mindre plass

Du bruker tråder mest der du skal blokkere med system kall. f.eks I/O. 
Tråder i kjernemodus
Ulemper: blokkerende system kall. Da stoppes hele prosessen. 
Page faults er også et problem.
Hvis trådene ikke gir fra seg CPu kan den kjøre hele tiden. Eksempel WINDOWS. 