# JavaScript - Obiekt String()

**String** - prosty typ danych w postaci ciągu znaków

## Metody String

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

## Właściwości String

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

## Stringi wieloliniowe

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

## Konkatenacja ciągów

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
