# Metodiky a životní cyklus vývoje softwaru

## O čem mluvit?
- shrnout proces vývoje sw
- uvést princip metodik
	- k čemu jsou dobré
- uvést jednotlivé metodiky
	- jejich plusy a mínusy
	- kde se používají
	- popsat je a jejich rozdíly
	- možná nakreslit nějaký diagram (waterfall je easy)
- **NEZMIŇOVAT SCRUM**

## Proces vývoje softwaru
Proces plánování a řízení vývoje softwaru. Většinou obnáší rozdělení celkového vývoje do menších částí, které se zabývají specifickým problémem, paralelních nebo postupných kroků nebo dílčích procesů za účelem zlepšení návrhu a/nebo správy produktů.

Používají se různé metodiky, které nám diktují jak má proces vývoje probíhat, postupují logicky (po návrhu nemůže být hned implementace).

## Metodiky
Existuje mnoho metodik, každá organizace může používat svojí vlastní metodiku, originální pro danou organizaci, proto si uvedeme jen ty nejznámnější a často používané.

### Vodopádový model
Vodopádový model je tzv. **sekvenční lineární proces**, kde se na vývoj hledí jako na „vodopád“ *n*-fází. Rozbíjí projekt na jednotlivé fáze, kde každá další může začít až ve chvíli, kdy předchozí skončila. Navíc se nemůžeme vracet k dokončeným fázím, nebo přeskakovat mezi fázemi. V opozici vůči vodopádovému modelu stojí novodobá agilní metodika (např. Scrum, ...). Jedná se o velmi zastaralou metodiku, kterou se v praxi v dnešní době nevyplatí využívat, vyplatí se pouze v určitých případech jako např. menší projekt, kdy máme naprosto jasno jak bude probíhat vývoj. Vyžaduje aby vše probíhalo dokonale. Nevyplatí se na větší projekty. Přesto je často využíván vládam, nebo i organizací NASA.

![waterfall](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/12_waterfall.png)

**Pozor! Design v tomto případě znamená Návrh -> UML, atd..! Ne grafický design!**

U vodopádu se skutečně **přísně** postupuje podle sekvenčního způsobu. Připraví se požadavky, které jsou dané a během vývoje se **nemění**. Když jsou požadavky kompletní, přechází se do fáze návrhu. Software je naprojektován a návrh je předán implementátorům; návrh by měl sloužit jako plán pro implementaci. Programátoři zodpovědní za implementaci návrh převezmou a podle něj stvoří software. V pozdějších fázích pak dochází ke skládání a kombinaci jednotlivých stvořených částí softwaru, modifikacím, opravám a zavádění nových funkcionalit.

Vodopádový model vyžaduje, aby se k další fázi přistoupilo jedině za podmínky, že předchozí fáze je kompletní a bezchybná. Existují i upravené modely na základě vodopádu, které se mohou výrazně lišit.

**Plusy:**
- Pokud se věnuje dostatek času přípravě, může se čas ušetřit v pozdějších etapách vývoje
- Klade stejný důraz na dokumentaci jako na zdrojový kód => noví členové týmu mají možnost se lépe začlenit a uchytit
- Je jednoduchý a dobře pochopitelný, snadno se v něm hledají konkrétní cíle a milníky
- Pokud máme jasně daný cíl a víme přesně co a jak dělat, nebo pracujeme na malém projektu, kde by byly agilní metodiky overkill, je to dobrá volba metodiky

**Mínusy:**
- Problém může nastat v případě, že klient nemá stoprocentně ujasněné požadavky a vyžaduje změnu v průběhu vývoje -> muselo by se začít odznova
- Panuje všeobecné přesvědčení, že nelze dovést jednu fázi vývoje do konečného stavu před tím, než bude započata fáze další
- Je velice těžké v tomto modelu provádět změny nebo počítat s neočekávanou skutečností (změna požadavků klienta, obtížnost implementace určité funkcionality apod.); u vodopádového modelu je lepší při takové situaci rovnou utvářet nový model a spousta práce přijde vniveč


## Prototypovací model
Založeno na vytváření prototypů, neboli částečných verzí softwaru.
Základní principy jsou:
- Prototypování není samostatná, úplná, vývojová metodika, ale spíše přístup, při kterém se zkoušejí určité vlastnosti v rámci úplné metodiky (např. inkrementální, spirálový nebo rapid application development (RAD)).
- Usiluje o omezení inherentního projektového rizika rozdělením projektu na menší segmenty a usnadněním změn během procesu vývoje.
- Zákazník nebo klient je zapojen do celého procesu vývoje, což zvyšuje šanci, že přijme konečnou implementaci.
- Zatímco u některých prototypů se očekává, že přispějí k ujasnění směru vývoje, a pak budou zahozeny, v některých případech je možné z prototypu vyvíjet cílový systém.

![prototype](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/12_prototype.jpg)

#### Druhy prototypů:
**Horizontální prototyp** 
- Termín běžně poukazující na první návrh UI; slouží k náhledu na celý systém nebo subsystém a hlavním účelem je demonstrace komunikace s uživatelem spíše než funkčnost
- Hodí se pro potvrzení požadavků na UI, ukázku systému pro získání zpětné vazby a případných objednávek od potenciálních zákazníků a na předběžný odhad času, nákladů a náročnosti projektu

**Vertikální prototyp**
- úplnější propracování jednoho podsystému nebo funkce produktu
- je vhodné pro získání lepších požadavků na danou funkci: zjemnění návrhu databáze, informace o objemu dat a výkonnostních potřebách (pro určení kapacity sítě apod.), zjednodušení složitých požadavků

#### Typy prototypování:
Prototypování má více variant, všechny ale vycházejí ze dvou hlavních forem: **zahazovacího prototypování** a **evolučního prototypování**.

**Zahazovací prototypování**
- Stvoření modelu, který se ve finální fázi přímo nestane součástí projektu a bude zahozen, zatímco požadavek, který reprezentoval, se zavede jako samostatná, propracovanější implementace
- Primární účel tohoto je vyobrazit zákazníkovi, jak zhruba bude požadovaná funkce/požadovaný subsystém vypadat

**Evoluční prototypování**
- Výrazně se liší od zahazovacího 
- Jeho principem je strukturovaná tvorba robustního prototypu, který slouží jako jádro výsledného systému a poté pouze dochází k opravám a rozšířením 
- Při takovém vývoji dochází neustále k zpřesnění a zjemnění systému. „Evoluční prototypování uznává, že nerozumíme všem požadavkům a implementujeme pouze ty, které dobře chápeme.“
- V evolučním prototypování teoreticky výrobek není nikdy hotov, pouze se rozvíjí s tím, jak se mění nároky na použití
- Není neobvyklé podat uživateli nekompletní prototyp rovnou k praktickému používání, uživatelé často zjistí, že nedokončený systém je lepší než žádný


**Plusy:**
- Snížení času a nákladů: zvýší kvalitu požadavků a standardů pro vývojáře; protože při vývoji cena roste exponenciálně, včasné stanovení toho, co zákazník chce, zpravidla vede k rychlejšímu a méně nákladnému vývoji
- Zlepšené zapojení uživatele: prototypování vyžaduje větší zapojení uživatele tak, aby mohl vidět prototyp a komunikovat s ním; to přináší lepší, úplnější a užitečnější zpětnou vazbu; výsledný produkt tak spíše bude vyhovovat požadavkům zákazníka

**Mínusy:**
- Nedostatečná analýza: soustředění se na konkrétní část prototypu může odvádět pozornost od pohledu na záležitost jako celek; lze tak přehlédnout lepší možnosti řešení, nebo např. přeměny prototypu na špatný návrh výsledku, který je těžké udržovat
- Zmatení prototypu a výsledného systému: uživatel se může chybně domnívat, že prototyp, který je určen k zahození, je nevyladěná verze konečného systému
- Nepochopení potřeb uživatele ze strany vývojářů: vývojáři mohou předpokládat, že uživatel rozumí jejim cílům a sdílí je
- Lpění vývojářů na prototypu: tj. potenciální snaha převést prototyp na funkční model, přestože má například nevhodnou podkladovou architekturu
- Nadměrný čas vývoje prototypu: pokud vývojáři zapomenou na fakt, že je cílem prototypu vyvinout jej rychle, může dojít k výraznému zdržení
- Náklady na implementaci prototypingu: počáteční náklady mohou být vysoké; mnoho společností má již funkční workflow a změna na prototypování může znamenat přeškolení, změnu nástrojů apod.


## Agilní (Inkrementální) model
Je schopen se přizpůsobit uživateli. Dělíme vývoj do sprinty, nebo jinak označených období. Celý development je rozdělen na více menších částí a sprinty jsou zde pro to, abychom mohli průběh vývoje kontrolovat. Je pro nás důležité zůstávat v kontaktu s klientem a představovat mu progres, abychom věděli, že se neoddalujeme od jeho původní idey. Máme velkou možnost vývoj měnit podle představ klienta.

Inkrementální model je vhodný v kombinaci se sekvenčním (např. vodopád) a iteračním (např. prototyping) softwarovým vývojem. Zavádí zjednodušení implementace změn přímo během vývoje.

Principy inkrementálního modelu:
1. Provádí se série malých vodopádů, kde každý vodopád je určen jen pro malou část systému a je dokončen před započetím práce na dalším přírůstku
2. Obecné požadavky definujeme dříve, než přikročíme k evolučnímu vývoji pomocí malých vodopádů
3. Koncept, analýza, design architektury a systémové jádro se definují pomocí vodopádu, poté přecházíme na prototypován

![agile](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/12_agile.jpg)

**Plusy:**
- Flexibilita: Agilní model umožňuje pružnou reakci na změny požadavků zákazníka během procesu vývoje. To znamená, že i když se požadavky mění, tým může rychle adaptovat.
- Zákaznická spokojenost: Agilní přístup klade důraz na pravidelné dodávky funkčního softwaru. To umožňuje zákazníkovi průběžně vidět pokrok a zapojit se do procesu, což může vést k vyšší spokojenosti.
- Zvýšená kvalita: Díky pravidelnému testování a zpětné vazbě od zákazníka může agilní tým rychle identifikovat a opravit chyby, což vede k lepší kvalitě výsledného produktu.
- Zvýšená motivace týmu: Práce v krátkých iteracích s jasnými cíli a pravidelnou zpětnou vazbou může zvýšit motivaci členů týmu a posílit jejich zapojení do projektu.

**Mínusy:**
- Nároky na aktivní účast zákazníka: Agilní model vyžaduje aktivní účast zákazníka, což může být obtížné, pokud zákazník není k dispozici nebo nemá čas se pravidelně angažovat.
- Náročnost plánování: Plánování krátkých iterací a prioritizace požadavků může být náročné, zejména v případech, kdy jsou požadavky komplexní nebo nejasné.
- Možnost přehlédnutí dlouhodobých cílů: Fokus na krátkodobé cíle a rychlé dodání může vést k tomu, že tým přehlédne dlouhodobé strategické cíle nebo nedostatky v architektuře.
- Náročnost managementu: Agilní model vyžaduje zkušeného a schopného vedení, které dokáže efektivně koordinovat tým, zvládat změny a udržovat jasnou vizi projektu.


## Spirálový model
Proces vývoje, který kombinuje designový a prototypový přístup tak, aby postupoval v kombinování výhod od shora dolů (prototypování) a zdola nahoru (designování).

Základní čtyři kvadranty modelu (iterace = jedno projití spirálou):
1. Analýza - stanovení cílů, alternativ a velikosti iterace
2. Vyhodnocení - probrání alternativ, identifikace a řešení rizik
3. Vývoj - vývoj a kontrola produktu, součástí vývoje je i testování
4. Plánování - plán pro příští iterace

![spiral](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/12_spiral.jpg)


## Extrémní programování
- Všechni části jsou řešené až extrémně do detajlu
- Mezi tyto metodyky spadá například programování ve dvou
    - Kde jeden programuje a druhý ho kontroluje a snaží se oběvit chyby které by později mohli být problémové či poradit jakým způsobem danou problematiku řešit
    - Mohou se vyměnit, víc očí víc vidí, víc hlav víc ví
- Důležitá je komunikace, jednoduchost, zpětná vazba, odvaha
- Programujeme vždy to co je potřeba
- Jedná se o iterativní model ale "sprinty" jsou mnohem kratší
- Snažíme se dělat vše co nejrychleji a do posledního detailu
- To co je pro nás důležité tomu se budeme stále věnovat to, co se pro nás osvědčilo tomu věnujeme nejvíce času


## Další postupy:
- Rapid Application Development (RAD)
- Objektově orientované metodické přístupy
- Metodou shora-dolů (dekompozice)
- Unified Process (založeno na UML)
