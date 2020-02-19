# React od podstaw

## Wstęp do kursu

**React** \- biblioteka JavaScript do budowania dynamicznych i interaktywnych interfejsów użytkownika\.

* Link do strony: [https://pl.reactjs.org/](https://pl.reactjs.org/)
* Projekt Open Source stworzony przez Facebook'a w 2013 roku
* Pozwala tworzyć SIngle Page Application - strony i aplikacje, których zawartość zmienia się dynamicznie bez przełądowania strony
* Interfejs składa się z komponentów, które tworzą strukturę i logikę (czym coś jest i jak się zachowuje)
* Komponenty posiadają stany, które wpływają na zachowanie elementów

**Komponent**, powinien:

* być mały
* być elastyczny (edytowalny)
* mieć znaczenie (struktura, logika)

Rodzaje:

* stanowy (klasowy) - zawiera state i props
* bezstanowy (funkcyjny) - zawiera props

**JSX** \- składnia używana w React\, przypomina składnię HTML

### Rozpoczęcie pracy z React

Podpięcie niezbędnych bibliotek

* React `<script crossorigin src="`[`https://unpkg.com/react@16/umd/react.production.min.js`](https://unpkg.com/react@16/umd/react.production.min.js)`"></script>`
* ReactDOM `<script crossorigin src="`[`https://unpkg.com/react-dom@16/umd/react-dom.production.min.js`](https://unpkg.com/react-dom@16/umd/react-dom.production.min.js)`"></script>`
* Babel `<script src="`[`https://unpkg.com/@babel/standalone/babel.min.js`](https://unpkg.com/@babel/standalone/babel.min.js)`"></script>`

W treści dokumentu

* Element `<html>` o id `root` lub `app` w którym renderować się będzie nasza aplikacja
* `<script type="text/babel" src="App.js"></script> - p`odpięcie naszego skryptu (po bibliotekach) w `<head>` lub `<body>`

### Przykładowa treść index.html

```
<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Example</title>
</head>
<body>
  <div id="root">
    <!-- kontener na aplikację react  -->
  </div>
  <script crossorigin src="https://unpkg.com/react@16/umd/react.production.min.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.production.min.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel" src="App.js"></script>
</body>
</html>
```

## JavaScript - zagadnienia potrzebne w pracy z React

### Funkcja strzałkowa

Przykład 1 - Zapis z nawiasami klamrowymi

``` javascript
const fn = (item) => {
    console.log("Podany argument to " + item)
}

fn("Hej!")

-----------------------------------------

// Zapis w Vanilla JavaScript

const fn = function() {
    console.log("Podany argument to " + item)
}
```

Przykład 2 - Zapis z pojedynczym argumentem i instrukcją

* Przy jednym argumencie możemy pominąć nawiasy
* Linia kodu po strzałce zwracana jest automatycznie jakby znajdowało się tam słowo kluczowe `return`

``` javascript
const fn = item => console.log("Podany argument to " + item)

fn("Hej!")
```

Przykład 3 - Zapis z nawiasami okrągłymi

* Możliwe jest użycie nawiasów okrągłych zamiast klamrowych

``` javascript
const fn = (item) => (
    console.log("Podany argument to " + item)
)

fn("Hej!")
```

Przykład 4 - Zapis z dwoma argumentami i stringiem

``` javascript
const fn = (item, item2) => {
    return `Podany argument to " + ${item} i ${item2})`
}

fn("Hej!", "Ho!")
```

Przykład 5 - This w funkcji strzałkowej

* W poniższym przykłądzie `this` będzie wskazywało na `window`(obiekt globalny) ponieważ funkcja strzałkowa nie tworzy własnego przypisania wiązania `this`, a zamiast
tego dziedziczy je (przejmuje `this`, który istnieje we wcześniejszym
kontekście)

``` javascript
const btn = document.querySelector('button');
btn.addEventListener('click', () => console.log(this));
```

* W poniższym przykładzie (funkcja stworzona za pomocą słowa kluczowego function) `this` będzie wskazywało na obiekt, na którym wywołane zostało zdarzenie

``` javascript
const btn = document.querySelector('button')
btn.addEventListener('click', function() {
console.log(this)
})
```

### Metody tablic i iteratory tablic

#### .join()

Łączy tablicę za pomocą podanego znaku i zwraca stringa. Oryginalna tablica pozostaje niezmieniona.

``` javascript
const users = ["adam", "bogdan", "czarek", "darek"];

const usersString = users.join(" ");
console.log(usersString); // "adam bogdan czarek darek"
```

#### .concat()

Łączy tablicę z innym elementem (np. tablicą, lub zmienną) i zwraca nową tablicę. Oryginalna tablica pozostaje niezmieniona.

``` javascript
const users= ["adam", "bogdan", "czarek", "darek"];
const newUser = "edyta";

const allUsers = users.concat(newUser);
console.log(allUsers); // ["adam", "bogdan", "czarek", "darek", "edyta"]
```

Operator spread - alternatywa dla metody `concat()`

``` javascript
const users = ["adam", "bogdan", "czarek", "darek"];
const allUsers = [...users, "edyta"];
console.log(allUsers); // ["adam", "bogdan", "czarek", "darek", "edyta"]
```

#### .map()

Iteruje po wszystkich elementach tablicy wykonując wskazane operacje i zwraca nową tablicę o tej samej długości. Oryginalna tablica pozostaje niezmieniona.

Przykład 1

``` javascript
const users = ["adam", "bogdan", "czarek", "darek"];
const usersFirstLetterUpperCase = users.map(user => user[0].toUpperCase());
console.log(usersFirstLetterUpperCase); // ["A", "B", "C", "D"]
```

Przykład 2

``` javascript
const numbers = [2, 3, 4];
const doubleNumber = numbers.map(number => number * 2);
console.log(doubleNumber); // [4, 6, 8]
```

#### .forEach(element, index, array)

Iteruje po wszystkich elementach tablicy wykonując wskazane operacje. Nie zwraca nowej tablicy (zwraca `undefined`).

Przykład 1

``` javascript
const usersAge = [20, 21, 23, 43];
usersAge.forEach(age => console.log(`W przyszłym roku użytkownik będzie miał ${age+ 1}lat`));
```

Przykład 2

``` javascript
const usersAge = [20, 21, 23, 43];
let usersTotalAge = 0;
usersAge.forEach(age => usersTotalAge += age);
console.log(usersTotalAge); // 107
```

Przykład 3

``` javascript
const usersAge = [20, 21, 23, 43];
const section = document.createElement('section');
usersAge.forEach((age, index, array) => {
    section.innerHTML += (
        `<h1> Użytkownik ${index + 1}</h1>
        <p>wiek: ${age}</p>`
    )
    if(index === array.length - 1) {
        document.body.appendChild(section);
    }
})
```

#### .filter()

Zwraca nową tablicę złożoną z elementów, przy których iterator zwrócił `true`

Przykład 1

``` javascript
const users = ["adam", "bogdan", "czarek", "darek"];
const NameWith6Letter = users.filter(user => user.length === 6);
console.log(NameWith6Letter); // ["bogdan", "czarek"]
```

Przykład 2 (z wykorzystaniem indexOf)

``` javascript
const users = ["adam", "bogdan", "czarek", "darek"];
const NameWithLetterK = users.filter((user) => {
    return (
        user.indexOf("k") > -1
    )
})
console.log(NameWithLetterK); // ["czarek", "darek"]

// Alternatywny zapis
const users = ["adam", "bogdan", "czarek", "darek"];
const NameWithLetterK = users.filter(user => user.indexOf("k") > -1);
console.log(NameWithLetterK); // ["czarek", "darek"]
```

#### .findIndex()

Zwraca indeks elementu, który jako pierwszy spełnia warunek (zwróci `true`). Jeśli w żadnej iteracji nie będzie spełniony warunek, to zwróci `-1`

``` javascript
const customers = [
    { name: "Adam", age: 67 },
    { name: "Basia", age: 27 },
    { name: "Marta", age: 17 },
];
const isUsersAdult = customers.findIndex(customer => customer.age < 18);
console.log(isUsersAdult); // 2
```

#### .find()

Zwraca element, który jako pierwszy spełnia warunek (zwróci `true`). Jeśli w żadnej iteracji nie będzie spełniony warunek, to zwróci `undefined`.

``` javascript
const customers = [
    { name: "Adam", age: 67 },
    { name: "Basia", age: 27 },
    { name: "Marta", age: 17 },
];
const firstAdultUser = customers.find(customer => customer.age >= 18);
console.log(firstAdultUser); // {name: "Adam", age: 67}
```

### Klasa i instancja

Deklaracja klasy

``` javascript
class City {
}
```

Tworzenie instancji klasy

``` javascript
const Warsaw = new City();
const NewYork = new City();
// Powstają dwa (różne, niepołączone) obiekty będące instancją City
```

Klasa - właściwości instancji i prototyp

``` javascript
class Country {
    // constructor() {}
}
const poland = new Country();
```

``` javascript
class Country {
    constructor(name, capital, population) {
        this.name = name;
        this.capital = capital;
        this.popultion = population;
    }
}
const poland = new Country('Polska', 'Warszawa', 38000000);
// Country {name: "Polska", capital: "Warszawa", popultion: 38000000}
```

``` javascript
class Country {
    ...
}
const poland = new Country('Polska', 'Warszawa', 38000000);

// poland (object)
1.capital:"Warsawa"
2.citizensNumber:38000000
3.name:"Polska"
4.__proto__:Object
```

Klasa - dodawanie metod do prototypów i instancji

``` javascript
class Country {
    constructor(name) {
        this.name = name; // właściwość każdej instancji
        this.showName = () => console.log(this.name); // metoda każdej instancji
    }

    // Wszystkie metody tworzone w klasie znajdują się w prorotypie klasy, do której dostęp mają wszystkie instancje.

    showCountryName() {
            console.log(`Nazwa kraju to ${this.name}`);
    }
}

const Poland = new Country('Polska');
const Italy = new Country('Italia');
Poland.showCountryName(); // Nazwa kraju to Polska
Italy.showCountryName(); // Nazwa kraju to Italia
Poland.showName(); // Polska
Italy.showName(); // Italia
```

``` javascript
class Country {
    constructor(name) {
        this.name = name;
        this.showName = () => console.log(this.name);
    }

    showCountryName() {
        console.log(`Nazwa kraju to ${this.name}`);
    }
}

const Poland = new Country('Polska');
Poland.showCountryName(); // Nazwa kraju to Polska
Poland.showName(); // Polska
```

Klasa - metody prototypu czy instancji?

``` javascript
class Country {
    constructor(name) {
        this.name= name;
        this.showCountryName = function() {
        console.log("Metoda w instancji wskazuje: " + this.name);
    }
}

    showCountryName() {
        console.log(`Metoda w prototypie wskazuje ${this.name}`);
    }
}

const Poland = new Country('Polska');
Poland.showCountryName(); // Metoda w instancji wskazuje Polska
```

Klasa - dziedziczenie

``` javascript
class Person {
    constructor(name) {
        this.name = name;
    }

    showName() {
        console.log(`Imię osoby to ${this.name}`);
    }
}

class Student extends Person {
    constructor(name = "", degrees= []) {
        super(name) // Wywołuje konstruktor rodzica
        this.degrees = degrees;
    }

    showDegrees() {
        const completed = this.degrees.filter(degree => degree > 2);
        console.log(`Student ${this.name} ma stopnie: ${this.degrees} i zaliczył już ${(completed.length} przedmiotów`);
    }
}
const Janek = new Student("Adam", [2, 3, 4, 5, 2, 3]);
Janek.showDegrees() // Student Adam ma stopnie: 2,3,4,5,2,3 i zaliczył już 4 przedmiotów
```