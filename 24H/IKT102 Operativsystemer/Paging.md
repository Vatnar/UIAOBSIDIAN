Paging
		MOVE REG 1000 så blir inneholdet i adr 1000 kopiert i REG. Program generert så virtuell
		Virtuell adresseområde.
		Hvis ikke virtuelt minne hvil den virtuella dressen sendt direkte ut på adressebussen for å finne fysiske minnet.
		Ved virtuelt minne går denne adr til memory management unit MMU som mapper den virtuell adr. til fysisk adr.
	Pages
		 Virtuelle adresseområdet delt inn i Sider eller pages 
		Den tilsvarende enheten i fysiske minnet kalles page frames.
		Pages og pageframes har alltid samme størrelse.
		Vanlig størrelse er 512 bytes til 8 K
		En maskin som genrerer 16 bits adresser kan ha et virtuelt minne fra 0 - 64 K
		Med et fysisk minne på 32 K vil vi ha 
		- 16 virutlle sider a 4K
		- 8 siderammer a 4K.
	Virtual memory paging.
	![[Pasted image 20241018134517.png]]
		![[Pasted image 20241018134535.png]]
		0-64K ligger virtuelle pages. Det fysiske minnet med page frames har 0-32K. 0k-4k i fysisk ligger lagra på 12k-16k
		Forbindelesen mellom virtuelle adresser og fysiske skissert i en sidetabell
Page table
	Hver prosess har sitt eget page table, hvert sitt virtuelle adresseområde.
	Virtuelle adr. blir oversatt til fysisk i page table.
	To problem
		Page table kan bli utrulig stor.
		Oversetting må utføres kjapt
	To enkle løsninger
		En page table + hardware registre
		Hele tabellen i minnet.
	![[Pasted image 20241018134832.png]]
	Caching disabled må den lagres ned med engang.
	Den har referenced bit, (har blitt lest, ikke forandringer), modified bit (endringer), beskyttelse, for hver enkel page ligger det beskyttelseskode som må være overens med prosessen som spør . Present absent bit, i fysiske minnet nå, eller på hardisken. LIgger på RAM eller VRAM(hardisk).
Paging systemet
	1. Swappe sjeldent brukte pages
	2. Håndtere gyldige page fault
		Page fault vil si å stoppe prosessen og få lest inn den eller de sidene som prosessen referer til og som IKKE befinner seg i arbeidsettet, slide 80.
[[TLB]]
[[Sideskiftsalgoritmer]]
