- Ikke velge en side som er nylig brukt, siden deter sannsynlig den blir brukt snrart.
- Optimale er å skifte ut den siden som blir minst brukt i fremtiden. OPtimalt men urealiserbart.
- Estimat ved å logge tidligere bruk.
NRU
- Hver side har en referanse nbit, som referere forandringer.
- Bits blir satt når siden blir referert, modifisert
- Sidene er klassifisert etter dette.
Referert, MOdifisert
1. 0 0
2. 0 1
3. 1 0
4. 1 1
Hvis den er referert siste gang er det størrse sansynlighet at den bir brukt iigjen enn at den er modifisert.
FIFI
- First in first out. Lenket liste over alle sidene. Eldste går først ot.
- Sider som er lenge i minne kan ofte være mye brukt. FIFO er sjeldent brukt i ren form.
Second chance
- Lenked liste, sorteres i FIFO orden. Har den blitt referert ved siste klokkesyklus, ja så får du ny sjanse. Reference og modified bytt blir resettet.
Clock page replacement alogirthm.
Samme som second chance, men istedenfor å flytte tilng i en rettet liste bruker man en peker som flytter seg. 
LRU(least recently use)
- Anta at sider som nylig har vært brukt vil bli brukt igjen snart. Hvi ut sider som er ubrukt lengst.
- Må ha en lenket liste med sider som oppdateres ved hver referanse.
- Alternativt ha en teller i hver sidetabellinngang, velge side med den laveste verdi på teller. Periodisk sette tellere til null
- Få om noen maskiner som bruker det.
Kan simule i hardware, med .
LRU i software
NFU
- Har en software teller som teller 1 hver gang siden blir referert. Når en side skal skiftes ut taes den med laverste teller. Hvis enside ahar blitt burkt mye for lenge siden å er fremdeles telleren høy. 
AGING
- Modifisert NFU
- Har en teller hvor man skifter bitene til høyre før vi legger til R bitet.
- R bitet blir lagt til på venstere sdiden. 
Demand paging
- Maskiner basert på paging arkitektur i minner hat mulighet for å iimplemnentere demand paing.
- Henter bare det som trengs.
- Mye pagefuaults i starten, men mindre etterhvert.
Working set
- Det antall pages som en prosess har referert til et visst antall minenrefereanser n, N blir kalt vinduet i et working set.
- WOrking set er de sidene som har blitt brukt i løpet av de k siste minnereferenasne.
- Lastet inn i gjen
- Working set/Arbeidssett
• Et arbeidssett er en del av den totale
prosessen. Bruk av arbeidssett-algoritme
medfører vanligvis:
• Flere prosesser i minnet
• Høyere gjennomføringsgrad (throughput)
• Redusert swappingtrakk
![[Pasted image 20241025135521.png]]![[Pasted image 20241025135528.png]]
'![[Pasted image 20241025135611.png]]
[[Virtuelt Minne]]
