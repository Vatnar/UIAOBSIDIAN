```table-of-contents
title: Viktig for eksamen
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
# Avhengigheter
### 🔗 **Funksjonell avhengighet (Functional Dependency)**

En funksjonell avhengighet mellom to attributter i en relasjonsdatabase uttrykker et forhold der verdien av ett attributt **entydig bestemmer** verdien av et annet attributt.

#### 💡 **Notasjon:**

Hvis attributtet `B` er funksjonelt avhengig av attributtet `A`, skrives det slik:

A→BA \rightarrow B

Dette betyr at verdien av `A` **bestemmer** verdien av `B`.

---

#### 📝 **Eksempel på funksjonell avhengighet:**

|StudentID|Navn|Alder|
|---|---|---|
|1|Ola|20|
|2|Kari|22|
|3|Per|21|

I denne tabellen har vi følgende funksjonelle avhengigheter:

1. `StudentID → Navn` (StudentID bestemmer navnet)
2. `StudentID → Alder` (StudentID bestemmer alderen)

---

### 🔁 **Transitiv avhengighet (Transitive Dependency)**

En transitiv avhengighet oppstår når en attributt er **indirekte avhengig** av en annen attributt via en tredje attributt.

#### 💡 **Definisjon:**

Hvis:

1. A→BA \rightarrow B (B er avhengig av A)
2. B→CB \rightarrow C (C er avhengig av B)
3. A→CA \rightarrow C (C er **transitivt** avhengig av A)

---

#### 📝 **Eksempel på transitiv avhengighet:**

|PersonID|Fødselsnummer|Fødselsdato|
|---|---|---|
|1|12345678901|12.03.1995|
|2|23456789012|08.07.1998|

Her har vi følgende avhengigheter:

1. `PersonID → Fødselsnummer` (direkte avhengighet)
2. `Fødselsnummer → Fødselsdato` (direkte avhengighet)
3. **Transitiv avhengighet:** `PersonID → Fødselsdato`

---

### 🚩 **Hvorfor er transitiv avhengighet problematisk?**

Transitiv avhengighet er et problem når vi snakker om **3. normalform (3NF)** i databasesystemer, fordi:

- Det kan føre til **redundans** og **anomali** ved oppdatering, innsetting eller sletting.
- Normalisering til 3NF krever at vi **fjerner transitive avhengigheter** ved å dele opp tabellen.

---

### 📝 **Eksempel på å fjerne transitiv avhengighet:**

Forrige tabell kan deles opp slik:

**PersonTabell:**

|PersonID|Fødselsnummer|
|---|---|
|1|12345678901|
|2|23456789012|

**FødselsnummerTabell:**

|Fødselsnummer|Fødselsdato|
|---|---|
|12345678901|12.03.1995|
|23456789012|08.07.1998|

Nå er transitive avhengigheter fjernet, og vi unngår **oppdateringsanomalier**.

---

### 🚀 **Oppsummering:**

- **Funksjonell avhengighet:** En attributt avhenger direkte av en annen.
- **Transitiv avhengighet:** En indirekte avhengighet mellom attributter via en tredje attributt.
- Transitive avhengigheter bryter med **3NF** og bør fjernes ved normalisering.
# **Views i databaser**

En **view** er en virtuell tabell i en database som er basert på resultatet av en **SQL-spørring**. Den lagrer ikke dataene selv, men viser data hentet fra én eller flere underliggende tabeller.

---

#### 💡 **Egenskaper ved views:**

1. **Virtuelle tabeller:** Ingen fysisk lagring av data.
2. **Dynamisk oppdatering:** Data i viewet oppdateres når de underliggende tabellene endres.
3. **Sikkerhet:** Kan brukes til å begrense tilgangen til sensitive data.
4. **Forenkling:** Gjør komplekse spørringer enklere ved å skjule kompleksiteten.

---

### 📝 **Syntaks for å opprette et view:**

```sql
CREATE VIEW view_navn AS
SELECT kolonne1, kolonne2, ...
FROM tabell
WHERE betingelse;
```

---

### 🔍 **Eksempel:**

Anta at vi har en tabell med ansatte:

**Ansatte-tabell:**

|AnsattID|Navn|Stilling|Lønn|
|---|---|---|---|
|1|Ola|Leder|70000|
|2|Kari|Utvikler|60000|
|3|Per|Designer|55000|

#### **Opprette et view for bare ledere:**

```sql
CREATE VIEW LederView AS
SELECT Navn, Lønn
FROM Ansatte
WHERE Stilling = 'Leder';
```

#### **Bruke viewet:**

```sql
SELECT * FROM LederView;
```

**Resultat:**

|Navn|Lønn|
|---|---|
|Ola|70000|

---

### 🛠️ **Fordeler med views:**

1. **Sikkerhet:** Begrense tilgangen til sensitive data.
2. **Forenkling:** Samle komplekse spørringer i én enkel visning.
3. **Gjenbruk:** Gjenbruk av spørringer uten å skrive dem på nytt.
4. **Abstraksjon:** Skjuler kompleksiteten til underliggende tabeller.

---

### ⚠️ **Ulemper med views:**

1. **Ytelse:** Komplekse views kan bli trege, spesielt hvis de er basert på flere tabeller.
2. **Ikke alltid oppdaterbare:** Noen views kan ikke oppdateres direkte hvis de inneholder aggregeringer, joins eller subspørringer.
3. **Vedlikehold:** Endringer i underliggende tabeller kan kreve at viewet oppdateres.

---

### 🚀 **Oppdaterbare vs. ikke-oppdaterbare views:**

- **Oppdaterbare views:** Endringer i viewet reflekteres i den underliggende tabellen.
- **Ikke-oppdaterbare views:** Viewet er basert på en kompleks spørring som hindrer direkte oppdatering.

**Eksempel på oppdaterbart view:**

```sql
CREATE VIEW UtviklerView AS
SELECT Navn, Lønn
FROM Ansatte
WHERE Stilling = 'Utvikler';

UPDATE UtviklerView
SET Lønn = 65000
WHERE Navn = 'Kari';
```

---

### 💡 **Oppsummering:**

Views er et kraftig verktøy for å forenkle datatilgang, øke sikkerheten og gi et abstraksjonslag over komplekse spørringer. Samtidig må man være oppmerksom på ytelsesproblemer og begrensninger knyttet til oppdaterbarhet.


#  **Transaksjon i databasesammenheng**

En **transaksjon** er en sekvens av én eller flere databaseoperasjoner som utføres som en **enhet**. Enten utføres alle operasjonene, eller ingen av dem – dette sikrer **dataintegritet**.

---

#### 💡 **Egenskaper (ACID):**

En transaksjon må oppfylle følgende egenskaper:

1. **Atomicity (Atomisitet):** Hele transaksjonen utføres eller ingen del av den.
2. **Consistency (Konsistens):** Transaksjonen fører databasen fra én konsistent tilstand til en annen.
3. **Isolation (Isolasjon):** Pågående transaksjoner påvirker ikke hverandre.
4. **Durability (Holdbarhet):** Når en transaksjon er bekreftet (commit), vil resultatet være permanent, selv om systemet krasjer.

---

#### 📝 **Eksempel:**

Tenk deg en bankoverføring fra konto A til konto B:

1. Trekk 1000 kr fra konto A.
2. Legg 1000 kr til konto B.
3. Hvis noen av operasjonene feiler, må hele transaksjonen rulles tilbake (rollback).

---

#### 🗃️ **SQL-eksempel:**

```sql
BEGIN TRANSACTION;

UPDATE Konto SET Saldo = Saldo - 1000 WHERE KontoID = 1;
UPDATE Konto SET Saldo = Saldo + 1000 WHERE KontoID = 2;

COMMIT; -- Lagre endringene permanent
-- ROLLBACK; -- Angre endringene hvis noe går galt
```

---

### 🚩 **Hvorfor er transaksjoner viktige?**

- Hindrer **inkonsistente data** ved feil.
- Sikrer **dataholdbarhet** ved krasj.
- Gir **isolasjonsgarantier** mellom samtidige prosesser.

# **Triggers og prosedyrer i databaser**

Både **triggers** og **lagrede prosedyrer** (stored procedures) er verktøy i en database for å automatisere oppgaver og håndtere data.  
Selv om de begge utfører forhåndsdefinerte handlinger, brukes de i ulike sammenhenger.

---

#### 💡 **Triggers:**

En **trigger** er en automatisk handling som utføres når en bestemt hendelse oppstår i databasen (for eksempel **INSERT**, **UPDATE** eller **DELETE**).

- **Aktiveres automatisk** når en hendelse inntreffer.
- Brukes til **validering**, **logging**, **sikkerhet** og **historikk**.
- Kan ikke kalles direkte av brukeren.

##### 📝 **Eksempel på en trigger:**

Logge alle oppdateringer i en ansatt-tabell:

```sql
CREATE TRIGGER LoggOppdatering
AFTER UPDATE ON Ansatte
FOR EACH ROW
BEGIN
    INSERT INTO Logg (AnsattID, Endringstidspunkt)
    VALUES (NEW.AnsattID, NOW());
END;
```

---

#### 🛠️ **Lagrede prosedyrer (Stored Procedures):**

En **lagret prosedyre** er en samling SQL-kommandoer som er lagret i databasen og kan utføres ved behov.

- **Aktiveres manuelt** ved kall.
- Brukes til **datahåndtering**, **batch-operasjoner**, **beregninger** og **rapporter**.
- Kan ta inn **parametere** og returnere verdier.

##### 📝 **Eksempel på en lagret prosedyre:**

Beregne gjennomsnittslønn i en avdeling:

```sql
CREATE PROCEDURE Gjennomsnittslønn (IN avdeling VARCHAR(50))
BEGIN
    SELECT AVG(Lønn) AS Gjennomsnitt
    FROM Ansatte
    WHERE Avdeling = avdeling;
END;
```

**Kall prosedyren:**

```sql
CALL Gjennomsnittslønn('IT');
```

---

### 🔑 **Forskjeller mellom trigger og prosedyre:**

|Egenskap|Trigger|Lagret prosedyre|
|---|---|---|
|Aktivering|Automatisk (på hendelse)|Manuell (via kall)|
|Bruksområde|Logging, validering, integritet|Kompleks logikk, rapporter|
|Kan ta parametere|Nei|Ja|
|Kan returnere data|Nei|Ja|

---

### ✅ **Oppsummering:**

- **Triggers** brukes til å utføre handlinger automatisk når spesifikke hendelser inntreffer.
- **Lagrede prosedyrer** er forhåndsdefinerte SQL-funksjoner som kan kalles manuelt.
- Begge brukes for å gjøre databaseadministrasjon mer effektiv og automatisert.

Gi beskjed om du trenger flere eksempler eller forklaringer! 😄
# Prinsipper for oppbygging av et B+ tre

Et **B+ tre** er en selvbalanserende trestruktur som brukes primært i databasesystemer og filsystemer for effektiv lagring og søking i store datamengder. Det er en variant av B-trær, men skiller seg fra disse ved at alle faktiske dataverdier er lagret i bladnodene, mens interne noder kun lagrer søkenøkler. Denne strukturen gjør B+ trær spesielt godt egnet for systemer med høy I/O-belastning, som disklagring.


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

For å gi et A-svar, må vi være mer grundige og presise. La oss gå litt dypere og dekke relasjonsdatabaser mer akademisk og omfattende:

---

### 📚 **Definisjon av relasjonsdatabase:**

En **relasjonsdatabase** er en strukturert samling av data som organiseres i relasjoner (tabeller), hvor dataene er logisk sammenkoblet ved hjelp av nøkler. Den følger det relasjonelle datamodellen, som ble foreslått av Edgar F. Codd i 1970.

#### 🎯 **Hovedprinsipper i en relasjonsdatabase:**

1. **Data lagres i tabeller (relasjoner)** som består av rader og kolonner.
2. **Relasjoner mellom tabeller** opprettes gjennom nøkler, vanligvis primær- og fremmednøkler.
3. **Dataintegritet** sikres ved bruk av integritetsbegrensninger (constraints), som sikrer at dataene oppfyller forretningsreglene.
4. **SQL (Structured Query Language)** brukes som grensesnitt for datahåndtering og spørringer.

---

### 🗺️ **Relasjonell modell:**

En relasjonsdatabase er bygget på følgende grunnprinsipper:

#### 1. **Relasjoner (Tabeller):**

- Hver tabell representerer en entitet eller en relasjon mellom entiteter.
- Rader representerer **forekomster** (tupler), mens kolonner representerer **attributter**.

#### 2. **Nøkler:**

- **Primærnøkkel (PK):** Unik identifikator for en rad. Ingen duplikater eller NULL-verdier er tillatt.
- **Fremmednøkkel (FK):** En attributt som refererer til en primærnøkkel i en annen tabell for å etablere en relasjon.

#### 3. **Integritetsregler:**

- **Entitetsintegritet:** Ingen primærnøkkelverdi kan være NULL.
- **Referanseintegritet:** Fremmednøkler må enten være NULL eller matche en eksisterende primærnøkkel.
- **Domeneintegritet:** Attributter må inneholde gyldige verdier i henhold til datatypen.
- **Brukerdefinert integritet:** Forretningsregler som pålegges gjennom constraints eller triggere.

---

### 💡 **Egenskaper ved relasjonsdatabaser:**

1. **Normalisering:**
    
    - Prosessen med å strukturere data for å minimere redundans og unngå uønskede avhengigheter.
    - Vanlige normalformer inkluderer:
        - 1NF (Første normalform): Ingen gjentatte grupper eller multiverdier.
        - 2NF (Andre normalform): Full funksjonell avhengighet.
        - 3NF (Tredje normalform): Fjerner transitive avhengigheter.
2. **ACID-egenskaper:**
    
    - **Atomicity:** Alt eller ingenting-prinsippet.
    - **Consistency:** Opprettholder konsistente tilstander.
    - **Isolation:** Sikrer at samtidige transaksjoner ikke påvirker hverandre.
    - **Durability:** Data forblir permanente etter en commit, selv ved krasj.

---

### 💾 **Eksempel: Relasjon mellom Kunder og Bestillinger**

**Kunder (Customer)**

|CustomerID (PK)|Name|City|
|---|---|---|
|1|Ola Hansen|Oslo|
|2|Kari Nord|Bergen|

**Bestillinger (Order)**

|OrderID (PK)|CustomerID (FK)|Product|
|---|---|---|
|101|1|Laptop|
|102|2|Mobiltelefon|

#### 📝 **SQL-spørring:**

```sql
SELECT Name, Product
FROM Kunder
JOIN Bestillinger ON Kunder.CustomerID = Bestillinger.CustomerID;
```

Denne spørringen henter navn og produkter fra begge tabellene ved å bruke relasjonen mellom `CustomerID`-feltene.

---

### 🌐 **Fordeler med relasjonsdatabaser:**

- **Høy dataintegritet og konsistens:** Ved hjelp av nøkler og integritetsregler.
- **Effektiv datahåndtering:** SQL gjør det enkelt å manipulere og hente data.
- **Skalerbarhet:** Støtter store datamengder med kompleks relasjonsstruktur.
- **Transaksjonsstøtte:** Garanterer ACID-egenskaper.

---

### 🚀 **Ulemper:**

- **Ytelsesproblemer ved store datamengder:** Kan bli tregt med mange JOIN-operasjoner.
- **Kompleks skjemahåndtering:** Endringer i skjemadesign kan være tidkrevende.

---

### 📝 **Konklusjon:**

Relasjonsdatabaser er svært effektive når det gjelder å lagre strukturerte data med komplekse relasjoner og opprettholde dataintegritet. De brukes ofte i kritiske applikasjoner som bank- og forretningssystemer, der pålitelighet og datakonsistens er avgjørende.

# Recovery
**Recovery** i databasesammenheng refererer til prosessen med å gjenopprette databasen til en konsistent tilstand etter en feil eller krasj. Målet er å sikre at dataene er korrekte og fullstendige, selv etter uforutsette hendelser som strømbrudd, systemkrasj eller programvarefeil.

---

### 💡 **Hvorfor er recovery nødvendig?**

Recovery er avgjørende for å opprettholde ACID-egenskapene, spesielt:

- **Atomicity:** Alle operasjoner i en transaksjon fullføres eller rulles tilbake.
- **Durability:** Dataene forblir permanente etter en commit, selv ved systemfeil.

---

### ⚙️ **Typer feil som krever recovery:**

1. **Systemfeil:** F.eks. strømbrudd eller maskinvarefeil som fører til at databasen krasjer.
2. **Diskfeil:** Fysiske feil på lagringsmediet som fører til tap av data.
3. **Transaksjonsfeil:** Feil under utførelse av en transaksjon, f.eks. på grunn av brudd på integritetsregler.
4. **Programvarefeil:** Feil i databasesystemet eller applikasjonsprogrammet.

---

### 🔄 **Recovery-teknikker:**

Det finnes flere teknikker for å sikre at dataene kan gjenopprettes på en pålitelig måte.

#### 1. **Loggbasert recovery:**

- Systemet holder en **transaksjonslogg** (Write-Ahead Logging, WAL) som lagrer alle operasjoner før de utføres.
- Ved en krasj brukes loggen til å gjøre følgende:
    - **Redo:** Gjenoppretter committed transaksjoner som ikke ble fullført.
    - **Undo:** Tilbakestiller ikke-committed transaksjoner for å sikre konsistens.

💡 _Eksempel:_

```
<START T1>
<WRITE T1, A, 100>
<COMMIT T1>
```

- Hvis T1 er committed før krasj, vil systemet bruke **redo** for å anvende endringen på nytt.
- Hvis T1 ikke er committed, vil systemet bruke **undo** for å tilbakestille verdien.

---

#### 2. **Checkpointing:**

- Et **checkpoint** er en sikkerhetskopi av hele databasen på et gitt tidspunkt.
- Ved gjenoppretting starter systemet fra det siste checkpointet og bruker transaksjonsloggen for å fullføre eventuelle manglende oppdateringer.
- Dette reduserer gjenopprettingstiden betydelig, da eldre transaksjoner ikke trenger å gjøres om på nytt.

---

#### 3. **Shadow Paging:**

- Bruker to sider (shadow og current) for å holde styr på dataendringer.
- Endringer blir gjort på en **kopi (shadow page)**, og når transaksjonen er ferdig, byttes sidene om.
- Fordel: Ingen behov for loggbasert recovery.
- Ulempe: Høyt lagringsforbruk på grunn av kopi av sider.

---

#### 4. **RAID og speiling:**

- Maskinvarebaserte løsninger som sikrer at data er tilgjengelig selv ved diskfeil.
- RAID (Redundant Array of Independent Disks) lagrer data over flere disker, slik at en krasj på én disk ikke fører til tap.

---

### 📝 **Eksempel på recovery-prosess:**

1. **Systemet krasjer midt i en transaksjon.**
2. **Ved oppstart skannes transaksjonsloggen.**
3. **Identifiserer committed og ikke-committed transaksjoner.**
4. **Utfører REDO for committed transaksjoner og UNDO for ikke-committed transaksjoner.**

---

### 🚀 **Oppsummering:**

Recovery er essensielt for å sikre at databasen alltid er i en konsistent tilstand, selv etter feil. Gjennom bruk av loggbasert recovery, checkpointing, shadow paging og maskinvareløsninger som RAID, kan databaser håndtere en rekke feilscenarier uten å miste data.

# Undo Redo
### 🔄 **Recovery i databaser**

Recovery i databaser handler om å gjenopprette databasen til en **konsistent tilstand** etter en feil, som strømbrudd, systemkrasj eller programvarefeil. Målet er å sikre at dataene oppfyller **ACID-egenskapene**, spesielt **Atomicity** og **Durability**.

---

### 💡 **Undo/Redo-algoritmen**

Undo/Redo-algoritmen er en av de mest brukte metodene for databasegjenoppretting. Den baserer seg på en **transaksjonslogg** (oftest med **Write-Ahead Logging (WAL)**) for å spore alle operasjoner som utføres.

---

#### 📝 **Hvordan fungerer Undo/Redo?**

1. **Loggføring før utførelse (WAL-prinsippet):**
    - Hver databaseoperasjon loggføres _før_ endringen utføres på databasen.
    - Loggen inneholder informasjon som:
        
        ```
        <START T1>
        <WRITE T1, A, old_value, new_value>
        <COMMIT T1>
        ```
        
    - Dette sikrer at loggen kan brukes til gjenoppretting selv om systemet krasjer midt i en transaksjon.

---

#### ⚙️ **Gjenopprettingsprosessen (Recovery):**

1. **Analyse:**
    
    - Skann loggen fra begynnelse til slutt for å identifisere hvilke transaksjoner som var **committed** og hvilke som var **ikke-committed** da krasjet skjedde.
2. **Redo (gjør om igjen):**
    
    - For alle transaksjoner som er **committed**, utfør alle handlinger på nytt for å sikre at oppdateringene er på plass.
    - Dette er nødvendig fordi en transaksjon som er committed kanskje ikke rakk å bli lagret på disk før krasjet.
3. **Undo (rull tilbake):**
    
    - For alle **ikke-committed** transaksjoner, reverser endringene for å gjenopprette den konsistente tilstanden før transaksjonen startet.
    - Dette forhindrer at uferdige operasjoner forblir i databasen.

---

### 📝 **Eksempel:**

Anta at loggen ser slik ut når systemet krasjer:

```
<START T1>
<WRITE T1, A, 100, 200>
<START T2>
<WRITE T2, B, 300, 400>
<COMMIT T1>
<START T3>
<WRITE T3, C, 500, 600>
```

#### **Recovery:**

1. **Analyse:**
    
    - T1 er **committed**.
    - T2 og T3 er **ikke-committed**.
2. **Redo:**
    
    - Utfør om igjen alle oppdateringer fra **T1** (siden den er committed).
3. **Undo:**
    
    - Rull tilbake endringer gjort av **T2** og **T3**.

---

### 🚀 **Hvorfor er Undo/Redo mest brukt?**

- **Effektivitet:**
    
    - Gjenoppretter bare de nødvendige transaksjonene, i stedet for å gå gjennom hele databasen.
- **Sikkerhet:**
    
    - Takket være WAL-prinsippet kan systemet være sikker på at alle endringer enten blir fullført eller rullet tilbake.
- **Fleksibilitet:**
    
    - Håndterer både **systemfeil** (f.eks. strømbrudd) og **transaksjonsfeil** (f.eks. integritetsbrudd).
- **Minimal tap av data:**
    
    - Fordi loggen skrives før selve dataene endres, kan systemet alltid finne tilbake til en konsistent tilstand.

---

### 💡 **Oppsummering:**

Undo/Redo-algoritmen er en robust og effektiv metode for databasegjenoppretting. Ved å bruke transaksjonslogger og WAL-prinsippet sikres både atomicity og konsistens, samtidig som prosessen er rask og pålitelig. Dette gjør algoritmen til et naturlig valg i de fleste relasjonsdatabaser.

