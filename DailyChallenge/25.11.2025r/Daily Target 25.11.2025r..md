
## Pytanie brzmi:  div::after lub div::before - dlaczego są one elementami Inline, mimo iż block typu div jest elementem blokowym ??


Dobre pytanie! Rzeczywiście, to może być trochę mylące, bo choć `div` jest elementem blokowym, pseudoelementy takie jak `::after` i `::before` są domyślnie traktowane jako elementy **inline**.

### Wyjaśnienie:

Pseudoelementy `::before` i `::after` są tworzone przez CSS w celu dodania zawartości przed lub po danym elemencie, ale nie są to pełnoprawne "dzieci" w tradycyjnym sensie. Mają one pewne cechy, które różnią się od standardowych elementów HTML, w tym domyślny **typ wyświetlania**.

Domyślnie, pseudoelementy są traktowane jak elementy **inline**, a nie blokowe, co oznacza, że zachowują się jak np. elementy `<span>`. W rezultacie:

- Pseudoelementy **nie zajmują całej szerokości dostępnego miejsca** (jak elementy blokowe),
    
- Pseudoelementy **nie zaczynają nowej linii** (jak elementy blokowe),
    
- Pseudoelementy **mogą być umieszczane obok innych elementów inline**, co jest charakterystyczne dla elementów inline.
    

To, że `div` jest blokowym elementem, nie ma wpływu na to, jak będą się zachowywać pseudoelementy, ponieważ pseudoelementy są traktowane jako odrębne jednostki, niezależnie od typu elementu, do którego się odnoszą.

### Dlaczego pseudoelementy są domyślnie `inline`?

Decyzja o tym, że pseudoelementy domyślnie mają `display: inline`, wynika z tego, jak zostały zaprojektowane w CSS. Chciano, aby były one małymi, lekkimi dodatkami do zawartości, które nie zmieniają układu całej strony, ale jedynie "uatrakcyjniają" ją, na przykład dodając ikony, teksty lub dekoracje.

### Jak zmienić to zachowanie?

Jeśli chcesz, żeby pseudoelementy `::before` i `::after` zachowywały się jak elementy blokowe, możesz jawnie ustawić dla nich `display: block` lub `display: inline-block`, w zależności od potrzeb.

Przykład:

```css
div::before {
  content: "Przykład: ";
  display: block; /* Teraz będzie elementem blokowym */
}
```

Jeśli ustawisz `display: block`, pseudoelement będzie traktowany jak blokowy element, co oznacza, że zacznie nową linię i zajmie pełną szerokość dostępnego miejsca (tak jak typowy element blokowy). Alternatywnie, `display: inline-block` sprawi, że pseudoelement będzie miał cechy zarówno elementu inline, jak i blokowego.

### Podsumowanie:

- **Dlaczego `::before` i `::after` są `inline`?** Pseudoelementy są domyślnie traktowane jak elementy inline, ponieważ zostały zaprojektowane do lekkich dekoracji i dodatków w obrębie innych elementów.
    
- **Czy to można zmienić?** Tak, możesz zmienić typ wyświetlania pseudoelementów, używając `display: block`, `display: inline-block` lub innych wartości `display`, w zależności od tego, jak chcesz, aby pseudoelementy się zachowywały.
    

To dość ważny szczegół, gdy próbujesz manipulować układem i stylem tych pseudoelementów.