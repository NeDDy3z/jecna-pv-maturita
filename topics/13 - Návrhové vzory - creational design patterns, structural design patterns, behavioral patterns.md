# Návrhové vzory - creational design patterns, structural design patterns, behavioral patterns

## O čem mluvit?
- Návrhové vzory
	- řešení známých a častých problémů 
	- používají se jenom ve světě IT? Ne
	- zmínit GoF
- Základní typy:
	- Creational
	      - zaměřuje se na vytváření objektů 
	      - Singleton, Factory
	- Structual
	      - organizace tříd a objektů aby dobře komunikovali
	      - Fasade - jednotne rozhraní pro pouzivani enjakeho komplexního systému
	      - Adapter - umožňuje pracovaní objektů s nekompatibilním rozhraním 
	- Behavioural
	      - chování mezi objekty a třídami 
	      - Iterator - prochazení objektů bez znalosti jejich vnitřnosti (např. listu)

## Návrhové vzory
- obecná řešení často vyskytujících se problémů v architektuře SW
- nejedná se o knihovnu nebo přesný kus kódu, ale popsání postupu / šablona, jak problém řešit
- **algoritmy nejsou považovány za návrhové vzory, jelikož řeší konkrétní problémy a nikoliv problémy návrhu**
- návrhové vzory můžeme najít taky mimo IT, např. v architektuře. Málo kdy totiž uvidíte jinak postavený dům a to je tím, že je už ověřený vzor domu, který se případně, dle potřeb upraví
- GoF (Gank of Four) je skupinka C# nerdu, kteří napsali knihu "Design Patterns", která se zabývá klady a zápory "object-oriented programming" a návrhovíma vzorama

#### Dělíme na
- **Creational Patterns (vytvářející)**
	- řeší problémy související s vytvářením a inicializací objektů
	- poskytují návod k tomu, které objekty se mají v dané situaci vytvořit

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
- každý z nich nabízí možnosti zpřehlednění nebo zefektivnění kódu
- mezi tyto vzory patří např:
	- Singleton
	- Object Pool
	- Factory Metoda
#### Singleton
- umožňuje vytvořit pouze jedinou instanci dané třídy
- je k ní globální přístup
- horší modularita
- ve vícevláknovém prostředí není jednoduché se o něj starat (musíme hlídat aby fakt byl jen jeden)
- např.: 
	- připojovník k DB
	- globální správu pouze jednou entitou
	- logger

C#
```csharp
using System;

public class Singleton
{
    // Privátní statická proměnná pro uložení instance singletonu
    private static Singleton instance;

    // Objekt pro synchronizaci vláken pro dvojité zámkování
    private static readonly object lockObject = new object();

    // Privátní konstruktor zabrání vytvoření instance třídy zvenčí
    private Singleton() { }

    // Metoda pro získání instance singletonu
    public static Singleton GetInstance()
    {
        // Použití dvojitého zámkování pro vláknovou bezpečnost
        if (instance == null)
        {
            lock (lockObject)
            {
                // Další kontrola, zda instance nebyla již vytvořena jiným vláknem
                if (instance == null)
                {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }

    // Metoda, kterou může singleton provádět
    public void DoSomething()
    {
        Console.WriteLine("Singleton instance is doing something.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Získání instance singletonu
        Singleton singleton1 = Singleton.GetInstance();
        Singleton singleton2 = Singleton.GetInstance();

        // Ověření, že obě proměnné odkazují na stejnou instanci
        Console.WriteLine(singleton1 == singleton2);  // Vypíše: True

        // Použití singletonu
        singleton1.DoSomething();
    }
}

```
#### Factory Method
- vhodný pro třídy/objekty se stejným interfacem
- v nadřazené třídě se definují základní objekty/funkce a podtřídy si pak jen volí jaké z nich instantizuje a jaké funkce použije (může je také upravit)
- zlepšuje modularitu kódu a udržitelnost
- umožňuje snadnou výměnu konkrétní implementace objektu bez změny kódu v klientovi

## Structural design pattern
- zaměřuje se na uspořádání jednotlivých tříd nebo komponent v systému
- snahou je zpřehlednit systém a využít možností strukturalizace kódu
- patří sem:
	- Fasáda –Ulehčuje komunikaci suživatelem
	- Proxy – prostředním v komunikac

#### Fasáda
- poskytuje jednotné rozhraní pro celou skupinu tříd, což umožňuje klientům jednodušší a srozumitelnější přístup k systému
- skrývá komplexitu systému a izoluje klienta od jeho interní implementace
	- může být omezením pro pokročilejší uživatele co chtějí vidět více do vnitřností
- například v komunikaci s DB
#### Proxy
- umožňuje vytvořit prostředníka mezi klientem a skutečným objektem
- nejčastější použití je zapouzdření instance jiného objektu nebo přidání pomocné funkčnosti
- řídí přístup ať už k celému či částečnému rozhraní objektu přes nějaký jiný zastupující objekt (proxy = zástupce, reprezentant)
- může zpomalit systém

Typy:
- Remote Proxy – Proxy může být použit pro přístup k vzdálenému objektu, který je uložen na jiném serveru nebo počítači.
- Virtual Proxy – Proxy může být použit pro zpřístupnění velkého objektu, který zabírá mnoho paměti, ale části objektu se používají jen zřídka. Proxy objekt pak inicializuje jen ty části objektu, které jsou potřeba.
- Protection Proxy – Proxy může být použit pro kontrolu přístupu k objektu, když je potřeba ověřit, zda má klient oprávnění k provedení určité akce.
- Reverse Proxy – load balancer Reverse Proxy funguje na principu množiny serverů, jenž všechny jsou co se týče obsahu identické. Zátěž je rozdělena na základě zatížení jednotlivých serverů, přičemž může být orientována dle výkonu serveru, či jeho již stávajícího vytížení.
## Behavioural patterns
- používají se pro definování interakcí mezi objekty a třídami v systému
- patří sem
	- Iterátor – Umožňuje nám procházet prvky v různých strukturách
	- Command
	- Null Object – Nahrazuje null hodnotu
#### Iterátor
- umožňuje procházet prvky kolekce bez ohledu na způsob, jakým jsou uloženy
- poskytuje jednotné rozhraní pro přístup k prvkům kolekce, což umožňuje snadnou iteraci a práci s daty
	- může být pomalý, pokud se používá s velkými datovými strukturami
	- nelze použít na neiterovatelné dat. struktury, např.: grafy(stromy)
- můžeme jednoduše procházet prvky kolekce bez znalosti vnitřního mechanismu, který je použit pro uložení dat
#### Command
- zapouzdří žádost jako objekt
- umožňuje parametrizaci klienta s žádostí, frontování žádostí nebo ukládání žádostí do protokolu
	- podporuje i undo operace

#### Null Object
- umožňuje nahradit null hodnoty objektem
- poskytuje objekt s výchozími hodnotami, který může být použit místo null hodnoty, a to bez nutnosti vytvářet složitou logiku pro kontrolu null hodnot
- pomáhá minimalizovat problémy s chybějícími hodnotami a umožňuje snadnější testování kódu a eliminovat většinu problémů sním spojeným, jako NullPointerException a podobné
- může zvýšit nároky na paměť, protože objekty s výchozími hodnotami mohou být vytvářeny často
