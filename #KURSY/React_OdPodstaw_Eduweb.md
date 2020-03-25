# React - Podstawy

**React** - biblioteka do tworzenia interfejsów

- Wykorzystuje komponenty
  - `<Button/>`
  - Własny "html" (JSX)
  - Własna logika
  - Własny styl
- React to biblioteka a nie framework bo nie zawiera narzędzi do routingu, walidacji oraz store'u (pamięci), ale społeczność stworzyła narzędzia zastępcze
  - Routing - React Router, Reach Router
  - Walidacja - React Final Form, Formik
  - Store - Redux, Mobx

### Jakie problemy rozwiązuje React?

- Virtual DOM pozwala renderować tylko zmiany zamiast całego DOM
  - Zmiany odbywają się na VDOM
  - Zmiany są porównywane z DOM
  - W DOM wprowadzane są zmiany dotyczące tylko tych elementów, które się zmieniły
- Komponenty
  - Możliwość wielokrotnego wykorzystania

### Aplikacja w React

```javascript
import React from "react";
import ReactDOM from "react-dom";

ReactDOM.render(
  // Rendered element
  <h1>Hello Anna!</h1>,
  // Target
  document.getElementById("root")
);
```

## JSX

**JSX** - cukier syntaktyczny który ułatwia pisanie komponentów React

```javascript
// Ten kod w JSX
ReactDOM.render(
  <h1>Hello Anna!</h1>, // JSX
  document.getElementById("root")
);

// Odpowiada temu
const App = React.createElement(
  "h1", // element
  {
    className: wrapper // propsy, className dla dodawania klas CSS
  },
  "Hello world" // children
);

ReactDOM.render(App, document.getElementById("root"));
```

## Komponent funkcyjny

Każdy komponent warto trzymać w oddzielnym pliku lub katalogu

```javascript
const App = () => (
  <div>
    <h1>Hello, World!</h1>
  </div>
);

ReactDOM.render(
  <App />, // Znacznik JSX renderujący komponent App
  document.getElementById("root")
);
```

Komponent funkcyjny należy wywołać `App()` lub wyrenderować `<App />`. W regularnej pracy stosowana jest zwykle ta druga metoda

```javascript
// 1) Składnia ze słowem kluczowym return
const App = () => {
  return (
    <div className="wrapper">
      <h1>Hello, World!</h1>
      <h2>Hello, Anna!</h2>
    </div>
  );
};

// 2) Implicit return dzięki składni ES6 bez słowa kluczowego return
const App = () => (
  <div className="wrapper">
    <h1>Hello, World!</h1>
    <h2>Hello, Anna!</h2>
  </div>
);

ReactDOM.render(<App />, document.getElementById("root"));
```

## Importy i exporty w ES modules

### Named export

Zawsze używamy takiej samej nazwy zmiennej jaką eksportowaliśmy

```javascript
// Eksport
export const App = () =>  {
	return(
		<div className="wrapper">
			<h1>Hello, World!</h1>
			<h2>Hello, Anna!</h2>
		</div>
	)
}

// Import
import { App } form ./App;
import { App, name } form './App'; // Nazwy komponnetów po przecinku jeśli kilka modułów
```

```javascript
// Eksport
export const App = () =>  {
	return(
		<div className="wrapper">
			<h1>Hello, World!</h1>
			<h2>Hello, Anna!</h2>
		</div>
	)
}

// Import z 'as'
import { App as ReactApp } form './App';
```

### Default export

```javascript
// Eksport
const App = () =>  {
	return(
		<div className="wrapper">
			<h1>Hello, World!</h1>
			<h2>Hello, Anna!</h2>
		</div>
	)
}

export default App;

// Import
import App form './App';
```
