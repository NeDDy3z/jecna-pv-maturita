# Strojové učení - Příprava dat, Chyby v datech a bias, Korelace a kauzalita

## O čem mluvit?

- AI
  - typy: úzká (řeší konkretni problém), silná (neexistuje, dokaze vše)
  - využití, problémy, ...
- Strojové učení
   - supervised - pro vstupni data je spravny výstup 
   - unsupervised - ke vstupu neni výstup
   - semi-supervised - mix obojiho nahoře
   - reinforcement - dostava odměny/trest, ai ve hrách, autopilot dronu?
- jak se připravují data (dělali jsme to na hodinách)
  - chyby v datech a čištění
  - zbavujeme se null, výchylek, zbytecnych atributů 
  - omezujeme na nějaký rozptyl
- bias
   - ovlivnění výsledků 
  - kdyz dame modelu data o drahych autech nebude mít data k tim levným 
- korelace a kauzalita
   - korelace je když např. žáci maji dobré vysledky a hodne spánku ale neni to zaroven kauzalitou (ma to by byl treba vetsi výzkum)
   - kauzalita je když např.: pití za volantem způsobuje vice nehod
   - pro kauzalitu je potrebna korelace

**Jelikož je toto velmi obsáhlé a složité téma, doporučuji podívat se zpětně na úlohy co jsme dělali ve škole (Google Colab) a přečíst si 8 ![prezentací](https://github.com/NeDDy3z/jecna-pv-maturita/tree/main/ai_presentations) o AI, jsou krátké a na jejich koncích bývají otázky o kterých můžete taky mluvit u maturity.**

## Umělá inteligence

Inteligence projevená stroji, jde o adaptaci v novém prostředí, vykonávání úkolů, které by normálně vyžadovali lidskou inteligenci.

Dělíme na dva typy:

**Úzká AI (slabá):**

- vždy řeší jeden konkrétní problém, neumí se adaptovat na nové problémy
- všechna existující AI jsou slabou umělou inteligencí

**Obecná AI (silná):**

- umí cokoliv, co dokáže člověk, nebo dokonce více
- zatím neexistuje

![AI](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/17_ui.png)

## Strojové učení

Strojové učení je jedním z nástrojů umělé inteligence. V současnosti nejrozšířenější metoda umělé inteligence s největšími dopady. Strojové učení je podmnožinou umělé inteligence. Zabývá se zjišťováním funkce _f_, která pro nový vstup určí odpovídající výstup.

![f](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/17_strojove_uceni.png)

Zkráceně - nalezne vzor z dat, namísto toho aby mu byl přímo tento vzor poskytnut.
Tento vzor - funkce - se pak dále zlepšuje pro co největší přesnost výstupu.
Příklady dvojic vstupů a výstupů nazýváme _trénovací data_.

Pomocí strojového učení se řeší problémy jako předpověď počasí, ceny, rozpoznání obrázků apod.

### Typy učení:

- **Učení s učitelem** („supervised learning“) - pro vstupní data je určen správný výstup (třída pro klasifikaci nebo hodnota pro regresi).
- **Učení bez učitele** („unsupervised learning“) - ke vstupním datům není známý výstup.
- **Kombinace učení s učitelem a bez učitele** („semi-supervised learning“) - část vstupních dat je se známým výstupem, ale další data, typicky větší, jsou bez něj.
- **Zpětnovazebné učení** („reinforcement learning“), též učení posilováním, funguje na principu agenta, který interaguje s prostředím a za své akce dostává odměnu či trest. Agent se snaží maximalizovat odměnu. … umělá inteligence ve hrách samořiditelné drony apod.

### Základní druhy úloh:

- **Klasifikace** rozděluje data do dvou nebo několika tříd (učení s učitelem)
- **Regrese** odhaduje číselné hodnoty výstupu podle vstupu (učení s učitelem)
- **Shlukování** zařazuje objekty do skupin s podobnými vlastnostmi (učení bez učitele) … využití například na sociálních sítí

## Příprava dat

Než s daty budeme nějak pracovat, je dobré je vyčistit (sanitizace dat), aby jsme dostali co nejpřesnější výsledky, tato sanitizace obsahuje:

- Co nejvíc zmenšit rozsah dat, např. mít hodnoty jen od 0 do 1, nepracovat s miliony ale jen s desitkami, atd.
- Zlikvidovat všechny prázdné nebo neúplné záznamy, např. záznam obsahuje hodnotu _null_
- Snažíme se se zbavit extrémních výjimek. Snažíme se co nejvíce zúžit rozptyl dat
- Všechny parametry převést do nějakého standardizovaného stavu
- Zbavit se irelevantních atributů
- Atributy v data setu by měli být vyjádřeny pouze čísly

Toto čištění se dá dělat ručně, ale při velkém množství vstupních dat je efektivnější data prohledat pomocí kódu, v Pythonu knihovny pandas a NumPy

### Bias

Jedná se o to, že máme nějaký extrém a funkce se podle něho řídí, ale už se odchyluje od reality. Tím pádem máme dobrý model pro testovací data, ale v realitě model nebude zas tak dobrý.

Př: Prodáváme spíše dražší auta takže jsou ceny zaujaté aby byly vyšší protože v modelu není dostatek levnějších aut, které by výslednou predikci vraceli do normálu a chybu (Bias) zmenšovali. Výsledkem je vyšší odhadovaná cena u levnějších aut.

### Korelace a kauzalita

Korelace neimplikuje kauzalitu. Ale pro kauzalitu je nutná korelace.

Korelace vztah mezi veličinami a procesy. Ve chvíli, kdy dojde ke změně v jedné věci dojde k změně v druhé věci. Jedna vílčina nezbytně neovlivňuje veličinu druhou.

V kauzalitě jedna veličina přímo ovlivňuje tu druhou. Protože se změnila jedna věc změní se i druhá.
