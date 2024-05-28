# [Principy objektového programování, agregace a kompozice objektů](https://youtu.be/r1diROtxcpo?si=MQ7B9JLApdrCnfPj)

## O čem mluvit?
- OOP
  - dědičnost
     - pro tridy se stejnými/podobnými vlastnostmi
     - ulehčení práce
     - např.: trida zamestnanec dědí od tridy člověk 
  - zapouzdření
     - k nějakému kodu se nemůže dostat celý porgram
     - private, public, protected, internal, static
  - polymorfismus
     - muzeme tak volat metodu s různými parametry
  - agregace a kompozice
     - agregace je volna vazba
     - kompozice neni volná, objekty nemuzou fungovat bez sebe
  - interface
     - používáme když vice trid používá stejnou metodu, v danych tridach ji pak upravujeme

## Objektově orientované programování (OOP)
- jedno z programovacích paradigmat
	- = vzorec / model myšlení
- silně se odráží od teorie objektů
- snaha kopírovat svět 1:1
	- např.: dveře otevíráme stále stejně; nezáleží na tom, jestli na dveřích je kukátko, řetízek, jsou bílé nebo hnědé
- můžeme věci během psaní kódu recyklovat, použít je klidně stokrát znovu, případně je trochu upravit, aby odpovídaly našim potřebám a potřebám programu *(což vyplívá i z příkladu nahoře)*

#### Teorie objektů
- základní pojem **třída**
- podpojmem třídy je **objekt**
	- objekt je instancí třídy
	- má dva základní "smysly existence":
		- pamatovat si svůj stav pomocí atributů
		- poskytovat své metody, aby se dalo s objektem zvnějšku pracovat

#### Dědičnost
- způsob ulehčení si práce s mnoha objekty
- používáme pro objekty se stejnými vlastnostmi
- např.: místo toho že každou třídu Učitel a Student budeme psát zvlášť, vytvoříme třídu Člověk s vlastnostmi jako např. výška, věk, ..., a třídy Učitel a Student budou pouze dědit od třídy Člověk (nebudeme muset psát vlastnosti výšky, věk, ... několikrát, pouze jednou v Člověkovi)
- nepotřebujeme-li tvořit instance od obecného Člověka, můžeme třídu označit za **abstraktní**, tím se zajistí, že od ní instance vytvořit nelze

#### Metody
- voláme pomoci tzn. **tečkové konvence** => _objekt.metoda()_
- dědění metod:
	- můžeme používat zděděnou metodu
	- můžeme přepsat metodu pomocí _override_

příklad z GeeksForGeeks:
```csharp
using System;

// Base Class
class Parent
{
    public virtual void Show()
    {
        Console.WriteLine("Parent's show()");
    }
}

// Inherited class
class Child : Parent
{
    // This method overrides Show() of Parent
    public override void Show()
    {
        Console.WriteLine("Child's show()");
    }
}

// Driver class
class Program
{
    static void Main(string[] args)
    {
        // If a Parent type reference refers
        // to a Parent object, then Parent's
        // Show is called
        Parent obj1 = new Parent();
        obj1.Show();

        // If a Parent type reference refers
        // to a Child object, Child's Show()
        // is called. This is called RUN TIME
        // POLYMORPHISM.
        Parent obj2 = new Child();
        obj2.Show();
    }
}
```

  - můžeme zanechat název metody, ale změnit vstupní paramtery, _overloading_
  - příklad z GeeksForGeeks:

```csharp
using System;

public class Sum
{
    // Overloaded Sum(). This Sum takes two int parameters
    public int Sum(int x, int y) { return (x + y); }

    // Overloaded Sum(). This Sum takes three int parameters
    public int Sum(int x, int y, int z)
    {
        return (x + y + z);
    }

    // Overloaded Sum(). This Sum takes two double parameters
    public double Sum(double x, double y)
    {
        return (x + y);
    }

    // Driver code
    public static void Main(string[] args)
    {
        Sum s = new Sum();
        Console.WriteLine(s.Sum(10, 20));
        Console.WriteLine(s.Sum(10, 20, 30));
        Console.WriteLine(s.Sum(10.5, 20.5));
    }
}
```

#### Rozhraní (Interface)
- používáme když naše (dvě) třídy budou mít stejnou metodu
- do rozhraní pouze napíšeme hlavičky metod tak, jak to odpovídá syntaxi daného jazyka, a po implementování rozhraní do třídy sepíšeme konkrétní implementaci dané metody
- např.: 
	- by dvě třídy pro člověka uměly to samé, ale měly jiné vlastnosti

```csharp
// Define an interface
interface IExampleInterface
{
    // Method declaration
    void SomeMethod();

    // Property declaration
    int SomeProperty { get; set; }
}

// Implement the interface in a class
class ExampleClass : IExampleInterface
{
    // Implementing the method declared in the interface
    public void SomeMethod()
    {
        Console.WriteLine("Implementation of SomeMethod");
    }

    // Implementing the property declared in the interface
    public int SomeProperty { get; set; }
}

class Program
{
    static void Main(string[] args)
    {
        // Create an instance of the class that implements the interface
        ExampleClass example = new ExampleClass();

        // Call the method defined in the interface
        example.SomeMethod();

        // Access the property defined in the interface
        example.SomeProperty = 10;
        Console.WriteLine("Value of SomeProperty: " + example.SomeProperty);
    }
}
```

#### Polymorfismus
Umožňuje:
- jednomu objektu volat jednu metodu s různými parametry
- objektům odvozeným z různých tříd volat tutéž metodu se stejným významem v kontextu jejich třídy, často pomocí rozhraní
- přetěžování operátorů neboli provedení rozdílné operace v závislosti na typu operandů
- jedné funkci dovolit pracovat s argumenty různých typů (parametrický polymorfismus, ne ve všech programovacích jazycích)

#### Zapouzdření
- k proměnným v nějakém objektu se mohou dostat jen blíže specifikované další části programu
- cílem je, aby při vytvoření objektu, jediné co objekt ukazuje navenek, byly metody a nějaký způsob komunikace se zbytkem 
	- (getters, setters, ToString apod). 
- úrovně přístupových práv se mohou mezi programovacími jazyky lišit

V **C#** pro to používáme:
- **public** - přístup odkudkoliv v rámci projektu
- **private** - přístup pouze v rámci třídy/struktury
- **protected** - přístup pouze v rámci třídy, nebo v odvozené třídě 
- **static** - prvek nemůže mít instanci, existuje pouze jeden

## Agregace a kompozice
- agregace a kompozice jsou vztahy mezi třídami
	- agregace = sdílená (shared) agregace 
	- kompozice = složená (composite) agregace
- agregace představuje volnou vazbu mezi celkem a součástí, kdy jeden objekt (celek) využívá služby dalších objektů (součástí)
- silnější formou agregace je kompozice
- např.: 
	- vztah mezi počítačem a tiskárnou je vztah typu agregace
		- kdy počítač s tiskárnou tvoří jeden celek, ale tiskárna může existovat i tehdy, pokud není k žádnému počítači připojena. 
- agregace je formou asociace a v grafické podobě se odlišuje prázdným kosočtvercem na straně celku

![alt-text](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/14_agregace.png)

- z obrázku(nahoře) je zřejmé, že ke každému počítači může být připojen libovolný počet tiskáren a že tiskárna může být připojena k nejvýše jednomu počítači. 
- podstatné je, že odpojíme-li tiskárnu od počítače a počítač dáme do šrotu, je tiskárna stále použitelná s jiným počítačem. Silnější formou agregace je kompozice
	- jde opět o vztah mezi celkem a součástí, ale tento vztah je velmi těsný a neumožňuje samostatnou existenci součásti, aniž by byla připojena k nějakému celku. Navíc na rozdíl od agregace tato součást musí patřit jen jedinému celku a není možné ji sdílet s více celky

![alt-text](https://github.com/NeDDy3z/jecna-pv-maturita/blob/main/images/14_kompozice.png)
