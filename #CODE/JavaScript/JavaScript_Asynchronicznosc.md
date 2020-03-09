# JavaScript - Asynchroniczność

## Pętle zdarzeń & callback hell

JavaScript jest językiem jednowątkowym (single threaded) co oznacza, że mamy tylko jeden call stack, który może na raz obsłużyć tylko jedną instrukcję.

Elementy mechanizmów JS w przeglądarce

- Stos (stack)
- Web APIs
- Callback (task) queue
- Render queue

![Call Stack](img/async_callstack.png)

### Event loop

**Event loop** - zadaniem pętli zdarzeń jest przyglądanie się stosowi (stack) oraz kolejce zadań (task queue). Jeśli stos jest pusty bierze pierwszą rzecz z kolejki zadań i przenosi ją na stos.

```javascript
console.log("START");

setTimeout(function() {
  console.log("MID");
}, 5000);

console.log("END");

// Zwróci trzy console.log w kolejności: START, END, MIDDLE
```

### Browser redering

Przeglądarka próbuje renderować widok (repaint screen) co 16.6 milisekund (60 FPS), ale jest ograniczone przez operacje w JavaScript. Przeglądarka nie może renderować jeśli coś znajduje się w stosie.

Render:

- Ma wyższy priorytet niż callback(i)
- Jeśli wykonujemy kod synchronicznie renderowanie zostaje wstrzymane (brak możliwości zaznaczania tekstu, klikania w przyciski itp.)

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

## Promise

`Promise` - obiekt reprezentujący zakończenie lub porażkę asynchronicznej operacji i jej wartość. Obiekt `Promise` zawiera funkcję, która przyjmuje dwa parametry:

- `resolve()` - określa działanie w przypadku gdy promise zostanie spełniony
- `reject()` - określa działanie w przypadku gdy promise nie zostanie spełniony

```javascript
const promise1 = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve("foo");
  }, 300);
});

promise1.then(function(value) {
  console.log(value);
  // expected output: "foo"
});

console.log(promise1);
// expected output: [object Promise]
```

```javascript
function makePizza(toppings = []) {
  return new Promise(function(resolve, reject) {
    // Reject if people try with pineapple
    if (toppings.includes("pineapple")) {
      reject("Seriously? Get out 🍍");
    }

    const amountOfTimeToBake = 500 + toppings.length * 200;
    // Wait 1 second for the pizza to cook:

    setTimeout(function() {
      // When you are ready, you can resolve this promise
      resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(" ")}`);
    }, amountOfTimeToBake);

    // If something went wrong, we can reject this promise;
  });
}
```

### `then()`

`then()` - uruchamia się gdy promise zostanie rozwiązany pozytywnie (`resolve`). Pozwala łączyć promise'y w łańcuchy i uruchamiać je sekwencyjnie (sequentially)

```javascript
makePizza(["pepperoni"])
  .then(function(pizza) {
    console.log(pizza);
    return makePizza(["ham", "cheese"]);
  })
  .then(function(pizza) {
    console.log(pizza);
    return makePizza(["hot peppers", "onion", "feta"]);
  })
  .then(function(pizza) {
    console.log(pizza);
    return makePizza(["pineapple"]);
  })
  .then(function(pizza) {
    console.log(pizza);
    return makePizza(["one", "two", "three", "four"]);
  })
  .then(pizza => {
    console.log("All done! here is your last pizza");
    console.log(pizza);
  });
```

### `catch()`

`catch()` - uruchamia się gdy promise zostanie rozwiązany negatywnie (`reject`). Pozwala wyłapać błąd i wykonać odpowiedni kod.

### `Promise.all()`

`Promise.all([promises])` - metoda statyczna, która łączy wiele promise'ów w grupę i zostaje rozwiązana (resolved) gdy wszystkie jej elementy zostaną wykonane. Jako argument przyjmuje tablicę z listą promise'ów.

```javascript
// Uruchamianie jednoczesne
const pizzaPromise1 = makePizza(["hot peppers", "onion", "feta"]);
const pizzaPromise2 = makePizza(["one", "two", "three", "four", "one", "two"]);
const pizzaPromise3 = makePizza(["ham", "cheese"]);

// Grupa promise'ów
const dinnerPromise = Promise.all([
  pizzaPromise1,
  pizzaPromise2,
  pizzaPromise3
]);
```

### `Promise.race()`

`Promise.race([promises])` - metoda statyczna, która łączy wiele promise'ów w grupę i zostaje rozwiązana (resolved) gdy pierwsza obietnica zostanie wykonana. Jako argument przyjmuje tablicę z listą promise'ów.

```javascript
const firstPizzaPromise = Promise.race([
  pizzaPromise1,
  pizzaPromise2,
  pizzaPromise3
]);

firstPizzaPromise.then(pizza => {
  console.log("You must be hungry, here is the first one ready");
  console.log(pizza);
});
```

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
