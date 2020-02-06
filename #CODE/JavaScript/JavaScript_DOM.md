# JavaScript - Document Object Model

## Document Object Model

**Document Object Model (DOM)** - model, interfejs, który za pomocą metod i właściwości odzwierciedla dokument HTML.

Składniki:

- Navigator - informacje o urządzeniu
- Window - informacje o przeglądarce
- Document - wyświetlany dokument np. plik HTML
- Element - tag HTML
- Node - zawartość elementu (tekst, tag itd.)

## Umieszczanie skryptów a DOM

Skrypty powinny być wczytywane po załadowaniu drzewa DOM. Aby się upewnić, że tak się stanie można:

- Umieścić znaczniki `<script></script>` w pliku `html` przed tagiem zamykającym `body`
- Dodać instrukcję `addEventListener` dla `DOMContentLoaded`

```javascript
document.addEventListener("DOMContentLoaded", function() {
    ...
});

document.addEventListener("DOMContentLoaded", nazwaFunkcji);
```

## Pobieranie elementów

### getElementById()

`getElementById(id)` - pobiera element o danym id

```javascript
document.addEventListener("DOMContentLoaded", function() {
  const btn = document.getElementById("btn");
  console.log(btn.innerText); // Kliknij mnie
});
```

### getElementsByTagName()

`getElementsByTagName(tag)` - pobiera kolekcję elementów o danym znaczniku

```javascript
document.addEventListener("DOMContentLoaded", function() {
  const tab = document.getElementById("tabelka");

  const td = tab.getElementsByTagName("td"); //pobieramy wszystkie td z tabeli
  console.log(td.length); //wypisuje sobie ilość elementów w kolekcji

  for (let i = 0; i < td.length; i++) {
    //pętla po wszystkich td
    td[i].style.backgroundColor = "red"; //ustawiamy tło komórek na czerwone
  }
});
```

### getElementsByClassName()

`getElementsByClassName(tag)` - pobiera kolekcję elementów po klasie

```javascript
document.addEventListener("DOMContentLoaded", function() {
  const buttons = document.getElementsByClassName("btn");

  for (let i = 0; i < buttons.length; i++) {
    //pętla po wszystkich buttonach o klasie .btn
    buttons[i].style.color = "white";
  }
});
```

### querySelector()

`querySelector(selector)` - zwraca pierwszy pasujący do selektora element, lub `null`, gdy nic nie znajdzie

```javascript
// Pobieramy pierwszy element .btn-primary w elemencie .module
const btn = document.querySelector(".module .btn-primary");

// Pobieramy pierwszy .btn w pierwszym li listy ul
const btnInFirstLi = document.querySelector("ul li:fist-of-type .btn");

// Pobieram tytuł w module
const module = document.querySelector(".module");
const title = module.querySelector(".module-title");

// Pobieram element .module który nie jest divem
const module = document.querySelector(".module:not(div)");

// Pobieram paragrafy, ale te które nie są pierwszym dzieckiem swojego rodzica
const p = document.querySelector("p:not(:first-child)");
```

### querySelectorAll()

`querySelectorAll(selector)` - zwraca kolekcję elementów lub pustą kolekcję gdy nic nie znajdzie

```javascript
const modules = document.querySelectorAll(".module");

for (const module of modules) {
  //pobieramy pojedynczy przycisk danego modulu
  const moduleToggle = module.querySelector(".module-toggle");

  //dodajemy mu klik
  moduleToggle.addEventListener("click", function() {
    const title = module.querySelector(".module-title").innerText;
    console.log(title);
  });
}
```

## Pętle po kolekcjach

Aby wykonać pętlę po elementach kolekcji możemy skorzystać z tradycyjnych pętli takich jak `for` czy `for of`.

```javascript
const divs = document.querySelectorAll('.module');

for (let i=0; i<divs.length; i++) {
    divs[i].style.color = "red";
}`
```

`forEach` została w nowych przeglądarkach dodana także dla kolekcji elementów.

```javascript
// To zadziała tylko w nowych przeglądarkach
document.querySelectorAll(".module").forEach(function(el) {
  el.style.color = "blue";
});
```

Alternatywny zapis dla starszych przeglądarek

```javascript
const divs = document.querySelectorAll("div.module");

[].forEach.call(divs, function(el) {
  el.style.background = "red";
});
```

Kolekcja mimo, że przypomina tablicę nie jest nią. Metod typowych dla tablic takich jak (`filter`, `some`, `map` itp.) nie będziemy mogli użyć, chyba, że wcześniej zamienimy taką kolekcję na typową tablicę za pomocą `spread operatora`

```javascript
const buttons = document.querySelectorAll("button");
const texts = [...buttons].filter(el => el.innerText.length >= 5);
// Tylko buttony, których tekst jest dłuższy niż 5 liter
```

Lub przy pomocy funkcji `Array.from()`

```javascript
const divs = document.querySelectorAll("div.module");

Array.from(divs).forEach(el => {
  console.log(el);
});

Array.from(divs).filter(el => {
  console.log(el);
});
```

Metody `getElementsBy...` zwracają tak zwane **żywe kolekcje** (dynamicznie aktualizujące się) w przeciwieństwie do metod `querySelector()` i `querySelectorAll()`.

### :scope

`:scope` - pseudoklasa reprezentująca elementy, które są punktem odniesienia dla selektorów do dopasowania

### Gotowe kolekcje

Wiele elementów dokumentu mamy bazowo podstawione pod zmienne i nie musimy ich wyciągać za pomocą dodatkowych metod.

- `document.forms` - formularze na stronie
- `document.images` - grafiki img na stronie
- `document.links` - linki na stronie
- `document.anchors` - linki będące kotwicami
- `document.body` - element body

**Uwaga:** Jeżeli stworzymy w HTML jakiś element z atrybutem `id`, w JavaScript zostanie dla nas stworzona zmienna o takiej samej nazwie, która będzie wskazywała na ten element, dlatego aby uniknąć niepotrzebnych konfliktów warto stylować za pomocą klas.

```html
<div id="test"></div>
console.log(test);
```

## Właściwości i metody elementów (Element)

| Nazwa                                                                            | Co robi                                                                                            |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `element.innerHTML`                                                              | zwraca lub ustawia kod HTML danego element                                                         |
| `element.outerHTML`                                                              | zwraca lub ustawia kod HTML wraz z tagiem                                                          |
| `HTMLElement.innerText`                                                          | zwraca lub ustawia tekst znajdujący się w elemencie (bez html)                                     |
| `element.insertAdjacentElement(position, element)`                               | dodaje element na wskazanej pozycji relatywnie względem Elementu na którym została wywołana metoda |
| `tagName`                                                                        | zwraca nazwę tagu                                                                                  |
| `element.getAttribute("name")`                                                   | pobiera atrybut elementu                                                                           |
| `element.setAttribute("name", "value")`                                          | ustawia atrybut `name` elementu na wartość `value`                                                 |
| `hasAttribute`                                                                   | sprawdza czy element ma dany atrybut                                                               |
| `element.dataset`                                                                | zwraca (obiekt) `dataset`, który przetrzymuje customowe atrybuty (`data-wlasnanazwa`).             |
| `element.classList`                                                              | zwraca zawartość atrybutu `class` w postaci stringa                                                |
| `element.classList.remove("name")`                                               | usuwa klasę name z elementu                                                                        |
| `element.classList.add("name")`                                                  | dodaje klasę name do elementu                                                                      |
| `element.classList.toggle("name")`                                               | dodaje/usuwa klasę z elementu w zależności od podanego warunku                                     |
| `element.classList.contains("name")`                                             | zwraca `true/false` w zależności od tego czy element posiada klasę                                 |
| `element.classList.replace("n1", "n2")`                                          | zastępuje klasę `n1` klasą `n2`                                                                    | `element.parentElement` | rodzic elementu lub `null` |
| `element.nextElementSibling`                                                     | następny element (brat) lub `null`                                                                 |
| `element.previousElementSibling`                                                 | poprzedni element (brat) lub `null`                                                                |
| `element.children`                                                               | dzieci elementu lub pusta tablica                                                                  |
| `element.firstElementChild` lub<br> `element.children[0]`                        | pierwsze dziecko elementu lub `null`                                                               |
| `element.lastElementChild` lub<br> `element.children[element.children.length-1]` | ostatnie dziecko elementu lub `null`                                                               |  |

### innerHTML

`innerHTML` - zwraca lub ustawia kod HTML danego element

```javascript
const btn = document.querySelector(".btn");
console.log(btn.innerHTML); //<span>Kliknij mnie!</span>
btn.innerHTML = "<span>Nie klikaj mnie!</span>";
```

### outerHTML

`outerHTML` - zwraca lub ustawia kod HTML wraz z tagiem

```javascript
const btn = document.querySelector(".btn");
console.log(btn.outerHTML);
// <button class="button" type="button"><span>Kliknij mnie</span></button>
```

### innerText

`innerText` - zwraca lub ustawia tekst znajdujący się w elemencie (bez html) po zaaplikowaniu stylów (np. `display:none;`)

```javascript
const btn = document.querySelector(".btn");

console.log(btn.innerHTML); //<span>Kliknij mnie</span>
console.log(btn.innerText); //Kliknij mnie
console.log(btn.textContent); //Kliknij mnie
```

### textContent

`textContent`- zwraca lub ustawia tekst znajdujący się w elemencie, pomija style (czyli pokaże ukryte za pomocą CSS elementy)

### tagName

`tagName`- zwraca nazwę tagu

```javascript
const btn = document.querySelector(".button");
console.log(btn.tagName); // Zwraca BUTTON
```

### getAttribute

`getAttribute(nazwaAtrybutu)`- pobiera atrybut elementu. Jeżeli dany atrybut nie zostanie odnaleziony, metoda zwróci `null`

### setAttribute

`setAttribute(nazwaAtrybutu, wartość)` - ustawia atrybut elementu

```html
<a href="http://google.pl"> Wyszukaj </a>
```

```javascript
const a = document.querySelector("a");
const href = a.getAttribute("href"); // http://google.pl
const target = a.getAttribute("target"); // null
```

### hasAttribute

`hasAttribute(nazwaAtrybutu)`- sprawdza czy element ma dany atrybut

### removeAttribute

`removeAttribute(nazwaAtrybutu)`- służy do usunięcia atrybutu

```javascript
const inputs = document.querySelector("input[readonly]"); // Pobiera pola readonly
for (const el of inputs) {
  el.removeAttribute("readonly");
}
```

### dataset

`dataset` - zwraca (obiekt) `dataset`, który przetrzymuje customowe atrybuty (`data-...`).

Atrybuty mogą być domyślne (np. `src`, `alt`, `tooltip`, `class` itp), oraz nasze własne. Te drugie powinny zaczynać się od słowa `data-` np. `data-text`. Atrybuty takie możemy obsługiwać za pomocą powyższych metod tak samo jak wszystkie atrybuty, ale też możemy dla nich skorzystać z właściwości `dataset`.

```html
<span class="tooltip" data-default-text="Lubie koty i psy" data-position="top">
  lorem ipsum
</span>
```

```javascript
const tooltip = document.querySelector(".tooltip");
console.log(tooltip.dataset.defaultText);
console.log(tooltip.dataset.position);
```

Zapis podczas odwołwania się - początek `data-` został pominięty, a zapis `default-text` zmieniliśmy na pisany camelCase czyli `defaultText`.

**Uwaga:** Jeżeli chcesz mieć pewność, że pobierasz dokładnie to co zostało wpisane w HTML, używaj `get/setAttribute`. Jeżeli działasz na dynamicznych wartościach (np. zmieniająca się wartość pola, jego pozycja itp) - używaj właściwości obiektu.

## Właściwości i metody węzłów (Node)

| Nazwa                  | Zwraca                                     |
| ---------------------- | ------------------------------------------ |
| `Node.childNodes`      | dzieci węzła lub pusta tablica             |
| `Node.firstChild`      | pierwsze dziecko węzła lub `null` gdy brak |
| `Node.lastChild`       | ostatnie dziecko węzła lub `null` gdy brak |
| `Node.parentNode`      | rodzica wskazanego węzła                   |
| `Node.nextSibling`     | węzeł poprzedzający lub `null` gdy brak    |
| `Node.previousSibling` | następny węzeł lub `null` gdy brak         |

```javascript
const text = document.querySelector("#text");

text.parentElement; // Wskazuje na nadrzędny node będący elementem - div.text-cnt
text.parentNode; // Wskazuje na nadrzędny node - div.text-cnt

text.firstChild; // Pierwszy node - w naszym przypadku to tekst "Mała "
text.lastChild; // Ostatni node - "" - html jest sformatowany, wiec ostatnim nodem jest znak nowej linii

text.firstElementChild; // Pierwszy element - <strong style="color:red">Ala</strong>
text.lastElementChild; // Ostatni element - <span style="color:blue">kota</span>

text.children; // [strong, span] - kolekcja elementów
text.children[0]; // Wskazuje na 1 element - <strong style="color:red">Ala</strong>

text.childNodes; // [text, strong, text] - kolekcja wszystkich dzieci - nodów
text.childNodes[0]; // "Mała"

text.nextSibling; // Następny węzeł
text.previousSibling; // Poprzedni węzeł
text.nextElementSibling; // Następny brat-element
text.previousElementSibling; // Poprzedni brat-element

text.firstElementChild.nextElementSibling; // Kolejny brat-element pierwszego elementu - <span style="color:blue">kota</span>
text.firstElementChild.nextSibling; // Kolejny brat-node pierwszego elementu - "miała"

text.firstElementChild.previousElementSibling; // Poprzedni brat-element pierwszego elementu - null, bo przed pierwszym stron nie ma elementów
text.firstElementChild.previousSibling; // Poprzedni brat-node pierwszego elementu - "Mała"

//powyższe możemy łączyć
text.children[0].firstChild; // Pierwszy element i w nim pierwszy nod : "Ala"
text.children[0].firstElementChild; // null - w pierwszym strong nie mamy juz elementów

text.firstChild.firstElementChild; // null - nie ma elementu w pierwszym tekście
text.firstElementChild.firstElementChild; // null - nie ma elementy w strong
text.firstElementChild.firstChild; // "Ala"
```

### closest()

`closest(selektor)`- odnajduje najbliższy elementowi element który pasuje do selektora

```html
<div class="module">
  <div class="module-content">
    <div>
      <div class="module-text">
        Lorem ipsum dolor sit amet...
      </div>
      <button class="button">Kliknij</button>
    </div>
  </div>
</div>
```

```javascript
document.querySelector(".button").addEventListener("click", function() {
  const module = this.closest(".module");
});
```

## Tworzenie i usuwanie elementów

### createElement

`document.createElement(typ)` - metoda tworzy pojedynczy element

### appendChild

`parentElement.appendChild(nowyElement)` - wstawia element do drzewa dokumentu

### insertBefore

`parentNode.insertBefore(newElement, element)` - wstawia dany element przed wskazanym

### createTextNode

`createTextNode()` - tworzy pojedynczy węzeł tekstowy

### append, prepend, before i after

| Nazwa       | Co robi                                           |
| ----------- | ------------------------------------------------- |
| `append()`  | wstawia treść/element na koniec danego elementu   |
| `prepend()` | wstawia treść/element na początku danego elementu |
| `before()`  | wstawia treść/element przed danym elementem       |
| `after()`   | wstawia treść/element za danym elementem          |

### cloneNode()

`cloneNode(deep)`- tworzy kopię html danego elementu (bez eventów)

### Usuwanie elementów

- `element.remove()`
- `parentNode.removeChild(element)`
- `removeChild()`
- `remove()`

### Zastępowanie elementów

`parent.replaceChild(newChild, oldChild)` - zastepuje jeden element drugim

### Tworzenie fragmentów dokumentu

`createDocumentFragment()`

## Zamiana stringów na elementy HTML

`Document.createRange()` - metoda tworzy nowy obiekt `Range`

```javascript
let range = document.createRange();
```

`Range.createContextualFragment()`

```javascript
let documentFragment = range.createContextualFragment(tagString);
```

```javascript
// Tworzymy string zawierający kod HTML
const myHTML = `
  <div class="wrapper">
    <h2>Cute ${desc}</h2>
    <img src="${src}" alt="${desc}"/>
  </div>
`;

// Przekształcamy string w element DOM
const myFragment = document.createRange().createContextualFragment(myHTML);

// Umieszczamy element DOM w treści dokumentu
document.body.appendChild(myFragment);
```
