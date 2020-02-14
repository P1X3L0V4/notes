# JavaScript - Obiekt Math()

**Obiekt Math()** -obiekt udostępniany przez Javascript, ułatwiający przeprowadzanie operacji matematycznych.

## Właściwości Math()

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

## Metody Math()

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

## Przykłady zastosowania obiektu `Math()`

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
