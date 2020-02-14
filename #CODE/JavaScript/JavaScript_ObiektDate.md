# JavaScript - Obiekt Date()

JavaScript udostępnia konstruktor `Date()` który umożliwia nam w łatwy sposób przeprowadzać operacje związane z czasem.

```javascript
const now = new Date();
console.dir(now);
```

## Metody Date

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

## Formatowanie daty

```javascript
const now = new Date();
const el = document.querySelector(".element");

const html = `
Jest teraz czas: ${now.getHours()} : ${now.getMinutes()} : ${now.getSeconds()} lt;br>
Dnia: ${now.getDate()} . ${now.getMonth() + 1} . ${now.getFullYear()}
`;

el.innerText = html;
```

## Ustawianie daty i czasu

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
