# JavaScript - Instrukcje warunkowe

## Instrukcje warunkowe

### if

Instrukcja if sprawdza dany warunek, i w zależności czy jest on równy true lub false wykona lub nie wykona sekcję kodu zawartą w klamrach:

```javascript
if (warunek) {
    ...instrukcje jeżeli warunek jest spełniony
}

// Przykłady:

const x = 1;
if (x === 1) { //warunek się wykona
    console.log('Liczba równa się 1');
}

const x = 2;
if (x !== 2) { //kod się nie wykona, bo x = 2
    console.log("Liczba " +x+ "jest różna od 2");
}
```

Wartości `false` dla warunku if:

```javascript
if (false)
if (null)
if (undefined)
if (0)
if (NaN)
if ('')
if ("")
if (document.all)
```

### else

Do podstawowego warunku if dodaje kod wykonywany w wypadku gdy warunek nie został spełniony

```javascript
const x = 5;

if (x === 1) {
  console.log("Liczba równa się 1");
} else {
  console.log("Liczba nie równa się 1");
}
```

### else if

Dodaje klilka sprawdzeń warunkowych

```javascript
const x = 5;

if (x > 5) {
  console.log("Liczba jest większa od 5");
} else if (x < 5) {
  console.log("Liczba jest mniejsza od 5");
} else {
  console.log("Liczba równa się 5");
}
```

### Operator warunkowy

Skrócona wersja warunku if

```javascript
const x = wyrażenie
  ? zwróć_jeżeli_wyrażenie_true
  : zwróć_jeżeli_wyrażenie_false;
```

```javascript
const i = 1;
let number = "";

if (i > 0) {
  number = "dodatnia";
} else {
  number = "ujemna";
}

// Zapis z pomocą operatora warunkowego
const number = i > 0 ? "dodatnia" : "ujemna";
```

```javascript
// Przykłady
const x = 3;
console.log(x % 2 === 0 ? "parzysta" : "nieparzysta");
// Zwraca 'nieparzysta'

const wiek = 21;
const status = wiek < 18 ? "jesteś za młody" : "zapraszamy na seans";
// Zwraca 'zapraszamy na seans'

const name = "Ola";
console.log(name === "Ola" ? "Masz na imię Ola" : "Nie masz na imię Ola");
// Zwraca 'Masz na imię Ola'

const someValue = user === "admin" ? true : false;

const answer = x === 2 ? "yes" : "no";

const isMember = true;
console.log("The fee is " + (isMember ? "$2.00" : "$10.00"));
```

### switch

```javascript
switch (wyrażenie) {
  case przypadek1:
    // Fragment kodu wykonywany gdy rezultat wyrażenia jest równy przypadek1 - potrzebuje break;
    break;
  case przypadek2:
    // Fragment kodu wykonywany gdy rezultat wyrażenia jest równy przypadek2 - potrzebuje break;
    break;
  default:
  // Fragment kodu wykonywany gdy powyższe rezultaty nie są równe rezultatowi wyrażenia - nie potrzebuje break;
}
```

Każdy przypadek kończy się słowem break, która kończy wykonywanie instrukcji switch.
Jeżeli pominiemy to słowo, wtedy nawet przy pomyślnym przyrównaniu zostaną wykonane kolejne sprawdzenia, co często może powodować błędy.

```javascript
const number = 4;
//Warunek zwróci "Numer równa się cztery"
switch (number) {
  case 1:
    console.log("Numer równa się jeden");
    break;
  case 2:
    console.log("Numer równa się dwa");
    break;
  case 3:
    console.log("Numer równa się trzy");
    break;
  case 4:
    console.log("Numer równa się cztery");
    break;
  default:
    console.log("Nie wiem ile równa się numer");
}
```
