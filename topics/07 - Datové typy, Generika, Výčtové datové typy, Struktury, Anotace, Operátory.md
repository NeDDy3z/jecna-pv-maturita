# Datové typy, Generika, Výčtové datové typy, Struktury, Anotace, Operátory
*Videoprezentace neexistuje*

## O čem mluvit?
- popsat datové typy, k čemu jsou
- ordinální x neordinální
- vyjmenovat příklady
- zmínit null
- enum
	- k čemu se používá
- struktury
	- popsat co to je, použití
- anotace a její příklady
- vyjmenovat operátory (všechny) a jejich značení
	- rozdíly v jazycích

## Datové typy
Definice hodnoty, které smí proměnná nebo konstanta nabývat. Součástí programovacího jazyka je definice základních datových typů. Pomocí těchto základních typů může ve většině jazyků programátor tvořit nové složené typy.

### Ordinální datové typy
Hodnoty ordinálního typu tvoří lineárně uspořádanou množinu, kde pro každý prvek je přesně definovaný předchůdce i následovník (z posledního prvku ve většině jazyků dochází k přetečení na první). Z funkčního hlediska tak lze k jednoduchým celočíselným datovým typům řadit i výčtový typ, i když jeho hodnoty jsou definovány programátorem. Ordinální celočíselné datové typy jsou základem současné informatiky.

#### Boolean - logická hodnota
- Nabývá pouze dvou hodnot, *True* nebo *False*
- V některých programovacích jazycích se používá k označení *True* a *False* hodnot *1* a *0* (např. C, umí to i Python, Lua, ..., protože jsou napsané v C)

Python:
```python
is_true = True
```

C:
```c
int is_true = 0;
```
nebo
```c
typedef int bool; 
#define true 1 
#define false 0

bool is_true = true;
//čitelnější
```

C#:
```csharp
bool is_true = true;
```

#### Integer - celé číslo
- Má určitý rozsah čísel které může nabývat, může přetéct
- Různé možnosti zápisu: 0, 12, -5651, 0xA9
- Programovací jazyky mohou (ale nemusí) rozlišovat celá čísla bez znaménka a se znaménkem
- Některé jazyky (například Python) místo přetečení pro číslo vyhradí větší množství paměti, tím je usnadněno programování, avšak snižuje se výkon programu
- Můžeme provádět matematické a logické operace mezi čísly, pomocí operátorů (+, -, *, /, <, >, \==, <=, >=), na složitější matematické operace se většinou využívají vlastní metody nebo knihovny (např. odmocniny)

Python:
```python
number = 16
neg_num = -32
```

C:
```c
int number = 16;
int neg_num = -32;
int hex_num = 0xA9;
```

C#:
```csharp
int number = 16;
int neg_num = -32;
```

#### Char - znak
- Využívá se kódování (ASCII/Unicode), ve skutečnosti je znak v počítači reprezentován pomocí celého čísla
- Využit zejména na stringy

Python:
```python
character = "a"
```

C:
```c
char ch = "$";
```

C#:
```csharp
char cha = "2";
```

### Neordinální datové typy
U neordinálních datových typů není jednoznačně určen předchůdce a následovník každé hodnoty.

#### Float, double, real - reálné čislo
- Zápis čísla s tečkou podle anglosaské konvence (3.14)
- Nelze reprezentovat všechna čísla stoprocentně správně
- Reálná čísla se v počítači mohou chovat jinak, než by se intuitivně dalo čekat
- V počítači bývá většinou implementováno ve dvojkové soustavě jako _mantisa_ * 2^_exponent_, kde _mantisa_ a _exponent_ jsou celá čísla
- Zásadní výhodou reálných čísel je, že mohou ve stejné velikosti paměti reprezentovat mnohem větší rozsah hodnot, než celé číslo
- Cenou za vyšší dynamický rozsah je horší přesnost u velkých čísel (což často nevadí) a vyšší nároky na architekturu procesoru

- **Float** 
	- 6 až 7 desetiných míst
- Double
	- až 15 desetiných míst

Python:
```python
pi = 3.14
f = 1.45e3
e = float(2) #bude to 2.0
```

C:
```c
#include <stdio.h>

float f = 255.06f;
double d = 15.8989;
```

C#:
```csharp
float myNum = 5.75F;
double myDoubleNum = 5.99D;
```

### Prázdný datový typ
- **void** – jedná se o specialitu jazyka C, tento typ nenabývá žádných hodnot, může sloužit mimo jiné pro deklaraci funkce, která nemá návratovou hodnotu, nebo označovat data nespecifikovaného typu
- V některých jazycích existuje rovněž prázdná hodnota ošetřující neplatný výsledek - _null_ nebo _nil_, která je vlastně současně zvláštním datovým typem, výsledkem většiny operací s konstantou nil je opět nil, takže chování programu je deterministické

Python:
```python
nothing = None

if nothing is None:
	print("nothing")

def no_ret_fun():
	pass

if no_ret_fun() is None:
	print("nothing again")
```

C:
```c
// využití hlavně v pointerech
#include <stdio.h>

int main(void) {
  int * p_some_variable = NULL;

  if (p_some_variable == NULL) {
    printf("equal");
  }
}
```

C#:
```csharp
string s = null;
```


## Výčtové datové struktury
Výčtové datové typy nefungují jako ty klasické. Používáme je ve chvíli, kdy chceme dát na výběr z **pevně daných možností, které se nemění**. Neslouží tak pro dynamické ukládání hodnot, jako klasické proměnné. Používanější je výraz enum.
Příklady enumu: dny v týdnu, měsíce, názvy levelů, stavy, atd.

Většinou se k jednotlivým hodnotám enumu přiřazuje numerická hodnota -> index.
Hodnoty enumu se používají jako konstanty.

Python:
```python
from enum import Enum

class Season(Enum):
	SPRING = 1
	SUMMER = 2
	AUTUMN = 3
	WINTER = 4
```

C:
```c
typedef enum{FALSE, TRUE} boolean;
typedef enum{Po, Ut, St, Ct, Pa, So, Ne} den;

boolean splneno = TRUE;
den streda = St;
```

C#:
```csharp
class Program
{
  enum Level
  {
    Low,
    Medium,
    High
  }
  static void Main(string[] args)
  {
    Level myVar = Level.Medium;
    Console.WriteLine(myVar);
  }
}

-> Medium
```


## Struktury
Struktury jsou podobné třídám. Používají se pro ukládání menších kolekcí dat, přičemž žádná z jeho vlastností nesmí být referenční datový typ. Na rozdíl od tříd:
- **Nejsou referenční datový typ**. Tzn. data se ukládají přímo na zásobníku => pokud nepotřebujeme používat metody dané struktury
- Nemohou dědit od jiných tříd ani být děděny
- Nemůže se změnit konstruktor, který nemá vstupní parametry

Python:
```python
#nejsou, nepoužívají se v Pythonu (podle toho co jsem našel)
```

C:
```c
#include <stdio.h>

struct myStructure {  
  int myNum;  
  char myLetter;  
};  
  
int main() {  
  struct myStructure s1;  
  
  s1.myNum = 13;  
  s1.myLetter = 'B';  
  
  printf("My number: %d\n", s1.myNum);  
  printf("My letter: %c\n", s1.myLetter);  
  
  return 0;  
}
```

C#:
```csharp
using System;
namespace CsharpStruct {
 
  struct Employee {
    public int id;

    public void getId(int id) {
      Console.WriteLine("Employee Id: " + id);
    }
  }
 
  class Program {
    static void Main(string[] args) {
    
      Employee emp;
      
      emp.id = 1;

      emp.getId(emp.id);

      Console.ReadLine();
    }
  }
}
```


## Anotace
Dodání metadat k funkcím, proměnným, třídám, ...
Poskytují dodatečné informace o jejich zamyšlením použití nebo chování. Anotace jsou obvykle používány kompilátory, interprety nebo jinými nástroji k uplatňování omezení, optimalizaci kódu nebo generování dokumentace.
Běžně začínají znakem @ (např. klasický @override)

Mohou sloužit k:
- Určení datového typu parametru funkce
- Typicky používáno v Javě, C#, atd kde je tato anotace nutná, ale může být použito i v Pythonu, GDScriptu jako doporučení, jaký typ má jít do funkce

Python:
```python
def say_phrase(phrase : str) -> str:
	return f"{phrase}"
```

- Validační anotace k ověření vstupních parametrů zda nejsou Null

Java:
```java
public void process(@NotNull String data) {
    ...
}
```

- Serializační anotace k naznačení jak se má kód chovat při serializaci/deserializaci dat

Java:
```java
public class User {
    @JsonProperty("username")
    private String name;
    ...
}
```

- Dokumentační anotace k automatické generaci dokumentace

Java:
```java
/**
 * Vrací součet dvou čísel.
 * 
 * @param a První číslo.
 * @param b Druhé číslo.
 * @return Součet a a b.
 */
public int add(int a, int b) {
    return a + b;
}
```

Je mnoho dalších anotací.


## Operátory
Symbol (nebo řada symbolů) využívaný k reprezentaci matematických či logických operací mezi proměnnými nebo hodnotami.
Každý programovací jazyk má svoji škálu použitelných operátorů, základní operátory jako např. +, -, \*, /, bývají všude stejné.

### Druhy
#### Aritmetické
- Používají se k základním matematickým operacím
- **Součet:** +
- **Rozdíl:** -
- **Součin:** \*
- **Podíl:** /
- **Modulo:** % nebo *mod* (zbytek z dělení)
(Myslím že tyhle všichni známe takže příklad je zbytečný)

#### Relační
- Používají se k porovnání dvou hodnot
- Nejčastější použití v **if**ech
- **Rovnost:** == nebo eq
- **Nerovnost:** != nebo ne
- **Větší než:** > nebo gt
- **Menší než:** < nebo lt
- **Větší rovno:** >= nebo ge/gte
- **Menší rovno:** <= nebo le/lte

#### Logické
- Logické operace AND, OR, atd...
- **Negace:** not nebo !
- **Konjunkce:** and nebo &&
- **Disjunkce:** or nebo ||
- **Non-ekvivalence:** xor nebo ^

#### Ternární
- Zjednodušeně: zapsání if podmínky na jeden řádek :D

Příklad:
```java
if (podmínka) {
    výraz1;
} else {
    výraz2;
}
```
Můžeme zapsat takto:
```java
podmínka ? výraz1 : výraz2;
```

#### Přiřazení
- Snad nejpoužívanější z 
- Používá se k přiřazení hodnoty k proměnné
- **Přiřazení:** =

```c
int num = 10;
```