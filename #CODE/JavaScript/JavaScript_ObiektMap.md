# JavaScript - Obiekt Map

**Obiekt Map** - jest prostym obiektem mapującym klucze na wartości (kolekcje z kluczem ang. keyed collection). Każdy element, zarówno obiekt jak i wartości proste mogą być użyte zarówno jako klucz jak i wartość. Wprowadzony w _JavaScript ES6_.

- Klucze w `Map` mogą być dowolnego typu
- Kolejność kluczy jest gwarantowana
- Nie może zawierać metod
- `Map` nie są obsługiwane przez `JSON.stringify()` i `JSON.parse()`

### Różnice między Map i Object

#### Brak ograniczeń dla kluczy

- każdy klucz w zwykłym obiekcie JavaScript musi być albo stringiem albo symbolem
- Mapy pozwalają na używanie funkcji, obiektów i innych prymitywnych typów (w tym `NaN`) jako kluczy.

```javascript
// Obiekt
const symbol = Symbol();
const string2 = 'string2';
const regularObject = {
  string1: 'value1',
  [string2]: 'value2',
  [symbol]: 'value3'
}​

// Map
const func = () => null;
const object = {};
const array = [];
const bool = false;

const map = new Map();
map.set(func, 'value1');
map.set(object, 'value2');
map.set(array, 'value3');
map.set(bool, 'value4');
map.set(NaN, 'value5');
```

#### Bezpośrednia iteracja

- Aby iterować klucze, wartości lub ich pary w obiekcie, musisz albo przekonwertować je do tablicy, używając metody takiej jak `Object.keys()`, `Object.values()` lub `Object.entries()` albo użyć pętli `for...in` z pewnymi ograniczeniami.
- Mapy są bezpośrednio iterowalne, a ponieważ tworzą kolekcje z kluczem, kolejność iteracji jest taka sama jak kolejność wstawiania. Aby iterować nad wpisami w mapie, można użyć metody `forEach()` lub pętli `for...of`.

## Tworzenie

```javascript
// Konstruktor (brak literału)
const myMap = new Map();
const myMap = new Map([
  ["name", "Anna"],
  ["age", "100"]
]);
```

## Metody

### set()

Ustawia `entry`

```javascript
myMap.set(klucz, wartość);
myMap.set("key", "Anna");
```

### get()

Sprawdza `entry`

```javascript
prizes.get(score);
```

### size()

Zwraca ilość `entries` w mapie

```javascript
myMap.size(;
```

### has()

```javascript
myMap.has("name");
```

### delete()

Usuwa `entry`

```javascript
myMap.delete("name");
```

## Konwersja typu

```javascript
// Map na Array (destrukturyzacja)
const map = new Map([
  ["one", 1],
  ["two", 2]
]);
const arr = [...map];

// Map na Object
Object.fromEntries(map);

// Object na Map
new Map(Object.entries(obj));
```
