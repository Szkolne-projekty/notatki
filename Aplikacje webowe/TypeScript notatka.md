# Notatka z TypeShit

<sub><sup><sub>wygenerowane przez ai</sub></sup></sub>

## Deklaracja zmiennych i typy prymitywne

W TypeScript obowiązuje statyczne typowanie, czyli definiujemy typ zmiennej podczas deklaracji.

-   **string** – tekst

```typescript
let nazwisko: string = "Kowalski"; // deklaracja zmiennej typu string
let imie = "Adam"; // typ wywnioskowany jako string
```

-   **number** – liczby całkowite i zmiennoprzecinkowe

```typescript
let liczba: number = 17.5; // zmienna typu number
```

-   **boolean** – wartość prawda/fałsz

```typescript
let czyAktywny: boolean = true; // wartość logiczna
```

### Uwagi dotyczące deklaracji zmiennych

Do deklaracji zmiennej można zamiast **let** użyć **var**, jednak nie jest to zalecana praktyka ze względu na różnice w zasięgu zmiennych.

Przy deklaracji zamiast **let** możemy użyć **const**, co oznacza stałą.  
Zmienna zadeklarowana przy użyciu **const** nie może być przypisana ponownie. Wartość przypisana podczas inicjalizacji pozostaje stała przez cały czas działania programu.

```typescript
// Przykład zmiennych var, let, const
var exampleVar = 1; // starszy sposób, zakres funkcji
let exampleLet = 2; // zalecany, zakres blokowy
const exampleConst = 3; // stała, wartość niezmienna
```

**"var"** jest starszym sposobem deklaracji zmiennych, obecnie zaleca się używanie "let" lub "const" ze względu na ich blokowy zasięg

```
var exampleVar = 1;
let exampleLet = 2;
const exampleConst = 3; // stała, której wartość nie może się zmienić
```

## Typy złożone

### Tablice - różne sposoby deklaracji

-   Tablica elementów typu string deklarowana jako `string[]`

```typescript
const imiona: string[] = ["Jan", "Filip", "Adam"]; // tablica stringów
```

-   Tablica elementów typu string deklarowana jako generyk `Array<string>`

```typescript
const imiona2: Array<string> = ["Tadeusz", "Gilberta", "Albert"];
```

-   Tablica z inferowanym typem (bez podawania typu)

```typescript
const nazwiska = ["Kowalski", "Nowak", "Tryla"];
```

-   Tablica elementów typu number

```typescript
const wiek: number[] = [45, 50, 19];
```

-   Dostęp do elementów tablicy i wypisanie ich na konsolę:

```typescript
console.log(nazwiska[0] + ", " + nazwiska[1] + ", " + nazwiska[2]); // Wynik: Kowalski, Nowak, Tryla
```

---

## Funkcje

Deklaracja funkcji z typami parametrów i wartości zwracanej:

```typescript
// Funkcja wyświetlająca powitanie na podstawie imienia
function przywitanie(imie: string): void {
    console.log(`Witaj, ${imie}!`);
}
przywitanie("Marek"); // wywołanie funkcji
```

Funkcja z parametrem domyślnym:

```typescript
// Funkcja sumująca trzy liczby, gdzie trzeci parametr jest opcjonalny i domyślnie 0
function suma(a: number, b: number, c: number = 0): number {
    return a + b + c;
}
console.log(suma(2, 5)); // wynik: 7
```

Funkcja z parametrem opcjonalnym (`?`):

```typescript
// Funkcja wypisująca powitanie, opcjonalnie z tytułem
function powitanie(imie: string, tytul?: string): string {
    return tytul ? `Witaj, ${tytul} ${imie}` : `Witaj, ${imie}`;
}
```

Funkcja wariadyczna (rest parameter):

```typescript
// Funkcja przyjmująca dowolną liczbę imion i zwracająca powitanie
function powitajWielu(...imiona: string[]): string {
    return `Witajcie ${imiona.join(", ")}`;
}
console.log(powitajWielu("Anna", "Tomek", "Ela"));
```

Funkcja strzałkowa – alternatywna składnia:

```typescript
// Funkcja dodająca dwie liczby
const suma = (a: number, b: number): number => a + b;
```

---

## Klasy i obiekty

Definicja klasy, konstruktor, pola, metody:

```typescript
// Klasa reprezentująca klienta z polami i metodą do wyświetlania danych
class Klient {
    imie: string;
    nazwisko: string;
    wiek: number;
    kontakt: string[];

    constructor(
        imie: string,
        nazwisko: string,
        wiek: number,
        kontakt: string[]
    ) {
        this.imie = imie; // przypisanie imienia
        this.nazwisko = nazwisko; // przypisanie nazwiska
        this.wiek = wiek; // przypisanie wieku
        this.kontakt = kontakt; // przypisanie kontaktów
    }

    // Metoda wyświetlająca informacje o kliencie
    wyswietl(): void {
        console.log(`Imię: ${this.imie}`);
        console.log(`Nazwisko: ${this.nazwisko}`);
        console.log(`Wiek: ${this.wiek}`);
        console.log(`Kontakt: ${this.kontakt.join(", ")}`);
    }
}

const klient1 = new Klient("Tadeusz", "Nowak", 45, [
    "123456789",
    "email@example.com",
]);
klient1.wyswietl();
```

### Modyfikatory dostępu

-   `public` - dostęp wszędzie (domyślnie)
-   `private` - dostęp tylko w obrębie klasy
-   `protected` - dostęp w klasie i klasach dziedziczących

### Gettery i settery

```typescript
// Klasa reprezentująca auto z getterem i setterem pola numer silnika
class Auto {
    public marka: string;
    private numerSilnika: string;

    constructor(marka: string, numerSilnika: string) {
        this.marka = marka;
        this.numerSilnika = numerSilnika;
    }

    // Getter zwraca numer silnika
    get silnik(): string {
        return this.numerSilnika;
    }

    // Setter pozwala zmienić numer silnika gdy nowy nie jest pusty
    set silnik(nowyNumer: string) {
        if (nowyNumer.length > 0) this.numerSilnika = nowyNumer;
        else console.log("Numer silnika nie może być pusty.");
    }
}
```

---

## Dziedziczenie i klasy abstrakcyjne

Dziedziczenie:

```typescript
// Klasa bazowa reprezentująca ogólną figurę geometryczną
class Figura {
    nazwa: string;

    constructor(nazwa: string) {
        this.nazwa = nazwa; // przypisanie nazwy figury
    }

    // Metoda zwracająca opis figury
    opis(): string {
        return `To jest figura: ${this.nazwa}.`;
    }

    // Metoda zwracająca pole obszaru (domyślnie 0)
    pole(): number {
        return 0;
    }
}

// Klasa potomna reprezentująca prostokąt dziedziczący po Figurze
class Prostokat extends Figura {
    szerokosc: number;
    wysokosc: number;

    constructor(szerokosc: number, wysokosc: number) {
        super("prostokąt"); // wywołanie konstruktora klasy bazowej
        this.szerokosc = szerokosc;
        this.wysokosc = wysokosc;
    }

    // Nadpisanie metody pola prostokąta
    pole(): number {
        return this.szerokosc * this.wysokosc;
    }
}

const prostokat = new Prostokat(10, 5);
console.log(prostokat.opis()); // To jest figura: prostokąt.
console.log(`Pole prostokąta: ${prostokat.pole()}`); // 50
```

Klasy abstrakcyjne:

```typescript
// Klasa abstrakcyjna definiująca szkielet figury z metodą abstrakcyjną
abstract class FiguraAbstrakcyjna {
    abstract pole(): number; // metoda bez implementacji

    // Metoda wyświetlająca pole figury
    pokazPole(): void {
        console.log(`Pole figury: ${this.pole()}`);
    }
}

// Klasa potomna implementująca klasę abstrakcyjną dla kwadratu
class Kwadrat extends FiguraAbstrakcyjna {
    bok: number;

    constructor(bok: number) {
        super();
        this.bok = bok;
    }

    // Implementacja metody pola kwadratu
    pole(): number {
        return this.bok * this.bok;
    }
}

const kwadrat = new Kwadrat(4);
kwadrat.pokazPole(); // Pole figury: 16
```

---
