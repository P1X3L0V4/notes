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

**UWAGA:** Wyrażenia JavaScript'owe w Reacie możemy wrzucać w nawiasy klamrowe.

## Inicjalizacja projektu

```bash
npx create-react-app my-app
cd my-app
npm start
```

### Aplikacja z Create React App

Starsza składnia

<!-- prettier-ignore -->
```javascript
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

### Tworzenie komponentu funkcyjnego

Dobra praktyka: Każdy komponent warto trzymać w oddzielnym pliku lub katalogu

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

- Zawsze używamy takiej samej nazwy zmiennej jaką eksportowaliśmy
- Możliwe obejście tej zasady poprzez zastosowanie `as`
- Wiele eksportów na jeden plik

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

- Tylko jeden export na cały plik

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

```javascript
// Plik index.js
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```

```javascript
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

```javascript
// Plik components/ListWrapper/ListWrapper.js

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
// Plik components/ListWrapper/ListItem/ListItem.js

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

**BEM (Block Element Modifier)** - metodyka nazywania zmiennych według schematu `Block__Element-Modifier`, która pozwala uniknąć konfliktów w kodzie. Więcej informacji: http://getbem.com/

## Props

### Dodawanie props

- W miejscu definiowania komponentu wskazujemy, że komponent przyjmuje props `const ListItem = props => (`
- W kodzie komponentu wykorzystujemy propsy np. `{props.image}`

```javascript
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

- W miejscu renderowania komponentu przypisujemy propsom wartości dla danej instancji komponentu np. `name`, `description`, `image`

```javascript
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
    // setState - metoda zmieniająca stan podajemy klucz : wartość
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

### Stary zapis komponentów klasowych

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      text: '';
    }

  }
}
```

Zatosowanie `class properties` pozwala zapomnieć o kontrukturze

Paczka do obsługi `propsal class properties`: https://babeljs.io/docs/en/babel-plugin-proposal-class-properties

## Funkcje strzałkowe w React

React korzysta często z funkcji strzałkowych ponieważ

- zachowują one kontekst `this`
- przy funkcjach tradycyjnych `handleChange(e){}` konieczne było bindowanie odpowiedniego kontekstu dla `this` poprzez dodanie `this.handleChange = this.handleChange.bind(this)` co przy wielu funkcjach zwiększało znacznie ilość kodu

## Dodawanie elementu do listy

```javascript
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

## Dodawanie CSS Modules i SCSS do aplikacji

Jeśli wykorzystujemy Create React App to instalacja według instrukcji: https://create-react-app.dev/docs/adding-a-sass-stylesheet/

CSS Modules umożliwia tworzenie takich samych nazw klas dla wielu elementów, które następnie są kompilowane do nazw z sufixem w postaci losowego ciągu znaków, które powodują, że każdy element ma docelowo unikalną nazwę klasy.

```javascript
import React from "react";
// Importujemy style
import styles from "./Form.module.scss";
// Nazwę obiektu ze stylami z importu i po kropce nazwa klasy
<div className={styles.wrapper}>
```

## `Target _blank`

Do `target="_black"` według dobrych praktyk nalezy dodać `rel=noopener norefeer`

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

```javascript
// Zmienna warunkowa z ternary operator
const ImageTag = image ? "img" : "div";

/* Tag HTML (JSX) ze zmienną ImageTag warunkująca użycie img lub div oraz w className klasa styles.image dla elementu jeśli jest img lub styles.imageNone jeśli brak */
<ImageTag
  src={image}
  className={image ? styles.image : styles.imageNone}
  alt={name}
/>;
```

## Refaktoryzacja formularza

- Sprawdzamy jakie elementy naszego formularza powinny być dynamiczne. W tym przypadku jest to tag, który raz będzie `input` innym razem np. `text-area`
- Do refaktoryzacji wykorzystujemy propsy
- Destrukturyzujemy propsy `{ tag: Tag, name, label, maxLength }`
- Pobieramy `propTypes` poprzez `import PropTypes from "prop-types";`
- Tworzymy propTypes dla naszego komponentu `Input.propTypes = {}`
- Tworzymy domyśle wartości dla propsów `Input.defaultProps = {}`
- Ponieważ zmieniamy nazwę komponentu na niegeneryczną (nieHMTLową) z `<input>` na `Tag` to musi być ona napisana wielką literą co ustawiamy za pomocą `{ tag: Tag }`. Jest to zmiana nazwy propsa wewnątrz komponentu.
- W `<label>` używamy `htmlFor` ponieważ `for` jest słowem zastrzeżonym w Javascripcie dal pętli
- Odpowiednie style umieszczamy w pliku `Input.module.scss`
- W `<Tag className>` sprawdzamy czy element jest `input` czy `textarea` i przydzielamy odpowiednią klasę za pomocą ternary operator

```javascript
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

Plik `components/Form` (fragment) po refaktoryzacji

```html
<form autocomplete="off" className="{styles.form}" onSubmit="{submitFn}">
  <input name="name" label="Name" maxlength="{30}" />
  <input name="link" label="Twitter link" />
  <input name="image" label="Image" />
  <input tag="textarea" name="description" label="Description" />
  <button className="{styles.button}">add new item</button>
</form>
```

## Renderowanie warunkowe

- Style dla `Button` przenosimy do odpowiedniego pliku `Button.module.scss`
- Funkcja `React.createElement()` jako jeden z parametrów przyjmuje `children`, daltego mamy props o tej nazwie, który następnie wstawiamy w tagu `<a></a>`
- Ponieważ chcemy aby nasz komponent `Button` miał zastosowanie zarówno w linkach utworzonych za pomocą `<button>` jak i zwykłego tagu `<a>` wykorzystujemy ternary operator do stworzenia warunku `{href ? ( <a></a> ) : ( <button></button> ) }`

```javascript
// Komponent Button
import React from "react";
import styles from "./Button.module.scss";

const Button = ({ children, href }) => (
  <>
    {href ? (
      <a
        href={href}
        target="_blank"
        className={styles.button}
        rel="noopener noreferrer"
      >
        {children}
      </a>
    ) : (
      <button className={styles.button}>{children}</button>
    )}
  </>
);

export default Button;
```

```html
<button href="{twitterLink}">
  visit twitter page
</button>
```

## Routing

Komunikacja ze serwerem w przypadku aplikacji opartych o React wygląda inaczej niż w przypadku statycznych stron internetowych. Jeśli użytkownik wysyła `request` o podstronę `myapp.com/about` to najprawdopodobniej nie będzie się ona znajdować na serwerze w postaci pliku `about.html`, ale będzie w plikach `.js` aplikacji. Zadaniem `React Router` jest poprawne renderowanie potrzebnych podstron i elementów aplikacji, które znajdują się w plikach JavaScript.

## Widoki (Views)

**Widoki (Views)**

- Widoki aplikacji składające się z komponentów
- Nie mogę być reużywane
- Najczęściej tworzymy nowe widok dla poszczególnych podstron

### Tworzenie nowego widoku

- W folderze `views` aplikacji dodajemy folder z nazwą nowego widoku np. `TwitterView` i wewnątrz niego plikiem skryptu `TwitterView.js`
- W pliku głwonym aplikacji `Root.js` przemianowanym z `App.js`
  - Importujemy wszystkie widoki
  - Instalujemy i importujemy `react-router`: https://www.npmjs.com/package/react-router
  - Instalujemy i importujemy `react-router-dom`: https://www.npmjs.com/package/react-router-dom

```javascript
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

```javascript
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

Komponent `<Switch></Switch>` renderuje ścieżki na zasadzie wymienności.
Jest to przydatne w przypadku ścieżek typu `/notes` i `/notes:id` w których nie chcemy podwójnie wyświetlać tego samego widoku.

```html
<Switch>
  <Route exact path="/" component="{TwittersView}" />
  <Route path="/articles" component="{ArticlesView}" />
  <Route path="/notes" component="{NotesView}" />
</Switch>
```

## Nawigacja

### Link

`<Link></Link>` pomaga przechwycić zapytanie do serwera i wyrenderować widok strony z plików `.js`

```javascript
import React from "react";
import { Link } from "react-router-dom";

const Navigation = () => (
  <ul>
    <li>
      <Link to="/">Twitters</Link>
    </li>
    <li>
      <Link to="/articles">Articles</Link>
    </li>
    <li>
      <Link to="/notes">Notes</Link>
    </li>
  </ul>
);

export default Navigation;
```

### NavLink

Przyjmuje dodatkowego propsa `activeClassName` pozwalającego zmienić klasę w zależności od stanu linka

- Do pierwszego `<NavLink>` dodajemy atrybut `exact` aby style były wyświetlane tylko dla strony głównej a nie dla wszystkich podstron

```javascript
import React from "react";
import { NavLink } from "react-router-dom";
import styles from "./Navigation.module.scss";

const Navigation = () => (
  <nav>
    <ul className={styles.wrapper}>
      <li className={styles.navItem}>
        <NavLink
          exact
          activeClassName={styles.navItemLinkActive}
          className={styles.navItemLink}
          to="/"
        >
          twitters
        </NavLink>
      </li>
      <li className={styles.navItem}>
        <NavLink
          activeClassName={styles.navItemLinkActive}
          className={styles.navItemLink}
          to="/articles"
        >
          articles
        </NavLink>
      </li>
      <li className={styles.navItem}>
        <NavLink
          activeClassName={styles.navItemLinkActive}
          className={styles.navItemLink}
          to="/notes"
        >
          notes
        </NavLink>
      </li>
    </ul>
  </nav>
);

export default Navigation;
```

## Dodawanie dodatkowych propsów

```javascript
const Button = ({ children, href, secondary, ...props }) => {};
```

```javascript
const buttonClass = secondary ? styles.secondary : styles.button;
```

```javascript
<Button secondary>Item</Button>
```

- Props `secondary` to sposób na dodanie alternatywnego stylu dla elementu przy pomocy `true/false`
- Ostatnia wartość `...props` dodaje do komponentu wszystkie brakujące propsy np. ze zdarzeń (`onClick`)

## Modal

```javascript
import React from "react";
import styles from "./Modal.module.scss";
import Form from "../Form/Form";

const Modal = () => (
  <div className={styles.wrapper}>
    <Form />
  </div>
);

export default Modal;
```

Style dal Modala z wyśrodkowaniem

```css
.wrapper {
  padding: 70px 80px 0;
  /* top: 50% razem z transform: translateY(-50%) i position: fixed wyśrodkowują element  */
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

```javascript
state = {
  items: [...initialStateItems],
  isModalOpen: false
};
```

W miejscu gdzie renderujemy modala dodajemy warunek

```javascript
{
  isModalOpen && <Modal closeModalFn={this.closeModal} />;
}
```

Zamiast pisać `this.state.isModalOpen` używamy destrukturyzacji w funkcji `render`

```javascript
const { isModalOpen } = this.state;
```

#### Funkcja otwierająca modal

```javascript
openModal = () => {
  this.setState({
    isModalOpen: true
  });
};
```

Przekazujemy ją do `<Header>` w którym znajduje się nasz `<Button>`

```javascript
<Header openModalFn={this.openModal} />
```

Dodajemy kod w pliku z `<Header>`

- Dodajemy destrukturyzację `{ openModalFn }` jako atrybut
- Do `<Button>` dodajemy `onClick={openModalFn}`

```javascript
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

#### Funkcja zamykająca modal

```javascript
closeModal = () => {
  this.setState({
    isModalOpen: false
  });
};
```

Przekazujemy ją do naszego modala

```javascript
{
  isModalOpen && <Modal closeModalFn={this.closeModal} />;
}
```

W pliku `<Modal>` dodajemy

- Dodajemy destrukturyzację `{ closeModalFn }` jako atrybut
- Do `<button>` dodajemy `onClick={closeModalFn}`

```javascript
const Modal = ({ closeModalFn }) => (
  <div className={styles.wrapper}>
    <button onClick={closeModalFn}>close me</button>
    <Form />
  </div>
);
```

## Dynamika formularza

- Zmiana komponentu na stanowy
- Dodana stała `types` dla rodzajów wpisów
- Dodana stała `descriptions` dla nagłówków
- Dodajemy `<input type="radio">` dla każdej opcji
- Dla każdego `<input type="radio">` dodajemy funkcję `onChange={() => this.handleRadioButtonChange(types.nazwa)}` odpowiedzialną za zmianę stanu
- Dodajemy kod odpowiedzialny za to czy nasz element radio będzie zaznaczony `checked={this.state.activeOption === types.twitter}`

```javascript
import React from "react";
import styles from "./Form.module.scss";
import Input from "../Input/Input";
import Button from "../Button/Button";
import Title from "../Title/Title";

const types = {
  twitter: "twitter",
  article: "article",
  note: "note"
};

const descriptions = {
  twitter: "favorite Twitter account",
  article: "Article",
  note: "Note"
};

class Form extends React.Component {
  state = {
    activeOption: types.twitter
  };

  handleRadioButtonChange = type => {
    this.setState({
      activeOption: type
    });
  };

  render() {
    return (
      <div className={styles.wrapper}>
        <Title>Add new {descriptions[this.state.activeOption]}</Title>
        <form
          autoComplete="off"
          className={styles.form}
          onSubmit={this.props.submitFn}
        >
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
          <Input name="name" label="Name" maxLength={30} />
          <Input name="link" label="Twitter link" />
          <Input name="image" label="Image" />
          <Input tag="textarea" name="description" label="Description" />
          <Button>add new item</Button>
        </form>
      </div>
    );
  }
}

export default Form;
```

## Renderowanie warunkowe pól formularza

Usuwamy obrazek jeśli wpis nie jest twitterem

```javascript
{
  activeOption === types.twitter ? <Input name="image" label="Image" /> : null;
}
```

Zmiana `label` w zależności od rodzaju wpisu

```javascript
<Input
  name="name"
  label={activeOption === types.twitter ? "Twitter Name" : "Title"}
  maxLength={30}
/>
```

Zmiana `label` w zależności od rodzaju wpisu

```javascript
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

### Tworzenie kontekstu

```javascript
// Plik context.js w głownym katalogu aplikacji

import React from "react";

const AppContext = React.createContext();

export default AppContext;
```

Kontekst importujemy w naszym `Root` aplikacji

```javascript
import AppContext from "../../context";
```

Aby umożliwić dostęp do kontekstu należy opleść elementy w `Provider`, poniżej w kodzie `<AppContext.Provider value={this.state.name}></AppContext.Provider>`

- `Provider`
  - Działa jak teleport
- `Consumer`
  - Pozwala "konsumować" kontekst i pobierać z niego potrzebne elementy
  - Wymaga funkcji zwracającej JSX z parametrem `context` (nazwa może być inna)

```javascript
// Plik Root.js
render() {
  const { isModalOpen } = this.state;

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
```

```javascript
// Plik views/ArticlesView.js
import React from "react";
import AppContext from "../../context";

const ArticlesView = () => (
  <AppContext.Consumer>
    {context => <p>This is {context}</p>}
  </AppContext.Consumer>
);

export default ArticlesView;
```

### Dynamiczna zmiana stanu i input

- Wykorzystujemy takie same nazwy w state i w `input` np. `name="title"`, `link`, `description`, `image` i tworzymy funkcję `handleInputChange`
- Do `input`ów dodajemy `value={this.state.title}` z odpowiednią nazwą elementu `title`, `link`, `image` itd.

```javascript
class Form extends React.Component {
  state = {
    type: types.twitter,
    title: "",
    link: "",
    image: "",
    description: "",
  };

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

...

}
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
