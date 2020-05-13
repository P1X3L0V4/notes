# Eduweb - PHP 7 Od Podstaw

## PHP

- dynamicznie typowany skryptowy język programowania, służący do rozszerzania możliwości stron internetowych
- rozwijany od 1994 roku
- najnowsza wersja 7 została wprowadzona z pominięciem numeru 6

## Linux - Podstawy

- `pwd` - zwraca ścieżkę do obecnego katalogu
- `ls` - lista plików i katalogów
- `ls -l` - lista plików i katalogów rozbudowana
- `ls -a` - lista plików i katalogów rozbudowana + pliki ukryte
- `ls man` - zwraca pełna dokumentację danej komendy
- `cd` - zmiana katalogu
- `cd ..` - przejdź katalog wyżej
- `mkdir` - tworzy katalog
- `apt-get update` - aktualizacja pakietów
- `apt-get install php` - instalacja wskazanego programu
- `php index.php` - uruchamianie skryptów

Uprawnienia plików:

- Pierwsza litera: `d` - katalog, `-` - plik
- 3 znaki - uprawnienia właściciela pliku
- 3 znaki - uprawnienia grupy
- 3 znaki - uprawnienia dla pozostałych użytkowników
- `r` - read, odczyt
- `w` - write, zapis
- `x` - execute, wykonywanie

## Konfiguracja środowiska

- Apache konfiguracja w pliku `000-default.conf`

## Podstawy PHP

```php
// Otwieranie i zamykanie znacznikó kodu

<?php

?>
```

```php
// Komentarz pojedyńczy

/*
Komentarz
wieloliniowy
*/
```

```php
// Wyświetlanie zawartości

echo "Hello world!";
echo $zmienna
```

## Zmienne

Definiowanie

```php
$nazwa = "wartość";

$text = "Abc";
$a = 90;
$b = 90.1;
```

### Rodzaje zmiennych w PHP

- `boolean` - prawda/fałsz
- `integer` - liczba całkowita
- `float` - liczba zmiennoprzecinkowa (podajemy z kropką)
- `string` - tekst
- `array` - tablica
- `object` - obiekt
- `resource`
- `null` - zamierzony brak wartości

```php
// Zwracanie wartość zmiennej wraz z jej typem

var_dump($bool); // Zwraca np. bool(false)
```

### Nazywanie zmiennych

Nazwy tworzymy zaczynając od znaku dolara `$` oraz:

- małej lub wielkiej litery lub
- podkreślnika `_`

Nazwy:

- piszemy `camelCase`
- mogą zawierać cyfry

### Zasięg zmiennych

**Zasięg zmiennych** - określa, gdzie możemy skorzystać z danej zmiennej

- globalne - dostępne dla całego programu
- lokalne - dostępne wewnątrz danego bloku kodu np. funkcji

Aby odwołać się wewnątrz funkcji do zmiennej globalnej

- Korzystamy ze słowa kluczowego `global`

  ```php
  $a = 90;

  function test(){
    global $a;
    echo "Zmienna globalna: " . $a;
  }

  test();
  ```

- Korzystamy z `$GLOBALS`

  ```php
  $a = 90;

  function test(){
    echo "Zmienna lokalna:" . $GLOBALS['a'];
    $a = 100;
  }

  test();
  ```

### Operacje na zmiennych

Operator łączenia

```php
// Do łączenia zmiennych wykorzytujemy operator kropki

$text1 = "Hello";
$text2 = "World!";

$text1.$text2 // Zwraca HelloWorld!
$text1." ".$text2 // Zwraca Hello World!
```

Cudzysłowy

- Pojedynczy `''` oznacza traktowanie danego fragmentu jako tekst
- Podwójny `""` pozwala również wyświetlać zmienne

## Funkcje

```php
function test($a = "Moja testowa funkcja"){
  echo $a;
}

test("Test funcji");
```

### Funkcje dla kalkulatora

```php
<?php

function add(float $a,float $b):float{ // Typowanie parametrów funkcji oraz typu wyjściowego
  return $a + $b;
}

function deduct(float $a, float $b):float{
    return $a - $b;
}

function multiply(float $a, float $b):float{
    return $a * $b;
}

function divide(float $a, float $b){
    if($b === 0.0){
      return "Nie można dzielić przez zero";
    }

    return $a / $b;
}


echo "dodawanie: " . add(3.1,5.2) . "\n";
echo "odejmowanie: " . deduct(5.3,3.3) . "\n";
echo "mnożenie: " . multiply(5.3,3.3) . "\n";
echo "dzielenie: " . divide(5.3,0) . "\n";
echo "dzielenie: " . divide(5.3,2) . "\n";

```

## Operatory

### Arytmetyczne

- Dodawanie `=`
- Odejmowanie `-`
- Mnożenie `*`
- Dzielnie `/`
- Modulo (reszta z dzielenia) `%`

```php
$a = 9;
$b = 4;

$d = $a / $b;
$c = $a % $b;

var_dump($d, $c);
```

### Przypisania

- Wykonanie operacji arytmetycznej i przypisanie wyniku do zmiennej `+=`, `-=`, `*=`, `/=`, `%=`
- Operator dalszego ciągu dla stringów `.=`

```php
$a = 3;
$a .= 3; // Wartości liczbowe zostaną zaminione na stringi

var_dump($a);
```

### Porównania

- Równość `==`
- Identyczność `===`
- Nierówność `!=`
- Mniejsze `<`
- Mniejsze równe `<=`
- Większe `>`
- Większe równe `>=`

```php
$a = 3;
$b = 4;

var_dump($a <= $b);
```

### Inkrementacji

- Preinkrementacja `++a`
- Postinkrementacja `a++`
- Predekrementacja `--a`
- Postdekrementacja `a--`

```php
$a = 4;

var_dump($a--, $a); // 4, 3
```

### Logiczne

- `AND` lub `&&`
- `OR` lub `||`
- `XOR` - ekskluzywny operator OR, zwraca `true` tylko dla pary wartości `true false`
- Operator zaprzeczenia `!`

```php
// TRUE AND TRUE => TRUE
// TRUE AND FALSE => FALSE
// FALSE AND FALSE => FALSE

// TRUE OR TRUE => TRUE
// TRUE OR FALSE => TRUE
// FALSE OR FALSE => FALSE

// TRUE XOR TRUE => FALSE
// TRUE XOR FALSE => TRUE
// FALSE XOR FALSE => FALSE

// !TRUE => FALSE
// !FALSE => TRUE
```

## Tablice

### Tworzenie

```php
// Tworzenie pustej tablicy
$a = arrray();
$a = [];

// Tworzenie tablicy z kluczami i wartościami
$a = [
  'kot' => 'a',
  'pies' => [
    'łapy' => 4, // Możemy tworzyć pary klucz - wartość
    'ogon' => 1,
  ],
  'fretka' => 'c',
];

var_dump($a);
```

### Dodawanie

```php
$tablica = [
  'kot' => 'a',
  'pies' => [
    'łapy' => 4,
    'ogon' => 1,
  ],
  'fretka' => 'c',
];

// Dodawanie elementów do tablicy w pierwszym wolnym indeksie
$tablica[] = "nowa_wartosc";

// Metoda push
array_push($tablica, "nowa_wartosc");
```

### Usuwanie

```php
// usuwanie wartości pod kluczem
unset($tablica['kot']);

// Metoda array_pop usuwa ostatni element tablicy i zwraca go
array_pop($tablica);
```

### Odwoływanie się do wartości

```php
// Odwoływanie się do wartości w tablicy zagnieżdżonej i zwykłej
$b = $a['kot'];
$b = $a['pies']['łapy'];

// Odwoływanie się do wartości w tablicy dynamiczne
$a = [
  'samochód' => [
    'koła' => 4,
    'szyby' => 2,
  ],
  'motocykl' => [
    'koła' => 2,
    'szyby' => 0,
  ],
];

$c = 'ciężarówka';
if(isset($a[$c])){
  $b = $a[$c]['koła'];
} else {
  $b = NULL;
}

var_dump($b);
```

### String <=> Tablica

```php
$a = "jakaś wartość tekstowa";

// Zamiana stringa na tablicę oddzielając podanym znakiem (pierwszy argument)
$b = explode(' ', $a);

// Zamiana tablicy na string oddzielając podanym znakiem (pierwszy argument)
$c = implode(' ', $b);

var_dump($b, $c);
```

### Porównywanie tablic

```php
$array1 = array("a" => "green", "red", "blue", "red");
$array2 = array("b" => "green", "yellow", "red");
$result = array_diff($array1, $array2);

print_r($result);
```

### Iterowanie po elementach

```php
$a = [
  'kot',
  'pies',
  'rybka',
];

// Przechodzenie po elementach tablicy
$b = array_walk($a, function() {

})

// Od PHP7 możliwe funkcje anonimowe
// Mapowanie tablicy, nie modyfikuje oryginalnej tablicy
$b = array_map(function ($value){
  return strtoupper($value);
}, $a);

var_dump($a, $b);
```

## Konwersja typów

PHP potrafi konwertować typy w sposób niejawny (automatycznie gdy np. dodajemy liczbę do tekstu) oraz jawny

```php
$a = '31kot';

// Jawny
var_dump((int)$a);
```
