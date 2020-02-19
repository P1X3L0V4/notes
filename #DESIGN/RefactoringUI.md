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

Nie każdy link wymaga wyróżnienia kolorystycznego

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

### Tworzenie skali dla tekstu

- Skale linearne nie sprawdzają się w przypadku tekstu (podobnie jak w przypadku odstępów)
- Skale modularne sprawdzają się nieco lepiej, ale powodują problemy i wymuszają wartości po przecinku oraz progi
  - 4:5 (_major third_)
  - 2:3 (_perfect fifth_)
  - 1:1.618 (_golden ratio_)
- Warto stosować skale dostosowane do danego projektu
  - 12px / 14px / 16px / 18px / 20xp / 24px / 30px / 36px / 48px / 60px / 72px
- Przy tworzeniu skali należy stosować `px` lub `rem` (jednostki em są względne do aktualnego rozmiaru fontu)

### Rodziny fontów

- Wykorzystywanie w projektach **dobrych fontów**, które posiadają często (nie zawsze) co najmniej 5 rodzajów pogrubienia
- Warto stosować fonty zgodnie z przeznaczeniem np. fonty dedykowane nagłówkom mają często krótszy _x-height_ (np. Futura PT)

### Paragrafy i wysokość linii

- Optymalna ilość znaków w linii to od 45 do 75 znaków
- W przypadku mieszanych rozmiarów fontów należy wyrównać je względem _baseline_
- Szerokość paragrafów i _line-height_ powinny być proporcjonalne
  - Wąska treść może używać mniejszej _line-height_ np. 1,5
  - Szeroka treść może wymagać _line-height_ o wysokości 2
- Wysokość linii i rozmiar czcionki są odwrotnie proporcjonalne
  - Warto stosować większy _line-height_ dla małego tekstu
  - Warto stosować mniejszy _line-height_ dla dla dużego tekstu

### Wyrównanie tekstu

- Tekst powinien być wyrównany z dopasowaniem do języka w którym pisany jest tekst (np. angielski do lewej)
- Warto używać centrowania tylko dla krótkich tekstów
- Numery w tabeli warto wyrównywać do prawej
- Dla wyjustowanego tekstu należy włączyć dzielenie tekstu `hyphens: auto`

### Odstępy między znakami

Generalna zasada jest taka że, warto zaufać projektantowi i pozostawić nie modyfikować odstępów między literami.

- Ścieśnianie nagłówków - gdy chcemy zasymulować _condensed_ dla fontu na główka można spróbować dodać mu mniejszy `letter-spacing` np. `-0.05em`
- Poprawienie czytelność tekstu pisanego wielkimi literami - odstępy między literami w większości rodzin fontów są zoptymalizowane pod kątem normalnego tekstu. Wielkie litery nie są tak zróżnicowane jak małe więc aby poprawić czytelność takiego tekstu warto zwiększyć `letter-spacing` do np. `0.05em`

## Kolor

- Warto używać formatu _HSL_ zamiast _HEX_
- Dobry projekt potrzebuje zestawów kolorów:
  - Szarości - 8 rodzajów od prawie czarnego do prawie białego
  - Kolory podstawowe - od 5 do 10
  - Kolory akcentujące - dla różnych stanów, statusów itp. Zazwyczaj kilka 5-10 palet po 5-10 kolorów każda

### Tworzenie palety

- Wybrać kolor bazowy - testy dla tła przycisku
- Wybieranie kolorów granicznych - testy dla wiadomości alertu (tło i tekst). Wychodzimy od tego samego odcienia (hue) i modyfikujemy jasność i nasycenie
- Wybieranie pozostałych barw - warto zacząć od wybrania kolorów w połowie pomiędzy końcami palety i powtarzać proces aż do zbudowania całej listy
- Podczas tworzenia palety w systemie _HSL_, aby uniknąć wrażenia wypranych kolorów, należy zwiększyć nasycenie gdy jasność oddala się od 50%

Manipulowanie _HSL_:

- Aby rozjaśnić kolor, zmień odcień w kierunku najbliższego jasnego - 60°, 180° lub 300°
- Aby przyciemnić kolor, zmień odcień w kierunku najbliższego ciemnego - 0°, 120° lub 240°
- Szarości mogą mieć odczuwalnie cieplejszy lub zimniejszy odcień

### Dostępność

#### Ratio kontrastu

Ratio kontrastu dla tekstu według _Web Content Accessibility Guidelines (WCAG)_:

- Normalny (poniżej ~18px) - 4.5:1
- duży tekst - 3:1

Jeśli chcemy spełnić wymogi wymaganego ratio kontrastu możemy zastosować kilka sztuczek:

- Odwracanie kontrastu - zamiast białego tekstu na kolorowym tle dla etykietek można zastosować ciemny kolorowy tekst na jasnym tle o tym samym odcieniu
- W przypadku białego tekstu wewnątrz ciemnych kolorowych bloków, aby spełnić warunek ratio kontrastowego należy często zbliżyć się do bieli. Aby tego uniknąć można obrócić odcień koloru (hue) na kole _HSL_ i na przykład użyć błękitnego tekstu zamiast białego w fioletowym boksie

#### Zaburzenia rozpoznawania barw

- W projekcie nie należy polegać wyłącznie na kolorach - warto dodawać inne wskaźniki np. ikony
- W przypadku wykresów bezpieczniej jest operować kontrastem tego samego koloru niż polegać na różnych kolorach, które mogą nie zostać poprawnie rozpoznane przez osoby z zaburzeniami

## Tworzenie głębi

### Wypukłość

Jeśli chcemy, aby element wyglądał na wypukły lub wklęsły, najpierw warto określić jaki ma mieć profil, a następnie naśladować sposób oddziaływania źródła światła na ten kształt.

Elementy wypukłe

- Światło od góry wewnątrz `box-shadow: inset 0 1px 0 hsl(224, 84%, 74%)`
- Cień na dole na zewnątrz `box-shadow: 0 1px 3px hsl(0, 0%, 0%, .2)`

Elementy wklęsłe

- Cień u góry wewnątrz `box-shadow: inset 0 2px 2px hsl(0, 0%, 0%, 0.1)`
- Światło na dole na zewnątrz `box-shadow: 0 -2px 0 hsl(0, 0%, 100%, .15)`

Cienie pozwalają również lokować obiekty na osi `z-axis`

### Cienie

Na początku projektowania warto stworzyć paletę cieni np.

- `box-shadow: 0 1px 3px hsl(0, 0%, .2)`
- `box-shadow: 0 4px 6px hsl(0, 0%, .2)`
- `box-shadow: 0 5px 15px hsl(0, 0%, .2)`
- `box-shadow: 0 10px 24px hsl(0, 0%, .2)`
- `box-shadow: 0 15px 35px hsl(0, 0%, .2)`

Cienie mogą również wspierać interakcje:

- Dodanie cienia do elementu, który użytkownik przeciąga, wybija go z tła
- Cień przycisku po jego kliknięciu można zmniejszyć aby wydawał się bardziej wklęsły

Łącznie dwóch cieni

- Pierwszy cień jest większy i jaśniejszy (większy offset pionowy i rozmycie), symuluje cień rzucany przez bezpośrednie źródło światła padające na obiekt
- Drugi cień jest mniejszy i ciemniejszy (mniejszy offset pionowy i rozmycie), symuluje cień rzucany przez ambientowe źródło światła padające na obiekt

### Głębia we flat designie

- Kolory: jasny - blisko, ciemny - daleko
- Proste cienie bez rozmycia

### Nakładanie elementów

Jednym z najskuteczniejszych sposobów tworzenia głębi jest nakładanie na siebie różnych elementów, aby wydawało się, że projekt ma wiele warstw.

Ten efekt łatwo osiągnąć dodając ujemne marginesy

## Praca z obrazami

Brzydkie zdjęcie (obraz) potrafi zepsuć nawet najlepszy projekt

### Tekst na zdjęciach

Tekst na zdjęciach (np. dużych bannerach) potrzebuje kontrastu, jeśli zdjęcie jest zróżnicowane można:

- Dodać ciemną nakładkę na zdjęcie `background-color: hsla(0, 0%, 0%, .55)`
- Obniżyć kontrast zdjęcia (efekt białej nakładki) - jasność +40%, kontrast -70%
- Koloryzacja zdjęcia
  - Obniżenie kontrastu zdjęcia
  - Desaturacja zdjęcia
  - Dodanie wypełnienia przy użyciu mieszania _multiply_
- Dodanie cienia do tekstu `text-shadow: 0 0 50px hsla(0, 0%, 0%, .4)`

### Wymiary obrazów

Skalowanie ikon

- Małych ikon nie należy skalować do dużych. Zamiast tego warto użyć:

  - Innego zestawu zaprojektowanego do tego celu
  - Nieprzeskalowanej ikony z tłem np. okrągłym

- Ikona favicon nie powinna byc skalowana, ale zaprojektowana w sposób uproszczony, tak aby dobrze wyglądać po zmniejszeniu

Skalowanie screenshotów

Duże screenshoty zmniejszone do małych wymiarów nie wyglądają dobrze, zamiast tego można:

- Wykonywać screenshot na mniejszym ekranie
- Zawrzeć na obrazie tylko fragment screenshota np. w kole
- Stworzyć obraz screenshota z uproszczonym UI

Kontrola treści uploadowanych przez użytkownika

- Wysokości i szerokości obrazów
- Obrazy ładowane jako avatary mogą być pozbawione kontrastu, warto stworzyć subtelne obramowanie za pomocą cienia: `box-shadow: inset 0 0 0 1px hsl(0, 0%, 0%, .1)`

## Ostatnie poprawki

Sposoby na dodanie jakości projektowi

- Ikony zamiast wypunktowania
- Ikony cudzysłowia zamiast wersji tekstowej
- Zmiana kolorów i pogrubienia linków
- Dodanie customowego podkreślenia dla linków
- Customowe stylowanie formularzy
- Dodanie kolorowego grubszego obramowania (linii) na górze boksów
- Dodanie podkreślenia do aktywnego linku w menu
- Dodanie kolorowego grubszego obramowania (linii) na lewo od boksa z alertem
- Dodanie kolorowej linii oddzielającej nagłówek od tekstu
- Dekorowanie tła
  - Kolor
  - Gradient - 2 odcienie których różnica wynosi nie więcej niż 30° w _HSL_
  - Subtelny wzorek na tle
  - Dodanie prostych kształtów lub ilustracji (fale, piramida lub mapa z kropek)
- Należy pamiętać o pustym stanie np. brak kontaktów na liście
- Oddzielanie elementów:
  - Warto ograniczyć `border` na rzecz `box-shadow`
  - Stosowanie dwóch kolorów tła
  - Zwiększenie odstępów
