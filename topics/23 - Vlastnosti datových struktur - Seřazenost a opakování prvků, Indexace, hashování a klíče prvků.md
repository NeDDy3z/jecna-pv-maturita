# 23 - Vlastnosti datových struktur - Seřazenost a opakování prvků, Indexace, hashování a klíče prvků

## O čem mluvit?
- Datová struktura
	- co to je?
	- k čemu to je
	- What's the deal...
	- základní vlastnosti
		- časova/prostorová složitost, dynamická/statická alokace...
	- typy
		- lineární: Array, List, Stack,...
		- selineární: Graphs, Trees
		- kdy se co na co hodí
- zbytek
## Úvod do datových struktur

- Datová struktura je způsob, jak organizovat a ukládat data tak, aby se s nimi dalo efektivně pracovat
- Správná volba datové struktury je klíčová pro efektivitu programu, protože ovlivňuje rychlost operací jako je vyhledávání, vkládání nebo mazání dat
- What's the deal with airline food?
![](../images/1200x791-1105816986.jpg)
## Základní vlastnosti datových struktur

- **Časová složitost:** Měří, jak dlouho trvají operace nad datovou strukturou. Používají se notace jako O(1), O(n), O(log n) apod.
- **Prostorová složitost:** Udává, kolik paměti datová struktura zabírá.
- **Dynamická vs. statická alokace:** 
	- Dynamické datové struktury mohou měnit svou velikost za běhu programu (např. seznamy) 
	- Statické mají pevně danou velikost (např. pole)
- **Imutabilita vs. mutabilita:** 
	- Imutabilní datové struktury nelze po vytvoření měnit (např. řetězce v některých jazycích)
	- Mutabilní ano
- **Seřazenost a opakování prvků:** 
	- Některé datové struktury (např. sety) neumožňují opakování prvků a někdy jsou seřazené
	- Jiné (např. seznamy) umožňují opakování a nemusí být seřazené.
- **Indexace:** Schopnost přistupovat k prvkům na základě jejich pozice nebo klíče.
- **Hashování a klíče prvků:** Metoda mapování dat na indexy pomocí hashovací funkce.

## Typy datových struktur

- **Lineární datové struktury:**
    
    - **Pole (Arrays):** Pevná velikost, rychlý přístup k prvkům pomocí indexu.
    - **Seznamy (Lists):** Dynamická velikost, umožňuje snadné vkládání a mazání prvků.
    - **Zásobníky (Stacks):** LIFO (last in, first out), operace push (vložení) a pop (odebrání).
    - **Fronty (Queues):** FIFO (first in, first out), operace enqueue (vložení) a dequeue (odebrání).
- **Nelineární datové struktury:**
    
    - **Stromy (Trees):** Hierarchická struktura složená z uzlů a hran.
    - **Grafy (Graphs):** Sada vrcholů a hran, mohou být směrované nebo nesměrované.
    - **Hash tabulky (Hash Tables):** Umožňují efektivní vyhledávání pomocí hashovacích funkcí.
## Praktické použití a příklady

- **Pole:** Používají se tam, kde je potřeba rychlý přístup k prvkům pomocí indexu (např. tabulky).
- **Seznamy:** Vhodné pro dynamické datové struktury, kde se často mění velikost (např. fronty v tiskových úlohách).
- **Zásobníky:** Používají se v rekurzivních algoritmech a při řešení problémů typu "zpět".
- **Fronty:** Vhodné pro správu úloh, které přicházejí postupně (např. fronty v síťových zařízeních).
- **Stromy:** Používají se pro reprezentaci hierarchických dat (např. souborové systémy).
- **Grafy:** Vhodné pro modelování sítí (např. sociální sítě, mapy).
- **Hash tabulky:** Používají se tam, kde je potřeba rychlé vyhledávání (např. databáze).
## Specifické vlastnosti a operace jednotlivých datových struktur

- **Pole:**
    - Rychlý přístup k prvkům (O(1)).
    - Pevná velikost.
    - Náročné vkládání a mazání prvků (O(n)).
- **Seznamy:**
    - Dynamická velikost.
    - Snadné vkládání a mazání prvků (O(1) pro vkládání/mazání na začátek).
    - Pomalejší přístup k prvkům (O(n)).
- **Zásobníky:**
    - Operace LIFO.
    - Rychlé vkládání a odebírání prvků (O(1)).
- **Fronty:**
    - Operace FIFO.
    - Rychlé vkládání a odebírání prvků (O(1)).
- **Stromy:
    - Hierarchická struktura.
    - Průchody: in-order, pre-order, post-order.
    - Efektivní vyhledávání, vkládání a mazání prvků (O(log n) pro vyvážené stromy).
- **Grafy:
    - Vrcholy a hrany.
    - Algoritmy pro průchod a hledání nejkratší cesty (DFS, BFS, Dijkstra).
- **Hash tabulky:
    - Hashovací funkce pro rychlé vyhledávání (O(1) v průměru).
    - Řešení kolizí pomocí různých metod (řetězení, otevřené adresování).

## Seřazenost a opakování prvků

- **Sety (Sets):** Neumožňují opakování prvků a mohou být buď seřazené (např. TreeSet) nebo neseřazené (např. HashSet).
- **Seznamy (Lists):** Umožňují opakování prvků a obvykle nejsou seřazené, pokud není explicitně požadováno.

## Indexace, hashování a klíče prvků

- **Indexace:** Umožňuje přístup k prvkům na základě jejich pozice v datové struktuře, typicky se používá v polích a seznamech.
- **Hashování:** Proces převodu klíče na index pomocí hashovací funkce. Klíč je vstupní hodnota, kterou hashovací funkce mapuje na specifický index v hash tabulce. Hashování je klíčové pro rychlé vyhledávání v hash tabulkách.

## Sorting objektů a implementace Comparable

- **Sorting (Řazení):** Proces uspořádání prvků podle určitého pořadí (např. vzestupně nebo sestupně).
    - **Comparable:** Rozhraní, které objekty implementují, aby bylo možné je porovnávat a třídit. Definuje metodu compareTo(), která určuje přirozené pořadí objektů.
    - **Comparator:** Další rozhraní, které umožňuje definovat externí pořadí objektů. Definuje metodu compare(), která umožňuje vytvořit více řazení pro stejnou třídu.

## HashSet a HashMap/Dictionary

- **HashSet:** Implementace rozhraní Set, která používá hash tabulku k ukládání prvků. Neumožňuje duplikáty a neudržuje pořadí prvků.
- **HashMap/Dictionary:** Implementace rozhraní Map, která používá hash tabulku k ukládání dvojic klíč-hodnota. Umožňuje efektivní vyhledávání, vkládání a mazání prvků na základě klíče.

