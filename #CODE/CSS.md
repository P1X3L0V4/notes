# CSS

## Hierarchia stylów CSS

* Ważne style użytkownika
* Ważne style autora
* Style autora
    * Style inline
    * Style w \<head> (zamknięte w tagu \<style>)
    * Style w pliku .css
* Style użytkownika
* Style przeglądarki

| 0 | 0 | 0 |
| :---: | :---: | :---: |
| ID | CLASS | TAG |

**Przykłady**
`p {color: black;}` \- waga: 001 \(id = 0\, class = 0\, tag = 1\)
`.nazwa p {color: black;}` \- waga: 011 \(id = 0\, class = 1\, tag = 1\)
`#nazwa .nazwa p ul li a {color: black;}` \- waga: 114

### Składnia selektorów

W składni CSS3 spacja oznacza wejście do danego selektora
`p.nazwa span {}` \- odnajdzie wszystkie `<p>` z klasą nazwa i ostyluje znajdujące się w nim elementy `<span>`
`p .nazwa span` \- odnajdzie wszystkie `<p>`, następnie poszuka w nich dowolnych elementów z klasą `nazwa`, a w tych elementach wszystkich elementów `<span>`

## Łączniki

### Selektor potomka

Selektor potomka tworzymy dzięki dwóm lub więcej selektorom prostym rozdzielonym znakiem białym. Reguły odnoszą się do elementów, które są potomkami elementu pasującego do pierwszego selektora prostego.
`div p { color:#f00; } -`wszystkie elementy `p`, które są potomkami elementu `div`
`div#myid li p.info { color:#f00; }` \- wszystkie elementy `p` z wartością `class` równą `info`, które znajdują się w elementach listy `li`, a te z kolei są zawarte w elemencie `div` o identyfikatorze `myid`

### Selektor dziecka

Selektor dziecka odnosi się do bezpośredniego potomka danego elementu. Selektor dziecka zawiera dwa lub więcej selektory rozdzielone znakiem większości, czyli “>”. Rodzic elementu występuje po lewej stronie “>”, a dopuszczalne znaki białe wokół łącznika. Tylko te elementy strong, które są bezpośrednimi potomkami elementu div będą objęte tą regułą.
`div > strong { color:#f00; }` \- reguła ta wpływa na wszystkie elementy `strong`, które są dziećmi elementu `div`

### Selektor sąsiedni

Selektor sąsiedni tworzymy przez połączenie dwóch selektorów prostych znakiem `+`. Dopuszczalne jest występowanie białych znaków wokół łącznika. Selektor pasuje do elementu, który jest rodzeństwem pierwszego elementu. Elementy muszą mieć tego samego rodzica, a pierwszy z nich występować przed drugim.
`p + p { color:#f00; }`

Jeżeli zastosujemy powyższe reguły do następnego przykładu to formatowaniu ulegnie jedynie drugi paragraf, czyli p2:

```
<div>
  <p>p1</p>
  <p>p2</p>
</div>
```

### Importowanie plików CSS

`@import (url);` \- pozwala zaimportować plik `.css` w innym pliku ze stylami

### Dobre praktyki CSS

* Pisanie krótkich selektorów
* Nie stosowanie identyfikatorów (tylko klasy)
* Używanie intuicyjnych nazw selektorów
* Osadzanie styli w pliku .css
* Nie używać !important
* Używanie pliku reset.css ([http://cssreset.com/](http://cssreset.com/))
* Używamy skróconą notację tam gdzie to możliwe

## Jednostki
### Absolutne
Mają fizyczne odzwierciedlenie w rzeczywistości

* in - 1in = 2.54 cm
* cm
* mm
* pt - 1/72 z 1 in
* pc - 1pc = 12pt
* px - 1px = 0.75pt

### Relatywne
Pozostają w relacji do elementów na stronie

* %
* em - 1em = 100%
    * font-size - odnosi się do wartości rodzica (jeśli font-size body to 16px to 2em = 32px)
    * padding i inne elementy - odnoszą się do elementu w którym sa zawarte (jeśli font-size body to 16px a font-size elementu to 2em, to padding 2em = 64px (32x2))
* rem - root em - wartości liczone zawsze w odniesieniu do wartości elementu nadrzędnego
    * Wszystkie wartości - odnoszą się do wartości rodzica (jeśli font-size/padding/margin itp. body to 16px to 2rem = 32px)
* ex (exes) - wysokość małych liter
* ch (character) - wysokość dużych liter
* vw - szerokość okna
* vh - wysokość okna
* vmin - minimalna wysokość
* vmax - minimalna szerokość

### Jednostki na stronach
```
html {
    font-size: 62.5%
    // wartość odpowiada 10px bo 100% = 16px, pozwala łatwiej przeliczać na remy
}

p {
	font-size: 2rem
}
```
## Kolory
### Szesnastkowy
`color: #000000` - po dwa znaki na kolor
### RGBA
`rgba(20, 100, 150, 1)` - red 0-255, green 0-255, blue 0-255, alpha 0-1
### HSLA
`hsla(170, 50%, 45%, 1)` - hue 0-360, saturation 0-100%, brightness -100%, aplha 0-1
