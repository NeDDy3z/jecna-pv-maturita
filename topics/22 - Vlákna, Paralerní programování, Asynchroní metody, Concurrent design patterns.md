# [Vlákna, Paralerní programování, Asynchroní metody, Concurrent design patterns](https://youtu.be/25J3XXahF3w?si=vcp1f1FF7fwRsbe_)
## O čem mluvit?
## Vlákna, paralelní programování
- imagine vymýšlet maturitní otázky a myslet si že existuje slovo arale**r**ní, smh
- průběh programu, kde běží několik činností zároveň
- při vytvoření nového vlákna se vytvoří nový zásobník na stacku
- je možné mít více vláken než jader procesoru, jádra procesoru vlákna střídají
### Využití:
- lze využít pro paralelnost, např. vytvoříme vlákno pro každého klienta, který se připojí na server
- lze využít pro zvýšení výkonu tím, že komputaci rozdělíme na několik vláken zároveň
	- nemá smysl využívat více vláken, než je jader procesoru k dispozici, výkon se tím akorát zhorší
### Jednoduchá implementace paralelnosti v C#:
#### Kód:
```
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
```
public class Doggie
{
    private readonly object _locker = new object();

    private int _age;
    public int Age
    {
        get => _age;
        set
        {
            lock (_locker)
            {
                _age = value;
            } 
        }
    }
}
``` 
- ke změně věku pejska má přístup vždy jen jedno vlákno současně, takže je třída thread safe
- pokud přistupujeme k proměnné, která odkazuje na nějaký objekt, může být nutné zamknout i čtení proměnné kvůli změnám, které mohou ostatní vlákna vykonat, než se k hodnotě dostaneme
### Asynchronní metody
- imagine vymýšlet maturitní otázky a nevědět že se "asynchronní" píše s dvěma n, smh
- často se používají např. v JavaScriptu
- umožňují konkurenci, exekuce programu nečeká na dokončení exekuce async metody
- v JavaScriptu můžeme použít `await` keyword při volání metody, čímž zajistíme, že program počká na dokončení asnyc metody
- hodí se např. při připojení k databázi, může to trvat delší dobu, program nemusí čekat a může mezitím např. načítat zbytek UI
- v JavaScriptu mohou async metody také vracet Promise, což je ještě nedokončený výsledek asynchronní metody, můžeme na jeho výsledek počkat někde jinde
### Concurrent design patterns
