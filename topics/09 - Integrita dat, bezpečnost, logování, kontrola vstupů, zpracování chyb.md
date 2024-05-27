# [Integrita dat, bezpečnost, logování, kontrola vstupů, zpracování chyb](https://www.youtube.com/watch?v=qHiZf9P0rW0)
*Videoprezentace není od Ječňáků, however, pán to vysvětluje hezky :3*

## O čem mluvit?
- Integrita dat (+ bezpečnot)
	- zajistujeme konzistentní data
	- zabraňujeme špatným vstupům
        - ověřujeme identitu
        - sifrujeme data
	- branime se proti útokům např sqlinjection
- Logování
	- zachytávání chyb
	- sledujeme co program dělá v čas selhání 
- Kontrola vstupů
	- důležité pro integritu dat
	- kontrolujeme třeba typ
	- regexy - email, tel číslo...
- Zpracování chyb
	- výjimky
		- pri vstupech, čtení souborů, zápis souborů, prostě všude 
		- try / catch / except

## Integrita dat a bezpečnost
- zajišťuje, aby data zůstala konzistentní a nedocházelo k neoprávněným změnám či poškození dat během zpracování nebo přenosu
- důležitá pro zajištění správného fungování aplikací a zabraňuje případnému poškození či ztrátě dat

#### Integrita
**Kontrola datových typů**
- zabraňuje neplatným datovým typům a formátům
- pokud je předpokládána určitá hodnota datového typu a není správně zadána, může dojít k nesprávným výsledkům a narušení integrity dat
- především v dynamických p. jazycích
- příklad kontroly dat. typů:w

Python:
```python
#Použitím podmínek
def say(phrase):
	if (type(phrase) is str):
		return f"Phrase is: {phrase}"
	else:
		return "Phrase is not a string"
```

**Validace vstupů** – 
- před zpracováním vstupních dat by měla být provedena validace, aby se zabránilo vstupu neplatných nebo nebezpečných dat
- validace může zahrnovat kontrolu datového typu, formátování a kontroly na případné nebezpečné prvky, jako jsou **SQL injection nebo cross-site scripting**
- nejčastěji se používá **regex** na kontrolu 
	- např. zadané e-mailové adresy, jestli zadané heslo splňuje podmínky, atd.

**Zálohování dat** 
- důležité pro zajištění integrity dat v případě, že dojde k havárii nebo ztrátě dat
	- můžeme pak data lehce obnovit.
- data lze zálohovat např. do souborů jako JSON, XML, na cloud, CD, flash disk, atd...

Bezpečnost zajišťuje ochranu před různými druhy hrozeb a errorů, které můžou nastat při chodu aplikace a zabezpečení dat před neoprávněným přístupem.
Důležitá je bezpečnost citlivých údajů uživatelů naší aplikace/programu.

#### Bezpečnost
**Šifrování dat** 
	- pomáhá chránit citlivá data před neoprávněným přístupem
	- např.: hashování hesel

**Ověřování identity**
- při práci s citlivými daty je důležité ověřit, že osoba nebo aplikace, která data požaduje, je oprávněna k přístupu
- k ověřování se obvykle používají různé metody, jako jsou například hesla, tokeny nebo biometrika

**Zabezpečení proti útokům**
- aplikace by měly být chráněny proti různým typům útoků, 
- proti útokům můžou být použita různá opatření
	- např.: 
		- bezpečné protokoly komunikace
		- ízení přístupu nebo monitorování aktivit
		- atd...
- druhy útoku mohou zahrnovat např.: 
	- útoky na přístupová hesla
	- útoky typu DDoS nebo Middle-Man

**Aktualizace a správa softwaru** 
- důležitá pro zajištění bezpečnosti a stability aplikace
	- patchujeme tak objevené díry v bezpečnosti aplikace
- při vývoji je tedy důležité pravidelně aktualizovat používané knihovny a spravovat celkovou infrastrukturu aplikace

## Logování
- používá se k zachycení stavu programu, co v daný moment dělá, jak se chová
- můžeme zachytit např. info, warning, critical errory, atd...
- velmi dobrý nástroj pro debugování programu a zachycení chyb, můžeme vidět přímo v jaké chvíli se program zasekne/nastane error
- typické informace obsahující v jednom řádku logu jsou: 
	- **čas**
	- **typ**(info, debug, warning, error)
	- **zpráva** - co v daný moment program dělá.

Příklad:
```
2024-04-17 21:31:42,629 - INFO - Checking password.
```

V Pythonu se používá knihovna *logging*.

Python:
```python
import logging

logging.basicConfig(filename="newfile.log",
					format='%(asctime)s %(message)s',
					filemode='w')

logger = logging.getLogger()

logger.setLevel(logging.DEBUG)

logger.debug("Harmless debug Message")
logger.info("Just an information")
logger.warning("Its a Warning")
logger.error("Did you try to divide by zero")
logger.critical("Internet is down")
```


## Kontrola vstupů
- kontrolujeme zadané data od uživatele, 
- kdyby kontrola byla nedostačující může docházet k špatnému chodu programu, ale i třeba k vážnějším věcem jako SQL injection nebo XSS.
- kontrolujeme např.: 
	- datový typ
	- rozsah hodnot / délka textu
	- platnost údajů (rod. číslo, datum, atd...)
	- zda jsou dostatečně bezpečné (hesla)
	- jestli odpovídají požadavku (např. aby e-mail byl e-mail a ne nějaká blbost)
	- zda neobsahují SQL injection abychom tomu zabránili

Příklady kontroly vstupů v Pythonu:
```python
#Žádná kontrola, vypíše se to, co napíše uživatel
inpt = input("Enter input:")
print(inpt)

#Vstup od uživatele rovnou měníme na požadovaný typ
#a kontrolujeme pomocí try/except
try:
	num = int(input("Enter number:"))
	print(num)
except:
	print("You did not enter a number.")

#Kontrola pomocí podmínek
i = input("Enter number:")
if (type(i) is int):
	print("bravo")
else:
	print("idiot")

#Pomocí aserce
age = 25
assert age > 0, "Age must be a positive number."
```

Toto jsou pouze základní kontroly vstupů od uživatele, na složitější kontrolu (jestli je e-mail e-mailem) se používá regulární výraz, nebo jiné prohledávání stringů. 

Příklad regexu v Pythonu:
```python
import re

regex = re.compile(r'([A-Za-z0-9]+[.-_])*[A-Za-z0-9]+@[A-Za-z0-9-]+(\.[A-Z|a-z]{2,})+')

def isValid(email):
    if re.fullmatch(regex, email):
      print("Valid email")
    else:
      print("Invalid email")

email = str(input("Enter e-mail address:"))

isValid(email)
```


## Zpracování chyb
- proces určení co se má stát když nastane **výjímka** v programu
- používá se blok try-except *(v Ptyhonu, liší se dle jazyku)*, který odchytne výjimku a provede nějaký kód, pokud k ní dojde
- používáme kód pro zpracování výjimek k odchycení chyb a provedení určitých kroků, aby se program nezastavil a nepřestal fungovat.

Klasicky máme na výber z normálních výjímek jako *file not found*, mimo tyto výjímky si můžeme vyrobit vlastní, s vlastním chováním.

Příklad vyjímek v Pythonu:
```python
#try/except
try:
	a = int(input("Enter first number: "))
	b = int(input("Enter second number: "))
	res = a/b
except ZeroDivisionError:
	print("Can't devide with 0")
except ValueError:
	print("Input is not a number.")
else:
	print("Divided first and second number: ", res)
finally:
	print("Thanks for using this shit program.")
```

Vlastní výjímky v Pythonu:
```python
class MyError(Exception):
	def __init__(self, value):
		self.value = value

	def __str__(self):
		return(repr(self.value))


try:
	raise(MyError(3*2))

except MyError as error:
	print('A New Exception occurred: ', error.value)
```

Když program narazí na nějakou chybu/spustí se výjímka, je dobré o chybě dát vědět uživateli. např. že uživatel udělal nějakou chybu a že to má zkusit znovu(input hesla), a ještě líp logovat nalezenou chybu, aby uživatel věděl kdy nastala, co jí předcházelo, atd.
