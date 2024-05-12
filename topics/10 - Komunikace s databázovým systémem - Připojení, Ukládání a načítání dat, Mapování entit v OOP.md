# Komunikace s databázovým systémem - Připojení, Ukládání a načítání dat, Mapování entit v OOP

## O čem mluvit?
- jak se připojit k db
- co k tomu potřebuju
- jakým způsobem ukládám a čtu data
- vysvětlit ORM, k čemu je dobré
- zmínit fasádu

## Připojení
Většinou programovací jazyk neobsahuje nástroje k připojení na databázi, proto se nejdřív musí instalovat potřebné knihovny pro daný jazyk, tyto knihovny jsou vyvíjeny přímo vydavateli dané databáze. Takovým knihovnám se říká konektory - dovolují nám připojit se k databázi. 
Připojení k databázovému systému je přes TCP/IP spojení, tudíž potřebujeme IP adresu a někdy i port(příklad u C#).

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

C:
```c
 #include <mysql.h>
 #include <stdio.h>
 main() {
     MYSQL *conn;
     MYSQL_RES *res;
     MYSQL_ROW row;
     char *server = "localhost";
     char *user = "root";
     char *password = "PASSWORD";
     char *database = "mysql";
     conn = mysql_init(NULL);

     if (!mysql_real_connect(conn, server,
         user, password, database, 0, NULL, 0)) {
        fprintf(stderr, "%s\n", mysql_error(conn));
        exit(1);
    }

    if (mysql_query(conn, "show tables")) {
        fprintf(stderr, "%s\n", mysql_error(conn));
        exit(1);
    }
    res = mysql_use_result(conn);

    printf("MySQL Tables in mysql database:\n");
    while ((row = mysql_fetch_row(res)) != NULL)
        printf("%s \n", row[0]);
    
    mysql_free_result(res);
    mysql_close(conn);
}
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
Používáme SQL příkazy (SELECT, UPDATE, ...)

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

print(mycursor.rowcount, "details inserted")

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

for x in myresult:
	print(x)

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
Tímto tématem se zybývá architektura ORM(Objektově relační mapování), která převádí hodnoty uložené v relační databázi na objekty v naší aplikaci a zajišťuje synchronizaci dat mezi databází a těmito objekty. V dnešní době se používá běžně a je standardem pro základ aplikace, která nějakým způsobem manipuluje s databází.

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

### Fasáda
Softwarový návrhový vzor, který slouží ke zjednodušení komunikace mezi uživatelem a systémem. Použití je výhodné, pokud je tento systém příliš komplexní (obsahuje mnoho tříd a vazeb) pro splnění dané oblasti úloh, jež po něm vyžadují uživatelé. Fasáda je způsob nahrazení velkého počtu rozhraní subsystémů, sjednoceným rozhraním, které bude zaštitovat všechna rozhraní subsystémů.

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

