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
```

## Typy zmiennych
