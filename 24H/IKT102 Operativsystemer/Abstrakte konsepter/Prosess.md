Program: En eksekverbar fil.
Proessess: En forekomst av et program under eksekvering
##### Prosess
- Prosessmodellen er basert på 2 prinsipper
	- Ressursgruppering og eksekvering
Ressursgruppering
	Address space MINNE
		Data 
		Text
	Andre ressurser
		Åpne filer
		Child prosesser
		Pending alarms
		Signal handler
		+++
	Letter å gruppere dem i en prosess.
	
Process Thread of execution
	En tråd som holder styr på hva som skal eksekveres på CPU
	Thread
		Minne som ligger i register for tråden.
		Program counter - Hvilken instruksjon skal eksekveres neste.
		Registre - Inneholder nåværeende variabler
		[[Stack]] - Inneholder eksekverings historien 
		State - Inneholder status informasjon.
	Tråder er enhetene som kjøres/utføres på CPUen

[[Prosesser og tråder]]
[[Minne fysisk]]
[[Concurrency IPC]]
[[Scheduling]]
