# JavaScript - Mechanizmy

## Silnik (Engine)

**Silnik (Engine)** - program odpowiedzialny za kompilację i wykonanie kodu JavaScript

**Kompilator (Compiler)** - odpowiedzialny za parsowanie i przygotowanie kodu dla silnika

## Hoisting

**Hoisting** - mechanizm wynoszenia zmiennych i funkcji na górę zakresu

- w języku JavaScript, funkcje oraz zmienne `var` są windowane
- windowanie odbywa się w ramach aktualnego zakresu
- `var/function` można użyć przed zadeklarowaniem
- `let/const/class` nie można użyć przed zadeklarowaniem (zasięg blokowy)

### Hoisting zmiennych

- Zmienne utworzone za pomocą `var` są hoistowane
- Zmienne utworzone za pomocą `let/const` nie są hoistowane

```javascript
console.log("x is", x); // x is undefined
var x;
console.log("x is", x); // x is undefined
x = 5;
console.log("x is", x); // x is 5
```

### Hoisting funkcji

- Funkcje utworzone za pomocą deklaracji - słowo kluczowe `function` są hoistowane
- Wyrażenia funkcyjne np. funkcje anonimowe przypisane do zminnej nie są hoistowane

```javascript
sayHello();

function sayHello() {
  console.log("Hello!");
}

// Hello!
// Funkcja jest deklarowana za pomocą function, jest hoistowana i dostępna
```

```javascript
sayHello();

var sayHello = function() {
  console.log("Hello!");
};

//TypeError: sayHello is not a function, wyrażenie funkcyjne (funkcja anonimowa) przypisana do zmiennej
```

#### Przykłady hoistingu funkcji

```javascript
sayHello();

function sayHello() {
  function hello() {
    console.log("Hello!");
  }

  hello();

  function hello() {
    console.log("Hey!");
  }
}

// Hey!
```

```javascript
sayHello();

function sayHello() {
  function hello() {
    console.log("Hello!");
  }

  hello();

  var hello = function() {
    console.log("Hey!");
  };
}

// Hello!
```

```javascript
sayHello();

var sayHello = function() {
  function hello() {
    console.log("Hello!");
  }

  hello();

  function hello() {
    console.log("Hey!");
  }
};

// TypeError: sayHello is not a function (bo undefined to nie funkcja)
```

```javascript
sayHello();

function sayHello() {
  var hello = function() {
    console.log("Hello!");
  };

  hello();

  var hello = function() {
    console.log("Hey!");
  };
}

// Hello!
```

```javascript
sayHello();

function sayHello() {
  var hello = function() {
    console.log("Hello!");
  };

  hello();

  function hello() {
    console.log("Hey!");
  }
}

// Hello!
```

## Zasięg / Zakres (Scope)

**Zasięg (Scope)** - system, odpowiedzialny za gromadzenie i zarządzanie zadeklarowanymi zmiennymi i funkcjami oraz tym, w jaki sposób są one dostępne są dla aktualnie w aktualnym miejscu w kodzie.

### Rodzaje zasięgu

- Globalny
  - Dostępny domyślnie jeszcze przed napisaniem kodu
  - Można podejrzeć jego zawartość wpisując `this` w konsoli - w przeglądarce zwróci obiekt `Window`
- Funkcyjny
- Blokowy

### Zasięg zmiennych

#### LHS a RHS

Zmienne mogą być wyszukiwane na potrzeby:

- Przypisania referencji (LHS - Left Hand Side look-up)
- Zwrócenia wartości (RHS - Right Hand Side look-up)

|     LHS      |     |   RHS    |
| :----------: | :-: | :------: |
| `const name` | `=` | `"Anna"` |

#### Typy zmiennych

- Globalne - mogą być modyfikowane z każdego innego zasięgu
- Lokalne - dostępne tylko wewnątrz danego zasięgu lokalnego np. ciała funkcji

#### Zasięg zmiennych a słowa kluczowe

Różnice w zasięgu zmiennych:

- `var` - gdy globalna, dołączana do obiektu `window`
- `let` - blokowy, nie dołączana do obiektu `window`
- `const` - blokowy, nie dołączana do obiektu `window`

```javascript
// Global scope

var greet = "Hello!"; // Scoped to the global scope

function sayHi() {
  // Local scope
  console.log("2: ", greet); // 2: undefined bo funkcja ma zmienną lokalną greet, która w tym momencie  ma przypisaną wartość undefined (hoisting, faza memory creation)
  var greet = "Ciao!";
  console.log("3: ", greet); // 3: Ciao!
}

console.log("1: ", greet); // 1: Hello! - dostęp do zmiennej globalnej poza funkcją
sayHi();
console.log("4: ", greet); // 4: Hello! - dostęp do zmiennej globalnej poza funkcją
```

## Kontekst wykonania (Execution Context)

**Kontekst wykonania (Execution Context)** - abstrakcyjny koncept środowiska w którym interpretowany i wykonywany jest kod JavaScript.

### Typy kontekstów wykonania

- **Globalny kontekst wykonania (Global Execution Context)**
  - tworzony przed wykonaniem jakiegokolwiek kodu
  - obsługuje kod nie znajdujący się wewnątrz żadnej funkcji
  - w programie JavaScript może być wyłącznie jeden taki kontekst
- **Functional Execution Context**
  - lokalny (funkcyjny) kontekst wykonania
  - za każdym razem gdy wykonywana jest funkcja, tworzony jest nowy kontekst dla tej funkcji
  - każda funkcja posiada swój własny kontekst
  - zmienne znajdujące się wewnątrz funkcji nie będą dostępne poza jej ciałem, chyba, że zwrócimy ich wartość i przypiszemy do zmiennej
- **Eval Function Execution Context**
  - kod wykonywany wewnątrz funkcji `eval` posiada swój własny kontekst

Po utworzeniu każdy kontekst umieszczany jest w **Execution Stack**

### Mechanizm tworzenia Execution Context

**1. Faza kreacji (The Memory Creation Stage)**

- Tworzony jest zasięg (Scope)
- Zachodzi hoisting
  - Deklaracje zmiennych są rozpoznawane (`var x;`)
  - Do zmiennych przypisywana jest wartość `undefined`
  - Tworzone jest miejsce w pamięci
- Tworzony jest łańcuch zasięgów (Scope Chain) dla danego elementu
- Określana jest wartość słowa kluczowego `this`
  - `this` wskazuje na wiodący obiekt nadrzędny wywołującej go funkcji
  - jeśli brak obiektu nadrzędnego, `this` wskazuje na obiekt globalny
  - jeśli brak obiektu nadrzędnego i włączony `strict mode` to `this` zwraca `undefined`

**2. Faza działania (Activation / Execution Stage)**

- Do zmiennych zostają przypisane wartości z prawej strony znaku `=`
- Funkcje zostają wykonane

### Execution Context ≠ Scope

```javascript
var globalThis = this;

function myFunc() {
  console.log("globalThis: ", globalThis);
  console.log("this inside: ", this);
  console.log(globalThis === this);
}

myFunc();

// globalThis: Window {...}
// this inside: Window {...}
// true
```

```javascript
// Określanie wartości this
var myObj = {
  myMethod: function() {
    console.log(this);
  }
};

var myFunc = myObj.myMethod;
myFunc(); // Zwraca Window ponieważ wartość this jest określana w momencie wywołania, gdy brak odniesienia do obiektu rodzica (myObj)

var myObj = {
  myMethod: function() {
    myFunc();

    function myFunc() {
      console.log(this);
    }
  }
};

myObj.myMethod(); // Zwraca Window
```

## Execution Stack

**Execution Stack** - miejsce w którym przechowywane są konteksty wykonania. Domyślnie trafia do niego Global Execution Context a następnie pozostałe konteksty są do niego dodawane i z niego usuwane według zasady **LIFO (Last In, First Out)**.

### Execution Stack - informacje

- JavaScript jest jednowątkowy - jednocześnie może być wykonywany wyłącznie jeden stos (single thread)
- Wykonywanie odbywa się synchronicznie
- Istnieje wyłącznie jeden globalny kontekst
- Może istnieć dowolna ilość Functional Execution Context / Eval execution context
- Każde wywołanie funkcji tworzy nowy kontekst (nawet gdy odwołuje się sama do siebie)

### Execution Stack i zasada LIFO

**LIFO (Last In, First Out)** - zasada według której po stworzeniu stosu kontekstów są one wykonywane i usuwane kolejno poczynając od najnowszego (Last in).

Kolejność dodawania kontekstów do Execution Stack

1. Global Context
2. First Function Context
3. Second Function Context

Kolejność usuwania kontekstów z Execution Stack

1. Second Function Context
2. First Function Context
3. Global Context

### Przykład działania silnika

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

### Zakres leksykalny

**Zakres dynamiczny** - zakres określany w momencie wykonywania kodu. Nie jest wykorzystywany w JavaScript

**Zakres leksykalny (Lexical Scope)** - zakres określany w momencie definiowania kodu, w czasie trwania fazy leksykalnej (lexical time). Jego strukturę określa informacja o tym gdzie definiowane są zmienne i bloki.

- Poszczególne zakresy mogą być w sobie wyłącznie ściśle zagnieżdżone
- JavaScript szukając identyfikatora zmiennej zaczyna od zakresu w którym się znajduje a następnie przechodzi do zewnętrznego zakresu i tak aż do momentu gdy dojdzie do zakresu globalnego lub do momentu odnalezienia szukanej wartości.

**Lexing (Tokenizing)** - pierwsza faza pracy kompilatora, polegająca na interpretowaniu ciągu tekstu kodu źródłowego na zrozumiałe dla silnika tokeny np. wyrażenie `const name = "Anna"` zostaje rozłożone na `["const", "name", "=", "Anna"]`

**Przysłonięcie (Shadow Ring)** - identyfikator znajdujący się w wewnętrznym scopie przesłania identyfikator znajdujący się w zewnętrznym scopie.

- Dodanie zmiennej `age` w scopie funkcji, gdy zmienna o takiej samej nazwie sitnieje globalnie spowoduje jej przysłonięcie
- Definiowanie zmiennej `glob` za pomocą słowa kluczowego `var` spowoduje dodanie tej zmiennej do obiektu globalnego `window` i umożliwi dostęp do wartości zmiennej poprzez `window.glob`
