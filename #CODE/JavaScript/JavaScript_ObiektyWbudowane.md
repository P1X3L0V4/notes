# JavaScript - Obiekty wbudowane

## Obiekt String

**String** - prosty typ danych w postaci ciągu znaków

### Metody String

| Nazwa                                     | Zwraca                                                                          |
| ----------------------------------------- | ------------------------------------------------------------------------------- |
| `String.prototype.charAt()`               | Znak znajdujący się w ciągu na podanej pozycji                                  |
| `String.prototype.charCodeAt()`           | Kod (Unicode) dla wskazanego znaku                                              |
| `String.prototype.concat(str2)`           | Zwraca połączonie stringu z `str2`                                              |
| `String.prototype.endsWith()`             | `true`/`false` w zależności od tego czy ciąg został znaleziony na końcu stringa |
| `String.prototype.fromCharCode()`         | Zwraca łańcuch znaków stworzony przez podaną sekwencję kodów Unicode            |
| `String.prototype.includes()`             | `true`/`false` w zależności od tego czy ciąg został znaleziony                  |
| `String.prototype.indexOf()`              | Pozycję szukanego ciągu znaków w stringu (-1 = brak)                            |
| `String.prototype.lastIndexOf()`          | Numer ostatniego wystąpienia ciągu                                              |
| `String.prototype.localeCompare()`        |                                                                                 |
| `String.prototype.match()`                |                                                                                 |
| `String.prototype.repeat(num)`            | Powtarza ciąg `num` razy                                                        |
| `String.prototype.replace(szukany, nowy)` | String, w którym ciąg `szukany` zostaje zamieniony na `nowy`                    |
| `String.prototype.search()`               |                                                                                 |
| `String.prototype.slice(start, stop)`     | Nowy string od znaku `start` do `stop` włącznie lub do końca                    |
| `String.prototype.split(znak, dlugosc)`   | Tablicę rozdzielając string na podstawie `znak`                                 |
| `String.prototype.startsWith()`           |                                                                                 |
| `String.prototype.substr(start, dlugosc)` | Ciąg znaków od znaku `start` o wskazanej `dlugosc` lub do końca                 |
| `String.prototype.substring(start, stop)` | Ciąg znaków od znaku `start` do `stop` włącznie lub do końca                    |
| `String.prototype.toLocaleLowerCase()`    | Treść stringu małymi literami według lokalnego?                                 |
| `String.prototype.toLocaleUpperCase()`    | Treść stringu wielkimi literami według lokalne?                                 |
| `String.prototype.toLowerCase()`          | Treść stringu małymi literami                                                   |
| `String.prototype.toString()`             | Zwraca wartość obiektu string                                                   |
| `String.prototype.toUpperCase()`          | Treść stringu wielkimi literami                                                 |
| `String.prototype.trim()`                 |                                                                                 |
| `String.prototype.valueOf()`              |                                                                                 |

### Właściwości String

| Nazwa           | Zwraca          |
| --------------- | --------------- |
| `String.lenght` | Długość stringa |

### Tworzenie stringów

```javascript
const text = "Ala ma kota, a kot ma Ale."; // podwójne cudzysłowy
const text = "Ala ma kota"; // pojedyncze apostrofy
const text = `Ala ma kota o imieniu ${catName}`; // backticki (template strings)
```

Stringi można zapisywać:

- przy użyciu cudzysłowów
- przy użyciu apostrofów
- przy wykorzystaniu backticków
- przy wymiennym użyciu cudzysłowów i apostrofów lub skorzystać ze znaku ucieczki

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

## Obiekt Array

**Tablica (Array)** - zbiór danych indeksowany numerycznie

### Tworzenie tablic

```javascript
// Przy użyciu nawiasów kwadratowych (literału)
const tab = [];
const tab2 = [1, 2, 3, 4];
const tab3 = ["Marcin", "Ania", "Agnieszka"];

// Przy użyciu konstruktora
const tab = new Array(10, "Ala", "Bala", "Cala");
console.log(tab); //["Ala", "Bala", "Cala", blank x 7]
```

### Metody Array

| Nazwa                                     | Działanie                                                                                                                                                                                                                                                                                                                           |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Array.of()`                              |                                                                                                                                                                                                                                                                                                                                     |
| `Array.isArray`                           | Zwraca `true/false` w zależności od tego czy obiekt jest tablicą                                                                                                                                                                                                                                                                    |
| `Array.prototype.concat()`                | t1.concat(t2) łączy tablice w kolejności t1 z t2 i opcjonalnie kolejnymi                                                                                                                                                                                                                                                            |
| `Array.prototype.copyWithin()`            |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.entries()`               |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.every()`                 | Sprawdza czy wszystkie elementy tablicy spełniają zadany warunek. Przyjmuje funkcję `fn(element, index, array)`. Zwraca `true/false`                                                                                                                                                                                                |
| `Array.prototype.fill(el, in1, in2)`      | Wypełnia tablicę elementem `el`, opcjonalnie od indeksu `in1` do `in2`                                                                                                                                                                                                                                                              |
| `Array.prototype.filter()`                | filtruje tablicę zwracając tylko elementy, które spełniają warunek zawarty w funkcji `fn(element, index, array)`. Zwraca nową tablicę, w któej znajdą się elementy dla których przekazana funkcja zwróci `true`.                                                                                                                    |
| `Array.prototype.find(f(el))`             | Zwraca pierwszy element spełniający warunek podany w funkcji                                                                                                                                                                                                                                                                        |
| `Array.prototype.findIndex(f(el))`        | Zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje funkcję jako parametr.                                                                                                                                                                                                                        |
| `Array.prototype.flat(num)`               | Spłaszcza tablicę wielowymiarową o `num` poziomów. `Infinity` spłąszcza tablicę do jednopoziomowej                                                                                                                                                                                                                                  |
| `Array.prototype.flatMap()`               |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.forEach(f(el, in, arr))` | metoda dla każdego elementu w tablicy wykonuje operację. Jako argument przyjmuje funkcję `fn(element, index, array)`. Metoda działą bezpośrednio na obiekcie i nic nie zwraca.                                                                                                                                                      |
| `Array.prototype.includes()`              | Zwraca true/false w zależności od tego czy szukana wartość znajduje się w tablicy                                                                                                                                                                                                                                                   |
| `Array.prototype.indexOf(el)`             | Zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje wartość jako parametr.                                                                                                                                                                                                                        |
| `Array.prototype.join(separator)`         | Łączy kolejne elementy tablicy w string za pomocą separatora                                                                                                                                                                                                                                                                        |
| `Array.prototype.keys()`                  |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.lastIndexOf(el)`         | Zwraca ostatni indeks elementu `el` w tablicy lub `-1` jeśli element nie został znaleziony                                                                                                                                                                                                                                          |
| `Array.prototype.map()`                   | Iteruje po tablicy i każdorazowo zwraca nowy element tablicy, na którym wywołana została funkcja `fn(element, index, array)`. Zwraca tablicę.                                                                                                                                                                                       |
| `Array.prototype.pop()`                   | Usuwa ostatni element z tablicy i zwraca go                                                                                                                                                                                                                                                                                         |
| `Array.prototype.push()`                  | Dodaje element na koniec tablicy i zwraca jej nową długość                                                                                                                                                                                                                                                                          |
| `Array.prototype.reduce()`                | wykonuje operacje na tablicy redukując ją według podanego warunku, przyjmuje dwa argumenty: funkcję, którą wywołuje na każdym elemencie `fn(result, element, index, array)`, gdzie `result` to wynik wywołania funkcji z poprzednim elementem oraz `initialValue` to wartość jaką przyjmie `result` dla pierwszego elementu tablicy |
| `Array.prototype.reduceRight()`           |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.reverse()`               | Odwraca kolejność elementów w tablicy                                                                                                                                                                                                                                                                                               |
| `Array.prototype.shift()`                 | Usuwa pierwszy element z tablicy i zwraca go                                                                                                                                                                                                                                                                                        |
| `Array.prototype.slice(od, do)`           | Zwraca nową tablicę z elementami od (zawiera) do (nie zawiera) lub do końca jesli nie podano indeksu                                                                                                                                                                                                                                |
| `Array.prototype.some()`                  | Sprawdza czy przynajmniej jeden element spełnia zadany warunek. Przyjmuje funkcję `fn(element, index, array)`. Zwraca `true/false`                                                                                                                                                                                                  |
| `Array.prototype.sort(f(a,b){})`          | Sortuje tablicę według warunku w funkcji f zwracającej wartość liczbową - `0` - kolejność bez zmian, `>0` - a większy indeks niż b, `0<` - b większy indeks niż a. Modyfikuje oryginalną tablicę                                                                                                                                    |
| `Array.prototype.splice(in, num, el)`     | Usuwa elementy od indeksu `in` w ilości `num` i/lub wstawia elementy `el` przed indeksem `in`                                                                                                                                                                                                                                       |
| `Array.prototype.toLocaleString(`)        |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.toSource()`              |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.toString()`              |                                                                                                                                                                                                                                                                                                                                     |
| `Array.prototype.unshift()`               | Dodaje element na początek tablicy i zwraca jej nową długość                                                                                                                                                                                                                                                                        |
| `Array.prototype.values()`                |

### Metody zmieniające oryginalną tablicę

Niektóre metody działają w ten sposób, że modyfikują oryginalną tablicę (mutable methods), dlatego przed użyciem metod obiektu `Array` warto upewnić się, że mamy kopię oryginalnej tablicy.

```javascript
const myArr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const reversedArr = [...myArr]; // Wykonuje kopię tablicy za pomocą operatora spread
reversedArr.reverse();
```

### Długość tablicy

`array.length` - zwraca długość tablicy (ilość jej elementów)

```javascript
// indeks:      0         1         2
const tab = ["Marcin", "Ania", "Agnieszka"];

console.log(tab.length); // 3
console.log(tab[tab.length - 1]); // Agnieszka
```

### Dodawanie elementów do tablicy

`array.unshift()` - dodaje element na początek tablicy i zwraca jej nową długość

`array.push()` - dodaje element na koniec tablicy i zwraca jej nową długość

### Usuwanie elementów z tablicy

`array.shift()` - usuwa pierwszy element z tablicy i zwraca go

`array.pop()` - usuwa ostatni element z tablicy i zwraca go

### Sortowanie tablicy

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

### Metoda forEach()

`array.forEach(fn)` - metoda dla każdego elementu w tablicy wykonuje operację. Jako argument przyjmuje funkcję `fn(element, index, array)`

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

### Sprawdzanie czy elementy spełniają warunek

`array.every()` - sprawdza czy każdy element tablicy spełnia podany warunek. Zwraca true/false

`array.some()` - sprawdza czy którykolwiek element tablicy spełnia podany warunek

### Mapowanie tablicy

`array.map()` - iteruje po tablicy i każdorazowo zwraca nowy element tablicy, na którym wywołana została funkcja `fn(element, index, array)`. Zwraca tablicę.

- `element` – aktualnie przetwarzany element tablicy
- `index` – pozycja na której znajduje się aktualnie przetwarzany element
- `array` – cała tablica

```javascript
const tab = [1, 2, 3];
const tab2 = tab.map(function(el) {
  return el * 2;
});

console.log(tab2); //[2, 4, 6]
```

### Filtrowanie elementów

`array.filter()` - filtruje tablicę zwracając tylko elementy, które spełniają warunek zawarty w funkcji `fn(element, index, array)`. Zwraca nową tablicę, w któej znajdą się elementy dla których przekazana funkcja zwróci `true`.

```javascript
const ourTable = [1, 2, 3, 4, 5, 6];

const evenNumbers = ourTable.filter(function(el) {
  return el % 2 === 0;
});

console.log(evenNumbers); //[2, 4, 6]
```

### Redukowanie tablicy

`array.reduce()` - wykonuje operacje na tablicy redukując ją według podanego warunku, przyjmuje dwa argumenty:

- funkcję, którą wywołuje na każdym elemencie `fn(result, element, index, array)`, gdzie `result` to wynik wywołania funkcji z poprzednim elementem
- `initialValue` to wartość jaką przyjmie `result` dla pierwszego elementu tablicy

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

```javascript
// Przykłady wykorzystania reduce zamiast innych metod

// Map using reduce
[1, 2, 3].reduce((result, num) => [...result, num ** 3], []); // [1, 8, 27]

// Filter using reduce
[1, 2, 3, 4].reduce((result, num) => {
  if (num % 2 === 0) return [...result, num];
  return result;
}, []); // [2, 4]

// Sum using reduce
[1, 2, 3].reduce((result, num) => result + num, 0); // 6
```

### Wyszukiwanie elementów w tablicy

`array.indexOf(el)` - zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje wartość jako parametr.

`array.lastIndexOf(el)` - zwraca ostatni indeks elementu `el` w tablicy lub `-1` jeśli element nie został znaleziony

`array.includes(el)` - Zwraca true/false w zależności od tego czy szukana wartość znajduje się w tablicy

`array.find(f())` - zwraca pierwszy element spełniający warunek podany w funkcji `fn(element, index, array)`

```javascript
const tab = [12, 5, 8, 130, 44];

const bigNr = tab.find(function(el) {
  return el >= 15;
});

console.log(bigNr); //130
```

`array.findIndex(f(el))` - zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje funkcję jako parametr.

## Obiekt Math()

**Obiekt Math()** -obiekt udostępniany przez Javascript, ułatwiający przeprowadzanie operacji matematycznych.

### Właściwości Math()

| Nazwa          | Zwraca                                                   | Wartość            |
| -------------- | -------------------------------------------------------- | ------------------ |
| `Math.E`       | Zwraca stałą Eulera, która wynosi ok. 2.71               | 2.718281828459045  |
| `Math.LN2`     | Zwraca logarytm dwóch, tj. ok. 0.69                      | 0.6931471805599453 |
| `Math.LN10`    | Zwraca logarytm z dziesięciu, tj. ok. 2.30               | 2.302585092994046  |
| `Math.LOG2E`   | Zwraca logarytm o podstawie 2 z liczby E, czyli ok. 1.44 | 1.4426950408889634 |
| `Math.LOG10E`  | Zwraca logarytm o podstawie 10 z E, czyli ok. 0.43       | 0.4342944819032518 |
| `Math.PI`      | Zwraca wartość liczby Pi, czyli ok. 3.14                 | 3.141592653589793  |
| `Math.SQRT1_2` | Zwraca pierwiastek kwadratowy z 0.5, czyli ok. 0.70      | 0.7071067811865476 |
| `Math.SQRT2`   | Zwraca pierwiastek kwadratowy z 2, czyli ok. 1.41        | 1.4142135623730951 |

### Metody Math()

| Nazwa                        | Zwraca                                                                 |
| ---------------------------- | ---------------------------------------------------------------------- |
| `Math.abs(liczba)`           | Zwraca wartość absolutną liczby                                        |
| `Math.acos(liczba)`          | Zwraca arcus cosinus z liczby (podanej w radianach)                    |
| `Math.asin(liczba)`          | Zwraca arcus sinus z liczby (podanej w radianach)                      |
| `Math.atan(liczba)`          | Zwraca arcus tangens z liczby (podanej w radianach)                    |
| `Math.ceil(liczba)`          | Zwraca najmniejszą liczbę całkowitą, większą lub równą podanej liczbie |
| `Math.cos(liczba)`           | Zwraca cosinus liczby (podanej w radianach)                            |
| `Math.exp(liczba)`           | Zwraca wartość E podniesionej do potęgi wyrażonej podanym argumentem   |
| `Math.floor(liczba)`         | Zwraca największą liczbę całkowitą mniejszą lub równą podanej liczbie  |
| `Math.log(liczba)`           | Zwraca logarytm naturalny liczby                                       |
| `Math.max(liczba1, liczba2)` | Zwraca większą z dwóch liczb                                           |
| `Math.min(liczba1, liczba2)` | Zwraca mniejszą z dwóch liczb                                          |
| `Math.pow(liczba1, liczba2)` | Zwraca wartość liczby1 podniesionej do potęgi liczby 2                 |
| `Math.random()`              | Zwraca wartość pseudolosową z przedziału 0 - 1                         |
| `Math.round(liczba)`         | Zwraca zaokrąglenie danej liczby do najbliższej liczby całkowitej      |
| `Math.sin(liczba)`           | Zwraca sinus liczby (podanej w radianach)                              |
| `Math.sqrt(liczba)`          | Zwraca pierwiastek kwadratowy liczby                                   |
| `Math.tan(liczba)`           | Zwraca tangens liczby (podanej w radianach)                            |

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

## Obiekt Date

JavaScript udostępnia konstruktor `Date()` który umożliwia nam w łatwy sposób przeprowadzać operacje związane z czasem.

```javascript
const now = new Date();
console.dir(now);
```

### Metody Date

| Nazwa              | Co robi                                                                                                                                        |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `getDate()`        | - zwraca dzień miesiąca (wartość z przedziału 1 - 31)                                                                                          |
| `getDay()`         | - zwraca dzień tygodnia (0 dla niedzieli, 1 dla poniedziałku, 2 dla wtorku itd)                                                                |
| `getYear()`        | - zwraca liczbę reprezentującą rok (dla lat 1900 - 1999 jest to 2-cyfrowa liczba np. 99, a dla późniejszych jest to liczba 4-cyfrowa np. 2002) |
| `getFullYear()`    | - zwraca pełną liczbę reprezentującą rok (np. 1999 lub 2000)                                                                                   |
| `getHours()`       | - zwraca aktualną godzinę (wartość z przedziału 0 - 23)                                                                                        |
| `getMillisecond()` | - zwraca milisekundy (wartość z przedziału 0 - 999)                                                                                            |
| `getMinutes()`     | - zwraca minuty (wartość z przedziału 0 - 59)                                                                                                  |
| `getMonth()`       | - zwraca aktualny miesiąc (0 - styczeń, 1 - luty itp.)                                                                                         |
| `getSeconds()`     | - zwraca aktualną liczbę sekund (wartość z przedziału 0 - 59)                                                                                  |
| `getTime()`        | - zwraca aktualny czas jako liczbę reprezentującą liczbę milisekund która upłynęła od godziny 00:00 1 stycznia 1970 roku                       |

### Formatowanie daty

```javascript
const now = new Date();
const el = document.querySelector(".element");

const html = `
Jest teraz czas: ${now.getHours()} : ${now.getMinutes()} : ${now.getSeconds()} lt;br>
Dnia: ${now.getDate()} . ${now.getMonth() + 1} . ${now.getFullYear()}
`;

el.innerText = html;
```

### Ustawianie daty i czasu

```javascript
// Metoda 1
const time = new Date(2008, 4, 12, 15, 24, 18);

// Metoda 2
const now = new Date();
now.setYear(2008);
now.setMonth(4);
now.setDate(12);
now.setHours(15);
now.setMinutes(24);
now.setSeconds(18);
```
