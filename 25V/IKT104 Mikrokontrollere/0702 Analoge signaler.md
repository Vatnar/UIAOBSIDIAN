Digital vs Analoge signaler
**Digital**, 1 eller på, bunn 0 eller av. 
Overfører bits. Eller skru noe av eller på.

**Analog**:
Sinuskurve, variabel spenning, -120v til + 120v f.eks. 0-3.3v hos oss. Sende ut alle verdiene mellom minimum og maksimum.

Digi
1 på 2.5 og opp.
Burde ikke ligge i mellom området siden man ikke vet hva man får.

Analoge er ikke like nøyaktige sånn sett.

Digital brukes for ren data.

Analog, vifte, sensorer, rotering, harddisk.  Ofte litt av begge deler
.
Analog krever ADC analog digital converter. 
0-1023
0 is 0v, 1023 is 3.3v

Analoge inputs sue cases.
Components
That have multiple steps
- turnable knobs (styre en motstand, helt åpen da kommer 3.3V, øke motstanden, spenningsfall)
- Levers
- Push buttons with depth sensing (R2).
Sensors:
Mikrophone
temperature sensor.
Humidity sensors
Light intensity Sensors.

**ADC** Kan ofte konfigurere oppløsning på den. ofte 10 eller 12 bit, for høyere og lavere nøyaktighet. Hastigheten avhenger av det. 
STM32L4xx er det 12-bit default. 0-4095. Microcontroller might have higher or lower internal resolution than the default. 