# Strojové učení s využitím umělých neuronových sítí

## O čem mluvit?

- popsat neuronovou síť
- vysvětlit od čeho se odvozuje název
- jak a podle čeho funguje
- jak vypadá nejlehčí neur. síť

## Neuronová síť

Jeden z výpočetních modelů, použitých v oblasti UI. Vzorem je chování neuronů v mozku, od toho je odvozen i název.

Umělá neuronová síť je struktura určená pro distribuované paralelní zpracování dat. Skládá se z umělých neuronů, jejichž volným předobrazem je biologický neuron. Neurony jsou vzájemně propojeny synaptickými vazbami a navzájem si předávají signály a transformují je pomocí aktivačních přenosových funkcí.

Neuron má libovolný počet vstupů, ale pouze jeden výstup.

![neuronova sit](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/19_neuronova_sit.png)

Základní stavební kámen je neuron. Každý neuron představuje nějakou funkci, která částečně pokrývá testovací data. Funkce v neuronech se navzájem překrývají a pokud jsou správně rozmístěny mohou pokrýt testovací data dohromady.

Neuronové sítě mají mnoho využití, např.:

- Rozpoznávání obrázků, řeči
- Predikce časových řad
- Analýza psaného textu
- Filtrování spamu
- ...

Využívá se hlavně u problémů co nedokáže vyřešit lineární regrese, a používá se pouze zřídka, kvůli vysokému nároku na výpočetní sílu.

Cílem učení neuronové sítě je nastavit síť tak, aby dávala co nejpřesnější výsledky. V biologických sítích jsou zkušenosti uloženy v synapsích. V umělých neuronových sítích jsou zkušenosti uloženy v jejich matematickém ekvivalentu – váhách. Učení neuronové sítě rozlišujeme na **učení s učitelem (supervised learning)** a **učení bez učitele (unsupervised learning)** . Fáze učení neuronové sítě bývá nazývána adaptivní, fáze vybavování po naučení neuronové sítě bývá nazývána aktivní.

### Perceptron

Nejjednodušší neuronová síť, skládající se pouze z jednoho neuronu.

![perceptron](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/19_perceptron.jpg)

Má _n_ vstupů, jeden výstup. Nejdřív se násobí vstupy s vahamy, tyto výsledky se sečtou, součet se pak "prožene" aktivační nelineární funkcí, často sigmoida.

Možné aktivační funkce:

![aktivační funkce](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/19_aktivacni_funkce.png)

### Algoritmus zpětné propagace chyby

Abychom mohli spočítat úpravu vah u jednotlivých neuron nejprve musíme provést krok vpřed za pomocí nějakých sample (testovacích) dat provedeme s vahami které na začátku byly přiřazeny náhodně. Dostaneme výstupní hodnotu. Výstupní hodnotu porovnáme s výslednou hodnotou z sample (testovacích) dat a spočítáme jak bychom měli opravit váhy aby jsme tu vypočtenou chybu zmenšili. Nejprve upravujeme váhy v první vrstvě (layer) od výstupního neuronu tím zas vynikne nová chyba kterou budeme upravovat v následující vrstvě (layer) a postupně se vracíme zpátky až do vrstvy u vstupních neuronů.

Tedy propagujeme chybu, která nám vznikla na výstupu na vstup.  
Deep learning se říká neuronové síti s velkém množství neuronů a vrstev s nimi. Využívá velký výpočetní výkon. Používá se jiné aktivační funkce či algoritmy

[Příklady na Google Colab](https://colab.research.google.com/drive/1XDJuMFQyvx5vTVE5E4BQCZwLbVs1YJGa?usp=sharing#scrollTo=LCNMnvvGvpM3)

[Video na pochopení neuronů](https://www.youtube.com/watch?v=0Hqz8u2TEcg)
