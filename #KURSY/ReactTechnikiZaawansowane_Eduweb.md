# Eduweb - Techniki Zaawansowane

## Zagadnienia warte opanowania

1. Znajomość zaawansowanych wzorców
   - Higher Order Components (HOC)
   - Render props
   - Compound Components
   - Hooks
2. Znajomość dobrych praktyk
3. Testowanie kodu
4. Znajomość zaawansowanych narzędzi
   - Circle CI
   - Buddy

## Konfiguracja środowiska pracy

```bash
# Instalacja create-react-app
npx create-react-app nazwaprojektu
```

Jeśli chcemy korzystać z `npm` zamiast `yarn` należy:

- Wejść do katalogu projektu i usunąć `node_modules` oraz `yarn.lock`
- Zainstalować dependencje ponownie `npm install`

Możliwe jest też użycie flagi `use npm` przy tworzeniu projektu

```bash
# Instalacja CSS Modules z SASS Loaderem
npm install node-sass --save
```

## Bulma

Adres strony: https://bulma.io/

```bash
# Instalacja Bulma
npm install bulma --save
```

W pliku importujemy bulmę

```javascript
import "bulma";
```

## `classnames`

`classnames` - biblioteka służąca do wygodnego łączenia klas z zaimportowanych bibliotek i plików CSS.

```bash
npm install classnames
```

```javascript
// Import
import cx from "classnames";
```

```html
<!-- Zastosowanie -->
<div className={cx(styles.app, "box")}>
```

## HOC

Podejście Higher Order Components pozwala uniknąć powtarzania kodu w przypadku np. komponentów wykorzystujących te same funkcje czy logikę.

### `{ Component }`

Importowanie `{ Component }` i pisanie komponentu `class MyClass extends Component` pozwala wykonać tzw. `named export`

```JSX
import React, { Component } from 'react';

class MyClass extends Component { ... }
```

### Classnames

Moduł pozwalający na stosowanie warunkowego łączenia klas w komponentach reactowych

- Link: https://www.npmjs.com/package/classnames
- Artykuł: https://zeph.co/multiple-classnames-css-modules-react

```JSX
const listClass = cx(styles.list, {
   [styles.isCollapsed]: this.state.isCollapsed,
});
```

### HOC `withCollapse.js`

- Należy pamiętać o dodaniu do zwracanego komponentu wszystkich propsów jakie mogą być przekazywane w kodzie komponentu, poniżej poprzez `{...this.props}` we `<WrappedComponent>`

```JSX
// Plik src/hoc/withCollapse.js

import React from "react";

const withCollapse = WrappedComponent => {
  return class WithCollapse extends React.Component {
    state = {
      isCollapsed: true,
    };

    toggle = () => {
      this.setState(prevState => ({
        isCollapsed: !prevState.isCollapsed,
      }));
    };

    render() {
      const { isCollapsed } = this.state;

      return (
        <WrappedComponent
          isCollapsed={isCollapsed}
          toggle={this.toggle}
          {...this.props}
        />
      );
    }
  };
};

export default withCollapse;

```

W przypadku komponentu funkcyjnego propsy przekazujemy w następujący sposób:

```JSX
return (props) => <WrappedComponent />;
```

### Zagnieżdżanie HOC

```JSX
export default withCollapse(ItemsList);
```

### HOC `withAuth.js`

- Dodajemy HOC z autoryzacją

```JSX
// Plik src/hoc/withAuth.js

import React from "react";

const withAuth = WrappedComponent => {
  return class WithAuth extends React.Component {
    state = {
      isAuthorised: false,
    };

    toggleAuth = () => {
      this.setState(prevState => ({
        isAuthorised: !prevState.isAuthorised,
      }));
    };

    render() {
      const { isAuthorised } = this.state;

      return (
        <WrappedComponent
          isAuthorised={isAuthorised}
          toggleAuth={this.toggleAuth}
          {...this.props}
        />
      );
    }
  };
};

export default withAuth;

```

- W komponencie niższego rzędu dodajemy warunkowe wyświetlanie treści tylko gdy użytkownik jest zalogowany

```JSX
// Plik src/components/Columns/Columns.js

import React from "react";
import cx from "classnames";
import styles from "./Columns.module.scss";
import withCollapse from "../../hoc/withCollapse";
import withAuth from "../../hoc/withAuth";

const Columns = ({ isCollapsed, isAuthorised, toggleAuth, toggle }) => {
  const rowClass = cx("columns", {
    [styles.isCollapsed]: isCollapsed,
  });

  return (
    <div className="columns">
      <div className="column">
        <p>Authorised: {isAuthorised.toString()}</p>
        <button className="button is-dark is-large" onClick={toggle}>
          collapse
        </button>
        <button className="button is-warning is-large" onClick={toggleAuth}>
          {isAuthorised ? "logout" : "login"}
        </button>
        {isAuthorised ? (
          <div className={rowClass}>
            <div className="column">
              <div className="notification is-primary">First column</div>
            </div>
            <div className="column">
              <div className="notification is-primary">Second column</div>
            </div>
            <div className="column">
              <div className="notification is-primary">Third column</div>
            </div>
            <div className="column">
              <div className="notification is-primary">Fourth column</div>
            </div>
          </div>
        ) : (
          <h2 class="title is-2">You must sign in to see this content</h2>
        )}
      </div>
    </div>
  );
};

export default withAuth(withCollapse(Columns));
```

### `recompose`

- Repo: https://github.com/acdlite/recompose

W sytuacji gdy chcemy opleść export w więcej niż jeden hoc można skorzystać z `compose` z `Redux` lub `compose` z `recompose`:

Recompose

```JSX
import { compose } from 'recompose'

export default compose(
  withResource,
  withSocket,
  withNotifications
)(TextComponent)
```

Redux

```JSX
import { compose } from 'redux'

export default compose(
  withResource,
  withSocket,
  withNotifications
)(TextComponent)
```

Przykład z komponentu `Columns` z plików kursu

```JSX
export default compose(
  withCollapse,
  withAuth
)(Columns);
```

## Render props

- Props `render` może zwracać JSX lub funkcję zwracającą JSX (wtedy trzeba ją wywoływać) np. `{props.render("Roman")}`

```JSX
// Plik src/views/Patterns.js

import React from "react";

const MyComponent = props => (
  <div>
    <p>Hello world</p>
    {props.render("Roman")}
  </div>
);

const Patterns = () => (
  <div>
    <h2 className="title is-3">Patterns</h2>
    <MyComponent render={data => <p>Hello {data}</p>} />
  </div>
);

export default Patterns;
```

Wykorzystanie children

```JSX
// Plik src/views/Patterns.js

import React from "react";

const MyComponent = ({ children }) => (
  <div>
    <p>Hello world</p>
    { children }
  </div>
);

const Patterns = () => (
  <div>
    <h2 className="title is-3">Patterns</h2>
    <MyComponent>Hello</MyComponent>
  </div>
);

export default Patterns;
```

- Wykorzystanie `children as a function` poprzez `children("Roman")`
- To co przekazujemy w funkcji `children("Roman")` dostępne jest jako `data` w `<MyComponent>{(data) => <p>Hello {data}</p>}</MyComponent>`, zamiast `data` możer być inna dowolna nazwa.

```JSX
// Plik src/views/Patterns.js

import React from "react";

const MyComponent = ({ children }) => (
  <div>
    <p>Hello world</p>
    { children("Roman") }
  </div>
);

const Patterns = () => (
  <div>
    <h2 className="title is-3">Patterns</h2>
    <MyComponent>{(data) => <p>Hello {data}</p>}</MyComponent>
  </div>
);

export default Patterns;
```

- Tworzymy `render props` w osobnym pliku
- W komponencie podajemy zdestrukturyzowane `render={({ isCollapsed, toggle }) => (...)`; bez destrukturyzacji `data.isCollapsed` i `data.toggle`

```JSX
// Plik src/providers/Collapse.js

import React from "react";

class Collapse extends React.Component {
  state = {
    isCollapsed: true,
  };

  toggle = () => {
    this.setState(prevState => ({
      isCollapsed: !prevState.isCollapsed,
    }));
  };

  render() {
    const renderProps = {
      isCollapsed: this.state.isCollapsed,
      toggle: this.toggle,
    };

    return this.props.render(renderProps);
  }
}

export default Collapse;

```

```JSX
// Plik src/components/ItemsList/ItemsList.js

import React from "react";
import styles from "./ItemList.module.scss";
import cx from "classnames";
import Collapse from "providers/Collapse";

const items = [`Docs1`, `Docs2`, `Docs3`, `Docs4`, `Docs5`];

const ItemsList = ({ isCollapsed, toggle }) => {
  const listClass = isCollapsed =>
    cx(styles.list, {
      [styles.isCollapsed]: isCollapsed,
    });

  return (
    <Collapse
      render={({ isCollapsed, toggle }) => (
        <div>
          <button className="button is-dark is-large" onClick={toggle}>
            Show / Collapse
          </button>
          <ul className={listClass(isCollapsed)}>
            {items.map(item => (
              <li className="notification is-primary">{item}</li>
            ))}
          </ul>
        </div>
      )}
    />
  );
};

export default ItemsList;

```

### Zagnieżdżanie render props

```JSX
// Plik src/components/Columns/Columns.js

import React from "react";
import cx from "classnames";
import styles from "./Columns.module.scss";
import Authorisation from "providers/Authorisation";
import Collapse from "providers/Collapse";

const Columns = ({ isCollapsed, isAuthorised, toggleAuth, toggle }) => {
  const rowClass = isCollapsed =>
    cx("columns", {
      [styles.isCollapsed]: isCollapsed,
    });

  return (
    <Collapse
      render={({ isCollapsed, toggle }) => (
        <Authorisation
          render={({ isAuthorised, toggleAuth }) => (
            <div className="columns">
              <div className="column">
                <p>Authorised: {isAuthorised.toString()}</p>
                <button
                  className={cx("button", "is-dark", "is-large", [
                    styles.button,
                  ])}
                  onClick={toggle}
                >
                  Show / Collapse
                </button>
                <button
                  className={cx("button", "is-warning", "is-large", [
                    styles.button,
                  ])}
                  onClick={toggleAuth}
                >
                  {isAuthorised ? "logout" : "login"}
                </button>
                {isAuthorised ? (
                  <div className={rowClass(isCollapsed)}>
                    <div className="column">
                      <div className="notification is-primary">
                        First column
                      </div>
                    </div>
                    <div className="column">
                      <div className="notification is-primary">
                        Second column
                      </div>
                    </div>
                    <div className="column">
                      <div className="notification is-primary">
                        Third column
                      </div>
                    </div>
                    <div className="column">
                      <div className="notification is-primary">
                        Fourth column
                      </div>
                    </div>
                  </div>
                ) : (
                  <h2 class="title is-2">
                    You must sign in to see this content
                  </h2>
                )}
              </div>
            </div>
          )}
        />
      )}
    />
  );
};

export default Columns;
```

### Render props i Downshift

**Downshift** - biblioteka pozwalająca dodawać przy pomocy render props dodatkowe rzeczy di naszych pól.

- Repo: https://github.com/downshift-js/downshift

React select

- Repo - https://github.com/JedWatson/react-select

```JSX
// Plik src/views/Patterns.js

import React from "react";
import cx from "classnames";
import Downshift from "downshift";

const items = [
  { value: "apple" },
  { value: "pear" },
  { value: "orange" },
  { value: "grape" },
  { value: "banana" },
];

const Patterns = () => (
  <Downshift>
    {({
      isOpen,
      inputValue,
      getInputProps,
      getMenuProps,
      getItemProps,
      selectedItem,
    }) => (
      <div className={cx("dropdown", { "is-active": isOpen })}>
        <input
          className="input"
          type="text"
          placeholder="Text input"
          {...getInputProps()}
        />
        <div className="dropdown-menu">
          <div className="dropdown-content" {...getMenuProps()}>
            {items
              .filter(item => item.value.includes(inputValue))
              .map(({ value }, index) => (
                <button
                  className={cx("dropdown-item", "button", "is-white", {
                    "is-active": value === selectedItem,
                  })}
                  key={value}
                  {...getItemProps({
                    key: value,
                    index,
                    item: value,
                  })}
                >
                  {value}
                </button>
              ))}
          </div>
        </div>
      </div>
    )}
  </Downshift>
);

export default Patterns;
```

## Hooks

**Hooks** - funkcje które zostały stworzone do tego żeby "zaczepiać się" o konkretne etapy cyklu życia komponentu których brakowało w komponentach funkcyjnych. Dzięki temu możemy wykorzystywać komponenty funkcyjne niemalże tak jak komponenty klasowe.

### `useState`

`useState()` - jako pierwszy argument przyjmuje inicjalny state

```JSX
// Plik src/views/Components.js

import React, { useState } from "react";

const Components = () => {
   // Przy destrukturyzacji tablicy liczy się kolejność elementów
  const [inputContent, setInputContent] = useState("Hello World");

  const handleInputChange = e => {
    setInputContent(e.target.value);
  };

  return (
    <div>
      <h2 className="title is-3">Components</h2>
      <p>Hi there, {inputContent}</p>
      <input name="name" onChange={handleInputChange} />
    </div>
  );
};

export default Components;

```

```JSX
// Plik src/views/Components.js

import React, { useState } from "react";
import cx from "classnames";
import styles from "./Components.module.scss";

const Components = () => {
  const [inputContent, setInputContent] = useState("Write your task");
  const [itemsList, setItemsList] = useState([
    {
      id: "1",
      content: "Hello, please add your first note",
    },
  ]);

  const handleInputChange = e => {
    setInputContent(e.target.value);
  };

  const addNewItem = () => {
    const newElement = {
      content: inputContent,
      id: itemsList.length + 1,
    };

    setItemsList([...itemsList, newElement]);
  };

  const removeElement = id => {
    const newItemsList = itemsList.filter(item => item.id !== id);

    setItemsList(newItemsList);
  };

  return (
    <div className={styles.wrapper}>
      <h2 className="title is-3">Components</h2>
      <input
        autoComplete="off"
        class="input is-large"
        name="name"
        type="text"
        value={inputContent}
        onChange={handleInputChange}
      />
      <button
        onClick={addNewItem}
        className={cx("button is-warning is-large", styles.button)}
      >
        Add item
      </button>
      {itemsList.map(item => (
        <div key={item.id} className={cx("notification is-info", styles.item)}>
          <button className="delete" onClick={() => removeElement(item.id)} />
          {item.content}
        </div>
      ))}
    </div>
  );
};

export default Components;

```
