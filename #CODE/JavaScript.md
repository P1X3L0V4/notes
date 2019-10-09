# JavaScript

## Umieszczenie JavaScript na stronach

Kod strony HTML czytany jest od góry do dołu. Skrypt uruchamiany jest w takiej kolejności, w jakiej został umieszczony w kodzie HTML.

### Wstrzyknięcie kodu JavaScript bezpośrednio w tagi HTML

```html
<a onClick="alert('uwaga'); return= false;" href="http://www.eduweb.pl"></a>
```

### Umieszczanie kodu JavaScript w tagu `<script></script>`

Kod umieszczamy w sekcji `<head>` lub na końcu `<body>`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Odit quia
    aspernatur optio recusandae, atque, reiciendis tempore doloremque temporibus
    aliquid nemo vitae sint?

    <script>
      console.log("Nasz pierwszy skrypt!");
    </script>
  </body>
</html>
```

### Umieszczanie kodu JavaScript w pliku zewnętrznym `.js`

Plik podpisany do dokumentu w `<head>` lub `<body>`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Odit quia
    aspernatur optio recusandae, atque, reiciendis tempore doloremque temporibus
    aliquid nemo vitae sint?

    <script src="plik_ze_skryptem.js"></script>
  </body>
</html>
```

#### Atrybuty `async` i `defer`

Do znacznika script można dodać atrybuty `async` i `defer`

```html
<script src="..." defer></script>
<script src="..." async></script>
<script src="..." async defer></script>
```

- `async` - jeżeli przeglądarka czytając kod strony natrafi na plik ze skryptem zacznie go wczytywać w tle, równocześnie czytając dalszą część kodu strony. Jeżeli cały plik ze skryptem się wczyta, wtedy kod zostanie wykonany.

- `defer` jeżeli przeglądarka czytając kod strony natrafi na plik ze skryptem zacznie go wczytywać w tle, równocześnie czytając dalszą część kodu strony. Jeżeli cały plik ze skryptem się wczyta, kod zostanie wykonany po po załadowaniu całego dokumentu (ale tuż przed odpaleniem zdarzenia `DOMContentLoaded`).

Skrypty z atrybutem `defer` będą odpalane w kolejności w jakiej zostały wstawione do dokumentu. W przypadku `async` skrypty będą odpalane w kolejności "kto pierwszy ten lepszy", czyli który skrypt wczyta się wcześniej, ten zostanie wcześniej wykonany.

## Komentarze

W JavaScript istnieją 2 rodzaje komentarzy: komentarze zajmujące jedną i wiele linii

```javascript
/*
Przykład komentarza składającego się z wielu linii.
Taki komentarz może zawierać wiele linii.
*/
console.log("To jest mój pierwszy skrypt");

//To jest przykład komentarza 1-liniowego
console.log("To jest mój pierwszy skrypt");
```

```javascript
/*
Skrypt wypisujący różne rzeczy w konsoli
Wykorzystuje do tego celu console debugera
*/

console.log("To jest mój pierwszy skrypt"); //to jest pierwsza linia
console.log("To jest mój pierwszy skrypt"); //to jest druga linia
```

## Strict mode

**Strict mode** - funkcjonalność wprowadzona w `ES5 (EcmaScript 2009)`, która pozwala uruchamiać skrypty w bardziej restrykcyjnym trybie - tak zwanym `"strict mode"`. Tryb ten:

- eliminuje niektóre "ciche" błędy (takie, które nie są sygnalizowane przez przeglądarkę
- sygnalizuje niebezpieczne operacje
  Domyślnie tryb ten jest wyłączony. Aby go włączyć, na początku naszego kodu musimy użyć zapisu `"use strict"` lub `'use strict'`

```javascript
"use strict";

//ten kod będzie działał w nowszym środowisku

```

Tryb `"strict mode"` możemy włączać dla całego kodu, ale i dla poszczególnych funkcji umieszczając go na ich początku

```javascript
// kod bez strict-mode...

(function() {
  "use strict";
  // kod działający na strict-mode
})();

// kod bez strict-mode...
```

### Różnice między "strict mode" a normalnym kodem

- Błąd przy używaniu zmiennych bez ich zadeklarowania

  ```javascript
  test = 20;
  console.log(test); //ok
  ```

  ```javascript
  "use strict";
  test = 20; //error - test is not defined
  console.log(test);
  ```

- Błąd przy pominięciu słów kluczowych przy pętlach

  ```javascript
  "use strict";

  for (el of elements) { //error - el is not defined
      ...
  }

  for (i=0; i<10; i++) {//error - i is not defined
      ...
  }
  ```

  ```javascript
  "use strict";

  for (const el of elements) { //ok
      ...
  }

  for (let i=0; i<10; i++) {//ok
      ...
  }
  ```

- Sygnalizowanie błędu, przy próbie:

  - nadpisania właściwości obiektu, które oznaczone są jako nie do zapisu
  - nadpisania elementów, które nie nadają się do nadpisania np. zmienne tworzone za pomocą słowa `var`

  ```javascript
  var top = "Nie wiem"; //window.top = "Nie wiem"
  //powyższy kod nie zadziała, bo window.top zawiera bardzo ważną informację o tym, jakie okno jest na samej górze hierarchii (np. ramek)
  console.log(top); //window

  //inny przykład
  NaN = 20;
  console.log(NaN); //NaN
  ```

  ```javascript
  "use strict";
  top = "Nie wiem"; //error: Cannot assign to read only property 'top' of object '#'

  NaN = 20; //error
  console.log(NaN);
  ```

- Błąd przy próbie usunięcia funkcji, zmiennych czy argumentów

  ```javascript
  function test() {}
  let nr = 20;

  delete test; //error - Delete of an unqualified identifier
  delete nr; //error - Delete of an unqualified identifier

  delete window.top; //error - Cannot delete property 'top' of #
  ```

- Błąd przy próbie użycia słów kluczowych jako nazw zmiennych

  ```javascript
  var let = 20;
  console.log(let); //20
  ```

  ```javascript
  "use strict";
  var let = 20; //Unexpected strict mode reserved word
  ```

- Błąd przy powtórzeniu parametrów funkcji

  ```javascript
  function test(a, a) {
    //ok
  }
  ```

  ```javascript
  "use strict";

  function test(a, a) { //error - Duplicate parameter name not allowed in this context

  }
  ```

- Błąd przy poprzedzaniu zmiennych typu `number` cyfrą `0`

  ```javascript
  let nr = 020; //error : Octal literals are not allowed in strict mode.
  ```

- Funkcja `eval()` w trybie `"strict mode"` tworzy swój własny scope dla swoich zmiennych

  ```javascript
  eval("var x = 20; console.log(x);");

  var x = 10;
  eval("var x = 20;");
  console.log(x); //20
  ```

  ```javascript
  eval("var x = 20; console.log(x);");

  var x = 10;
  eval("var x = 20; console.log(x);"); //20
  console.log(x); //10
  ```

- Błąd przy próbie wykorzystania instrukcji [`with`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/with)

## Typy danych

### Typy proste / prymitywne

- Dane typu prostego reprezentują proste typy danych - liczby, teksty, wartości boolowskie (prawda/fałsz), niezdefiniowane (undefined) oraz null.
- Zmienne typu prostego charakteryzują się tym, że ich wartości są przypisane bezpośrednio do zmiennych (są oddzielnymi bytami)

#### number

Reprezentuje zmienne zmiennoprzecinkowe i stałoprzecinkowe

```javascript
var x = 50;
var x = 1.23;
```

#### string

Ciąg znaków

```javascript
var x = "Ala";
var y = "50";
```

#### boolean

Przyjmuje jedną z dwóch wartości: `true` lub `false`

```javascript
var x = true;
var y = false;
```

#### undefined

Zmienne niezdefiniowane bez wartości

```javascript
var x;
```

#### null

Typ do przypisywanie wartości "nic"

```javascript
const myNul = null; // nic
```

#### symbol

- Możemy być utworzony za pomocą konstruktora, ale nie literału
- Każdorazowo przyjmuje całkowicie nową wartość, która zawsze jest unikatowa

```javascript
const sym = Symbol();
console.log(typeof sym); //symbol

//dla każdego symbolu możemy przekazać własną nazwę
//która ułatwia debugowanie
const sym2 = Symbol("Moj symbol");
console.log(sym2); //Symbol(Moj symbol)
```

```javascript
//false bo oba symbole mają podobny tekst opisowy, ale ich "wartości" są całkowicie unikatowe
console.log(Symbol("foo") === Symbol("foo"));
```

#### Operacje na danych prostych

Podczas wykonywania operacji na typie prostym w tle dokonuje automatycznie tymczasowa konwersja typu prostego na obiekt, uruchamiana jest właściwość lub metoda, a następnie dana zmienna przywracana jest do typu prostego. Dzięki powyższej konwersji w JavaScript wszystko zachowuje się jak obiekt. Zasada ta nie dotyczy się tylko `undefined` i `null`, które nie potrzebują mieć właściwości i metod.

```javascript
const ourText = "Przykładowy tekst"; //deklarujemy prostą zmienną
ourText.length; //js poza sceną skonwertuje ourText na obiekt String, zwróci jego długość i przywróci zmienną do typu prostego

const nr = 23;
nr.toFixed(2); //znowu to samo działanie - numer został na chwilę zamieniony na obiekt, została użyta metoda toFixed po czym przywrócono go do typu prostego
```

### Typy złożone - Object

**Wszystkie zmienne nie będące typem prostym są obiektami i są typu referencyjnego.**
Ten typ danych charakteryzuje się tym, że **zmienne nie mają przypisanej bezpośrednio wartości, a tylko wskazują na miejsce w pamięci, gdzie te dane są przetrzymywane.**

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1; //zmienna arr2 wskazuje na tablicę [1, 2, 3]

arr1.push(4);
console.log(arr1); //1, 2, 3, 4
console.log(arr2); //1, 2, 3, 4

// Zmiana jednej zmiennej, powoduje zmieny w obu. Dzieje się tak ponieważ obie zmienne wskazują na ten sam obiekt.
```

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1.slice(); //kopiuje całą tablicę za pomocą metody slice()

arr1.push(4);
console.log(arr1); //1, 2, 3, 4
console.log(arr2); //1, 2, 3
// Zmiany dokonywane są na kopii tablicy
```

## Zmienne

JavaScript należy do języków programowania które są dynamicznie typowane, oraz słabo typowane.

### Tworzenie

- Podczas tworzenia należy korzystać ze znaku przypisania `=`
- Zapis y `= 123` bez `var` lub `let` może spowodować nadpisanie innych istniejących już zmiennych

```javascript
var x;
var y = 123;
var z = true;
var i = "Ala ma kota";
```

### Nazwy zmiennych/funkcji

- nazwa musi rozpoczynać się od: wielkiej litery, małej litery, podkreślenia
- nazwa nie może zaczynać się od: cyfry, spacji, myślnika
- w środku używać możemy: liter, cyfr, podkreślenia
- w środku nie możemy używać: myślnika

### Typowanie zmiennych (sprawdzanie typu zmiennej)

```javascript
const num = 10;
const str = 'przykładowy tekst';
const arr = [];
const obj = {};
const nul = null;
//zmiennej und specjalnie nie zadeklarowałem

//wypisujemy typy zmiennych
console.log( typeof num ); //"number"
console.log( typeof str ); //"string"
console.log( typeof arr ); //"object" hmm?
console.log( typeof obj ); //"object"
console.log( typeof und ); //"undefined"
console.log( typeof nul ); //"object" hmm?

//sprawdzamy typy zmiennych
if (typeof num === "number") {...}
if (typeof str === "string") {...}
if (Array.isArray(arr)) {...}
if (typeof obj === "object") {...}
if (typeof und === "undefined") {...}
if (nul === null) {...}
```

### Automatyczna konwersja typów

JavaScript nie wymaga od deklarowania typu zmiennych.
W wielu przypadkach następuje automatyczna konwersja danych danego typu na inny

```javascript
"kot" + "kot" //"kotkot"
20 + 1  //21
"20" + 1  //"201"
"kot" + 20  //"kot20"
[1,2,3] + "kot" //1,2,3kot, bo tablica została skonwertowana na 1,2,3
[] + "kot"  //"kot", bo tablica została skonwertowana na ""
[]  + []  //"", bo obie tablice zostały skonwertowane na "" czyli mamy "" + ""
[] + false  //"false"
23 + "" + false  //"23false"
"" + {}  //"[object Object]" bo obiekt został skonwertowany na zapis [object Object]
[1,2,3] + {}  //1,2,3[object Object]
{} + {}  //[object Object][object Object]
"23" + [1,2,3] + {} + true + false + !true  //"231,2,3[object Object]truefalsefalse"
```

```javascript
23 + true; //24, bo true zostało skonwertowane na 1
true + true + true; //3
true + false; //1, bo false zostało skonwertowane na 0
true + {}; //"true[object Object]" - konwersja true na 1 i tak by nic nie dała, bo 1 do obiektu nie da się dodać. Dlatego zostało skonwertowane na "true"
23 + 2 * []; //23 - bo tablica została skownerowana na 0
```

### Manualna konwersja na liczby

```javascript
Number(str); //konwertuje tekst na liczbę
parseInt(str, system_liczbowy); //parsuje tekst na liczbę całkowitą
parseFloat(str); //parsuje tekst na liczbę
```

#### parseInt(x, y)

`x` konwertowany na `integer` (stałoprzecinkowa)<br />
`y` określa system na jaki chcemy konwertować np. system `10`

#### parseFloat(x, y)

`x` konwertowany na `float` (zmiennoprzecinkowa)

`y` określa system na jaki chcemy konwertować np. system `10`

```javascript
console.log(Number("100")); //100
console.log(Number("50.5")); //50.5
console.log(Number("50px")); //NaN

console.log(parseInt("24px", 10)); //24
console.log(parseInt("26.5", 10)); //26
console.log(parseInt("100kot", 10)); //100
console.log(parseInt("Ala102", 10)); //NaN - zaczyna się od liter
console.log(parseInt("Hello", 10)); //NaN

console.log("20px" + "20px"); //20px20px
console.log(parseInt("20px", 10) + parseInt("20px", 10) + "px"); //40px
```

Inne, mniej znane metody konwersji tekstu na liczby

```javascript
console.log(+"20"); //20
console.log("20" * 1); //20
console.log("20" / 1); //20
console.log(~~"20"); //20
```

## Kontekst wykonania (Execution Context)

**Kontekst wykonania (Execution Context)** \- abstrakcyjny koncept środowiska w którym interpretowany i wykonywany jest kod JavaScript\. Za każdym razem gdy uruchamiamy kod JS\, dzieje się to w Execution Context\.
**Typy kontekstów wykonania**

- **Global Execution Context** \- globalny kontekst wykonania to domyślny kontekst wykonywania\, który obsługuje kod nie znajdujący się wewnątrz żadnej funkcji\. W programie JavaScript może byc wyłącznie jeden taki kontekst\.
- **Functional Execution Context** \- lokalny \(funkcyjny\) kontekst wykonania; za każdym razem gdy wykonywana jest funkcja\, tworzony jest nowy kontekst dla tej funkcji\. Każda funkcja posiada swój własny kontekst\.
- **Eval Function Execution Context** \- kod wykonywany wewnętrz funkcji `eval` posiada swój własny kontekst.

### Execution Stack

**Execution Stack** \- miejsce w którym przechowywane są konteksty wykonania\. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.

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

**1\. Creation Stage** \- etap uruchamiany w momencie gdy funkcja jest wywoływana lecz zanim zostanie wykonany kod\, który się w niej znajduje\. W trakcie ustalane są:

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

**2\. Activation / Execution Stage** \- etap pod czas którego przypisywana jest wartość do zmiennych\, referencji funkcji oraz interpretowany / wykonywany jest kod\.

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
**Zakres** \- system\, któego rola polega na określeniu gdzie i w jaki sposób zmienne mogą być onalezione\. Zmienne mogą być wyszukiwane na potrzeby:

- przypisania referencji (LHS - Left Hand Side look-up)
- zwrócenia wartości (RHS - Right Hand Side look-up)

|     LHS      |     |   RHS    |
| :----------: | :-: | :------: |
| `const name` | `=` | `"Anna"` |

### Zakres leksykalny

**Zakres dynamiczny** \- zakres określany w momencie wykonywania kodu\. Nie jest wykorzystywany w JavaScript
**Zakres leksykalny (Lexical Scope)** \- zakres określany w momencie definiowania kodu\, w czasie trwania fazy leksykalnej \(lexical time\)\. Jego strukturę określa informacja o tym gdzie definiowane są zmienne i bloki\.

- Poszczególne zakresy mogą być w sobie wyłącznie ściśle zagnieżdżone
- JavaScript szukając identyfikatora zmiennej zaczyna od zakresu w którym się znajduje a następnie przechodzi do zewnętrznego zakresu i tak aż do momentu gdy dojdzie do zakresu globalnego lub do momentu odnalezienia szukanej wartości.

**Lexing (Tokenizing)** \- pierwsza faza pracy kompilatora\, polegająca na interpretowaniu ciągu tekstu kodu źródłowego na zrozumiałe dla silnika tokeny np\. wyrażenie `const name = "Anna"` zostaje rozłożone na `["const", "name", "=", "Anna"]`
**Przysłonięcie (Shadow Ring)** \- identyfikator znajdujący się w wewnętrznym scopie przesłania identyfikator znajdujący się w zewnętrznym scopie\.
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
