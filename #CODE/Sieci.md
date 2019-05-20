# 🌐Internet

## Zapytania

![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536228644/Education/net_architecture.png)

### Przebieg zapytania

1. Przeglądarka wysyła zapytanie (Request) do serwera
2. ISP (Internet Service Provider) przeprowadza wyszukiwanie DNS (Domain Name Service) i tłumaczy adres domeny (np. [name.com](http://name.com)) na IP serwera
3. Serwer zwraca odpowiedź (Response) do przeglądarki

Przebieg zapytania można sprawdzić w przeglądarce: Google Chrome - F12 > Network > Lista ładowanych stron i zasobów > Wybrać stronę np. Google.com

### Zapytanie (request) zawiera

* Nagłówki (Headers)
    * Host
        * :host: [www.google.pl](http://www.google.pl)
    * Metoda
        * `GET` \- pobieranie informacji // :method: GET
        * `POST` \- tworzenie informacji
            * Dodaje POST BODY do zapytania (np. username & password)
        * `PUT` \- edycja informacji
        * `DELETE` \- usuwanie informacji
    * Path
        * `:path: /`
        * `:path: images/logo.png`
    * Cookies
        * String
        * `cookie: SID=cgZMXms9F2k-5SHUzm4bJZzNXYejMpdT4zEDMza9GHA2yHiaqbyCk7sH3ionu1o3XPqfYg.; HSID=AUMwGmQFpVYqATjuU; SSID=A0qUs8sGMe5wy1o3T; APISID=5yJDWVVVEjWYK9DC/A4vPJEPOedYRyEg3W; SAPISID=HOF48Z-WnJ8QKVDk/AA9hh9i9mLFZnVi30; NID=138=DKWGEYMEIEZUdPeb3YRS2-pCqeIOkGKwIPx_lfr__BOeoU4SDTrQSEybxfnCrJoHKR0MaY07evQgIpVOa8IfFwzLllDVPA8v_APtGS_nqJifiot-hz1gAQy2wQ6NN0yWX8Sf2sCk_yOwRtBb7cjqJdnTd902H29hsnJgkBM_sJjDWrQsDe_sJ1HW6_hJpE9olW5CzvQTz27Ybz-NmLjfnKc2B8A-4WYW3RQudm_P; 1P_JAR=2018-9-6-11`
    * User-agent
        * String
        * user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36
    * Content type
        * application/json
* POST Body
    * zapytanie może, ale nie musi je zawierać
    * `({username: 'xxx', password: 'yyy'})`

### Odpowiedź (response) zawiera

* Nagłówki (Headers)
    * Content type
        * content-type: text/html; charset=UTF-8
    * Status Code
        * `200` \- OK
        * `300` \- Redirected
        * `400` \- Not found
        * `500` \- Error
* Response Body
    * Pliki (html, css, js, image) lub
    * Rezultaty (json, xml)

# 🖥️ Serwer

**Serwer** \- maszyna podłączona do internetu z własnym unikalnym numerem IP

## Przykładowe konfiguracje serwerów

### Basic Website Server

* Apache (Web Server)
    * Nasłuchuje portu 80
    * Konfiguruje hosty tak aby wskazywały na odpowiednie foldery w systemie plików
        * [mysite.com](http://mysite.com) ->> domains/[mysite.com/public_html/index.html](http://mysite.com/public_html/index.html)
        * [mysite.com/logo.png](http://mysite.com/logo.png) ->> domains/[mysite.com/public_html/imgs/logo.png](http://mysite.com/public_html/imgs/logo.png)

### Web Application Server

* Web Application
    * [twitter.com/login](http://twitter.com/login) ->> renderuje zawartość strony
    * [mysite.com/logo.png](http://mysite.com/logo.png) ->> wysyła odpowiedź zawierającą wskazany obraz
* Database
    * Użytkownicy
    * Tweety

### Typy serwerów

* **LAMP** \- Linux \+ Apache \+ MySQL \+ PHP
* **Load Balancer** \- Oddzielna maszyna\, która przekierowuje ruch z zapytań do jednej z kilku maszyn zawierających tę samą aplikację\. Przykład: \[Load Balancer\] \-\>\> \[Twitter\_01\]\[Twitter\_02\]\[Twitter\_03\] \(\-\>\> Wspólna baza danych\)

### Konfiguracja własnego serwera

* Gotowe rozwiązania
    * XAMPP - [https://www.apachefriends.org/](https://www.apachefriends.org/)
    * WAMPP - [http://www.wampserver.com/](http://www.wampserver.com/en/)

# 🔌 Sieć

**Sieć** \- zbiór urządzeń \(komputery\, telefony\, drukarki\, tablety itp\.\) podłączonych \(za pomocą kabla\, WIFI\, satelity itp\.\) do internetu; Celem sieci jest przesył danych\.
**Dane** (Data) - wszelkie informacje przesyłane wewnątrz sieci

**NIC** (Network Interface Card) - Karta sieciowa pozwalająca połączyć komputer z internetem. Składa się z dwóch elementów: wejścia do płyty głównej oraz wyjścia na kabel internetowy

### Typy sieci

Podział według zasięgu i rozmiaru:

* **LAN** \- Local Area Network \- Urządzenia w tym samym budynku
* **MAN** \- Metropolitan Area Network \- Zasięg miasta np\. szpitale połączone we wspólną sieć
* **WAN** \- Wide Area Network \- Zasięg powyżej 30 mil / 48 km === Internet

SOHO (Small Office Home Office Networks) - małe sieci w biurach, domach itp.

### Elementy sieci

* **Węzeł (Node)** \- element sieci będący urządzeniem np\. PC\, modem\, router\, drukarka\, serwer
    * Klient - otrzymuje dane
    * Host - węzeł który przekazuje dane
* **Media komunikacyjne (Communications media)** \- element sieci służący do przesyłu np\. kable\, fale radiowe i inne sposoby łączenia ze sobą węzłów

### Topologia sieci komputerowych

#### Topologia liniowa (Line)

Wszystkie elementy sieci (oprócz granicznych) połączone są z dwoma sąsiadującymi.

#### Topologia magistrali (szyny, liniowa) (BUS)

Magistrala (kabel w linii prostej) do której podpięte są wszystkie urządzenia
Cechy

* Tania
* Wymaga terminatorów na końcu kabla
* Łatwo się psuje (wystarczy, że zepsuje się terminator i otrzymujemy dużo odbić)

#### Topologia pierścienia (Ring)

* Kabel w kształcie pierścienia (koła) do którego podpięte są wszystkie urządzenia.
* Terminatory nie są potrzebne
* Sygnał przemieszcza się wzdłuż pierścienia do każdego węzła (nawet jeśli już otrzyma odpowiedź od serwera) dopóki nie dotrze do węzła który wysłał zapytanie
* Zwykle tworzy się 2 pierścienie koło siebie (dane przepływają na nich w przeciwne strony)

Cechy

* Lepszy przepływ danych niż w BUS
* Droższy niż BUS

#### Topologia podwójnego pierścienia (Double Ring)

Poszczególne elementy są połączone pomiędzy sobą odcinkami tworząc dwa zamknięte pierścienie

#### Topologia gwiazdy (Star)

Wiele urządzeń podłączonych do jednego centralnego urządzenia np. routera
Cechy

* Niski koszt
* Łatwy do rozbudowy
* Awaria węzłów nie wpływa na działanie sieci
* Awaria centralnego urządzenia powoduje awarię całej sieci

#### Topologia siatki (Mesh)

Każdy węzeł sieci jest połączony z każdym innym węzłem.

* Stosowana raczej w MAN i WAN (nie LAN)
* Kosztowna (potrzebne karty NIC z większą ilością wejść)

**Terminator** \- musi znajdować się na końcu kabla\. Powodują że sygnał nie zostaje odbity

## Protokoły

Zasady komunikacji pomiędzy elementami sieci

* Format wiadomości
* Kolejność wiadomości

### Rodzaje portokołów

#### TCP/IP (Transmission Control Protocol/Internet Protocol)

Protokół komunikacyjny definiujący jak dane powinny podróżować po sieci
Warstwy

* **Aplikacji**
    * Warstwa procesowa czy warstwa aplikacji (ang. process layer) to najwyższy poziom, w którym pracują użyteczne dla człowieka aplikacje takie jak np. serwer WWW czy przeglądarka internetowa
    * Obejmuje ona zestaw gotowych protokołów, które aplikacje wykorzystują do przesyłania różnego typu informacji w sieci
* **Transportowa**
    * Kieruje właściwe informacje do odpowiednich aplikacji
    * TCP (Transport Control Protocol)
        * CONNECTION ORIENTED - 3 kierunkowy uścisk dłoni; gwarancja wysłania danych z komputera A do B
        * Dzieli dane z aplikacji na mniejsze pakiety
        * Dołącza nagłowki, aby pakiety mołgy być poprawnie połączone w całość
        * Porotokoły zależne
            * HTTP (Hyper Text Transfer Protocol) - protokół przesyłania dokumentów hipertekstowych (protokół sieci WWW - World Wide Web)
            * HTTPS (Hypertext Transfer Protocol Secure) - szyfrowane przesyłanie danych hipertekstowych przy pomocy SSL lub TLS (nowszy)
            * SMTP (Simple Mail Transfer Protocol) - protokół poczty elektronicznej, komunikacja pomiędzy serwerami poczty
            * IMAP4 (Internet Message Access Protocol) - protokół poczty elektronicznej, pobiera wiadomość z serwera zostawiając kopię w skrzynce
            * POP3 (Post Office Protocol) - protokół poczty elektronicznej, pobiera wiadomość z serwera nie zostawiając kopii w skrzynce
            * FTP (File Transfer Program) - protokół umożliwiający dwukierunkowy transfer plików
            * TFTP (Trivial File Transfer Protocol)
            * SFTP (Secure File Transfer Protocol)
            * SSH (SSH File Transfer Protocol / Secure Shell)
            * Telnet - protokół pozwala połączyć się zdalnie z innym kompueterem, obsługuje terminale alfanumeryczne

#### UDP (User Datagram Protocol)

* CONNECTION - LESS - brak gwarancji wysłania danych z komputera A do B
* Porotokoły zależne
    * SNMP (Simple Network Managment Protocol) - zbiera informacje o infrastrukturze sieci (serwery, routery, firewalle) i wysyła je do aplikacji
    * NTP (Network Time Protocol) - synchronizacja urządzeń
    * SIP (Session Initiation Protocol) - głos i wideo
    * RTSP (Real Time Streaming Protocol) - streaming mediów
    * DHCP (Dynamic Host Configuration Protocol) - protokół komunikacyjny umożliwiający hostom uzyskanie od serwera danych konfiguracyjnych
        * DORA - 4 stopnie w procesie przypisania adresu IP do klienta
            * Discovery
            * Offer
            * Request
            * Acknowledgement

#### Protokoły zależne od UDP i TCP

* DNS (Domain Name System) - dopasowuje domeny do adresów IP
* LDAP (Lightweight Directory Access Protocol) - protokół przeznaczony do korzystania z usług katalogowych (imię, nazwa usera, hasło, nazwa serwera)
* RDP (Remote Desktop Protocol) - protokół pozwalający na komunikację z usługą terminala graficznego w Windows
* **Internetowa**
    * Warstwa protokołu internetowego przetwarza datagramy posiadające adresy IP i ustala odpowiednią drogę do docelowego komputera w sieci
    * IP - Internet Protocol
        * IPv4
        * IPv5
        * IPv6
* **Dostępu do sieci (Network)**
    * Odpowiada za wysłanie danych w postaci elektrycznych impulsów do właściwej fizycznej maszyny

#### Protokół DHCP (Dynamic Host Configuration Protocol)

* Nowo podpięty pod sieć komputer wysyła DHCP Discover Message
* Bazowy adres IP przed przypisaniem to 0.0.0.0
* Router odsyła DHCP Offer z dostępnym numerem IP np.106.66.67.68
* Komputer odsyła DHCP Request prosząc o przyznanie otrzymanego wcześniej IP
* Router odsyła ACK: numer IP, subnet mask i inne przydatne informacje

#### Protokół DNS

**DNS** \- Domain Name System\, który pozwala tłumaczyć adres stron internetowych na adresy IP\. DNS to specjalne serwery zawierające informacje\.

* localhost - 127.0.0.1
* Przypisywanie masek dla localhost: C:\Windows\System32\drivers\etc
* Zmiana DNS dla stron internetowych: Panel sterowania\Sieć i Internet\Połączenia sieciowe > PKLIK na połączeniu > Właściwości > Protokół Internetowy w wersji 4 > Właściwości > DNSy na dole

**Routing Tables**

* Router = Gateway - brama do innych sieci
* Przy próbie połączenia z adresem IP sprawdzane są reguły. Jeśli żadna nie pasuje wybierana jest domyślna. Każda routing table ma przynajmniej jedną domyślną drogę.
* Jeśli adres pasuje do więcej niż jeden reguły wybiera tę w najdłuższą maską subnet
* Flagi
    * U - Up
    * G - Gateway

**iptables Firewall Rules**

* iptables -L // wyświetla wszystkie zasady
* Zbiory zasad nazywane są chains
* 3 rodzaje danych:
    * INPUT - dane otrzymywane z internetu
    * OUTPUT - dane wysyłane
    * FORWARD - przesyłanie danych pomiędzy urządzeniami
* iptables -P FORWARD DROP // ustawia dla reguły FORWARD domyślną akcję (-P) DROP
* iptables -A INPUT -s 192.168.0.23 -j DROP // Dla reguły INPUT dodajemy/rozszerzamy regułę (-A) - ze źródła (-s) o numerze IP 192.168.0.23, gdy otrzymujemy dane (-j) chcemy by następował DROP
* iptables -A INPUT -s 129.168.0.0/24 -p tcp --destination-port 25 -j DROP // Kiedykolwiek komputer otrzyma dane z sieci o IP 129.168.0.0 i będzie to ruch z portu 25 to należy go odrzucić (odrzucanie upierdliwych maili od stalkingującej grupy ludzi).
* iptables -A INPUT -s 192.168.0.66 -j ACCEPT // Akceptujemy dane przychodzące od podanego adresu IP, reguła zostaje dodana na końcu łańcucha
* Kolejność reguł ma znaczenie - na górze ważniejsze, na dole mniej ważne
* iptables -D INPUT 3 // Usuwamy regułę (-D) o numerze 3 (od góry)
* iptables -I INPUT -s 192.168.0.66 -j ACCEPT // Akceptujemy dane przychodzące od podanego adresu IP, reguła zostaje dodana na początku łańcucha

## Porty

Umożliwiają komunikację między warstwą Aplikacji i Transportu\
Lista popularnych portów\
`53` \- DNS\
`80` \- HTTP\, dodatkowe serwery\, np\. proxy\, są najczęściej umieszczane na porcie 8080\
`443` \- HTTPS \(HTTP na SSL\)\
`25` (`465` \- TLS/SSL\) \- SMTP\
`110` (`995`\- TLS/SSL nazwane POP3S\) \- POP3\
`143` (`993` \- TLS/SSL\) \- IMAP4\
`220` \- IMAP3\
`20` \- FTP – przesyłanie danych\
`21` \- FTP – przesyłanie poleceń \(ustanowienie połączenia\)\
`69` \- TFTP\
`22` \- SSH\
`22` \- SFTP\
`23` \- Telnet
`67` \- DHCP – serwer\
`68` \- DHCP – klient\
`161-162` \- SNMP\
`5060` (`5061` \- TLS/SSL\) \- SIP\
`3389` \- RDP\
`79` \- Finger\
`70` \- Gopher\
`6661 – 6667` \- IRC\
`5222` \- XMPP – dla serwera sieci Jabber\
`389` \- LDAP\
`636` \- LDAPS \(LDAP na SSL\)\
`3306` \- MySQL\
`119` \- NNTP\
`5432` \- PostgreSQL\
`873` \- Rsync\
`514` \- Syslog\
`6000 – 6007` \- X11\
`123` \- NTP\
`554` \- RTSP

## OSI Model (ISO Open Systems Interconnection Reference Model)

Model OSI opisuje drogę danych od aplikacji w systemie jednej stacji roboczej do aplikacji w systemie drugiej
![image](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536308472/Education/seven-layers-of-OSI-model.png)

### Warstwy

Warstwy ułożone są od górnej - najbliższej użytkownikowi, do dolnej - najdalszej od UX

### Warstwy wyższe

* **Aplikacji (Application)**
    * Przeglądarka
    * Klient pocztowy
* **Prezentacji (Presentation)**
    * Działa na poziomie systemu operacyjnego (OS)
    * Konwertuje znaki zrozumiałe dla człowieka (litery i liczby) na ASCII
    * Odpowiada za
        * kodowanie i konwersję danych
        * kompresję / dekompresję
        * szyfrowanie / deszyfrowanie
    * Obsługuje np. MPEG, JPG, GIF
* **Sesji (Session)**
    * Odpowiada za:
        * Zapoczątkowanie połączenia, utrzymanie go i zakończenie
        * Właściwy kierunek przepływu danych

#### Warstwy niższe

* **Transportowa (Transport)**
    * Rozdziela dane na pakiety
    * Transportuje pakiety danych
    * Dostarcza pakiety w odpowiedniej kolejności
    * Protokoły: TCP i UDP
* **Sieciowa (Network)**
    * Determinuje najlepszą drogę dla danych (najszybszą i najbardziej odpowiednią drogę do adresu docelowego)
    * Protokoły: IPv4, IPv6
* **Łącza danych (Data Link)**
    * Nadzoruje przekazywanych informacji
    * Rozpoznaje i naprawia błędy
    * Karty sieciowe (NIC)
* **Fizyczna (Physical)**
    * Określa składniki sieci niezbędne do obsługi elektrycznego, optycznego, radiowego wysyłania i odbierania sygnałów
    * Kabel, światłowód

### Proces kapsułkowania (enkapsulacji)

Zmiana formatu danych podczas ich przesyłania\
![image](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536306614/Education/kapsulkowanie.png)

### Porównanie Modelu OSI do TCP/IP

![image](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536308472/Education/comparison-of-OSI-and-TCPIP.jpg)

## Sprzęt sieciowy (Network Hardware)

### Role

* W nowoczesnych sieciach komputer może być klientem, hostem lub pełnić obie role
* Software zainstalowany na danej maszynie determinuje jaką rolę odgrywa urządzenie

### Urządzenia

* **Modem**
    * Urządzenie, które pozwala podłączyć sieć do Internetu
    * Zmienia sygnały cyfrowe z routera na sygnały analogowe które mogą być rozsyłane po sieci
    * DOCSIS - zasady komunikacja dla modemów
* **Router**
    * Łączy sieci w całość (na przykład sieć domową z internetem)
* **Switch**
    * Posiada dużą ilość portów do podłączenia urządzeń do routera
* **Repeater (Extender)**
    * Wzmacniacz sygnału
    * Switche i routery działają także jako wzmacniacze sygnału

# 0️⃣1️⃣ System binarny

Bit = binary digit\
W systemie binarnym liczby są wielokrotnością 2 (1, 2, 4, 8, 16, 32, 64, 128, itd.)

### Tworzenie liczb w systemie binarnym 8 bitowym (liczby od 0 do 256)

##### Dla liczby 19

![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229379/Education/bianry_digits.png)
\<br />Suma liczb przy których mamy 1 daje 19\
Obliczanie możliwych wartości w danym systemie bitów\

* $2^x$ - dwa do potęgi x, gdzie x to ilość bitów
* $2^8$ = 156$$

##### Adresy IP

Adres identyfikujący użytkownika sieci. Składa się z oktetów (ocetet).\
Zapisywane są w systemie 32 bitowym: 4 oktety po 8 bitów = 32 bity\
![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229779/Education/ip_adress_01.png)

##### Subnet mask

Zawiera informację o rozmiarze sieci\
![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229779/Education/ip_adress_02.png)
1 oznaczają, że cyfra z adresu IP dotyczy sieci\
0 oznacza, że cyfra dotyczy hosta\
Sprawdzanie adresu IP sieci\
Potrzebujemy numer IP naszego komputera i maskę subnet\
Zestawiamy oba numery:\
![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229779/Education/ip_adress_03.png)\
Zamieniamy adresy na postać binarną i porównujemy je jeden pod drugim.\
Dwie jedynki oznaczają 1\
Jakiekolwiek 0 w górnym lub dolnym adresie oznacza 0\
![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229779/Education/ip_adress_04.png)\
Sprawdzamy ile jest wartości 1 w masce Subnet. Pozostałe bity to wartości zarezerwowane dla dla hostów w danej sieci.\
![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229779/Education/ip_adress_05.png)\
Cztery zera to 4 bity informacji.\
Ilość hostów w danej sieci: 2 do potęgi ilość wolnych bitów z maski subnet. 24 = 16\
Ilość hostów do wykorzystania = ilość hostów w danej sieci -2 (pierwszy dla adresu sieci, ostatni dla adresu broadcast)\
Maksymalny rozmiar ID sieci to 30 bitów (inaczej nie byłaby to sieć bo zawierałaby tylko 1 lub 0 komputerów)\
CIDR Notation\
Sposób zapisu adresu IP wraz z maską Subnet\
Po adresie IP wstawiamy / i podajemy ilość jedynek po których mają nastąpić zera. Powyższy przykład zapisany zostałby tak:\
169.174.141.10/28

# 📤Operacje

* PuTTy - wklejanie - SHIFT + INSERT; hasło nie będzie widoczne
    * Zmieniamy hasło
    * Tworzymy nowego użytkownika: adduser nazwa
    * Dajemy użytkownikowi przywileje administracyjne: gpasswd -a bucky sudo
* PuTTy Key Generator
    * Potrzebna jest para kluczy: prywatny i publiczny
    * Wybieramy typ klucza: SSH-2 RSA
    * Generujemy klucze
    * Zapisujemy klucze (do prywatnego warto dodać hasło)
* PuTTy
    * Zmieniamy użytkownika na nowo utworzonego: su - nazwa
    * Czyścimy ekran: clear
    * Tworzymy folder na klucze: mkdir .ssh
    * Nadajemy folderowi uprawnienia: chmod 700 .ssh
    * Uruchamiamy wbudowany edytor tekstu: nano .ssh/authorized_keys
    * Wklejamy klucz, wychodzimy i zapisujemy: CTRl + X (+ Yes)
    * Nadajemy plikowi uprawnienia: chmod 600 .ssh/authorized_keys
* Pageant
    * Dodajemy zapisane na dysku klucze
* Zmiana domyślnego portu SSH
    * Domyślne porty:
        * HTTP - 80
        * HTTPS - 443
        * PuTTy - 22 dla połączenie SSH z serwerem
    * PuTTy
        * Otwieramy plik konfiguracyjny SSH sudo nano /ect/ssh/sshd_config
        * Zmieniamy port na niestandardowy np 7777
        * Restartujemy usługę sudo service ssh restart
* Firewall
    * Warto ustawić filtrowanie po portach lub usługach
    * PuTTy
        * Umożliwiamy połączenie przez port 7777: sudo ufw 7777/tcp
        * Umożliwiamy połączenie przez port 80: sudo ufw 80/tcp
        * Umożliwiamy połączenie przez port 443: sudo ufw 443/tcp
        * Sprawdzamy dodane uprawnienia: sudo ufw show added
        * Włączamy firewall: sudo ufw enable
* Zmiana czasu serwera
    * PuTTy
        * Zmiana czasu serwera: sudo dkpg-reconfigue tzdata
* Instalacja LAMP
* LAMP - Linux, Apache, MySQL and PHP
* PuTTy
    * Aktualizujemy narzędzie do instalacji: sudo apt-get update
    * Instalujemy Apache: sudo apt-get install apache2
    * Instalujemy MySQL i PHP: sudo apt-get install mysql-server php5-mysql
    * Instalacja wersji php7: sudo apt-get install php php7.0-mysql
    * Sprawdzenie wersji PHP: sudo php7.0 -v
    * Instalujemy strukturę katalogów: sudo mysql\_install\_db
    * Instalacja skryptu który usuwa luki bezpieczeństwa: sudo mysql\_secure\_installation
    * Instalacja PHP: sudo apt-get install php5 libapache2-mod-php php5-mcrypt
    * Zmiana domyślnego pliku z index.html na index.php (edytujemy kolejność): sudo nano /ect/apache2/ mods-enabled/dir.conf
    * Restartujemy Apache: sudo service apache2 restart
    * Przeszukiwanie modułów: apt-cache search php5-
    * Sprawdzanie informacji o pakiecie: apt-cache show nazwa (php5-json)
    * Instalujemy pakiet JSON: sudo apt-get install php5-json
* Tworzenie strony do testów
    * PuTTy
        * Tworzymy plik index.php: sudo nano /var/www/html/index.php
        * Tworzymy plik z informacjami o PHP - phpinfo(): sudo nano /var/www/html/info.php
        * Usuwanie strony: sudo rm [ścieżka]
* Instalowanie phpMyAdmin
    * PuTTy
        * Instalowanie phpMyAdmin: sudo apt-get install phpmyadmin
        * Konfigurujemy phpMyAdmin
        * Włączamy pakiet encrypt: sudo php5enmod mcrypt
        * Kopiowanie plików do innej lokalizacji \(np gdy plik konfiguracyjny znajduje się w złym miejscu\): sudo cp \[plik kopiowany\]\[miejsce docelowe\]
            * sudo cp /ect/phpmyadmin/apache.conf /ect/apache2/conf-enabled/phpmyadmin.conf
        * Restartujemy apache: sudo service apache2 restart
* Zabezpieczanie phpMyAdmin
    * PuTTy:
        * Włączamy nadpisywanie domyślnych ustawień:
            * sudo nano /ect/apache2/conf-enabled/phpmyadmin.conf
    * W pliku dodajemy linijkę AllowOverride All
    * Restartujemy apache: sudo service apache2 restart
    * Tworzymy plik .htaccess: sudo nano /usr/share/phpmyadmin/.htaccess
    * Tworzymy podstawowe hasło do strony z phpMyAdmin:
        * AuthType Basic
        * AuthName “Restricted Files”
        * Auth UserFile etc/phpmyadmin/.htpasswd
        * Require valid-user
    * Instalujemy pakiet który pozwala na przekierowania: sudo apt-get install apache2-utils
    * Tworzymy plik .htpasswd: sudo htpasswd -c etc/phpmyadmin/.htpasswd [nazwausera]
* FileZilla + SFTP
    * Edycja > Ustawienia > SFTP > Dodaj prywatny klucz SSH z dysku
    * Plik > Menedżer stron > Dodajemy nowy wpis i podajemy: nazwę, adres, port, protokół SFTP, typ logowania: interaktywne

# 🔄 CISCO Networking

Rodzaje danych

* Volunteer data - dane udostępniane celowo (np. wiadomość na Facebooku)
* Inferred data - dane generowane przez nasze aktywności, niekoniecznie celowo (np. dane wygenerowane przy transakcji kartą debetową)
* Observed data - np. dane lokalizacyjne wysyłane do operatora telefonii komórkowej

**Throughput** \- przepustowość łącza \(jaka faktycznie ma miejsce\)\
**Bandwidth** \- przepustowość łącza \(maksymalna\)\.
Miary:

* Bits per second (b/s)
* Thousands of bits per second (kb/s)
* Millions of bits per second (Mb/s)
* Billions of bits per second (Gb/s)
* Trillions of bits per second (Tb/s)

![Cat](https://res.cloudinary.com/p1x3l0v4/image/upload/v1536229780/Education/network_definitions.png)

* The network infrastructure contains three categories of hardware components:
    * Intermediate devices
    * End devices
    * Network media