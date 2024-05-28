# [Asymptotické paměťové a časové složitosti](https://youtu.be/zojej6FYgYQ?si=Gn2t4RPM3-uLhTYD)

## O čem mluvit?
- určujeme jak dlouho času a kolik pameti zabere vykonat nějaký úkon 
- Způsoby klasifikace 
	- Big O, Theta, Omega
- Která složitost je přijatelná a co už je moc? (konstantní, logaritmická, linární...)
- Časová / Paměťová
    - příklady u různých algoritmů 
	    - výhody, nevýhody
	    - vzájemná kompenzace
	    - analýza požadavků na konkrétní problém
- Jak analyzovat složitost?

## Asymptotická složitost programu
- způsob klasifikace určitého algoritmu
	- algoritmus je přesně daný postup, jak vyřešit určitý problém
- způsob, kterým se dá určit kolik prostředků bude potřeba k dosažení cíle
	- asymptotická, protože se zabývá výkonností u programu, který může pracovat s neomezeným počtem dat
- v základu se rozděluje na **časovou** a **paměťovou**
- je důležité zmínit, že jiné zařízení mají jiné parametry
	- tím pádem se výsledek bude lišit na různých zařízeních 
	- tyto složitosti rozlišují tím, jak doba vykonání roste se změnou množství dat

#### Klasifikace
- **Big O** [big O]
	- nejpoužívanější
	- určuje nejhorší možný případ složitosti (horní mez)
	- ![BigO](../images/06_bigo.png)
- **Big Ω** [big omega]
	- určuje nejlepší možný případ složitosti (dolní mez)
	- ![BigO](../images/06_bigomega.png)
- **Big Θ** [big théta]
	- určuje složitost ve vymezených hranicích
	- tzn. že reálná se bude lišit od perfektní složitosti maximálně ve vymezených limitách (průměr)
	- ![BigO](../images/06_bigtheta.png)

## Asymptotická časová složitost
- Time Complexity
- určuje dobu, kterou procesor vyžaduje k vykonání úlohy
	- (počítá se s tím, že máme neomezenou paměť)

#### Typy
- **Konstantní – Θ (1)**
	- konstantní složitost nám říká, že na počtu dat nezáleží
	- algoritmus bude trvat stále stejně ř
	- říká se mu také dokonalý / perfektní algoritmus n
		- ale ne pokud bude trvat i tak pět let...
	- např.: skok na index v poli 
		- je jedno, kolik bude prvků, první bude vždy 1., osmý vždy 8.
		- ```python
		  pole = [1,2,3,4]  
		  print(pole[2])
- **Logaritmická - Θ (Log n)**
	- rozděl a panuj 
		- (nedělí tak dlouho dokud nezůstanou jen dvojice na rozdíl od Linearitmetické)
	- algoritmus si rozdělí prvky jak potřebuje
	- např.: 
		- hledání jména v telefoním seznamu 
			- nemusíme kontrolovat každé jméno, když víme, že příjmení začíná na určité písmeno 
			- rozdělíme seznam na polovinu a zjistíme, v jaké polovině leží toto jméno
- **Odmocninová - Θ (√n)**
	- prohledávání prvků v **k**-dimenzionálním stromu
- **Lineární – Θ (n)**
	- složitost, kde pro 10 prvků se provádí 10 operací, pro 100 prvků 100 operací, atd...
	- např.: 
		- vypsání všech prvků v pol, tolikrát, kolik je prvků
			- pokud se 100.000 prvků se vypíše za sekundu, 1MIL prvků se vypíše za deset sekund
		- ```python
		  pole = [1,2,3,4]
		  for p in pole:  
			  print(p)
- **Linearitmická Θ (n * log n)**
	- rozděl a panuj
		- vezme nesetříděné pole a dělí je na poloviny tak dlouho, dokud nejsou pouze dvojice
		- následně dvojici seřadí a poté všechny dvojice spolu s další dvojicí spojuje, tak dlouho dokud nemá celé pole
	- např.: 
		- [Merge sort](02%20-%20Algoritmizace%20-%20Grafy,%20Prohlédávání%20stavového%20prostoru,%20Řazení####%20Merge%20sort) a [Quick sort](02%20-%20Algoritmizace%20-%20Grafy,%20Prohlédávání%20stavového%20prostoru,%20Řazení####%20Quick%20sort)
- **Kvadratická – Θ (n²)**
	- složitost je kvadratická – *("v sortingu"):* pro sedm prvků, sedmkrát proběhne sedm míst
		- projíždí i ty prvky, u kterých si je jistý, že jsou seřazené na konci správně
	- např.: 
		- [Bubble sort](02%20-%20Algoritmizace%20-%20Grafy,%20Prohlédávání%20stavového%20prostoru,%20Řazení####%20Bubble%20sort) a [Insertion sort](02%20-%20Algoritmizace%20-%20Grafy,%20Prohlédávání%20stavového%20prostoru,%20Řazení####%20Insertion%20sort)
		- dva for-cykly v sobě
		- ```python
		  pole = [1,2,3,4]
		  for p in pole:  
			  for pp in range(len(pole)):  
				  print(pp)
- **Faktoriálová – Θ (n!)**
	- řešení čehokoliv pomocí hrubé síly - [Brute force](03%20-%20Algoritmizace%20-%20Rekurze,%20Brute%20Force,%20Heuristiky,%20Nedeterministické%20algoritmy##%20Brute%20force)
	- na grafech udávána vždy jako nejhorší možnost
		- (i když existují ještě horší) 
	- např.: 
		- řešení problému obchodního cestujícího
			- postupně projdeme absolutně všechny kombinace cest, které existují, a poté vybereme tu nejsnazší

## Asymptotická paměťová složitost
- Space / Memory Complexity
- určuje kolik operační paměti bude využito
- častá chyba je, že si někdo může říct, že paměťovou složitost nelze rozlišit, protože na různých zařízeních bude využívat stejné množství paměti, což sice je pravda, ale stále ji můžeme rozlišit. 
- A rozlišit jí můžeme naprosto stejně jako u časové, akorát se změní otázka na **jak** **paměť vykonání roste se změnou množství dat.**

#### Typy
- **Konstantní – Θ (1)**
	- s pamětí se nic neděje, využíváme stále to stejné množství/obsah
	- např.: 
		- for-cyklus, kde tiskneme „i“ 
			- v tomto případě se totiž s pamětí neděje nic jiného než že jsme jednou vytvořili proměnnou i a neustále jí jen přepisujeme (upravujeme její obsah) a tiskneme 
				- = paměťová složitost je konstantní
		- ```python
		  pole = [1,2,3,4]   
		  for p in pole:  
			  print(p)
- **Lineární – Θ (n)**
	- např.: 
		- rekurzivní řešení faktoriálu 
			- pokud máme například faktoriál 6, je to 6x5x4x3x2x1 – Tudíž pro faktoriál šesti potřebujeme šestkrát uchovat největší hodnotu
		- ArrayList
			- jak arraylist roste, roste i jeho potřeba pro paměť
		- ```python
		  pole = [1,2,3,4]   
		  pole.append(5)
- **Kvadratická - Θ (n2)**
	- např.: 
		- 2D Array
		- násobení matic
