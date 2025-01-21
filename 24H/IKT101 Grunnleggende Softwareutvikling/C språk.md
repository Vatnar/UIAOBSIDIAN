Utviklet i Bell Labs. Videreutvikling av B.

```c
size_t // Tilpasser seg for å holde på størrelsen til ting.
int number = 5;
size_t size_of_number = sizeof(number)
```
sizeof() er definert for arrays for å gi størrelsen på hele arrayen.
Kan bruke sizeof slik
```c
int numbers[100] = {0};
for (int i = 0; i < sizeof(numbers) / sizeof(int); i++)

```
Kan bruke for å fikse enkel feil.

```c
sizeof(numbers) / sizeof(numbers[0]) // Da slipper man å endre fra int hvis man bytter datatype
```
[[C Structs]]
[[Hvordan minne er representert i C.]]
[[C progression]]
