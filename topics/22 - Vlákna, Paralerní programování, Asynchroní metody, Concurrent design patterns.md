# [Vlákna, Paralerní programování, Asynchroní metody, Concurrent design patterns](https://youtu.be/25J3XXahF3w?si=vcp1f1FF7fwRsbe_)
## O čem mluvit?
- vysvětlit, co to je
- jak fungují vlákna
- k čemu se konkurence používá
- napsat jednoduchý kód který se spouští paralelně
- vysvětlit problém s konkurencí a jak se mu dá předejít
- vysvětlit asynchronní metody, v jakých jazycích se často používají
- popsat konkurentní design patterns, jak fungují, k čemu jsou
## Vlákna, paralelní programování
- imagine vymýšlet maturitní otázky a myslet si že existuje slovo parale**r**ní, smh
- průběh programu, kde běží několik činností zároveň
- při vytvoření nového vlákna se vytvoří nový zásobník na stacku
- je možné mít více vláken než jader procesoru, jádra procesoru vlákna střídají
### Využití:
- lze využít pro paralelnost, např. vytvoříme vlákno pro každého klienta, který se připojí na server
- lze využít pro zvýšení výkonu tím, že komputaci rozdělíme na několik vláken zároveň
	- nemá smysl využívat více vláken, než je jader procesoru k dispozici, výkon se tím akorát zhorší
### Jednoduchá implementace paralelnosti v C#:
#### Kód:
```csharp
var thread1 = new Thread(() =>
{
	for (var i = 0; i < 10; i++) Console.WriteLine("1");
});

var thread2 = new Thread(() =>
{
	for (var i = 0; i < 10; i++) Console.WriteLine("2");
});

thread1.Start();
thread2.Start();

Console.WriteLine("Thready byly spuštěny, ale Main() metoda běží dál.");

thread1.Join();
thread2.Join();

Console.WriteLine("Vše je dokončeno.");
```
- metoda Join() zajistí, že Main() počká, než thread skončí svou exekuci 

```python
import threading
import time

def print_numbers():
    for i in range(1, 6):
        print(f"Number: {i}")
        time.sleep(1)

def print_letters():
    for letter in 'abcde':
        print(f"Letter: {letter}")
        time.sleep(1)

# Create threads
thread1 = threading.Thread(target=print_numbers)
thread2 = threading.Thread(target=print_letters)

# Start threads
thread1.start()
thread2.start()

# Wait for both threads to complete
thread1.join()
thread2.join()

print("Done!")
```
#### Output:
```
Thready byly spuštěny, ale Main() metoda běží dál.
1
2
1
2
2
1
1
2
1
2
Vše je dokončeno.
```
## Problémy s několika vlákny
- všechna vlákna přistupují k datům na haldě současně, což může způsobit, že se dvě vlákna pokusí změnit proměnnou současně, což může výrazně narušit logiku programu
- proměnné a metody můžeme zamknout, čímž zajistíme, že thready počkají na dokončení operace jiného threadu, než budou pokračovat ve vlastní exekuci
### Jednoduchý příklad zamykání metod v C#:
```csharp
public class Doggie
{
    private readonly object _locker = new object();

    private int _age;
    public int Age
    {
        get => _age;
        set
        {
            lock (_locker) //tady 
            {
                _age = value;
            } 
        }
    }
}
``` 
- ke změně věku pejska má přístup vždy jen jedno vlákno současně, takže je třída thread safe
- pokud přistupujeme k proměnné, která odkazuje na nějaký objekt, může být nutné zamknout i čtení proměnné kvůli změnám, které mohou ostatní vlákna vykonat, než se k hodnotě dostaneme
## Asynchronní metody
- imagine vymýšlet maturitní otázky a nevědět že se "asynchronní" píše s dvěma n, smh
- často se používají např. v JavaScriptu
- umožňují konkurenci, exekuce programu nečeká na dokončení exekuce async metody
- v JavaScriptu můžeme použít `await` keyword při volání metody, čímž zajistíme, že program počká na dokončení asnyc metody
- hodí se např. při připojení k databázi, může to trvat delší dobu, program nemusí čekat a může mezitím např. načítat zbytek UI
- v JavaScriptu mohou async metody také vracet Promise, což je ještě nedokončený výsledek asynchronní metody, můžeme na jeho dokončení počkat někde jinde
## Concurrent design patterns
### Producer-Consumer
- některé thready vytvářejí data na zpracování, jiné je zpracovávají
    - produceři data dávají do sdílené kolekce
    - comsumeři je berou a zpracovávají
### Future/Promise
- asynchronní funkce vrátí promise, což je objekt reprezentující budoucí výsledek, který ovšem ještě není hotový
### Thread pool
- na začátku programu vytvoříme thready, které jsou idle, dokud pro ně nemáme práci
- práce je pak rozdělena mezi thready, které už jsou vytvořeny
- nemusíme tvořit thready pokaždé, čímž se zvyšuje výkon