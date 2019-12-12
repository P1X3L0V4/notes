# JavaScript

## Document Object Model

**Document Object Model (DOM)** - model, interfejs, który za pomocą metod i właściwości odzwierciedla dokument HTML.

### Pobieranie elementów

#### getElementById()

`getElementById(id)` - pobiera element o danym id

```javascript
document.addEventListener("DOMContentLoaded", function() {
    const btn = document.getElementById('btn');
    console.log(btn.innerText); // Kliknij mnie
});
```

#### getElementsByTagName()

`getElementsByTagName(tag)` - pobiera kolekcję elementów o danym znaczniku

```javascript
document.addEventListener("DOMContentLoaded", function() {
    const tab = document.getElementById('tabelka');

    const td = tab.getElementsByTagName('td'); //pobieramy wszystkie td z tabeli
    console.log(td.length); //wypisuje sobie ilość elementów w kolekcji

    for (let i=0; i<td.length; i++) { //pętla po wszystkich td
        td[i].style.backgroundColor = 'red'; //ustawiamy tło komórek na czerwone
    }
});
```
#### getElementsByClassName()

`getElementsByClassName(tag)` - pobiera kolekcję elementów po klasie

```javascript
document.addEventListener("DOMContentLoaded", function() {
    const buttons = document.getElementsByClassName('btn');

    for (let i=0; i<buttons.length; i++) { //pętla po wszystkich buttonach o klasie .btn
        buttons[i].style.color = "white";
    }
});
```

#### querySelector() i querySelectorAll()

`querySelector(selector)` - zwraca pierwszy pasujący do selektora element, lub null, gdy nic nie znajdzie

```javascript
// Pobieramy pierwszy element .btn-primary w elemencie .module
const btn = document.querySelector('.module .btn-primary');

// Pobieramy pierwszy .btn w pierwszym li listy ul
const btnInFirstLi = document.querySelector('ul li:fist-of-type .btn');

// Pobieram tytuł w module
const module = document.querySelector('.module');
const title = module.querySelector('.module-title');

// Pobieram element .module który nie jest divem
const module = document.querySelector('.module:not(div)');

// Pobieram paragrafy, ale te które nie są pierwszym dzieckiem swojego rodzica
const p = document.querySelector('p:not(:first-child)');
```

`querySelectorAll(selector)` - zwraca kolekcję elementów lub pustą kolekcję gdy nic nie znajdzie

```javascript
const modules = document.querySelectorAll('.module');

for (const module of modules) {
    //pobieramy pojedynczy przycisk danego modulu
    const moduleToggle = module.querySelector('.module-toggle');

    //dodajemy mu klik
    moduleToggle.addEventListener('click', function() {
        const title = module.querySelector('.module-title').innerText;
        console.log(title);
    });
}
```
### Pętle po kolekcjach
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
document.querySelectorAll('.module').forEach(function(el) {
    el.style.color = "blue";
});
```
Alternatywny zapis dla starszych przeglądarek

```javascript
const divs = document.querySelectorAll('div.module');

[].forEach.call(divs, function(el) {
    el.style.background = "red"
});
```

Kolekcja mimo, że przypomina tablicę nią nie jest. Metod typowych dla tablic takich jak (`filter`, `some`, `map` itp.) nie będziemy mogli użyć, chyba, że wcześniej zamienimy taką kolekcję na typową tablicę za pomocą `spread operatora`

```javascript
const buttons = document.querySelectorAll('button');
const texts = [...buttons].filter(el => el.innerText.length >= 5);
// Tylko buttony, których tekst jest dłuższy niż 5 liter
```

Lub przy pomocy funkcji `Array.from()`

```javascript
const divs = document.querySelectorAll('div.module');

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

**Uwaga:** Jeżeli stworzymy w HTML jakiś element z atrybutem id, w JavaScript zostanie dla nas stworzona zmienna o takiej samej nazwie, która będzie wskazywała na ten element, dlatego aby uniknąć niepotrzebnych konfliktów warto stylować za pomocą klas.

```html
<div id="test"></div>
console.log(test);
```

### Właściwości elementów

| Nazwa          | Co robi                                                                    |
| -------------- | -------------------------------------------------------------------------- |
| `innerHTML`    | zwraca lub ustawia kod HTML danego element                                 |
| `outerHTML`    | zwraca lub ustawia kod HTML wraz z tagiem                                  |
| `innerText`    | zwraca lub ustawia tekst znajdujący się w elemencie (bez html)             |
| `tagName`      | zwraca nazwę tagu                                                          |
| `getAttribute` | pobiera atrybut elementu                                                   |
| `setAttribute` | ustawia atrybut elementu                                                   |
| `hasAttribute` | sprawdza czy element ma dany atrybut                                       |
| `dataset`      | zwraca (obiekt) dataset, który przetrzymuje customowe atrybuty (data-...). |

#### innerHTML

`innerHTML` - zwraca lub ustawia kod HTML danego element

```javascript
const btn = document.querySelector('.btn');
console.log( btn.innerHTML ); //<span>Kliknij mnie!</span>
btn.innerHTML = "<span>Nie klikaj mnie!</span>"
```

#### outerHTML

`outerHTML` - zwraca lub ustawia kod HTML wraz z tagiem

```javascript
const btn = document.querySelector('.btn');
console.log(btn.outerHTML);
// <button class="button" type="button"><span>Kliknij mnie</span></button>
```

#### innerText

`innerText` - zwraca lub ustawia tekst znajdujący się w elemencie (bez html) po zaaplikowaniu stylów (np. `display:none;`)

```javascript
const btn = document.querySelector('.btn');

console.log(btn.innerHTML); //<span>Kliknij mnie</span>
console.log(btn.innerText); //Kliknij mnie
console.log(btn.textContent); //Kliknij mnie
```

#### textContent

`textContent `- zwraca lub ustawia tekst znajdujący się w elemencie, pomija style (czyli pokaże ukryte za pomocą CSS elementy)

#### tagName

`tagName `- zwraca nazwę tagu

```javascript
const btn = document.querySelector('.button');
console.log(btn.tagName); // Zwraca BUTTON
```

#### getAttribute

`getAttribute(nazwaAtrybutu) `- pobiera atrybut elementu. Jeżeli dany atrybut nie zostanie odnaleziony, metoda zwróci `null`

#### setAttribute

`setAttribute(nazwaAtrybutu, wartość)` - ustawia atrybut elementu

```html
<a href="http://google.pl"> Wyszukaj </a>
```

```javascript
const a = document.querySelector('a');
const href = a.getAttribute('href'); // http://google.pl
const target = a.getAttribute('target'); // null
```

#### hasAttribute

`hasAttribute(nazwaAtrybutu) `- sprawdza czy element ma dany atrybut

#### removeAttribute

`removeAttribute(nazwaAtrybutu) `- służy do usunięcia atrybutu

```javascript
const inputs = document.querySelector('input[readonly]'); // Pobiera pola readonly
for (const el of inputs) {
    el.removeAttribute('readonly');
}
```

#### dataset

`dataset` - zwraca (obiekt) `dataset`, który przetrzymuje customowe atrybuty (`data-...`).

Atrybuty mogą być domyślne (np. `src`, `alt`, `tooltip`, `class` itp), oraz nasze własne. Te drugie powinny zaczynać się od słowa `data-` np. `data-text`. Atrybuty takie możemy obsługiwać za pomocą powyższych metod tak samo jak wszystkie atrybuty, ale też możemy dla nich skorzystać z właściwości `dataset`.

```html
<span class="tooltip" data-default-text="Lubie koty i psy" data-position="top">
    lorem ipsum
</span>
```

```javascript
const tooltip = document.querySelector('.tooltip');
console.log(tooltip.dataset.defaultText);
console.log(tooltip.dataset.position);
```
Zapis podczas odwołwania się - początek `data-` został pominięty, a zapis `default-text` zmieniliśmy na pisany camelCase czyli `defaultText`.

**Uwaga:** Jeżeli chcesz mieć pewność, że pobierasz dokładnie to co zostało wpisane w HTML, używaj `get/setAttribute`. Jeżeli działasz na dynamicznych wartościach (np. zmieniająca się wartość pola, jego pozycja itp) - używaj właściwości obiektu.

### Węzły

#### Właściwości węzłów

| Nazwa                                                                    | Co robi                            |
| ------------------------------------------------------------------------ | ---------------------------------- |
| element.parentElement                                                    | rodzic elementu lub null           |
| element.nextElementSibling                                               | następny element (brat) lub null   |
| element.previousElementSibling                                           | poprzedni element (brat) lub null  |
| element.children                                                         | dzieci elementu lub pusta tablica  |
| element.firstElementChild lub element.children[0]                        | pierwsze dziecko elementu lub null |
| element.lastElementChild lub element.children[element.children.length-1] | ostatnie dziecko elementu lub null |

```javascript
const text = document.querySelector('#text');

text.parentElement // Wskazuje na nadrzędny nod będący elementem - div.text-cnt
text.parentNode // Wskazuje na nadrzędny nod - div.text-cnt

text.firstChild // Pierwszy node - w naszym przypadku to tekst "Mała "
text.lastChild // Ostatni node - "" - html jest sformatowany, wiec ostatnim nodem jest znak nowej linii

text.firstElementChild // Pierwszy element - <strong style="color:red">Ala</strong>
text.lastElementChild // Ostatni element - <span style="color:blue">kota</span>

text.children; // [strong, span] - kolekcja elementów
text.children[0] // Wskazuje na 1 element - <strong style="color:red">Ala</strong>

text.childNodes // [text, strong, text] - kolekcja wszystkich dzieci - nodów
text.childNodes[0] // "Mała"

text.nextSibling // Następny węzeł
text.previousSibling // Poprzedni węzeł
text.nextElementSibling // Następny brat-element
text.previousElementSibling // Poprzedni brat-element

text.firstElementChild.nextElementSibling // Kolejny brat-element pierwszego elementu - <span style="color:blue">kota</span>
text.firstElementChild.nextSibling // Kolejny brat-node pierwszego elementu - "miała"

text.firstElementChild.previousElementSibling // Poprzedni brat-element pierwszego elementu - null, bo przed pierwszym stron nie ma elementów
text.firstElementChild.previousSibling // Poprzedni brat-node pierwszego elementu - "Mała"

//powyższe możemy łączyć
text.children[0].firstChild // Pierwszy element i w nim pierwszy nod : "Ala"
text.children[0].firstElementChild // null - w pierwszym strong nie mamy juz elementów

text.firstChild.firstElementChild // null - nie ma elementu w pierwszym tekście
text.firstElementChild.firstElementChild // null - nie ma elementy w strong
text.firstElementChild.firstChild // "Ala"
```

#### closest()

`closest(selektor) `- odnajduje najbliższy elementowi element który pasuje do selektora

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
document.querySelector('.button').addEventListener('click', function() {
    const module = this.closest('.module');
})
```

### Tworzenie i usuwanie elementów

#### createElement

`document.createElement(typ)` - metoda tworzy pojedynczy element

#### appendChild

`parentElement.appendChild(nowyElement)` - wstawia element do drzewa dokumentu

#### insertBefore

`parentNode.insertBefore(newElement, element)` - wstawia dany element przed wskazanym

#### createTextNode

`createTextNode()` - tworzy pojedynczy węzeł tekstowy

#### append, prepend, before i after

| Nazwa       | Co robi                                           |
| ----------- | ------------------------------------------------- |
| `append()`  | wstawia treść/element na koniec danego elementu   |
| `prepend()` | wstawia treść/element na początku danego elementu |
| `before()`  | wstawia treść/element przed danym elementem       |
| `after()`   | wstawia treść/element za danym elementem          |

#### cloneNode()

`cloneNode(deep) `- tworzy kopię html danego elementu (bez eventów)

#### Usuwanie elementów

- `element.remove()`
- `parentNode.removeChild(element)`
- `removeChild()`
- `remove()`

#### Zastępowanie elementów

`parent.replaceChild(newChild, oldChild)` - zastepuje jeden element drugim

#### Tworzenie fragmentów dokumentu

`createDocumentFragment()`

## Style CSS

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

console.log( styleComp.getPropertyValue("height") );
console.log( styleComp.width );
console.log( styleComp['background-color'] );

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
const btn = document.querySelector('.btn');

btn.classList; //zwraca pseudo tablicę z nazwami klas
btn.classList.add('btn'); //dodaję klasę .btn
btn.classList.remove('btn'); //usuwam klasę .btn
btn.classList.toggle('btn'); //przełączam (dodaję lub usuwam) klasę .btn
btn.classList.contains('btn'); //sprawdzam czy dany element ma klasę .btn
```

#### className

`className` - zwraca jako tekst wszystkie klasy jakie posiada dany element

```javascript
const btn = document.querySelector('.btn');
console.log(btn.className); //btn btn-primary
```

### Zmienne w CSS

Zmienne w CSS zachowują się podobnie do zmiennych w JS - ich zasięg jest dostępny dla coraz bardziej zagnieżdżonych elementów (tak jak zmienne w JS są dostępne dla coraz bardziej zagnieżdżonych funkcji).

```css
:root {
    --color : red; /* zmienne deklarujemy poprzedzając ich nazwę -- */
}

.module-error {
    border:1px solid var(--color); /* a używamy ze słowem var */
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
    --color-link : #fff;

    background: linear-gradient(var(--color1), var(--color2));
}

.header a {
    color: var(--color-link); /* ok */
}

.element {
    /* jeżeli ten element nie jest w header to nie ma dostępu do powyższych zmiennych */
}
```

## Zdarzenia

**Zdarzenia** - czynności, które dzieją się w przeglądarce. Może je wywoływać użytkownik, lub element na stronie. Większość zdarzeń składa się z 3 faz:
- faza capture - kiedy event podąża od góry drzewa (od `window`) do danego elementu
- faza target - kiedy event dotrze do elementu, który wywołał to zdarzenie
- faza bubbling - kiedy event pnie się w górę drzewa aż dotrze do `window`

Niektóre eventy takie jak np. `focus`, `blur` domyślnie pomijają fazę bubbling.

[Event reference na MDN web docs](https://developer.mozilla.org/en-US/docs/Web/Events)

| Typ zdarzenia:       | Opis                                                                                                       |
| -------------------- | ---------------------------------------------------------------------------------------------------------- |
| `mouseover`          | odpalane, gdy kursor znalazł się na elemencie                                                              |
| `click`              | odpalane, gdy element został kliknięty (np. input)                                                         |
| `mouseout`           | odpalane, gdy kursor opuścił element                                                                       |
| `mouseenter`         | odpalane, gdy kursor znalazł się na elemencie                                                              |
| `mouseleave`         | odpalane, gdy kursor opuścił element                                                                       |
| `dblclick`           | odpalane, gdy podwójnie klikniemy na element (np. input)                                                   |
| `change`             | odpalane, gdy opuściliśmy element, i zmienił on swoją zawartość (np. pole tekstowe), ale też na zmianę np. | selekta, checkboxa itp. |
| `submit`             | odpalane, gdy formularz jest wysyłany                                                                      |
| `resize`             | odpalane, gdy rozmiar okna przeglądarki jest zmieniany                                                     |
| `focus`              | odpalane, gdy element stał się aktywny (np. pole tekstowe, link, button, element z tabindex)               |
| `blur`               | odpalane, gdy element przestał być aktywny (np. opuściliśmy input)                                         |
| `keydown`            | odpalane, gdy został naciśnięty klawisz na klawiaturze                                                     |
| `keyup`              | odpalane gdy puścimy klawisz na klawiaturze                                                                |
| `keydown`            | odpalane gdy naciśniemy klawisz, lub go przytrzymamy                                                       |
| `input`              | odpalany gdy coś wpiszemy do pola, wybierzemy coś z selecta, klikniemy na input itp.                       |
| `load`               | odpalane, gdy obiekt został załadowany (np. cała strona, pojedyncza grafika)                               |
| `contextmenu`        | odpalane, gdy kliknięto prawym klawiszem myszki i pojawiło się menu kontekstowe                            |
| `wheel`              | odpalane, gry kręcimy kółeczkiem myszki                                                                    |
| `select`             | odpalane, gdy zawartość obiektu została zaznaczona                                                         |
| `unload`             | odpalane, gdy użytkownik opuszcza dana stronę                                                              |
| `animationstart`     | odpalane, gdy animacja css się zacznie                                                                     |
| `animationend`       | odpalane, gdy animacja css się zakończy                                                                    |
| `animationiteration` | odpalane, gdy animacja css zrobi jedną iterację                                                            |
| `transitionstart`    | odpalane, gdy transition css się zacznie                                                                   |
| `transitionend`      | odpalane, gdy transition css się zakończy                                                                  |
| `transitionrun`      | odpalane, gdy transition zostanie stworzone (odpalane przed rozpoczęciem opóźnienia)                       |

### Podpinanie zdarzeń

Oznacza to, że zanim zaczniemy cokolwiek podpinać, musimy się upewnić, że został już wczytany html i zostało stworzone drzewo dokumentu.

Aby mieć pewność, że elementy już istnieją użyjemy jednej z trzech metod:
- Wstawienie skryptu na końcu strony (najlepiej tuż przed tagiem `</body>`)
- Dodanie do skryptu atrybutu `defer`
- Wykrycie czy dokument został w całości wczytany - zdarzenie `DOMContentLoaded`


### DOMContentLoaded

```javascript
document.addEventListener("DOMContentLoaded", function(event) {
    console.log("DOM został wczytany");
    console.log("Tutaj dopiero wyłapujemy elementy");
});
```
**Uwaga:** W bardzo wielu skryptach zamiast `DOMContentLoaded` używane jest zdarzenie `load` dla obiektu `window`. Jest to często błąd, wynikający z niewiedzy autora skryptu. Event `load` dla `window` jest odpalany, gdy wszystkie elementy na stronie zostaną załadowane - nie tylko drzewo dom, ale także i grafiki. Bardzo często będzie to powodować mocno zauważalne opóźnienia. Jeżeli więc twój skrypt ma tylko działać na elementach, a nie czekać na wczytanie całych grafik, zawsze używaj zdarzenia `DOMContentLoaded`.

### Rejestrowanie zdarzeń

Aby zdarzenie było dostępne dla danego obiektu, musimy je dla niego zarejestrować.

#### Bezpośrednio w kodzie HTML

Zdarzenia deklarowane inline, jako atrybut elementu. Metoda niezalecana:
- miesza warstwy logiki i danych - JavaScript z kodem HTML
- pozbawia kontekstu

```html
<a href="jakasStrona.html" onclick="alert('Kliknąłeś')"> kliknij </a>

<body onload="pageLoaded()">
    ...
</body>
```

#### Zdarzenie jako właściwość obiektu

Ta metoda przypisywania zdarzeń polega na ustawieniu zdarzenia jako właściwości danego obiektu.

- Przy podpinaniu funkcji przez referencję (przez nazwę) do zdarzeń pomijamy nawiasy, ponieważ nie chcemy wywoływać funkcji, a tylko ją podpiąć pod dane zdarzenie.
- Problem z tym modelem podpinania zdarzeń polega na tym, że do jednego elementu możemy podpiąć tylko jedną funkcję dla jednego rodzaju zdarzenia.

```javascript
function showText() {
    console.log('Kliknięto przycisk');
}

const element = document.querySelector('#przycisk');

element.onclick = showText;

element.onmouseover = function() {
    console.log('Najechano na przycisk');
}

// Usuwanie podpięcia
element.onclick = null;
```

#### addEventListener()

Funkcja `addEventListener()` przyjmuje 3 argumenty:
- typ zdarzenia
- funkcję wywoływaną
- trzeci opcjonalny argument, służący do ustawiania dodatkowych opcji dla eventu

```javascript
const element = document.querySelector('.btn');

function showMe() {
    console.log("Jakiś tekst");
}

function showSomething() {
    console.log("Inny tekst");
}

// Rejestrujemy 3 zdarzenia click dla elementu
element.addEventListener('click', showMe);
element.addEventListener('click', showSomething)
element.addEventListener('click', function() {
    this.style.color = 'red';
});
```

```javascript
// Wyrejestrowywanie funkcji
element.removeEventListener('click', showMe);
element.removeEventListener('click', showSomething);
```

### Wywyoływanie zdarzeń

```javascript
// Klikamy na element
element.click();

// Opuszczamy element
element.blur();

// Wskazuje dany element - tak jakbyśmy go wybrali np. za pomocą klawiatury
element.focus();

// Wysyłamy formularz
form.submit();
```

### Informacje o evencie

Podpinając funkcję do eventu, możemy ustawić jej parametr, pod który JavaScript wstawi nam obiekt z informacjami związanymi z tym eventem

```javascript
element.document.addEventListener('click', function(event) {
    console.log(event);
});
```

#### Typ zdarzenia

`e.type` - właściwość mówiąca o tym, jakiego typu jest dane zdarzenie

```javascript
const btn = document.querySelector('#uberButton');

btn.addEventListener('click', function(e) {
    console.log('Typ zdarzenia: ' + e.type);
});

```

#### Wstrzymanie domyślnej akcji

`e.preventDefault()` - metoda pozwalająca zapobiec wykonaniu domyślnej akcji

```javascript
form.addEventListener("submit", function(e) {
    e.preventDefault();
    console.log('Ten formularz się nie wyśle');
});

input.addEventListener("keydown", function(e) {
    e.preventDefault();
    console.log('W ten input nic nie wpiszesz');
});

link.addEventListener('click', function(e) {
    e.preventDefault();

    console.log('Ten link nigdzie nie przeniesie.');
});
```
Niektórych zdarzeń nie da się w ten sposób zatrzymać (np. load), o czym mówi nam właściwość `e.cancelable`

#### Zatrzymanie propagacji

`e.stopPropagation()` - blokuje propagację zdarzenia (wędrówkę). Jeżeli chcemy całkowicie zablokować przedostanie się danego typu eventu w górę, metodę `stopPropagation` musimy wywołać w pierwszej funkcji nasłuchującej.

```javascript
btn.addEventListener('click', function(e) {
    console.log('Kliknięto przycisk');
});

btn.addEventListener('click', function(e) {
    e.stopPropagation(); //powyższa funkcja już puściła event w górę
    console.log('Kliknięto przycisk');
});
```

#### target

`e.target` - właściwość wskazuje na element, na którym dane zdarzenie się wydarzyło

`e.currentTarget` wskazuje na element, który nasłuchuje dane zdarzenie

```javascript
const parent = document.querySelector('.parent');
parent.addEventListener('click', function(e) {
    console.log('e.target: ', e.target);
    console.log('e.currentTarget: ', e.currentTarget);
})
```

#### Ograniczanie ilości podpiętych eventów

Zamiast podpinać się bezpośrednio pod dane elementy np. `.delete` możemy podpniąć się pod rodzica i za pomocą `e.target` możemy sprawdzać jaki element wywołał dany event. Dzięki temu:
- ograniczamy liczbę eventów do jednego
- nasz event działa dla elementów, które dopiero zostaną dodane

```javascript
// Elementem nasłuchującym jest element .list, który istnieje od samego początku
list.addEventListener('click', function(e) {
    // e.target - ten który kliknął
    // e.currentTarget - ten który nasłuchuje

    if (e.target.classList.contains('.delete')) {
        const element = e.target.parentElement;
        element.parentElement.removeChild(element);
    }
});
```

### Customowe eventy

Nie musimy ograniczać się do eventów, które są domyślnie dostępne - możemy też tworzyć własne.

```javascript
const ob = {
    ...
}

const event = new CustomEvent('loadDataComplete', {
    detail: { ourData: ob },
    bubbles: true, // Idąc w góre dokumentu, event będzie odpalany dla elementów (jeżeli mają nasłuch)
	cancelable: false // Czy można przerwać za pomocą e.stopPropagation()
});
```

`e.isTrusted` - sprawdza, czy dany event został realnie wykonany przez użytkownika, czy wywołany poprzez skrypt

## Funkcje interwałowe

### setTimeout()

`setTimeout(fn, time)` - przyjmuje dwa parametry:
- funkcję, która ma zostać wywołana z opóźnieniem
- czas w milisekundach po jakim zostanie wywołana funkcja

```javascript
function myFunc() {
    console.log('Jakiś tekst');
}

setTimeout(myFunc, 1200); // Zostanie wywołana po 1.2 s
```

`clearTimeout()` - przerywa wcześniej zainicjowany `setTimeout`

### setInterval()

`setInterval(fn, time)` - przyjmuje dwa parametry:
- funkcję, która ma zostać wywołana
- czas w milisekundach co jaki ma zostać wywołana funkcja

```javascript
const time = setInterval(function() {
    console.log('Przykładowy napis');
}, 1000);
```

`clearInterval()` - przerywa wcześniej zainicjowany `setInterval`

### Technika throttle

```javascript
function throttled(delay, fn) {
    let lastCall = 0;
    return function (...args) {
        const now = (new Date).getTime();
        if (now - lastCall < delay) {
            return;
        }
        lastCall = now;
        return fn(...args);
    }
}
```

```javascript
const tHandler = throttled(200, printKey);
const input = document.querySelector('input');
input.addEventListener("input", tHandler);
```

### Technika debounce

**debounce** - technika, która pozwala na "zgrupowanie" wielu występujących jeden po drugim wywołań tej samej funkcji w jedno wywołanie.

```javascript
function debounced(delay, fn) {
    let timerId;
    return function (...args) {
        if (timerId) {
            clearTimeout(timerId);
        }
        timerId = setTimeout(() => {
            fn(...args);
            timerId = null;
        }, delay);
    }
}
```

```javascript
const tHandler = debounced(200, printKey);
const input = document.querySelector('input');
input.addEventListener("input", tHandler);
```

## Okna

### Okna dialogowe

```javascript
alert('Treść komunikatu'); // OK
confirm('Treść komunikatu'); // OK, Anuluj
prompt('Treść komunikatu', 'Domyślna wartość'); // Inputem, OK, Anuluj
```

### Okna przeglądarki

Otwieranie nowych okien za pomocą JavaScript jest niezalecane (sa one często blokowane). Struktura kodu:
- url -	ścieżka do otwieranej strony lub pusty ciąg, jeżeli okno generujemy dynamicznie
- name - nazwa okna, do której możemy się odwoływać atrybutem target w linkach i formularzach. Możemy też tutaj podać `target="_blank"` jeżeli chcemy otworzyć okno jako nową kartę
- options	- dodatkowe opcje otwieranego okna
```javascript
const win = window.open(url, name, options)
```

`opener` - właściwość która pozwala odwoływać do okna, z którego utworzyliśmy nowe okno. Może posłużyć do manipulowania

```javascript
opener.window.location = "https://www.mbąnk.pl/logoutpage.html?type=t"

// Przy otwieraniu nowych okien, warto używać właściwości noopener
const win = window.open('window-test-opener.html', 'target="_blank"', 'noopener,....');
<a href="..." target="_blank" rel="noopener">Klik</a>
```

## Cookies

### Format cookies

Format cookies w nagłówku `Set-Cookie`

```javascript
Set-Cookie: value;max-age=seconds;domain=domena;path=sciezka;secure;HttpOnly
```

| Parametr | Wymagane   | Co oznacza                                                          | Przykładowa wartość |
| -------- | ---------- | ------------------------------------------------------------------- | ------------------- |
| value    | Wymagane   | Wartość i nazwa ciasteczka                                          | username=Marcin     |
| max-age  | Opcjonalne | czas w sekundach                                                    | 6050050             |
| domain   | Opcjonalne | domena na której będzie działać to ciasteczko                       | domena.pl           |
| path     | Opcjonalne | sciezka do domeny, albo do podkatalogu                              | /                   |
| secure   | Opcjonalne | Zabezpieczenia ciasteczka. Czy ma ono się odwoływać tylko do https  | secure              |
| HttpOnly | Opcjonalne | Czy będzeimy mogli się odwoływać do ciasteczek z poziomu JavaScript | HttpOnly            |

### Tworzenie cookies

```javascript
document.cookie = "nazwaCookie=wartoscCookie; expires=dataWygasniecia; path=/; secure"
```

```javascript
// Funkcja tworząca ciasteczka
function setCookie(name, val, days, path, domain, secure) {
    if (navigator.cookieEnabled) { //czy ciasteczka są włączone
        const cookieName = encodeURIComponent(name);
        const cookieVal = encodeURIComponent(val);
        let cookieText = cookieName + "=" + cookieVal;

        if (typeof days === "number") {
            const data = new Date();
            data.setTime(data.getTime() + (days * 24*60*60*1000));
            cookieText += "; expires=" + data.toGMTString();
        }

        if (path) {
            cookieText += "; path=" + path;
        }
        if (domain) {
            cookieText += "; domain=" + domain;
        }
        if (secure) {
            cookieText += "; secure";
        }

        document.cookie = cookieText;
    }
}
```

### Odczyt cookies

```javascript
// Odczyt
nazwacookie1=wartosccookie1; nazwacookie2=wartosccookie2; nazwacookie3=wartosccookie3;

// Wydzielanie cześci cookie do tablicy
const cookies = document.cookie.split(/; */); // Dopasuje "; " ale też ";"
console.log(cookies[0]); // Zwróci nazwacookie1=wartosccookie1
console.log(cookies[0].split("=")[0]) // Nazwa pierwszego ciastka
console.log(cookies[0].split("=")[1]) // Wartość pierwszego ciastka

// Funkcja, w której pobieramy cookie za pomocą nazwy
function showCookie(name) {
    if (document.cookie !== "") {
        const cookies = document.cookie.split(/; */);

        for (let i=0; i<cookies.length; i++) {
            const cookieName = cookies[i].split("=")[0];
            const cookieVal = cookies[i].split("=")[1];
            if (cookieName === decodeURIComponent(name)) {
                return decodeURIComponent(cookieVal);
            }
        }
    }
}

//czytamy ciastko
console.log(showCookie("Przedmiot"));
```

### usuwanie cookies

```javascript
function deleteCookie(name) {
    const data = new Date();
    data.setTime(date.getMonth()-1);
    const name = encodeURIComponent(name);
    document.cookie = name + "=; expires=" + data.toGMTString();
}
```

## Wyrażenia regularne (RegExp)

`RegExp(wyrażenie, flaga)` - obiekt, który przyjmuje 2 argumenty:
- wyrażenie, którym będziemy testować
- dodatkowe flagi

```javascript
const reg = new RegExp("pani?" , "gi")
// lub
const reg = /pani?/gi

var regexp = new RegExp('Ania'); // Konstrukcja wyrażeń regularnych
var regexp = /Ania/; // Alternatywna konstrukcja wyrażeń regularnych
var imie = 'Ania'; // Ciąg do sprawdzenia
var regexp = /Ania/igm; // Ciąg z flagami i, g oraz m
```

### Metaznaki

- `^`  - początek wzorca
- `$`  - koniec wzorca
- `.`  - dowolny znak oprócz znaku nowego wiersza
- `[...]` - dowolny z wymienionych znaków
- `[^...]` - dowolny z niewymienionych znaków
- `|` - dowolny z rozdzielonych znakiem ciągów
- `(...)` - zawężenie zasięgu
- `?`  - zero lub jeden poprzedzający znak lub element
- `*`  - zero lub więcej poprzedzających znaków lub elementów
- `+`  - jeden lub więcej poprzedzających znaków lub elementów
- `{4}` - dokładnie 4 poprzedzające znaki lub elementy
- `{4,}`- 4 lub więcej poprzedzających znaków lub elementów
- `{2,4}` - od 2 do 4 poprzedzających znaków lub elementów
- `\`  - ogólny znak zmiany znaczenia, różnie wykorzystywany

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
const reg = /[a-z]*/mg
const reg = new RegExp("[a-z]*","g")
```

- `i` -	powoduje niebranie pod uwagę wielkości liter
- `g`	- powoduje zwracanie wszystkich pasujących fragmentów, a nie tylko pierwszego
- `m`	- powoduje wyszukiwanie w tekście kilku liniowym. W trybie tym znak początku i końca wzorca `(^$`) jest wstawiany przed i po znaku nowej linii `(\n)`.

### Zastosowanie metody test()

`regexp.test(wyrazenie)` - metoda służąca do sprawdzania, czy dane wyrażenie znajduje się w tekście

```javascript
const text = "cat dog";
const reg = /cat/;
reg.test(text) === true

const reg2 = /^cat$/;
alert(reg2.test(text)); // false - wzorzec zaczyna się z początkiem i kończy z końcem tekstu (znaki ^ i $) - jedyny pasujący tekst to "cat"
```

### Zastosowanie metody exec()

`regexp.excec(wyrazenie)` - metoda przeszukuje dany ciąg znaków, a następnie zwraca tablicę zawierającą składowe pierwszego wyszukanego fragmentu.

```javascript
const re = /d(b+)(d)/ig;
const result = re.exec("cdbBdbsbz");

console.log(result[0]) // dbBd
console.log(result.index) // 1
console.log(result.input) // cdbBdbsbz

console.log(re.lastIndex) // 5
console.log(re.multiline) // false
console.log(re.ignoreCase) // true
console.log(re.source) // d(b+)(d)
```

### Match()

Obiekt `String` posiada metodę `match()`, która spełnia tę samą funkcję co metoda `exec()` obiektu RexExp, jednak zwraca od razu wszystkie pasujące fragmenty.

```javascript
const text = "Numer1, Numer2, Numer3, NumerB, Numer5, NumerD";
const reg = /Numer[1-4A-C]/g;
console.log(text.match(reg)); //Numer1, Numer2, Numer3, NumerB
```

```javascript
const reg = /d(b+)(d)/ig;
const result = "cdbBdbsbz".match(reg);

if (result.length) {
    console.log(result.join('-')); //dbBd
}
```

### Zastosowanie metody search()

`regexp.search(wyrazenie)` - metoda obiektu `RexExp` działa tak samo jak metoda `indexOf() `obiektu string, czyli zwraca indeks pierwszego wystąpienia podciągu w ciągu

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

## Kontekst wykonania (Execution Context)

**Kontekst wykonania (Execution Context)** - abstrakcyjny koncept środowiska w którym interpretowany i wykonywany jest kod JavaScript\. Za każdym razem gdy uruchamiamy kod JS, dzieje się to w Execution Context.

**Typy kontekstów wykonania**

- **Global Execution Context** - globalny kontekst wykonania to domyślny kontekst wykonywania\, który obsługuje kod nie znajdujący się wewnątrz żadnej funkcji. W programie JavaScript może byc wyłącznie jeden taki kontekst.
- **Functional Execution Context** - lokalny (funkcyjny) kontekst wykonania; za każdym razem gdy wykonywana jest funkcja\, tworzony jest nowy kontekst dla tej funkcji. Każda funkcja posiada swój własny kontekst.
- **Eval Function Execution Context** - kod wykonywany wewnętrz funkcji `eval` posiada swój własny kontekst.

### Execution Stack

**Execution Stack** - miejsce w którym przechowywane są konteksty wykonania\. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.

**Przykładowe dodawanie kontekstów do Execution Stack**

1. Global Context
2. First Function Context
3. Second Function Context

**Przykładowe usuwanie kontekstów z Execution Stack**

1. Second Function Context
2. First Function Context
3. Global Context

#### Execution Stack - informacje

- Jednocześnie może być wykonywany wyłącznie jeden stos (single threaded)
- Wykonywanie odbywa się synchronicznie
- Istnieje wyłącznie jeden globalny kontekst
- Może istnieć dowolna ilość functional execution context
- Każde wywołanie funkcji tworzy nowy kontekst (nawet gdy odwołuje się sama do siebie)

#### Tworzenie Execution Stack

**1. Creation Stage** - etap uruchamiany w momencie gdy funkcja jest wywoływana lecz zanim zostanie wykonany kod\, który się w niej znajduje. W trakcie ustalane są:

- Łańcuch zakresów (Scope Chain)
- Definicje zmiennych, funkcji i argumentów
- Określana jest wartość słowa kluczowego `this`

```javascript
// Global Execution Context - Creation
globalExecutionContext = {
  activationObj: {
    argumentObj: {
      length: 0
    },
    temp: "uninitialized",
    old: undefined,
    first: "Pointer to the function definition"
  },
  scopeChain: ["global execution context variable object"],
  this: "global object"
};
```

**2. Activation / Execution Stage** - etap pod czas którego przypisywana jest wartość do zmiennych\, referencji funkcji oraz interpretowany / wykonywany jest kod\.

```javascript
// Global Execution Context - Execution
globalExecutionContext = {
  activationObj: {
    argumentObj: {
      length: 0
    },
    temp: 10,
    old: 5,
    first: "Pointer to the function definition"
  },
  scopeChain: ["global execution context variable object"],
  this: "global object"
};
```

## Zakres

**Przechowywanie i zarządzanie zmiennymi**
Zarządzanie zmiennymi jest fundamentalną cechą języka programowania i wymaga złożonego systemu zasad. System ten nazywamy zakresem.
**Zakres** - system\, któego rola polega na określeniu gdzie i w jaki sposób zmienne mogą być onalezione. Zmienne mogą być wyszukiwane na potrzeby:

- przypisania referencji (LHS - Left Hand Side look-up)
- zwrócenia wartości (RHS - Right Hand Side look-up)

|     LHS      |       |   RHS    |
| :----------: | :---: | :------: |
| `const name` |  `=`  | `"Anna"` |

### Zakres leksykalny

**Zakres dynamiczny** - zakres określany w momencie wykonywania kodu\. Nie jest wykorzystywany w JavaScript
**Zakres leksykalny (Lexical Scope)** - zakres określany w momencie definiowania kodu\, w czasie trwania fazy leksykalnej (lexical time). Jego strukturę określa informacja o tym gdzie definiowane są zmienne i bloki.

- Poszczególne zakresy mogą być w sobie wyłącznie ściśle zagnieżdżone
- JavaScript szukając identyfikatora zmiennej zaczyna od zakresu w którym się znajduje a następnie przechodzi do zewnętrznego zakresu i tak aż do momentu gdy dojdzie do zakresu globalnego lub do momentu odnalezienia szukanej wartości.

**Lexing (Tokenizing)** - pierwsza faza pracy kompilatora, polegająca na interpretowaniu ciągu tekstu kodu źródłowego na zrozumiałe dla silnika tokeny np. wyrażenie `const name = "Anna"` zostaje rozłożone na `["const", "name", "=", "Anna"]`
**Przysłonięcie (Shadow Ring)** - identyfikator znajdujący się w wewnętrznym scopie przesłania identyfikator znajdujący się w zewnętrznym scopie.
Definiowanie zmiennej `glob` za pomocą słowa kluczowego `var` spowoduje dodanie tej zmiennej do obiektu globalnego `window` i umożliwi dostęp do wartości zmiennej poprzez `window.glob`

### Silnik, kompilator i zakres

Engine & Compilator & Scope

- Engine - odpowiedzialny za kompilację i wykonanie kodu
- Compiler - odpowiedzialny za parsowanie i przygotowanie kodu dla silnika
- Scope - odpowiedzialny za gromadzenie i zarządzanie zadeklarowanymi zmiennymi i tym, w jaki sposób te informacje dostepne są dla aktualnie wykonywanego kodu.

#### Przykład działania

`const name = "Anna"`

**Kompilator**

1. Na etapie tworzenia globalnego zakresu kompilator pyta zakres o zmienną o identyfikatorze `name`. Dochodzi do przeszukania zakresu w celu przypisania referencji (przypisanie referencji - LHS). Zmienna nie zostaje znaleziona.
2. Ponieważ zmienna nie została znaleziona zakres tworzy nowy identyfikator `name` w `activationObj` znajdującym się w `globalExecutionContext`. W przypadku słowa kluczowego `const` wartość początkowa zostaje ustawiona na `uninitialized` (dla `var` byłoby to `undefined`). Kompilator kończy swoje zadanie.

**Silnik JavaScript**

1. Silnik JavaScript wykorzystuje utworzony kontekst aby wykonać kod. W celu przypisania wartości do zmiennej ponownie przeszukiwany jest zakres (zwrócenie wartości - RHS).
2. Zakres stwierdza, że zawiera szukaną zmienną `name` i przypisuje do niej wartość `Anna`

### Obsługa błędów

- przypisania referencji (LHS - Left Hand Side look-up)
  - w trybie "non-strict" gdy zmienna nie została znaleziona, zadeklarowana zostanie nowa zmienna o poszukiwanym identyfikatorze
  - w trybie "strict mode" gdy zmienna nie została znaleziona, zwrócenony zostanie `Refrence Error`
- zwrócenia wartości (RHS - Right Hand Side look-up)
  - gdy zmienna nie została znaleziona, w zakresie wrzucony zostanie `Refrence Error`
  - gdy zmienna zostanie znaleziona w zakresie, ale operacja którą wykonujemy nie jest dozwolona (np. wywołanie zmiennej która nie jest funkcją czy odwołanie się do wartości `null` lub `undefined`) - zwrócony zostanie `Type Error`

## Dobre praktyki

- Samodzielne wstawianie średników na końcu linii (inaczej JavaScript wstawia je automatycznie co może dać niepożądane efekty)
- Uważać na to gdzie wstawiamy nową linię (znak powrotu karetki) np. w przupadku nowej linii po słowie `return` parser może automatycznie wstawić średnik i zakończyć działanie funkcji.
- Dodawać metody do `prototype` konstruktora obiektu. Wtedy dana metoda zajmuje w pamięci mniej miejsca niż gdyby była umieszczona w konstuktorze i kopiowana za każdym razem gdy tworzony jest nowy pusty obiekt danego typu.

## Właściwości JavaScript

- Dla każdego elementu z ID w strukturze strony tworzona jest zmienna o takiej samej nazwie, która wskazuje na dany element

```javascript
console.log(mainContent); // Nie stworzyliśmy nigdzie zmiennej mainContent, ale jeśli na stronie znajduje się element o takim id console.log zwróci go
```
