# JavaScript - Podstawy

## Umieszczenie JavaScript na stronach

Kod strony HTML czytany jest od góry do dołu. Skrypt uruchamiany jest w kolejności, w jakiej został umieszczony w kodzie.

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
    <meta charset="UTF-8" data-tomark-pass data-tomark-pass />
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
    <meta charset="UTF-8" data-tomark-pass data-tomark-pass />
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

Do znacznika `<script>` można dodać atrybuty `async` i `defer`

```html
<script src="..." defer></script>
<script src="..." async></script>
<script src="..." async defer></script>
```

- `async` - jeżeli przeglądarka czytając kod strony natrafi na plik ze skryptem zacznie go wczytywać w tle, równocześnie czytając dalszą część kodu strony. Jeżeli cały plik ze skryptem się wczyta, wtedy kod zostanie wykonany.
- `defer` - jeżeli przeglądarka czytając kod strony natrafi na plik ze skryptem zacznie go wczytywać w tle, równocześnie czytając dalszą część kodu strony. Jeżeli cały plik ze skryptem się wczyta, kod zostanie wykonany po załadowaniu całego dokumentu (ale tuż przed odpaleniem zdarzenia `DOMContentLoaded`).

Skrypty z atrybutem `defer` będą odpalane w kolejności w jakiej zostały wstawione do dokumentu. W przypadku `async` skrypty będą odpalane w kolejności "kto pierwszy ten lepszy", czyli który skrypt wczyta się wcześniej, ten zostanie wcześniej wykonany.

## Komentarze

W JavaScript istnieją 2 rodzaje komentarzy: komentarze zajmujące jedną i wiele linii

```javascript
/*
Przykład komentarza składającego się z wielu linii.
Taki komentarz może zawierać wiele linii.
*/

// To jest przykład komentarza 1-liniowego
```

## Strict mode

**Strict mode** \- funkcjonalność wprowadzona w `ES5 (EcmaScript 2009)`, która pozwala uruchamiać skrypty w bardziej restrykcyjnym trybie - tak zwanym `"strict mode"`. Tryb ten:

- eliminuje niektóre "ciche" błędy (takie, które nie są sygnalizowane przez przeglądarkę)
- sygnalizuje niebezpieczne operacje

Domyślnie tryb ten jest wyłączony. Aby go włączyć, na początku naszego kodu musimy użyć zapisu `"use strict"` lub `'use strict'`

```javascript
"use strict";

// Ten kod będzie działał w nowszym środowisku

```

Tryb `"strict mode"` możemy włączać dla całego kodu, ale i dla poszczególnych funkcji umieszczając go na ich początku

```javascript
// Kod bez strict-mode...

(function() {
  "use strict";
  // Kod działający na strict-mode
})();

// Kod bez strict-mode...
```

### Różnice między "strict mode" a normalnym kodem

**Błąd przy używaniu zmiennych bez ich zadeklarowania**

```javascript
test = 20;
console.log(test); // OK
```

```javascript
"use strict";
test = 20; // Error - test is not defined
console.log(test);
```

**Błąd przy pominięciu słów kluczowych przy pętlach**

```javascript
"use strict";

for (el of elements) { // Error - el is not defined
    ...
}

for (i=0; i<10; i++) {// Error - i is not defined
    ...
}
```

```javascript
"use strict";

for (const el of elements) { // OK
    ...
}

for (let i=0; i<10; i++) { // OK
    ...
}
```

- Sygnalizowanie błędu, przy próbie:
  - nadpisania właściwości obiektu, które oznaczone są jako nie do zapisu
  - nadpisania elementów, które nie nadają się do nadpisania np. zmienne tworzone za pomocą słowa `var`

```javascript
var top = "Nie wiem"; // window.top = "Nie wiem"
// Powyższy kod nie zadziała, bo window.top zawiera bardzo ważną informację o tym, jakie okno jest na samej górze hierarchii (np. ramek)
console.log(top); // window

// Inny przykład
NaN = 20;
console.log(NaN); // NaN
```

```javascript
"use strict";
top = "Nie wiem"; // Error: Cannot assign to read only property 'top' of object '#'

NaN = 20; // Error
console.log(NaN);
```

- Błąd przy próbie usunięcia funkcji, zmiennych czy argumentów

```javascript
function test() {}
let nr = 20;

delete test; // Error - Delete of an unqualified identifier
delete nr; // Error - Delete of an unqualified identifier

delete window.top; // error - Cannot delete property 'top' of #
```

- Błąd przy próbie użycia słów kluczowych jako nazw zmiennych

```javascript
var let = 20;
console.log(let); // 20
```

```javascript
"use strict";
var let = 20; // Unexpected strict mode reserved word
```

- Błąd przy powtórzeniu parametrów funkcji

```javascript
function test(a, a) {
  //ok
}
```

```javascript
"use strict";

function test(a, a) {
  // error - Duplicate parameter name not allowed in this context
}
```

- Błąd przy poprzedzaniu zmiennych typu `number` cyfrą `0`

```javascript
let nr = 020; // error : Octal literals are not allowed in strict mode.
```

- Funkcja `eval()` w trybie `"strict mode"` tworzy swój własny `scope` dla swoich zmiennych

```javascript
eval("var x = 20; console.log(x);");

var x = 10;
eval("var x = 20;");
console.log(x); // 20
```

```javascript
eval("var x = 20; console.log(x);");

var x = 10;
eval("var x = 20; console.log(x);"); // 20
console.log(x); // 10
```

- Błąd przy próbie wykorzystania instrukcji [`with`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/with)

## Typy danych

### Typy proste / prymitywne

- Dane typu prostego reprezentują proste typy danych - liczby, teksty, wartości boolowskie (prawda/fałsz), niezdefiniowane (`undefined`) oraz `null`.
- Zmienne typu prostego charakteryzują się tym, że ich wartości są przypisane bezpośrednio do zmiennych (są oddzielnymi bytami)

#### Number

Reprezentuje zmienne zmiennoprzecinkowe i stałoprzecinkowe

```javascript
var x = 50;
var x = 1.23;
```

```javascript
NaN == true; // false
NaN === true; // false
NaN == false; // false
NaN === false; // false
NaN == NaN; // false
Boolean(NaN) == false; // true
```

#### String

Ciąg znaków

```javascript
var x = "Ala";
var y = "50";
```

#### Boolean

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

Zamierzony brak wartości (brak referencji, wiemy, że obiekt nie istnieje)

```javascript
const myNul = null; // nic
```

```javascript
typeof null; // "object" (not "null" for legacy reasons)
typeof undefined; // "undefined"
null === undefined; // false
null == undefined; // true
null === null; // true
null == null; // true
undefined === undefined; // true
undefined == undefined; // true
!null; // true
!undefined; // true
isNaN(1 + null); // false
isNaN(1 + undefined); // true

Number(null); // 0
Number(undefined); // NaN
```

#### Symbol

- Każdorazowo przyjmuje całkowicie nową wartość, która zawsze jest unikatowa

```javascript
Symbol() === Symbol(); // false
```

- Możemy być utworzony za pomocą konstruktora, ale nie literału
- Mogą być użyte jako klucz właściwości obiektu
  - klucz właściwości (`property key`) to `symbol` lub `string`
  - nazwa właściwości (`property name`) to `string`

```javascript
const sym = Symbol();
console.log(typeof sym); // symbol

// Dla każdego symbolu możemy przekazać własną nazwę
// Która ułatwia debugowanie
const sym2 = Symbol("Moj symbol");
console.log(sym2); // Symbol(Moj symbol)
```

```javascript
// false bo oba symbole mają podobny tekst opisowy, ale ich "wartości" są całkowicie unikatowe
console.log(Symbol("foo") === Symbol("foo"));
```

#### Operacje na danych prostych

Podczas wykonywania operacji na typie prostym w tle dokonuje automatycznie tymczasowa konwersja typu prostego na obiekt, uruchamiana jest właściwość lub metoda, a następnie dana zmienna przywracana jest do typu prostego. Dzięki powyższej konwersji w JavaScript wszystko zachowuje się jak obiekt. Zasada ta nie dotyczy się tylko `undefined` i `null`, które nie potrzebują mieć właściwości i metod.

```javascript
const ourText = "Przykładowy tekst"; // Deklarujemy prostą zmienną
ourText.length; // JS poza sceną skonwertuje ourText na obiekt String, zwróci jego długość i przywróci zmienną do typu prostego

const nr = 23;
nr.toFixed(2); // Number został na chwilę zamieniony na obiekt, została użyta metoda toFixed po czym przywrócono go do typu prostego
```

### Typy złożone - Object

**Wszystkie zmienne nie będące typem prostym są obiektami i są typu referencyjnego.Ten typ danych charakteryzuje się tym, że zmienne nie mają przypisanej bezpośrednio wartości, a tylko wskazują na miejsce w pamięci, gdzie te dane są przetrzymywane.**

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1; // Zmienna arr2 wskazuje na tablicę [1, 2, 3]

arr1.push(4);
console.log(arr1); // 1, 2, 3, 4
console.log(arr2); // 1, 2, 3, 4

// Zmiana jednej zmiennej, powoduje zmieny w obu. Dzieje się tak ponieważ obie zmienne wskazują na ten sam obiekt.
```

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1.slice(); // Kopiuje całą tablicę za pomocą metody slice()

arr1.push(4);
console.log(arr1); // 1, 2, 3, 4
console.log(arr2); // 1, 2, 3
// Zmiany dokonywane są na kopii tablicy
```

## Zmienne

JavaScript należy do języków programowania które są dynamicznie typowane, oraz słabo typowane.

### Deklarowanie zmiennych

Aby zadeklarować zmienną, powinniśmy posłużyć się słowem kluczowym `var` lub `let` (_wprowadzone w ES6 (EcmaScript 2015)_)

```javascript
var x;
var y = 123;
var z = true;
var i = "Ala ma kota";
```

### Nazwy zmiennych/funkcji

- nazwa musi rozpoczynać się od: wielkiej litery, małej litery, podkreślenia
- nazwa nie może zaczynać się od: cyfry, spacji, myślnika
- nazwa nie może zawierać: spacji, kropki, przecinka, myślnika
- nazwa może zawierać: litery, cyfry, podkreślenia
- nazwą zmiennej nie może być słowo kluczowe zarezerwowane przez JavaScript

**Dobra praktyka:** Stosowanie istotnych znaczeniowo, angielskich nazw zmiennych z wykorzystaniem `camelCase`

## Stałe

**Stała** - po przypisaniu jej wartości nie może być zmieniana podczas wykonywania programu

Aby zadeklarować stałą, powinniśmy posłużyć się słowem kluczowym `const` (_wprowadzone w ES6 (EcmaScript 2015)_) lub `var`.

```javascript
const NR = 102; // stała
```

Dla raz stworzonej stałej `const`:

- nie możemy przypisać nowych wartości za pomocą `=`

  ```javascript
  const tab = [1, 2, 3];
  tab = [1, 2, 3, 4]; // błąd - przypisanie do stałej nowej tablicy
  ```

- możemy zmienić składową stałej

  ```javascript
  const tab = [1, 2, 3];
  tab[3] = 4; // nie ma błędu, zmiana składowej obiektu (tablicy)
  ```

**Częsta praktyka:** Tworzenie nazw stałych za pomocą samych wielkich liter

### Różnice między var a let/const

#### Zasięg zmiennych

- Zmienne deklarowane za pomocą `let` i `const` mają zasięg blokowy (od klamry do klamry)
- Zmienne deklarowane za pomocą `var` mają zasięg funkcyjny (ich zasięg określa ciało funkcji)

#### Ponowna deklaracja

- Niemożliwa przypadku `let` i `const`
- Możliwa w przypadku `var`

#### Różnice w hoistingu

- W przypadku `let` i `const` hoisting istnieje, ale nie jesteśmy w stanie używać zmiennych przed ich zadeklarowaniem

  ```javascript
  console.log(a); // Error: Cannot access 'a' before initialization

  let a = 20;
  ```

- W przypadku `var` hoisting pozwala używać zmiennych przed ich zadeklarowaniem

  ```javascript
  //  var a;
  // Hoisting wyniósł na początek kodu deklarację zmiennej ale bez jej wartości

  console.log(a); // Zwraca undefined (ale brak błędu)

  let a = 20;
  ```

#### Właściwość obiektu `Window`

- Deklaracja zmiennej globalnej (poza ciałem funkcji) za pomocą `let` lub `const` nie dodaje jej jako właściwości obiektu `Window`
- Deklaracja zmiennej globalnej za pomocą `var` powoduje dodanie jej jako właściwości obiektu `Window`

```javascript
var a = 20;
let b = 30;

console.log(window.a); // 20
console.log(window.b); // undefined
```

### Typowanie zmiennych / stałych (sprawdzanie typu)

```javascript
const num = 10;
const str = 'przykładowy tekst';
const arr = [];
const obj = {};
const nul = null;
// Zmiennej und specjalnie nie zadeklarowano

// Wypisujemy typy zmiennych
console.log( typeof num ); // "number"
console.log( typeof str ); // "string"
console.log( typeof arr ); // "object" (!)
console.log( typeof obj ); // "object"
console.log( typeof und ); // "undefined"
console.log( typeof nul ); // "object" (!)

// Sprawdzamy typy zmiennych
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
"kot" + "kot" // "kotkot"
20 + 1  // 21
"20" + 1  // "201"
"kot" + 20  // "kot20"
[1,2,3] + "kot" // 1,2,3kot, bo tablica została skonwertowana na 1,2,3
[] + "kot"  // "kot", bo tablica została skonwertowana na ""
[]  + []  // "", bo obie tablice zostały skonwertowane na "" czyli mamy "" + ""
[] + false  // "false"
23 + "" + false  // "23false"
"" + {}  // "[object Object]" bo obiekt został skonwertowany na zapis [object Object]
[1,2,3] + {}  // 1,2,3[object Object]
{} + {}  // [object Object][object Object]
"23" + [1,2,3] + {} + true + false + !true  // "231,2,3[object Object]truefalsefalse"
```

```javascript
23 + true; // 24, bo true zostało skonwertowane na 1
true + true + true; // 3
true + false; // 1, bo false zostało skonwertowane na 0
true + {}; // "true[object Object]" - konwersja true na 1 i tak by nic nie dała, bo 1 do obiektu nie da się dodać. Dlatego zostało skonwertowane na "true"
23 + 2 * []; // 23 - bo tablica została skownerowana na 0
```

<!-- prettier-ignore -->
```javascript
[] + []; // JavaScript zwraca "", TypeScript Error
{} + []; // JS : 0, TS Error
[] + {}; // JS : "[object Object]", TS Error
{} + {}; // JS : "[object Object][object Object]", TS Error
"hello" - 1; // JS : NaN, TS Error
```

### Manualna konwersja na liczby

```javascript
Number(str); // konwertuje tekst na liczbę
parseInt(str, system_liczbowy); // parsuje tekst na liczbę całkowitą
parseFloat(str); // parsuje tekst na liczbę
```

#### `parseInt(x, y)`

`x` konwertowany na `integer` (stałoprzecinkowa)
`y` określa system na jaki chcemy konwertować np. system `10`

#### `parseFloat(x, y)`

`x` konwertowany na `float` (zmiennoprzecinkowa)

`y` określa system na jaki chcemy konwertować np. system `10`

```javascript
console.log(Number("100")); // 100
console.log(Number("50.5")); // 50.5
console.log(Number("50px")); // NaN

console.log(parseInt("24px", 10)); // 24
console.log(parseInt("26.5", 10)); // 26
console.log(parseInt("100kot", 10)); // 100
console.log(parseInt("Ala102", 10)); // NaN - zaczyna się od liter
console.log(parseInt("Hello", 10)); // NaN

console.log("20px" + "20px"); // 20px20px
console.log(parseInt("20px", 10) + parseInt("20px", 10) + "px"); // 40px
```

Inne, mniej znane metody konwersji tekstu na liczby

```javascript
console.log(+"20"); // 20
console.log("20" * 1); // 20
console.log("20" / 1); // 20
console.log(~~"20"); // 20
```
