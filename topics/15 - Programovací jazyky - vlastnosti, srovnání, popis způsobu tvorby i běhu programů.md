# [Programovací jazyky - vlastnosti, srovnání, popis způsobu tvorby i běhu programů](https://youtu.be/zVIofQ_HYoI?list=PLmW7bUCTvOeTSag9ZZBYXdHs_iEwB4OHM)

## O čem mluvit?
- Co je programovací jazyk?
	- různé jazyky
	- využití jazyků v různých zaměřeních
- Kompilace kódu
    - Kompilovaný / Interpretovaný / Virtuální stroj (např. JVM) jazyky
- Strojový kód
- Dělení podle abstrakce
    - Vyšší (Java..)
        - IMPERATIVNÍ
        - NEIMPERATIVNÍ
    - Nižší (Assembler..)
- *Objektové / Procedurální / Funkcionální jazyky*
- *Staticky / Dynamicky typované jazyky (JAVA vs Python..)*
- Popsat spouštění, běh a ukončení programu

## Základní pojmy
- prostředek, kterým zadáváme jednotlivé instrukce počítači 
- programovací jazyk je vlastně soubor pravidel pro zápis algoritmu, odborně řečeno se jedná o formální jazyk
- existuje mnoho jazyků, které se liší v implementaci, použitím, schopnostech, rychlosti, abstrakci (podle "levelu"), atd...
	- u některých jazyků se může jednat o "dialekt" určitého jiného jazyka
- existuje několik možných kritérií, podle kterých jazyky dělit

## Abstrakce 
#### Vyšší programovací jazyky (High-Level)
- čitelný a pochopitelný člověkem
	- rychleji se tvoří programy
	- méně programátorských chyb
		- vývojové prostředí zvýrazňuje napsané chyby a mnohdy ani nedovolí spustit program s nimi 
- vyšší programovací jazyky jsou obvykle pomalejší a mají větší nároky na paměť 
- nepracujeme s primitivním kódem jako v Low-Levelu
	- můžeme dělat složitější informace
	- (počítač vlastně neví, co je for each, procesor ho sám nezvládne - potřebujeme kompilátor)
- kompilátor zkompiluje kód
	- obvykle se kompilují do mezikódu, který je následně interpretován pro CPU
- Python, Java, C#, C++, atd...

#### Nižší programovací jazyky (Low-Level)
- pro člověka složitější na osvojení a méně čitelnější
- blíže strojovému kódu a hardwaru
	- jsou obvykle úzce spojeny s konkrétními architekturami a hardwarovými platformami
		- často používány pro účely přístupu k hardwaru, jako jsou ovladače, operační systémy a firmware
		- těžší je použít i jinde
- obvykle se kompilují přímo do strojového kódu
- rychlejší a mají menší nároky na paměť než High-Level
- např.: C v CITech na STM vývojové desce

###### Asmebler
- kód psaný v asembleru je kompilován pomocí překladače assembler na strojový kód
- assemblery jsou programovací jazyky, které umožňují programátorům psát instrukce, které jsou přímo srozumitelné CPU
	- tyto instrukce jsou obvykle zapsány ve formě mnemonik, což jsou zkrácené názvy pro strojové instrukce, např. MOV pro přesunutí dat. 
- assembler kód je tedy v podstatě jen lidsky čitelnou verzí strojového kódu 
	- stále je ale potřeba ho převést do strojového kódu

## Kompilace / Interpretace
#### Kompilované jazyky
- zdrojový kód se překládá na strojový kód jednou kompilací 
	- výsledný strojový kód pak může být spuštěn na cílovém počítači 
- kompilace může zabrat mnoho času
- pokud kód obsahuje chybu (odhalitelnou kompilátorem), tak kompilátor vyhodí chybu, díky tomu můžeme zjistit, kde je chyba před tím, než začneme spouštět program
- nevýhodou je že zkompilovaný program je závislý na platformě a na architektuře procesoru či OS
- C, C++, ...

#### Interpretované jazyky
- zdrojový kód se interpretuje postupně za běhu programu
- interpreter čte zdrojový kód a provádí ho bez překladu na strojový kód 
- přenositelný mezi platformami
	- nejprve je ale potřeba si stáhnout „tlumočníka“ který kód bude překládat
- nemusíme deklarovat datové typy, interpret při běhu programu automaticky rozpoznává typ každé proměnné podle její hodnoty a provádí příslušné operace
- Python, Ruby, JavaScript, ...

#### Hybridní jazyky či Jazyky s virtuálním strojem
- jazyky, které jsou kompilované i interpretované
- mohou mít překladový krok při kompilaci, ale také mohou být interpretovány při běhu programu
- např.: 
	- **Java** - vytváří *mezikód* v (pojmenován bytecode) - proběhne proces kompilace, ale zároveň se následně bude vytvořený kód interpretovat 
		- díky tomu není závislí na daném hardwaru + mezikód bude interpretován rychleji než zdrojový kód
	- nebo také **C#**

## Paradigmata
- způsoby jak zařadit programovací jazyky na základě jejich vlastností
	- prog. jazyky mohou být zařazeny do více paradigmat
- dělíme je na imperativní a deklarativní

#### Imperativní (procedurální)
- založeno na příkazech, které programu říkají, jak provádět určité kroky a jakým způsobem změnit stav proměnných
- strukturovaný
- OOP … je program vytvořen z objektů, objekt je instancí třídy, což je zapouzdření dat (tzv. Pole) a procedur (nazývaných metody), které s nimi manipulují.

#### Deklarativní (neprocedurální) 
- založeno na myšlence programování aplikací pomocí definic co se má udělat, a ne jak se to má udělat.
- **Funkcionální** programování chápe výpočet jako vyhodnocení matematických funkcí. Funkcionální programování má své kořeny v lambda-kalkulu, formálním systému vyvinutém v 30. letech k vyšetřování definicí funkcí, jejich aplikace a rekurze
- **Logické** programování je v širším významu použití matematické logiky jako prostředku pro programování.
- **Reaktivní** programování orientované kolem datových toků a šíření změn. To znamená, že by mělo být možné vyjádřit statické nebo dynamické datové toky v programovacích jazycích jednoduše a že základní provedení modelu bude automaticky kopírovat změny prostřednictvím datového toku.


## Syntaxe
- každý jazyk má svojí originální syntaxy = způsob zápisu
- v mnoha jazycích se využívají složité závorky *{ }* k vyznačení bloku kódu nebo funkcí *(C, C++, Java, JavaScript, atd...)*
- někde se používá odsazení - Python
- často se používá i středník na konci řádku *~~Python~~, GDScript, Bash, Java, C, C#, ...* 
	- vynechání středníku způsobuje syntax error
- např.:
	- ```c
	  // C
	  #include <stdio.h>
	  int main(void)
	  {
	  int i;
	  int *p;
	  i = 5;
	  p = &i;
	  printf("%d %d\n", *p, i);
	  printf("%d %d\n", p, &i);
	  return 0;
	  }  ```
	- ```java
	  // Java
	  public static void main(String[] args) {
	  System.out.println("hi");
	  }
	- ```python
	  def hello():
		  greeting = "hi"
	  return greeting
	  
	  goodbye = "bye"
	  print(hello(), goodbye) # "hi bye"```

## Způsoby tvorby a běhu programů

#### Tvorba programů
Při vytváření programů je důležité si předem vybrat vhodný jazyk, který bude splňovat požadavky programu který chceme vytvořit. (nebudu programovat AI v Bashi když mám Python).

K vytvoření programu budeme potřebovat IDE, neboli prostor pro vývoj programu, pro Javu - Eclipse/InteliJ IDEA, Python - PyCharm, C# - Studio Code, pro další (multifunkční) Vidual Studio Code, můžeme ale použít jakýkoliv textový editor. IDE nám jen usnadňuje vývoj pomocí např. debug, hledání syntax errorů v kódu, přímé spouštění v IDE, atd...

Dále můžeme použít ruzné návrhové vzory a architektury k usnadnění vývoje a lepší čitelnosti/funkcionalitě, například P2P, Client/Server, Fasáda, Command design pattern, atd... (určitě toho bude víc v tématu o architekturách)

#### Běh programu

Při spuštění programu se, podle použitého typu jazyku, kompiluje nebo interpretuje kód (už to bylo zmíněno nahoře), také možnost že se program spouští pomocí spustitelného souboru jako např. _.exe_.

Dochází k překladu kódu na strojový jazyk, který je procesor schopný pochopit a vykonat, program samotný pak běží, buďto jako daemon (v pozadí) nebo s nějakou uživatelskou interakcí (hra, prohlížeč, atd), do té doby dokud nedojde k:

- vypnutí systému
- vypnutí programu
- spadnutí programu (error v kódu, atd)

Tím je běh programu ukončen a všechno místo v paměti, které program zabíral, uvolněno pro jiné použití.
