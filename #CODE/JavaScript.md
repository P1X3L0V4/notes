# JavaScript
### Kontekst wykonania (Execution Context)
**Kontekst wykonania (Execution Context)** - abstrakcyjny koncept środowiska w którym interpretowany i wykonywany jest kod JavaScript. Za każdym razem gdy uruchamiamy kod JS, dzieje się to w Execution Context.
**Typy kontekstów wykonania**

* **Global Execution Context** - globalny kontekst wykonania to domyślny kontekst wykonywania, który obsługuje kod nie znajdujący się wewnątrz żadnej funkcji. W programie JavaScript może byc wyłącznie jeden taki kontekst.
* **Functional Execution Context** - lokalny (funkcyjny) kontekst wykonania; za każdym razem gdy wykonywana jest funkcja, tworzony jest nowy kontekst dla tej funkcji. Każda funkcja posiada swój własny kontekst.
* **Eval Function Execution Context** - kod wykonywany wewnętrz funkcji `eval` posiada swój własny kontekst.
#### Execution Stack
**Execution Stack** - miejsce w którym przechowywane są konteksty wykonania. Domyslnie trafia do niego Global Execution Context a następnie według zasady **LIFO (last in, first out)** pozostałe konteksty zostają do niego kolejno dodawane i w trakcie wykonywania - usuwane.

### Silnik, kompilator i zakres
Engine & Compilator & Scope

* Engine - odpowiedzialny za kompilację i wykonanie kodu
* Compiler - odpowiedzialny za parsowanie i przygotowanie kodu dla silnika
* Scope - odpowiedzialny za gromadzenie i zarządzanie zadeklarowanymi zmiennymi i tym, w jaki sposób te informacje dostepne są dla aktualnie wykonywanego kodu.

### Zakres

**Przechowywanie i zarządzanie zmiennymi**
Zarządzanie zmiennymi jest fundamentalną cechą języka programowania i wymaga złożonego systemu zasad. System ten nazywamy zakresem.
**Zakres** \- system\, któego rola polega na określeniu gdzie i w jaki sposób zmienne mogą być onalezione\. Zmienne mogą być wyszukiwane na potrzeby:

* przypisania referencji (LHS - Left Hand Side look-up)
* zwrócenia wartości (RHS - Right Hand Side look-up)

| LHS | | RHS |
| :---: | :---: | :---: |
| `const name` | `=` | `"Anna"` |

**Zakres dynamiczny** \- zakres określany w momencie wykonywania kodu\. Nie jest wykorzystywany w JavaScript
**Zakres leksykalny (Lexical Scope)** \- zakres określany w momencie definiowania kodu\, w czasie trwania fazy leksykalnej \(lexical time\)\. Jego strukturę określa informacja o tym gdzie definiowane są zmienne i bloki\.

* Poszczególne zakresy mogą być w sobie wyłącznie ściśle zagnieżdżone
* JavaScript szukając identyfikatora zmiennej zaczyna od zakresu w którym się znajduje a następnie przechodzi do zewnętrznego zakresu i tak aż do momentu gdy dojdzie do zakresu globalnego lub do momentu odnalezienia szukanej wartości.

**Lexing (Tokenizing)** \- pierwsza faza pracy kompilatora\, polegająca na interpretowaniu ciągu tekstu kodu źródłowego na zrozumiałe dla silnika tokeny np\. wyrażenie `const name = "Anna"` zostaje rozłożone na `["const", "name", "=", "Anna"]`
**Przysłonięcie (Shadow Ring)** \- identyfikator znajdujący się w wewnętrznym scopie przesłania identyfikator znajdujący się w zewnętrznym scopie\.
Definiowanie zmiennej `glob` za pomocą słowa kluczowego `var` spowoduje dodanie tej zmiennej do obiektu globalnego `window` i umożliwi dostęp do wartości zmiennej poprzez `window.glob`

## JavaScript - Understanding the Weird Parts

### Konteksty wywołania i środowiska leksykalne

Kod w JavaScript → Parser składni → Kompilator → Kod zrozumiały dla komputera
**Parser składni** \- program\, który sprawdza kod pod kątem poprawności składni\.
**Kompilator** \- program\, który kompiluje kod do postaci zrozumiałej dla komputera\.
**Lexical Environment** \- wystepuje w językach programowania w któych istotne jest fizyczne rozmieszczenie kodu który piszemy
\*\*Execution Context  \*\*\- A wrapper to help manage the code that is running