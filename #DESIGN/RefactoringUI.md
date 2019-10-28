# Refactoring UI - Adam Wathan, Steve Schoger

- Rozpoczynanie od projektowania funkcji, a nie layoutu
- Projektowanie od ogółu do szczegółu
- Projektowanie w czarno-bieli
- Rozpoczynanie projektu od niezbędnych funkcji
- Projektowanie w cyklach (projektowanie -> kodowanie)
- Osobowość projektu
  - Typografia
  - Kolor
  - Border-radius
  - Język przekazu
- Systematyzowanie
  - Tworzenie systemów decyzyjnych
    - Paleta kolorów
    - Rozmiary fontów
    - Pogrubienie fontów
    - Wysokość wiersza
    - Margines
    - Padding
    - Szerokość
    - Wysokość
    - Box-shadow
    - Border radius
    - Border width
    - Przezroczystość
  - Proces eliminacji poprzez porówywanie elementów

## Hierarchia

**Hierarchia wizualna** odnosi się do tego, jak ważne są elementy interfejsu w relacji do siebie nawzajem

### Fonty

Hierarchizacja oparta wyłącznie na rozmiarze nie jest efektywna.

Warto wybrać i stosować 2 lub 3 kolory dla fontów (hierarchia oparta na kontraście)

- Ciemny kolor dla najważniejszej zawartości (np. nagłówki)
- Szary dla zawartości drugorzędnej (np. data publikacji)
- Jasno-szary dla zawartości trzeciorzędnej (np. copyright w stopce)

Warto stosować 2 rodzaje _font-weight_ w projekcie

- Normalne pogrubienie (400 lub 500) dla większości tekstu
- Większe pogrubienie (600 lub 700) dla tekstu, który chcemy wyróżnić

Czego unikać

- Należy ostrożnie stosować fonty poniżej 400, ze względu na ich widoczność na mniejszych ekranach.
- Nie używać szarego tekstu na kolorowych tłach, zamiast tego wybrać kolor o tym samym odcieniu (hue) i dopasować nasycenie i jasność

### Podkreślanie znaczenia

Czasem, aby podkreślić znaczenie elementu należy zmniejszyć znaczenie elementów z nim sąsiadujących (np. zmienić kolor nieaktywnych elementów w menu z czarnego na szary)

### Etykiety

- Unikanie pułapki prezentowania danych w postaci etykiet, które czasem utrudniają hierarchizowanie.
- Warto prezentować dane w taki sposób, aby etykiety były elementem treści np. "3 pokoje" zamiast "Pokoje: 3"
- Gdy etykiety dla treści są potrzebne należy pamiętać o tym by ich rola w designie była drugorzędna (mniejszy rozmiar fontu, jaśniejszy kolor, mniejsze pogrubienie)
- W przypadku treści gdzie etykiety są kluczowe np. w dokumentacji należy podkreślić ich widoczność

### Oddzielanie hierarchii wizualnej od hierarchii dokumentu

Nie pozwól, aby element, którego używasz, wpływał na sposób jego stylizacji - wybieraj elementy do celów semantycznych i styluj je w taki sposób by stworzyć jak najlepszą wizualną hierarchię.

### Pogrubienie i kontrast

- Mniejszy kontrast może kompensować pogrubienie np. w przypadku ikon nie możemy zmniejszyć pogrubienia, ale możemy przydzielić danej ikonie jaśniejszy kolor
- Większe pogrubienie może kompensować niski kontrast np. pogrubienie jasnoszarego obramowania pozwala zwiększyć jego widoczność bez utraty lekkości

### Semantyka

Podczas projektowania nie należy zapominać o hierarchii akcji

- Najważniejsze akcje powinny być wyraźnie oznaczone np. poprzez wysoki kontrast tła
- Akcje drugorzędne powinny być być jasne, ale nie uwidocznione np. przycisk z jaśniejszym obramowaniem lub kolorem tła
- Akcje trzeciorzędne powinny być dostępne, ale dyskretne np. podobne stylowanie jak w przypadku linków

## Layout i odstępy

Warto zaczynać projektowanie od dodania dużej ilości pustej przestrzeni (_white space_) i stopniowym jej usuwaniu. Zwarte layouty nadal sprawdzają się w przypadku niektórych projektów.

### Tworzenie systemów dla rozmiarów i odstępów

- Jeśli chcesz, aby Twój system ułatwiał podejmowanie decyzji dotyczących rozmiarów, upewnij się, że dwie wartości w skali nie są nigdy bliższe niż około 25%.
- 16px to świetna liczba na początek, ponieważ łatwo się dzieli, a także jest domyślnym rozmiarem fontów w każdej większej przeglądarce internetowej.
- Projekt nie musi wypełniać całego ekranu
- Projektowanie _mobile first_
- W przypadku niektórych treści warto dzielić layout na kolumny (sekcje)
- Nie zawsze warto używać grida w projektowaniu np. jeśli mamy projekt z menu w sidebarze warto mu ustawić _fixed-width_ dostosowany do zawartości
- Rozmiary względne nie są skalowane np. ustawienie 2.5em dla nagłówka może dobrze sprawdzić się dla desktopu, ale być zbyt dużym rozmiarem w przypadku mobile
- Generalna zasada jest taka, że duże elementy na dużych ekranach muszą się kurczyć szybciej niż elementy, które są małe. Różnica między małymi a dużymi elementami powinna być mniej ekstremalna na małych ekranach.
- Poszczególne elementy niekoniecznie powinny skalować się proporcjonalnie np. przyciski mogą mieć proporcjonalnie większy _padding_ na desktopie niż na małym ekranie
- Unikaj niejednoznacznych odstępów. Ilekroć korzystasz z odstępów w celu połączenia grupy elementów, zawsze upewnij się, że wokół grupy jest więcej miejsca niż w jej obrębie

## Projektowanie tekstu
