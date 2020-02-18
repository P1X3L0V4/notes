# JavaScript - Obiekt Array()

**Tablica (Array)** - zbiór danych indeksowany numerycznie

## Tworzenie tablic

```javascript
// Przy użyciu nawiasów kwadratowych (literału)
const tab = [];
const tab2 = [1, 2, 3, 4];
const tab3 = ["Marcin", "Ania", "Agnieszka"];

// Przy użyciu konstruktora
const tab = new Array(10, "Ala", "Bala", "Cala");
console.log(tab); //["Ala", "Bala", "Cala", blank x 7]
```

## Metody Array

| Nazwa                                      | Działanie                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Array.of(el, el, el)`                     | Tworzy tablicę z podanych elementów                                                                                                                                                                                                                                                                                                                  |
| `Array.from({length: x}, fn(item, index))` | Tworzy tablicę o określonej długości wypełnioną elementami według funkcji                                                                                                                                                                                                                                                                            |
| `Array.isArray()`                          | Zwraca `true/false` w zależności od tego czy obiekt jest tablicą                                                                                                                                                                                                                                                                                     |
| `Array.prototype.concat()`                 | `t1.concat(t2)` łączy tablice w kolejności t1 z t2 i opcjonalnie kolejnymi                                                                                                                                                                                                                                                                           |
| `Array.prototype.copyWithin()`             |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.entries()`                |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.every()`                  | Sprawdza czy wszystkie elementy tablicy spełniają warunek podany w funkcji `arr.some(fn(element, index, array))` i zwraca `true/false`                                                                                                                                                                                                               |
| `Array.prototype.fill(el, in1, in2)`       | Wypełnia tablicę elementem `el`, opcjonalnie od indeksu `in1` do `in2`                                                                                                                                                                                                                                                                               |
| `Array.prototype.filter()`                 | Filtruje tablicę zwracając nową tablicę zawierającą tylko elementy, które spełniają warunek (`true`) zawarty w funkcji `fn(element, index, array)`                                                                                                                                                                                                   |
| `Array.prototype.find(f(el))`              | Zwraca pierwszy element spełniający warunek podany w funkcji                                                                                                                                                                                                                                                                                         |
| `Array.prototype.findIndex(f(el))`         | Zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje funkcję jako parametr.                                                                                                                                                                                                                                         |
| `Array.prototype.flat(num)`                | Spłaszcza tablicę wielowymiarową o `num` poziomów. `Infinity` spłąszcza tablicę do jednopoziomowej                                                                                                                                                                                                                                                   |
| `Array.prototype.flatMap()`                |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.forEach(f(el, in, arr))`  | Metoda dla każdego elementu w tablicy wykonuje operację. Jako argument przyjmuje funkcję `fn(element, index, array)`. Metoda działą bezpośrednio na obiekcie i nic nie zwraca.                                                                                                                                                                       |
| `Array.prototype.includes()`               | Zwraca true/false w zależności od tego czy szukana wartość znajduje się w tablicy                                                                                                                                                                                                                                                                    |
| `Array.prototype.indexOf(el)`              | Zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje wartość jako parametr.                                                                                                                                                                                                                                         |
| `Array.prototype.join(separator)`          | Łączy kolejne elementy tablicy w string za pomocą separatora                                                                                                                                                                                                                                                                                         |
| `Array.prototype.keys()`                   |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.lastIndexOf(el)`          | Zwraca ostatni indeks elementu `el` w tablicy lub `-1` jeśli element nie został znaleziony                                                                                                                                                                                                                                                           |
| `Array.prototype.map()`                    | Iteruje po tablicy i każdorazowo zwraca nowy element tablicy, na którym wywołana została funkcja `fn(element, index, array)`. Zwraca tablicę.                                                                                                                                                                                                        |
| `Array.prototype.pop()`                    | Usuwa ostatni element z tablicy i zwraca go                                                                                                                                                                                                                                                                                                          |
| `Array.prototype.push()`                   | Dodaje element na koniec tablicy i zwraca jej nową długość                                                                                                                                                                                                                                                                                           |
| `Array.prototype.reduce()`                 | Wykonuje operacje na tablicy redukując ją według mechanizmu funkcji, przyjmuje dwa argumenty: funkcję, którą wywołuje na każdym elemencie `fn(accumulator, element, index, array)`, gdzie `accumulator` to wynik wywołania funkcji z poprzednim elementem oraz `initialValue` to wartość jaką przyjmie `accumulator` dla pierwszego elementu tablicy |
| `Array.prototype.reduceRight()`            |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.reverse()`                | Odwraca kolejność elementów w tablicy                                                                                                                                                                                                                                                                                                                |
| `Array.prototype.shift()`                  | Usuwa pierwszy element z tablicy i zwraca go                                                                                                                                                                                                                                                                                                         |
| `Array.prototype.slice(od, do)`            | Zwraca nową tablicę z elementami od (zawiera) do (nie zawiera) lub do końca jesli nie podano indeksu                                                                                                                                                                                                                                                 |
| `Array.prototype.some()`                   | Sprawdza czy przynajmniej jeden element tablicy spełnia warunek podany w funkcji `arr.some(fn(element, index, array))` i zwraca `true/false`                                                                                                                                                                                                         |
| `Array.prototype.sort(f(a,b){})`           | Sortuje tablicę według warunku w funkcji f zwracającej wartość liczbową - `0` - kolejność bez zmian, `>0` - a większy indeks niż b, `0<` - b większy indeks niż a. Modyfikuje oryginalną tablicę                                                                                                                                                     |
| `Array.prototype.splice(in, num, el)`      | Usuwa elementy od indeksu `in` w ilości `num` i/lub wstawia elementy `el` przed indeksem `in`                                                                                                                                                                                                                                                        |
| `Array.prototype.toLocaleString(`)         |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.toSource()`               |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.toString()`               |                                                                                                                                                                                                                                                                                                                                                      |
| `Array.prototype.unshift()`                | Dodaje element na początek tablicy i zwraca jej nową długość                                                                                                                                                                                                                                                                                         |
| `Array.prototype.values()`                 |

## Metody zmieniające oryginalną tablicę

Niektóre metody działają w ten sposób, że modyfikują oryginalną tablicę (mutable methods), dlatego przed użyciem metod obiektu `Array` warto upewnić się, że mamy kopię oryginalnej tablicy.

```javascript
const myArr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const reversedArr = [...myArr]; // Wykonuje kopię tablicy za pomocą operatora spread
reversedArr.reverse();

// Lista mutable methods
copyWithin();
fill();
pop();
push();
reverse();
shift();
sort();
splice();
unshift();

//forEach() - nie mutuje tablicy, ale jej callback może to zrobić
```

## Długość tablicy

`array.length` - zwraca długość tablicy (ilość jej elementów)

```javascript
// indeks:      0         1         2
const tab = ["Marcin", "Ania", "Agnieszka"];

console.log(tab.length); // 3
console.log(tab[tab.length - 1]); // Agnieszka
```

## Dodawanie elementów do tablicy

`array.unshift()` - dodaje element na początek tablicy i zwraca jej nową długość

`array.push()` - dodaje element na koniec tablicy i zwraca jej nową długość

## Usuwanie elementów z tablicy

`array.shift()` - usuwa pierwszy element z tablicy i zwraca go

`array.pop()` - usuwa ostatni element z tablicy i zwraca go

## Sortowanie tablicy

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
// Sortowanie liczbod najmniejszej do nawiększej
function compareNr(a, b) {
  return a - b;
}

const tab = [100, 320, 10, 25, 310, 1200, 400];

const tab3 = tab.sort(compareNr);
console.log(tab3); //[10, 25, 100, 310, 320, 400, 1200]
```

## Metoda forEach()

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

## Sprawdzanie czy elementy spełniają warunek

`array.every()` - sprawdza czy każdy element tablicy spełnia podany warunek. Zwraca `true/false`

```javascript
const allMeats = Object.values(meats).every(meatVal => meatVal >= 3);
```

`array.some()` - sprawdza czy którykolwiek element tablicy spełnia podany warunek

```javascript
const minMeats = Object.values(meats).some(meatVal => meatVal >= 5);
```

## Mapowanie tablicy

`array.map()` - iteruje po tablicy i każdorazowo zwraca nowy element tablicy, na którym wywołana została funkcja `fn(element, index, array)`. Zwraca tablicę.

- `element` – aktualnie przetwarzany element tablicy
- `index` – pozycja na której znajduje się aktualnie przetwarzany element
- `array` – cała tablica

```javascript
const tab = [1, 2, 3];
const tab2 = tab.map(function(el) {
  return el * 2;
});

console.log(tab2); // [2, 4, 6]
```

## Filtrowanie elementów

`array.filter()` - filtruje tablicę zwracając tylko elementy, które spełniają warunek zawarty w funkcji `fn(element, index, array)`. Zwraca nową tablicę, w której znajdą się elementy dla których przekazana funkcja zwróci `true`.

```javascript
// Przykład 1
const ourTable = [1, 2, 3, 4, 5, 6];

const evenNumbers = ourTable.filter(function(el) {
  return el % 2 === 0;
});

console.log(evenNumbers); //[2, 4, 6]

// Przykład 2
const onlyGoodRaitings = feedback.filter(function(feedback) {
  return feedback.rating > 1;
});
```

## Redukowanie tablicy

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

## Wyszukiwanie elementów w tablicy

`array.indexOf(el)` - zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje wartość jako parametr.

`array.lastIndexOf(el)` - zwraca ostatni indeks elementu `el` w tablicy lub `-1` jeśli element nie został znaleziony

```javascript
toppings.indexOf("Avocado");
```

`array.includes(el)` - Zwraca true/false w zależności od tego czy szukana wartość znajduje się w tablicy

```javascript
const burgerRating = feedback.find(function(feedback) {
  return feedback.comment.includes("burg");
});

// Alternatywnie
const burgerRating = feedback.find(feedback =>
  feedback.comment.includes("burg")
);
```

`array.find(f())` - zwraca pierwszy element spełniający warunek podany w funkcji `fn(element, index, array)`

```javascript
// Przykład 1
const tab = [12, 5, 8, 130, 44];

const bigNr = tab.find(function(el) {
  return el >= 15;
});

console.log(bigNr); //130

// Przykład 2
const burgerRating = feedback.find(feedback =>
  feedback.comment.includes("burg");
);
```

`array.findIndex(f(el))` - zwraca indeks pierwszego pasującego elementu lub `-1` jeśli nie znaleziono. Przyjmuje funkcję jako parametr.

## Tworzenie tablicy z obiektu

**Object.entries()** - tworzy tablicę zawierającą zagnieżdżone tablice zawierające pary klucz - wartość obiektu

**Object.keys()** - tworzy tablicę zawierającą klucze obiektu

**Object.values()** - tworzy tablicę zawierającą wartości obiektu

```javascript
const meats = {
  beyond: 10,
  beef: 5,
  pork: 7
};

console.log(Object.entries(meats)); // (3) ["beyond", 10], ["beef", 5], ["pork", 7]]
console.log(Object.keys(meats)); // (3) ["beyond", "beef", "pork"]
console.log(Object.values(meats)); //(3) [10, 5, 7]
```

## Array.of()

**Array.of()** - Tworzy tablicę z podanych elementów

```javascript
const test = Array.of(1, 2, 3, 4, 5);
console.log(test); // (5) [1, 2, 3, 4, 5]
```

## Array.from()

**Array.from({length: x}, fn(item, index))** - tworzy tablicę o określonej długości `{length: x}` wypełnioną elementami według mechanizmu działania funkcji `fn`.

```javascript
// Funkcja która zwraca tablicę z cyframi od x do y z wykorzystaniem emtody Array.from();
function createRange(start, end) {
  return Array.from({ length: end - start + 1 }, function(item, index) {
    return start + index;
  });
}
```

## Array.isArray()

**Array.isArray()** - zwraca `true/false` w zależności do tego czy obiekt jest tablicą

```javascript
Array.isArray(tablica);
```
