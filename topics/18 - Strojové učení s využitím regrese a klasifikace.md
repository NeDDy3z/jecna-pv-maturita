# Strojové učení s využitím regrese a klasifikace

## O čem mluvit?
- popsat regresy
	- jak funguje
	- co je jejím grafem
	- vstupy, výstupy
- popsat klasifikaci
	- jak funguje
	- jak rozděluje data
	- vstupy, výstupy

## Regrese
Typ řízeného učení, kde je cílem předpovídat závislou proměnnou na základě jedné nebo více vstupních funkcí (také nazývaných prediktory nebo nezávislé proměnné).

Obecně je cílem regrese sestavit model, který dokáže přesně předpovědět výstup na základě vstupních funkcí a porozumět základnímu vztahu mezi vstupními vlastnostmi a výstupem.

![regrese](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/18_regrese.png)

Snažíme se proložit přímku mezi všemi body tak abychom dospěly k nejmenší odchylce mezi všemi body. Opíráme se o square error tedy chybu na druhou z kterých následně uděláme průměr a zjistíme tak chybovost modelu

Vstupní data by měla být pouze číselné hodnoty.

Výsledek lineární regrese je reálné číslo (hodnota odpovídající hodnotě na výsledné přímce) oboje z sklearn.metrics

![druhy regrese](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/18_druhy_regrese.png)

![Příklady v Google Colab](https://colab.research.google.com/drive/1mOroDym6F0vWQYk_qWma0j5KsgOQHJas?usp=sharing)


## Klasifikace
Technika strojového učení, která zahrnuje trénování modelu pro přiřazení štítku třídy danému vstupu. Jedná se o řízenou učební úlohu, což znamená, že model je trénován na označeném datovém souboru, který obsahuje příklady vstupních dat a odpovídajících označení tříd.

![klasifikace](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/18_klasifikace.png)

*(Pokud si dobře pamatuju tak Mandík chce aby jsme znali ty vzorečky)*

Cílem modelu je naučit se vztah mezi vstupními daty a štítky tříd, aby bylo možné předpovědět štítek třídy pro nový, neviditelný vstup.

Datové typy ve vstupních datech můžou být různé - text, číslo, logická hodnota, ...

Snažím se do grafu vložit přímku tak abych rozdělil co nejlépe dvě množiny prvků, následně funkce zjisti, do jaké kategorie hledaný prvek patří, jestli do kategorie na jedné straně od přímky nebo na druhé straně.

Výsledek klasifikace je nějaká budě accuracy_score(y_test, y_pred) … (např.: 0.8, 0.9, 1.1) nebo classification_report(y_test, y_pred) … oboje from sklearn.metrics

![Příklady v Google Colab](https://colab.research.google.com/drive/1J2j72dMF1q0Errgu2RkuMCOZUYoSiIBd?usp=sharing)

