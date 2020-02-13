# JavaScript - Obiekt Map

**Obiekt Map** - Map jest prostym obiektem mapującym klucze na wartości. Każdy element (zarówno obiekt jak i wartości proste) mogą być użyte zarówno jako klucz jak i wartość.Wprowadzony do JavaScript w ES6.

- Klucze w `Map` mogą być dowolnego typu
- Kolejność kluczy jest gwarantowana
- Nie może zawierać metod
- `Map` nie są obsługiwane przez `JSON.stringify()` i `JSON.parse()`

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

### Object.fromEntries()

Konwertuje `Map` na `Object`

```javascript
const myObj = Object.fromEntries(myMap);
```
