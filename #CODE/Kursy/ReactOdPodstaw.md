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

## JavaScript - zagadnienia potrzebne w pracy z React