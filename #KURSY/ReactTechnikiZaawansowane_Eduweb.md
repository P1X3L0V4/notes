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

W sytuacji gdy chcemy opleść export w więcej niż jeden hoc można skorzystać z `compose` z `Redux` lub `compose` z `recompose`:

Redux

```JSX
import { compose } from 'redux'

export default compose(
  withResource,
  withSocket,
  withNotifications
)(TextComponent)
```

Recompose

```JSX
import { compose } from 'recompose'

export default compose(
  withResource,
  withSocket,
  withNotifications
)(TextComponent)
```

### HOC `withAuth.js`

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
