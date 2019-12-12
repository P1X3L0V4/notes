# JavaScript

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

## Wyrażenia regularne (RegExp)

`RegExp(wyrażenie, flaga)` - obiekt, który przyjmuje 2 argumenty:

- wyrażenie, którym będziemy testować
- dodatkowe flagi

```javascript
const reg = new RegExp("pani?", "gi");
// lub
const reg = /pani?/gi;

var regexp = new RegExp("Ania"); // Konstrukcja wyrażeń regularnych
var regexp = /Ania/; // Alternatywna konstrukcja wyrażeń regularnych
var imie = "Ania"; // Ciąg do sprawdzenia
var regexp = /Ania/gim; // Ciąg z flagami i, g oraz m
```

### Metaznaki

- `^` - początek wzorca
- `$` - koniec wzorca
- `.` - dowolny znak oprócz znaku nowego wiersza
- `[...]` - dowolny z wymienionych znaków
- `[^...]` - dowolny z niewymienionych znaków
- `|` - dowolny z rozdzielonych znakiem ciągów
- `(...)` - zawężenie zasięgu
- `?` - zero lub jeden poprzedzający znak lub element
- `*` - zero lub więcej poprzedzających znaków lub elementów
- `+` - jeden lub więcej poprzedzających znaków lub elementów
- `{4}` - dokładnie 4 poprzedzające znaki lub elementy
- `{4,}`- 4 lub więcej poprzedzających znaków lub elementów
- `{2,4}` - od 2 do 4 poprzedzających znaków lub elementów
- `\` - ogólny znak zmiany znaczenia, różnie wykorzystywany

### Klasy znaków

**Klasa znaków** - część wzorca ujęta w nawiasy kwadratowe

- `\s` - znak spacji, tabulacji lub nowego wiersza
- `\S` - znak nie będący spacją, tabulacją lub znakiem nowego wiersza
- `\w` - każdy znak będący literą, cyfrą i znakiem `_`
- `\W` - każdy znak nie będący literą, cyfrą i znakiem `_`
- `\d` - każdy znak będący cyfrą
- `\D` - każdy znak nie będący cyfrą
- `[abc]` - oznacza jedną z liter a, b lub c
- `[a-z]` - dowolna mała litera
- `[a-zA-Z]` - dowolna litera
- `[ąćęłńóśżź]` - dowolna mała polska litera
- `[0-9\-+]` - dowolna cyfra lub znak + lub -, inaczej można zapisać `[\d\-+]`
- `[^0-9]` - dowolny znak nie będący cyfrą (to samo co `\D`), użyliśmy znaku `^` (zaprzeczenia logicznego klasy, musi być na pierwszej pozycji)

### Flagi

**flagi** - specjalne parametry, które oddziałują na wyszukiwanie wzorców

```javascript
const reg = /[a-z]*/gm;
const reg = new RegExp("[a-z]*", "g");
```

- `i` - powoduje niebranie pod uwagę wielkości liter
- `g` - powoduje zwracanie wszystkich pasujących fragmentów, a nie tylko pierwszego
- `m` - powoduje wyszukiwanie w tekście kilku liniowym. W trybie tym znak początku i końca wzorca `(^$`) jest wstawiany przed i po znaku nowej linii `(\n)`.

### Zastosowanie metody test()

`regexp.test(wyrazenie)` - metoda służąca do sprawdzania, czy dane wyrażenie znajduje się w tekście

```javascript
const text = "cat dog";
const reg = /cat/;
reg.test(text) === true;

const reg2 = /^cat$/;
alert(reg2.test(text)); // false - wzorzec zaczyna się z początkiem i kończy z końcem tekstu (znaki ^ i $) - jedyny pasujący tekst to "cat"
```

### Zastosowanie metody exec()

`regexp.excec(wyrazenie)` - metoda przeszukuje dany ciąg znaków, a następnie zwraca tablicę zawierającą składowe pierwszego wyszukanego fragmentu.

```javascript
const re = /d(b+)(d)/gi;
const result = re.exec("cdbBdbsbz");

console.log(result[0]); // dbBd
console.log(result.index); // 1
console.log(result.input); // cdbBdbsbz

console.log(re.lastIndex); // 5
console.log(re.multiline); // false
console.log(re.ignoreCase); // true
console.log(re.source); // d(b+)(d)
```

### Match()

Obiekt `String` posiada metodę `match()`, która spełnia tę samą funkcję co metoda `exec()` obiektu RexExp, jednak zwraca od razu wszystkie pasujące fragmenty.

```javascript
const text = "Numer1, Numer2, Numer3, NumerB, Numer5, NumerD";
const reg = /Numer[1-4A-C]/g;
console.log(text.match(reg)); //Numer1, Numer2, Numer3, NumerB
```

```javascript
const reg = /d(b+)(d)/gi;
const result = "cdbBdbsbz".match(reg);

if (result.length) {
  console.log(result.join("-")); //dbBd
}
```

### Zastosowanie metody search()

`regexp.search(wyrazenie)` - metoda obiektu `RexExp` działa tak samo jak metoda `indexOf()`obiektu string, czyli zwraca indeks pierwszego wystąpienia podciągu w ciągu

```javascript
const text = "Fantomas robi masę - marchewkowo-marcepanowa";
const reg = /at/gi";

console.log("Search: " + text.search(reg));
console.log("Index of: " + text.indexOf("at"));
```

### Zastosowanie metody replace()

Obiekt `String` posiada metodę `replace()`, która służy do zamiany jednego ciągu na drugi. Przy jej stosowaniu możemy używać wyrażeń regularnych.

```javascript
const text = "Super Samson jest fajny.";
const reg = /fajny/;
const textEnhanced = text.replace(reg, function(match) {
  return "super" + match;
});

console.log(textEnhanced); // Super Samson jest super fajny
```

## Kontekst wykonania (Execution Context)

**Kontekst wykonania (Execution Context)** - abstrakcyjny koncept środowiska w którym interpretowany i wykonywany jest kod JavaScript\. Za każdym razem gdy uruchamiamy kod JS, dzieje się to w Execution Context.

**Typy kontekstów wykonania**

- **Global Execution Context** - globalny kontekst wykonania to domyślny kontekst wykonywania\, który obsługuje kod nie znajdujący się wewnątrz żadnej funkcji. W programie JavaScript może byc wyłącznie jeden taki kontekst.
- **Functional Execution Context** - lokalny (funkcyjny) kontekst wykonania; za każdym razem gdy wykonywana jest funkcja\, tworzony jest nowy kontekst dla tej funkcji. Każda funkcja posiada swój własny kontekst.
- **Eval Function Execution Context** - kod wykonywany wewnętrz funkcji `eval` posiada swój własny kontekst.

### Execution Stack

**Execution Stack** - miejsce w którym przechowywane są konteksty wykonania\. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.

**Przykładowe dodawanie kontekstów do Execution Stack**

1. Global Context
2. First Function Context
3. Second Function Context

**Przykładowe usuwanie kontekstów z Execution Stack**

1. Second Function Context
2. First Function Context
3. Global Context

#### Execution Stack - informacje

- Jednocześnie może być wykonywany wyłącznie jeden stos (single threaded)
- Wykonywanie odbywa się synchronicznie
- Istnieje wyłącznie jeden globalny kontekst
- Może istnieć dowolna ilość functional execution context
- Każde wywołanie funkcji tworzy nowy kontekst (nawet gdy odwołuje się sama do siebie)

#### Tworzenie Execution Stack

**1. Creation Stage** - etap uruchamiany w momencie gdy funkcja jest wywoływana lecz zanim zostanie wykonany kod\, który się w niej znajduje. W trakcie ustalane są:

- Łańcuch zakresów (Scope Chain)
- Definicje zmiennych, funkcji i argumentów
- Określana jest wartość słowa kluczowego `this`

```javascript
// Global Execution Context - Creation
globalExecutionContext = {
  activationObj: {
    argumentObj: {
      length: 0
    },
    temp: "uninitialized",
    old: undefined,
    first: "Pointer to the function definition"
  },
  scopeChain: ["global execution context variable object"],
  this: "global object"
};
```

**2. Activation / Execution Stage** - etap pod czas którego przypisywana jest wartość do zmiennych\, referencji funkcji oraz interpretowany / wykonywany jest kod\.

```javascript
// Global Execution Context - Execution
globalExecutionContext = {
  activationObj: {
    argumentObj: {
      length: 0
    },
    temp: 10,
    old: 5,
    first: "Pointer to the function definition"
  },
  scopeChain: ["global execution context variable object"],
  this: "global object"
};
```

## Zakres

**Przechowywanie i zarządzanie zmiennymi**
Zarządzanie zmiennymi jest fundamentalną cechą języka programowania i wymaga złożonego systemu zasad. System ten nazywamy zakresem.
**Zakres** - system\, któego rola polega na określeniu gdzie i w jaki sposób zmienne mogą być onalezione. Zmienne mogą być wyszukiwane na potrzeby:

- przypisania referencji (LHS - Left Hand Side look-up)
- zwrócenia wartości (RHS - Right Hand Side look-up)

|     LHS      |     |   RHS    |
| :----------: | :-: | :------: |
| `const name` | `=` | `"Anna"` |

### Zakres leksykalny

**Zakres dynamiczny** - zakres określany w momencie wykonywania kodu\. Nie jest wykorzystywany w JavaScript
**Zakres leksykalny (Lexical Scope)** - zakres określany w momencie definiowania kodu\, w czasie trwania fazy leksykalnej (lexical time). Jego strukturę określa informacja o tym gdzie definiowane są zmienne i bloki.

- Poszczególne zakresy mogą być w sobie wyłącznie ściśle zagnieżdżone
- JavaScript szukając identyfikatora zmiennej zaczyna od zakresu w którym się znajduje a następnie przechodzi do zewnętrznego zakresu i tak aż do momentu gdy dojdzie do zakresu globalnego lub do momentu odnalezienia szukanej wartości.

**Lexing (Tokenizing)** - pierwsza faza pracy kompilatora, polegająca na interpretowaniu ciągu tekstu kodu źródłowego na zrozumiałe dla silnika tokeny np. wyrażenie `const name = "Anna"` zostaje rozłożone na `["const", "name", "=", "Anna"]`
**Przysłonięcie (Shadow Ring)** - identyfikator znajdujący się w wewnętrznym scopie przesłania identyfikator znajdujący się w zewnętrznym scopie.
Definiowanie zmiennej `glob` za pomocą słowa kluczowego `var` spowoduje dodanie tej zmiennej do obiektu globalnego `window` i umożliwi dostęp do wartości zmiennej poprzez `window.glob`

### Silnik, kompilator i zakres

Engine & Compilator & Scope

- Engine - odpowiedzialny za kompilację i wykonanie kodu
- Compiler - odpowiedzialny za parsowanie i przygotowanie kodu dla silnika
- Scope - odpowiedzialny za gromadzenie i zarządzanie zadeklarowanymi zmiennymi i tym, w jaki sposób te informacje dostepne są dla aktualnie wykonywanego kodu.

#### Przykład działania

`const name = "Anna"`

**Kompilator**

1. Na etapie tworzenia globalnego zakresu kompilator pyta zakres o zmienną o identyfikatorze `name`. Dochodzi do przeszukania zakresu w celu przypisania referencji (przypisanie referencji - LHS). Zmienna nie zostaje znaleziona.
2. Ponieważ zmienna nie została znaleziona zakres tworzy nowy identyfikator `name` w `activationObj` znajdującym się w `globalExecutionContext`. W przypadku słowa kluczowego `const` wartość początkowa zostaje ustawiona na `uninitialized` (dla `var` byłoby to `undefined`). Kompilator kończy swoje zadanie.

**Silnik JavaScript**

1. Silnik JavaScript wykorzystuje utworzony kontekst aby wykonać kod. W celu przypisania wartości do zmiennej ponownie przeszukiwany jest zakres (zwrócenie wartości - RHS).
2. Zakres stwierdza, że zawiera szukaną zmienną `name` i przypisuje do niej wartość `Anna`

### Obsługa błędów

- przypisania referencji (LHS - Left Hand Side look-up)
  - w trybie "non-strict" gdy zmienna nie została znaleziona, zadeklarowana zostanie nowa zmienna o poszukiwanym identyfikatorze
  - w trybie "strict mode" gdy zmienna nie została znaleziona, zwrócenony zostanie `Refrence Error`
- zwrócenia wartości (RHS - Right Hand Side look-up)
  - gdy zmienna nie została znaleziona, w zakresie wrzucony zostanie `Refrence Error`
  - gdy zmienna zostanie znaleziona w zakresie, ale operacja którą wykonujemy nie jest dozwolona (np. wywołanie zmiennej która nie jest funkcją czy odwołanie się do wartości `null` lub `undefined`) - zwrócony zostanie `Type Error`

## Dobre praktyki

- Samodzielne wstawianie średników na końcu linii (inaczej JavaScript wstawia je automatycznie co może dać niepożądane efekty)
- Uważać na to gdzie wstawiamy nową linię (znak powrotu karetki) np. w przupadku nowej linii po słowie `return` parser może automatycznie wstawić średnik i zakończyć działanie funkcji.
- Dodawać metody do `prototype` konstruktora obiektu. Wtedy dana metoda zajmuje w pamięci mniej miejsca niż gdyby była umieszczona w konstuktorze i kopiowana za każdym razem gdy tworzony jest nowy pusty obiekt danego typu.

## Właściwości JavaScript

- Dla każdego elementu z ID w strukturze strony tworzona jest zmienna o takiej samej nazwie, która wskazuje na dany element

```javascript
console.log(mainContent); // Nie stworzyliśmy nigdzie zmiennej mainContent, ale jeśli na stronie znajduje się element o takim id console.log zwróci go
```
