# JavaScript - Understanding the Weird Parts

## Execution Context & Lexical Environements

Kod w JavaScript → Parser składni → Kompilator → Kod zrozumiały dla komputera\
**Parser składni** \- program\, który sprawdza kod pod kątem poprawności składni\
**Kompilator** \- program\, który kompiluje kod do postaci zrozumiałej dla komputera\
**Lexical Environment** \- wystepuje w językach programowania w któych istotne jest fizyczne rozmieszczenie kodu który piszemy\
**Execution Context** \- otoczka w której uruchamiany jest kod

### Name / Value Pairs and Objects

**Nazwa / wartość** \- para w której nazwa odnosi się do unikalnej wartości\.

* Nazwa może być zdefiniowana więcej niż jeden raz, ale może mieć tylko jedną wartość w danym kontekście
* Wartość może zawierać zagnieżdżone pary nazwa - wartość

**Obiekt** \- kolekcja par nazwa \- wartość \(najprostsza definicja w JavaScript\)

### The Global Environment and The Global Object

**Global Execution Context** \- kontekst globalny\, wszystko to co nie znajduje się wewnętrz poszczególnych funkcji\. Kontekst globalny zawiera:

* Global Object
* Zmienna `this` - w przeglądarce domyślnie przypisana do obiektu `window`
* Outer Environment
    * Dla funkcji - link do obiektu globalnego
    * Dla obiektu globalnego - `null`
* Kod napisany przez programistę

### The Execution Context

**Hoisting** \- W języku JavaScript\, funkcje oraz zmienne są windowane\. Windowanie \(hoisting\) oznacza przeniesienie deklaracji na samą górę \(do globalnego zasięgu lub do zasięgu funkcji\)\. Można dzięki temu użyć funkcji lub zmiennej przed jej zadeklarowaniem\.

* Funkcje trafiają do pamięci w całości więc można je normalnie wywołać
* Zmienne zadeklarowane po ich wywołaniu będą miały wartość `undefined` lub `uninitialized`

**Execution Context - Creation**

* Global Object
* Zmienna `this`
* Outer Environment
* Zarezerwowanie pamięci dla zmiennych i funkcji ("Hoisting")

**Execution Context - Code Execution**

* Uruchamia kod linijka po linijce

### Single Threaded, Synchronous Execution

**Single Threaded** \- jedna komenda na raz od strony programistycznej \(od strony przeglądarki procesy mogą być bardziej złożone\)
**Synchronous** \- synchronicznie\, jedna linijka kodu po kolei

### Function Invocation and the Execution Stack

**Invocation** \- wywołanie funkcji\. W JavaScript poprzez zastosowanie nawiasów `()`\
**Execution Stack** \- miejsce w którym przechowywane są konteksty wykonania\. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.

### Functions, Context, and Variable Environments

**Variable Environment** \- miejsce gdzie znajdują się zmienne i jak odnoszą się do siebie wzajemnie w pamięci\
**Scope** \- zasięg zmiennej\, określa gdzie zmienna jest dostepna w kodzie \(oraz czy jest to ta sama zmienna czy jej nowa kopia\)

### The Scope Chain

**Scope Chain** \- łańcuch zakresów\, powiązania między konkretnym zakresem np\. funkcją a jego outer environement czyli np\. zakresem globalnym lub inną funkcją w której funkcja jest zagnieżdżona\. Istotne jest gdzie dana funkcja lub zmienna zostałą utworzona\.

```
function a() {
    function b() {
    }
}
var x = 0;
```

* Outer reference dla `function a` jest kontekst globalny
* Outer reference dla `function b` jest `function a`

ES6 (ECMAScript 6) wprowadziła nowy sposób deklarowania zmiennych za pomocą `let`

* Nie mogą być użyte dopóki nie zostaną wywołane
* Dostępne tylko w bloku, w którym zostały zadeklarowane

### Asynchronous Callbacks

**Asynchronous** \- więcej niż jeden w danym momencie\
**Event Queue** \- lista wydarzeń\, które silnik analizuje gdy Execution Stack jest pusty \(czyli gdy Js nie zajmuje się w danym momencie żadną funkcją\, zmienną itp\.\) Wydarzenia są obsługiwane synchroniczne \(jedno po drugim\)\, jedynie przeglądarka umieszcza je w kolejce w sposób asynchroniczny\.

## Types and Operators

### Types

**Dynamic Typing** \- dynamiczne typowanie zmiennych\. Typu zmiennych nie określa się przy ich deklarowaniu\. Silnik JS określa typ zmiennych gdy kod zostaje uruchomiony\.\
**Primitive Types** \- typ danych który reprezentuje pojedyńczą wartość \(nie jest to obiekt\)

* `undefined` \- reprezentuje brak przypisania wartości\. Nie powinno się jej przypisywać ręcznie
* `null` \- reprezentuje brak przypisania wartości\. Można przypisywać ją ręcznie
* `boolean` \- wartość `true/false` (prawda/fałsz)
* `number` \- floating point number czyli liczba zmiennoprzecinkowa\, w której zawsze znajują się wartości po przecinku
* `string` \- sekwencja znaków
* `symbol` \- wprowadzony w ES6

### Operators

**Operator** \- specjalny rodzaj funkcji który zestawia dwa parametry i zwraca rezultat\.\
**Infix notation** \- notacja infiksowa\, sposób zapisu w którym operator będący nazwą funkcji zostaje umieszczony pomiędzy argumentami tej funkcji\. Wykorzystywana w operatorach JavaScript\.\
**Prefix notation** \- operator umieszczany przed argumentami\
**Postfix notation** \- operator umieszczany po argumentach \(stosowane np\. w starych kalkulatorach\)

#### Operators Precedence & Associativity

**Operator Precedence** \- pierwszeństwo operatorów określa które funkcje bazujące na operatorach zostają wykonane jako pierwsze
**Operator Associativity** \- łączność określa kolejność\, w jakiej przetwarzane są operatory o takim samym pierwszeństwie:

* od lewej do prawej - lewa łączność
* od prawej do lewej - prawa łączność

[Tabela pierwszeństwa opeatorów \(MDN web docs\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

#### Coercion

**Coercion** \- konwertowanie wartości danego typu na inny\. W funkcjach operatorów koercja najpierw sprowadza obydwie porównywane zmienne do jednego typu\, a następnie dokonuje porównania\.\

**Przykład 1**\
`var a = 1 + '2' // zwraca string 12`\
**Przykład 2**\
`3 < 2 < 1 // zwraca true` ponieważ\
`3 < 2 // zwraca false` więc otrzymujemy\
`false < 1` w wyniku koercji `false` zostaje zamienione na `0`\
`0 < 1 // zwraca true`\

**Operator identyczności** `===` \- pozwala uniknąć błędów wynikających z użycia operatora równości `==` oraz niejawnej koercji
Koercja może być przydatna jeśli zastosujemy ją w wyrażeniach warunkowych aby sprawdzić czy dana zmienna ma przypisaną wartość (zwraca `true`)\
`if(x) { code }`

[Equality comparisons and sameness \(MDN web docs\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)\
[Equality table Github](https://dorey.github.io/JavaScript-Equality-Table/unified/)

### Default Values

**Operator lub** `||` \- gdy przekażemy mu dwie wartości\, które mogą być sprowadzone do true or false zwróci tę która będzię prawdziwa\. To sprawia\, że możemy stosować go nie tylko w działaniach matematycznych i logicznych ale także ustawić np\. domyślną wartość dla argumentu funckji \(jesli nie istnieje argument zwróć coś innego\)\.
```
function greet(name) {
    name = name || '<your name="" here="">'; // jeśli brak wartości name zwróć '<your name="" here="">'
    console.log('Hello ' + name);
}

greet('Tony'); // zwraca Hello Tony
greet(); // zwraca Hello <your name="" here="">';
```

## Objects and Functions

**Obiekt** \- kolekcja par nazwa \- wartość\, może zawierać w sobie:

* podstawowe typy danych
* obiekty
* metody (funkcje obiektu)

### Operatory
**Computed Member Access (nawiasty kwadratowe)**
```
var person = new Object();
person["firstname"] = "Tony";
person["lastname"] = "Alicea";
```
**Member Access Operator (kropka)**
```
person.address = new Object();
person.address.street = "111 Main St.";
person.address.city = "New York";
person.address.state = "NY";
```
### Object Literals
**Tworzenie obiektu**\
`var person = new Object();`\
`var person = {}`\
**Inicjalizacja obiektu za pomocą nawiasów klamrowych**
```
var Tony = { 
    firstname: 'Tony', 
    lastname: 'Alicea',
    address: {
        street: '111 Main St.',
        city: 'New York',
        state: 'NY'
    }
};
```
Nowy obiekt może być przekazany bezpośrednio jako argument funkcji tak samo jak inne typy danych\
**Namespace** - pojemnik na zmienne lub funkcje. W JavaScript możemy zasymulować namespaces przy użyciu obiektów (Faking Namespaces)

### JSON
**JSON** - JavaScrip Object Notation, podzbiór składni literału obiektu.

* JSON jest zawsze poprawnym zapisem obiektu w JS
* Obiekt w JS nie zawsze jest poprawnym kodem JSON

JSON - różnice względem składni JS

* Nazwy piszemy w cudzysłowach
* Nie przyjmuje funkcji jako wartości

#### Konwertowanie
`JSON.stringify(objectLiteral)` - konwertuje obiekt JS na string JSON\
`var jsonValue = JSON.parse('{ "firstname": "Mary", "isAProgrammer": true }');` - parsuje plik JSON do obiektu JS

### Funkcje to obiekty
**First Class Functions** - wszystko co można zrobić z innymi typami danych jest także możliwe w przypadku funkcji: przypisywanie do zmiennych, tworzenie w locie, przekazywanie jako argument itp.\
Funkcje w JS są specjalnym rodzajem obiektu, który zawiera:

* nazwę - opcjonalnie, funkcja może być anonimowa
* CODE - własność zawierająca kod, który jest wykonywany po odwołaniu się do niego za pomocą `()`

Function Statements and Function Expressions