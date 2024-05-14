# [Testování, Unit testování a dokumentace zdrojového kódu](https://youtu.be/8X5PS8CZyIs?si=cg49xrzwNqY5VgCP)0

---
## O čem mluvit
-
---
## Testování
- Proces při kterém porovnáváme očekavané výsledky s doopravdovými výsledky
- Nejdříve si musíme dát dohromady nějaké vstupní hodnoty (**test case**). Ty pak vložíme do naší funkce.
    - Je výsledek takový jaký jsme očekávali?
        - Ano
            - Výborně!
        - Ne
            - -> Debugging
- Testování napomáha při objevování potencionálních chyb
    - "Jak mohu tento kód rozbít?"
- **Kdy testujeme?**
    1. Kód musí být spustitelný
        - Eliminace (nejen) syntaxových errorů
    2. Test case
        - Množina párů vstupů a výstupů na základě toho, co od kódu očekáváme
- **Typy testování**
    - **Unit testy**
        - Testování kódu v malém izolovaném prostoru
        - Každou funckci testujeme samostatně
    - **Regression testing**
        - Pokud nalezneme v Unit testu bug, funkci opravíme a používáme Regression testing
        - Kontroluje, zda opravení bugu nevyrobylo nové chyby ve zbytku kódu
        - Pokud ano, vracíme se k **Unit testingu**
    - **Integration testing**
        - Testování programu jako celek
        - Testuje zda jednotlivé bloky kódu spolu interagují tak jak mají
        - Pokud ne, vracíme se k **Regression testingu**
- **Postup testování**
    - **Intuice**
        - Méně přesné testování
        - ```Python
            def is_bigger(x, y):
            """ Assumes x and y are ints
            Returns True if y is less than x, else False """
        - V tomto kódu můžeme použít tyto porovnání:
            - ```x < y```
            - ```x > y```
            - ```x = y```
            - ```x <= y```
            - ```x >= y```
        - Pokud se jedná o sloužitější kód, používáme **random testing**
            - Čim více uděláme random testů, tím větší je pravděpodobnost, že je náš kód správný
    - Black box testování
    - Glass box testování
### **Black box testování**
- <details><hr/><summary><a>Obrázek</a></summary><img src="../images/24_black_box.png"><p>Blackbox, protože nevidíme dovnitř</p><hr/></details>
- <details><summary><a>Příklad testování</a></summary>
    <hr/>
  
    ```python
    def sqrt(x, eps):
        """ Assumes x, eps floats, x>= 0, eps > 0
        Returns res such that x=eps <= res*res <= x+eps """
    ```
  <table>
    <tr>
      <th>CASE</th>
      <th>x</th>
      <th>eps</th>
    </tr>
    <tr>
      <td>boundary</td>
      <td>0</td>
      <td>0.0001</td>
    </tr>
    <tr>
      <td>perfect square</td>
      <td>25</td>
      <td>0.0001</td>
    </tr>
    <tr>
      <td>less than 1</td>
      <td>0.05</td>
      <td>0.0001</td>
    </tr>
    <tr>
      <td>irrational square root</td>
      <td>2</td>
      <td>0.0001</td>
    </tr>
    <tr>
      <td>extremes</td>
      <td>2</td>
      <td>1.0/2.0**64.0</td>
    </tr>
    <tr>
      <td>extremes</td>
      <td>1.0/2.0**64.0</td>
      <td>1.0/2.0**64.0</td>
    </tr>
    <tr>
      <td>extremes</td>
      <td>2.0**64.0</td>
      <td>1.0/2.0**64.0</td>
    </tr>
    <tr>
      <td>extremes</td>
      <td>1.0/2.0**64.0</td>
      <td>2.0**64.0</td>
    </tr>
    <tr>
      <td>extremes</td>
      <td>2.0**64.0</td>
      <td>2.0**64.0</td>
    </tr>
  </table>
  <hr/>
  </details>

    - Testy vytváříme na základě specifikací a požadavků, které o funkci víme, nikoliv na základě kódu samotného
    - Black box testy budou vždy fungovat nehledě na to, jak někdo dannou funcki implementuje
        - Pokud ji samozřejmě implementuje podle danných specifikací :)
    - Rysy
        - Nezávislost na vnitřní implementaci (na programátorovi)
        - Založeno na specifikacích a požadavcích
### **Glass box testování**
- <details><summary><a>Příklad</a></summary><hr/>

  ```Python
  def abs(x):
    """ Assumes x is an int
    Returns x if x>=0 and -x otherwise """
    if x < -1:
        return -x
    else:
        return x
  ```
  
  - Path complete může přejít chybu
  - Path complete je v tomto případě `2` a `-2`
  - Ale `abs(-1)` nesprávně vrací `-1`
  - Musíme kontrolovat i boundary cases (`-1`)
  <hr/>
  </details>

- Narozdíl od blackbox testování používáme samotný kód
- Path complete test je test Case, který prochází každou možnou cestou v kódu
- Problém přichází u cyklů
    - "Kód neprojde cyklem ani jednou"
    - "Kód projde cyklem jednou"
    - "Kód projde cyklem dvakrát"
    - ...
    - Možnost velmi velkého testu
- **Pravidla glassbox testování**
    - **Větvení**
        - Musíme mít test case, který prochází všechny možné větve
    - **Cykly**
        - Musíme mít test case, který
            - Neprochází cyklem
            - Prochází cyklem
                - Jednou
                - Vícekrát
        - **While cykly**
            - Stejné jako ostatní cykly
            - Test casy, které zachycují všechny možné způsoby opuštění cyklu
