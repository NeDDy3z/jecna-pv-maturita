# Soubory a serializace - Ukládání a načítání dat, formáty souborů

## O čem mluvit?
- typycky mám nějaký file reader, kterym přečtu co je v souboru 
- mám: txt, json, ini, csv
- pro převod dic na json potřebujeme (v py) json.dump(dic) / pro čtení json.read()
- nesmí se zapomínat na vyjímky (try catch okolo readeru)
- jak probíha ser./deser.
	- proces přeměny objektu na stream bytů (v py se používá pickle knihovna) 
	- ukládáme do byte souboru

## Ukládání a načítání dat
Při ukládání proměnných v našem programu, proměnné se uloží pouze na dobu chodu programu. Tyto data jsou ztracena po vypnutí programu. Proto, na uchování dat na delší dobu, se používají soubory. Například uložení stavu herní postavy - kolik má životů, atd. Tyto data jsou načteny při startu programu ze souboru, do kterého byli uloženy.

Typické soubory do kterých ukládáme data jsou JSON, INI, CSV, XML, někdy TXT.

Můžeme využít také serializaci k uložení celých objektů a jejich stav do binárních souborů. Toto nám povoluje lehce přemisťovat nebo ukládat složitější struktury.

### Ukládání do TXT
Pokud není soubor, do kterého chceme data zapsat, nalezen, soubor se nejdřív vytvoří.

Python:
```python
f = open("file.txt", "a") # -> "a" for appending "w" for writing
f.write("Text that will go into file")  
f.close()
```

C:
```c
FILE *fptr;  
fptr = fopen("file.txt", "w");  
fprintf(fptr, "Boom");  
fclose(fptr);
```

C#:
```csharp
using(StreamWriter writetext = new StreamWriter("write.txt"))
{
    writetext.WriteLine("writing in text file");
}
```

### Načítání z TXT

Python:
```python
f = open("file.txt", "r")  
print(f.read())  
f.close()
```

C:
```c
FILE *fptr;  
fptr = fopen("file.txt", "r");
char myString[100];  
fgets(myString, 100, fptr);  
printf("%s", myString);  
fclose(fptr);
```

C#:
```csharp
using(StreamReader readtext = new StreamReader("readme.txt"))
{
   string readText = readtext.ReadLine();
}
```

### Ukládání dat
Aby jsme uložili data do jiného typu souboru než TXT, musíme znát jeho syntaxi, způsob zápisu. Např. kdyby jsme chťeli zapsat data v INI formátu do JSON souboru, dostali by jsme z toho JSON soubor, ale nevalidní JSON soubor, když by se potom načítal zpátky došlo by k chybě.

**JSON**

Python:
```python
import json

dictionary = {
	"name": "sathiyajith",
	"rollno": 56,
	"cgpa": 8.6,
	"phonenumber": "9976770500"
}

json_object = json.dumps(dictionary, indent=4)

with open("sample.json", "w") as outfile:
	outfile.write(json_object)
```

C:
```c
#include <stdio.h> 
#include <cjson/cJSON.h> //použití cJSON knihovny

int main() { 
// create a cJSON object 
cJSON *json = cJSON_CreateObject(); 
cJSON_AddStringToObject(json, "name", "John Doe"); 
cJSON_AddNumberToObject(json, "age", 30); 
cJSON_AddStringToObject(json, "email", "john.doe@example.com"); 

// convert the cJSON object to a JSON string 
char *json_str = cJSON_Print(json); 

// write the JSON string to a file 
FILE *fp = fopen("data.json", "w"); 
if (fp == NULL) { 
	printf("Error: Unable to open the file.\n"); 
	return 1; 
} 
printf("%s\n", json_str); 
fputs(json_str, fp); 
fclose
// free the JSON string and cJSON object 
cJSON_free(json_str); 
cJSON_Delete(json); 
return 0; 
}
```

C#:
```csharp
using System.IO;
using System.Collections.Generic;
using System.Text.Json;
using System.Text.Json.Serialization;

public class Customer
{
    public string Name { get; set; }
    public int Age { get; set; }
}

public class Program
{
    public static void Main()
    {
        List<Customer> customers = new List<Customer>();
        customers.Add(new Customer {Name = "Jason", Age = 25});
        customers.Add(new Customer {Name = "Nikki", Age = 20});
        string json = JsonSerializer.Serialize(customers);

        File.WriteAllText("customers.json", json);
    }
}
```

**CSV**

Python:
```python
import csv

data = [{"name": "John", "age": 30, "city": "New York"},
	{"name": "Jane", "age": 25, "city": "Los Angeles"},
	{"name": "Bob", "age": 40, "city": "Chicago"}]

with open("data.csv", "w", newline="") as file:
	writer = csv.DictWriter(file, fieldnames=["name", "age", "city"])
	writer.writeheader()

for item in data:
	writer.writerow(item)
```

**INI**

Python:
```python
import configparser

def create_config():
	config = configparser.ConfigParser()
	# Add sections and key-value pairs
	config['General'] = {'debug': True, 'log_level': 'info'}
	config['Database'] = {'db_name': 'example_db',
						'db_host': 'localhost', 'db_port': '5432'}
	# Write the configuration to a file
	with open('config.ini', 'w') as configfile:
		config.write(configfile)

if __name__ == "__main__":
	create_config()
```

### Načítání dat

**JSON**

Python:
```python
import json

# Opening JSON file
f = open('data.json')

# returns JSON object as 
# a dictionary
data = json.load(f)

# Iterating through the json
# list
for i in data['emp_details']:
	print(i)

f.close()
```

C: 
```c
#include <stdio.h> 
#include <cjson/cJSON.h> 

int main() { 
	// open the file 
	FILE *fp = fopen("data.json", "r"); 
	if (fp == NULL) { 
		printf("Error: Unable to open the file.\n"); 
		return 1; 
	} 

	// read the file contents into a string 
	char buffer[1024]; 
	int len = fread(buffer, 1, sizeof(buffer), fp); 
	fclose(fp); 

	// parse the JSON data 
	cJSON *json = cJSON_Parse(buffer); 
	if (json == NULL) { 
		const char *error_ptr = cJSON_GetErrorPtr(); 
		if (error_ptr != NULL) { 
			printf("Error: %s\n", error_ptr); 
		} 
		cJSON_Delete(json); 
		return 1; 
	} 

	// access the JSON data 
	cJSON *name = cJSON_GetObjectItemCaseSensitive(json, "name"); 
	if (cJSON_IsString(name) && (name->valuestring != NULL)) { 
		printf("Name: %s\n", name->valuestring); 
	} 

	// delete the JSON object 
	cJSON_Delete(json); 
	return 0; 
}
```

C#:
```csharp
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main(string[] args)
    {
        string filePath = "file.json";
        if (File.Exists(filePath))
        {
            try
            {
                string jsonString = File.ReadAllText(filePath);

                using (JsonDocument document = JsonDocument.Parse(jsonString))
                {
                    JsonElement root = document.RootElement;
                    string name = root.GetProperty("name").GetString();
                    int age = root.GetProperty("age").GetInt32();
                    string city = root.GetProperty("address").GetProperty("city").GetString();
                    string country = root.GetProperty("address").GetProperty("country").GetString();

                    Console.WriteLine("Name: " + name);
                    Console.WriteLine("Age: " + age);
                    Console.WriteLine("Address: " + city + ", " + country);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error reading JSON file: " + ex.Message);
            }
        }
        else
        {
            Console.WriteLine("File not found: " + filePath);
        }
    }
}
```

**CSV**

Python:
```python
import csv

with open('file.csv', mode ='r')as file:
csvFile = csv.reader(file)
for lines in csvFile:
		print(lines)
```

**INI**

Python:
```python
from configparser import ConfigParser 

configur = ConfigParser() 
print (configur.read('config.ini')) 

print ("Sections : ", configur.sections()) 
print ("Installation Library : ", configur.get('installation','library')) 
print ("Log Errors debugged ? : ", configur.getboolean('debug','log_errors')) 
print ("Port Server : ", configur.getint('server','port')) 
print ("Worker Server : ", configur.getint('server','nworkers'))
```


## Serializace a deserializace
Serializace je proces transformující objekt v operační paměti na stream bytů. Deserializace je opačný proces – rekonstruující objekt do operační paměti ze streamu bytů do stejného stavu, ve kterém byl objekt serializován.

V Pythonu se používá knihovna Pickle k serializaci a deserializaci objektů.

**Pickle dump:**

Python:
```python
import pickle

data = "Ajajajajj"

# open a file, where you ant to store the data
file = open('important', 'wb')

# dump information to that file
pickle.dump(data, file)

# close the file
file.close()
```

**Pickle load:**

Python:
```python
import pickle

# open a file, where you stored the pickled data
file = open('important', 'rb')

# dump information to that file
data = pickle.load(file)

# close the file
file.close()

print(data) # -> "Ajajajajj"
```


## Formáty souborů
K ukládání dat máme mnoho možností jak tyto data můžeme uložit, někdy chceme ukládat objekty nebo informace o nich, někdy jen konfiguraci programu, někdy nám stačí plain text. Podle těchto kritérií si určíme jaký typ souboru použít k uložení našich dat. Každý má, samozřejmě, svoji syntaxi.

**JSON:

Do JSON souborů můžeme ukládat stringy, celá čísla, logickou hodnotu a přidávat je ke klíčům. Můžeme ale také ukládat celé listy nebo objekty. Z tohoto důvodu je JSON často používaný soubor k ukládání dat, je i lehce čitelný.

```json
{
    "name": "Jason Ray",
    "profession": "Software Engineer",
    "age": 31,
    "address": {
        "city": "New York",
        "postalCode": 64780,
        "Country": "USA"
    },
    "languages": ["Java", "Node.js", "JavaScript", "JSON"],
    "socialProfiles": [
        {
            "name": "Twitter",
            "link": "https://twitter.com"
        },
        {
            "name": "Facebook",
            "link": "https://www.facebook.com"
        }
    ]
}
```

**CSV:**

Do CSV souborů ukládáme především data, která se dají uložit do tabulky. Soubor ve formátu CSV obsahuje řádky, ve kterých jsou jednotlivé položky odděleny čárkou.

```csv
Year,Make,Model,Length
1997,Ford,E350,2.35
2000,Mercury,Cougar,2.38
```

**INI:**

INI je jeden z konfiguračních souborů, ukládá stringy, může i čísla, ale zapíší se jako string, můžeme je ale přečíst jako čísla, ale můsíme vědět zda položka obsahuje čísla či ne. INI soubor se skládá z sekcí, každá sekce obsahuje klíče s daty.

```ini
[owner]
name = John Doe
organization = Acme Widgets Inc.

[database]
server = 192.0.2.62     
port = 143
file = "payroll.dat"
```

A mnoho dalších...
