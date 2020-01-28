# JavaScript - CSS

## Manipulacja CSS

### Właściwości i metody CSS

#### style

- Jeżeli właściwość składa się z jednego słowa, to zapisujemy ją tak jak w css
- Jeżeli właściwość składa się z kilku słów oddzielonych myślnikiem, stosujemy CamelCase lub norację z kropką

```javascript
const btn = document.querySelector(".button");

btn.addEventListener("click", function() {
  this.style.backgroundColor = "#4BA2EA";
  this.style.fontSize = "1.6rem";
  this.style.borderRadius = "3rem";
  this.style.color = "#F7F781";
});
```

#### setProperty()

`style.setProperty(propertyName, value, priority*)` - służy do ustawiania stylowania. Ostatni opcjonalny parametr priority służy do ewentualnego dodania do danych styli deklaracji `!important` i najczęściej jest pomijany.

#### getPropertyValue()

`style.getPropertyValue(property)` - służy do pobierania stylowania

```javascript
const btn = document.querySelector(".button");

btn.addEventListener("click", function() {
  if (this.style.getPropertyValue("font-size") !== "1.5rem") {
    this.style.setProperty("background-color", "#4BA2EA");
    this.style.setProperty("font-size", "1.5rem");
    this.style.setProperty("border-radius", "3rem");
  } else {
    this.style.setProperty("background-color", "");
    this.style.setProperty("font-size", "");
    this.style.setProperty("border-radius", "");
  }
});
```

#### getComputedStyle()

`getComputedStyle(elem, pseudoEl*)` - pobiera style zadeklarowane w arkuszach stylów. Zwraca przeliczone przez przeglądarkę stylowanie.

- Pierwszy parametr określa badany element
- Drugi - opcjonalny pozwala pobierać style dla pseudo elementów (wtedy podajemy selektor pseudoelementu jako string)

```javascript
const btn = document.querySelector(".button");
const styleComp = getComputedStyle(btn);

console.log(styleComp.getPropertyValue("height"));
console.log(styleComp.width);
console.log(styleComp["background-color"]);

// Pobieramy style dla pseudo elementu
const btn = document.querySelector(".button-pseudo");
const styleComp = getComputedStyle(btn, "::before"); //pobieram dane dla pseudoelementu
```

#### classList

| Nazwa                     | Co robi                                                      |
| ------------------------- | ------------------------------------------------------------ |
| `add("nazwa-klasy")`      | dodawanie klasy                                              |
| `remove("nazwa-klasy")`   | usuwanie klasy                                               |
| `toggle("nazwa-klasy")`   | przełączanie (jak nie ma to dodaje, jak jest to usuwa) klasy |
| `contains("nazwa-klasy")` | sprawdza czy element ma taką klasę                           |

```javascript
const btn = document.querySelector(".btn");

btn.classList; //zwraca pseudo tablicę z nazwami klas
btn.classList.add("btn"); //dodaję klasę .btn
btn.classList.remove("btn"); //usuwam klasę .btn
btn.classList.toggle("btn"); //przełączam (dodaję lub usuwam) klasę .btn
btn.classList.contains("btn"); //sprawdzam czy dany element ma klasę .btn
```

#### className

`className` - zwraca jako tekst wszystkie klasy jakie posiada dany element

```javascript
const btn = document.querySelector(".btn");
console.log(btn.className); //btn btn-primary
```

### Zmienne w CSS

Zmienne w CSS zachowują się podobnie do zmiennych w JS - ich zasięg jest dostępny dla coraz bardziej zagnieżdżonych elementów (tak jak zmienne w JS są dostępne dla coraz bardziej zagnieżdżonych funkcji).

```css
:root {
  --color: red; /* zmienne deklarujemy poprzedzając ich nazwę -- */
}

.module-error {
  border: 1px solid var(--color); /* a używamy ze słowem var */
  box-shadow: 0 1px 3px var(--color);
}
.module-error-title {
  color: var(--color);
}
```

```css
.header {
  --font-size: 14px; /* zmienne dostępne tylko dla .header i jego dzieci */
  --color1: #222;
  --color2: #000;
  --color-link: #fff;

  background: linear-gradient(var(--color1), var(--color2));
}

.header a {
  color: var(--color-link); /* ok */
}

.element {
  /* jeżeli ten element nie jest w header to nie ma dostępu do powyższych zmiennych */
}
```
