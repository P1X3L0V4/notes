# JavaScript - Asynchroniczność

## Asynchroniczność

JavaScript jest językiem jednowątkowym (single threaded) co oznacza, że mamy tylko jeden call stack, który może na raz obsłużyć tylko jedną instrukcję.

```javascript
console.log("START");

setTimeout(function() {
  console.log("MID");
}, 5000);

console.log("END");

// Zwróci trzy console.log w kolejności: START, END, MIDDLE
```

### Callback hell

Wynikająca z tego asynchroniczność prowadzi w konsekwencji do zjawiska nazywanego **callback hell**, która polega na tym, że jeśli potrzebujemy wykonać operacje w określonej kolejności to musimy zagnieżdżać callbacki

```html
<div class="go">Click Me</div>
```

```javascript
function go(e) {
    const el = e.currentTarget;
    // 1. Change the text to GO when clicked.
    el.textContent = 'GO';
    setTimeout(function () {
    // 2. Make it a circle after 2 seconds
    el.classList.add('circle');
    setTimeout(function () {
        // 3. Make it red after 0.5s
        el.classList.add('red');
        setTimeout(function () {
        // 4. make it square after 0.25s
        el.classList.remove('circle');
        setTimeout(function () {
            // 5. make it purple
            el.classList.remove('red');
            el.classList.add('purple');
            setTimeout(function () {
            // 6. fade out after 0.5s
            el.classList.add('invisible');
            setTimeout(function () {
                console.log('You have reacted the 7th layer of callback hell');
                el.classList.remove('invisible', 'purple');
            }, 500);
            }, 500);
        }, 500);
        }, 500)
    }, 500)
    }, 500)
```

http://latentflip.com/loupe/ - narzędzie do obrazowania asynchroniczności

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

### Metoda open()

`xhr.open(typ, url, [async, login*, password*])` - metoda konfigurująca połączenie, przyjmuje 3 atrybuty:

- typ połączenia (`get, post, put, patch, delete`)
- adres do którego się łączymy
- parametr określający czy nasze połączenie ma być asynchroniczne czy synchroniczne (dodatkowo możemy podać login i hasło w przypadku Basic HTTP Authentication).

### Metoda send()

`xhr.send()` - metoda służąca do wysyłania połączenia na serwer. Jeśli wysyłamy dane podajemy je jako atrybut.

```javascript
const xhr = new XMLHttpRequest();

//typ połączenia, url, czy połączenie asynchroniczne
xhr.open("GET", "https://jsonplaceholder.typicode.com/posts", true);
xhr.send();

// GET
xhr.send(null);

// POST
xhr.send(formData);
```
