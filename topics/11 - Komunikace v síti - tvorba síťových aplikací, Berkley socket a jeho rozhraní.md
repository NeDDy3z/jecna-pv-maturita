# Komunikace v síti - tvorba síťových aplikací, Berkley socket a jeho rozhraní

## O čem mluvit?
- protokoly
	- vyjmenovat různé protokoly
	- mluvit hlavně o TCP x UDP
	- **rozdíly**
	- na co se používají
	- uvést HTTP, typy requestů
- nějak popsat tvorbu síťových aplikací
- vysvětlit BSD
	- dát příklady z BSD API příkazů

## Komunikace v síti
Komunikace v síti probíhá díky určitým protokolům, mají určená využití. 
- výměna informací a dat např. mezi klienty, mezi klientem a serverem

### Transmission Control Protocol (**TCP**)
Nejpoužívanější protok transportní vrstvy (čtvrtá vrstva OSI). Použitím TCP mohou aplikace na počítačích propojených do sítě vytvořit mezi sebou _spojení_, přes které mohou obousměrně přenášet data. Protokol garantuje spolehlivédoručování a doručování ve správném pořadí. TCP také umožňuje rozlišovat a rozdělovat data pro více aplikací (například webový server a emailový server) běžících na stejném počítači.

TCP využívá mnoho populárních aplikačních protokolů a aplikací na internetu, včetně WWW, e-mailu a SSH.

**Navázání spojení** 
Probíhá ve třech krocích(3-way handshake):
- Klient odešle na server datagram s nastaveným příznakem SYN a náhodně vygenerovaným pořadovým číslem (x), potvrzovací číslo=0.
- Server odešle klientovi datagram s nastavenými příznaky SYN a ACK, potvrzovací číslo=x+1, pořadové číslo je náhodně vygenerované (y)
- Klient odešle datagram s nastaveným příznakem ACK, pořadové číslo=x+1, číslo odpovědi=y+1.

<img src="images/11_3-way_handshake.png">

Obě strany si pamatují pořadové číslo vlastní i protistrany. Používají se totiž i pro další komunikaci a určují pořadí paketů. Když úspěšně proběhne trojcestný handshaking, je spojení navázáno a zůstane tak až do ukončení spojení.

<img src="images/11_tcp_communication.png">

**Ukončení spojení** 
Probíhá podobně jako jeho navázání. Používá se k tomu příznaků FIN a ACK:
- Strana, která nechce posílat další data, odešle datagram s nastaveným příznakem FIN
- Protistrana odpoví datagramem s nastaveným příznakem ACK s potvrzovacím číslem o jedničku větším, než bylo pořadové číslo v datagramu s příznakem FIN (jako kdyby protistrana poslala místo FIN jeden byte dat)
- Druhá strana, která ukončuje posílání dat, odešle datagram s nastaveným příznakem FIN
- Protistrana odpoví datagramem s nastaveným příznakem ACK

<img src="images/11_3-way_handshake(term).jpg">

Po prvních dvou krocích může druhá strana pokračovat v posílání dat. Pokud žádná data posílat nebude, mohou být kroky 2 a 3 sloučeny. Teprve po těchto čtyřech krocích je spojení ukončeno.

**TCP Příklad:**
Python:
Server:
```python
import socket

HOST = '127.0.0.1'
PORT = 12345

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server_socket:
    server_socket.bind((HOST, PORT))
    server_socket.listen()

    print("Server is listening on port", PORT)
    connection, address = server_socket.accept()
    print("Connected to", address)

    with connection:
        while True:
            data = connection.recv(1024)
            if not data:
                break
            print("Received:", data.decode())
            connection.sendall(data.upper())
```

Klient:
```python
import socket

HOST = '127.0.0.1'
PORT = 12345

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as client_socket:
    client_socket.connect((HOST, PORT))
    
    message = "Hello, server!"
    client_socket.sendall(message.encode())
    print("Sent:", message)

    response = client_socket.recv(1024)
    print("Received:", response.decode())
```

### User Datagram Protocol (UDP)
Jednoduchý protokol založený na posílání nezávislých zpráv. Nezachovává pořadí paketů. Prostě to “chrlí”. Když se jeden paket ztratí, nic se neděje.

Toto z něj dělá značně rychlejší protokol než je TCP. Je ale nespolehlivý a to v tom, že nekontroluje doručené packety.

Protokol UDP je vhodný pro nasazení, které vyžaduje jednoduchost, malá režie nebo pro aplikace pracující systémem otázka-odpověď (např. DNS, sdílení souborů v LAN. Jeho bezstavovost je užitečná pro servery, které obsluhují mnoho klientů nebo pro nasazení, kde se počítá se ztrátami datagramů a není vhodné, aby se ztrácel čas novým odesíláním (starých) nedoručených zpráv (např. VoIP, online hry).

<img src="images/11_udp_communication.png">

**UDP Příklad:**
Python:
Server:
```python
import socket

HOST = '127.0.0.1'
PORT = 12345

# Create a UDP socket
with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as server_socket:
    server_socket.bind((HOST, PORT))
    print("Server is listening on port", PORT)

    while True:
        data, address = server_socket.recvfrom(1024)
        print("Received from", address, ":", data.decode())
        server_socket.sendto(data.upper(), address)
```

Klient:
```python
import socket

HOST = '127.0.0.1'
PORT = 12345

# Create a UDP socket
with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as client_socket:
    message = "Hello, server!"
    client_socket.sendto(message.encode(), (HOST, PORT))
    print("Sent:", message)

    response, server_address = client_socket.recvfrom(1024)
    print("Received from server:", response.decode())
```


### Rozdíly mezi TCP a UDP
TCP je spojově orientovaný protokol což znamená, že k navázání "end-to-end" komunikace potřebuje, aby proběhl mezi klientem a serverem tzv. "handshaking". Poté, co bylo spojení navázáno, data mohou být posíláná oběma směry. Charakteristické vlastnosti TCP protokolu jsou:

- spolehlivost – TCP používá potvrzování o přijetí, opětovné posílání a překročení časového limitu. Pokud se jakákoliv data ztratí po cestě, server si je opětovně vyžádá. U TCP nejsou žádná ztracená data, jen pokud několikrát po sobě vyprší časový limit, tak je celé spojení ukončeno.
- zachování pořadí – Pokud pakety dorazí ve špatném pořadí, TCP vrstva příjemce se postará o to, aby se některá data pozdržela a finálně je předala správně seřazená.
- vyšší režie – TCP protokol potřebuje např. tři pakety pro otevření spojení, umožňuje to však zaručit spolehlivost celého spojení.

UDP je jednodušší protokol založený na odesílání nezávislých zpráv. Charakteristika protokolu:

- bez záruky – Protokol neumožňuje ověřit, jestli data došla zamýšlenému příjemci. Datagram se může po cestě ztratit. UDP nemá žádné potvrzování, přeposílání ani časové limity. V případě potřeby musí uvedené problémy řešit vyšší vrstva.
- nezachovává pořadí – Při odeslání dvou zpráv jednomu příjemci nelze předvídat, v jakém pořadí budou doručeny.
- jednoduchost – Nižší režie než u TCP (není zde řazení, žádné sledování spojení atd.).


### Hyper Text Transfer Protocol (HTTP)
Postavený na protokolu TCP.

V tomto případě jsme většinou v roli klienta a komunikujeme se vzdáleným webserverem (nginx, apache). Využít můžeme například jednoduchou třídu WebClient. Ve většině případů posíláme 2 typy requestů, a to POST a GET.

#### GET
- request pomocí URL např. pro ověření konektivity na stránku 'https://w3schools.com' pomocí *get* metody v pythonu
- v Pythonu existuje modul *requests* který se o HTTP requesty stará
- 
Python:
```python
import requests

x = requests.get('https://w3schools.com')

print(x.status_code)
```

#### POST
- odesílá uživatelská data na server
- používá se například při odesílání formuláře na webu
- s předaným objektem se pak zachází podobně jako při metodě GET. Data může odesílat i metoda GET (viz search_query) , metoda POST se však používá pro příliš velký objem dat (víc než 512 bajtů, což je velikost požadavku GET), nebo pokud není vhodné přenášená data zobrazit jako součást URL (data předávaná metodou POST jsou obsažena v HTTP požadavku)

Python:
```python
import requests

url = 'https://www.w3schools.com/python/demopage.php'

myobj = {'somekey': 'somevalue'}

x = requests.post(url, json = myobj)

print(x.text)
```

#### Další typy requestů:
- **PUT**
	- Nahraje data na server. Objekt je jméno vytvořeného souboru. Používá se velmi zřídka, pro nahrávání dat na server se běžně používá FTP nebo SCP/SSH.

- **DELETE**
	- Smaže uvedený objekt ze serveru. K tomu je zapotřebí jistých oprávnění stejně jako u metody PUT.
- **TRACE**
	- Odešle kopii obdrženého požadavku zpět odesílateli, takže klient může zjistit, co na požadavku mění nebo přidávají servery, kterými požadavek prochází.
- **OPTIONS**
	- Dotaz na server, jaké podporuje metody.
- **HEAD**
	- Metoda podobná GET, avšak nepředává data. Poskytne pouze metadata o požadovaném cíli (velikost, typ, datum změny, …).


### Další protokoly
- File Transfer Protocol (FTP)
- SSH File Transfer Protocol (SFTP)
- Simple Mail Transfer Protocol (SMTP)


## Tvorba síťových aplikací
K vývoji síťové aplikace, jako např. e-mail, online hra, nějaký FTP server, ..., se nejdřív muíme rozhodnout jaký protokol je vhodný pro naši aplikaci. Například UDP na online hru, SMTP na e-mail, atd.

Zajistit šifrování a bezpečnost. Např. webovou stránku mít na HTTPS ne HTTP, pokud manipulujeme s citlivými daty. 

(pls o doplnění jestli někdo ví co by sem mohlo ještě patřit)

## Berkeley socket
Berkeley Socket (BSD socket) poskytuje programátorům sadu/knihovnu funkcí a metod pro vytváření síťových aplikací, jako jsou klienti a servery. Tyto funkce umožňují programům vytvářet a spravovat síťová spojení, posílat a přijímat data přes síť a manipulovat se síťovými adresami.

Tato technologie byla vyvinuta v Univerzitě v Berkeley v 80. letech a stala se de facto standardem pro síťovou komunikaci v UNIXových a UNIX-like operačních systémech. Berkley Socket API je k dispozici v mnoha programovacích jazycích, včetně C, C++, Pythonu a dalších. Je základem pro vytváření široké škály síťových aplikací, včetně webových serverů, emailových klientů, online her a mnoho dalšího.

Aktuálně je implementace BSD sockets dostupná v každém moderním operačním systému a jedná se tak o standard v rámci připojování k Internetu.

Výpis funkcí, které nabízí API BSD sockets:

- `socket()` vytváří nový socket daného typu, identifikovaný celým číslem, s alokovanými systémovými prostředky.
- `bind()` je obvykle používán na straně serveru a typicky spojuje lokální port s IP adresou.
- `listen()` se používá na straně serveru uvádí TCP socket do stavu listen.
- `connect()` se používá na straně klienta a přiřazuje volný lokální port k socketu. V případě TCP socketu vytvoří nové TCP spojení.
- `accept()` se používá na straně serveru. Potvrzuje příchozí požadavek na ustavení nového TCP spojení od vzdáleného klienta a vytváří nový socket.
- `send()` a `recv()`, nebo `write()` a `read()`, nebo `sendto()` a `recvfrom()`, se používají pro odesílání a přijímání dat z/na vzdálený socket.
- `close()` požádá systém o uvolnění prostředků, které měl socket alokované. V případě TCP je spojení přerušeno.
- `gethostbyname()` a `gethostbyaddr()` se používají pro vzájemný překlad jmen hostů a adres. Podporováno je pouze IPv4.
- `select()` je využíván k čekání, než bude socket nebo seznam socketů připraven.
- `poll()` se používá ke kontrole stavu socketu ze skupiny socketů. Skupina může být kontrolována, zda je možné do některého socketu zapsat, číst z něj, nebo zda nenastala nějaká chyba.
- `getsockopt()` umožňuje získat aktuální stav dané vlastnosti socketu.
- `setsockopt()` umožňuje nastavit hodnotu dané vlastnosti socketu.
