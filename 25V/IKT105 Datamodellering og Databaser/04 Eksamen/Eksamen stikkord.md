Generell  
<span style="color:rgb(255, 0, 0)">(Projection (Rader))  
(Selection (Kolonner))  </span>
(Kryssprodukt Tabeller + betingelse for rader)  
(Algebra (nei det kommer ikke på eksamen))  
Normalisering:  
1, 2 og 3 NF  
Normaliser til du blør denormaliser til det virker  
Primærnøkkel Foreign Key  
Relasjoner(1:1, 1:m, n:m)  
(Funksjonell avhengighet/transisativ avhengighet )  
Tabell fra 1NF til 2 og eller 3 NF  
Ingen normalform  
Skjønne PilOppgaver  d
Tekst til normalform Tekst til tabell?  
<span style="color:rgb(255, 0, 0)">Kandidatnøkkel  ( MINIMAL SUPERNØKKEL)</span>
Surrogatnøkkel(løpenummer?)  
<span style="color:rgb(255, 0, 0)">View  </span>
Modellering  
Notasjon(Kråkefot (<span style="color:rgb(255, 0, 0)">NIAM)</span> Maksimum/minimum Relasjoner(1:1, 1:m, n:m)  
Objekt(entitetet/MySQL entitet) modell  
Lage datamodell(fra tekst) - 1 Objekter 2 Relasjoner 3 Attributter  
Bestemmer nøkler  
Tabeller  
Ta forutsetninger hvis du føler det er nyttig  
Objektifisering(Koblingsobjekt(tabell))  
SQL  
Select*, From*, Where, Group By, Having, order By Må være med  
Create/insert Into Kanksje generelt i et flervalgsspørsmål  
Insert/Delete/Update kan være aktuelt i forhold til flervalg sannsynligvis  
Insert/Delete/Update uten en where gjelder dette alle rader i tabellen  
Tabell med spørsmål om resultat (select(/delete/update))  
SUM/MIN/MAX/COUNT/AVG aggregatfunksjoner gjerne i sammenheng med Group By  
Group By (typisk for hver enkelt et eller anne eller lignende + aggregatfunksjon)  
Koble flere tabeller (Tabel1 + tabell 2 = Where fremmednøkkel + Primærnøkkel som  
oftest)  
Natural join/innerjoin bruk Where på eksamen!!! (dere som er 100% sikke rpå join er  
det ok)  
Betingelser for rader WHERE  
Bruke tabell navn hvis flere tabeller  
Group By Brukes ALLTID hvis man skal ha HAVING  
HAVING Betingelse for gruppe. Det som det grupperes på.  
<span style="color:rgb(255, 0, 0)">Generell teori  </span>
Tabeller, rader, <span style="color:rgb(255, 0, 0)">kolonner med assosiasjoner  </span>
Relasjoner(1:1, 1:m, n:M)  
<span style="color:rgb(255, 0, 0)">Relasjonesdatabase definisjon  </span>
<span style="color:rgb(255, 0, 0)">Andre ord og uttrykk for Databaser  </span>
Transaksjoner  
Operasjon  
<span style="color:rgb(255, 0, 0)">Tilstand  </span>
<span style="color:rgb(255, 0, 0)">Transaksjon(definisjon)</span>

Logg  
<span style="color:rgb(255, 0, 0)">ACID</span>  
<span style="color:rgb(255, 0, 0)">Serialiserbar  </span>
<span style="color:rgb(255, 0, 0)">Recovery  </span>
<span style="color:rgb(255, 0, 0)">Undo/Redo  </span>
<span style="color:rgb(255, 0, 0)">Logg  </span>
Andre  
<span style="color:rgb(255, 0, 0)">trigger  </span>
<span style="color:rgb(255, 0, 0)">Prosedyre  </span>
<span style="color:rgb(255, 0, 0)">View  </span>
Er noe mer, men kom ikke lenger nå... Hvis dere har kontroll på dette så bør det  
holde til minimum en C sannsynligvis en B. A bør ha enda litt brede kunnskap
 
<span style="color:rgb(255, 0, 0)">TRIGGER</span> 
Hva er en trigger i databasesammenheng, hvorfor og hvordan kan man bruke triggere i databaser?
<span style="color:rgb(255, 0, 0)">UNDO/REDO</span>  
FOrklar Recovery, algoritmen Undo/Redo, hvorfor den er mest brukt?

B+
# Prinsipper for oppbygging av et B+ tre

Et **B+ tre** er en selvbalanserende trestruktur som brukes primært i databasesystemer og filsystemer for effektiv lagring og søking i store datamengder. Det er en variant av B-trær, men skiller seg fra disse ved at alle faktiske dataverdier er lagret i bladnodene, mens interne noder kun lagrer søkenøkler. Denne strukturen gjør B+ trær spesielt godt egnet for systemer med høy I/O-belastning, som disklagring.

---

## Grunnprinsipper

### Orden og Kapasitet

- Et B+ tre av orden mmm har maksimalt m−1m-1m−1 nøkler i hver node og opptil mmm pekere til undernoder.
- Minimum antall nøkler i en ikke-rot-node er ⌈m/2⌉−1\lceil m/2 \rceil - 1⌈m/2⌉−1, og minimum antall pekere er ⌈m/2⌉\lceil m/2 \rceil⌈m/2⌉.
- Roten kan ha færre nøkler, men skal alltid ha minst to pekere dersom den ikke er en bladnode.

### Hierarkisk Struktur

- Treet består av interne noder og bladnoder.
    - **Interne noder:** Inneholder kun søkenøkler og pekere til undernoder, men ingen faktiske data.
    - **Bladnoder:** Inneholder alle dataelementer eller pekere til data, samt en peker til neste bladnode, noe som muliggjør effektiv sekvensiell traversering.

### Balansert Struktur

- Treet er alltid balansert, noe som betyr at alle bladnoder er på samme nivå.
- Høyden på treet er derfor lav, selv for store datamengder, som gir rask tilgang med en tidskompleksitet på O(log⁡n)O(\log n)O(logn).

---

## Oppbygging av B+ tre

### Innsetting

1. Finn riktig bladnode ved hjelp av søkealgoritmen.
2. Sett nøkkelen inn i sortert rekkefølge.
3. Hvis bladnoden er full, splittes den:
    - Midtnøkkelen flyttes opp til foreldrenoden.
    - To nye bladnoder opprettes med jevn fordeling av nøklene.
4. Hvis foreldrenoden også er full, repeteres splittingen oppover i treet.

### Sletting

1. Finn nøkkelen i riktig bladnode.
2. Slett nøkkelen og oppdater pekere.
3. Hvis slettingen fører til for få nøkler:
    - **Låne fra nabonode:** Flytt en nøkkel fra en nabonode til den underfylte noden.
    - **Fusjon:** Slå sammen noden med en nabonode og trekk en nøkkel fra foreldrenoden.
4. Hvis roten tømmes, kan trehøyden reduseres ved å fjerne roten.

### Søking

- Start i rotnoden og følg pekere til riktig undernode basert på søkenøkkelen.
- Gjenta prosessen nedover til en bladnode er nådd.
- Søk i bladnoden for å finne nøkkelen.
- Tidskompleksiteten er O(log⁡n)O(\log n)O(logn).

---

## Fordeler med B+ trær

- **Høy ytelse:** Søking, innsetting og sletting har kompleksiteten O(log⁡n)O(\log n)O(logn).
- **Effektiv sekvensiell tilgang:** Bladnodene er koblet som en lenket liste for rask iterering.
- **God diskoptimalisering:** Store noder reduserer antall disktilganger.
- **Balansert tre:** Alle bladnoder er på samme nivå, noe som gir rask tilgang.

---

## Konklusjon

B+ trær er en robust og effektiv struktur som er ideell for databasesystemer hvor store 
datamengder må lagres og hentes raskt. Den balanserte naturen, sammen med en struktur som er 
optimalisert for disktilgang, gjør at B+ trær er det foretrukne valget i mange modern
databasesystemer, som for eksempel MySQL og PostgreSQL.
![[B+-tree-remove-61.png]]



**Tapt oppdatering** skjer når to eller flere transaksjoner leser samme data og deretter oppdaterer det, men den ene oppdateringen overskriver den andre. Dette skjer ofte i miljøer uten skikkelig transaksjonskontroll eller låsing.

**Inkonsistent analyse** oppstår når en transaksjon leser data som er midlertidig inkonsistente på grunn av en annen pågående transaksjon som endrer dataene samtidig. Dette kan føre til at en transaksjon får et feil bilde av dataene.

Så forskjellen er:

- Tapt oppdatering: En oppdatering blir overskrevet av en annen.
- Inkonsistent analyse: En transaksjon leser inkonsistente data mens en annen transaksjon pågår.
![[btree-6.png]]

# Locks
**Optimistisk låsing** og **pessimistisk låsing** er to strategier for å håndtere samtidighet i databaser.

---

### 🔒 **Pessimistisk låsing**

- **Filosofi:** "Forhindre konflikter før de skjer."
- **Hvordan:** En transaksjon låser data før lesing eller skriving, og andre transaksjoner må vente.
- **Brukes når:** Det er høy sannsynlighet for konflikt mellom samtidige transaksjoner.
- **Eksempler:**
    - _Eksklusiv lås (WRITE LOCK)_: Ingen andre kan lese eller skrive.
    - _Delt lås (READ LOCK)_: Andre kan lese, men ikke skrive.

#### ✅ Fordeler:

- Forhindrer _tapt oppdatering_ og _skittent lesing_.
- Garanterer sterk isolasjon.

#### ❌ Ulemper:

- Kan føre til _dødlock_ (to transaksjoner venter på hverandre).
- Reduserer ytelsen ved høy samtidighet.

---

### 🚀 **Optimistisk låsing**

- **Filosofi:** "Anta at konflikter er sjeldne."
- **Hvordan:** Ingen lås ved lesing. Før oppdatering sjekkes det om dataene har blitt endret siden de ble lest.
- **Brukes når:** Det er lav sannsynlighet for konflikt og høy leseytelse er viktig.
- **Eksempel:**
    - _Versjonskontroll (MVCC)_: Hver transaksjon får sin egen kopi av dataene. Ved oppdatering sjekkes om originalen har endret seg.

#### ✅ Fordeler:

- Høy ytelse i miljøer med mange lesere og få skrivere.
- Ingen dødlock.

#### ❌ Ulemper:

- Kan føre til _rollback_ hvis en konflikt oppdages ved oppdatering.
- Kostnad ved konfliktløsning kan være høy.

---

### 🥊 **Oppsummering: Optimistisk vs. Pessimistisk låsing**

|Kjennetegn|Pessimistisk låsing|Optimistisk låsing|
|---|---|---|
|Konflikthåndtering|Forhindre på forhånd|Oppdage og håndtere etterpå|
|Ytelse (høy samtidighet)|Lavere|Høyere|
|Risiko for dødlock|Høy|Ingen|
|Typisk bruk|Skriveintensive apper|Lesetunge apper|

---

**Valg av strategi:**

- Bruk pessimistisk låsing når konflikter er vanlige og konsekvensene er alvorlige.
- Bruk optimistisk låsing når konflikter er sjeldne og ytelse er viktigere enn konfliktbehandling.

