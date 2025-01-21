- Enhver prosess trenger et minneområde  lagre dataen instruksjoner på
- Det blir satt av et x antall MB/GB stort minneområde
- Hvis de trenger mer minne kan det bli utvidet. Enhver prosess tror de har minnet for seg selv.
**Parkinson's law** Programs expand too fill the memory available to hold them. 
Nå $2^{64}$. 
Ultimate minnet [[Minne fysisk]]
Løsningen 
- Minnehierarki
	Flere nivåer der det på toppen er lite superkjapt minne 
	Under er det mer minne mmen mindre raskt
	![[Pasted image 20241011134752.png]]
	Toppen registere som ligger på CPU. Cache har vi L1 L2 L3 osv. 
	L1 er direkte på kjernen til CPU, L2 er delt mellom Kjerner, L3 mellom alle CPuer.
	Main Memory er RAM.
	Hvor befinner prosessen seg? 
		Er i RAM eller harddisk. Deler den seg opp i cache,  har ikke plass i registerert. Liten del i register, noe cache, alt i main memory hvis plass, hvis ikkke harddisk. 
		Blokkert: Ikke i register. Vil prøve være så langt opp som mulig. Mest sannsynlig i main memory. 
		Klar: Så nærme så mulig registeret så mulig. Kanskje L2 eller L3 cache.
Memory manager
	Hvilke deler av minner er /ikke i bruk
	TIldele minne til prosesser
	Swappe minne mellom RAM og hardisk når det ikke er nok til å halde alle prrosesser
Basic maemory management
	Monoprogrammering without Swapping or  
	paging  
	• Multi Programming with fixed partitions  
	• Modeling multiprogramming  
	• Relocation and protection
	Kan dele minneadministrasjonssystemene  
	opp i to  
	– De som bruker swapping og paging  
	– De som ikke gjør det  
	• Swapping og paging blir brukt fordi vi ikke  
	har nok minne
Virtual memory på harddisk. 

Memory swapping: Memory manager flytter minne ned til disk fra RAM siden RAM ikke har plass til å holde minnet.
