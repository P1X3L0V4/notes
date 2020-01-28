# JavaScript - Pętle

## Pętle

### for

```javascript
for (zainicjowanie_licznika;  warunek_kończący_wykonywanie_pętli;  zmiana_licznika) {
    kod który zostanie wykonany pewną ilość razy
}
```

```javascript
for (let i = 0; i < 10; i++) {
  console.log(i);
}

let sum = 0;
for (let i = 0; i < 10; i++) {
  sum += i;
}
console.log(sum); // Zwróci 45
```

### while

```javascript
while (wyrażenie-sprawdzające-zakończenie-pętli) {
    ...fragment kodu który będzie powtarzany...
}
```

```javascript
let i = 1;

while (i <= 100) {
  console.log("Nie będę...");
  i++;
}
```

#### do while

```javascript
let i = 0;

do {
  i++;
  console.log(i);
} while (false);
```

Warunek od początku nie spełniony ale i tak wykona się 1 raz (najpierw wykonywane jest do a potem sprawdzany warunek)

### for of

W wersji ES6 wprowadzono pętlę for of, która służy do iterowania po zmiennych iterowalnych (stringi, kolekcje, tablice itp).

```javascript
const tab = [1, 2, 3, 4];

for (const el of tab) {
  console.log(el);
}

const buttons = document.querySelectorAll("button");
for (const btn of buttons) {
  console.log(btn);
}

const txt = "ALa ma kota";
for (const letter of txt) {
  console.log(letter.toUpperCase());
}
```

### Instrukcje break i continue

**break** - kończy wykonywanie pętli

```javascript
const tab = ["Ala", "Monika", "Beata", "Karol"];

let userExist = false;

for (let i = 0; i < tab.length; i++) {
  if (tab[i] === "Beata") {
    userExist = true;
    break; // Dalej nie ma sensu sprawdzać
  }
}
```

**continue** - powoduje przerwanie danej iteracji (aktualnego powtórzenia)

```javascript
const tab = ["Ala", "Monika", "Beata", "Karol", "Alicja"];

for (let i = 0; i < tab.length; i++) {
  if (tab[i] === "Karol") {
    continue; // Karola pomiń
  }
  console.log(tab[i]);
}
```