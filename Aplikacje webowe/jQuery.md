# jQuery - Funkcje i składnia (skrócone)

## 1. Selektory

-   **Uniwersalny:** `*`  
    Wybiera wszystkie elementy w dokumencie.
-   **Elementu:** `element` (np. `p`)  
    Wybiera wszystkie elementy podanego typu.
-   **ID:** `#id`  
    Wybiera element o danym unikalnym ID.
-   **Klasy:** `.klasa`  
    Wybiera elementy z określoną klasą CSS.
-   **Wielu elementów:** `element1, element2`  
    Wybiera elementy różnych typów.
-   **Wielu klas:** `.klasa1, .klasa2`  
    Wybiera elementy z różnych klas.
-   **Pierwszy element w typie:** `element:first`  
    Wybiera pierwszy element danego typu.
-   **Ostatni element w typie:** `element:last`  
    Wybiera ostatni element danego typu.
-   **Atrybutu:** `[nazwa-atrybutu]`  
    Wybiera elementy posiadające dany atrybut.

## 2. Eventy i ich obsługa

-   `bind(eventType, handler)`  
    Przypisuje zdarzenie do elementu.
-   `blur(handler)`  
    Gdy element traci fokus.
-   `change(handler)`  
    Gdy zmienia się wartość elementu (np. w formularzu).
-   `click(handler)`  
    Po kliknięciu na element.
-   `dblclick(handler)`  
    Po podwójnym kliknięciu.
-   `mouseenter(handler)`  
    Kursor wchodzi na element.
-   `mouseleave(handler)`  
    Kursor wychodzi z elementu.
-   `hover(handlerIn, handlerOut)`  
    Efekt najechania i opuszczenia myszką.
-   `submit(handler)`  
    Przesłanie formularza.
-   `scroll(handler)`  
    Przewijanie elementu.
-   `focus(handler)`  
    Element zyskuje fokus.
-   `keyup(handler)`  
    Zwolnienie klawisza.
-   `keydown(handler)`  
    Wciśnięcie klawisza.
-   `resize(handler)`  
    Zmiana rozmiaru okna przeglądarki.
-   `on(eventType, handler)`  
    Nowoczesny sposób przypisywania zdarzeń.
-   `off(eventType)`  
    Usuwanie zdarzeń.
-   `trigger(eventType)`  
    Ręczne wywołanie zdarzenia.

## 3. Efekty i animacje

-   `animate(properties, duration)`  
    Animuje CSS elementu.
-   `fadeIn(duration)`  
    Płynne pojawienie elementu.
-   `fadeOut(duration)`  
    Płynne zniknięcie elementu.
-   `hide(duration)`  
    Ukrywa element.
-   `show(duration)`  
    Pokazuje element.
-   `slideUp(duration)`  
    Zwijanie elementu w pionie (ukrywanie).
-   `toggle(duration)`  
    Przełączanie widoczności elementu.
-   `fadeToggle(duration)`  
    Przełączanie przez zanikanie i pojawianie.
-   `delay(duration)`  
    Opóźnia wykonanie animacji.
-   `stop()`  
    Zatrzymuje bieżącą animację.
-   `finish()`  
    Kończy wszystkie animacje i czyści kolejkę.

## 4. Manipulacja stylem i zawartością

-   `css(property)` lub `css(property, value)`  
    Pobiera lub ustawia styl CSS.
-   `width()` / `height()`  
    Pobiera lub ustawia szerokość/wysokość elementu.
-   `innerWidth()` / `innerHeight()`  
    Uwzględnia padding.
-   `outerWidth()` / `outerHeight()`  
    Uwzględnia padding i border (opcjonalnie margin).
-   `text()` / `text(value)`  
    Pobiera lub ustawia tekst bez HTML.
-   `html()` / `html(value)`  
    Pobiera lub ustawia kod HTML wewnątrz elementu.
-   `val()` / `val(value)`  
    Pobiera lub ustawia wartość pola formularza.

## 5. Zarządzanie klasami CSS

-   `addClass(className)`  
    Dodaje klasę do elementu.
-   `removeClass(className)`  
    Usuwa klasę z elementu.
-   `toggleClass(className)`  
    Dodaje lub usuwa klasę (przełącznik).
-   `hasClass(className)`  
    Sprawdza, czy element ma daną klasę.

## 6. Atrybuty HTML

-   `attr(attribute)` lub `attr(attribute, value)`  
    Pobiera lub ustawia atrybut.
-   `removeAttr(attribute)`  
    Usuwa atrybut.

## 7. Traversing DOM (przemieszczanie się po drzewie DOM)

-   `parent()`  
    Bezpośredni rodzic elementu.
-   `parents()`  
    Wszyscy przodkowie elementu.
-   `children()`  
    Wszystkie dzieci elementu.
-   `find(selector)`  
    Elementy zagnieżdżone w elemencie, pasujące do selektora.
-   `siblings()`  
    Rodzeństwo tego samego rodzica.
-   `next()`  
    Następny element na tym samym poziomie.
-   `nextAll()`  
    Wszystkie następne elementy.
-   `nextUntil(selector)`  
    Wszystkie następne aż do określonego selektora (nie wliczając go).
-   `prev()`  
    Poprzedni element.
-   `prevAll()`  
    Wszystkie poprzednie elementy.
-   `prevUntil(selector)`  
    Wszystkie poprzednie aż do określonego selektora (nie wliczając go).
-   `first()`  
    Pierwszy element kolekcji.
-   `last()`  
    Ostatni element kolekcji.
-   `eq(index)`  
    Element o wskazanym indeksie (0-based).
-   `filter(selector)`  
    Filtruje elementy kolekcji wg selektora.
-   `not(selector)`  
    Zwraca elementy kolekcji, które nie pasują do selektora.

---

Można teraz tę treść wkleić do edytora Markdown, a także szybko przekonwertować do PDF lub .docx do dalszej edycji.
Jeśli chcesz, mogę pomóc w kolejnym kroku z konwersją lub przygotować plik.
