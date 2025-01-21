- Sentralt i moderne OS å administrere flere prosesser
	 Multiprogrammering
	 Multiprossessering
	 Distribuert prosessering
- Stor issue er [[Concurrency IPC]]
	Managing the interaction of all of these processes
- Tråder er avhengige av hverandre.
	konkurrerer om felles ressurs
	OS må styre dette samarbeidet og konkurranse.
	Samarbeid
		Når en tråd ber en annen tråd om et arbeid
	Må finnes mekanismer for synkronisering av trådene, samt å utveksle meldinger / signaler mellom trådene
	Konkurranse
		Flere tråder prøve å bruke / aksessere en ressurs
			To tråder prøver å aksessere samme enhet i en linket liste.
	Formel beskrivelse: "Mange tråder som kjører samtidig  har en kritisk seksjon. En kritisk seksjon er kode som  kan påvirke andre tråder og andre tråders gjøremål. En  må passe på at kun en tråd får kjøre hele sin kritiske  seksjon om gangen!"


**Viktige termer**
[[Atomic Operation]]
[[critical sections]]
[[Deadlock]]
[[Livelock]]
[[mutual exclusion OS]]
[[Race condition]]
[[starvation]]

IPC
	3 forutsetinger
	- Hvordan informasjonen blir sent mellom  prosessene  
	– At prosessene ikke kommer i veien for  hverandre under ”kritisk” jobbing  
	– Riktig ”sequencing” når det er avhengighet mellom prosessene
Murphys law: If something can go wrong it will.
prosesser må kommunisere, hvis de jobber sammen hvor begge kan lese og skrive kan vi får race condition.
[[Race condition]]
Occurs
- Multiple processes or threads read and write data items.
- They do so in a way where the final result  depends on the order of execution of the  processes
output depends on who finishes race last.
Hvis Pa holder på en ressurs Pb vil ha, må vi si at Pb må vente på Pa.
[[spooler directory]]
![[Pasted image 20241101132441.png]]
Debugging
- Ikke gøy å lete etter disse feilene.
- Oppstår sjeldent og er vanskelig å finne
- Er det noe problem da???
	atomkraftverk f.eks. 
-
What design and management issues are raised by the excistence of Concurrency?
OS must
- Keep track of various processes
- Allocate and de-allocate resources
- Protect the data and rresorurces aginst intereference by other preesses.
- Ensure that processes and outputs are independent of processing speeds.
![[Pasted image 20241101134357.png]]
Når det er konkurranse mellom prosesser for ressurser
- Trenger [[mutual exclusion OS]] 
	[[critical sections]]
	Ingen prosesser som stopper på utsiden av kritisk fase må kunne blokkere for andre prosesser.
![[Pasted image 20241101134708.png]]
![[Pasted image 20241101134717.png]]
Forslag for å løse Race Condition  
• Mutal Exclusion with busy waiting  ( er vi framme er vi framme osv.)
	– Petersons’s solution  
		Slå av interrupts 
			Slå av interrupts så det ikke skjer [[Context Switch]] i en kritistk fase. Ikke gi dette til vanlig prosess, men gi til OS eller kjerne
		Lås variablen
			Setter en variabel til 0 eller 1. Tester på variable. Hvis 1 blir ekslkudert, Samme som med [[spooler directory]]
		Strict alternation
		![[Pasted image 20241101135105.png]]
		Pettersons løsning
			![[Pasted image 20241101135055.png]]
			![[Pasted image 20241101135119.png]] Problemet med dette er bruker busy waiting, sløser med cpu, kan få uventa problemer, 
• TSL Instruction (Test and Set Lock)  
• Sleep and Wakeup  
	Sleep and wakeup system kall som blokkere i plassen for å bruke busy waiting. 
	Producer - Consumer problem  
– Producer legger til i bufferet og consumer tar ut.  
– Hvis det er fullt så går producer i søvn og motsatt hvis det er  
tomt går consumer i søvn  
– Så sender den motsatte part en melding til den andre om at den  
må våkne  
• Får samme problem som med [[spooling]] directory  
– pga meldinger som går tapt  
– Kan løses med å teste på en bit, men man må lage et bit for alle  
forskjellige tråder som er aktive!

• Semaphores  [[semaphore]] Strong semaphores
	Ikke-negativt tall. Tråder kan bruke semaforer ved å utføre to operasjoner. Wait down eller signal eller up. Trådene vet ikke om hverandre eller om semarofren, bare dens navn.
	Wait down, minsker semafor med 1 hvis semafor er større en 0. Er semafor lik 0, settes tråden i ventekø. Signal(up) øker semaforen med 1, hvis semaforen er større en 0. er semafor lik 0, "vekken" en tråd i ventekø. Er det ingen flere tråder i ventekø økes semaforen til 1. 
		Øke og minske verdien på seg selv. Samarbeide med planlegger hvilken tråd skal få CPu tid. Kontroll på trådene som venter. Alt må gjøres uavbrutt, en udelelig operasjon atomic action. Fletere tråder kan ikke operere på en semafor samtidig. Et signal kan være 20 30 maskininsturksjoner. Problem, en tråd kan miste CPu midt i et signal.
		![[Pasted image 20241101135455.png]]
		
• Mutexes  weak semaphore [[Lock - Mutex]]
	En forenklet semafor
	Når man ikke trenger å tell hvor mange som er inne i et kritisk moråde. Enten 0 eller 1.
	Velger vilkårlig fra de i ventekø.
	Gode til å håndtere ekslkludering fra delte ressurser eller delt kode.
	veldig effektive å bruke og passer dermed bra i userspace. Kan brukes som programmerer.
	![[Pasted image 20241101135941.png]]![[Pasted image 20241101135949.png]]
Semaforer begrensinger.
- Der er ikke pålagt, en programmer kan velge å delvis ikke bruke de.
- Feil bruk fører til deadlock
- Lavprioritetstråder kan få ekslklusiv rett på en ressurs og dermed holde den gjømt for en høypriorirets tråd.
- Semaforer kan ikke utveklse data mellom tråder
- En blokk kan ikke ha en timout
- Man kan ikke spesifisere venting på to eller flere  
semaforer ved bruk av AND/OR-tilstander.

• Monitors  
- Laget for å lage data abstraksjoner og for å gjemme data.
- Inneholder felles data og en eller flere av dens funksjoner.
- Kritiske seksjoner ek un akssesserbar indirekte igjennom monitor (C# og Java har det)
- Kjøring av kritiske seksjoner og data-deklarasjon skjer via monitoren.
- Kan derfor oppleve kort pause
- 
• Message Passing  
	Kombinerer datautveksling med gjensidig utelukkelse og synkronisering.
	En fikk det vi kaller strukturert meldingsutveksling.
	Operativsystemet tilbyr å sende meldinger. Synkronisering mellom de to trådene og en kø hos mottaker.
	Trådene snakker aldri med hverandre, men trådene tar iniativet som OS tar hensyn til.
	Kan sende meldinger synkront eller asynkront.
		Asynkront
		- Sendertråden må aldri vente
		- Operativsystemet tilbyr en kø hos mottaker
		Synkront
		- Begge trådene må i synk
			- Man trenger ikke å administrere en felles buffer
			- Mottakertråden må være klar og ventende, og kan dermed bklokkere andre tråder.
• Barriers
	Blir brukt på grupper av prosesser.
	Vil si at en prosess som kommer til et  punkt må vente til de andre prosessene  den er avhengig av når samme punkt  
	For eksempel en stor matrise der man  bruker parallelle prosesser for å kalkulere
	Deadlock  Stavation