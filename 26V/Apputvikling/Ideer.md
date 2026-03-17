# App Ideer - IKT205 Prosjekt

##  "Community Hazard"
*App hvor brukere "pinner" farer i nærområdet (ødelagte ting, is, osv), med bilder og farenivå.*

> [!SUCCESS] PROS
> - **Google Maps API:** Gir mye "nice" UI-stuff og visualisering.
> - **Lokasjonsbaserte notifikasjoner:** Varsle brukere når de nærmer seg en fare.
> - **Teknisk dybde:** Caching av kart, håndtering av bilder og media.
> - **Rapport-mat:** Gode muligheter for å skrive om Privacy/GDPR.

> [!WARNING] CONS
> - **Datamangel:** Vanskelig å få en god app-opplevelse uten masse data (kjipt med tomt kart).
> - **Datakvalitet:** Validering av brukerinnsendt data og håndtering av misbruk (troll-pins).
> - **GDPR-surr:** Registreringsnumre på biler eller ansikter i bilder må sensureres.

---

##  "Silent Guardian"
*Bruker Geofencing API for å tracke lokasjoner. Kobles opp mot kart med definerte "Silent Zones" (f.eks. bibliotek). Bruker Foreground Services eller WorkManager.*

### Key Features
- **Zone Management:** Map interface (Google Maps SDK) for å definere soner.
- **Sosialt:** Deling av soner/communities og globale definerte soner.
- **Automatisering:** Gå automatisk på "Ikke forstyrr" eller send SMS-svar: *"In a silent zone"*.

> [!SUCCESS] PROS
> - **UI + OS Interaction:** Gir ekstremt god kunnskap om Android-systemet (ikke bare en standard CRUD-app).
> - **Teknisk Stack:** Avansert bruk av Google Maps, Background Services, Geofencing API og WorkManager.
> - **Optimalisering:** Fokus på batteri og ressursbruk (JobScheduler/WorkManager).
> - **TDD-vennlig:** Veldig egnet for Test Driven Development i logikk-laget.

> [!WARNING] CONS
> - **Tilganger:** Bakgrunnslokasjon er strengt og "kranglete" i moderne Android.
> - **Testing:** Kan være utfordrende å teste background services manuelt.
> - **Arkitektur:** Ekstremt viktig å holde logikken og Android-servicene separat for å kunne kjøre tester.
> - **Maskinvare:** Noe funksjonalitet (som auto-reply) må testes fysisk.

---

##  Oppsummering 

- **Community Hazard** er mest sannsynlig et enklere prosjekt rent teknisk, men har større utfordringer rundt innhold og moderering.
- **Silent Guardian** gir mulighet for høyere karakter da det treffer de "avanserte" kriteriene i emnebeskrivelsen bedre.
- Det kan faktisk være "enklere" på sikt hvis man unngår utfordringene med brukergenerert innhold og bilde-moderasjon som man får i Hazard-appen.