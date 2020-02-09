# JavaScript - Dobre praktyki

- Samodzielne wstawianie średników na końcu linii (inaczej JavaScript wstawia je automatycznie co może dać niepożądane efekty)
- Uważać na to gdzie wstawiamy nową linię (znak powrotu karetki) np. w przypadku nowej linii po słowie `return` parser może automatycznie wstawić średnik i zakończyć działanie funkcji.
- Dodawać metody do `prototype` konstruktora obiektu. Wtedy dana metoda zajmuje w pamięci mniej miejsca niż gdyby była umieszczona w konstruktorze i kopiowana za każdym razem gdy tworzony jest nowy pusty obiekt danego typu.

## Zmienne

- Nie tworzyć zmiennych globalnych

## Właściwości JavaScript

- Dla każdego elementu z ID w strukturze strony tworzona jest zmienna o takiej samej nazwie, która wskazuje na dany element

```javascript
console.log(mainContent); // Nie stworzyliśmy nigdzie zmiennej mainContent, ale jeśli na stronie znajduje się element o takim id console.log zwróci go
```

## Dostępność

- Stosować `link` tylko do linków, czyli elementów zmieniających URL a `button` do akcji w ramach danej strony
- Jeśli chcemy wykorzystać dowolny element HTML jako przycisk zamiast elementu `button`, należy dodać do niego atrybut `role="button"`, oraz `tabindex="0"` (wartość liczbowa w zależności o fokusyjności elementu).
