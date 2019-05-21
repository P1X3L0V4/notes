# JavaScript - Understanding the Weird Parts

## Execution Context & Lexical Environements

Kod w JavaScript → Parser składni → Kompilator → Kod zrozumiały dla komputera
**Parser składni** \- program\, który sprawdza kod pod kątem poprawności składni\.
**Kompilator** \- program\, który kompiluje kod do postaci zrozumiałej dla komputera\.
**Lexical Environment** \- wystepuje w językach programowania w któych istotne jest fizyczne rozmieszczenie kodu który piszemy
**Execution Context** \- otocza w której uruchamiany jest kod\

### Name / Value Pairs and Objects

**Nazwa / wartość** \- para w której nazwa odnosi się do unikalnej wartości\.

* Nazwa może być zdefiniowana więcej niż jeden raz, ale może mieć tylko jedną wartość w danym kontekście
* Wartość może zawierać zagnieżdżone pary nazwa - wartość

Obiekt - kolekcja par nazwa - wartość (najprostsza definicja w JavaScript)

### The Global Environment and The Global Object

**Global Execution Context** - kontekst globalny, wszystko to co nie znajduje się wewnętrz poszczególnych funkcji. Kontekst globalny zawiera:

* Global Object
* Zmienna `this` - w przeglądarce domyślnie przypisana do obiektu `window`
* Outer Environment
    * Dla funkcji - link do obiektu globalnego
    * Dla obiektu globalnego - `null`
* Kod napisany przez programistę

### The Execution Context
**Hoisting** - W języku JavaScript, funkcje oraz zmienne są windowane. Windowanie (hoisting) oznacza przeniesienie deklaracji na samą górę (do globalnego zasięgu lub do zasięgu funkcji). Można dzięki temu użyć funkcji lub zmiennej przed jej zadeklarowaniem.

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
**Single Threaded** - jedna komenda na raz od strony programistycznej (od strony przeglądarki procesy mogą być bardziej złożone)\
**Synchronous** - synchronicznie, jedna linijka kodu po kolei
### Function Invocation and the Execution Stack
**Invocation** - wywołanie funkcji. W JavaScript poprzez zastosowanie nawiasów `()`\
**Execution Stack** \- miejsce w którym przechowywane są konteksty wykonania\. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.
### Functions, Context, and Variable Environments
**Variable Environment** - miejsce gdzie znajdują się zmienne i jak odnoszą się do siebie wzajemnie w pamięci\
**Scope** - zasięg zmiennej
### The Scope Chain
**Scope Chain** - łańcuch zakresów, powiązania między konkretnym zakresem np. funkcją a jego outer environement czyli np. zakresem globalnym lub inną funkcją w której funkcja jest zagnieżdżona.