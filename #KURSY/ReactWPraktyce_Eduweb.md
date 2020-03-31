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

Notatka: Wspomniane podejście Atomic Design

```
npm install --save styled-components
```

## Struktura projektu

```
public
--index.html
src
--components
--views
----Root
------Root.js
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
