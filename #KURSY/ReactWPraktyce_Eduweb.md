# Eduweb - React w praktyce

## Konfiguracja projektu

`create-react-app`

- Repozytorium: https://github.com/facebook/create-react-app
- Dokumentacja: https://create-react-app.dev/

`npx`

- https://www.npmjs.com/package/npx

`ESLint`

- Dokumentacja: https://eslint.org/
- Konfiguracja `eslint-config-airbnb`: https://www.npmjs.com/package/eslint-config-airbnb

Instalacje przy użyciu `npx`

```
npx install-peerdeps --dev eslint-config-airbnb
```

```json
// Plik .eslintrc
{
  "extends": ["react-app", "airbnb"],
  "rules": {
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".js"]
      }
    ]
  }
}
```

Przydatny skrót: `CTRL + SHIFT + P` -> ESLint: Fix all auto-fixable Problems
Ustawienia: ESLint: Auto Fix On Save

`Prettier`

- Plugin VSCode: https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

```json
// Plik konfiguracyjny .prettierrc
{
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 100
}
```

Łączenie konfiguracji ESLint z Prettier

```
npm install -D eslint-config-prettier prettier
```

```json
// Nowy plik .eslintrc
{
  "extends": ["airbnb", "prettier", "prettier/react"],
  "rules": {
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".js"]
      }
    ]
  }
}
```

Ustawienia -> Editor: Format on Save

`Husky` & `lint-staged`

- `husky` repozytorium: https://github.com/typicode/husky
- `lint-staged` repozytorium: https://github.com/okonet/lint-staged

```
npm install -D husky lint-staged
```

```json
// Do package.json dodajemy
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.js": ["prettier --config .prettierrc --write", "eslint --fix", "git add"]
  }
}
```

Testowy commit - zmiany dodajemy do ostatniego commita `--amend` bez dodatkowego komunikatu `--no-edit`

```
git commit --amend --no-edit
```

Dodatkowe ustawienia dla ESLinta

- Środowisko
- Zmienne globalne

```json
// Do pliku .eslintrc dodajemy:
{
  "env": {
    "jest": true
  },
  "globals": {
    "document": true
  }
}
```

## Styled Components

**Styled Components** - Biblioteka umożliwiająca pisanie styli CSS w JavaScripcie

- Styled Components: https://styled-components.com/
- Dokumentacja: https://styled-components.com/docs
- Repozytorium: https://github.com/styled-components/styled-components
- `vscode-styled-components`: https://marketplace.visualstudio.com/items?itemName=jpoissonnier.vscode-styled-components (Wersja autorstwa Juliena Poissonnier)

```
npm install --save styled-components
```

## Struktura projektu

```
public
--index.html
src
--components
--themes
---GlobalStyle.js
--views
----Root
-----Root.js
--index.js
.env
.eslintrc
.gitignore
.prettierrc
package.json
package-lock.json
```

### Importy absolutne

Tworzymy plik `.env` w głównym folderze aplikacji

```
NODE_PATH=src
```

To spowoduje, że domyślnym katalogiem dla ścieżek importów i eksportów będzie katalog `src`

Sprawdzić czy ścieżka nie powinna być

```
NODE_PATH=SRC/
```

## Propsy w Style components

- Wyciągamy je za pomocą funkcji strzałkowej
- Zmiana koloru tła w zależności od tego czy komponent `Button` ma props `secondary`:

```css
/* Wersja bazowa */
background-color: ${({ props }) => (props.secondary ? '#E6E6E6' : '#FFD82B')};

/* Wersja z destrukturyzacją */
background-color: ${({ secondary }) => (secondary ? '#E6E6E6' : '#FFD82B')};
```

```javascript
import styled from "styled-components";

const Button = styled.button`
  padding: 0;
  background-color: ${({ secondary }) => (secondary ? "#E6E6E6" : "#FFD82B")};
  width: ${({ secondary }) => (secondary ? "105px" : "220px")};
  height: ${({ secondary }) => (secondary ? "30px" : "47px")};
  border: none;
  border-radius: 50px;
  font-family: "Montserrat";
  font-weight: 600;
  font-size: ${({ secondary }) => (secondary ? "10px" : "16px")};
  text-transform: uppercase;
`;

export default Button;
```

## Propsy w Style components refaktoryzacja

- Importujemy `{ css }` z biblioteki `"styled-components"`
- Zagnieżdżamy funkcję `${({ secondary }) =>` wewnątrz
- Propsy z wartością `<Button width="20px">Close / Save</Button>`

```javascript
// Plik Button.js
import styled, { css } from "styled-components";

const Button = styled.button`
  padding: 0;
  background-color: #e6e6e6;
  width: ${({ width }) => width || "220px"};
  height: 47px;
  border: none;
  border-radius: 50px;
  font-family: "Montserrat";
  font-weight: 600;
  font-size: 16px;
  text-transform: uppercase;

  ${({ secondary }) =>
    secondary &&
    css`
      background-color: #ffd82b;
      width: 105px;
      height: 30px;
      font-size: 10px;
    `}
`;

export default Button;
```

```javascript
// Plik Root.js
import React from "react";
import Button from "components/Button/Button";

const Root = () => (
  <div>
    <h1>Hello Roman</h1>
    <Button width="20px">Close / Save</Button>
    <Button secondary>Remove</Button>
  </div>
);

export default Root;
```

## Tworzenie globalnych stylów

```javascript
// Plik GlobalStyle.js
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,600');

  *, *::before, *::after {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-size: 1.6rem;
    font-family: "Montserrat", sans-serif;
  }
`;

export default GlobalStyle;
```

Uwaga: `@import url('https://...');` nie jest zalecany w tej formie ponieważ może powodować konflikty

## Happy REM

**Happy REM** - Sposób pozwalający na stosowanie sensownych wartości dla jednostek `rem` w CSS

- Domyślnie 1rem to 16px w przeglądarce co powoduje, że musimy przeliczać wszystkie wartości z cyframi po przecinku

Wdrożenie Happy REM

```css
/* Ustawiamy by 1rem == 10px; */
html {
  font-size: 62.5%;
}
/* Ustawiamy bazową wielkość fonta dla body na 16px (1.6rem przy font-size: 62.5% dla html wynosi 16px) */
body {
  font-size: 1.6rem;
}
```

## CSS Antialiasing

- Link: https://devhints.io/css-antialias

```css
* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

## Storybook

```bash
# Instalacja
npx storybook

# Inna wersja
npx -p @storybook/cli sb init
```

### Folder .storybook

```
.storybook
--addons.js
--config.js
```

```javascript
// Plik .storybook/addons.js
import "@storybook/addon-actions/register";
import "@storybook/addon-links/register";
```

```javascript
// Plik .storybook/config.js
import { configure } from "@storybook/react";

function loadStories() {
  const req = require.context("../src/components", true, /\.stories\.js$/);
  req.keys().forEach(filename => req(filename));
}

configure(loadStories, module);
```

## Komponent w Stories

- Podstawowym elementem jest `storiesOf` , któe zawsze zaczyna każde story
- Importujemy `import { storiesOf } from '@storybook/react';`
- Importujemy element `import Button from "./Button";`
- Dodajemy kolejne węzły poprzez `.add()`

```javascript
// Plik src/components/Button/Button.stories.js
import React from "react";
import { storiesOf } from "@storybook/react";
import Button from "./Button";

storiesOf("Button", module)
  .add("Primary", () => <Button>Hello Roman</Button>)
  .add("Secondary", () => <Button secondary>Hello Roman</Button>);
```

## Dodawanie globalnych styli do Storybook

Do Storybooka należy dodać style oddzielnie, ponieważ środowisko to jest odseparowane od naszych `Global Styles`

Należy stworzyć plik `.storybook/preview-head.html` i w sekcji `<head>` dodawać odpowiednie style

```javascript
// Plik .storybook/preview-head.html

<style>
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,600');

  *, *::before, *::after {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    font-size: 62.5%;
  }

  body {
    font-size: 1.6rem;
    font-family: "Montserrat", sans-serif;
  }
</style>
```

## Storybook Knobs

Instalujemy

- npm: https://www.npmjs.com/package/@storybook/addon-knobs

```bash
npm install  --dev @storybook/addon-knobs
```

Do pliku `.storybook/addons.js` dodajemy

```javascript
import "@storybook/addon-knobs/register";
```

Do pliku `src/components/Button/Button.stories.js` importujemy `withKnobs` typu `select`

```javascript
import React from "react";
import { storiesOf } from "@storybook/react";
import { withKnobs, select } from "@storybook/addon-knobs";
import Button from "./Button";

storiesOf("Button", module)
  .addDecorator(withKnobs)
  .add("Primary", () => {
    const label = "Colors";
    const options = {
      Primary: "hsl(49, 100%, 58%)",
      Secondary: "hsl(196, 83%, 75%)",
      Tertiary: "hsl(106, 47%, 64%)"
    };
    const defaultValue = "hsl(49, 100%, 58%)";
    const groupId = "GROUP-ID1";
    const value = select(label, options, defaultValue, groupId);
    return <Button color={value}>Hello Roman</Button>;
  })
  .add("Secondary", () => <Button secondary>Hello Roman</Button>);
```

## Atomic Design

**Atomic Design** - podejście do projektowania, w którym projekt rozbijany jest na mniejsze elementy:

- Atomy (Atoms) - najmniejsze elementy w projekcie np `label`, `input`, `button`
- Molekuły (Molecules) - element składający się z kilku atomów np. `search form`
- Organizmy (Organisms) - element składający się z kilku molekuł lub atomów np. `nawigacja`, która zawiera `menu`, `logo` i `search form`
- Szablony (Templates) - składają się z wielu organizmów tworząc kompletne interfejsy
- Strony (Pages) - w przypadku projektu roboczego są to `views`

Artykuł Brada Frosta: https://bradfrost.com/blog/post/atomic-web-design/
