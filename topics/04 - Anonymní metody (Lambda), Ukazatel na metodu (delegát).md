# [Anonymní metody (Lambda), Ukazatel na metodu (delegát)](https://youtu.be/tNwfoEaFF68?si=YaftN8RaOIRkU47k)
*Upřímně, tenhle dokument stojí za prd a potřebuje těžkou revizi*

## O čem mluvit?
- Anonymní metoda (Lambda)
    - anonymni metoda 
    - syntax
    - pouzivana treba na hledani v poli
- Ukazatel na metodu (Delegát)
    - ukazatel na metodu
    - typy delegátu v C# - (Func, Action, Predicate)
    - využití -> Callback, Event

## Anonymní metody
- blok kódu, který je nadefinován beze jména
- může být použit jako proměnná
```csharp
var calc = delegate (int a, int b) {
    return a + b;
};

Action line = () => Console.WriteLine();

Func<int, int, bool> testForEquality = (x, y) => x == y;

var IncrementBy = (int source, int increment = 1) => source + increment;

Console.WriteLine(IncrementBy(5)); // 6

Console.WriteLine(IncrementBy(5, 2)); // 7 testForEquality = (x, y) => x == y;
```

## Lambda
- zkrácený zápis anonymní metody
- kus kódu, který na vstup dostane proměnnou a další vrátí
	- nemusí při tom volat metodu, oni sami jsou jim podobné
- nemají jméno
- můžou být použity jako proměnná
- Lambdy mají určitá pravidla -> Nemohou uvnitř obsahovat proměnné čí cykly. Mohou být psány více způsoby.
- Lambda je v c# řešena pomocí knihovny Linq

#### Proč lambdu použít?
- můžu funkce posílat jiné funkci jako proměnnou
- pomáhají filtrovat a získávat data z kolekcí bez zbytečně dlouhého kódu 
- jsou převážně krátké a jednoduché na pochopení
- můžeme díky nim splnit určitý interface

#### Lambda výraz se dělí na dva typy
1. Expression Lambda
	- tvořena inputem a výrazem
	- C#:
	  ```csharp
		List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

        // Použití lambda výrazu s metodou Where
        var evenNumbers = numbers.Where(n => n % 2 == 0).ToList();

        foreach (var number in evenNumbers)
        {
            Console.WriteLine(number);  // Output: 2 4
        }
		```
	- Python:
	  ```python
	  # Lambda metoda
	  add = lambda x, y : x + y
	  add(1,2) # -> 3
	  
	  # Výběr čísel > 2 z listu
	  mujlist = [1,2,3,4,5,]
	  filtered = list(filter(lambda x : x > 2, mujlist)) # -> [3,4,5]
	  ```
1. Statement Lambda
	- tvořena inputem a více příkazy které budou vykonány
	- C#
	  ```csharp
	  //Příklad:
	  Action<string> greet = name => {
		  string greeting = $"Hello {name}!";
		  Console.WriteLine(greeting);
	  };
	  
	  greet("Šnoulo"); // Prints "Hello Šmoulo
	  
	  // Syntaxe:
	  input => { statements };
	  ```
	- Python:
	  ```python
	  # Python
	  greet = lambda name: print(f"Hello {name}!")
	  greet("Ňoumo") # -> "Hello Ňoumo!"
	  ```
#### Volání funkce
```csharp
greet("Šmoulo")  # Vytiskne "Hello Šmoulo!"
```

- další příklad: lambda metody pro sečtení dvou čísel
```csharp
int sum(int a, int b) => (a+b);
```

## Delegát
- deklaruju si vlastní typ anonymních funkcí
- proměnná která odkazuje na nějakou metodu
	- technicky je to referenční datový typ
- pro vytvoření se používá **delegate** 
	- při deklaraci mu určujeme jaké metody do něj můžeme ukládat a jaké bude mít vstupní a výstupní hodnoty

C#:
```csharp
 class Program {
    public delegate int Calculation(int a, int b);
    
    public static void Main(string[] args) {
        Calculation calc = ((a, b) => a + b);
        
        Console.WriteLine(calc(3, 5));
        
        calc = ((a, b) => a * b);
        
        Console.WriteLine(calc(3, 5));
    }
}
```

#### Využití delgátů
- callback funkce
- eventy
- např. Callback
C#:
```csharp
class Program {
	public delegate int Calculation(int a, int b);
    
    public static void Main(string[] args) {
        Program.TestCallback((a,b) => a*b);
        Program.TestCallback(Program.Add);
    }
    
    public static int Add(int a, int b) {
        return a+b; 
    }
    
    public static void TestCallback(Calculation callback) {
        Console.WriteLine("Po tomto nastane callback");
        callback(5, 6);
    }
}
```

#### Generické delgáty
- V C# máme předdefinované delegáty, takže většinu času není třeba definovat vlastní
![mandik](../images/Skyrim_Mandiky_2%20(1).png)
#### Func
- nemusí mít žádný vstup (0-16)
- 1 výstup
```csharp
Func<int, int, int> calc;

calc = ((a, b) => a + b);
Console.WriteLine(calc(3, 5));

calc = ((a, b) => a * b);
Console.WriteLine(calc(3, 5));
```

#### Predicate
- bere jeden vstupní parametr
- vrací true / false
```csharp
Predicate<string> isUpper = s => s.Equals(s.ToUpper());

bool result = isUpper("hello world!!");
```

#### Action
- nemá výstup, tzv. delegát co vrací void
```csharp
// Action s jedním vstupním parametrem
Action<string> print = message => Console.WriteLine(message);
print("Hello, world!"); // Vytiskne "Hello, world!"
```
