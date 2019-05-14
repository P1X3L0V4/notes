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
* **Load Balancer** \- Oddzielna maszyna\, która przekierowuje ruch z zapytań do jednej z kilku maszyn zawierających tę samą aplikację
    * \[Load Balancer\] \-\>\> \[Twitter\_01\]\[Twitter\_02\]\[Twitter\_03\] \(\-\>\> Wspólna baza danych\)

### Konfiguracja własnego serwera

* Gotowe rozwiązania
    * XAMPP - [https://www.apachefriends.org/](https://www.apachefriends.org/)
    * WAMPP - [http://www.wampserver.com/en/](http://www.wampserver.com/en/)

# 🔌 Sieć

**Sieć** \- zbiór urządzeń \(komputery\, telefony\, drukarki\, tablety itp\.\) podłączonych \(za pomocą kabla\, WIFI\, satelity itp\.\) do internetu; Celem sieci jest przesył danych
**Dane** (Data) - wszelkie informacje przesyłane wewnątrz sieci
**NIC** (Network Interface Card) - Karta sieciowa pozwalająca połączyć komputer z internetem. Składa się z dwóch elementów: wejścia do płyty głównej oraz wyjścia na kabel internetowy

### Typy sieci

Podział według zasięgu i rozmiaru:

* **LAN** \- Local Area Network \- Urządzenia w tym samym budynku
* **MAN** \- Metropolitan Area Network \- Zasięg miasta np\. Szpitale połączone we wspólną sieć
* **WAN** \- Wide Area Network \- Zasięg powyżej 30 mil / 48 km ===\> Internet

Networks installed in small offices, or homes and home offices, are referred to as Small Office Home Office (SOHO) networks