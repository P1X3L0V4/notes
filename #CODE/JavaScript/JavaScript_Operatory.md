# JavaScript - Operatory

## Operatory

### Operatory matematyczne

```javascript
Tabela dla y = 5
```

| Operator | Nazwa działania    | Równanie     | Wynik y | Wynik x    |
| -------- | ------------------ | ------------ | ------- | ---------- |
| `+`      | Dodawanie          | `x = y + 2`  | `y = 5` | `x = 7`    |
| `-`      | Odejmowanie        | `x = y - 2`  | `y = 5` | `x = 3`    |
| `*`      | Mnożenie           | `x = y * 2`  | `y = 5` | `x = 10`   |
| `/`      | Dzielenie          | `x = y / 2`  | `y = 5` | `x = 2.5`  |
| `%`      | Reszta z dzielenia | `x = y % 2`  | `y = 5` | `x = 1`    |
| `**`     | Potęgowanie        | `x = y ** y` | `y = 5` | `x = 3125` |
| `++`     | Inkrementacja      |              |         |            |
|          | Preinkrementacja   | `x = ++y`    | `y = 6` | `x = 6`    |
|          | Postinkrementacja  | `x = y++`    | `y = 6` | `x = 5`    |
| `--`     | Dekrementacja      |              |         |            |
|          | Predekrementacja   | `x = --y`    | `y = 4` | `x = 4`    |
|          | Postdekrementacja  | `x = y--`    | `y = 4` | `x = 5`    |

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

| Operator | Przykład  | Równoznaczne z | Wynik    |
| -------- | --------- | -------------- | -------- |
| `=`      | `x = y`   | `x = y`        | `x = 5`  |
| `+=`     | `x += y`  | `x = x + y`    | `x = 15` |
| `-=`     | `x -= y`  | `x = x - y`    | `x = 5`  |
| `*=`     | `x \*= y` | `x = x \* y`   | `x = 50` |
| `/=`     | `x /= y`  | `x = x / y`    | `x = 2`  |
| `%=`     | `x %= y`  | `x = x % y`    | `x = 0`  |

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

| Operator | Opis                   | Równanie    | Zwróci  |
| -------- | ---------------------- | ----------- | ------- |
| `==`     | równe                  | `x == 8`    | `false` |
| `!=`     | różne                  | `x != 8`    | `true`  |
| `===`    | identyczność           | `x === 5`   | `true`  |
|          |                        | `x === "5"` | `false` |
| `!==`    | nieidentyczność        | `x !== "5"` | `true`  |
|          |                        | `x === 5`   | `false` |
| `>`      | większe od             | `x > 8`     | `false` |
| `<`      | mniejsze od            | `x < 8`     | `true`  |
| `>=`     | większe bądź równe od  | `x >= 8`    | `false` |
| `<=`     | mniejsze bądź równe od | `x <= 8`    | `true`  |

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

| Operator | Nazwa                              | Opis                                    | Przykład              | Wynik                                                       |
| -------- | ---------------------------------- | --------------------------------------- | --------------------- | ----------------------------------------------------------- |
| `&&`     | Koniunkcja<br />(iloczyn logiczny) | and (i)                                 | `(x < 10 && y > 1)`   | Prawda, bo x jest mniejsze od 10 i y jest większe od 1      |
| `||`     | Alternatywa<br />(suma logiczna)   | or (lub)                                | `(x > 8 \|\| y > 1)`  | Prawda, bo x nie jest większe od 8, ale y jest większe od 1 |
| `^`      | Albo                               | xor (jeden z, ale nie dwa równocześnie) | `(x === 6 ^ y === 3)` | Fałsz, bo obydwa są prawdziwe                               |
| `!`      | Negacja                            | not (negacja)                           | `!(x === y)`          | Prawda, bo negujemy to, że x === y                          |

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