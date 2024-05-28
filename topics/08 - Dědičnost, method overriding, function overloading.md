# [Dědičnost, method overriding, function overloading](https://youtu.be/x6Ka2BdxwT8?list=PLmW7bUCTvOeTSag9ZZBYXdHs_iEwB4OHM)

## O čem mluvit?
- Dědičnost
        - základ OOP
	- dědime od tříd s kterymi maji child tridy společně funkce / vlastnosti
	- můžeme tomu zabranit pomocí sealed
- Method overriding
        - overriduju často tostring
        - prepisujeme metody s rodičovské třídy 
- Function overloading
	- děláme více funkcí se stejným jménem (dáme jí pak víc vstupů třeba)
	- např více konstruktorů 

## Dědičnost (Inheritance)
- spolu se zapouzdřením a polymorfismem je jednou ze tří primárních charakteristik OOP 
- dědičnost umožňuje vytvářet nové třídy, které znovu používají, rozšiřují a upravují chování definované v jiných třídách

Dělíme na:
- **Parent class** (rodičovská třída) - Třída, od které ostatní třídy dědí
- **Child class** (potomek) - Třída, která dědí od rodičovské třídy
	- může dědit pouze od jedné **Parent class**(toto platí v jazyce Java i C#, některé jazyky ale vícenásobnou dědičnost povolují, např. C++).

Třídy (a metody) můžeme nastavit jako již dále **neděditelnou**
- **Java** - klíčové slovo **final** 
	- ```java 
	  public final class Person{ }
- **C#** - klíčové slovo **sealed** 
	- ```csharp
	  public sealed class Person{ }

Proměnné a metody můžeme nastavit jako **protected**
- tím zamezíme přístup jiným třídám, ale bude možné nadále dědit
- **C#** - třída dědí pomocí znaku “**:**” (stejně jako při implementaci rozhraní),
- **Java** - používá slovo **extends**

#### Příklady dědičnosti
Python:
```python
class Animal:
    name = ""
    
    def eat(self):
        print("I can eat")

class Dog(Animal):
    def display(self):
        print("My name is ", self.name)

labrador = Dog()
labrador.name = "I <3 MayGen"
labrador.eat()
labrador.display()
```

C#
```csharp
class Person {
    
    private string firstName
    protected string FirstName {
		get {return firstName;}
		set {name = value;}
    }

    protected string LastName { get; set; }
    protected byte Age { get; set; }
    protected string FullName => $"{FirstName} {LastName}";
    
    protected Person(string firstName, string lastName, byte age) {
        FirstName = firstName;
        LastName = lastName;
        Age = age;
    }

    protected string Introduce() => $"Hi, I'm {FullName}.";
} 

// Employee.cs
class Employee : Person {                                             

    public string JobTitle { get; set; }
    public decimal Salary { get; set; }

    public Employee(string firstName, string lastName, 
		    byte age, string jobTitle, decimal salary): 
	    base(firstName, lastName, age)
{
```

Třída **Animal** je v těchto případech *rodičovskou třídou*, má atribut **name** a funkci **eat()**. Třída Dog dědí od třídy Animal, je tedy *potomkem* rodičovské třídy Animal. Potomek Dog má jak zděděné vlastnosti od rodiče, tak má vlastní funkci **display()**.

## Method overriding (Překrytí)
- mnoho OOP jazyků dovoluje objektu nebo třídě nahrazení funkce, která byla zděděná
	- tento proces je nazýván překrytí. 
- toto přináší komplikaci: 
	- kterou verzi funkce instance zděděné třídy používá – tu co je součástí vlastní třídy, nebo tu co je z rodičovské třídy? 
	- odpověď se liší jazyk od jazyka, nějaké jazyky obsahují deklarace pro určení, že určité metody nemohou být překryty, některé obsahují deklarační slova pro označení překrytých metod.
- nejběžnější příklad překrytí je ToString.

Python:
```python
class Animal:
    def eat(self):
        print("I can eat")

class Dog(Animal):
    def eat(self):
        print("I eat bones")

class Cat(Animal):
    def eat(self):
        print("I eat fish")

dog = Dog()
dog.eat() -> "I eat bones"
cat = Cat()
cat.eat() -> "I eat fish"
animal = Animal()
animal.eat() -> "I can eat"
```
- Potomci třídy Animal, Dog a Cat, překrývají metodu **eat()**, aby vracela originální výstup pro každou třídu. V Javě se před překrytím metody používá anotace *@Override*.

C#
```csharp
class Karel {
	private string jmeno;

	public Karel() {
		jmeno = "Prdel"
	}
	public override ToString() {
		return "Karel není"+ jmeno;
	}
}
```

## Method overloading (Přetěžování)
- zápis více funkcí se stejným názvem
	- ale s odlišným množstvím/typem vstupních parametrů nebo různými implementacemi
- každá taková funkce se může chovat odlišně 
- všechny overloaded metody jsou vyhodnoceny ve chvíli kdy se aplikace kompiluje
- některé jazyky nepodporují přetěžování.

Python:
```python
class Calculator:
	def add(self, a, b):
		return a+b
	
	def add(self, a, b, c):
		return a+b+c
	
	def add(self, *args):
		return sum(args)
```

C#:
```csharp
class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }

    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }

    public double Add(double a, double b)
    {
        return a + b;
    }
}
```

## Polymorfismus
- označení pro stav, kdy v množině existuje pro určitý úkaz minimálně 2 varianty
- často označován jako třetí pilíř OOP po zapouzdření a dědičnosti

Polymorfismus je řecké slovo, které znamená "mnoho-formoval" a má dva odlišné aspekty:
- za běhu objekty odvozené třídy mohou být považovány za objekty základní třídy v místech, jako jsou parametry metody a kolekce nebo pole. Dojde-li k tomuto polymorfismu, deklarovaný typ objektu již není shodný s typem za běhu.
- základní třídy mohou definovat a implementovat virtuální _metody a_ odvozené třídy je mohou přepsat, což znamená, že poskytují vlastní definici a implementaci. Za běhu, když kód klienta volá metodu, CLR vyhledá typ běhu objektu a vyvolá toto přepsání virtuální metody. Ve zdrojovém kódu můžete volat metodu na základní třídy a způsobit odvozené třídy verze metody, které mají být provedeny.

#### Příklad
- Představme si, že máte v ruce mobilní telefon. Za předpokladu, že chcete komunikovat, mobilní telefon je toho schopen mnoha způsoby. Může volat, může psát zprávu, poslat obrázek, mail a tak dále. Účel všech těchto akcí ale zůstává stejný, komunikace. To samé by platilo pro vozidlo s hybridním pohonem, jenž by bylo schopné jet jak na fosilní paliva, tak čistě elektrický pohon. V obou případech jde o akci pohybu, leč jiným způsobem.
- Trošku jiným příkladem je entita vozidlo. Ta může mít 2, 3, 4, 6 a více kol, avšak stále zůstává vozidlem a jeho účelem je pohyb.
