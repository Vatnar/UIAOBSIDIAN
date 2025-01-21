>[!tip] [[Minne]]
>- [[Swapping]] og [[Paging]]. (funnet opp fordi man ikke har nok RAM)
>	Men nå har de fleste nok ram, men brukes fremdeles paging fordi den har noen gode egenskaper.
>- Swapping flytter hele prosess fra RAM til harddisk fram og tilbake
>- Paging, deler av prosessen
>- Monoprogramming uten swapping og paging.
>- Minnet delt mellom programmet og OS, når et nytt program startes overskrives minnet til det forrige programmet. Sjeldent bruk i dag utenom embedded.
>- Fixed partisjoner med multiprogrammering
>	En prosess venter på io så kan en annen prosess kjøre
>	Prosessene kjører ikke hele tida, (IO BOUND, venter), hvor mange som kan være i minnet om gangen, må du se på hvor mye CPU utilization de har
>	![[Pasted image 20241018124244.png]]
>	![[Pasted image 20241018124256.png]]
>- Relocation and protection.
>	To problemer, relokasjon og beskyttelse.
>	Relokasjon
>		 hver prosess har forskjellig minneområde.
>		  Må finne en måte å finne ut hvilket minne som hører sammen.
>	Beskyttelse
>		Vil at programmer skal kun kunne lese fra sitt eget minneområde
>		Beskytte minneområdene fra hverandre
>		Paging hjelper til å beskytte mot dette, f.eks skrive fysisk adresse 0 som er OS.
>	Løsninger
>		IBM: De ga hver blokk en 4 bits beskyttelseskode, hvert program hadde en PSW program status word en 4 bits nøkkel. Hvis PSW og beskyttelsene ikke stemte ble den låst slik at OS kunne bestemme. Internt, i OS.
>		1. Utstyre maskinene med hardware registere base og limit. Baseregisteret legger til den verdien som partisjonen er på. Limitregisteret sjekke at forespørselen ikke er lengre en det partisjonen er. Ulempe tar mer tid. CDC 6600 første supercomputer brukte dette, men ikke i mye bruk nå. 
>- Adresser
>	Logiske og virtuell (virtuell på harddisk, små nyanser)
>		Referanse til et minne lokasjon som er selvstendig fra den nåværende oppgaven av data til minne.
>		Fysisk adresse må bli oversettes til virtuell. 
>	Relative
>		address på en måte som er relativ til en kjent lokasjon.
>	Fysisk
>		Absolutt adresse eller den faktiske lokasjonen i RAM

![[Pasted image 20241018131102.png]]


- Timesharing systems
	I disse systemene må prosessene bytte på minnet.
	De som ikke har plass må på harddisk
	Bringer inn prosessene i minnet dynamisk når de trengs
	To hovedmåter
		Swapping  (Hele prosessen)
		Virtual memory (deler av prosessen)
[[Swapping]] 

[[Virtuelt Minne]]

## Minnehåndtering take 2
