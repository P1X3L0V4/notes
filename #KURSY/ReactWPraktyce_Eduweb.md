# Eduweb - React w praktyce

## Konfiguracja projektu

Możemy korzystać z różnych `package managerów` np. `npm` lub `yarn`. To w jakim managerze jest napisany projekt poznajemy np. po pliku `yarn.lock` lub `package-lock.json`

`create-react-app`

- Repozytorium: https://github.com/facebook/create-react-app
- Dokumentacja: https://create-react-app.dev/

`npx`

- https://www.npmjs.com/package/npx

Jedną z zalet narzędzia jest brak konieczności pisania pełnych długich ścieżek do `node_modules`

`ESLint`

- Dokumentacja: https://eslint.org/
- Konfiguracja `eslint-config-airbnb`: https://www.npmjs.com/package/eslint-config-airbnb

Instalacje przy użyciu `npx`

```bash
npx install-peerdeps --dev eslint-config-airbnb
```

Przydatny skrót: `CTRL + SHIFT + P` -> `ESLint: Fix all auto-fixable Problems`
Ustawienia: `ESLint: Auto Fix On Save`

Jeśli w ESLint wyskakują nam jakieś mniejsze błędy, warto wyszukać je po nazwie reguły i ewentualnie dodać wyjątek w pliku konfiguracyjnym.

```json
// Plik .eslintrc

// Pierwszy arguemnt reguły (rules): 0/1/error/warning
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

`Prettier`

**Prettier** - narzędzie do estetycznego formatowania kodu

- Plugin VSCode: https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

Jeśli brak konfiguracji to Prettier pobiera konfigurację z ustawień edytora kodu

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

Narzędzia pozwalające uniknąć zacommitowania błędnego kodu.

- `husky` repozytorium: https://github.com/typicode/husky
- `lint-staged` repozytorium: https://github.com/okonet/lint-staged

```bash
npm install -D husky lint-staged
```

- Hook husky `pre-commit` odpali się przed zacommitowaniem kodu i sprawdzi czy nie ma błędów.
- W `lint-staged` podajemy komendy w takiej kolejności w jakiej mają się wykonać . Na końcu mamy `git add` ponieważ kolejność wykonywania operacji jest następująca:
  - `git add`
  - `git commit`
  - uruchamiają się komendy z lint-staged i jeśli coś zostało sformatowane to konieczne jest ponowne dodanie zmian przez `git add`

```json
// Do package.json dodajemy:

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

```bash
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

```bash
npm install --save styled-components
```

### Struktura projektu

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

```bash
NODE_PATH=src
```

To spowoduje, że domyślnym katalogiem dla ścieżek importów i eksportów będzie katalog `src`

Sprawdzić czy ścieżka nie powinna być

```bash
NODE_PATH=SRC/
```

Aktualne podejście (link z komentarzy użytkowników): https://alligator.io/react/clean-import-statements-in-react/

W tym miejscu należy dodać do `.eslintrc` regułę obsługującą importy absolutne (do sprawdzenia)

```json

"settings": {
  "import/resolver": {
    "node": {
      "moduleDirectory": ["node_modules", "src/"]
    }
  }
}
```

### Propsy typu Boolean w Style components

- Wyciągamy je za pomocą funkcji strzałkowej
- Ponieważ korzystamy z `tag template literals` możemy skorzystać z `${}`
- Zmiana koloru tła w zależności od tego czy komponent `Button` ma props `secondary`:

```css
/* Wersja bazowa */
background-color: ${({ props }) => (props.secondary ? '#E6E6E6' : '#FFD82B')};

/* Wersja z destrukturyzacją */
background-color: ${({ secondary }) => (secondary ? '#E6E6E6' : '#FFD82B')};
```

Podanie propsa w formie `<Button secondary>` jest tym samym co `<Button secondary={true}>`

```JSX
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

### Propsy z wartością w Style components

- Importujemy `{ css }` z biblioteki `"styled-components"`
- Zagnieżdżamy funkcję `${({ secondary }) =>` wewnątrz
- Wykorzystanie `&&` pozwala zwrócić drugi element, czyli style
- W `styled components` możemy podawać propsy z wartością np. `width` jak w przykładzie `<Button width="20px">Close / Save</Button>` można przekazać w `styled components` i stworzyć na tej bazie warunek: jeśli mamy propsa `width` to taką szerokość ma mieć button a jeśli nie (operator `OR ||`) to domyślne `220`, kod w całości: `width: ${({ width }) => width || "220px"};`

```JSX
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

```JSX
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

```JSX
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

- Domyślnie `1rem` to `16px` w przeglądarce co powoduje, że musimy przeliczać wszystkie wartości z cyframi po przecinku
- Ustawienie `font-size: 62.5%;` dla `html` powoduje, że jednostki `rem` będą miały równe wartości np. `1.6rem` to przy tym ustawieniu `16px`

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

Link: https://devhints.io/css-antialias

```css
* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

## Storybook

**Uwaga!** Nowa wersja Storybook działa inaczej niż opisana w kursie. Komentarz od użytkownika:

```
Nowa wersja Storybook (5.3) wygląda trochę inaczej
- nie ma config.js ani addon js w .storybook jest tylko main.js
- robi się osobne Button.stories, Welcome.stories itp w /stories
- zadziałało dopiero po npx -p @storybook/cli sb init
```

```bash
# Instalacja
npx storybook

# Inna wersja
npx -p @storybook/cli sb init
```

Uruchamianie

```bash
npm run storybook
```

### Folder .storybook

```
.storybook
--addons.js
--config.js
```

```JSX
// Plik .storybook/addons.js

import "@storybook/addon-actions/register";
import "@storybook/addon-links/register";
```

W konfiguracji za pomocą wyrażeń regularnych możemy ustalić jakie pliki mają być brane pod uwagę `/\.stories\.js$/` i w jakich ścieżkach `"../src/components"`.

```javascript
// Plik .storybook/config.js

import { configure } from "@storybook/react";

function loadStories() {
  const req = require.context("../src/components", true, /\.stories\.js$/);
  req.keys().forEach((filename) => req(filename));
}

configure(loadStories, module);
```

### Komponent w Stories

- Podstawowym elementem jest `storiesOf` , któe zawsze zaczyna każde story
- Importujemy `import { storiesOf } from '@storybook/react';`
- Importujemy element `import Button from "./Button";`
- Dodajemy kolejne węzły poprzez `.add()`

```JSX
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

```JSX
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

### Storybook Knobs

Instalujemy

- npm: https://www.npmjs.com/package/@storybook/addon-knobs

```bash
npm install --dev @storybook/addon-knobs
```

Do pliku `.storybook/addons.js` dodajemy

```JSX
import "@storybook/addon-knobs/register";
```

Do pliku `src/components/Button/Button.stories.js` importujemy `withKnobs` typu `select`

```JSX
// Plik src/components/Button/Button.stories.js

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
      Tertiary: "hsl(106, 47%, 64%)",
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

## Theme Provider

**Theme Provider** - jest dla Styled Components rodzajem teleportu, który pozwala nam na przenoszenie danych dotyczących wyglądu naszych elementów do różnych miejsc, by mieć do nich dostęp z każdego komponentu, w którym będziemy tworzyć nasze style.

### Dodawanie Theme Provider do projektu

- Importujemy `ThemeProvider` przy pomocy `import { ThemeProvider } from 'styled-components';`
- Tworzymy `theme` za pomocą `const`a
- Oplatamy nasze elementy w `<ThemeProvider>` podając mu `theme={theme}`
- `ThemeProvider` musi oplatać jeden element więc wykorzystujemy fragment `<></>` do oplecenia kodu

```JSX
// Plik src/views/Root/Root.js

import React from "react";
import { ThemeProvider } from "styled-components";
import Button from "components/atoms/Button/Button";
import GlobalStyle from "theme/GlobalStyle";

const theme = {
  primary: "black",
};

const Root = () => (
  <div>
    <GlobalStyle />
    <ThemeProvider theme={theme}>
      <>
        <h1>Hello Roman</h1>
        <Button>Close / Save</Button>
        <Button secondary>Remove</Button>
      </>
    </ThemeProvider>
  </div>
);

export default Root;
```

Zastosowanie w komponencie `Button`

- W stylach `background-color` dodajemy `${({ props }) => props.theme.primary};`
- Zapis z destrukturyzacją `${({ theme }) => theme.primary};`

```JSX
import styled, { css } from "styled-components";

const Button = styled.button`
  padding: 0;
  background-color: ${({ theme }) => theme.primary};
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
      background-color: hsl(0, 0%, 90%);
      width: 105px;
      height: 30px;
      font-size: 10px;
    `}
`;

export default Button;
```

## Globalne zmienne

Dodajemy plik `mainTheme.js` do katalogu `src/theme/`

```JSX
// Plik src/theme/mainTheme.js

export const theme = {
  primary: "hsl(49, 100%, 58%)",
  secondary: "hsl(196, 83%, 75%)",
  tertiary: "hsl(106, 47%, 64%)",
  grey100: "hsl(0, 0%, 96%)",
  grey200: "hsl(0, 0%, 90%)",
  black: "hsl(0, 0%, 0%)",
  light: 300,
  bold: 300,
};
```

- Do `ThemeProvider` dodajemy `theme`: `<ThemeProvider theme={theme}>`

```JSX
// Plik src/views/Root/Root.js

import React from 'react';
import { ThemeProvider } from 'styled-components';
import Button from 'components/atoms/Button/Button';
import GlobalStyle from 'theme/GlobalStyle';

const theme = {
  primary: 'black',
};

const Root = () => (
  <div>
    <GlobalStyle />
    <ThemeProvider theme={theme}>
      <>
        <h1>Hello Roman</h1>
        <Button>Close / Save</Button>
        <Button secondary>Remove</Button>
      </>
    </ThemeProvider>
  </div>
);

export default Root;
```

- W pliku `Button` zmieniamy linijkę `background-color: ${({ theme }) => theme.primary};` destrukturyzując `theme` i dodając odwołanie do koloru zapisanego pod `theme.primary`

```JSX
import styled, { css } from 'styled-components';

const Button = styled.button`
  padding: 0;
  background-color: ${({ theme }) => theme.primary};
  width: ${({ width }) => width || '220px'};
  height: 47px;
  border: none;
  border-radius: 50px;
  font-family: 'Montserrat';
  font-weight: 600;
  font-size: 16px;
  text-transform: uppercase;

  ${({ secondary }) =>
    secondary &&
    css`
      background-color: hsl(0, 0%, 90%);
      width: 105px;
      height: 30px;
      font-size: 10px;
    `}
`;

export default Button;
```

## Komponent Input

W Storybook dodajemy dekorator, który przekaże style z `theme`

```javascript
// Plik .storybook\config.js

addDecorator((story) => <ThemeProvider theme={theme}>{story()}</ThemeProvider>);
```

Komentarz użytkownika

```
W Storybook w wersji 5.3, z której korzystałem w momencie nauki z kursu trochę się zmieniło i nie ma już pliku config.js. Więc by dodać obsługę ThemeProvider tworzymy w katalogu .storybook plik preview.js a w nim:

import React from 'react';
import { addDecorator } from '@storybook/react';
import { ThemeProvider } from 'styled-components';
import { theme } from '../src/theme/mainTheme';

addDecorator(story => {story()});
```

Stylowanie `Input`

```JSX
// Plik src/components/atoms/Input/Input.js

import styled, { css } from 'styled-components';
import magnifierIcon from 'assets/magnifier.svg';

const Input = styled.input`
  padding: 15px 30px;
  font-size: ${({ theme }) => theme.fontSize.s};
  font-weight: ${({ theme }) => theme.regular};
  background-color: ${({ theme }) => theme.grey100};
  border: none;
  border-radius: 50px;

  ::placeholder {
    text-transform: uppercase;
    letter-spacing: 1px;
    color: ${({ theme }) => theme.grey300};
  }

  ${({ search }) =>
    search &&
    css`
      padding: 10px 20px 10px 40px;
      font-size: ${({ theme }) => theme.fontSize.xs};
      background-image: url(${magnifierIcon});
      background-size: 15px;
      background-position: 15px 50%;
      background-repeat: no-repeat;
    `}
`;

export default Input;
```

## Podawanie ikony jako props

W pliku z komponentem `ButtonIcon` w `background-image:` podajemy `url` jako propsa `background-image: url(${({ icon }) => icon});`

```JSX
// Plik /src/components/atoms/ButtonIcon/ButtonIcon.js
const ButtonIcon = styled.button`
  width: 67px;
  height: 67px;
  border-radius: 20px;
  background-image: url(${({ icon }) => icon});
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-size: 40%;
  border: none;
  background-color: ${({ active }) => (active ? 'white' : 'transparent')};
`;

export default ButtonIcon;
```

- W Stories dla `ButtonIcon` importujemy ikony i przekazujemy `url` jako propsa np.`<ButtonIcon icon={bulbIcon} />`.
- Do wyświetlania ikony w Stories warto dodać style z kolorowym tłem poprzez `const YellowBackground = styled.div` a następnie zaaplikować je do wszystkich potrzebnych buttonów poprzez odpowiednio skonfigurowany: `.addDecorator(story => <YellowBackground>{story()}</YellowBackground>)`

```JSX
// Plik src/components/atoms/ButtonIcon/ButtonIcon.stories.js

import React from 'react';
import styled from 'styled-components';
import { storiesOf } from '@storybook/react';
import bulbIcon from 'assets/icons/bulb.svg';
import logoutIcon from 'assets/icons/logout.svg';
import penIcon from 'assets/icons/pen.svg';
import plusIcon from 'assets/icons/plus.svg';
import twitterIcon from 'assets/icons/twitter.svg';
import ButtonIcon from './ButtonIcon';

const YellowBackground = styled.div`
  display: flex;
  justify-content: center;
  align-items: center;
  width: 500px;
  height: 500px;
  background: ${({ theme }) => theme.primary};
`;

storiesOf('ButtonIcon', module)
  .addDecorator(story => <YellowBackground>{story()}</YellowBackground>)
  .add('Bulb', () => <ButtonIcon icon={bulbIcon} />)
  .add('Active', () => <ButtonIcon active icon={bulbIcon} />)
  .add('Logout', () => <ButtonIcon icon={logoutIcon} />)
  .add('Pen', () => <ButtonIcon icon={penIcon} />)
  .add('Plus', () => <ButtonIcon icon={plusIcon} />)
  .add('Twitter', () => <ButtonIcon icon={twitterIcon} />);
```

`.addDecorator()` - metoda przyjmująca `story` jako parametr; które zwraca "opleciony" w zdefiniowany component Zastosowanie

- Globalnie (w poprzez `config file` dodawanie zmiennych z `theme` do wszystkich stories)
- Lokalnie (dla poszczególnych komponentów)
- Dokumentacja: https://storybook.js.org/docs/basics/writing-stories/#decorators

## Tworzenie komponentu karty

Warunkowe

- Warunkowe stylowanie wrappera: `background-color: ${({ yellow, theme }) => (yellow ? theme.primary : 'white')};`
- Warunkowe dodawanie flexa funkcja `${({ flex }) => ...`
- Pozycjonowanie karty za pomocą `flex` i `grid`
- Początkowe podejście to zmiana koloru karty za pomocą `background-color: ${({ activeColor, theme }) => (activeColor ? theme[activeColor] : 'white')};` który to props przekazujemy następnie wewnątrz karty `<InnerWrapper activeColor={cardType}>` ale zmieniamy to na podejście `cardType` - kolory dodawane na podstawie typu wpisu
- `oneOf` to sposób na weryfikowanie `PropTypes` np. `cardType: PropTypes.oneOf(['note', 'twitter', 'article'])`
- Warunkowe wyświetlanie avatar lub link
-

```JSX
{cardType === 'twitter' && <StyledAvatar src="https://avatars.io/twitter/hello_roman" />}
{cardType === 'article' && <StyledLinkButton href="https://youtube.com/helloroman" />}
```

```JSX
// src/components/molecules/Card/Card.js

import React from 'react';
import PropTypes from 'prop-types';
import styled, { css } from 'styled-components';
import Paragraph from 'components/atoms/Paragraph/Paragraph';
import Heading from 'components/atoms/Heading/Heading';
import Button from 'components/atoms/Button/Button';
import LinkIcon from 'assets/icons/link.svg';

const StyledWrapper = styled.div`
  min-height: 380px;
  box-shadow: 0 10px 30px -10px hsla(0, 0%, 0%, 0.1);
  border-radius: 10px;
  overflow: hidden;
  position: relative;
  display: grid;
  grid-template-rows: 0.25fr 1fr;
`;

const InnerWrapper = styled.div`
  position: relative;
  padding: 17px 30px;
  background-color: ${({ activeColor, theme }) => (activeColor ? theme[activeColor] : 'white')};

  :first-of-type {
    z-index: 9999;
  }

  ${({ flex }) =>
    flex &&
    css`
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    `}
`;

const DateInfo = styled(Paragraph)`
  margin: 0 0 5px;
  font-weight: ${({ theme }) => theme.bold};
  font-size: ${({ theme }) => theme.fontSize.xs};
`;

const StyledHeading = styled(Heading)`
  margin: 5px 0 0;
`;

const StyledAvatar = styled.img`
  width: 86px;
  height: 86px;
  border: 5px solid ${({ theme }) => theme.twitter};
  border-radius: 50px;
  position: absolute;
  right: 25px;
  top: 25px;
`;

const StyledLinkButton = styled.a`
  display: block;
  width: 47px;
  height: 47px;
  border-radius: 50px;
  background: white url(${LinkIcon}) no-repeat;
  background-size: 60%;
  background-position: 50%;
  position: absolute;
  right: 25px;
  top: 50%;
  transform: translateY(-50%);
`;

const Card = ({ cardType }) => (
  <StyledWrapper>
    <InnerWrapper activeColor={cardType}>
      <StyledHeading>Hello Roman</StyledHeading>
      <DateInfo>3 days</DateInfo>
      {cardType === 'twitter' && <StyledAvatar src="https://avatars.io/twitter/hello_roman" />}
      {cardType === 'article' && <StyledLinkButton href="https://youtube.com/helloroman" />}
    </InnerWrapper>
    <InnerWrapper flex>
      <Paragraph>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit nemo ducimus fuga
        repellendus illum
      </Paragraph>
      <Button secondary>REMOVE</Button>
    </InnerWrapper>
  </StyledWrapper>
);

Card.propTypes = {
  cardType: PropTypes.oneOf(['note', 'twitter', 'article']),
};

Card.defaultProps = {
  cardType: 'note',
};

export default Card;
```

## Dodawanie React Router

- Tworzymy szablon

```JSX
// Plik src/templates/MainTemplate.js

import React from 'react';
import PropTypes from 'prop-types';
import { ThemeProvider } from 'styled-components';
import GlobalStyle from 'theme/GlobalStyle';
import { theme } from 'theme/mainTheme';

const MainTemplate = ({ children }) => (
  <div>
    <GlobalStyle />
    <ThemeProvider theme={theme}>{children}</ThemeProvider>
  </div>
);

MainTemplate.propTypes = {
  children: PropTypes.element.isRequired,
};

export default MainTemplate;

```

- Do `Root` dodajemy `BrowserRouter`
- Tworzymy widoki aplikacji

## Sidebar

Foldery do stories dodajemy w `storiesOf('Organisms/Sidebar', module)`

```JSX
storiesOf('Organisms/Sidebar', module)
  .addDecorator(StoryRouter())
  .add('Normal', () => <Sidebar />);
```

### Używanie komponentu jako inny komponent

Możemy użyć naszego styled komponentu jako inny komponent poprzez props `as` np. `<ButtonIcon exact as={NavLink} to="/" icon={penIcon} activeclass="active" />`

```JSX
import React from 'react';
import { Link } from 'react-router-dom';
import ButtonIcon from 'components/atoms/ButtonIcon/ButtonIcon';
import bulbIcon from 'assets/icons/bulb.svg';
import logoutIcon from 'assets/icons/logout.svg';
import penIcon from 'assets/icons/pen.svg';
import twitterIcon from 'assets/icons/twitter.svg';

const Sidebar = ({ pageType }) => (
  <StyledWrapper activeColor={pageType}>
    <StyledLogoLink to="/" />
    <StyledLinksList>
      <li>
        <ButtonIcon exact as={NavLink} to="/" icon={penIcon} activeclass="active" />
      </li>
      <li>
        <ButtonIcon as={NavLink} to="/twitters" icon={twitterIcon} activeclass="active" />
      </li>
      <li>
        <ButtonIcon as={NavLink} to="/articles" icon={bulbIcon} activeclass="active" />
      </li>
    </StyledLinksList>
    <StyledLogoutButton as={NavLink} to="/login" icon={logoutIcon} />
  </StyledWrapper>
);

export default Sidebar;
```

Aby to rozwiązanie działało w storybooku musimy zaimportować `storybook-router`
Linki do storybook-router:

- https://github.com/gvaldambrini/storybook-router
- https://www.npmjs.com/package/storybook-react-router

```JSX
import StoryRouter from 'storybook-react-router';
```

**Uwaga:** Należy pamiętać, że linki są `inline` a ikony mogą potrzebować `display: block`

## Osadzanie sidebara w aplikacji

Jeśli `Sidebar` znajduje się na wszystkich stronach:

- Powinien mieć pozycję `fixed`
- Powinien być odpowiednio osadzony w `BrowserRouter` i `ThemeProvider` a nie poza nimi
- `body` strony powinno dostać `padding-left: 150px` aby całą zawartość była odsunięta od `Sidebar`

Jeśli `Sidebar` znajduje się na niektóych stronach:

- Tworzymy nowy `UserPageTemplate` z `<Sidebar pageType={pageType} />{children}`
- Dodajemy w propsach `UserPageTemplate` propsa `pageType`
- W stylach `Sidebar` dodajemy warunek stylujący `background-color: ${({ activeColor, theme }) => (activeColor ? theme[activeColor] : theme.note)};` i podajemy propsa `<StyledWrapper activeColor={pageType}>`
- Osadzamy w plikach odpowiednich widoków np. w `Twitters` `<UserPageTemplate pageType="twitter">`

```JSX
// Plik src/templates/UserPageTemplate.js

import React from 'react';
import PropTypes from 'prop-types';
import Sidebar from 'components/organisms/Sidebar/Sidebar';

const UserPageTemplate = ({ children, pageType }) => (
  <>
    <Sidebar pageType={pageType} />
    {children}
  </>
);

UserPageTemplate.propTypes = {
  children: PropTypes.element.isRequired,
  pageType: PropTypes.oneOf(['note', 'twitter', 'article']),
};

UserPageTemplate.defaultProps = {
  pageType: 'note',
};

export default UserPageTemplate;
```

```JSX
// Plik src/components/organisms/Sidebar/Sidebar.js

import React from 'react';
import { NavLink } from 'react-router-dom';
import PropTypes from 'prop-types';
import styled from 'styled-components';
import ButtonIcon from 'components/atoms/ButtonIcon/ButtonIcon';
import bulbIcon from 'assets/icons/bulb.svg';
import logoutIcon from 'assets/icons/logout.svg';
import penIcon from 'assets/icons/pen.svg';
import twitterIcon from 'assets/icons/twitter.svg';
import logoIcon from 'assets/icons/logo.svg';

const StyledWrapper = styled.nav`
  position: fixed;
  left: 0;
  top: 0;
  padding: 25px 0;
  width: 150px;
  height: 100vh;
  background-color: ${({ activeColor, theme }) => (activeColor ? theme[activeColor] : theme.note)};
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
`;

const StyledLogoLink = styled(NavLink)`
  display: block;
  width: 67px;
  height: 67px;
  background-image: url(${logoIcon});
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-size: 80%;
  border: none;
  margin-bottom: 10vh;
`;

const StyledLogoutButton = styled(ButtonIcon)`
  margin-top: auto;
`;

const StyledLinksList = styled.ul`
  margin: 0;
  padding: 0;
  list-style: none;
`;

const Sidebar = ({ pageType }) => (
  <StyledWrapper activeColor={pageType}>
    <StyledLogoLink to="/" />
    <StyledLinksList>
      <li>
        <ButtonIcon exact as={NavLink} to="/" icon={penIcon} activeclass="active" />
      </li>
      <li>
        <ButtonIcon as={NavLink} to="/twitters" icon={twitterIcon} activeclass="active" />
      </li>
      <li>
        <ButtonIcon as={NavLink} to="/articles" icon={bulbIcon} activeclass="active" />
      </li>
    </StyledLinksList>
    <StyledLogoutButton as={NavLink} to="/login" icon={logoutIcon} />
  </StyledWrapper>
);

Sidebar.propTypes = {
  pageType: PropTypes.string.isRequired,
};

export default Sidebar;

```

```JSX
// Plik src/views/Twitters.js

import React from 'react';
import UserPageTemplate from 'templates/UserPageTemplate';

const Twitters = () => (
  <UserPageTemplate pageType="twitter">
    <h1>Twitters view</h1>
  </UserPageTemplate>
);

export default Twitters;
```
