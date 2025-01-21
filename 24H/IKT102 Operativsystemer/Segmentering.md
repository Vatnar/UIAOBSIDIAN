Mange problemer kan løses med flere separate virtuelle adresseområde.
En kompilator har disse tabellene 
- Source text
- Symbol table
- Constant table
- parse tree
- call stack
De 4 første vokser kontinuerlig men stacken vokser og synker ukontrollert.
Hva om en av dem krasjer i en annen.

![[Pasted image 20241025142424.png]]
Endimensjonal addresseområde med voksende tabeller.
Tabeller kan gro inn i hverandre.
Hvis en av tabellene blir for stor må OS enten fortelle til programmet ikke kan gjøre mer før den fjerner noe fra vinduet. Eller så kan programmeren selv ta litt adrsseområde fra andre tabeller som ikke er så store.
Løsningen man er ute etter er å frigjøre programmeren fra disse problemene. Løsningen er segmentering.

Ved segmentering blir maskinene utstyrt med helt uavhengige adresseomrdåer kalt segmeneter. Hvor hvert segment er en linæer sekvens av adressser. LEngden kan da variere fra 0 - maks. De forskjellige segmenetene kan ha forskjellig mengde.




> [!NOTE] Ulike segmenter
> 1. Source Text
> 2. symbol table
> 3. constant table
> 4. parse tree
> > [!FAQ] [[Hvordan minne er representert i C.]]
> > > 
> >1. Text Segment (i.e instructions)
> >2. Initialized data segment
> >3. Uninitialized data segment (BSS)
> >4. Heap
> >5. Stack
> ![[Pasted image 20241025144325.png]]


