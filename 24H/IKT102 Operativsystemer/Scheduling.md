- Flere prosesser som sloss om tid på CPU.
- CPU er viktig ressurs, mye arbeid på å utvikle god rutiner for å skifte prosesser.
- For servere også videre enda viktigere.
### Prosess oppførsel
- CPU/COMPUTE BOUND og IO bound.
- Noen bruker lang tid på CPUen og kort tid på å vente.
- Noen bruker kort tid på CPUen og bruker mye tid på å vente.
Når man skal planlegge
- Mange situasjoner der man trenger å bytte prosess
- Ny prosess
- Avslutter
- Prosess blokkering, IO semafor.
All systems:
Fairness.
Policy enforcmement seeing that stated policy is carried aout. Balancing
**Batcj system:**
Througput, maximize jobs per hour
Turnaaround time, minimizre time between subimission and termination.
CPU utilization keep the CPU busy all the time.
**Interactive systems**
Response time.
Proportionality, meet users' expectations.
**Real time systems**
meeting deadlines - avoid losing data fabrikk også videre.
Predictability - avoid quality degradiation in multimedia systems. 


## Algoritme


Prioriteter applikasjon i fokus.

### Eksempel algoritmer
- First come first served
	- utført i rekkefølgen kommer
	- dårlig utnyttelse
- Shortest job first
	Non preemptive med kjente tidsintervaller for jobbene
	Velger den korteste jobben som er i køen først og så i stigende rekkefølge for de neste jobbene
	Gjør turnaround time mindre.
- Shortest time remaining time next
	preemptiv versjon av shortest time reimaning.
	Algoritmen velger alltid den jobben som tar kortest tid.
	Stor jobb blir aldri gjort
Three level scheduling. 
![[Pasted image 20241011131708.png]]
![[Pasted image 20241011131718.png]]
Round robin
	Hver prosess vil bli tildelt et tidsintervall på CPU
	Kort tidsintervall = mange bytter mellom prosessor og dårlig utnyttelse context switch
	lang dårlig response tid.
Priority
	Det blir avgjort hvilken prosess som er neste avhengig av priortet.
	Fikse inf loop: MInske prioriteten til kjørende prosesser, maks tidsintervall quantum, dynamisk og statisk prioritet.
Priority scheduling
	![[Pasted image 20241011131929.png]]
	![[Pasted image 20241011131938.png]]
	Shortest process next
		Kjøre den prosessen som har minst responstid.
		Estimerer hvilke prosesser detter er i forhold til tidligere oppførsel. Kalles noen ganger "aging"
Guaranteed Scheduling
	Gir brukere "lovt" tid
	1/n
Lottery scheduling
	Lotto!
	Kan gi ganske nøyaktige lovnader om hvor mye en bruker får.
	Bruker bonger som prosessene får en hver av så trkekker man fra dem.
	Prosesser med mer tid flere bonger.
	En ny prosess som får bonger kan kjøre med en gang.
	Samarbeidende prosesser kan utvekskle bonger
	Løse problemer som andre alrgoritmer har vasneklig å behandle. Videostreaming med forskjellig rate. 
	![[Pasted image 20241011132346.png]]
	
ALle tråder skal få en rettferdig del av CPUen. Det avhenger av system og bruk hva som er viktig g hvordan tid fordeles. Prioritet blir satt på tråder. Prioriteten bestemmer hvor i køene en tråd havener. Mulig å ha to eller flere prioritetskøer.
Mye av tiden går på context switch.
Avhenger av OS.
