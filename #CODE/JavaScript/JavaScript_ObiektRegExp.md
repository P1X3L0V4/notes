# JavaScript - Obiekt RegExp()

## Wyrażenia regularne (RegExp)

`RegExp(wyrażenie, flaga)` - obiekt, który przyjmuje 2 argumenty:

- wyrażenie, którym będziemy testować
- dodatkowe flagi

```javascript
const reg = new RegExp("pani?", "gi");
// lub
const reg = /pani?/gi;

var regexp = new RegExp("Ania"); // Konstrukcja wyrażeń regularnych
var regexp = /Ania/; // Alternatywna konstrukcja wyrażeń regularnych
var imie = "Ania"; // Ciąg do sprawdzenia
var regexp = /Ania/gim; // Ciąg z flagami i, g oraz m
```

### Metaznaki

- `^` - początek wzorca
- `$` - koniec wzorca
- `.` - dowolny znak oprócz znaku nowego wiersza
- `[...]` - dowolny z wymienionych znaków
- `[^...]` - dowolny z niewymienionych znaków
- `|` - dowolny z rozdzielonych znakiem ciągów
- `(...)` - zawężenie zasięgu
- `?` - zero lub jeden poprzedzający znak lub element
- `*` - zero lub więcej poprzedzających znaków lub elementów
- `+` - jeden lub więcej poprzedzających znaków lub elementów
- `{4}` - dokładnie 4 poprzedzające znaki lub elementy
- `{4,}`- 4 lub więcej poprzedzających znaków lub elementów
- `{2,4}` - od 2 do 4 poprzedzających znaków lub elementów
- `\` - ogólny znak zmiany znaczenia, różnie wykorzystywany

### Klasy znaków

**Klasa znaków** - część wzorca ujęta w nawiasy kwadratowe

- `\s` - znak spacji, tabulacji lub nowego wiersza
- `\S` - znak nie będący spacją, tabulacją lub znakiem nowego wiersza
- `\w` - każdy znak będący literą, cyfrą i znakiem `_`
- `\W` - każdy znak nie będący literą, cyfrą i znakiem `_`
- `\d` - każdy znak będący cyfrą
- `\D` - każdy znak nie będący cyfrą
- `[abc]` - oznacza jedną z liter a, b lub c
- `[a-z]` - dowolna mała litera
- `[a-zA-Z]` - dowolna litera
- `[ąćęłńóśżź]` - dowolna mała polska litera
- `[0-9\-+]` - dowolna cyfra lub znak + lub -, inaczej można zapisać `[\d\-+]`
- `[^0-9]` - dowolny znak nie będący cyfrą (to samo co `\D`), użyliśmy znaku `^` (zaprzeczenia logicznego klasy, musi być na pierwszej pozycji)

### Flagi

**flagi** - specjalne parametry, które oddziałują na wyszukiwanie wzorców

```javascript
const reg = /[a-z]*/gm;
const reg = new RegExp("[a-z]*", "g");
```

- `i` - powoduje niebranie pod uwagę wielkości liter
- `g` - powoduje zwracanie wszystkich pasujących fragmentów, a nie tylko pierwszego
- `m` - powoduje wyszukiwanie w tekście kilku liniowym. W trybie tym znak początku i końca wzorca `(^$`) jest wstawiany przed i po znaku nowej linii `(\n)`.

### Zastosowanie metody test()

`regexp.test(wyrazenie)` - metoda służąca do sprawdzania, czy dane wyrażenie znajduje się w tekście

```javascript
const text = "cat dog";
const reg = /cat/;
reg.test(text) === true;

const reg2 = /^cat$/;
alert(reg2.test(text)); // false - wzorzec zaczyna się z początkiem i kończy z końcem tekstu (znaki ^ i $) - jedyny pasujący tekst to "cat"
```

### Zastosowanie metody exec()

`regexp.excec(wyrazenie)` - metoda przeszukuje dany ciąg znaków, a następnie zwraca tablicę zawierającą składowe pierwszego wyszukanego fragmentu.

```javascript
const re = /d(b+)(d)/gi;
const result = re.exec("cdbBdbsbz");

console.log(result[0]); // dbBd
console.log(result.index); // 1
console.log(result.input); // cdbBdbsbz

console.log(re.lastIndex); // 5
console.log(re.multiline); // false
console.log(re.ignoreCase); // true
console.log(re.source); // d(b+)(d)
```

### match()

Obiekt `String` posiada metodę `match()`, która spełnia tę samą funkcję co metoda `exec()` obiektu RexExp, jednak zwraca od razu wszystkie pasujące fragmenty.

```javascript
const text = "Numer1, Numer2, Numer3, NumerB, Numer5, NumerD";
const reg = /Numer[1-4A-C]/g;
console.log(text.match(reg)); //Numer1, Numer2, Numer3, NumerB
```

```javascript
const reg = /d(b+)(d)/gi;
const result = "cdbBdbsbz".match(reg);

if (result.length) {
  console.log(result.join("-")); //dbBd
}
```

### Zastosowanie metody search()

`regexp.search(wyrazenie)` - metoda obiektu `RexExp` działa tak samo jak metoda `indexOf()`obiektu string, czyli zwraca indeks pierwszego wystąpienia podciągu w ciągu

```javascript
const text = "Fantomas robi masę - marchewkowo-marcepanowa";
const reg = /at/gi";

console.log("Search: " + text.search(reg));
console.log("Index of: " + text.indexOf("at"));
```

### Zastosowanie metody replace()

Obiekt `String` posiada metodę `replace()`, która służy do zamiany jednego ciągu na drugi. Przy jej stosowaniu możemy używać wyrażeń regularnych.

```javascript
const text = "Super Samson jest fajny.";
const reg = /fajny/;
const textEnhanced = text.replace(reg, function(match) {
  return "super" + match;
});

console.log(textEnhanced); // Super Samson jest super fajny
```
