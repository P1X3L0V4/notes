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

Do znacznika script można dodać atrybuty `async` i `defer`

```html
<script src="..." defer></script>
<script src="..." async></script>
<script src="..." async defer></script>
```

- `async` \- jeżeli przeglądarka czytając kod strony natrafi na plik ze skryptem zacznie go wczytywać w tle\, równocześnie czytając dalszą część kodu strony\. Jeżeli cały plik ze skryptem się wczyta\, wtedy kod zostanie wykonany\.
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

// To jest przykład komentarza 1-liniowego
console.log("To jest mój pierwszy skrypt");
```

```javascript
/*
Skrypt wypisujący różne rzeczy w konsoli
Wykorzystuje do tego celu console debugera
*/

console.log("To jest mój pierwszy skrypt"); // to jest pierwsza linia
console.log("To jest mój pierwszy skrypt"); // to jest druga linia
```

## Strict mode

**Strict mode** \- funkcjonalność wprowadzona w `ES5 (EcmaScript 2009)`, która pozwala uruchamiać skrypty w bardziej restrykcyjnym trybie - tak zwanym `"strict mode"`. Tryb ten:

- eliminuje niektóre "ciche" błędy (takie, które nie są sygnalizowane przez przeglądarkę
- sygnalizuje niebezpieczne operacje
  Domyślnie tryb ten jest wyłączony. Aby go włączyć, na początku naszego kodu musimy użyć zapisu `"use strict"` lub `'use strict'`

```javascript
"use strict";

// ten kod będzie działał w nowszym środowisku

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
console.log(test); // ok
```

```javascript
"use strict";
test = 20; // error - test is not defined
console.log(test);
```

- Błąd przy pominięciu słów kluczowych przy pętlach

```javascript
"use strict";

for (el of elements) { // error - el is not defined
    ...
}

for (i=0; i<10; i++) {// error - i is not defined
    ...
}
```

```javascript
"use strict";

for (const el of elements) { // ok
    ...
}

for (let i=0; i<10; i++) { // ok
    ...
}
```

- Sygnalizowanie błędu, przy próbie:

```javascript
var top = "Nie wiem"; // window.top = "Nie wiem"
// powyższy kod nie zadziała, bo window.top zawiera bardzo ważną informację o tym, jakie okno jest na samej górze hierarchii (np. ramek)
console.log(top); // window

//inny przykład
NaN = 20;
console.log(NaN); // NaN
```

```javascript
"use strict";
top = "Nie wiem"; // error: Cannot assign to read only property 'top' of object '#'

NaN = 20; //error
console.log(NaN);
```

- nadpisania właściwości obiektu, które oznaczone są jako nie do zapisu
  - nadpisania elementów, które nie nadają się do nadpisania np. zmienne tworzone za pomocą słowa `var`
- Błąd przy próbie usunięcia funkcji, zmiennych czy argumentów

```javascript
function test() {}
let nr = 20;

delete test; // error - Delete of an unqualified identifier
delete nr; // error - Delete of an unqualified identifier

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

- Funkcja `eval()` w trybie `"strict mode"` tworzy swój własny scope dla swoich zmiennych

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
console.log(typeof sym); // symbol

// dla każdego symbolu możemy przekazać własną nazwę
// która ułatwia debugowanie
const sym2 = Symbol("Moj symbol");
console.log(sym2); //Symbol(Moj symbol)
```

```javascript
// false bo oba symbole mają podobny tekst opisowy, ale ich "wartości" są całkowicie unikatowe
console.log(Symbol("foo") === Symbol("foo"));
```

#### Operacje na danych prostych

Podczas wykonywania operacji na typie prostym w tle dokonuje automatycznie tymczasowa konwersja typu prostego na obiekt, uruchamiana jest właściwość lub metoda, a następnie dana zmienna przywracana jest do typu prostego. Dzięki powyższej konwersji w JavaScript wszystko zachowuje się jak obiekt. Zasada ta nie dotyczy się tylko `undefined` i `null`, które nie potrzebują mieć właściwości i metod.

```javascript
const ourText = "Przykładowy tekst"; // deklarujemy prostą zmienną
ourText.length; // js poza sceną skonwertuje ourText na obiekt String, zwróci jego długość i przywróci zmienną do typu prostego

const nr = 23;
nr.toFixed(2); // number został na chwilę zamieniony na obiekt, została użyta metoda toFixed po czym przywrócono go do typu prostego
```

### Typy złożone - Object

**Wszystkie zmienne nie będące typem prostym są obiektami i są typu referencyjnego.**
Ten typ danych charakteryzuje się tym, że **zmienne nie mają przypisanej bezpośrednio wartości, a tylko wskazują na miejsce w pamięci, gdzie te dane są przetrzymywane.**

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1; // zmienna arr2 wskazuje na tablicę [1, 2, 3]

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

**Częsta praktyka:** Tworzenie nazw zmiennych za pomocą wielkich liter

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
// zmiennej und specjalnie nie zadeklarowano

// wypisujemy typy zmiennych
console.log( typeof num ); // "number"
console.log( typeof str ); // "string"
console.log( typeof arr ); // "object" (!)
console.log( typeof obj ); // "object"
console.log( typeof und ); // "undefined"
console.log( typeof nul ); // "object" (!)

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

### Manualna konwersja na liczby

```javascript
Number(str); // konwertuje tekst na liczbę
parseInt(str, system_liczbowy); // parsuje tekst na liczbę całkowitą
parseFloat(str); // parsuje tekst na liczbę
```

#### parseInt(x, y)

`x` konwertowany na `integer` (stałoprzecinkowa)
`y` określa system na jaki chcemy konwertować np. system `10`

#### parseFloat(x, y)

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

## Operatory

### Opeeratory matematyczne

```javascript
Tabela dla y = 5
```

| Operator | Nazwa działania    | Równanie     | Wynik y | Wynik x  |
| -------- | ------------------ | ------------ | ------- | -------- |
| +        | Dodawanie          | x = y + 2    | y = 5   | x = 7    |
| -        | Odejmowanie        | x = y - 2    | y = 5   | x = 3    |
| \*       | Mnożenie           | x = y \* 2   | y = 5   | x = 10   |
| /        | Dzielenie          | x = y / 2    | y = 5   | x = 2.5  |
| %        | Reszta z dzielenia | x = y % 2    | y = 5   | x = 1    |
| \*\*     | Potęgowanie        | x = y \*\* y | y = 5   | x = 3125 |
| ++       | Inkrementacja      |              |         |          |
|          | Preinkrementacja   | x = ++y      | y = 6   | x = 6    |
|          | Postinkrementacja  | x = y++      | y = 6   | x = 5    |
| --       | Dekrementacja      |              |         |          |
|          | Predekrementacja   | x = --y      | y = 4   | x = 4    |
|          | Postdekrementacja  | x = y--      | y = 4   | x = 5    |

```javascript
x = 5;
y = x + 2; // y = 7
y = x - 1; // y = 4
y = x * 3; // y = 15
y = x / 2; // y = 2.5
y = x % 2; // 1 bo % oznacza resztę z dzielenia
x--; // to to samo co x = x - 1
x++; // to to samo co x = x + 1
y = x--; // y = 5, x = 4
y = --x; // y = 4, x = 4
y = 2 ** 4; // y = 16
```

### Operatory przypisania

**Operatory przypisania** - służą do przypisania do zmiennej jakiejś wartości np. pola obiektu itp.

```javascript
Tabela dla x = 10 i y = 5
```

| Operator | Przykład | Równoznaczne z | Wynik  |
| -------- | -------- | -------------- | ------ |
| =        | x = y    | x = y          | x = 5  |
| +=       | x += y   | x = x + y      | x = 15 |
| -=       | x -= y   | x = x - y      | x = 5  |
| \*=      | x \*= y  | x = x \* y     | x = 50 |
| /=       | x /= y   | x = x / y      | x = 2  |
| %=       | x %= y   | x = x % y      | x = 0  |

```javascript
let myVar = "Przykładowy tekst";
myVar += " który nie";
myVar += " zmieścił by się w jednej linijce";

let x = 10;
x -= 5;
```

### Operatory porównania

**Operatory porównania** - stosuje się w instrukcjach warunkowych. Służą one do porównywania lewej strony równania do prawej.

```javascript
Tabela dla x = 5
```

| Operator | Opis                   | Równanie  | Zwróci |
| -------- | ---------------------- | --------- | ------ |
| ==       | równe                  | x == 8    | false  |
| !=       | różne                  | x != 8    | true   |
| ===      | identyczność           | x === 5   | true   |
|          |                        | x === "5" | false  |
| !==      | nieidentyczność        | x !== "5" | true   |
|          |                        | x === 5   | false  |
| >        | większe od             | x > 8     | false  |
| <        | mniejsze od            | x < 8     | true   |
| >=       | większe bądź równe od  | x >= 8    | false  |
| <=       | mniejsze bądź równe od | x <= 8    | true   |

- **Operator równości** - sprawdza czy zmienne mają tę samą wartość
- **Operator identyczności** - sprawdza czy zmienne mają tę samą wartość i typ

```javascript
const myVar = 8;
if (myVar === 10) {
  // ten kawałek kodu się nie wykona
}

if (myVar <= 10) {
  // ten kawałek kodu się wykona
}

if (myVar !== 8) {
  // ten kawałek kodu się nie wykona
}
```

#### Ciekawe przypadki relacji

```javascript
true == "1"; // true
0 == false; // true
null == undefined; // true
NaN == NaN; // false
```

### Operatory logiczne

**Operatory logiczne** - pozwalają łączyć kilka porównań w jedną całość

```javascript
Tabela dla x = 6 i y = 3
```

| Operator | Nazwa                              | Opis                                    | Przykład            | Wynik                                                       |
| -------- | ---------------------------------- | --------------------------------------- | ------------------- | ----------------------------------------------------------- |
| &&       | Koniunkcja<br />(iloczyn logiczny) | and (i)                                 | (x < 10 && y > 1)   | Prawda, bo x jest mniejsze od 10 i y jest większe od 1      |
| \|\|     | Alternatywa<br />(suma logiczna)   | or (lub)                                | (x > 8 \|\| y > 1)  | Prawda, bo x nie jest większe od 8, ale y jest większe od 1 |
| ^        | Albo                               | xor (jeden z, ale nie dwa równocześnie) | (x === 6 ^ y === 3) | Fałsz, bo obydwa są prawdziwe                               |
| \!       | Negacja                            | not (negacja)                           | \!(x === y)         | Prawda, bo negujemy to, że x === y                          |

- **Koniunkcja** - Wyrażenie jest prawdziwe jeżeli pierwszy i drugi warunek jest spełniony
- **Alternatywa** - Wyrażenie jest prawdziwe jeżeli pierwszy lub drugi warunek jest spełniony
- **Albo** - Wyrażenie jest prawdziwe jeżeli pierwszy lub drugi warunek jest spełniony, ale nie oba na raz
- **Negacja** - Zmienia wartość wyrażenia na przeciwną

```javascript
const myVar = 8;
const myVar2 = 15;

if (myVar === 8 && myVar2 === 10) {
  // ten kawałek kodu się nie wykona bo mamy "i", oba muszą być spełnione, a nie są
}

if (myVar === 8 || myVar2 === 8) {
  // ten kawałek się wykona bo mamy "lub" - jeden z warunków jest poprawny
}

if ((myVar === 8) ^ (myVar2 === 15)) {
  // ten kawałek się nie wykona bo mamy "xor", a oba są spełnione
}

if (!(myVar === 8)) {
  // ten kawałek się nie wykona, bo mamy negację!
  // powyższy warunek jest jednoznaczny z myVar !== 8
}

if (myVar === 2 || 1) {
  // ten kawałek zawsze się wykona, bo myVar nie jest 2,
  // ale drugi fragment warunku zawsze zwróci true (1 jest rzutowana na true)
}
```

#### Wyrażenia fałszywe w JavaScript

```javascript
false;
0;
("");
null;
undefined;
NaN;
```

## Obiekt Math()

**Obiekt Math()** -obiekt udostępniany przez Javascript, ułatwiający przeprowadzanie operacji matematycznych.

### Właściwości Math()

| Nazwa        | Zwraca                                                   | Wartość            |
| ------------ | -------------------------------------------------------- | ------------------ |
| Math.E       | Zwraca stałą Eulera, która wynosi ok. 2.71               | 2.718281828459045  |
| Math.LN2     | Zwraca logarytm dwóch, tj. ok. 0.69                      | 0.6931471805599453 |
| Math.LN10    | Zwraca logarytm z dziesięciu, tj. ok. 2.30               | 2.302585092994046  |
| Math.LOG2E   | Zwraca logarytm o podstawie 2 z liczby E, czyli ok. 1.44 | 1.4426950408889634 |
| Math.LOG10E  | Zwraca logarytm o podstawie 10 z E, czyli ok. 0.43       | 0.4342944819032518 |
| Math.PI      | Zwraca wartość liczby Pi, czyli ok. 3.14                 | 3.141592653589793  |
| Math.SQRT1_2 | Zwraca pierwiastek kwadratowy z 0.5, czyli ok. 0.70      | 0.7071067811865476 |
| Math.SQRT2   | Zwraca pierwiastek kwadratowy z 2, czyli ok. 1.41        | 1.4142135623730951 |

### Metody Math()

| Nazwa                      | Zwraca                                                                 |
| -------------------------- | ---------------------------------------------------------------------- |
| Math.abs(liczba)           | Zwraca wartość absolutną liczby                                        |
| Math.acos(liczba)          | Zwraca arcus cosinus z liczby (podanej w radianach)                    |
| Math.asin(liczba)          | Zwraca arcus sinus z liczby (podanej w radianach)                      |
| Math.atan(liczba)          | Zwraca arcus tangens z liczby (podanej w radianach)                    |
| Math.ceil(liczba)          | Zwraca najmniejszą liczbę całkowitą, większą lub równą podanej liczbie |
| Math.cos(liczba)           | Zwraca cosinus liczby (podanej w radianach)                            |
| Math.exp(liczba)           | Zwraca wartość E podniesionej do potęgi wyrażonej podanym argumentem   |
| Math.floor(liczba)         | Zwraca największą liczbę całkowitą mniejszą lub równą podanej liczbie  |
| Math.log(liczba)           | Zwraca logarytm naturalny liczby                                       |
| Math.max(liczba1, liczba2) | Zwraca większą z dwóch liczb                                           |
| Math.min(liczba1, liczba2) | Zwraca mniejszą z dwóch liczb                                          |
| Math.pow(liczba1, liczba2) | Zwraca wartość liczby1 podniesionej do potęgi liczby 2                 |
| Math.random()              | Zwraca wartość pseudolosową z przedziału 0 - 1                         |
| Math.round(liczba)         | Zwraca zaokrąglenie danej liczby do najbliższej liczby całkowitej      |
| Math.sin(liczba)           | Zwraca sinus liczby (podanej w radianach)                              |
| Math.sqrt(liczba)          | Zwraca pierwiastek kwadratowy liczby                                   |
| Math.tan(liczba)           | Zwraca tangens liczby (podanej w radianach)                            |

Przykłady zastosowania obiektu `Math()`

```javascript
const var1 = 56.5;
const var2 = 74.3;

Math.min(var1, var2) // 56.5
Math.max(var1, var2)) // 74.3
Math.max(1,3,6,2) // 6

Math.cos(0) // 1
Math.abs(-1) // 1

Math.round(var1) // 56
Math.round(20.52) // 21
Math.round(-10.21) // -10
Math.round(-11.82) // -12

Math.floor(var1) // 56
Math.floor(20.52) // 20
Math.floor(-10.21) // -11
Math.floor(-11.82) // -12

Math.ceil(var1) // 57
Math.ceil(20.52) // 21
Math.ceil(-10.21) // -10
Math.ceil(-11.82) // -11
```

## String

**String** - prosty typ danych w postaci ciągu znaków

### Tworzenie stringów

```javascript
const text = "Ala ma kota, a kot ma Ale."; // podwójne cudzysłowy
const text = "Ala ma kota"; // pojedyncze apostrofy
const text = `Ala ma kota`; // backticki (template strings)
```

Stringi można zapisywać:

- przy użyciu cudzsłowów
- przy użyciu apostrofów
- przy wykorzystaniu backticków
- przy wymiennym użyciu cudzsłowów i apostrofów lub skorzystać ze znaku ucieczki

<!-- prettier-ignore -->
```javascript
// Wykorzystanie wymienności
const img = '<div class="element" data-text="test">';
const txt = "It's a big year";

// Wykorzystanie znaku ucieczki
const img = "<div class=\"element\" data-text=\"test\">";
const txt = 'It\'s a big year';
```

Do tworzenia zmiennych typu string możemy użyć konstruktora by uzyskać obiekt. Nie zaleca się tej praktyki, ponieważ obiekty są typem referencyjnym i przy operacjach możemy dostawać wyniki niezgodne z oczekiwaniami.

```javascript
//Deklaracja za pomocą literału
const text1 = "abc";
const text2 = "abc";
console.log(text1 === text2); // true

// Deklaracja za pomocą konstruktora
const text1 = new String("abc");
const text2 = new String("abc");
console.log(text1 === text2); // false, ponieważ porównujemy 2 obiekty, a nie wartości
console.log(typeof text1); // object
```

### Stringi wieloliniowe

```javascript
// Poprzez operator przypisania
let text = '';
text += 'Stoi na stacji lokomotywa,<br>';
text += 'Ciężka, ogromna i pot z niej spływa:<br>';
text += 'Tłusta oliwa.';

// Poprzez dodawanie kolejnych części tekstu
let text = ''
+ 'Stoi na stacji lokomotywa,<br>'
+ 'Ciężka, ogromna i pot z niej spływa:<br>'
+ 'Tłusta oliwa.'

// Poprzez zastosowanie znaku backslash na końcu linii
let text = '\n
Stoi na stacji lokomotywa,<br>\
Ciężka, ogromna i pot z niej spływa:<br>\
Tłusta oliwa.\
'

// Najlepsza metoda - użycie template strings
let text = `
Stoi na stacji lokomotywa,<br>
Ciężka, ogromna i pot z niej spływa:<br>
Tłusta oliwa.
`
```

### Konkatenacja ciągów

**Konkatenacja ciągów** - łączenie ciągów w jedną całość

Jeżeli w zapisie znajdują się łańcuchy znaków (stringi) to plus zmienia swoją logikę i jest to konkatenacja.

```javascript
const age = 10;
const text = "Ten pies ma " + age + " lat";
const text = "Ten kot ma " + age + " lat";
const text = `Ten chomik ma ${age} lat`;
```

<!-- prettier-ignore -->
```javascript
const a = 112;
const b = 120;

const text = "Cena produktu A to " + a + "zł, cena produktu B to " + b + "zł, a suma to " + (a+b)+ "zł";
const text = `Cena produktu A to ${a}zł, cena produktu B to ${b}zł, a suma to ${a+b}zł`;
```

### Właściwości i metody stringów

| Typ | Nazwa                  | Zwraca                                                                          |
| --- | ---------------------- | ------------------------------------------------------------------------------- |
| M   | charAt()               | Znak znajdujący się w ciągu na podanej pozycji                                  |
| M   | charCodeAt()           | Kod (Unicode) dla wskazanego znaku                                              |
| M   | concat(str2)           | Zwraca połączonie stringu z `str2`                                              |
| M   | endsWith()             | `true`/`false` w zależności od tego czy ciąg został znaleziony na końcu stringa |
| M   | fromCharCode()         | Zwraca łańcuch znaków stworzony przez podaną sekwencję kodów Unicode            |
| M   | includes()             | `true`/`false` w zależności od tego czy ciąg został znaleziony                  |
| M   | indexOf()              | Pozycję szukanego ciągu znaków w stringu (-1 = brak)                            |
| M   | lastIndexOf()          | Numer ostatniego wystąpienia ciągu                                              |
| P   | lenght                 | Długość stringa                                                                 |
| M   | localeCompare()        |                                                                                 |
| M   | match()                |                                                                                 |
| M   | repeat(num)            | Powtarza ciąg `num` razy                                                        |
| M   | replace(szukany, nowy) | String, w którym ciąg `szukany` zostaje zamieniony na `nowy`                    |
| M   | search()               |                                                                                 |
| M   | slice(start, stop)     | Nowy string od znaku `start` do `stop` włącznie lub do końca                    |
| M   | split(znak, dlugosc)   | Tablicę rozdzielając string na podstawie `znak`                                 |
| M   | startsWith()           |                                                                                 |
| M   | substr(start, dlugosc) | Ciąg znaków od znaku `start` o wskazanej `dlugosc` lub do końca                 |
| M   | substring(start, stop) | Ciąg znaków od znaku `start` do `stop` włącznie lub do końca                    |
| M   | toLocaleLowerCase()    | Treść stringu małymi literami według lokalnego?                                 |
| M   | toLocaleUpperCase()    | Treść stringu wielkimi literami według lokalne?                                 |
| M   | toLowerCase()          | Treść stringu małymi literami                                                   |
| M   | toString()             | Zwraca wartość obiektu string                                                   |
| M   | toUpperCase()          | Treść stringu wielkimi literami                                                 |
| M   | trim()                 |                                                                                 |
| M   | valueOf()              |                                                                                 |

## Instrukcje warunkowe

### if

Instrukcja if sprawdza dany warunek, i w zależności czy jest on równy true lub false wykona lub nie wykona sekcję kodu zawartą w klamrach:

```javascript
if (warunek) {
    ...instrukcje jeżeli warunek jest spełniony
}

// Przykłady:

const x = 1;
if (x === 1) { //warunek się wykona
    console.log('Liczba równa się 1');
}

const x = 2;
if (x !== 2) { //kod się nie wykona, bo x = 2
    console.log("Liczba " +x+ "jest różna od 2");
}
```

Wartości `false` dla warunku if:

```javascript
if (false)
if (null)
if (undefined)
if (0)
if (NaN)
if ('')
if ("")
if (document.all)
```

### else

Do podstawowego warunku if dodaje kod wykonywany w wypadku gdy warunek nie został spełniony

```javascript
const x = 5;

if (x === 1) {
  console.log("Liczba równa się 1");
} else {
  console.log("Liczba nie równa się 1");
}
```

### else if

Dodaje klilka sprawdzeń warunkowych

```javascript
const x = 5;

if (x > 5) {
  console.log("Liczba jest większa od 5");
} else if (x < 5) {
  console.log("Liczba jest mniejsza od 5");
} else {
  console.log("Liczba równa się 5");
}
```

### Operator warunkowy

Skórcona wersja warunku if

```javascript
const x = wyrażenie
  ? zwróć_jeżeli_wyrażenie_true
  : zwróć_jeżeli_wyrażenie_false;
```

```javascript
const i = 1;
let number = "";

if (i > 0) {
  number = "dodatnia";
} else {
  number = "ujemna";
}

// Zapis z pomocą operatora warunkowego
const number = i > 0 ? "dodatnia" : "ujemna";
```

```javascript
// Przykłady
const x = 3;
console.log(x % 2 === 0 ? "parzysta" : "nieparzysta");
// Zwraca 'nieparzysta'

const wiek = 21;
const status = wiek < 18 ? "jesteś za młody" : "zapraszamy na seans";
// Zwraca 'zapraszamy na seans'

const name = "Ola";
console.log(name === "Ola" ? "Masz na imię Ola" : "Nie masz na imię Ola");
// Zwraca 'Masz na imię Ola'

const someValue = user === "admin" ? true : false;

const answer = x === 2 ? "yes" : "no";

const isMember = true;
console.log("The fee is " + (isMember ? "$2.00" : "$10.00"));
```

### switch

```javascript
switch (wyrażenie) {
  case przypadek1:
    // Fragment kodu wykonywany gdy rezultat wyrażenia jest równy przypadek1 - potrzebuje break;
    break;
  case przypadek2:
    // Fragment kodu wykonywany gdy rezultat wyrażenia jest równy przypadek2 - potrzebuje break;
    break;
  default:
  // Fragment kodu wykonywany gdy powyższe rezultaty nie są równe rezultatowi wyrażenia - nie potrzebuje break;
}
```

Każdy przypadek kończy się słowem break, która kończy wykonywanie instrukcji switch.
Jeżeli pominiemy to słowo, wtedy nawet przy pomyślnym przyrównaniu zostaną wykonane kolejne sprawdzenia, co często może powodować błędy.

```javascript
const number = 4;
//Warunek zwróci "Numer równa się cztery"
switch (number) {
  case 1:
    console.log("Numer równa się jeden");
    break;
  case 2:
    console.log("Numer równa się dwa");
    break;
  case 3:
    console.log("Numer równa się trzy");
    break;
  case 4:
    console.log("Numer równa się cztery");
    break;
  default:
    console.log("Nie wiem ile równa się numer");
}
```

## Pętle

### Pętla typu for

```javascript
for (zainicjowanie_licznika;  warunek_kończący_wykonywanie_pętli;  zmiana_licznika) {
    kod który zostanie wykonany pewną ilość razy
}
```

```javascript
for (let i = 0; i < 10; i++) {
  console.log(i);
}

let sum = 0;
for (let i = 0; i < 10; i++) {
  sum += i;
}
console.log(sum); // Zwróci 45
```

### Pętla typu while

```javascript
while (wyrażenie-sprawdzające-zakończenie-pętli) {
    ...fragment kodu który będzie powtarzany...
}
```

```javascript
let i = 1;

while (i <= 100) {
  console.log("Nie będę...");
  i++;
}
```

#### do while

```javascript
let i = 0;

do {
  i++;
  console.log(i);
} while (false);
```

Warunek od początku nie spełniony ale i tak wykona się 1 raz (najpierw wykonywane jest do a potem sprawdzany warunek)

### Pętla for of

W wersji ES6 wprowadzono pętlę for of, która służy do iterowania po zmiennych iterowalnych (stringi, kolekcje, tablice itp).

```javascript
const tab = [1, 2, 3, 4];

for (const el of tab) {
  console.log(el);
}

const buttons = document.querySelectorAll("button");
for (const btn of buttons) {
  console.log(btn);
}

const txt = "ALa ma kota";
for (const letter of txt) {
  console.log(letter.toUpperCase());
}
```

### Instrukcje break i continue

**break** - kończy wykonywanie pętli

```javascript
const tab = ["Ala", "Monika", "Beata", "Karol"];

let userExist = false;

for (let i = 0; i < tab.length; i++) {
  if (tab[i] === "Beata") {
    userExist = true;
    break; // Dalej nie ma sensu sprawdzać
  }
}
```

**continue** - powoduje przerwanie danej iteracji (aktualnego powtórzenia)

```javascript
const tab = ["Ala", "Monika", "Beata", "Karol", "Alicja"];

for (let i = 0; i < tab.length; i++) {
  if (tab[i] === "Karol") {
    continue; // Karola pomiń
  }
  console.log(tab[i]);
}
```

## Funkcje

### Tworzenie funkcji

```javascript

// Deklaracja
function myFunc() {
    ...
}

// Wyrażenie funkcyjne (funkcja anonimowa)
const myFunc = function() {
    ...
}

// Funkcja strzałkowa (wyrażenie funkcyjne)
const myFunction = () => {
    console.log(a, b);
}

// Immediately-invoked function expression (IIFE)
(function() {
    console.log('Jakiś tekst'); //wywoła się od razu
})();

// Funkcja zwrotna (callback)
element.addEventListener('click', function() {
    ...
});
```

```javascript
nazwaFunkcji(); // Wywołanie
```

### arguments

**arguments** - obiekt zawierający wszystkie argumenty funkcji

```javascript
function sum() {
  console.log(arguments);
}

sum(1, 2, 3, 4); //[1, 2, 3, 4]
sum("ala", "ma", "kota"); // ["ala", "ma", "kota"]
```

### Operator rest

**rest** - operator zawierający wszystkie argumenty funkcji w postaci tablicy

```javascript
function superSum(...args) {
  console.log(args);
  [1, 2, 3, 4];
}
superSum(1, 2, 3, 4);
```

```javascript
function superSum(...args) {
  let result = args.reduce(function(a, b) {
    return a + b;
  });

  console.log(result);
}

superSum(1, 2, 3, 4);
```

### Domyślne wartości dla parametrów

W ES6 wprowadzono domyślne wartości dla parametrów

```javascript
function print(name = "Marcin", status = "najlepszy") {
  console.log(name + " jest " + status);
}

print(); // "Marcin jest najlepszy"
print("Karol"); // "Karol jest najlepszy"
print("Marcin", "głupi"); // "Marcin jest głupi"
```

### Instrukcja return

**return** - kończy działanie funkcji i zwraca wykonanie kodu po słowie kluczowym

### Funkcja strzłkowa

Wprowadzony w ES6 sposób zapisy, który zmienia słowo kluczowe function na strzałkę (fat arrow)

```javascript
// Jeżeli funkcja nie ma parametrów, dajemy nawiasy i strzałkę (fat arrow)
const myF = function() { ... }
const myF = () => { ... }

// Jeżeli funkcja wymaga tylko jednego parametru pomijamy nawiasy
const myF = function(a) { ... }
const myF = a => { ... }

// Jeżeli funkcja wymaga większej ilości parametrów, dajemy nawiasy
const myF = function(a, b) { ... }
const myF = (a, b) => { ... }

// Jeżeli funkcja zwraca tylko jedną instrukcję możemy pominąć klamry
const myF = function(a) { console.log(a); }
const myF = a => console.log(a);

// Jeżeli funkcja tylko coś zwraca, możemy pominąć instrukcję return
const myF = function(a) { return a * a; }
const myF = a => a * a;
```

## Tablice

_Tablica_ - zbiór danych indeksowany numerycznie

### Tworzenie tablic

```javascript
// Przy użyciu nawiasów kwadratowych
const tab = [];
const tab2 = [1, 2, 3, 4];
const tab3 = ["Marcin", "Ania", "Agnieszka"];

// Przy użyciu konstruktora
const tab = new Array(10, "Ala", "Bala", "Cala");
console.log(tab); //["Ala", "Bala", "Cala", blank x 7]
```

### Właściwości i metody tablic

| Typ | Nazwa                   | Działanie                                                                                                                                                                                                                           |
| --- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| M   | of()                    |                                                                                                                                                                                                                                     |
| M   | t1.concat(t2)           | Łączy tablice w kolejności t1 z t2 i opcjonalnie kolejnymi                                                                                                                                                                          |
| M   | copyWithin()            |                                                                                                                                                                                                                                     |
| M   | entries()               |                                                                                                                                                                                                                                     |
| M   | every()                 | Sprawdza czy każdy element tablicy spełnia podany warunek. Zwraca true/false                                                                                                                                                        |
| M   | fill(el, in1, in2)      | Wypełnia tablicę elementem `el`, opcjonalnie od indeksu `in1` do `in2`                                                                                                                                                              |
| M   | filter()                | Filtruje tablicę zwracając tylko elementy, które pasują do danego warunku. Zwraca nową tablicę.                                                                                                                                     |
| M   | find(f(el))             | Zwraca pierwszy element spełniający warunek podany w funkcji                                                                                                                                                                        |
| M   | findIndex(f(el))        | Zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje funkcję jako parametr.                                                                                                                        |
| M   | flat(num)               | Spłaszcza tablicę wielowymiarową o `num` poziomów. `Infinity` spłąszcza tablicę do jednopoziomowej                                                                                                                                  |
| M   | flatMap()               |                                                                                                                                                                                                                                     |
| M   | forEach(f(el, in, arr)) | Iteruje po tablicy i przyjmuje jako parametr funkcję, w której możemy ustawić 3 parametry element z tablicy `el`, indeks elementu `in`, tablicę po której iterujemy `arr`. Metoda działą bezpośrednio na obiekcie i nic nie zwraca. |
| M   | includes()              | Zwraca true/false w zależności od tego czy szukana wartość znajduje się w tablicy                                                                                                                                                   |
| M   | indexOf(el)             | Zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje wartość jako parametr.                                                                                                                        |
| M   | join(separator)         | Łączy kolejne elementy tablicy w string za pomocą separatora                                                                                                                                                                        |
| M   | keys()                  |                                                                                                                                                                                                                                     |
| P   | length                  | Zwraca długość tablicy (ilość jej elementów)                                                                                                                                                                                        |
| M   | lastIndexOf(el)         | Zwraca ostatni indeks elementu `el` w tablicy lub `-1` jeśli element nie został znaleziony                                                                                                                                          |
| M   | map()                   | Iteruje po tablicy i każdorazowo zwraca nowy element tablicy, na którym wywołana została funkcja. Zwraca tablicę.                                                                                                                   |
| M   | pop()                   | Usuwa ostatni element z tablicy i zwraca go                                                                                                                                                                                         |
| M   | push()                  | Dodaje element na koniec tablicy i zwraca jej nową długość                                                                                                                                                                          |
| M   | reduce()                | Wykonuje operacje na tablicy redukując ją według podanego warunku                                                                                                                                                                   |
| M   | reduceRight()           |                                                                                                                                                                                                                                     |
| M   | reverse()               | Odwraca kolejność elementów w tablicy                                                                                                                                                                                               |
| M   | shift()                 | Usuwa pierwszy element z tablicy i zwraca go                                                                                                                                                                                        |
| M   | slice(od, do)           | Zwraca nową tablicę z elementami od (zawiera) do (nie zawiera) lub do końca jesli nie podano indeksu                                                                                                                                |
| M   | some()                  | Sprawdza czy któykolwiek element tablicy spełnia podany warunek. Zwraca true/false                                                                                                                                                  |
| M   | sort(f(a,b){})          | Sortuje tablicę według warunku w funkcji f zwracającej wartość liczbową - `0` - kolejność bez zmian, `>0` - a większy indeks niż b, `0<` - b większy indeks niż a                                                                   |
| M   | splice(in, num, el)     | Usuwa elementy od indeksu `in` w ilości `num` i/lub wstawia elementy `el` przed indeksem `in`                                                                                                                                       |
| M   | toLocaleString()        |                                                                                                                                                                                                                                     |
| M   | toSource()              |                                                                                                                                                                                                                                     |
| M   | toString()              |                                                                                                                                                                                                                                     |
| M   | unshift()               | Dodaje element na początek tablicy i zwraca jej nową długość                                                                                                                                                                        |
| M   | values()                |                                                                                                                                                                                                                                     |

#### Długość tablicy

`array.length` - zwraca długość tablicy (ilość jej elementów)

```javascript
// indeks:      0         1         2
const tab = ["Marcin", "Ania", "Agnieszka"];

console.log(tab.length); // 3
console.log(tab[tab.length - 1]); // Agnieszka
```

#### Dodawanie elementów do tablicy

`array.unshift()` - dodaje element na początek tablicy i zwraca jej nową długość

`array.push()` - dodaje element na koniec tablicy i zwraca jej nową długość

#### Usuwanie elementów z tablicy

`array.shift()` - usuwa pierwszy element z tablicy i zwraca go

`array.pop()` - usuwa ostatni element z tablicy i zwraca go

#### Sortowanie tablicy

`array.sort(f)` - sortuje tablicę według warunku w funkcji f zwracającej wartość liczbową

- `0` - kolejność bez zmian
- `>0` - a większy indeks niż b
- `0<` - b większy indeks niż a

```javascript
function compare(a, b) {
  if (a < B) {
    return -1;
  } else if (a > b) {
    return 1;
  }
  //if (a === b)
  return 0;
}

tab.sort(compare);
```

```javascript
// Sortowanie według numerów
function compareNr(a, b) {
  return a - b;
}

const tab = [100, 320, 10, 25, 310, 1200, 400];

const tab3 = tab.sort(compareNr);
console.log(tab3); //[10, 25, 100, 310, 320, 400, 1200]
```

#### Metoda forEach()

`array.forEach(f(el, in, arr))` - metoda przyjmuje jako parametr funkcję, w której możemy ustawić 3 parametry:

- element z tablicy `el`
- indeks elementu `in`
- tablica po której iterujemy `arr`

```javascript
const tab = ["Marcin", "Ania", , "Agnieszka"];

//pod zmienną el trafią kolejne elementy
tab.forEach(function(el) {
  console.log(el.toUpperCase());
});

// Przykład
const tab = ["Marcin", "Ania", "Agnieszka"];

let letterCount = 0;
tab.forEach(function(el) {
  letterCount += el.length;
});

console.log("Liczba liter wszystkich imion to: " + letterCount); // 19
```

Alternatywnie do iterowania można uzyć pętli for

```javascript
const tab = ["Marcin", "Ania", "Agnieszka", "Piotrek", "Grześ", "Magda"];

for (let i = 0; i < tab.length; i++) {
  console.log(tab[i]);
}
```

#### Sprawdzanie czy elementy spełniają warunek

`array.every()` - sprawdza czy każdy element tablicy spełnia podany warunek. Zwraca true/false

`array.some()` - sprawdza czy którykolwiek element tablicy spełnia podany warunek

#### Mapowanie tablicy

`array.map()` - iteruje po tablicy i każdorazowo zwraca nowy element tablicy, na którym wywołana została funkcja. Zwraca tablicę.

```javascript
const tab = [1, 2, 3];
const tab2 = tab.map(function(el) {
  return el * 2;
});

console.log(tab2); //[2, 4, 6]
```

#### Filtrowanie elementów

`array.filter()` - filtruje tablicę zwracając tylko elementy, które pasują do danego warunku. Zwraca nową tablicę

```javascript
const ourTable = [1, 2, 3, 4, 5, 6];

const evenNumbers = ourTable.filter(function(el) {
  return el % 2 === 0;
});

console.log(evenNumbers); //[2, 4, 6]
```

#### Redukowanie tablicy

`array.reduce()` - wykonuje operacje na tablicy redukując ją według podanego warunku

```javascript
const tab = [1, 2, 3, 4];
const result = tab.reduce(function(prev, next) {
  return prev + next;
});

// 1 iteracja => prev = 1, next = 2
// 2 iteracja => prev = 3, next = 3
// 3 iteracja => prev = 6, next = 4
// Wynik = 10
```

```javascript
const tab = [3, 2, 4, 2];
const result = tab.reduce(function(a, b) {
  return a * b;
});

// 1 iteracja => prev = 3, next = 2
// 2 iteracja => prev = 6, next = 4
// 3 iteracja => prev = 24, next = 2

// Wynik = 48
```

```javascript
// Atrybut po funkcji to początkowa wartość
const sum1 = [1, 2, 3].reduce(function(a, b) {
  return a + b;
}, 0);

// sum1 = 6
```

### Wyszukiwanie elementów w tablicy

`array.indexOf(el)` - zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje wartość jako parametr.

`array.lastIndexOf(el)` - zwraca ostatni indeks elementu `el` w tablicy lub `-1` jeśli element nie został znaleziony

`array.includes(el)` - Zwraca true/false w zależności od tego czy szukana wartość znajduje się w tablicy

`array.find(f(el))` - zwraca pierwszy element spełniający warunek podany w funkcji

```javascript
const tab = [12, 5, 8, 130, 44];

const bigNr = tab.find(function(el) {
  return el >= 15;
});

console.log(bigNr); //130
```

`array.findIndex(f(el))` - zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje funkcję jako parametr.

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

## Właściwości JavaScript

- Dla każdego elementu z ID w strukturze strony tworzona jest zmienna o takiej samej nazwie, która wskazuje na dany element

```javascript
console.log(mainContent); // Nie stworzyliśmy nigdzie zmiennej mainContent, ale jeśli na stronie znajduje się element o takim id console.log zwróci go
```
