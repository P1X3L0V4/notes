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
