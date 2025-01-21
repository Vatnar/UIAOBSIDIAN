Variable stores one value of one type.
A struct stores multiple related values.
A student has a name (string) and age(int).
A point has x (int) and y (int) position.
A bank account has a name (string) number (string) and balance (double).

Kan strukturere data men ikke funksjoner i structs.

Eksempel:
Bank konto
- Eiernavn
- Kontonummer
- Eierbalanse
Datatyper:
- Eiernavn - string (char array)
- Kontonummer - integer
- Balanse - float

```c 
//Definere struct
struct Account
{
char ownerName[100];
int accountNumber;
float accountBalance
};```
```c
int number; //int er oppskriften som bestemmer hvor stor data, maks og min, osv.

struct Account myAccount; // struct Account er oppskrift
//Kan kalles et object, et instanse av Account. 
```
```c
//Preprocessor directives. Skjer før kompilering. 
#ifndef ACCOUNT_H  
#define ACCOUNT_H  
  
#endif //ACCOUNT_H
```

```c
typedef struct  
{  
    int number;  
    float balance;  
    char owner[100];  
} account_t; //Understrek t, hvor t er type. AccountType. 
// Gjør at vi kan skrive account_t istedet for struct Account
```
```c
void printAccount(account_t account)
{
printf(...);
}
account_t readAccount()
{
	account_t result;
	fscanf(...);
	return result;
}
```