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

``` javascript
constusers= ["adam", "bogdan", "czarek", "darek"];
// Metoda join -zwraca stringa z tablicy
constusersString= users.join(" ");
console.log(usersString); //"adam bogdan czarek darek"
```

#### .concat()

``` javascript
constusers= ["adam", "bogdan", "czarek", "darek"];
// Metoda concat -łączymy tablicę z innym elementem (czy inną tablicą) i zwracamy nową tablicę.
constnewUser= "edyta"

constallUsers= users.concat(newUser)
console.log(allUsers);
//["adam", "bogdan", "czarek", "darek", "edyta"]
```

Operator spread - alternatywa dla metody `concat()`

``` javascript
constusers= ["adam", "bogdan", "czarek", "darek"];
constallUsers= [...users, "edyta"]
console.log(allUsers);
//["adam", "bogdan", "czarek", "darek", "edyta"]
```

#### .map()

Przykład 1

``` javascript
// Metoda map zwraca nową tablicę o tej samej długości
constusers= ["adam", "bogdan", "czarek", "darek"];
constusersFirstLetterUpperCase= users.map(user=>user[0].toUpperCase())
console.log(usersFirstLetterUpperCase);
// ["A", "B", "C", "D"]
```

Przykład 2

``` javascript
// Metoda map zwraca nową tablicę o tej samej długości
constnumbers= [2, 3, 4]
constdoubleNumber= numbers.map(number=>number* 2)
console.log(doubleNumber);
```

#### .forEach()

Przykład 1

``` javascript
// forEach -pracuje na tablicy, nie zwraca nowej (zwraca undefined)
constusersAge= [20, 21, 23, 43];
usersAge.forEach(age=>console.log(`W przyszłym roku użytkownik będzie miał ${age+ 1}lat`))
```

Przykład 2

``` javascript
constusersAge= [20, 21, 23, 43];
letusersTotalAge= 0;
usersAge.forEach(age=>usersTotalAge+= age);
console.log(usersTotalAge);
//zmienna zawiera wartość 107
```

Przykład 3

``` javascript
constusersAge= [20, 21, 23, 43];
constsection= document.createElement('section')
usersAge.forEach((age, index, array) =>{
section.innerHTML+= (
`<h1> Użytkownik ${index+ 1}</h1>
<p>wiek: ${age}</p>`
)
if(index=== array.length-1) {
document.body.appendChild(section);
}
})
```

#### .filter()

Przykład 1

``` javascript
//Zwraca nową tablicę złożoną z tych elementów, przy których iterator zwrócił true
constusers= ["adam", "bogdan", "czarek", "darek"];
constNameWith6Letter= users.filter(user=>user.length=== 6)
console.log(NameWith6Letter);
//["bogdan", "czarek"]
```

Przykład 2 (z wykorzystaniem indexOf)

``` javascript
//Zwraca nową tablicę złożoną z tych elementów, przy których iterator zwrócił true
constusers= ["adam", "bogdan", "czarek", "darek"];
constNameWithLetterK= users.filter((user)=>{
return(
user.indexOf("k") > -1
)
})
console.log(NameWithLetterK);
//["czarek", "darek"]
```

``` javascript
//Zwraca nową tablicę złożoną z tych elementów, przy których iterator zwrócił true
constusers= ["adam", "bogdan", "czarek", "darek"];
constNameWithLetterK= users.filter(user=>user.indexOf("k") > -1)
console.log(NameWithLetterK);
//["czarek", "darek"]
```

#### .findIndex()

``` javascript
// Metoda findIndex zwraca indeks elementu, który jako pierwszy zwróci true (spełnia warunek). Jeśli w żadnej iteracji nie będzie spełniony warunek, to zwróci -1
constcustomers= [
{ name:"Adam", age:67},
{ name:"Basia", age:27},
{ name:"Marta", age:17},
];
constisUsersAdult= customers.findIndex(customer=>customer.age< 18)
console.log(isUsersAdult); //2
```

#### .find()

``` javascript
// Metoda find zwraca element, który jako pierwszy zwróci true (spełnia warunek). Jeśli w żadnej iteracji nie będzie spełniony warunek, to zwróci undefined.
constcustomers= [
{ name:"Adam", age:67},
{ name:"Basia", age:27},
{ name:"Marta", age:17},
];
constfirstAdultUser= customers.find(customer=>customer.age>= 18)
console.log(firstAdultUser); //{name: "Adam", age: 67}
```