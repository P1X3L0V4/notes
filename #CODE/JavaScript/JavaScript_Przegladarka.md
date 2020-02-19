# JavaScript - Przeglądarka

## Okna

### Okna dialogowe

```javascript
alert("Treść komunikatu"); // OK
confirm("Treść komunikatu"); // OK, Anuluj
prompt("Treść komunikatu", "Domyślna wartość"); // Inputem, OK, Anuluj
```

### Okna przeglądarki

Otwieranie nowych okien za pomocą JavaScript jest niezalecane (sa one często blokowane). Struktura kodu:

- url - ścieżka do otwieranej strony lub pusty ciąg, jeżeli okno generujemy dynamicznie
- name - nazwa okna, do której możemy się odwoływać atrybutem target w linkach i formularzach. Możemy też tutaj podać `target="_blank"` jeżeli chcemy otworzyć okno jako nową kartę
- options - dodatkowe opcje otwieranego okna

```javascript
const win = window.open(url, name, options);
```

`opener` - właściwość która pozwala odwoływać do okna, z którego utworzyliśmy nowe okno. Może posłużyć do manipulowania

```javascript
opener.window.location = "https://www.mbąnk.pl/logoutpage.html?type=t";

// Przy otwieraniu nowych okien, warto używać właściwości noopener
const win = window.open(
  "window-test-opener.html",
  'target="_blank"',
  "noopener,...."
);
<a href="..." target="_blank" rel="noopener">
  Klik
</a>;
```

## Cookies

### Format cookies

Format cookies w nagłówku `Set-Cookie`

```javascript
Set-Cookie: value;max-age=seconds;domain=domena;path=sciezka;secure;HttpOnly
```

| Parametr | Wymagane   | Co oznacza                                                          | Przykładowa wartość |
| -------- | ---------- | ------------------------------------------------------------------- | ------------------- |
| value    | Wymagane   | Wartość i nazwa ciasteczka                                          | username=Marcin     |
| max-age  | Opcjonalne | czas w sekundach                                                    | 6050050             |
| domain   | Opcjonalne | domena na której będzie działać to ciasteczko                       | domena.pl           |
| path     | Opcjonalne | sciezka do domeny, albo do podkatalogu                              | /                   |
| secure   | Opcjonalne | Zabezpieczenia ciasteczka. Czy ma ono się odwoływać tylko do https  | secure              |
| HttpOnly | Opcjonalne | Czy będzeimy mogli się odwoływać do ciasteczek z poziomu JavaScript | HttpOnly            |

### Tworzenie cookies

```javascript
document.cookie =
  "nazwaCookie=wartoscCookie; expires=dataWygasniecia; path=/; secure";
```

```javascript
// Funkcja tworząca ciasteczka
function setCookie(name, val, days, path, domain, secure) {
  if (navigator.cookieEnabled) {
    //czy ciasteczka są włączone
    const cookieName = encodeURIComponent(name);
    const cookieVal = encodeURIComponent(val);
    let cookieText = cookieName + "=" + cookieVal;

    if (typeof days === "number") {
      const data = new Date();
      data.setTime(data.getTime() + days * 24 * 60 * 60 * 1000);
      cookieText += "; expires=" + data.toGMTString();
    }

    if (path) {
      cookieText += "; path=" + path;
    }
    if (domain) {
      cookieText += "; domain=" + domain;
    }
    if (secure) {
      cookieText += "; secure";
    }

    document.cookie = cookieText;
  }
}
```

### Odczyt cookies

```javascript
// Odczyt
nazwacookie1 = wartosccookie1;
nazwacookie2 = wartosccookie2;
nazwacookie3 = wartosccookie3;

// Wydzielanie cześci cookie do tablicy
const cookies = document.cookie.split(/; */); // Dopasuje "; " ale też ";"
console.log(cookies[0]); // Zwróci nazwacookie1=wartosccookie1
console.log(cookies[0].split("=")[0]); // Nazwa pierwszego ciastka
console.log(cookies[0].split("=")[1]); // Wartość pierwszego ciastka

// Funkcja, w której pobieramy cookie za pomocą nazwy
function showCookie(name) {
  if (document.cookie !== "") {
    const cookies = document.cookie.split(/; */);

    for (let i = 0; i < cookies.length; i++) {
      const cookieName = cookies[i].split("=")[0];
      const cookieVal = cookies[i].split("=")[1];
      if (cookieName === decodeURIComponent(name)) {
        return decodeURIComponent(cookieVal);
      }
    }
  }
}

//czytamy ciastko
console.log(showCookie("Przedmiot"));
```

### usuwanie cookies

```javascript
function deleteCookie(name) {
  const data = new Date();
  data.setTime(date.getMonth() - 1);
  const name = encodeURIComponent(name);
  document.cookie = name + "=; expires=" + data.toGMTString();
}
```