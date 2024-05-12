# Integrita dat, bezpečnost, logování, kontrola vstupů, zpracování chyb

## O čem mluvit?
- co je integrita dat
	- proč je důležitá
	- co se může stát když není
- vysvětlit logování
	- proč je dobré
	- jak ho využívat
	- dát příklad z projektů
- co to je kontrola vstupů, proč je nutná
- co to jsou výjímky
- vysvětlit try/except

## Integrita dat a bezpečnost
Integrita dat zajišťuje, aby data zůstala konzistentní a nedocházelo k neoprávněným změnám či poškození dat během zpracování nebo přenosu. Integrita dat je důležitá pro zajistění správného fungování aplikací a zabraňuje případnému poškození či ztrátě dat.

**Integrita**:
- **Kontrola datových typů** – Kontrola datových typů zabraňuje neplatným datovým typům a formátům. Pokud je předpokládána určitá hodnota datového typu a není správně zadána, může dojít k nesprávným výsledkům a narušení integrity dat.
	- Především v dynamických p. jazycích
	- Příklad kontroly dat. typů
Python:
```python
#Použitím podmínek
def say(phrase):
	if (type(phrase) is str):
		return f"Phrase is: {phrase}"
	else:
		return "Phrase is not a string"
```

- **Validace vstupů** – Před zpracováním vstupních dat by měla být provedena validace, aby se zabránilo vstupu neplatných nebo nebezpečných dat. Validace může zahrnovat kontrolu datového typu, formátování a kontroly na případné nebezpečné prvky, jako jsou SQL injection nebo cross-site scripting.
	- Nejčastěji se používají regulární výrazy na kontrolu např. zadané e-mailové adresy, jestli zadané heslo splňuje podmínky, atd.

- **Zálohování dat** – Zálohování dat je důležité pro zajištění integrity dat v případě, že dojde k havárii nebo ztrátě dat. Můžeme pak data lehce obnovit.
	- Můžeme zálohovat data např. do souborů jako JSON, XML, na cloud, CD, flash disk, atd...

Bezpečnost zajišťuje ochranu před různými druhy hrozeb a errorů, které můžou nastat při chodu aplikace a zabezpečení dat před neoprávněným přístupem.
Důležitá je bezpečnost citlivých údajů uživatelů naší aplikace/programu.

**Bezpečnost**:
- **Šifrování dat** – Šifrování dat pomáhá chránit citlivá data před neoprávněným přístupem. Např. hashování hesel

- **Ověřování identity** – Při práci s citlivými daty je důležité ověřit, že osoba nebo aplikace, která data požaduje, je oprávněna k přístupu. K ověřování identity se obvykle používají různé metody, jako jsou například hesla, tokeny nebo biometrické údaje.

- **Zabezpečení proti útokům** – Aplikace by měly být chráněny proti různým typům útoků, jako jsou například útoky na přístupová hesla, útoky typu denial-of-service nebo útoky typu man-in-the-middle. K zabezpečení proti těmto útokům může být použita různá opatření, jako jsou například bezpečné protokoly komunikace, řízení přístupu nebo monitorování aktivit.

- **Aktualizace a správa softwaru** – Aktualizace softwaru je důležitá pro zajištění bezpečnosti a stability aplikace. Při vývoji je tedy důležité pravidelně aktualizovat používané knihovny a spravovat celkovou infrastrukturu aplikace.

## Logování
Používá se k zachycení stavu programu, co v daný moment dělá, jak se chová. Můžeme zachytit např. info, warning, critical. Velmi dobrý nástroj pro debugování programu a zachycení chyb, můžeme vidět přímo v jaké chvíli se program zasekne/nastane error.
Typické informace obsahující v jednom řádku logu jsou: **čas**, **typ**(info, debug, warning, error), **zpráva** - co v daný moment program dělá.

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
Kontrolujeme zadané data od uživatele, zda jsou dostatečně bezpečné(hesla), jestli odpovídají požadavku(např. aby e-mail byl e-mail a ne nějaká blbost). Kdyby kontrola byla nedostačující může docházet k špatnému chodu programu, ale i třeba k vážnějším věcem jako SQL injection nebo XSS.

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
Proces určení co se má stát když nastane **výjímka** v programu. Používá se blok try-except, který odchytne výjimku a provede nějaký kód, pokud k ní dojde. Používáme kód pro zpracování výjimek k odchycení chyb a provedení určitých kroků, aby se program nezastavil a nepřestal fungovat.

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