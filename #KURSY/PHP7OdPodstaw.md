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
