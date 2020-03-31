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

```javascript
// Plik .eslintrc
{
  "extends": [
    "react-app",
    "airbnb"
  ],
  "rules": {
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [
          ".js"
        ]
      }
    ]
  }
}
```

Przydatny skrót: `CTRL + SHIFT + P` -> ESLint: Fix all auto-fixable Problems
Ustawienia: ESLint: Auto Fix On Save

`Prettier`

- Plugin VSCode: https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

```javascript
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

```javascript
// Nowy plik .eslintrc
{
  "extends": [
    "airbnb",
    "prettier",
    "prettier/react"
  ],
  "rules": {
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [
          ".js"
        ]
      }
    ]
  }
}
```

Ustawienia -> Editor: Format on Save
