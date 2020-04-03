# Eduweb - React od podstaw

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

## Inicjalizacja projektu

```bash
npx create-react-app my-app
cd my-app
npm start
```

### Aplikacja z Create React App

Starsza składnia

<!-- prettier-ignore -->
```JSX
// Wzór
const App = React.createElement(
  element,
  propsy,
  ...children = zawartość elementu
)

// Przykład
const App = React.createElement(
'h1',
{
  className: "nazwa_klasy",
  items: "2",
},
'Hello World!',
)
```

Korzystamy z Create React App: https://github.com/facebook/create-react-app

```JSX
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

```JSX
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

```JSX
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

**UWAGA:** Aby w plikach JSX wykonać jakiekolwiek wyrażenia JSX'owe należy wykorzystać nawiasy klamrowe `{ code }`

## Komponent funkcyjny

### Tworzenie komponentu funkcyjnego

Dobra praktyka: Każdy komponent warto trzymać w oddzielnym pliku lub katalogu

```JSX
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

```JSX
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

- Zawsze używamy takiej samej nazwy zmiennej jaką eksportowaliśmy
- Możliwe obejście tej zasady poprzez zastosowanie `as`
- Wiele eksportów na jeden plik

```JSX
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

```JSX
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

- Tylko jeden export na cały plik

```JSX
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

## Komponenty prywatne i publiczne

- **Komponent prywatny** - komponent, który wykorzystywany jest wyłącznie przez jeden komponent nadrzędny
- **Komponent publiczny** - komponent, który wykorzystywany jest w innych komponentach naszej aplikacji

## Aplikacja Twitter Quotes

Zastosowane mechanizmy

- Komponent prywatny
- Metodyka nazewnictwa klas CSS BEM
- Mapowanie propsów za pomocą `map()`
- Wykorzystanie operatora spread `...` do rozciągnięcia propsów
- Wykorzystanie destrukturyzacji w `ListItem`
- Wykorzystanie nawiasów klamrowych do zapisu wyrażeń JS w plikach React

```JSX
// Plik index.js

import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```

```JSX
// Plik App.js

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

```JSX
// Plik components/ListWrapper/ListWrapper.js

import React from "react";
import ListItem from "./ListItem/ListItem";
import "./ListWrapper.css";
import { twitterAccounts } from "../../data/twitterAccounts";

const ListWrapper = () => (
  <ul className="listWrapper__wrapper">
    <ListItem
      name={twitterAccounts[0].name}
      description={twitterAccounts[0].description}
      image={twitterAccounts[0].image}
    />
    <ListItem
      name={twitterAccounts[1].name}
      description={twitterAccounts[1].description}
      image={twitterAccounts[1].image}
    />
    <ListItem
      name={twitterAccounts[2].name}
      description={twitterAccounts[2].description}
      image={twitterAccounts[2].image}
    />
    <ListItem
      name={twitterAccounts[3].name}
      description={twitterAccounts[3].description}
      image={twitterAccounts[3].image}
    />
  </ul>
);

export default ListWrapper;
```

```JSX
// Plik components/ListWrapper/ListItem/ListItem.js

import React from "react";
import "./ListItem.css";
import danAbramovImage from "../../../assets/images/danabramov.jpg";

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

export default ListItem;
```

```css
/* CSS */
/* Plik index.css */
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
/*Plik components/ListWrapper/ListWrapper.css*/

.listWrapper__wrapper {
  width: 80vw;
  margin: 100px auto 0;
}
```

```css
/* Plik components/ListWrapper/ListItem/ListItem.css */

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
  padding: 7px 12px;
  font-weight: 500;
  background: none;
  border: 2px solid #1e58ff;
  color: #1e58ff;
}
```

### BEM

**BEM (Block Element Modifier)** - metodyka nazywania zmiennych według schematu `Block__Element-Modifier`, która pozwala uniknąć konfliktów w kodzie. Więcej informacji: http://getbem.com/

## Props

### Dodawanie props

- W miejscu definiowania komponentu wskazujemy, że komponent przyjmuje props `const ListItem = props => (`
- W kodzie komponentu wykorzystujemy propsy np. `{props.image}`

```JSX
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

- W komponencie nadrzędnym (rodzicu) przypisujemy propsom wartości dla danej instancji komponentu np. `name={twitterAccounts[0].name}`

```JSX
const ListWrapper = () => (
  <ul className="listWrapper__wrapper">
    <ListItem
      name={twitterAccounts[0].name}
      description={twitterAccounts[0].description}
      image={twitterAccounts[0].image}
    />
  </ul>
);

export default ListWrapper;
```

## Mapowanie tablicy w React

- Mapujemy tablicę z danymi aby działać w zgodzie z zasadą DRY (Don't Repeat Yourself)
- Wewnątrz `map()` odwołujemy się do `item` bo tak nazywa się element tablicy w tym kontekście `{item.name}`

```JSX
// Plik components/ListWrapper/ListWrapper.js

import React from "react";
import ListItem from "./ListItem/ListItem";
import "./ListWrapper.css";
import { twitterAccounts } from "../../data/twitterAccounts";

const ListWrapper = () => (
  <ul className="listWrapper__wrapper">
    {twitterAccounts.map(item => (
      <ListItem
        name={item.name}
        description={item.description}
        image={item.image}
        link={item.twitterLink}
      />
    ))}
  </ul>
);

export default ListWrapper;
```

### Refactoring aplikacji

Destrukturyzacja propsów w `ListWrapper` (Wariant 1)

- `item` zmieniamy na `{name, description, image, twitterLink}`
- `item.name` na `name`
- `item.description` na `description`
- `item.image` na `image`
- `item.twitterLink` na `twitterLink`

```JSX
const ListWrapper = () => (
  <ul className="listWrapper__wrapper">
    {twitterAccounts.map(({ name, description, image, twitterLink }) => (
      <ListItem
        name={name}
        description={description}
        image={image}
        link={twitterLink}
      />
    ))}
  </ul>
);
```

Alternatywnie: Wykorzystanie spread operatora w `ListWrapper` (Wariant 2)

- Wykorzystujemy `spread operator` w postaci `...items`, który rozsmarowuje wartości tablicy
- - Każdy element który mapujemy musi mieć wartość `key` stąd w kodzie `<ListItem key={item.name} {...item} />`

```JSX
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

Destrukturyzacja propsów w `ListItem`

- `props` zamieniamy na `{ image, name, description, twitterLink }`
- nazwy propsów z `{prosps.nazwapropsa}` zamieniamy na `{nazwapropsa}` np. `{description}`

```JSX
import React from "react";
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

export default ListItem;
```

## PropTypes

**PropTypes** - Narzędzie, które pozwala nam weryfikować jakiego rodzaju propsy podajemy do naszego komponentu i czy są one odpowiedniego typu.

- `.defaultProps` - służą wskazaniu wartości domyślnych dla propsów
- `.propTypes` - służy określaniu zasad dla propsów

Struktura dla `PropTypes`

```
PropTypes.nazwaTypuDanych.isRequired(opcjonalnie)
```

```JSX
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

## Komponenty klasowe (Statefull Components)

**Komponenty klasowe (Statefull Components)** - Ich polska nazwa wynika z tego, że wykorzystują notację klasy znaną z ES6

`React.Component` udostępnia dwie możliwości:

- Stan (State) - narzędzie służące do dynamicznej zmiany zawartości komponentów
- Life Cycle Functions

```JSX
import React from "react";

// Tworzenie komponentu klasowego
class MyComponent extends React.Component {
  // Dodawanie stanu
  state = {
    text: ""
  };

  // Funkcja obsługująca event onChange={this.handleChange}
  handleChange = e => {
    // setState - metoda wbudowana zmieniająca stan podajemy klucz : nowa_wartość
    this.setState({ text: e.target.value.toUpperCase() });
  };

  // Wykorzystanie funkcji render() która pozwala wyświetlać elementy do widoku aplikacji
  render() {
    return (
      // Oplatamy JSX we fragment <></>
      <>
        <input
          placeholder="Your text"
          onChange={this.handleChange}
          value={this.state.text}
        />
        <h1>{this.state.text}</h1>
      </>
    );
  }
}

export default MyComponent;
```

### Stary zapis komponentów klasowych

```JSX
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      text: '';
    }

  }
}
```

### Inny zapis deklaracji funkcji

```JSX
class MyComponent extends React.Component {
  state = {
    text: ""
  };

  // Bind dodany aby nadać this odpowiedni kontekst w funkcji handleChange(e)
  this.handleChange = this.handleChange.bind(this);

  // Alternatywny zapis deklaracji funkcji (pomijamy słowo kluczowe function)
  // Uwaga! this ma tu inny kontekst niż w funkcji strzałkowej
  handleChange(e) {
    this.setState({ text: e.target.value.toUpperCase() });
  }

  render() {
    return (
      <>
        <input
          placeholder="Your text"
          onChange={this.handleChange}
          value={this.state.text}
        />
        <h1>{this.state.text}</h1>
      </>
    );
  }
}
```

Zastosowanie `class properties` pozwala zapomnieć o konstruktorze

Paczka do obsługi `propsal class properties`: https://babeljs.io/docs/en/babel-plugin-proposal-class-properties

## State

**State (stan)** - pozwala na wprowadzanie dynamicznych zmian w komponentach.

Jak pracować ze state:

- Zmieniamy state poprzez wbudowaną metodę `setState()` np. `this.setState({ text: e.target.value.toUpperCase() });`
- Tworzymy funkcję zmieniającą state np. `handleChange = e => { ... }`
- Funkcję podpisany do zdarzenia np `onClick` lub `onChange` np. `onChange={this.handleChange}`
- Value pola opieramy o state `value={this.state.text}` tak by wartość pola była dynamicznie podmieniana

Mechanizm działania (kolejność):

- Odpala się `event`
- Event podmienia `state`
- State podmienia `value` w naszym `<input>`

## Funkcje strzałkowe w React

React korzysta często z funkcji strzałkowych ponieważ

- zachowują one kontekst `this`
- przy funkcjach tradycyjnych `handleChange(e){}` konieczne było bindowanie odpowiedniego kontekstu dla `this` poprzez dodanie `this.handleChange = this.handleChange.bind(this)` co przy wielu funkcjach zwiększało znacznie ilość kodu

## Dodawanie elementu do listy

```JSX
addItem = e => {
  e.preventDefault();

  const newItem = {
    name: e.target[0].value,
    twitterLink: e.target[1].value,
    image: e.target[2].value,
    description: e.target[3].value
  };

  this.setState(prevState => ({
    items: [...prevState.items, newItem] // prevState.items ze spread operatorem potrzebne by nie usunąć poprzednich elemnetów
  }));

  e.target.reset(); // resetujemy formularz
};
```

## Przesyłanie danych w górę (od dzieci do rodzica)

- Możemy podawać funkcje jako propsy
- Do funkcji możemy przekazać argumenty, które wrócą do rodzica

### Przykładowy mechanizm

- W rodzicu funkcję `addItem()`
- W rodzicu w `render()` przekazujemy funkcję jako propsa `<Form submitFn={this.addItem} />`

```JSX
// Plik (fragment) src/App.js

class App extends React.Component {
  state = {
    items: [...initialStateItems]
  };
  // Funkcja addItem
  addItem = e => {
    e.preventDefault();
    console.log(e.target[0].value);
    console.log(e.target[1].value);
    console.log(e.target[2].value);
    console.log(e.target[3].value);
  };

  // W render() przekazujemy naszą funkcję jako propsa <Form submitFn={this.addItem} />
  render() {
    return (
      <div>
        <ListWrapper items={this.state.items} />
        <Form submitFn={this.addItem} />
      </div>
    );
  }
}
```

W komponencie dziecku

- Wyciągamy propsa `submitFn` za pomocą destrukturyzacji `{ submitFn }`
- Do formularza dodajemy zdarzenie z naszym propsem w postaci funkcji `<form onSubmit={submitFn}>`
- Upewniamy się, że `<button>` w formularzu ma odpowiedni typ `<button type="submit">`

```JSX
// Plik src/components/Form/Form.js

import React from "react";

const Form = ({ submitFn }) => (
  <form onSubmit={submitFn}>
    <input placeholder="name" name="name" />
    <input placeholder="link" name="link" />
    <input placeholder="image" name="image" />
    <textarea placeholder="description" name="description" />
    <button type="submit">add new item</button>
  </form>
);

export default Form;
```

### Funkcja dodająca element do listy

```JSX
addItem = e => {
  // Zapobiegamy domyślnemu zdarzeniu jakim jest przełądowanie okna przeglądarki
  e.preventDefault();

  // Tworzyemy zmienną newItem ze wszystkimi polami z formularza
  const newItem = {
    name: e.target[0].value,
    twitterLink: e.target[1].value,
    image: e.target[2].value,
    description: e.target[3].value
  };

  // Zmieniamy state komponentu App na poprzednie elementy + newItem
  // Wykorzystujemy funkcję prevState (zalecana praktyka)
  this.setState(prevState => ({
    items: [...prevState.items, newItem]
  }));

  // Resetujemy formularz
  e.target.reset();
};
```

## Debugowanie

- Usunąć katalog `node_modules` z aplikacji
- Usunąć `package-lock.json` lub `yarn.lock`
- Jeśli występuje konflikt z paczką warto sprawdzić też katalog globalny `node_modules`

## Dodawanie CSS Modules i SCSS do aplikacji

```bash
# Instalacja
npm install node-sass --save
```

Jeśli wykorzystujemy `Create React App` to instalacja według instrukcji: https://create-react-app.dev/docs/adding-a-sass-stylesheet/

CSS Modules umożliwia tworzenie takich samych nazw klas dla wielu elementów, które następnie są kompilowane do nazw z sufixem w postaci losowego ciągu znaków, które powodują, że każdy element ma docelowo unikalną nazwę klasy.

```JSX
import React from "react";
// Importujemy obiekt styles z danego pliku scss
import styles from "./Form.module.scss";
// Nazwę obiektu ze stylami z importu i po kropce nazwa klasy
<div className={styles.wrapper}>
```

## `Target _blank`

Do `target="_black"` według dobrych praktyk należy dodać `rel=noopener norefeer`

## Animacje

Link do artykułu: https://css-tricks.com/snippets/css/keyframe-animation-syntax/

```css
@keyframes appear {
  0% {
    opacity: 0;
    top: 35px;
  }
  100% {
    opacity: 1;
    top: 0;
  }
}

/* Animowany element dostaje własność animation */
.wrapper {
  animation: appear 0.5s ease;
}
```

## Zmienna warunkująca użycie tagu

W React mamy możliwość zastosowania zmiennej warunkującej jaki tag HTML zostanie wykorzystany w wyrenderowanym kodzie.

```JSX
// Zmienna warunkowa z ternary operator
const ImageTag = image ? "img" : "div";

/* Tag HTML (JSX) ze zmienną ImageTag warunkująca użycie img lub div oraz w className klasa styles.image dla elementu jeśli jest img lub styles.imageNone jeśli brak */
<ImageTag
  src={image}
  className={image ? styles.image : styles.imageNone}
  alt={name}
/>;
```

## Zmiana styli w zależności od rodzaju elementu

Jeśli `image` istnieje to dostaje klasę `styles.image` a jeśli nie to `styles.imageNone`

```JSX
<ImageTag
  src={image}
  className={image ? styles.image : styles.imageNone}
  alt={name}
/>
```

## Placeholdery dla obrazków

https://picsum.photos/

```
https://picsum.photos/200/300
```

Unsplash

```
https://unsplash.it/200/200
```

## Ekstrakcja komponentów

Na tym etapie najgorzej zaprojektowanym elementem aplikacji jest `Form`, w którym powtarzamy wielokrotnie tagi `input`. Warto zmienić je na dynamiczny komponent do którego przekazywać będziemy propsy.

- Tworzymy komponent `<Input>` i odpowiadające mu style w pliku `Input.module.scss`
- Sprawdzamy jakie elementy naszego formularza powinny być dynamiczne. W tym przypadku jest to tag, który raz będzie `input` innym razem np. `text-area`
- Do dynamicznej zmiany tagu wykorzystujemy element `<Tag />`
- Do refaktoryzacji wykorzystujemy propsy
- Destrukturyzujemy propsy `{ tag: Tag, name, label, maxLength }`
- Pobieramy `propTypes` poprzez `import PropTypes from "prop-types";`
- Tworzymy propTypes dla naszego komponentu `Input.propTypes = {}`
- Tworzymy domyśle wartości dla propsów `Input.defaultProps = {}`
- Ponieważ zmieniamy nazwę komponentu na niegeneryczną (nieHMTLową) z `<input>` na `Tag` to musi być ona napisana wielką literą co ustawiamy za pomocą `{ tag: Tag }`. Jest to zmiana nazwy propsa wewnątrz komponentu.
- W `<label>` używamy `htmlFor` ponieważ `for` jest słowem zastrzeżonym w Javascripcie dla pętli
- Odpowiednie style umieszczamy w pliku `Input.module.scss`
- W `<Tag className>` sprawdzamy czy element jest `input` czy `textarea` i przydzielamy odpowiednią klasę za pomocą `ternary operator`

```JSX
// Plik src/components/Input/Input.js

import React from "react";
import PropTypes from "prop-types";
import styles from "./Input.module.scss";

const Input = ({ tag: Tag, name, label, maxLength }) => (
  <div className={styles.formItem}>
    <Tag
      className={Tag === "textarea" ? styles.textarea : styles.input}
      type="text"
      name={name}
      id={name}
      required
      maxLength={maxLength}
      placeholder=" "
    />
    <label className={styles.label} htmlFor={name}>
      {label}
    </label>
    <div className={styles.formItemBar} />
  </div>
);

Input.propTypes = {
  tag: PropTypes.string,
  name: PropTypes.string.isRequired,
  label: PropTypes.string.isRequired,
  maxLength: PropTypes.number
};

Input.defaultProps = {
  tag: "input",
  maxLength: 200
};

export default Input;
```

```JSX
// Plik src/components/Form/Form.js

import React from "react";
import styles from "./Form.module.scss";
import Input from "../Input/Input";

const Form = ({ submitFn }) => (
  <div className={styles.wrapper}>
    <h2>Add new twitter account</h2>
    <form autoComplete="off" className={styles.form} onSubmit={submitFn}>
      <Input name="name" label="Name" maxLength={30} />
      <Input name="link" label="Twitter link" />
      <Input name="image" label="Image" />
      <Input tag="textarea" name="description" label="Description" />
      <button className={styles.button}>add new item</button>
    </form>
  </div>
);

export default Form;
```

## Props children i renderowanie warunkowe

**children** - specjalny props, który wskazuje na dzieci elementu np. jeśli mamy tag `<button>abc</button>` to `abc` będzie `children` dla tagu `<button>`

- Funkcja `React.createElement()` jako jeden z parametrów przyjmuje specjalny props `children`
- Ponieważ chcemy aby nasz komponent `Button` miał zastosowanie zarówno w linkach utworzonych za pomocą `<button>` jak i zwykłego tagu `<a>` wykorzystujemy `ternary operator` do stworzenia warunku - jeśli mamy atrybut `href` to generujemy tag `<a>`, w przeciwnym razie generujemy `<button>` np. `{href ? ( <a></a> ) : ( <button></button> ) }
- Kod warunku umieszczamy w nawiasach klamrowych

```JSX
// Plik Plik src/components/Button/Button.js

import React from 'react';
import styles from './Button.module.scss';

const Button = ({ children, href }) => (
  <>
    {
      href ? (
        <a
          href={href}
          target="_blank"
          className={styles.button}
          rel="noopener noreferrer"
        >
          {children}
        </a>
      ) : (
          <button className={styles.button}>
            {children}
          </button>
        )
    }
  </>
);

export default Button;
```

Tekst `visit twitter page` jest podstawiany właśnie w miejsce propsa `children`

```html
<button href="{twitterLink}">
  visit twitter page
</button>
```

## Routing

**Routing** - czynność polegająca na kierowaniu drogą przepływu pakietów informacji w sieci komputerowej, czyli wyznaczanie odpowiedniej ścieżki.

Komunikacja ze serwerem w przypadku aplikacji opartych o React wygląda inaczej niż w przypadku statycznych stron internetowych. Jeśli użytkownik wysyła `request` o podstronę `myapp.com/about` to najprawdopodobniej nie będzie się ona znajdować na serwerze w postaci pliku `about.html`, ale będzie w plikach `.js` aplikacji, które trzeba wyrenderować.

Sam React nie posiada w swoich zasobach narzędzia odpowiedzialnego za Routing więc musimy skorzystać z zewnętrznej biblioteki np. `React Router`

Zadaniem `React Router` jest pośredniczenie (przechwytywanie requestu) i poprawne renderowanie potrzebnych podstron i elementów aplikacji, które znajdują się w plikach JSX.

## Widoki (Views)

**Widoki (Views)**

- Widoki aplikacji składające się z komponentów
- Nie mogę być reużywane
- Najczęściej tworzymy nowe widok dla poszczególnych podstron

### Tworzenie nowego widoku

```bash
# Instalacja react-router i react-router-dom

npm install --save react-router
npm install --save react-router-dom
```

- W folderze `views` aplikacji dodajemy folder z nazwą nowego widoku np. `TwitterView` i wewnątrz niego plikiem skryptu `TwitterView.js`
- W pliku głównym aplikacji `Root.js` przemianowanym z `App.js`
  - Importujemy `react-router` oraz `react-router-dom` za pomocą `import { BrowserRouter, Route } from "react-router-dom";`
  - Importujemy wszystkie widoki

```JSX
import React from "react";
import "./index.css";
import { BrowserRouter, Route } from "react-router-dom";
import TwittersView from "../TwittersView/TwittersView";
import ArticlesView from "../ArticlesView/ArticlesView";
import NotesView from "../NotesView/NotesView";
```

- W kodzie `Root` dodajemy `<BrowserRouter></BrowserRouter>`

### Browser Router

- Odpowiada za właściwe nawigowanie po naszej aplikacji w przeglądarce
- Powinien mieć tylko jedno dziecko (opakowane we "fragment" `<></>`)

```JSX
<BrowserRouter>
  <>
    <h1>Costam</h1>
  </>
</BrowserRouter>
```

- Za pomocą komponentu `<Route>` opisujemy ścieżki aplikacji

## Route

- Komponent służy do wskazywania ścieżek w aplikacji
- `<Route>` przyjmuje propsa o nazwie `<path>` w którym podajemy ścieżkę jako string
- `<Route>` przyjmuje propsa o nazwie `<component>` w którym podajemy nazwę widoku do wyrenderowania

Działanie: jeśli jesteśmy na ścieżce i spełniamy warunek zawarty w `path=""` to wyświetlamy to co zawiera `component`

```html
render() {
  return (
    <BrowserRouter>
      <>
        <Navigation />
        <h1>hello world</h1>
        <Switch>
          <Route exact path="/" component={TwittersView} />
          <Route path="/articles" component={ArticlesView} />
          <Route path="/notes" component={NotesView} />
        </Switch>
      </>
    </BrowserRouter>
  );
}
```

`React Router` został zaprojektowany w taki sposób by wyświetlać wiele komponentów na jednej ścieżce na zasadzie warunków łącznych. Jeśli chcemy zmienić sposób wyświetlania musimy użyć:

- Propsa `exact`, któy działa w ten sposób, że widok będzie renderowany tylko i wyłącznie przy podanej ścieżce lub
- Bardziej zaawansowanego komponentu `<Switch></Switch>`

## Switch

Komponent `<Switch></Switch>` renderuje ścieżki na zasadzie wymienności tzn. jeśli renderowany jest jeden komponent to nawet jeśli drugi spełnia warunek ścieżki to i tak nie zostanie wyrenderowany.

Jest to przydatne w przypadku ścieżek typu `/notes` i `/notes:id` dla których nie chcemy podwójnie wyświetlać tego samego widoku.

Element `Switch` należy zaimportować z `'react-router-dom'` za pomocą `import { BrowserRouter, Route, Switch } from 'react-router-dom';`

```JSX
// Plik src/views/Root/Root.js

import React from "react";
import "./index.css";
import { BrowserRouter, Route, Switch } from 'react-router-dom';
import TwittersView from '../TwittersView/TwittersView';
import ArticlesView from '../ArticlesView/ArticlesView';
import NotesView from '../NotesView/NotesView';
import Navigation from '../../components/Navigation/Navigation';
```

```html
<Switch>
  <Route exact path="/" component="{TwittersView}" />
  <Route path="/articles" component="{ArticlesView}" />
  <Route path="/notes" component="{NotesView}" />
</Switch>
```

## Nawigacja

### Link

`<Link></Link>` pomaga przechwycić zapytanie do serwera i wyrenderować widok strony z plików `.js` bez przeładowywania całej strony

```JSX
// Plik src/components/Navigation/Navigation.js

import React from "react";
import { Link } from "react-router-dom";

const Navigation = () => (
  <ul>
    <li><Link to="/">Twitters</Link></li>
    <li><Link to="/articles">Articles</Link></li>
    <li><Link to="/notes">Notes</Link></li>
  </ul>
);

export default Navigation;
```

### NavLink

**NavLink** - moduł do tworzenia nawigacji. Przyjmuje dodatkowego propsa `activeClassName` pozwalającego zmienić klasę w zależności od stanu linka.

- Importujemy `NavLink` za pomocą `import { NavLink } from 'react-router-dom';`
- Do pierwszego `<NavLink>` dodajemy atrybut `exact` aby style były wyświetlane tylko dla strony głównej a nie dla wszystkich podstron

```JSX
// Plik /src/components/Navigation/Navigation.js

import React from 'react';
import { NavLink } from 'react-router-dom';
import styles from './Navigation.module.scss';

const Navigation = () => (
  <nav>
    <ul className={styles.wrapper}>
      <li className={styles.navItem}>
      <NavLink exact
      activeClassName={styles.navItemLinkActive}
      className={styles.navItemLink} to="/">twitters</NavLink>
      </li>
      <li className={styles.navItem}>
      <NavLink
      activeClassName={styles.navItemLinkActive}
      className={styles.navItemLink} to="/articles">articles</NavLink>
      </li>
      <li className={styles.navItem}>
      <NavLink
      activeClassName={styles.navItemLinkActive}
      className={styles.navItemLink} to="/notes">notes</NavLink>
      </li>
    </ul>
  </nav>
);

export default Navigation;
```

## Dodawanie dodatkowych propsów

- Props `secondary` to sposób na dodanie alternatywnego stylu dla elementu przy pomocy `true/false`
- Ostatnia wartość `...props` dodaje do komponentu wszystkie brakujące propsy np. ze zdarzeń takich jak `onClick` czy `onChange`

```JSX
const Button = ({ children, href, secondary, ...props }) => {};
```

```JSX
const buttonClass = secondary ? styles.secondary : styles.button;
```

```html
<button secondary>Item</button>
```

## Modal

```JSX
// Plik /src/components/Modal/Modal.js

import React from 'react';
import styles from './Modal.module.scss';
import Form from '../Form/Form';

const Modal = () => (
  <div className={styles.wrapper}>
    <Form />
  </div>
);

export default Modal;
```

```css
/* Plik src/components/Modal/Modal.module.scss */

.wrapper {
  padding: 70px 80px 0;
  top: 50%;
  transform: translateY(-50%);
  left: 0;
  right: 0;
  margin: 0 auto;
  width: 60vw;
  height: 70vh;
  background-color: white;
  box-shadow: 0 20px 40px -5px rgba(#1e58ff, 0.3);
  position: fixed;
}
```

### Otwieranie i zamykanie modala

W `state` dla pliku `Root.js` dodajemy `isModalOpen`

```JSX
state = {
  items: [...initialStateItems],
  isModalOpen: false
};
```

W miejscu gdzie renderujemy `Modal` dodajemy renderowanie warunkowe

```JSX
{
  isModalOpen && <Modal closeModalFn={this.closeModal} />;
}
```

Zamiast pisać `this.state.isModalOpen` używamy destrukturyzacji w funkcji `render()`

```JSX
const { isModalOpen } = this.state;
```

#### Funkcja otwierająca modal

```JSX
openModal = () => {
  this.setState({
    isModalOpen: true
  });
};
```

Przekazujemy ją do `<Header>` w którym znajduje się nasz `<Button>`

```JSX
<Header openModalFn={this.openModal} />
```

Dodajemy kod w pliku z `<Header>`

- Dodajemy destrukturyzację `{ openModalFn }` jako atrybut
- Do `<Button>` dodajemy `onClick={openModalFn}`

```JSX
const Header = ({ openModalFn }) => (
  <header className={styles.wrapper}>
    <img className={styles.logo} src={logoImage} alt="FavNote logo" />
    <HeaderNavigation />
    <Button onClick={openModalFn} secondary>
      new item
    </Button>
  </header>
);
```

W tym miejscu należy pamiętać, że nasz `<Button>` nie jest generycznym elementem HTML ale kolejnym komponentem, któremu podajemy w tej sytuacji nowego propsa. Tego typu dodatkowe propsy należy przekazać w postaci `...props` w komponencie `<Button>`.

```JSX
const Button = ({ children, href, secondary, ...props }) => {}
```

```html
<button className="{buttonClass}" {...props}>
  {children}
</button>
```

#### Funkcja zamykająca modal

```JSX
closeModal = () => {
  this.setState({
    isModalOpen: false
  });
};
```

Przekazujemy ją do naszego komponentu `Modal`

```JSX
{
  isModalOpen && <Modal closeModalFn={this.closeModal} />;
}
```

W pliku `Modal.js` :

- Dodajemy destrukturyzację `{ closeModalFn }` jako atrybut
- Do `<button>` dodajemy `onClick={closeModalFn}`

```JSX
const Modal = ({ closeModalFn }) => (
  <div className={styles.wrapper}>
    <button onClick={closeModalFn}>close me</button>
    <Form />
  </div>
);
```

## Dynamika formularza

- Zmiana komponentu na stanowy
- Dodana zmienna `types` dla rodzajów wpisów
- Dodana zmienna `descriptions` dla nagłówków
- Dodajemy `<input type="radio">` dla każdej opcji
- Dla każdego `<input type="radio">` dodajemy funkcję `onChange={() => this.handleRadioButtonChange(types.nazwa)}` odpowiedzialną za zmianę stanu
- Dodajemy kod odpowiedzialny za to czy nasz element radio będzie zaznaczony `checked={this.state.activeOption === types.twitter}`

```JSX
// Plik  src/components/Form/Form.js

import React from "react";
import styles from "./Form.module.scss";
import Input from "../Input/Input";
import Button from '../Button/Button';
import Title from '../Title/Title';

const types = {
  twitter: 'twitter',
  article: 'article',
  note: 'note',
}

const descriptions = {
  twitter: 'favorite Twitter account',
  article: 'Article',
  note: 'Note',
}

class Form extends React.Component {
  state = {
    activeOption: types.twitter,
  }

  handleRadioButtonChange = (type) => {
    this.setState({
      activeOption: type,
    })
  }

  render() {
    return (
      <div className={styles.wrapper}>
        <Title>Add new {descriptions[this.state.activeOption]}</Title>
        <form autoComplete="off" className={styles.form} onSubmit={this.props.submitFn}>
          <input
            id={types.twitter}
            type="radio"
            checked={this.state.activeOption === types.twitter}
            onChange={() => this.handleRadioButtonChange(types.twitter)}
          />
          <label for={types.twitter}>Twitter</label>
          <input
            id={types.article}
            type="radio"
            checked={this.state.activeOption === types.article}
            onChange={() => this.handleRadioButtonChange(types.article)}
          />
          <label for={types.article}>Article</label>
          <input
            id={types.note}
            type="radio"
            checked={this.state.activeOption === types.note}
            onChange={() => this.handleRadioButtonChange(types.note)}
          />
          <label for={types.note}>Note</label>
          <Input
            name="name"
            label="Name"
            maxLength={30}
          />
          <Input
            name="link"
            label="Twitter link"
          />
          <Input
            name="image"
            label="Image"
          />
          <Input
            tag="textarea"
            name="description"
            label="Description"
          />
          <Button>add new item</Button>
        </form>
      </div>
    )
  }
}

export default Form;
```

#### Opcje w stanie

**Dobra praktyka:** Opcje w state warto podawać w postaci obiektu zawierającego pary klucz - wartość np. `twitter: "twitter"`, a nie czystych stringów, co pozwoli na dodatkową walidację przez mechanizmy Reacta i uniknięcie pomyłek typu literówki.

```JSX
const types = {
  twitter: 'twitter',
  article: 'article',
  note: 'note',
}

// Fragment ze stanem
state = {
  activeOption: types.twitter,
}

// Zamiast:
state = {
  activeOption: "twitter",
}

```

#### Funkcja obsługująca zmianę typu notatki

Funkcja zmienia typ notatki na podany

```JSX
handleRadioButtonChange = (type) => {
  this.setState({
    activeOption: type,
  })
}
```

W `input` zapis `onChange={() => this.handleRadioButtonChange(types.twitter)} />` czyli mamy funkcję zwracają funkcję `() =>` ponieważ nie chcemy jej od razu wywoływać, tylko dopiero gdy nastąpi zdarzenie `onChange`.

Do handlerów zdarzeń powinniśmy przekazywać zawsze wskaźnik na funkcję (lub samo wyrażenie funkcji),

Atrybut `checked`, któy decyduje o tym, czy dane pole jest zaznaczone ustawiamy za pomocą warunku `checked={this.state.activeOption === types.twitter}`

<!-- prettier-ignore -->
```html
<input
  id={types.twitter}
  type="radio"
  checked={this.state.activeOption === types.twitter}
  onChange={() => this.handleRadioButtonChange(types.twitter)}
/>
<label for={types.twitter}>Twitter</label>
```

#### Opisy dla różnych typów notatek

Dodajemy zmienną `descriptions`

```JSX
const descriptions = {
  twitter: 'favorite Twitter account',
  article: 'Article',
  note: 'Note',
}
```

W komponencie `Title` dostajemy się do właściwego opisu poprzez `<Title>Add new {descriptions[this.state.activeOption]}</Title>` ponieważ nazwy kluczy w `descriptions` (`twitter`, `article` i `note`) są takie same jak w `types`

```JSX
<Title>Add new {descriptions[this.state.activeOption]}</Title>
```

## Warunkowe renderowanie pól formularza

Usuwamy obrazek jeśli wpis nie jest typu `twitter`

**Dobra praktyka:** Jeśli chcemy aby w związku z warunkiem dany element nie był renderowany warto zwrócić `null`.

```JSX
{
  activeOption === types.twitter ? <Input name="image" label="Image" /> : null;
}
```

Zmiana `label` w zależności od rodzaju wpisu

```JSX
<Input
  name="name"
  label={activeOption === types.twitter ? "Twitter Name" : "Title"}
  maxLength={30}
/>
```

Zmiana `label` w zależności od rodzaju wpisu

```JSX
{
  activeOption !== types.note ? (
    <Input
      name="link"
      label={activeOption === types.twitter ? "Twitter Link" : "Link"}
    />
  ) : null;
}
```

## Contex API

**Contex API** - narzędzie, któe do pewnego stopnia pozwala zastąpić globalny state

### Tworzenie kontekstu

- Tworzymy plik `context.js` w głownym katalogu aplikacji
- Kontekst importujemy w naszym `Root` aplikacji

Aby umożliwić dostęp do kontekstu należy opleść elementy w `Provider`, poniżej w kodzie `<AppContext.Provider value={this.state.name}></AppContext.Provider>`

- `Provider`
  - Działa jak teleport
  - Umożliwia znajdującym się nim elementom dostęp do kontekstu
  - Props `value` służy do wskazywania co chcemy przekazać
- `Consumer`
  - Pozwala "konsumować" kontekst i pobierać z niego potrzebne elementy
  - Musi zawierać funkcję, która będzie zwracać kod JSX i jako parametr przyjmować to co zostało przekazane do kontekstu.

```JSX
// Plik context.js

import React from "react";
const AppContext = React.createContext();
export default AppContext;
```

```JSX
// Plik src/views/Root/Root.js

import React from "react";
import "./index.css";
// Importujemy kontekst
import AppContext from '../../context';
import { BrowserRouter, Route, Switch } from 'react-router-dom';
import TwittersView from '../TwittersView/TwittersView';
import ArticlesView from '../ArticlesView/ArticlesView';
import NotesView from '../NotesView/NotesView';
import Header from '../../components/Header/Header';
import Modal from '../../components/Modal/Modal';

const initialStateItems = [
  {
    image: "https://pbs.twimg.com/profile_images/906557353549598720/oapgW_Fp.jpg",
    name: "Dan Abramov",
    description: "React core member",
    twitterLink: "https://twitter.com/dan_abramov"
  }
];

class Root extends React.Component {
  state = {
    items: [...initialStateItems],
    isModalOpen: false,
    name: 'Roman',
  };

  addItem = e => {
    e.preventDefault();

    const newItem = {
      name: e.target[0].value,
      twitterLink: e.target[1].value,
      image: e.target[2].value,
      description: e.target[3].value
    };

    this.setState(prevState => ({
      items: [...prevState.items, newItem]
    }));

    e.target.reset();
  };

  openModal = () => {
    this.setState({
      isModalOpen: true,
    })
  }

  closeModal = () => {
    this.setState({
      isModalOpen: false,
    })
  }

  render() {
    const { isModalOpen } = this.state;

    // W funkcji return oplatamy elementy w <AppContext.Provider></AppContext.Provider>
    // W value wskazujemy co chcemy przekazać
    return (
      <BrowserRouter>
        <AppContext.Provider value={this.state.name}>
          <Header openModalFn={this.openModal} />
          <h1>hello world</h1>
          <Switch>
            <Route exact path="/" component={TwittersView} />
            <Route path="/articles" component={ArticlesView} />
            <Route path="/notes" component={NotesView} />
          </Switch>
          { isModalOpen && <Modal closeModalFn={this.closeModal} /> }
        </AppContext.Provider>
      </BrowserRouter>
    );
  }
}

export default Root;

```

```JSX
// Plik src/views/ArticlesView.js

import React from "react";
// Importujemy kontekst
import AppContext from "../../context";

const ArticlesView = () => (
  // Odbieramy dane z Providera oplatając kod w <AppContext.Consumer>
  // <AppContext.Consumer> musi mieć w sobie funkcję, któa zwraca kod JSX (wymóg)
  <AppContext.Consumer>
    {context => <p>This is {context}</p>}
  </AppContext.Consumer>
);

export default ArticlesView;
```

## Przekazywanie metod i stanu za pomocą AppContext

- Tworzymy obiekt `contextElements` z potrzebnymi informacjami wewnątrz funkcji `render()` zawierający:
  - state
  - metodę `addItem`

```JSX
// Plik src/views/Root/Root.js

import React from "react";
import "./index.css";
// Mamy zaimportowany kotekst
import AppContext from '../../context';
import { BrowserRouter, Route, Switch } from 'react-router-dom';
import TwittersView from '../TwittersView/TwittersView';
import ArticlesView from '../ArticlesView/ArticlesView';
import NotesView from '../NotesView/NotesView';
import Header from '../../components/Header/Header';
import Modal from '../../components/Modal/Modal';

class Root extends React.Component {
  state = {
    items: {
      twitters: [],
      articles: [],
      notes: [],
    },
    isModalOpen: false,
  };

  addItem = e => {
    e.preventDefault();

    console.log('It works!!');

    const newItem = {
      name: e.target[0].value,
      twitterLink: e.target[1].value,
      image: e.target[2].value,
      description: e.target[3].value
    };

    this.setState(prevState => ({
      items: [...prevState.items, newItem]
    }));

    // e.target.reset();
  };

  openModal = () => {
    this.setState({
      isModalOpen: true,
    })
  }

  closeModal = () => {
    this.setState({
      isModalOpen: false,
    })
  }

  render() {
    const { isModalOpen } = this.state;
    // Tworzymy obiekt `contextElements` z potrzebnymi informacjami
    const contextElements = {
      ...this.state,
      addItem: this.addItem
    }

    // W <AppContext.Provider> przekazujemy nasz obiekt contextElements jako value
    return (
      <BrowserRouter>
        <AppContext.Provider value={contextElements}>
          <Header openModalFn={this.openModal} />
          <h1>hello world</h1>
          <Switch>
            <Route exact path="/" component={TwittersView} />
            <Route path="/articles" component={ArticlesView} />
            <Route path="/notes" component={NotesView} />
          </Switch>
          { isModalOpen && <Modal closeModalFn={this.closeModal} /> }
        </AppContext.Provider>
      </BrowserRouter>
    );
  }
}

export default Root;

```

```JSX
// Plik src/components/Form/Form.js

import React from "react";
// Importujemy kotekst
import AppContext from "../../context";
import styles from "./Form.module.scss";
import Input from "../Input/Input";
import Button from "../Button/Button";
import Title from "../Title/Title";
import Radio from "./FormRadio";

const types = {
  twitter: "twitter",
  article: "article",
  note: "note",
};

const descriptions = {
  twitter: "favorite Twitter account",
  article: "Article",
  note: "Note",
};

class Form extends React.Component {
  state = {
    type: types.twitter,
    title: "",
    link: "",
    image: "",
    description: "",
  };

  handleRadioButtonChange = type => {
    this.setState({
      type: type,
    });
  };

  handleInputChange = e => {
    this.setState({
      [e.target.name]: e.target.value,
    });

  };

  render() {
    const { type } = this.state;

    // Oplatamy nasz kod formularza <AppContext.Consumer>
    // W <AppContext.Consumer> zwracamy kod JSX w funkcji strzłkowej z atrybutem context
    // W form dodajemy funkcję onSubmit={context.addItem} zamiast starej już nieaktualnej
    return (
      <AppContext.Consumer>
        {context => (
          <div className={styles.wrapper}>
            <Title>Add new {descriptions[type]}</Title>
            <form
              autoComplete="off"
              className={styles.form}
              onSubmit={context.addItem}
            >
              <div className={styles.formOptions}>
                <Radio
                  id={types.twitter}
                  checked={type === types.twitter}
                  changeFn={() => this.handleRadioButtonChange(types.twitter)}
                >
                  Twitter
                </Radio>
                <Radio
                  id={types.article}
                  checked={type === types.article}
                  changeFn={() => this.handleRadioButtonChange(types.article)}
                >
                  Article
                </Radio>
                <Radio
                  id={types.note}
                  checked={type === types.note}
                  changeFn={() => this.handleRadioButtonChange(types.note)}
                >
                  Note
                </Radio>
              </div>
              <Input
                onChange={this.handleInputChange}
                value={this.state.title}
                name="title"
                label={
                  type === types.twitter ? "Twitter Name" : "Title"
                }
                maxLength={30}
              />
              {type !== types.note ? (
                <Input
                  onChange={this.handleInputChange}
                  value={this.state.link}
                  name="link"
                  label={
                    type === types.twitter ? "Twitter Link" : "Link"
                  }
                />
              ) : null}

              {type === types.twitter ? (
                <Input
                  onChange={this.handleInputChange}
                  value={this.state.image}
                  name="image"
                  label="Image"
                />
              ) : null}
              <Input
                onChange={this.handleInputChange}
                value={this.state.description}
                tag="textarea"
                name="description"
                label="Description"
              />
              <Button>add new item</Button>
            </form>
          </div>
        )}
      </AppContext.Consumer>
    );
  }
}

export default Form;
```

## Formularz i Controlled Components

**Komponenty kontrolowane (Controlled Components)** - takie komponenty, których wewnętrzny stan jest kontrolowany przez Reacta.

Zmiana formularza na dynamiczny

- Rozbudowujemy stan
- Wykorzystujemy takie same nazwy kluczy/atrybutów w state i w `input` np. `name="title"`, `link`, `description`, `image`

```JSX
  state = {
    items: {
      twitters: [],
      articles: [],
      notes: [],
    },
    isModalOpen: false,
  };
```

- Tworzymy funkcję `handleInputChange`
- Do każdego `Input` dodajemy funkcję poprzez `onChange={this.handleInputChange}`
- Do każdego `Input` dodajemy `value={this.state.title}` z odpowiednią nazwą elementu `title`, `link`, `image` itd.

```JSX
handleInputChange = e => {
  this.setState({
    [e.target.name]: e.target.value,
  });

};

// Fragment returna:
<Input
  onChange={this.handleInputChange}
  value={this.state.title}
  name="title"
  label={
    type === types.twitter ? "Twitter Name" : "Title"
  }
  maxLength={30}
/>
```

## Deployment na Netlify

https://www.netlify.com/

Kroki:

- Instalacja `netlify-cli`: https://www.npmjs.com/package/netlify-cli
- Tworzenie `build`u aplikacji
- Deploy aplikacji `netlify deploy`
- Podanie folderu `build`em
- Deploy produkcyjny: `netlify deploy --prod`

Konieczne jest stworzenie dodatkowej konfiguracji po stronie serwera, dla Netlify:

- W folderze `public` tworzymy plik `_redirects`

```
/* /index.html 200
```

Po dodaniu pliku robimy build na nowo

## Inne

- Przy formularzach jeśli nie potrzeba automatycznego uzupełniania dodajemy `<form autoComplete="off">`
- Jeśli elementy zaczynają się powtarzać warto zrefaktoryzować kod i utworzyć z nich komponent
- Dla dużych projektów React nie ma jednego słusznego sposobu na organizację plików. "Move files until it feels right" na podstawie twitta Dana Abramova
- Przy stylowaniu radio buttonów chowamy w CSS domyślny input i dodajemy własny element do stylowania
- Instalacja React Dev Tools: https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi
