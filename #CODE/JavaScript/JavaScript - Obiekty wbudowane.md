# JavaScript - Obiekty wbudowane

## String

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
