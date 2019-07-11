# JavaScript - Understanding the Weird Parts

## Execution Context & Lexical Environements

Kod w JavaScript → Parser składni → Kompilator → Kod zrozumiały dla komputera
**Parser składni** \- program\, który sprawdza kod pod kątem poprawności składni
**Kompilator** \- program\, który kompiluje kod do postaci zrozumiałej dla komputera
**Lexical Environment** \- wystepuje w językach programowania w któych istotne jest fizyczne rozmieszczenie kodu który piszemy
**Execution Context** \- otoczka w której uruchamiany jest kod

### Name / Value Pairs and Objects

**Nazwa / wartość** \- para w której nazwa odnosi się do unikalnej wartości\.

* Nazwa może być zdefiniowana więcej niż jeden raz, ale może mieć tylko jedną wartość w danym kontekście
* Wartość może zawierać zagnieżdżone pary nazwa - wartość

**Obiekt** \- kolekcja par nazwa \- wartość \(najprostsza definicja w JavaScript\)

### The Global Environment and The Global Object

**Global Execution Context** \- kontekst globalny\, wszystko to co nie znajduje się wewnętrz poszczególnych funkcji\. Kontekst globalny zawiera:

* Global Object
* Zmienna `this`
* Outer Environment
    * Dla funkcji - link do obiektu globalnego (w przeglądarce `window`) lub do zewnętrznego kontekstu
    * Dla obiektu globalnego - `null`
* Kod napisany przez programistę

### The Execution Context

**Hoisting** \- W języku JavaScript\, funkcje oraz zmienne są windowane\. Windowanie \(hoisting\) oznacza przeniesienie deklaracji na samą górę \(do globalnego zasięgu lub do zasięgu funkcji\)\. Można dzięki temu odwołać się do funkcji lub zmiennej przed jej zadeklarowaniem\.

* Funkcje zdefiniowane za pomocą `function` trafiają do pamięci i można je wywołać przed zadeklarowaniem
* Zmienne wywołane przed ich zadeklarowaniem będą miały wartość `undefined` lub `uninitialized`

**Execution Context - Creation**

* Global Object
* Zmienna `this`
* `arguments` (dla funkcji) - lista wszystkich parametrów przekazanych do funkcji
* Outer Environment
* Zarezerwowanie pamięci dla zmiennych i funkcji ("Hoisting")
    * Funkcje trafiają do pamięci
    * Zmienne dostają przypisaną domyślną dla JS wartość `undefined` lub `uninitialized`

**Execution Context - Code Execution**

* Uruchamia kod linijka po linijce
    * Do zmiennych zamiast `undefined` lub `uninitialized` zostają przypisane wartości znajdujące się po prawej stronie `=`

### Single Threaded, Synchronous Execution

**Single Threaded** \- jedna komenda na raz od strony programistycznej \(od strony przeglądarki procesy mogą być bardziej złożone\)
**Synchronous** \- synchronicznie\, jedna linijka kodu po kolei

### Function Invocation and the Execution Stack

**Invocation** \- wywołanie funkcji\. W JavaScript poprzez zastosowanie nawiasów `()`
**Execution Stack** \- miejsce w którym przechowywane są konteksty wykonania\. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.

### Functions, Context, and Variable Environments

**Variable Environment** \- miejsce gdzie znajdują się zmienne i jak odnoszą się do siebie wzajemnie w pamięci
**Scope** \- zasięg zmiennej\, określa gdzie zmienna jest dostepna w kodzie \(oraz czy jest to ta sama zmienna czy jej nowa kopia\)

### The Scope Chain

**Scope Chain** \- łańcuch zakresów\, powiązania między konkretnym zakresem np\. funkcją a jego outer environement czyli np\. zakresem globalnym lub inną funkcją w której funkcja jest zagnieżdżona\. Istotne jest gdzie dana funkcja lub zmienna zostałą utworzona\.

``` javascript
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

**Asynchronous** \- więcej niż jeden w danym momencie
**Event Queue** \- lista wydarzeń\, które silnik analizuje gdy Execution Stack jest pusty \(czyli gdy Js nie zajmuje się w danym momencie żadną funkcją\, zmienną itp\.\) Wydarzenia są obsługiwane synchroniczne \(jedno po drugim\)\, jedynie przeglądarka umieszcza je w kolejce w sposób asynchroniczny\.

## Types and Operators

### Types

**Dynamic Typing** \- dynamiczne typowanie zmiennych\. Typu zmiennych nie określa się przy ich deklarowaniu\. Silnik JS określa typ zmiennych gdy kod zostaje uruchomiony\.
**Primitive Types** \- typ danych który reprezentuje pojedyńczą wartość \(nie jest to obiekt\)

* `undefined` \- reprezentuje brak przypisania wartości\. Nie powinno się jej przypisywać ręcznie
* `null` \- reprezentuje brak przypisania wartości\. Można przypisywać ją ręcznie
* `boolean` \- wartość `true/false` (prawda/fałsz)
* `number` \- floating point number czyli liczba zmiennoprzecinkowa\, w której zawsze znajują się wartości po przecinku
* `string` \- sekwencja znaków
* `symbol` \- wprowadzony w ES6

### Operators

**Operator** \- specjalny rodzaj funkcji który zestawia dwa parametry i zwraca rezultat\.
**Infix notation** \- notacja infiksowa\, sposób zapisu w którym operator będący nazwą funkcji zostaje umieszczony pomiędzy argumentami tej funkcji\. Wykorzystywana w operatorach JavaScript\.
**Prefix notation** \- operator umieszczany przed argumentami
**Postfix notation** \- operator umieszczany po argumentach \(stosowane np\. w starych kalkulatorach\)

### Operators Precedence & Associativity

**Operator Precedence** \- pierwszeństwo operatorów określa które funkcje bazujące na operatorach zostają wykonane jako pierwsze
**Operator Associativity** \- łączność określa kolejność\, w jakiej przetwarzane są operatory o takim samym pierwszeństwie:

* od lewej do prawej - lewa łączność
* od prawej do lewej - prawa łączność

[Tabela pierwszeństwa opeatorów \(MDN web docs\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

### Coercion

**Coercion** \- konwertowanie wartości danego typu na inny\. W funkcjach operatorów koercja najpierw sprowadza obydwie porównywane zmienne do jednego typu\, a następnie dokonuje porównania\.\

**Przykład 1**
`var a = 1 + '2' // zwraca string 12`
**Przykład 2**
`3 < 2 < 1 // zwraca true` ponieważ
`3 < 2 // zwraca false` więc otrzymujemy
`false < 1` w wyniku koercji `false` zostaje zamienione na `0`
`0 < 1 // zwraca true`\

**Operator identyczności** `===` \- pozwala uniknąć błędów wynikających z użycia operatora równości `==` oraz niejawnej koercji
Koercja może być przydatna jeśli zastosujemy ją w wyrażeniach warunkowych aby sprawdzić czy dana zmienna ma przypisaną wartość (zwraca `true`)
`if(x) { code }`

[Equality comparisons and sameness \(MDN web docs\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
[Equality table Github](https://dorey.github.io/JavaScript-Equality-Table/unified/)

### Default Values

**Operator lub** `||` \- gdy przekażemy mu dwie wartości\, które mogą być sprowadzone do true or false zwróci tę która będzię prawdziwa\. To sprawia\, że możemy stosować go nie tylko w działaniach matematycznych i logicznych ale także ustawić np\. domyślną wartość dla argumentu funckji \(jesli nie istnieje argument zwróć coś innego\)\.

``` javascript
function greet(name) {
    name = name || 'Your name here'; // jeśli brak wartości name zwróć 'Your name here'
    console.log('Hello ' + name);
}

greet('Tony'); // zwraca Hello Tony
greet(); // zwraca Hello 'Your name here'
```

## Objects and Functions

**Obiekt** \- kolekcja par nazwa \- wartość\, może zawierać w sobie:

* podstawowe typy danych
* obiekty
* metody (funkcje obiektu)

### Operatory

**Computed Member Access (nawiasty kwadratowe)**

``` javascript
var person = new Object();
person["firstname"] = "Tony";
person["lastname"] = "Alicea";
```

**Member Access Operator (kropka)**

``` javascript
person.address = new Object();
person.address.street = "111 Main St.";
person.address.city = "New York";
person.address.state = "NY";
```

### Object Literals

**Tworzenie obiektu**
`var person = new Object();`
`var person = {}`
**Inicjalizacja obiektu za pomocą nawiasów klamrowych**

``` javascript
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

Nowy obiekt może być przekazany bezpośrednio jako argument funkcji tak samo jak inne typy danych
**Namespace** \- pojemnik na zmienne lub funkcje\. W JavaScript możemy zasymulować namespaces przy użyciu obiektów \(Faking Namespaces\)

### JSON

**JSON** \- JavaScrip Object Notation\, podzbiór składni literału obiektu\.

* JSON jest zawsze poprawnym zapisem obiektu w JS
* Obiekt w JS nie zawsze jest poprawnym kodem JSON

JSON - różnice względem składni JS

* Nazwy piszemy w cudzysłowach
* Nie przyjmuje funkcji jako wartości

#### Konwertowanie

`JSON.stringify(objectLiteral)` \- konwertuje obiekt JS na string JSON
`var jsonValue = JSON.parse('{ "firstname": "Mary", "isAProgrammer": true }');` \- parsuje plik JSON do obiektu JS

### Funkcje to obiekty

**First Class Functions** \- wszystko co można zrobić z innymi typami danych jest także możliwe w przypadku funkcji: przypisywanie do zmiennych\, tworzenie w locie\, przekazywanie jako argument itp\.
Funkcje w JS są specjalnym rodzajem obiektu, który zawiera:

* Nazwę - opcjonalnie, funkcja może być anonimowa
* CODE - własność zawierająca kod, który jest wykonywany po wywołaniu go za pomocą `()`
* Dostęp do specjalnych metod
    * `call()`
    * `apply()`
    * `bind()`
* `prototype` \- właściwość\, która pojawia się gdy używamy funkcji jako konstruktora obiektów\, wskazuje co jest prototypem dla danego typu obiektów\. Nie jest to prototyp samej funkcji do której dostep jest możliwy przez `__proto__`

**Function Statement** \- deklaracja funkcji
Po zadeklarowaniu funkcja trafia do pamięci, ale nic nie zostaje zwrócone

``` javascript
function greet() {
    console.log('hi');
}
```

**Function Expression** \- wyrażenie funkcyjne
Przypisanie obiektu funkcji do zmiennej za pomocą `=` powoduje zwrócenie tego obiektu więc mamy do czynienia z Function Expression

``` javascript
var anonymousGreet = function() {
    console.log('hi');
}
```

### By Value vs By Reference

By Value - odwołanie poprzez kopiowanie wartości. W JS dotyczy typów prostych (primitives), takich jak liczby, stringi itp.

``` javascript
a = 5
b = a
b = 5 // do zmiennej b przypisana została kopia wartości 5
```

By Refrence - odwołanie poprzez przypisanie adresu w pamięci. W JS dotyczy obiektów oraz funkcji

``` javascript
a = {}
a = b
b = {} // zmienna b zawiera odniesienie do tego samego obiektu do którego odnosi się a
```

**Mutate** \- zmienić coś
**Immutable** \- oznacza\, że danego elementu nie można zmodyfikować

### Objects, Functions, and 'this'

Słowo kluczowe `this` wskazuje na:

* Funkcje → obiekt globalny
* Metoda obiektu → obiekt w któym ta metoda się znajduje

W przypadku metod i funkcji wewnątrz obiektów w JavaScript zachodzi problem. Słowo kluczowe `this` w metodach obiektu wskazuje na obiekt, w którym ta metoda się znajduje, ale funkcja przypisana do zmiennej wewnątrz metody odwołuje się do obiektu globalnego.

``` javascript
var c = {
    name: 'The c object',
    log: function() {

        this.name = 'Updated c object'; // zmienia name obiektu c
        console.log(this);

        var setname = function(newname) {
            this.name = newname; // zmienia/dodaje name do obiektu globalnego
        }
        setname('Updated again! The c object');
        console.log(this);
    }
}
```

Aby zapobieg problemowi z odróżnieniem na co wskazuje słowo kluczowe this można zainicjować wewnątrz metody zmienną np. `self` lub `that` i przypisać do niej `this` (czyli obiekt) przed wykonaniem dalszych operacji.

``` javascript
var c = {
    name: 'The c object',
    log: function() {
        var self = this;

        self.name = 'Updated c object';
        console.log(self);

        var setname = function(newname) {
            self.name = newname;
        }
        setname('Updated again! The c object');
        console.log(self);
    }
}
```

### Arrays - Collections of Anything

**Array** \- tablica\, może przechowywać dowolne kolekcje danych

``` javascript
var arr = [
    1,
    false,
    {
        name: 'Tony',
        address: '111 Main St.'
    },
    function(name) {
        var greeting = 'Hello ';
        console.log(greeting + name);
    },
    "hello"
];
```

### Arguments

**Arguments** \- tablica ze wszystkimi parametrami przekazanymi do funkcji
**Spread parameter** \- parametr rozpakowania w formie `...other` pozwala dodać ciąg o lub więcej argumentów do funkcji

``` javascript
function greet(firstname, lastname, language, ...other) { // other to spread parameter

    if (arguments.length === 0) {
        console.log('Missing parameters!');
        console.log('-------------');
        return;
    }
}
```

### Function Overloading

**Function Overloading** \- koncept w językach programowania \(np\. Java\)\, który polega an tym\, że możemy zadeklarować funkcje o tej samej nazwie ale różnej ilości parametrów\. W JavaScript brak tej funkcjonalności ponieważ funkcje są obiektami\.
**Rozwiązanie zastępcze**

``` javascript
function greet(firstname, lastname, language) {

    language = language || 'en';

    if (language === 'en') {
        console.log('Hello ' + firstname + ' ' + lastname);
    }

    if (language === 'es') {
        console.log('Hola ' + firstname + ' ' + lastname);
    }

}

function greetEnglish(firstname, lastname) {
    greet(firstname, lastname, 'en');
}

function greetSpanish(firstname, lastname) {
    greet(firstname, lastname, 'es');
}
```

**Automatic Semicolon Insertion** \- należy samodzielnie wstawiać średniki na końcu wyrażeń i uważać na znak powrotu karetki \(nowa linia\) aby uniknąć automatycznego uzupełniania przez silnik JS/
**Whitespace** \- niewidoczne znaki\, które tworzą wizualną przestrzeń w kodzie

* spacja
* tabulator
* powrót karetki

### Immediately Invoked Functions Expressions (IIFEs)

Immediately Invoked Functions Expressions (IIFEs) - wyrażenie funkcyjne które są od razu wywoływane
**Sposób 1** \- wyrażenie funkcyjne z `()` na końcu

``` javascript
var greeting = function(name) {
    return 'Hello ' + name;
}('John');

console.log(greeting);
```

**Sposób 2** \- funkcja anonimowa w nawiasach `()`

``` javascript
var firstname = 'John';

(function(name) {
    var greeting = 'Inside IIFE: Hello';
    console.log(greeting + ' ' + name);
}(firstname)); // wywołanie może znaleźć się także poza nawiasem (function(){})()
```

IIFEs są użyteczne ponieważ dzięki temu możemy uniknąć konfliktów między różnymi bibliotekami JSa. Wszystko co zostaje umieszczone wewnątrz IIFE trafia do kontekstu tej konkretnej funkcji i nie ociera się o kontekst globalny.

### Closures

``` javascript
function greet(whattosay) {

   return function(name) {
       console.log(whattosay + ' ' + name);
   }

}

var sayHi = greet('Hi');
sayHi('Tony'); // Ta funkcja nadal ma dostęp do whattosay
```

Mimo, że funkcja `greet` zakończyłą swoje działanie i jej kontekst egzekucyjny został usunięty ze stosu, wszystkie funkcje stworzone wewnątrz niej kiedy zostaną wywołane będa nadal posiadały referencję do pamięci funkcji `greet`.
**Przykład 1**
Funkcja zawsze będzie miała dostęp do swojego wewnętrznego kontekstu i do kontekstu rodzica w aktualnym momencie czasu a nie w konkteście, w którym rodzic został utworzony.

``` javascript
function buildFunctions() {
    var arr = [];
    for (var i = 0; i < 3; i++) {
        arr.push(
            function() {
                console.log(i);
            }
        )
    }
    return arr;
}

var fs = buildFunctions();

fs[0](); // zwraca 3
fs[1](); // zwraca 3
fs[2](); // zwraca 3
```

Wszystkie 3 wywołania `fs` zwracają 3 bo po zakończeniu iteracji w pętli `for` funkcji `buildFunctions` pamięci zostaje zapisane `i = 3`. Do tej wartości w pamięci ma dostęp każda funkcja `fs` podczas wywołania.

``` javascript
function buildFunctions2() {
    var arr = [];
    for (var i = 0; i < 3; i++) {
        arr.push(
            (function(j) {
                return function() {
                    console.log(j);
                }
            }(i))
        )
    }
    return arr;
}

var fs2 = buildFunctions2();

fs2[0](); // zwraca 1
fs2[1](); // zwraca 2
fs2[2](); // zwraca 3
```

Zastosowanie IIFE pozwala przekazać wartość iteratora `i` jako parametr funkcji `j`

### Function Factories

**Factory Functions** \- każda funkcja\, która nie jest klasa lub konstruktorem a zwraca \(prawdopodobnie nowy\) obiekt\.
Wykorzystanie domknięć JS w tworzeniu fabryk (factory functions)

``` javascript
function makeGreeting(language) {

    return function(firstname, lastname) {
        if (language === 'en') {
            console.log('Hello ' + firstname + ' ' + lastname);
        }
        if (language === 'es') {
            console.log('Hola ' + firstname + ' ' + lastname);
        }
    }
}

var greetEnglish = makeGreeting('en');
var greetSpanish = makeGreeting('es');

greetEnglish('John', 'Doe');
greetSpanish('John', 'Doe');
```

Dwa odrębne wywoałania funkcji zewnętrznej `makeGreeting('en')` oraz `makeGreeting('es')` tworzą dwa konteksty w których istnieją dwie różne wartości w pamięci: `language = 'en'` oraz `language = 'es'`. We wcześniejszym przykładzie z iterowaniem funkcja zewnętrzna wywoływana była tylko raz `var fs = buildFunctions()` i w związku z tym w pamięci istniało tylko jedno odwołanie `i = 3`.

### Closures and Callbacks

**Przykład 1**

``` javascript
function sayHiLater() {
    var greeting = 'Hi!';
    setTimeout(function() {
        console.log(greeting);
    }, 3000);
}

sayHiLater();
```

**Przykład 2**

``` javascript
function tellMeWhenDone(callback) {
    var a = 1000; // some work
    var b = 2000; // some work
    callback(); // the 'callback', it runs the function I give it!
}

tellMeWhenDone(function() {
    console.log('I am done!');
});

tellMeWhenDone(function() {
    console.log('All done...');
});
```

**Callback Function** \- funkcja przekazywana jako parametr innej funkcji\, uruchamiana gdy inna funkcja dobiegnie końca\.
**Przykład 3**

``` javascript
// jQuery uses function expressions and first-class functions
$("button").click(function() {
});
```

### call(), apply(), & bind()

``` javascript
var person = {
    firstname: 'John',
    lastname: 'Doe',
    getFullName: function() {
        var fullname = this.firstname + ' ' + this.lastname;
        return fullname;
    }
}

var logName = function(lang1, lang2) {
    console.log('Logged: ' + this.getFullName());
    console.log('Arguments: ' + lang1 + ' ' + lang2);
    console.log('-----------');
}
```

#### bind()

`bind()` \- tworzy kopię funkcji i określa na co ma wskazywać `this` podczas jej wywołania

``` javascript
var logPersonName = logName.bind(person);
// tworzy kopię logName w której this odnosi się do obiektu person
```

#### call()

`call()` \- wywołuje funkcję i określa na co ma wskazywać `this` podczas jej wywołania, argumenty w formie listy

``` javascript
logName.call(person, 'en', 'es');
```

#### apply()

`apply()` \- wywołuje funkcję i określa na co ma wskazywać `this` podczas jej wywołania, argumenty w formie tablicy

``` javascript
logName.apply(person, ['en', 'es']);
```

#### Function Borrowing

Pozwala pożyczać funkcje (metody) innych obiektów

``` javascript
var person2 = {
    firstname: 'Jane',
    lastname: 'Doe'
}

console.log(person.getFullName.apply(person2)); // Pożyczamy metodę getFullName z obiektu person
```

#### Function Currying

**Function Currying** \- tworzenie kopii funkcji\, ale z domyślnymi parametrami \(argumentami\)

``` javascript
function multiply(a, b) {
    return a*b;
}

var multipleByTwo = multiply.bind(this, 2); // Ustawia 2 jako pierwszy argument
console.log(multipleByTwo(4)); // Wywołuje multipleByTwo z 4 jako drugim arg

var multipleByThree = multiply.bind(this, 3); // Ustawia 3 jako pierwszy argument
console.log(multipleByThree(4)); // Wywołuje multipleByTwo z 4 jako drugim arg
```

### Functional Programming

**Przykład 1**

``` javascript
function mapForEach(arr, fn) {

    var newArr = [];
    for (var i=0; i < arr.length; i++) {
        newArr.push(
            fn(arr[i])
        )
    };

    return newArr;
}

var arr = mapForEach(arr1, function(item) {
   return item * 2;
});
console.log(arr);
```

Zastosowanie `bind()` do ustawienia domyślnego parametru dla `checkPastLimit` w przypadku przekazywania funkcji do `mapForEach`, które posiada tylko jeden argument `fn(arr[i])`

``` javascript
var checkPastLimit = function(limiter, item) {
    return item > limiter;
}
var arr2 = mapForEach(arr1, checkPastLimit.bind(this, 1)); // limiter ustawiony domyślnie na 1
console.log(arr2);
```

Uproszczona wersja funkcji `checkPastLimit`

``` javascript
var checkPastLimitSimplified = function(limiter) {
    return function(limiter, item) {
        return item > limiter;
    }.bind(this, limiter);
};

var arr3 = mapForEach(arr1, checkPastLimitSimplified(1));
console.log(arr3);
```

[Underscore.js](https://underscorejs.org/) \- biblioteka JS wykorzystująca możliwości functional programming

``` javascript
// Underscore.JS - Przykłady
var arr6 = _.map(arr1, function(item) { return item * 3 });
console.log(arr6);

var arr7 = _.filter([2,3,4,5,6,7], function(item) { return item % 2 === 0; });
console.log(arr7);
```

## Object-Oriented Javascript and Prototypal Inheritance

### Klasyczne vs prototypowe dziedziczenie

**Dziedziczenie** \- jeden obiekt otrzymuje dostęp do właściwości i metod drugiego obiektu
**Klasyczne dziedziczenie** \- w językach takich jak Java\, C\#

* Rozwlekła składnia
* Wykorzystuje słowa kluczowe: friend, protected, private, interface

**Prototypowe dziedziczenie** \- w JavaScript

* Prosta składnia
* Elastyczność

### Understanding the Prototype

**Prototyp** \- obiekt `proto {}`, do którego powiązany jest każdy obiekt (w tym funkcje).

* Obiekt zawiera swoje właściwości i metody a także dziedziczy właściwości i metody prototypu.
* Dwa różne obiekty mogą mieć ten sam prototyp

**Prototype Chain** \- łańcuch powiązań między prototypami obiektów\. Sprawia\, że możemy odwołać się do własności prototypu poprzez `obj.prop2` zamiast `obj.proto.prop2`
\*\*Przykład \*\*

``` javascript
var person = {
    firstname: 'Default',
    lastname: 'Default',
    getFullName: function() {
        return this.firstname + ' ' + this.lastname;
    }
}

var john = {
    firstname: 'John',
    lastname: 'Doe'
}

// Nie należy zmieniać ręcznie prototypu! Przykład poglądowy!
john.__proto__ = person;
console.log(john.getFullName());
console.log(john.firstname);
```

### Reflection and Extend

**Reflection** \- obiekt może spojrzeć na siebie wyświetlając listę i zmieniając swoje własne właściwości i metody `obj.hasOwnProperty(prop)`
**Extend** \- możliwe jest rozszerzanie właściwości i mnetod obiektu

``` javascript
var john = {
    firstname: 'John',
    lastname: 'Doe'
}

for (var prop in john) {
    if (john.hasOwnProperty(prop)) { // Sprawdza czy obiekt posiada właściwość prop
        console.log(prop + ': ' + john[prop]);
    }
}

var jane = {
    address: '111 Main St.',
    getFormalFullName: function() {
        return this.lastname + ', ' + this.firstname;
    }
}

var jim = {
    getFirstName: function() {
        return firstname;
    }
}

_.extend(john, jane, jim); // Przykład z  biblioteki Uderscore.js

console.log(john);
```

## Building Objects

### Konstruktor funkcji i operator new

**Konstruktor funkcji** \- funkcja używana do konstrukowania obiektów\. Definiuje typ obiektu poprzez określenie nazwy\, właściwości i metod\. Zwyczajowo nazwy konstruktora piszemy wielką literą\.

* Słowo kluczowe `this` wskazuje na nowy utworzony pusty obiekt
* Funkcja automatycznie zwraca nowy pusty obiekt
* Zastosowanie konstruktora automatycznie wskazuje prototyp dla tworzonego obiektu

``` javascript
function Person(firstname, lastname) { // Konstruktor
    this.firstname = firstname;
    this.lastname = lastname;
}

var john = new Person('John', 'Doe'); // Tworzy nowy pusty obiekt typu Person
console.log(john);
```

### Konstruktor funkcji i .prototype

`prototype` \- właściwość\, która pojawia się gdy używamy funkcji jako konstruktora obiektów\, wskazuje co jest prototypem dla danego typu obiektów\. Nie jest to prototyp samej funkcji do której dostep jest możliwy przez `__proto__`

``` javascript
function Person(firstname, lastname) {
    this.firstname = firstname;
    this.lastname = lastname;
}

Person.prototype.getFullName = function() {
    return this.firstname + ' ' + this.lastname;
}
```

Ze względu na wydajność kodu kolejne metody lepiej jest dodawać do `prototype` konstruktora - pozwala to zaoszczędzić miejsce w pamięci ponieważ dana funkcja (metoda) pojawia się w pamięci tylko raz (przypięta do `prototype`) i nie jest powielana przy każdym obiekcie, jak miałoby to miejsce w przypadku dodania jej bezpośrednio w konstuktorze (wtedy każdy obiekt zawierałby kopię tej metody).

#### prototype a **proto**

`prototype` \- właściwość funkcji konstuktora\, wskazuje jaki konstruktor jest prototypem dla wszystkich instancji obiektów utworzonych za pomocą tego konstuktora np `Person {}`
`__proto__` \- właściwość obecna dla każdej instancji obiektu z osobna\, wskazuje co jest prototypem \(rodzicem\) dla tego obiektu np `Object {}`

### Wbudowane funkcje

Istnieje różnica między wykorzystaniem wbudowanych funkcji z użyciem słowa kluczowego `new` i bez niego.

* `new Number()` \- tworzy obiekt z numerem vs `Number()` \- wywoła funkcję
* `new String()` \- tworzy obiekt ze stringiem vs `String()` \- wywoła funkcję
* `new Date()` \- tworzy obiekt z datą vs `Date()` \- wywoła funkcję

Dodawanie metod do prototypów wbudowanych funkcji. Należy pamiętać aby nie nadpisać istniejących metod.

``` javascript
String.prototype.isLengthGreaterThan = function(limit) {
    return this.length > limit;
}

console.log("John".isLengthGreaterThan(3));

Number.prototype.isPositive = function() {
    return this > 0;
}
```

[Moment.js](https://momentjs.com/)\- biblioteka do manipulowania datami w JavaScript

### Tablice i pętla for..in

Używanie pętli `for...in` dla tablic obarczone jest ryzykiem, że poza wartościami w tablicy dodane zostaną dodatkowe własności dodane do prototypu. Dlatego dla tablic zamiast pętli `for...in` należy używać pętli `for`.

``` javascript
Array.prototype.myCustomFeature = 'Cool!';

var arr = ['John', 'Jane', 'Jim']

for (var prop in arr) {
    console.log(prop +  ': ' + arr[prop]);
}

/* Pętla for in zwraca
0: John
1: Jane
2: Jim
myCustomFeature: Cool! // niechciana wartość dodana z prototypu
*/
```

### Object.create & Pure Prototypal Inheritance

Tworzenie obiektu przy pomocy `Object.create()`

``` javascript
var person = {
    firstname: 'Default',
    lastname: 'Default',
    greet: function() {
        return 'Hi ' + this.firstname;
    }
}

var john = Object.create(person); // Tworzy pusty obiekt którego prototypem jest person
john.firstname = 'John'; // Dodaje 'John' do obiektu john nadpisując wartość z prototypu
john.lastname = 'Doe'; // Dodaje 'Doe' do obiektu john nadpisując wartość z prototypu
```

**Polyfill** \- fragment kodu\, który dodaje obsługę funkcjonalności która może nie być obsługiwana przez silnik \(np przeglądarki\)\. Polyfill dla `Object.create()`:

``` javascript
// Polyfill
if (!Object.create) {
  Object.create = function (o) {
    if (arguments.length > 1) {
      throw new Error('Object.create implementation'
      + ' only accepts the first parameter.');
    }
    function F() {}
    F.prototype = o;
    return new F();
  };
}
```

### ES6 & klasy

ES6 wprowadził klasy do JavaScript, które podobnie jak wszystkie elementy poza typami prostymi są obiektami. Tworzenie klasy:

``` javascript
class Person {
    constructor(firstname, lastname) {
        this.firstmane = firstname'
        this.lastname = lastname;
    }

    greet() {
        return 'Hi ' + firstname;
    }
}
```

Rozszerzanie prototypu obiektu przy pomocy klasy

``` javascript
class InformalPerson extends Person {
    constructor(firstname, lastname) {
        super(firstname, lastname); // super() wywołuje konstruktor rodzica
    }

    greet() {
        return 'Yo ' + firstname;
    }
}
```

## Odds and Ends

### Typy danych w JavaScript

``` javascript
// Number
var a = 3;
console.log(typeof a);

// String
var b = "Hello";
console.log(typeof b);

// Object
var c = {};
console.log(typeof c);

// Array
var d = [];
console.log(typeof d); // weird!
console.log(Object.prototype.toString.call(d)); // better!

// Object constructor
function Person(name) {
this.name = name;
}

var e = new Person('Jane');
console.log(typeof e);
console.log(e instanceof Person); // Sprawdza czy obiekt e jest instancją konstruktora Person

console.log(typeof undefined); // zwraca undefined
console.log(typeof null); // zwraca object (wiele bibliotek bazuje na tej dziwnej właściwości)

var z = function() { };
console.log(typeof z); // zwraca function
```

### Strict Mode

Kod umieszczamy na górze pliku lub na górze konkretnej funkcji

``` javascript
"use strict";

function logNewPerson() {
    "use strict";
    var person2;
    persom2 = {};
    console.log(persom2);
}
```

[Strict mode MDN web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

## jQuery

\*\*Method chaining \- \*\*<span class="highlight" style="background-color:inherit"><span class="colour" style="color:var(--vscode-editor-foreground)">wywoływanie kolejnych metod jedna po drugiej w taki sposób, że wszystkie odwołują się do obiektu rodzica.</span></span>

``` javascript
obj.method1().method2() // W obu metodach this wskazuje na obj
```

Jednym ze sposbów na to aby metoda nadawała się do chainowania jest zwrócenie w niej na końcu `this`

## Building Framework

### Zasady budowy własnego frameworka

1. Cały framework umieszczamy w IFEE (Immediately Invoked Functions Expression)
2. Metody umieszczamy na prototypie a nie w konstruktorze obiektu
3. Metody łańcuchowe tworzymy dodając `return this` na końcu

### Greetr.js

``` javascript
(function(global, $) {

// 'new' an object
var Greetr = function(firstName, lastName, language) {
return new Greetr.init(firstName, lastName, language);
}

// hidden within the scope of the IIFE and never directly accessible
var supportedLangs = ['en', 'es'];

// informal greetings
var greetings = {
en: 'Hello',
es: 'Hola'
};

// formal greetings
var formalGreetings = {
en: 'Greetings',
es: 'Saludos'
};

// logger messages
var logMessages = {
en: 'Logged in',
es: 'Inició sesión'
};

// prototype holds methods (to save memory space)
Greetr.prototype = {

// 'this' refers to the calling object at execution time
fullName: function() {
return this.firstName + ' ' + this.lastName;
},

validate: function() {
// check that is a valid language
// references the externally inaccessible 'supportedLangs' within the closure
if (supportedLangs.indexOf(this.language) === -1) {
throw "Invalid language";
}
},

// retrieve messages from object by referring to properties using [] syntax
greeting: function() {
return greetings[this.language] + ' ' + this.firstName + '!';
},

formalGreeting: function() {
return formalGreetings[this.language] + ', ' + this.fullName();
},

// chainable methods return their own containing object
greet: function(formal) {
var msg;

// if undefined or null it will be coerced to 'false'
if (formal) {
msg = this.formalGreeting();
}
else {
msg = this.greeting();
}

if (console) {
console.log(msg);
}

// 'this' refers to the calling object at execution time
// makes the method chainable
return this;
},

log: function() {
if (console) {
console.log(logMessages[this.language] + ': ' + this.fullName());
}

// make chainable
return this;
},

setLang: function(lang) {

// set the language
this.language = lang;

// validate
this.validate();

// make chainable
return this;
},

HTMLGreeting: function(selector, formal) {
if (!$) {
throw 'jQuery not loaded';
}

if (!selector) {
throw 'Missing jQuery selector';
}

// determine the message
var msg;
if (formal) {
msg = this.formalGreeting();
}
else {
msg = this.greeting();
}

// inject the message in the chosen place in the DOM
$(selector).html(msg);

// make chainable
return this;
}

};

// the actual object is created here, allowing us to 'new' an object without calling 'new'
Greetr.init = function(firstName, lastName, language) {

var self = this;
self.firstName = firstName || '';
self.lastName = lastName || '';
self.language = language || 'en';

self.validate();

}

// trick borrowed from jQuery so we don't have to use the 'new' keyword
Greetr.init.prototype = Greetr.prototype;

// attach our Greetr to the global object, and provide a shorthand '$G' for ease our poor fingers
global.Greetr = global.G$ = Greetr;

}(window, jQuery));
```

## TypeScript, ES6, and Transpiled Languages

**Transpilacja **\- konwertowanie składni jednego języka programowania na inny