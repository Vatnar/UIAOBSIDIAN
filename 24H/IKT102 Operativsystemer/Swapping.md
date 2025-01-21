![[Pasted image 20241018131535.png]]
	Flytter hele prosesser
	Flytter du den inn og ut, får du små hull. 
	Memory compactation man presser prosesser nedover får  å ikke få hull
	Hvor my minne, fast eller dynamisk.
	![[Pasted image 20241018131803.png]]
	To måter
		Bitmaps
		![[Pasted image 20241018131845.png]]
		![[Pasted image 20241018131853.png]]
			En hvis opptatt, 0 hvis ledig.
			Bitkart over minneområdet.
			Må lese gjennom bitmap for å se hvor det err plass for en ny prosess.
		Linked list
			Liste med prosessene om hvor de starter og hvor lange de er. 
			Må oppdateres hver gang en ny prosess starter eller slutter.
			First fit
				Søker gjennom listen og finner det segmenetet som passer
			Next fit
				Søker gjennom listen til han finner segmentet som passer og fortsetter derfra neste gang
				- LItt dårligere en nfirst
			Best fit
				Søker gjennom listen for å finne det segmentet som passer beste.
				Dårlig utnyttelse av minnet mange smp hull fragment
			Worst fit 
				Finner det segmentet som passer dårligst
				Får større hull osm kan være nyttige.
			Begge er tregere en first fit.
			Kan lage to lister.
			Kjappere allokering av minne, men man må oppdatere listene når man tar bort fra minnet.
			Sortering av listene best fit raskere.
				Quick fit
					En liste for de vangliste, veldig kjapp algoritme, vanskelig å slå sammen hull