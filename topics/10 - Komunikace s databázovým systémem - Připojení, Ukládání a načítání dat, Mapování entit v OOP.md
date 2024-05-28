# [Komunikace s databázovým systémem - Připojení, Ukládání a načítání dat, Mapování entit v OOP](https://youtu.be/lFRMdGfo_XA)

## O čem mluvit?
- Připojení k DB
	- connection string
        - knihovny od vývojářů DB
        - TCP
	- potřebujeme ip,port,user,psswd,...
- Ukládání a načítaní dat
	- connection string
        - queries
- Mapování v OOP s ORM
	- převádění dat z DB -> objekty v programu
        - nemapujeme vsechny (např poznámky)
        - dulezita soucast pri pesci s DB
- Fasáda
        - návrhový vzor
        - zjednodušuje komunikaci uživ. s DB
        - treba si jdelam metody na kazdou akci s DB

## Připojení
- většinou programovací jazyk neobsahuje nástroje k připojení na databázi
	- pro to se obvykle používají knihovny 
		- tyto knihovny jsou vyvíjeny přímo tvůrci daného DB systému
		- takovým knihovnám se říká konektory - dovolují nám připojit se k databázi
- připojujeme se k DB přes TCP/IP spojení
	- tudíž potřebujeme IP adresu a někdy i port (příklad u C#)
- k připojení obvykle potřebujeme následující údaje *(příklady v mysql - data jsou příkladová)*
	- username *root*
	- password *student*
	- hostname *127.0.0.1*
	- port *3306*

Příklady instalace MySQL konektoru:
Python:
```
pip install mysql-connector-python
```

C:
```
Stáhnout konektor knihovnu z: https://dev.mysql.com/downloads/connector/cpp/
```

C#:
```
Instalovat Sql.Data NuGet package
```

Příklad připojení na databázi:
Python:
```python
import mysql.connector
  
mydb = mysql.connector.connect(  
  host="localhost",  
  user="_yourusername_",  
  password="_yourpassword_"  
)

```

C#:
```csharp
using System;
using MySql.Data.MySqlClient;

class Program
{
    static void Main()
    {
        string connectionString = "server=localhost;port=3306;database=mydatabase;uid=myusername;password=mypassword";
        try
        {
            using (MySqlConnection connection = new MySqlConnection(connectionString))
            {
                connection.Open();
                Console.WriteLine("Connected to MySQL database.");
                connection.Close();
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}
```

## Ukládání a načítání dat
- používáme SQL příkazy (SELECT, UPDATE, ...)
- vytváříme tzv. queries které pak posíláme DB

**Ukládání**
Python:
```python
import mysql.connector
  
mydb = mysql.connector.connect(  
  host="localhost",  
  user="_yourusername_",  
  password="_yourpassword_"  
)

mycursor = mydb.cursor()
sql = "INSERT INTO Student (Name, Roll_no) VALUES (%s, %s)"
val = ("Ram", "85")

mycursor.execute(sql, val)
mydb.commit()

mydb.close()
```

**Načítání**
Python:
```python
import mysql.connector 
 
mydb = mysql.connector.connect(  
  host="localhost",  
  user="_yourusername_",  
  password="_yourpassword_"  
)

mycursor = mydb.cursor()

print("Displaying NAME and ROLL columns from the STUDENT table:")

query = "SELECT NAME, ROLL FROM STUDENT"
mycursor.execute(query)

myresult = mycursor.fetchall()

for result in myresult:
	print(result)

mydb.close()
```

Pomocí tohoto příkladu můžeme provádět i složitější querries v naší databázi. Např.:

Python:
```python
import mysql.connector 
 
mydb = mysql.connector.connect(  
  host="localhost",  
  user="_yourusername_",  
  password="_yourpassword_"  
)

mycursor = mydb.cursor()

print("Displaying NAME and ROLL columns from the STUDENT table:")

query = "SELECT NAME, ROLL FROM STUDENT WHERE Roll_no>101" #Můžeme vytvářet vlastní querries
mycursor.execute(query)

myresult = mycursor.fetchall()

for x in myresult:
	print(x)

mydb.close()
```

Samozřejmě potřebujeme mít nějaké znalosti s SQL jazykem a znát databázový systém s kterým pracujeme.

## Mapování entit v OOP
- tímto tématem se zabývá architektura ORM (Objektově relační mapování)
	- převádí hodnoty uložené v relační databázi na objekty v naší aplikaci a zajišťuje synchronizaci dat mezi databází a těmito objekty
- v dnešní době se používá běžně a je standardem pro základ aplikace, která nějakým způsobem manipuluje s databází

ORM je vestavěné do webových frameworků jako např. Symphony.

Třídy které vytváříme na základě entit v databázi **nemusí** mapovat všechny sloupce entity. (např. můžeme vynechat poznámky - pokud nejsou třeba v aplikaci)

Python:
```python
#Taky potřebujeme sqlalchemy knihovnu -> pip install sqlalchemy

from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Create the database engine
engine = create_engine('mysql+mysqlconnector://username:password@localhost/mydatabase')

# Define the base class for declarative
Base = declarative_base()

# Define a simple User model
class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    age = Column(Integer)

# Create the database schema
Base.metadata.create_all(engine)

# Create a session to interact with the database
Session = sessionmaker(bind=engine)
session = Session()

# Create a new user
new_user = User(name='John Doe', age=30)
session.add(new_user)
session.commit()

# Query all users
users = session.query(User).all()
for user in users:
    print(user.name, user.age)

# Update a user
user_to_update = session.query(User).filter_by(name='John Doe').first()
user_to_update.age = 35
session.commit()

# Delete a user
user_to_delete = session.query(User).filter_by(name='John Doe').first()
session.delete(user_to_delete)
session.commit()

# Close the session
session.close()
```

#### Fasáda
- návrhový vzor 
- slouží ke zjednodušení komunikace mezi uživatelem a systémem 
- použití je výhodné, pokud je tento systém příliš komplexní (obsahuje mnoho tříd a vazeb) pro splnění dané oblasti úloh, jež po něm vyžadují uživatelé. 
- fasáda je způsob nahrazení velkého počtu rozhraní subsystémů, sjednoceným rozhraním, které bude zaštitovat všechna rozhraní subsystémů

Vytvoření fasády pro lehčí manipulaci s entitou Users.

Python:
```python
import mysql.connector

class UserDatabase:
	def __init__(self, host, user, password, database):
		self.connection = mysql.connector.connect(
		host=host,
		user=user,
		password=password,
		database=database
	)
	self.cursor = self.connection.cursor()

	def create_user(self, name, email):
		sql = "INSERT INTO users (name, email) VALUES (%s, %s)"
		values = (name, email)
		self.cursor.execute(sql, values)
		self.connection.commit()
		return self.cursor.lastrowid

	def get_user(self, id):
		sql = "SELECT * FROM users WHERE id = %s"
		values = (id,)
		self.cursor.execute(sql, values)
		return self.cursor.fetchone()

	def update_user(self, id, name=None, email=None):
		sql = "UPDATE users SET "
		values = []
		if name is not None:
			sql += "name = %s, "
			values.append(name)
		if email is not None:
			sql += "email = %s, "
			values.append(email)
		sql = sql[:-2] + " WHERE id = %s"
		values.append(id)
		self.cursor.execute(sql, values)
		self.connection.commit()
		return self.cursor.rowcount > 0

	def delete_user(self, id):
		sql = "DELETE FROM users WHERE id = %s"
		values = (id,)
		self.cursor.execute(sql, values)
		self.connection.commit()
		return self.cursor.rowcount > 0

	def __del__(self):
		self.connection.close()
```

