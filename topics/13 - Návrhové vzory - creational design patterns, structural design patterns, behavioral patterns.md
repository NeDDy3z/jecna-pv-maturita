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
- **Proč je pořebujem?**  Aby pozdější úpravy byli co nejrychlejší, bezproblémové a cool


## Základní typy
- **Creational Patterns (vytvářející)**
	- Řeší problémy související s **vytvářením objektů v systému**
	- Zabývá se vytvářením a inicializací objektů
	- Poskytuje návod k tomu, které objekty se mají v dané situaci vytvořit
	- Používají se zejména ke zvýšení flexibility a k opakovanému použití stávajícího kódu.

- **Structural Patterns (strukturální)**
	- Skupina návrhových vzorů zaměřujících se na možnosti uspořádání jednotlivých tříd nebo komponent v systému
	- Strukturální návrhové vzory vysvětlují, jak sestavovat objekty a třídy do větších struktur a zároveň zachovat jejich flexibilitu a efektivitu
	- Poskytují způsob, jak definovat vztahy mezi komponentami aplikace, a jsou užitečné zejména ve větších a složitějších systémech

- **Behavioral Patterns (chování)**
	- Starají se o efektivní komunikaci mezi jednotlivými složkami systému
	- Zabývají se interakcí mezi objekty a přidělováním odpovědností mezi ně.
	- Cílem je, aby tyto procesy byly co nejjednodušší a nejsrozumitelnější.
- ----
- **Concurrency patterns (souběžné)** 
	- Více vláknové operace
	- Koordinace více procesl či vláken v softwarovém systému
	- Cílem je dosáhnout efektivnosti a bezpečnosti souběžného zpracování

## Druhy typů
- **Creational Patterns (Vzory tvorby)**:
	- **Tovární metoda**: vytváří objekty se společným rozhraním a umožňuje třídě jejich znázornění do podtřídy.
	- **Abstraktní továrna**: vytváří rodinu příbuzných objektů.
	- **Stavitel**: vzor pro vytváření složitých objektů krok za krokem, který odděluje konstrukci a reprezentaci.
	- **Prototyp**: podporuje kopírování existujících objektů, aniž by se kód stal závislým na třídách.
	- **Jedináček**: omezuje vytváření objektů třídy pouze na jednu instanci.

- **Structural Patterns (Strukturální vzory)**:
	- **Adaptér**: vzor, jak změnit nebo přizpůsobit rozhraní jiné existující třídě, aby nekompatibilní rozhraní mohla fungovat společně.
	- **Most**: metoda, jak oddělit rozhraní od jednotlivé implementace.
	- **Kompozit**: využívá stromovou strukturu pro podporu manipulace s jedním objektem.
	- **Dekorátor**: dynamicky rozšiřuje (přidává nebo přepisuje) funkce.
	- **Fasáda**: definuje vysokoúrovňové rozhraní pro zjednodušení používání rozsáhlého souboru kódu.
	- **Muší váha**: minimalizuje využití paměti sdílením dat s podobnými objekty.
	- **Zástupce**: způsob reprezentace objektu jiným objektem, který umožňuje řízení přístupu, snižuje náklady a složitost.

- **Behavioral Patterns (Chování)**:
	- **Řetězec odpovědnosti**: způsob delegování příkazů na řetězec zpracovávaných objektů.
	- **Příkaz**: zprostředkovává požadavek na příkaz do objektu.
	- **Interpret**: podporuje použití jazykových prvků v rámci aplikace.
	- **Iterátor**: podporuje iterativní (sekvenční) přístup k prvkům kolekce.
	- **Prostředník**: umožňuje jednoduchou komunikaci mezi třídami.
	- **Pamětník**: slouží k ukládání a obnově vnitřního/původního stavu objektu.
	- **Pozorovatel**: definuje způsob oznamování objektů o změnách jiných objektů.
	- **Stav**: jak se změní chování objektu, když se změní jeho fáze.
	- **Strategie**: zahrne algoritmus do třídy.
	- **Návštěvník**: definuje novou operaci na třídě, aniž by došlo k její změně.
	- **Šablonová metoda**: definuje kostru operace a zároveň umožňuje podtřídám upřesnit některé kroky.



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