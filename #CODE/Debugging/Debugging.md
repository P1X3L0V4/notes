# Debugowanie kodu

`debugger;` - wpisane w kodzie zatrzymuje działanie kodu

**breakpoint** - kropka wstawiana w kodzie pozwalająca zatrzymać egzekucję we wskazanym miejscu. `P-KLIK` na punkcie pozwala edytować dodatkowe opcje.

## Developer Tools Chrome

[Chrome DevTools Keyboard Shortcuts](https://developers.google.com/web/tools/chrome-devtools/shortcuts)

| Komenda                                                   | Działanie                                                                     |
| --------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `F12`                                                     | Otwórz narzędzia deweloperskie (ostatni używany panel)                        |
| `CTRL + SHIFT + I`                                        | Otwórz narzędzia deweloperskie (ostatni używany panel)                        |
| `CTRL + SHIFT + P`                                        | Otwórz listę komend (przy otwartych narzędziach)                              |
| `CTRL + SHIFT + J`                                        | Otwórz narzędzia deweloperskie (Console)                                      |
| `CTRL + SHIFT + C`                                        | Otwórz narzędzia deweloperskie (Elements)                                     |
| `CTRL + SHIFT + D`                                        | Zmień pozycję narzędzi dół/bok                                                |
| `CTRL + [`                                                | Następny panel                                                                |
| `CTRL + ]`                                                | Poprzedni panel                                                               |
| `P-KLIK na ikonę odświeżenia → Opróżnij pamięć podręczną` | Przy włączonych narzędziach deweloperskich czyści cache i przeładowuje stronę |
| `Preserve log`                                            | Konsola nie czyści się przy przeładowaniu (Panel opcji ikona zębatki)         |

### Console

| Komenda                              | Działanie                                                            |
| ------------------------------------ | -------------------------------------------------------------------- |
| `console.clear()`                    | Wyczyść konsolę                                                      |
| `console.log()`                      | Wyświetla podany komunikat                                           |
| `console.dir(element)`               | Wyświetla obiektową reprezentację wskazanego elementu                |
| `console.table(element)`             | Wyświetla element w konsoli w postaci tabeli                         |
| `console.group('Nazwa grupy')`       | Tworzy grupę komend                                                  |
| `console.assert(warunek, false-msg)` | Sprawdza czy `warunek` jest spełniony, jeśli nie drukuje `false-msg` |
| `console.time()`                     | Wykonuje test szybkości skryptu                                      |
| `$(selektor)`                        | Odpowiednik `querySelector`                                          |
| `$$`                                 | Odpowiednik `querSelectorAll`                                        |
| `$_`                                 | Zwraca wynik ostatniej operacji                                      |

```javascript
// Grupowanie wielu komend
console.group("Nazwa grupy");
console.log("Ala ma kota");
console.log("Kot ma Alę");
console.groupEnd(); // Koniec grupy

// Grupa domyślnie zwinięta
console.groupCollapsed("Nazwa grupy");
console.log("Ala ma kota");
console.log("Kot ma Alę");
console.groupEnd(); // Koniec grupy

// Test szybkości skryptu
console.time('test 1'); //rozpoczyna test - zaczyna liczyć czas
for (let i=0; i<10000; i++) {
    ...
}
console.timeEnd('test 1'); //kończy test
```

## Elements (HTML)

`P-KLIK na element HTML → Break on` - pozwala śledzić wpływ kodu np. JavaScript na dany element HTML

## Network

`P-KLIK na zapytaniu → Copy → Copy as fetch` - pozwala skopiować zapytanie i następnie zasymulować je wklejając do konsoli

`Preserve log` - zaznaczenie checkboxa pozwoli zachować listę zapytań mimo przeładowania strony

## More Tools

### Show coverage

`L-KLIK na Kropce` - włącza narzędzie `Instrument coverage` które raportuje użycie bajtów

## Widok mobilny

U góry aktywny pasek do płynnej zmiany progów rozdzielczości

## Debugowanie w Visual Studio Code

### Pluginy

- [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) - plugin pozwalający debugować kod bezpośrednio w edytorze VSC
  - `F5 (Debug → Start Debuging)` - Tryb debugowania
- [EsLint](https://eslint.org/) - konfigurowalny linter kodu
- [Prettier](https://prettier.io/) - plugin formatujący kod
- [Quokka](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode) - plugin wyświetlający rezultat działania edytowanej linii kodu
