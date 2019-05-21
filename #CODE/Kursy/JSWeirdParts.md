# JavaScript - Understanding the Weird Parts

### Execution Context, Lexical Environements, Syntax Parsers

Kod w JavaScript → Parser składni → Kompilator → Kod zrozumiały dla komputera
**Parser składni** \- program\, który sprawdza kod pod kątem poprawności składni\.
**Kompilator** \- program\, który kompiluje kod do postaci zrozumiałej dla komputera\.
**Lexical Environment** \- wystepuje w językach programowania w któych istotne jest fizyczne rozmieszczenie kodu który piszemy
**Execution Context** \- A wrapper to help manage the code that is running\

### Name / Value Pairs and Objects

**Nazwa / wartość** \- para w której nazwa odnosi się do unikalnej wartości\.

* Nazwa może być zdefiniowana więcej niż jeden raz, ale może mieć tylko jedną wartość w danym kontekście
* Wartość może zawierać zagnieżdżone pary nazwa - wartość

Obiekt - kolekcja par nazwa - wartość (najprostsza definicja w JavaScript)

## The Global Environment and The Global Object

Global Execution Context

* Global Object
* `this` - domyślnie obiekt `window`