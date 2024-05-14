# Návrhové vzory - creational design patterns, structural design patterns, behavioral patterns

## O čem mluvit?
- Návrhové vzory
	- co jsou zač
	- proč se používají
	- používají se jenom ve světě IT? Ne.
	- zmínit GoF
- Základní typy
	- v čem se liší
	- jejich podtypy a jak fungují
	- dokumentace

## Návrhové vzory
- Představují obevné řešení problému, které se využívá při návrhu programů
- Jedná se o popis řešení problému nebo šablonu, která mlžu být použita v různých situacích
- **Algoritmy nejsou považovány za návrhové vzory, jelikož řeší konkrétní problémy a nikoliv problémy návrhu**
- Návrhovo vzory můžem najít taky mimo IT, např. v architektuře. Málo kdy totiž uvidíte jinak postavený dům a to je tím, že je už ověřený vzor domu, který se případně, dle potřeb upraví
- GoF (Gank of Four) je skupinka C# nerdu, kteří napsali knihu "Design Patterns", která se zabývá klady a zápory "object-oriented programming" a návrhovíma vzorama

## Základní typy
- **Creational Patterns (vytvářející)**
	- Řeší problémy související s **vytvářením objektů v systému**
	- Snaha o **popsání postupu výběru třídy nového objektu** a zajištění správného počtu těchto objektů
	- Většinou se jedná o dynamická rozhodnutí učiněná za běhu programu
- **Structural Patterns (strukturální)**
	- Skupina návrhových vzorů zaměřujících se na možnosti uspořádání jednotlivých tříd nebo komponent v systému
	- Snahou je zpřehlednit systém a využít možností strukturalizace kódu.
- **Behavioral Patterns (chování)**
	- Chování systému
	- Založeny na třídách nebo objektech
	- u tříd se při návrhu řešení využívá princip dědičnosti
- ----
- **Concurrency patterns (souběžné)** 
	- Více vláknové operace
	- Koordinace více procesl či vláken v softwarovém systému
	- Cílem je dosáhnout efektivnosti a bezpečnosti souběžného zpracování

## Druhy typů
- **Creational Patterns (Vzory tvorby)**:
	- **Abstract Factory**:
	    - *"groups object factories that have a common theme."*
	    - Tento vzor poskytuje rozhraní pro vytváření rodin souvisejících nebo závislých objektů bez specifikování jejich konkrétních tříd. To umožňuje vytváření objektů s ohledem na jejich rodinné vztahy.
	- **Singleton**:
	    - *"restricts object creation for a class to only one instance."*
	    - Singleton je vzor, který zajistí, že určitá třída má pouze jednu instanci a poskytuje globální přístup k této instanci. Tento vzor se používá, když chceme, aby určitá třída měla pouze jednu instanci po celou dobu běhu aplikace.
	- **Builder**:
	    - *"constructs complex objects by separating construction and representation."*
	    - Slouží k abstrahování tvorby složitých objektů. A to tak, aby stejné výrobní schéma mohlo být použito pro tvorbu různých objektů. Někdy se využívá společně s návrhovím vzorem Compsite
	- **Object Pool**:
	    - Tento vzor umožňuje předem vytvořit a udržovat určitý počet předem vytvořených objektů v "bazénu". Namísto opakovaného vytváření nových objektů můžeme použít objekty z tohoto bazénu a po použití je vrátit zpět.

- **Structural Patterns (Strukturální vzory)**:
	- **Proxy**:
	    - *"provides a placeholder for another object to control access, reduce cost, and reduce complexity."*
	    - Proxy je vzor, který poskytuje náhradu nebo zástupce za jiný objekt, aby mohl kontrolovat přístup k tomuto objektu. Tento zástupce může provádět různé operace, jako je ověření, před a po volání reálného objektu.
	- **Decorator**:
	    - *dynamically adds/overrides behavior in an existing method of an object.*
	    - Tento vzor umožňuje přidávat nové funkcionality nebo chování k existujícím objektům dynamicky, bez nutnosti změny jejich struktury. To je dosaženo pomocí kompozice, kdy jsou objekty obaleny dalšími objekty, které poskytují další funkcionalitu.
	- **Bridge**:
	    - *decouples an abstraction from its implementation so that the two can vary independently.*
	    - Bridge je vzor, který rozděluje abstrakci od její implementace, takže mohou být obě nezávisle měněny. To umožňuje hierarchickou strukturu a umožňuje jednodušší rozšíření funkcí.
	- **Adapter**:	
		- *allows classes with incompatible interfaces to work together by wrapping its own interface around that of an already existing class.*
	    - Tento vzor umožňuje propojení dvou nekompatibilních rozhraní tak, aby mohly spolupracovat. To je dosaženo pomocí třetí třídy, která převádí volání mezi dvěma rozhraními.

- **Behavioral Patterns (Chování)**:
	- **Observer** (Minecraft!!):
		- *is a publish/subscribe pattern, which allows a number of observer objects to see an event.*
	    - Tento vzor definuje závislost mezi objekty tak, že když se stav jednoho objektu změní, všechny jemu závislé objekty jsou automaticky informovány a aktualizovány. To je v Minecraftu například použito pro události typu "když hráč změní svou polohu".
	- **Chain of Responsibility**:
		- *delegates commands to a chain of processing objects.*
	    - Tento vzor umožňuje spojení řady objektů, zvaných "handler", kde každý handler má možnost zpracovat požadavek a předat ho dalšímu handleru v řetězci, pokud nemůže požadavek zpracovat sám.
	- **Iterator**:
		- *accesses the elements of an object sequentially without exposing its underlying representation.*
	    - Iterator je vzor, který poskytuje způsob, jak přistupovat k prvkům v kolekci bez nutnosti znát její vnitřní strukturu. To umožňuje iteraci přes prvky kolekce jednoduše pomocí univerzálního rozhraní.
	- **Interpreter**:
		- *implements a specialized language.*
	    - Tento vzor definuje způsob, jak přeložit nebo interpretovat určitý jazyk nebo gramatiku. Tento vzor je často používán ve spojení s parserem pro analýzu a vykonání složitých jazykových konstrukcí.

## Dokumentace návrhového vzoru
-  **Název a klasifikace Vzoru:** Unikátní jméno, které dostatečným způsobem popisuje vzor, pomáhá v jeho identifikaci a odkazování se na něj.
- **Cíl:** Popis cíle, kvůli kterému vzor vznikl
- **Také znám jako:** Jiné názvy pro stejný vzor.
- **Kontext:** Architektonická či designová situace kde je popis vzoru užitečný (platný).
- **Motivace (protichůdné síly):** Popis problému, který má daný vzor řešit
- **Použití:** Situace, ve kterých lze daný vzor použít. Jde o kontext vzoru.
- **Struktura:** Grafické znázornění vzoru. Pro tento účel mohou být použity class diagramy nebo interaction diagramy.
- **Účastníci:** Výpis tříd a objektů, které tento vzor používá a jejich role v návrhu.
- **Spolupráce:** Popis toho, jak spolu třídy použité v daném vzoru komunikují.
- **Důsledky:** Popis výsledků, vedlejších efektů a problémů, které přináší použití daného vzoru.
- **Implementace:** Popis implementace vzoru.
- **Ukázkový kód:** Ilustrace toho, jak může být daný vzor použit v nějakém programovacím jazyce.
- **Známá použití:** Příklady praktického využití daného vzoru.
- **Související vzory:** Jiné vzory, které jsou v nějakém vztahu s tímto vzorem. Diskuze rozdílů mezi tímto vzorem a vzory jemu podobnými.