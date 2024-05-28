# Strojové učení s využitím regrese a klasifikace

## O čem mluvit?
- Regrese
	- dám stroji data a chci po něm na výstupu číslo
	- snažím se vytvořit matematickou funkci která ke každé hodnotě něco vrátí, (cena domu, ...)
	- ukázat její gráfek
- Klasifikace
	- po dání stroji dat po něm chci přesná data
	- např.: co je na obrázku za zvíře, jakou má střecha barvu, ...

## Regrese
- typ řízeného učení, kde je cílem předpovídat výstupní hodnotu na základě vstupních dat
- obecně je cílem regrese sestavit model, který dokáže přesně předpovědět výstup na základě vstupních hodnot a porozumět základnímu vztahu mezi nimi
	- např.: cena nemovitostí, OCR pro čísla [Video na pochopení neuronů](https://youtu.be/aircAruvnKk?si=C9XAgIpqNWmIsXJ3)

![regrese](../images/18_regrese.png)

- snažíme se proložit přímku mezi všemi body tak abychom dospěly k nejmenší odchylce mezi všemi body
- opíráme se o square error tedy chybu na druhou z kterých následně uděláme průměr a zjistíme tak chybovost modelu
- vstupní data by měla být pouze číselné hodnoty

Výsledek lineární regrese je reálné číslo (hodnota odpovídající hodnotě na výsledné přímce) oboje z sklearn.metrics

![druhy regrese](../images/18_druhy_regrese.png)

[Příklady v Google Colab](https://colab.research.google.com/drive/1mOroDym6F0vWQYk_qWma0j5KsgOQHJas?usp=sharing)


## Klasifikace
- strojové učení kde se snažíme výstupní data zařadit do předem stanovaných skupin / tříd / klasifikací
	- snažíme se nalézt matematický vztah mezi vstupními hodnotami a výstupem
- supervised-learning = model je trénován na označeném datovém souboru, který obsahuje příklady vstupních dat a odpovídajících označení tříd
	- datové typy ve vstupních datech můžou být různé - text, číslo, logická hodnota, ...
- cílem je naučit model aby zvádl zařadit neznámá/nová data do stanovených skupin správně
- např.:
	- rozpoznání spamu, co je na obrázku (kočička/pes/...), diagnostika chorob

![klasifikace](../images/18_klasifikace.png)
*(Pokud si dobře pamatuju tak Mandík chce aby jsme znali ty vzorečky)*

Snažím se do grafu vložit přímku tak abych rozdělil co nejlépe dvě množiny prvků, následně pomocí funkce zjistit, do jaké kategorie hledaný prvek patří, jestli do kategorie na jedné straně od přímky nebo na druhé straně.

Výsledek klasifikace je nějaká bude accuracy_score(y_test, y_pred) … (např.: 0.8, 0.9, 1.1) nebo classification_report(y_test, y_pred) … oboje from sklearn.metrics

[Příklady v Google Colab](https://colab.research.google.com/drive/1J2j72dMF1q0Errgu2RkuMCOZUYoSiIBd?usp=sharing)

