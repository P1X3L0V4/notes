# JavaScript - Zdarzenia

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

## Podpinanie zdarzeń

Oznacza to, że zanim zaczniemy cokolwiek podpinać, musimy się upewnić, że został już wczytany html i zostało stworzone drzewo dokumentu.

Aby mieć pewność, że elementy już istnieją użyjemy jednej z trzech metod:

- Wstawienie skryptu na końcu strony (najlepiej tuż przed tagiem `</body>`)
- Dodanie do skryptu atrybutu `defer`
- Wykrycie czy dokument został w całości wczytany - zdarzenie `DOMContentLoaded`

### DOMContentLoaded

`DOMContentLoaded` warto wykorzystać jeżeli skrypt ma działać na elementach, a nie czekać na wczytanie całych grafik.

```javascript
document.addEventListener("DOMContentLoaded", function(event) {
  console.log("DOM został wczytany");
  console.log("Tutaj dopiero wyłapujemy elementy");
});
```

`load` dla `window` warto wykorzystać jeżeli skrypt do działania wymaga załadowania grafik lub innych elementów (często będzie to powodować mocno zauważalne opóźnienia).

### load

```javascript
window.addEventListener("load", event => {
  console.log("page is fully loaded");
});
```

## Rejestrowanie zdarzeń

Aby zdarzenie było dostępne dla danego obiektu, musimy je dla niego zarejestrować.

### Bezpośrednio w kodzie HTML

Zdarzenia deklarowane inline, jako atrybut elementu. Metoda niezalecana:

- miesza warstwy logiki i danych - JavaScript z kodem HTML
- pozbawia kontekstu

```html
<a href="jakasStrona.html" onclick="alert('Kliknąłeś')"> kliknij </a>

<body onload="pageLoaded()">
  ...
</body>
```

### Zdarzenie jako właściwość obiektu

Ta metoda przypisywania zdarzeń polega na ustawieniu zdarzenia jako właściwości danego obiektu.

- Przy podpinaniu funkcji przez referencję (przez nazwę) do zdarzeń pomijamy nawiasy, ponieważ nie chcemy wywoływać funkcji, a tylko ją podpiąć pod dane zdarzenie.
- Problem z tym modelem podpinania zdarzeń polega na tym, że do jednego elementu możemy podpiąć tylko jedną funkcję dla jednego rodzaju zdarzenia.

```javascript
function showText() {
  console.log("Kliknięto przycisk");
}

const element = document.querySelector("#przycisk");

element.onclick = showText;

element.onmouseover = function() {
  console.log("Najechano na przycisk");
};

// Usuwanie podpięcia
element.onclick = null;
```

### addEventListener() & removeEventListener()

Funkcja `addEventListener()` przyjmuje 3 argumenty:

- typ zdarzenia
- funkcję wywoływaną
- trzeci opcjonalny argument, służący do ustawiania dodatkowych opcji dla eventu

```javascript
const element = document.querySelector(".btn");

function showMe() {
  console.log("Jakiś tekst");
}

function showSomething() {
  console.log("Inny tekst");
}

// Rejestrujemy 3 zdarzenia click dla elementu
element.addEventListener("click", showMe);
element.addEventListener("click", showSomething);
element.addEventListener("click", function() {
  this.style.color = "red";
});
```

```javascript
// Wyrejestrowywanie funkcji
element.removeEventListener("click", showMe);
element.removeEventListener("click", showSomething);
```

### Obiekt opcji

Do metody `addEventListener` jako trzeci parametr możemy dodać obiekt z opcjami

```javascript
window.addEventListener(
  "click",
  function(event) {
    console.log("YOU CLICKED THE WINDOW");
    console.log(event.target);
    console.log(event.type);
    console.log(event.bubbles);
  },
  { capture: true } // Obiekt z opcjami
);
```

## Wywoływanie zdarzeń

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

## Obiekt event

Podpinając funkcję do zdarzenia, możemy ustawić jej parametr o dowolnej nazwie (zwyczajowo `event` lub `e`), pod który JavaScript wstawi nam obiekt z informacjami związanymi z tym zdarzeniem.

```javascript
element.document.addEventListener("click", function(event) {
  console.log(event);
});
```

## Typ zdarzenia

`e.type` - właściwość mówiąca o tym, jakiego typu jest dane zdarzenie

```javascript
const btn = document.querySelector("#uberButton");

btn.addEventListener("click", function(e) {
  console.log("Typ zdarzenia: " + e.type);
});
```

### Wstrzymanie domyślnej akcji

`e.preventDefault()` - metoda pozwalająca zapobiec wykonaniu domyślnej akcji

```javascript
form.addEventListener("submit", function(e) {
  e.preventDefault();
  console.log("Ten formularz się nie wyśle");
});

input.addEventListener("keydown", function(e) {
  e.preventDefault();
  console.log("W ten input nic nie wpiszesz");
});

link.addEventListener("click", function(e) {
  e.preventDefault();

  console.log("Ten link nigdzie nie przeniesie.");
});
```

Niektórych zdarzeń nie da się w ten sposób zatrzymać (np. load), o czym mówi nam właściwość `e.cancelable`

### Zatrzymanie propagacji

`e.stopPropagation()` - blokuje propagację zdarzenia - wędrówkę w górę (bubbling up). Jeżeli chcemy całkowicie zablokować przedostanie się danego typu eventu w górę to metodę tę musimy wywołać w pierwszej funkcji nasłuchującej.

```javascript
btn.addEventListener("click", function(e) {
  console.log("Kliknięto przycisk");
});

btn.addEventListener("click", function(e) {
  e.stopPropagation(); //powyższa funkcja już puściła event w górę
  console.log("Kliknięto przycisk");
});
```

### target & currentTarget

`e.target` - właściwość wskazuje na element, na którym dane zdarzenie się wydarzyło (np. pogrubiony element `<span>` znajdujący się wewnętrz przycisku, kliknięty przez użytkownika)

`e.currentTarget` wskazuje na element, który odpalił zdarzenie (czyli np. cały przycisk)

```javascript
const parent = document.querySelector(".parent");
parent.addEventListener("click", function(e) {
  console.log("e.target: ", e.target);
  console.log("e.currentTarget: ", e.currentTarget);
});
```

#### Ograniczanie ilości podpiętych eventów

Zamiast podpinać się bezpośrednio pod dane elementy np. `.delete` możemy podpniąć się pod rodzica i za pomocą `e.target` możemy sprawdzać jaki element wywołał dany event. Dzięki temu:

- ograniczamy liczbę eventów do jednego
- nasz event działa dla elementów, które dopiero zostaną dodane

```javascript
// Elementem nasłuchującym jest element .list, który istnieje od samego początku
list.addEventListener("click", function(e) {
  // e.target - ten który kliknął
  // e.currentTarget - ten który nasłuchuje

  if (e.target.classList.contains(".delete")) {
    const element = e.target.parentElement;
    element.parentElement.removeChild(element);
  }
});
```

## Własne eventy

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
  console.log("Jakiś tekst");
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
  console.log("Przykładowy napis");
}, 1000);
```

`clearInterval()` - przerywa wcześniej zainicjowany `setInterval`

### Technika throttle

```javascript
function throttled(delay, fn) {
  let lastCall = 0;
  return function(...args) {
    const now = new Date().getTime();
    if (now - lastCall < delay) {
      return;
    }
    lastCall = now;
    return fn(...args);
  };
}
```

```javascript
const tHandler = throttled(200, printKey);
const input = document.querySelector("input");
input.addEventListener("input", tHandler);
```

### Technika debounce

**debounce** - technika, która pozwala na "zgrupowanie" wielu występujących jeden po drugim wywołań tej samej funkcji w jedno wywołanie.

```javascript
function debounced(delay, fn) {
  let timerId;
  return function(...args) {
    if (timerId) {
      clearTimeout(timerId);
    }
    timerId = setTimeout(() => {
      fn(...args);
      timerId = null;
    }, delay);
  };
}
```

```javascript
const tHandler = debounced(200, printKey);
const input = document.querySelector("input");
input.addEventListener("input", tHandler);
```
