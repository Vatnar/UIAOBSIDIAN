
Linux har seperat kjerne, samme med windows og UNIX.

Operativsystem som en del av brukerprosesser. Alle prosessene har operativsystemet inne i seg. Operativsystemprosess.
![[Pasted image 20240920131303.png]]
**Non Process Kernel.**
Operating system code is executed as a seperate entitiy that operates in privilegde mode.

**Execution witihin user processes.**
Operarting system software witihin context of a user process. No need to process switch to run OS routine. 

**Process based operating system.** 
Implement The OS as a collection of System process. 
Hvis en av funksjonene krasjer, f.eks filsystemet, kan man bare restarte processen. Kan kjøre flere forskjellige filsystemer. 