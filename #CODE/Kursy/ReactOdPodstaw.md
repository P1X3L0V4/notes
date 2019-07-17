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

* W poniższym przykłądzie `this ` będzie wskazywało na `window `(obiekt globalny) ponieważ funkcja strzałkowa nie tworzy własnego przypisania wiązania `this`, a zamiast
tego dziedziczy je (przejmuje `this`, który istnieje we wcześniejszym
kontekście)

``` javascript
const btn = document.querySelector('button');
btn.addEventListener('click', () => console.log(this));
```

* W poniższym przykłądzie `this ` będzie wskazywało na obiekt, na którym wywołane zostało zdarzenie

``` javascript
const btn = document.querySelector('button')
btn.addEventListener('click', function() {
console.log(this)
})
```