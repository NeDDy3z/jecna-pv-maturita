# [Výjimky a aserce, debugování a zpracování chyb](https://youtu.be/n74uts2mz6s?si=QRnqaFWBCSdHzCLX)
[//]: # (Odkaz v názvu je na přednášku z MIT OpenCourseWave od Dr. Any Bellové)

---
## O čem mluvit?

- **Základní koncepty:** 
  - Definice vyjímky, aserce a chyb v programování
  - Vysvětli:
    - co jsou to výjimky
    - proč jsou důležité
    - jaký je rozdíl mezi vyjímkami a asercemi.
- **Použití a výhody vyjímek:**
  - Diskutuj o tom, jak a proč programátoři používají vyjímky.
  - Uveď příklady situací, ve kterých se vyjímky hodí, a jak mohou zlepšit čitelnost a údržbu kódu.
- **Zacházení s vyjímkami:** 
  - Představ různé způsoby zacházení s vyjímkami, jako je try-catch blok.
  - Vysvětli, jaké jsou doporučené postupy při zacházení s vyjímkami a jak je možné je řídit.
- **Aserce a kontrola podmínek:**
  - Diskutuj o tom, jak mohou aserce pomoci odhalit chyby v kódu a proč je důležité prověřovat podmínky.
- **Debugování:**
  - Vysvětli proces debugování a jeho důležitost při odhalování chyb v kódu.
  - Ukaž na různé nástroje a techniky, které programátoři používají k debugování, jako jsou ladicí výpisy, breakpointy nebo ladicí prostředí.
- **Zpracování chyb:**
  - Diskutuj o strategiích pro zpracování chyb v kódu.
  - Zmiň různé způsoby, jak programátoři mohou chyby identifikovat, zaznamenávat a zpracovávat, aby zajistili robustnost a spolehlivost svého softwaru.
- **Best practices:**
  - Zdůrazni nejlepší postupy při práci s vyjímkami, asercemi, debugováním a zpracováním chyb.
  - To může zahrnovat psaní srozumitelných a přehledných chybových zpráv, zachování konzistence v zacházení s vyjímkami nebo pravidelné testování kódu na chyby.
---
## Defensivní programování
- **Modulace kódu**
  - = psaní kódu v jednotlivých blocích
  - Napomáhá v obecném přehledu v kódu pro pozdější debuggování
    - Například pomocí **funkcí**
  - Po napsání takového kódu je potřeba ho otestovat

## Debuggování
- Zkoumání událostí, které vedly k chybě
  - ✔️ _"Proč mi kód nevrátil to, co jsem očekával/a?"_
    - ✔️ _"Jak jsem se dostal/a k neočekávanému výsledku?"_
  - ❌ _"Co je špatně?"_ --> To je Testování

<details><summary><a>Příběh</a></summary>
  <hr/>

- V roce 1947 byl dostaven sálový počítač Harvard MK2
  - Skupina vědců pracovala na programu, které měla vypočítat trigonometrickou funcki
  - Zjistili že jejich program nefunguje správně
  - Prošli všechny panely a relé
    - V paneu F relé 70 našli můru, která byla příčinnou chyby
      - "First actual case of bug being found" | "První doopravdový případ nalezení bugu"
        - Věta v denníku jednoho z vědců
<hr/>
</details>

- Mezi nástroje pro debuggování patří například i prostý `print()`, nebo nástroje v PyCharmu, či jiném IDE
  - Například při testování funkcí můžeme použít `print()` pro vypsání a následou kontrolu hodnoty v proměnné, před předáním proměnné do další funkce
- **Bisection debugging**
  - Zhruba v polovině kódu použijete `print()` pro získání relevantních hodnot proměnných v kódu
  - Pokud je vše tak jak má být, tak je první polovina kódu bez bugů
  - Pokud ne, tak to znamená, že druhá polovina kódu má bug
    - Zhruba ve 3/4 kódu použijete `print()` pro získání relevantních hodnot proměnných v kódu
    - ...
- **Vědecká metoda**
  1. Studování dostupných dat
    - Test case
  2. Hypotéta
    - _"Možná indexuji od 1 namísto od 0"_
  3. Experiment, který mohu opakovat
  4. Vyběr Test caseu, na kterém mohu hypotézu zkoušet
### Error message
- = Vyjímky
- Jsou velice jednoduché na opravení
  - Interpreter je společně s konkrétním řádkem označí
- `IndexError`
  - Pokus o přístup za hranice listu
  - ```Python
    test = [1,2,3]
    print(test[4])  # IndexError
- `TypeError`
  - Pokus o převod nevhodného typu 
  - ```Python
    int(test)  # TypeError
- `NameError`
  - Odkazování na neexistující proměnnou
  - ```Python
    print(a)  # NameError
- `TypeError`
  - Míchání datových typů
  - ```
    '3'/4  # TypeError
- `SyntaxError`
  - Zapomenutí na uzavření závorky, citace atd.
  - ```Python
    a = len([1,2,3]  # SyntaxError
    print(a)
- ...
### Logické chyby
- Při řešení logických problémů je dobré dělat si přestávky. Jít na čerstvý vzuch, najíst se, vyspat se...
- Je možné že bude i potřeba začít psát kód znovu od začátku
- Rubber ducky debbuging
  - Programátor vysvětluje svůj kód "gumové kachně" (Ideálně někdo, kdo nerozumí programování) (Klidně i té kachně)
  - Back to basics
### Co nedělat
- Psát celý kód
- Testovat celý kód
- Debuggovat celý kód
- Měnit celý kód
  - Zapamatovat kde je chyba
- Testovat kód
  - Zapomenout kde je chyba
- Panika 
### Co dělat
- Psát funkce
- Testovat funkce
- Debuggovat funkce
  - A znovu
    - = Integration testing
- Zálohovat kód
- Měnit kód
- Sepsat si potencionální bugy do komentářů
- Porovnat novou verzi kódu se starou
---
## Vyjímky (Exceptions)
- Pokud víme, že část kódu může vyvolat vyjímku, dokážeme ji **ošetřit**
  - Například **vstupní data od uživatele**
- K tomu používáme `try` bloky 
  - ```Python
    try: 
      a = int(input("Zadejte první číslo:"))
      b = int(input("Zadejte druhé číslo:"))
      print(a/b)
    except:
      print("Chyba v uživatelském vstupu")
- Výsledná error message je **hezčí** a **lépe čitelná** pro uživatele než klasická error message
- Co když ale chceme chytit určitou vyjímku?
  - ```Python
    try: 
      a = int(input("Zadejte první číslo:"))
      b = int(input("Zadejte druhé číslo:"))
      print("a/b = ", a/b)
      print("a+b = ", a+b)
    except ValueError:
      print("Nelze převést na číslo")
    except: ZeroDivisionError:
      print("Nelze dělit nulou")
    except:
      print("Něco se strašně posralo")
    ```
    - Poslední error chytí vše ostatní co není specificky deklarováno 
- Struktura `try` bloku
  - `try`
    - Do `try` vkládáme kód, u kterého očekáváme, že by mohl vyhodit vyjímku
  - `except`
    - Vkládáme kód, který se spustí, pokud kód v `try` vyhodí vyjímku
    - Můžeme specifikovat, kterou vyjímku chceme aby `except` "chytal"
  - `else`
    - Kód, který se spustí, pokud kód v `try` nevyhodí vyjímku
  - `finally`
    - Kód, který se spustí nehledě na to, co se stane s kódem v `try`
    - Vždy se spustí až po `try`, `else` a `except`
    - Pozn. autora : Moc nerozumím k čemu tohle je. Stačilo by vložit kód pod celý `try` blok, ale ok
- Jak se postavit k vyjímce
  - **Fail silently**
    - Přenastavíme hodnotu na nějakou defaultní hodnotu 
    - Není ideální, protože uživatel dostane něco jiného než chtěl
  - **Vrácení "error" hodnoty**
    - Není ideální, protože musíme ve zbytku kódu kontrolovat, zde funkce vrací dannou error hodnotu
  - **Vyvolání vlastní vyjímky**
```Python 
      raise <jmenoVyjimky>(<argumenty>)
      raise ValueError("Uživatel zadal záporné číslo")
    
      ```Python
      def get_ratios(L1, L2):
      """ Assumes: L1 and L2 are lists of equal length of numbers
          Returns: a lisr containing L1[i]/L2[i] """
      ratios = []
      for index in range (len(L1)):
        try:
          ratios.append(L1[index]/L2[index])
        except ZeroDivisionError:
          ratios.append(float('nan'))  # nan = not a number
        except:
          raise ValueError('get_ratios called with bad arg')
      return ratios
```

---
## Aserce (Asserions)
- Předpoklad pro hodnoty ve funkci
	- Elegantní řešeni kontroly vstupních a výstupních hodnot
- Při nesplnění vyvolá `AssertionError`
- Většinou se používají na začátku nebo na konci funkce
- Lze si představit jako past na bugy

  ```Python
  def avg(grades):
    assert not len(grades) == 0, 'no grades data'
    return sum(grades)/len(grades)
  ```
