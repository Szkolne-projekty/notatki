# TABLICE
Tablice pozwalają na przechowywanie zbioru danych okeślonego typu

## Indeksowanie numeryczne (klasyczne)

### Tworzenie tablicy
```php
$tablica = array(wartosc1, wartosc2, wartoscN);
```

Można również zapisać
```php
$tablica = array(
wartosc1,
wartosc2,
wartoscN);
```
### Wyświetlanie
```php
<?php
$kolory = array ("czerwony", "zielony", "niebieski");
echo " kolor[0] = $kolory[0] <br>";   //czerwony
echo " kolor[2] = $kolory[2] <br>";   //niebieski
```

Wypisanie wszystkiego za pomocą pętli
```php
$kolory = array ("czerwony", "zielony", "niebieski");
for ($i = 0; $i < 3; $i++){
  echo " kolor[$i] = $kolory[$i] <br> ";
}
?>
```

## Tablice asocjacyjne
```php
$nazwa_tablicy['nazwa_kolumn'] = array("klucz1" => "wartosc1", "klucz2" => "wartosc2");
```

Modyfikacja 
```php
$tablica['nazwa_klucza'] = 'cos tam';
```

# Tablice dwuwymiarowe

### Tworzenie 
```php
<?php
$tablica = array
(
array(1,2,3),
array(4,5,6)
};

$tablica[wiersz, kolumna]
echo " $tablica[0][0] ";   //itd
```

### Do odczytu stosujemy pętle FOR
```php
for($i = 0; $i < 3; $i++){
  for($j = 0; $j < 3; $j++){
    $wart = $tablica[$i][$j];
    echo " Tablica [$i][$j] = $wart ";
  }
}
```

## Mogą być też tabele asocjacyjne
```php
$tablica = array(
array("Autor" => "Autor1",
      "Tytuł" => "Tytuł1",
      "Numer" => "Numer1"),
array("Autor" => "Autor2",
      "Tytuł" => "Tytuł2",
      "Numer" => "Numer2"),
array("Autor" => "Autor3",
      "Tytuł" => "Tytuł3",
      "Numer" => "Numer3")
);
```

## Tablice nieregularne
```php
$tablica = array
(
array (1,2,3,4),
array (5,6,),
array (7),
array (8,9,10)
);
```

```php
foreach ($tablica as $tab){
  foreach ($tab as $val){
    echo "$val";
  }
}
```

# Implementacja i eksplodacja

## Funkcja implode
```php
$arr = array('jeden', 'dwa', 'trzy');
echo implode (',', $arr);    // wyswietli jeden, dwa, trzy
echo implode ('_', $arr);    // wyswietli jeden_dwa_trzy
```

## Funkcja explode
```php
explode (separator, ciąg[ile]);

$str = 'jeden, dwa, trzy';
$str = explode (',', $str);
```

Możemy ustawić limit:
```php
$text = "jabłko,banan,gruszka,malina";
$wynik = explode(",", $text, 3);
print_r($wynik);

Array
(
    [0] => jabłko
    [1] => banan
    [2] => gruszka,malina
)
```

Jeśli limit damy ujemny, np -2 to:
```php
Array
(
    [0] => jabłko
    [1] => banan
)
```

# Poruszanie się po tablicy

- reset($tab) – ustawia wskaźnik na pierwszy element tablicy i go zwraca
- next($tab) – przesuwa wskaźnik na następny element 
- prev($tab) – cofa wskaźnik na poprzedni element 
- end($tab) – ustawia wskaźnik na ostatni element 
- current($tab) – zwraca bieżący element wskazywany przez wskaźnik

# Dodawanie i usuwanie elementów

Dodawanie:
- array_push($tab, $x, $y) – dodaje elementy na koniec tablicy
- array_unshift($tab, $x, $y) – dodaje elementy na początek tablicy

Usuwanie:
- array_pop($tab) – usuwa i zwraca ostatni element tablicy
- array_shift($tab) – usuwa i zwraca pierwszy element tablicy

Przykład:
```php
$tab = [1, 2, 3];

array_push($tab, 4);  // [1, 2, 3, 4]
array_unshift($tab, 0); // [0, 1, 2, 3, 4]

echo array_pop($tab);  // 4 (usunie ostatni)
echo array_shift($tab); // 0 (usunie pierwszy)
```

# Liczenie elementów w tablicy

```php
$tab = array(1,2,3);
$rozmiar = count($tab); // Wypisze 3
```

array_count_values($tab) – zlicza wystąpienia unikalnych wartości w tablicy
```php
$tab = ["a", "b", "a", "c", "b", "b"];
$wynik = array_count_values($tab);
print_r($wynik);

Array
(
    [a] => 2
    [b] => 3
    [c] => 1
)
```
