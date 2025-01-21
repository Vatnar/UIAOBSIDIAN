The "Brain"
Henter instruksjoner fra minnne og eksekverer dem i en evig sirkel
Har spesifikke instruksjonsett som den kan skekvere
	Intel pentium kan ikke kjøre SPRAC-prgoram og visa vesa
		Aksessere minnet er mye tregere enn å utføre instruksjon
			Registere er like kjappe som cpuen.
			Spesialregistere
			Program counter
				Adressen til neste instruksjon som skal hentes
		[[Stack pointer]]
			Peker til toppen av stacken
		PSW Program status word
			Inneholder kontroll bit som for eksempel CPU priorotet. modus kernel, user og andre.
				User kan ofte lese, men bare skifte noen få av bita.
			Når et program stoppes må alle registrene lagres slik at program kan gjenopprettes der den var.
			Basic instruction cycle.
				Start
				Henter instruksjon
				Eksekverer
				Fortsetter evig.
			Instruction cycle with interrupts
				Henter
				Eksekverer, Sjekker om den har en interrupt. Da går den og henter interrupt prosedyren. Hvis ikke går den på nytt i loop