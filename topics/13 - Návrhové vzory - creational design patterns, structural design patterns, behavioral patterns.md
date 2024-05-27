# Návrhové vzory - creational design patterns, structural design patterns, behavioral patterns

## O čem mluvit?
- Návrhové vzory
	- řešení známých a častých problémů 
	- používají se jenom ve světě IT? Ne.
	- zmínit GoF
- Základní typy

   - Creational
      - zemruje se na vytváření objektů 
      - Singleton, Factory
  	- Structual
      - organizace tříd a objektů aby dobre komunikovali
      - Fasade - jednotne rozhraní pro pouzivani enjakeho komplexnoho systému
      - Adapter - umoznuje pracovani objektů s nekompatibilním rozhraním 
  	- Behavioural
      - chicani mezi objekty a třídami 
      - Iterator - prochazeni objekti bez znalosti jejich vnitřnosti, procházení listu třeba 

## Návrhové vzory
- obecná řešení často vyskytujících se problémů v architektuře softwaru
- nejedná se o knihovnu nebo přesný kus kódu, ale popsání postupu / šablona, jak problém řešit
- řeší různé problémy, jako je například omezení výkonu počítače
- **algoritmy nejsou považovány za návrhové vzory, jelikož řeší konkrétní problémy a nikoliv problémy návrhu**
- návrhové vzory můžeme najít taky mimo IT, např. v architektuře. Málo kdy totiž uvidíte jinak postavený dům a to je tím, že je už ověřený vzor domu, který se případně, dle potřeb upraví
- GoF (Gank of Four) je skupinka C# nerdu, kteří napsali knihu "Design Patterns", která se zabývá klady a zápory "object-oriented programming" a návrhovíma vzorama

#### Dělíme na
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

## Creational Design Patterns
- snahou je popsat postup výběru třídy nového objektu a zajištění správného počtu těchto objektů
- každý z nich nabízí možnosti zpřehlednění nebo zefektivnění kódu.
- mezi tyto vzory patří např:
	- Singleton – zajistí, že třída má pouze jednu instanci a poskytuje globální přístup k ní
	- Object Pool
	- Factory Metoda – vytváří objekty pomocí metody továrny, která deleguje vytváření na sub-třídy

#### Object Pool
- využívá se v situaci, když je náročnější (vyžaduje více výkonu) vytvoření instance nějaké třídy
- je to jednoduše kontejner který obsahuje nějaký počet objektů dané třídy
	- takže ve chvíli, kdy je objekt vypůjčen z pool stane se nedostupný až do té chvíle kdy je navrácen
- na podobném principu funguje multiprocessing.

Výhody:
- Minimalizuje náklady na vytváření a ničení objektů, což zvyšuje výkon a snižuje paměťové nároky.
- Zlepšuje efektivitu systému tím, že poskytuje opakované využití objektů.
- Umožňuje omezit počet objektů vytvářených a používaných v systému, což pomáhá zabránit zahlcení paměti a zvyšuje stabilitu systému.
- Může pomoci zabránit problémům s konkurencí a zlepšit synchronizaci vláken v systému.

Nevýhody:
- Může být obtížné určit správnou velikost poolu objektů, což může vést k nadměrné spotřebě paměti nebo k nedostatku objektů.
- Může být složité synchronizovat vlákna v případě, že více vláken současně přistupuje k poolu objektů.
- Může vést k vytváření objektů, které nejsou využity, což může vést k zbytečné spotřebě paměti a snížení výkonu systému.

#### Singleton
- umožňuje vytvořit pouze jedinou instanci dané třídy
- používáme ho např. v manažeru připojení k databázi nebo v místech, kde chceme globální správu pouze jednou entitou. Návrhový vzor singleton je doporučeno spíše nepoužívat.

Výhody:
- Zajišťuje, že třída má pouze jednu instanci v systému, což snižuje paměťové nároky a zvyšuje výkon.
- Poskytuje globální přístup k instanci třídy, což usnadňuje používání objektu v celém systému.
- Je vytvořen až ve chvíli kdy je poprvé potřeba

Nevýhody:
- Může být obtížné testovat třídu, protože singleton třídy jsou globálně přístupné.
- Singleton třídy mohou vést k vytváření tvrdých závislostí v kódu, a tedy zhoršit modularitu.
- Není jednoduché používat singlton ve více vláknovém prostředí, protože musíme se starat aby jednotlivá vláka nevytvořili singlton vícekrát.

#### Factory Method
- používáme, když máme několik tříd, implementujících stejný interface nebo, ze kterých můžeme udělat instance a chceme nechat rozhodnout program, která z těchto tříd bude nejlepší
- také používáme, když chceme vytvářet instance z těchto tříd na základě určité business logiky nebo jiných podmínek

Výhody:
- Poskytuje rozhraní pro vytváření objektů, což umožňuje oddělení vytváření objektů od jejich použití.
- Umožňuje snadnou výměnu konkrétní implementace objektu bez změny kódu v klientovi.
- Zlepšuje modularitu kódu a udržitelnost.

Nevýhody:
- Vyžaduje vytvoření sub-tříd pro každou konkrétní implementaci objektu, což může vést k velkému počtu tříd v systému.
- Může být komplikované zjistit, kterou sub-třídu použít pro vytvoření správného objektu, pokud jich existuje více.

## Structural design pattern
Structural Patterns představují skupinu návrhových vzorů zaměřujících se na možnosti uspořádání jednotlivých tříd nebo komponent v systému. Snahou je zpřehlednit systém a využít možností strukturalizace kódu.
- Fasáda –Ulehčuje komunikaci suživatelem.  
- Proxy – prostředním v komunikaci

#### Fasáda
- poskytuje jednotné rozhraní pro celou skupinu tříd, což umožňuje klientům jednodušší a srozumitelnější přístup k systému
- skrývá komplexitu systému a izoluje klienta od jeho interní implementace

Výhody:
- Poskytuje jednoduché a srozumitelné rozhraní pro komunikaci s komplexním systémem.
- Skrývá komplexitu systému a izoluje klienta od jeho interní implementace.
- Umožňuje snadné řízení přístupu k systému a umožňuje správu systému na jednom místě.

Nevýhody:
- Fasáda může být omezením pro pokročilejší uživatele, kteří potřebují více přístupu ke komponentám systému.
- Přidání dalších funkcí nebo komponent do systému může být složité a náročné na úpravu Fasády.

#### Proxy
- je strukturální vzor, který umožňuje vytvořit prostředníka mezi klientem a skutečným objektem
- jeho asi nejčastější použití je zapouzdření instance jiného objektu nebo přidání pomocné funkčnosti
- úroxy nám tedy umožňuje řídit přístup ať už k celému či částečnému rozhraní objektu přes nějaký jiný zastupující objekt (proxy – zástupce, reprezentant)

Typy:
- Remote Proxy – Proxy může být použit pro přístup k vzdálenému objektu, který je uložen na jiném serveru nebo počítači.
- Virtual Proxy – Proxy může být použit pro zpřístupnění velkého objektu, který zabírá mnoho paměti, ale části objektu se používají jen zřídka. Proxy objekt pak inicializuje jen ty části objektu, které jsou potřeba.
- Protection Proxy – Proxy může být použit pro kontrolu přístupu k objektu, když je potřeba ověřit, zda má klient oprávnění k provedení určité akce.
- Reverse Proxy – load balancer Reverse Proxy funguje na principu množiny serverů, jenž všechny jsou co se týče obsahu identické. Zátěž je rozdělena na základě zatížení jednotlivých serverů, přičemž může být orientována dle výkonu serveru, či jeho již stávajícího vytížení.

Výhody:
- Oddělení klienta od skutečného objektu umožňuje snadné dodání nové funkcionality bez nutnosti měnit kód klienta nebo skutečného objektu.
- Proxy může být použit pro optimalizaci výkonu, když není nutné inicializovat skutečný objekt, dokud není skutečně potřeba.
- Proxy umožňuje snadné řízení přístupu k objektu, když je potřeba zabezpečit určitou funkci nebo data.

Nevýhody:
- Přidání dalšího prostředníka mezi klienta a skutečný objekt může snížit výkon a zpomalit systém.
- Komunikace přes proxy může způsobit komplikace v případě, že objekt vyžaduje okamžitou odpověď, protože proxy zpomaluje přístup k objektu.

## Behavior patterns
tyto vzory se používají pro definování interakcí mezi objekty a třídami v systému
- Iterátor –Umožňuje nám procházet prvky v různých strukturách.
- Null Object –Nahrazuje null hodnotu.

#### Iterátor
- návrhový vzor, který umožňuje procházet prvky kolekce bez ohledu na způsob, jakým jsou uloženy
- poskytuje jednotné rozhraní pro přístup k prvkům kolekce, což umožňuje snadnou iteraci a práci s daty
- můžeme jednoduše procházet prvky kolekce bez znalosti vnitřního mechanismu, který je použit pro uložení dat

Výhody:
- Umožňuje snadnou iteraci a práci s daty bez nutnosti znalosti vnitřního mechanismu kolekce
- Jednoduše se používá v kombinaci s dalšími návrhovými vzory, jako je například Fasáda nebo Strategie

Nevýhody:
- Může být pomalý, pokud se používá s velkými datovými strukturami
- Nelze použít na některé specifické datové struktury, které nejsou iterovatelné, například stromy nebo grafy. V takových případech je třeba použít jiné návrhové vzory, jako je například Prohlížeč (Visitor) nebo Návštěvník (Traversal).

#### Null Object
- umožňuje nahradit null hodnoty objektům, které implementují stejný rozhraní, jako jsou ostatní objekty
- poskytuje objekt s výchozími hodnotami, který může být použit místo null hodnoty, a to bez nutnosti vytvářet složitou logiku pro kontrolu null hodnot
- pomáhá minimalizovat problémy s chybějícími hodnotami a umožňuje snadnější testování kódu a eliminovat většinu problémů sním spojeným, jako NullPointerException a podobné

Výhody:
- Minimalizuje problémy s chybějícími hodnotami a zlepšuje stabilitu aplikace
- Umožňuje snadnější testování kódu
- Snadno se používá v kombinaci s dalšími návrhovými vzory, jako je například Iterátor

Nevýhody:
- Může zvýšit nároky na paměť, protože objekty s výchozími hodnotami mohou být vytvářeny často
- Může být náročné implementovat u složitějších objektů

## Dokumentace návrhového vzoru
- **Název a klasifikace Vzoru:** Unikátní jméno, které dostatečným způsobem popisuje vzor, pomáhá v jeho identifikaci a odkazování se na něj.
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
