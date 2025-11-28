
---

# 🎯 CSSBattle — Lista Tricków i Techniki Minimalizacji Kodu

Zbiór najczęściej stosowanych sztuczek używanych w CSSBattle — szczególnie w ekstremalnie krótkich rozwiązaniach typu _Code Golf_. Przykłady odnoszą się do challengu z 27.11.2025 r., ale techniki są uniwersalne.

---

## 1. Używanie minimalnej struktury HTML

Im krótszy kod, tym lepszy wynik, dlatego stosuje się ultrakrótkie tagi:

- `<dl>`
    
- `<p>`
    
- `<a>`
    
- `<b>`
    

oraz dowolną mieszankę wielkości liter:

```html
<stYle>
```

Przeglądarka akceptuje to bez problemu — jest to zgodne z zasadą, że HTML jest case-insensitive.

---

## 2. Globalny selektor `*`

Zamiast pisać klasy czy identyfikatory, w CSSBattle często stosuje się uniwersalny selektor:

```css
* { ... }
```

Jednym ruchem aktualizuje wszystkie elementy, co oszczędza znaki.

---

## 3. Ustawianie tła strony najkrótszym możliwym sposobem

```css
background:#3f4869
```

Kolor tła pola gry często jest ustawiany globalnie. Nie ma potrzeby tworzyć żadnych elementów.

---

## 4. Pozycjonowanie elementu przy pomocy `margin`

Zamiast `position`, `top`, `left`, transformów czy flexboxa stosuje się:

```css
margin:37.5% 50%;
```

Marginesy procentowe są nieprzewidywalne, ale w CSSBattle liczy się tylko efekt końcowy.

---

## 5. Użycie właściwości `color` nawet gdy nie ma tekstu

`color` jest krótka i dziedziczona, więc można jej użyć jako „domyślnego koloru” np. dla box-shadow.

Przykład:

```css
color:#70B7A5
```

---

## 6. Rysowanie figur poprzez `box-shadow`

To najpotężniejszy trik w CSSBattle.

Każdy cień to nowy prostokąt:

```css
box-shadow:
  52Q 0 0 26Q,
  69Q 0 0 26Q,
  239Q 0 0 1in #3f4869;
```

### Jak to działa?

Format:

```
offset-x offset-y blur spread color
```

Dzięki temu:

- można tworzyć dowolne ilości prostokątów,
    
- bez dodawania dodatkowych elementów HTML.
    

To fundament gry.

---

## 7. Użycie nietypowych jednostek: `Q`, `q`, `ch`, `in`, `vw`

Dlaczego?

Bo są **krótsze niż `px`**.

Przykłady:

- `1Q = 0.25mm`
    
- `1ch = szerokość znaku "0"`
    
- `1vw = 1% szerokości ekranu`
    
- `in` jest krótką jednostką absolutną
    

Używanie ich jest często całkowicie przypadkowe — liczy się _skrót_, nie logiczność.

---

## 8. Obrót sceny przez `rotate`

Zamiast obracać pojedyncze cienie, łatwiej obrócić cały element:

```css
rotate:90deg
```

Pozwala to uprościć pozycjonowanie.

---

## 9. Celowe niedomknięcie reguły CSS

Hack typu:

```css
*{font:0"
```

Przeglądarka automatycznie zamknie:

- cudzysłów
    
- selektor
    
- blok CSS
    

Pozwala to obciąć końcówkę kodu o kilka znaków.

---

## 10. Wykorzystywanie elastyczności (i błędów) parsera CSS

Przeglądarka:

- domyka brakujące nawiasy,
    
- ignoruje błędne linie,
    
- akceptuje mieszany case,
    
- wybacza brak `;` na końcu.
    

W CSSBattle jest to wykorzystywane do ekstremum.

---

## 11. Brak troski o semantykę

Wyzwanie dotyczy jedynie **odtworzenia obrazka**.  
Dlatego:

- HTML bywa „śmieciowy”,
    
- CSS jest „łamany”, ale działający,
    
- liczy się tylko efekt wizualny i liczba znaków.
    

---

## 12. Cała grafika na jednym elemencie

Najbardziej „golfowe” podejście:

- jeden element HTML,
    
- jeden selektor CSS,
    
- jedna reguła `box-shadow` generująca 5–20 prostokątów.
    

To często najbardziej punktowane podejście.

---

# 📌 Podsumowanie

Te triki to podstawowy arsenał każdego gracza CSSBattle, który celuje w **najkrótsze możliwe rozwiązania**. Wszystkie bazują na:

- manipulacji parserem,
    
- ekstremalnym skracaniu składni,
    
- nadużywaniu `box-shadow`,
    
- wykorzystywaniu nietypowych jednostek,
    
- minimalnej liczbie elementów.
    

---

