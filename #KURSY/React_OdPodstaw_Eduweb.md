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

JSX wymaga aby każdy element HTML renderowany w kodzie był opleciony jakimś elementem nadrzędnym. Wcześniej oplatano tagi elementami

- `<div></div>`
- `<React.Fragment></React.Fragment>`

Aktualnie stosuje się:

- `<></>`

```javascript
class MyComponent extends React.Component {
  render() {
    return (
      <>
        <input placeholder="Your text" value={this.state.text} />
        <h1>{this.state.text}</h1>
      </>
    );
  }
}
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

## Aplikacja Twitter Quotes

Zastosowane mechanizmy

- Komponent prywatny
- Mapowanie propsów za pomocą `map()`
- Wykorzystanie operatora spread `...` do rozciągnięcia propsów
- Wykorzystanie destrukturyzacji w `ListItem`

```javascript
// index.js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```

```javascript
// App.js
import React from "react";
import ListWrapper from "./components/ListWrapper/ListWrapper";
import "./index.css";

const App = () => (
  <div>
    <ListWrapper />
  </div>
);

export default App;
```

```javascript
// components/ListWrapper/ListWrapper.js

import React from "react";
import ListItem from "./ListItem/ListItem";
import "./ListWrapper.css";
import { twitterAccounts } from "../../data/twitterAccounts";

const ListWrapper = () => (
  <ul className="listWrapper__wrapper">
    {twitterAccounts.map(item => (
      <ListItem key={item.name} {...item} />
    ))}
  </ul>
);

export default ListWrapper;
```

Każdy element który mapujemy musi mieć wartość `key` stąd w kodzie `<ListItem key={item.name} {...item} />`

```javascript
// components/ListWrapper/ListItem/ListItem.js

import React from "react";
import PropTypes from "prop-types";
import "./ListItem.css";

const ListItem = ({ image, name, description, twitterLink }) => (
  <li className="listItem__wrapper">
    <img src={image} className="listItem__image" alt={name} />
    <div>
      <h2 className="listItem__name">{name}</h2>
      <p className="listItem__description">{description}</p>
      <a href={twitterLink} className="listItem__button">
        visit twitter page
      </a>
    </div>
  </li>
);

ListItem.propTypes = {
  image: PropTypes.string.isRequired,
  name: PropTypes.string.isRequired,
  description: PropTypes.string,
  twitterLink: PropTypes.string.isRequired
};

ListItem.defaultProps = {
  description: "One of the React creators"
};

export default ListItem;
```

```css
/* CSS */
/* index.css */
@import url("https://fonts.googleapis.com/css?family=Montserrat:300,500,700");

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family: "Montserrat", sans-serif;
}
```

```css
/* components/ListWrapper/ListItem/ListItem.css */

.listItem__wrapper {
  list-style: none;
  padding: 50px 30px;
  display: flex;
  align-items: center;
}

.listItem__image {
  flex-shrink: 0;
  margin-right: 30px;
  width: 150px;
  height: 150px;
  border-radius: 50%;
}

.listItem__name {
  margin: 0;
  color: #1e58ff;
  font-weight: 700;
}

.listItem__description {
  margin: 10px 0 20px;
  font-weight: 300;
}

.listItem__button {
  font-size: 10px;
  text-decoration: none;
  padding: 7px 12px;
  font-weight: 500;
  background: none;
  border: 2px solid #1e58ff;
  color: #1e58ff;
}
```

### BEM

**BEM** - Block Element Modifier. Metody nazywania klas, która pozwala uniknąć konfliktów między komponentami. Adres strony: http://getbem.com/

## Props

### Dodawanie props

```javascript
const ListWrapper = () => (
  <ul className="listWrapper__wrapper">
    <ListItem
      // Dodajemy propsy o dowolnych nazwach np. name, description, image
      name={twitterAccounts[0].name}
      description={twitterAccounts[0].description}
      image={twitterAccounts[0].image}
    />
  </ul>
);

export default ListWrapper;
```

```javascript
// Wskazujemy, że komponent przyjmuje props
const ListItem = props => (
  <li className="listItem__wrapper">
    <img src={props.image} className="listItem__image" />
    <div>
      <h2 className="listItem__name">{props.name}</h2>
      <p className="listItem__description">{props.description}</p>
      <button className="listItem__button">visit twitter page</button>
    </div>
  </li>
);
```

## PropTypes

**PropTypes** - Narzędzie, które pozwala nam weryfikować jakiego rodzaju propsy podajemy do naszego komponentu i czy są one odpowiedniego typu.

```javascript
ListItem.propTypes = {
  image: PropTypes.string.isRequired,
  name: PropTypes.string.isRequired,
  description: PropTypes.string,
  twitterLink: PropTypes.string.isRequired
};

ListItem.defaultProps = {
  description: "One of the React creators"
};
```

`.defaultProps` - służą wskazaniu wartości domyślnych dla propsów

`.propTypes` - służy określaniu zasad dla propsów

## Komponenty klasowe (Statefull Components)

Komponenty klasowe udostępniają funkcje

- Stan (State) - narzędzie służące do dynamicznej zmiany zawartości komponentów
- Life Cycle Functions

```javascript
import React from "react";

// Tworzenie komponentu klasowego
class MyComponent extends React.Component {
  // Dodawanie stanu
  state = {
    text: ""
  };

  // Funkcja obsługująca event onChange={this.handleChange}
  handleChange = e => {
    this.setState({ text: e.target.value.toUpperCase() });
  };

  render() {
    return (
      <>
        <input
          placeholder="Your text"
          onChange={this.handleChange}
          value={this.state.text}
        />
        <h1>{this.state.text}</h1>
      </-->
    );
  }
}

export default MyComponent;
```
