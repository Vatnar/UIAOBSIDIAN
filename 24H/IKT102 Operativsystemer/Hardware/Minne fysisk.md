[[Minne]]

burde være ekstremt kjapt, uendelig stort og ufattelig billig. Er ikke sånn. 
		I et 32 bits system hvor mange mb kan en prosess få til minneråd? Maks 4.2GB.
		Pga dette innførte man 64 bit. 
		Minnehierarki
			<1KB Register 1nsec
			1 MB Cache 2nsec, 
			Main memory Ram 10nsec
			Magnetic disk 10 msec
			Magnetic tape 100sec.
Minne er delt mellom flere programmer for å utnytte cpuen bedre
		To problem
			Hvordan beskytte programmene fra dem alle og hvordan beskytte kjernen
		Program [[Prosess]] som starter alltid fra adresse 0 og går oppover.
		Når programmet kjøres så bestemmer Opsys hvor i minnet programmet er og det er aldri fra adresse 0 i det fysiske minnet.
		Bruker hardware løsninger.
		2 Essentielle ting
			Cache skjuler at minne ram er tregt i forhold til CPU.  Men hvis man bytter [[Prosess]] er cache full, så man må bytte ut. Må skifte alle registrene. Dette tar tid og kalles [[Context Switch]]. 
		[[Base register  limit register]]
[[Prosesser og tråder]]		