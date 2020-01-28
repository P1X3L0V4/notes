# JavaScript - Asynchroniczność

## AJAX

**AJAX (Asynchronous JavaScript and XML)** - technika, wzorzec, który umożliwia pobieranie i wysyłanie danych w sposób asynchroniczny, bez potrzeby przeładowania całej strony.

## JSON

**JSON** - format plików zbliżony strukturą do obiektów w JavaScript. Różni się od nich:

- Nazwy kluczy piszemy w cudzysłowach
- Uzywamy tylko podwójnych cudzysłowów
- Brak możliwości komentowania kodu

### Obiekt JSON

**Obiekt JSON** - pojedynczy obiekt, który udostępnia nam 2 metody: `stringify` i `parse`. Nie jest to klasa obiektów (więc nie używamy do tworzenia słowa kluczowego `new`).

`JSON.stringify(ob)` - Zamienia dany obiekt na tekstowy zapis w formacie JSON

`JSON.parse(obStr)` - Zamienia zakodowany wcześniej tekst na obiekt JavaScript

```Javascript
const ob = {
    name : "Piotr",
    surname : "Nowak"
}

const obStr = JSON.stringify(ob);
console.log(obStr); // "{"name":"Piotr","subname":"Nowak"}"

console.log( JSON.parse(obStr) ); // Nasz wcześniejszy obiekt
```

## CORS

**CORS - Cross-Origin Resource Sharing** - istniejące w przeglądarkach zabezpieczenie, które nakłada restrykcje na wykonywanie połączeń między różnymi domenami.

Zabezpieczenie takie powoduje, że domyślnie nie jesteśmy w stanie wykonywać dynamicznych połączeń między plikami na dysku, jeżeli naszą stronę otwieramy bezpośrednio z dysku (np. 2x klikając na ikonę). Wynika to z tego, że taki plik otwierany jest na adresie `file://...`, a adres ten nie jest poprawną domeną. Rozwiązaniem jest serwowanie strony z serwera lokalnego.

## XMLHttpRequest

**XMLHttpRequest** - obiekt, służy do nawiązywania dynamicznych połączeń XHR
