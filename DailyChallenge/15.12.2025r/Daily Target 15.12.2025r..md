
```
<style>*{background:#0b2429;border:32Q solid#ce6f4a;margin:-60 80 9%0;border-radius:5vw}&{border-width:30 0 120;margin:80 90
```
By  https://cssbattle.dev/player/eguiluz

Oraz:

```
<stYle>*{border:32Q solid#ce6f4a;border-radius:21Q}&{border-width:30 0 120;margin:80 90;*{background:#0b2429;margin:-60 80 9%0
```
By  https://cssbattle.dev/player/emohdaziz


Są to **bardzo typowe „cssbattle’owe” potworki**, więc fajny przykład do analizy 🙂  
Poniżej **porównanie obu rozwiązań + listę sztuczek**, które zostały użyte.

---

## 1️⃣ Kod pierwszy

```css
<style>
*{
  background:#0b2429;
  border:32Q solid #ce6f4a;
  margin:-60 80 9% 0;
  border-radius:5vw
}
&{
  border-width:30 0 120;
  margin:80 90
}
```

### Co tu się dzieje?

#### 🔹 Uniwersalny selektor `*`

- Styluje **wszystko**, w tym `html` i `body`
    
- Brak znaczników = mniej bajtów
    

#### 🔹 Jednostka `Q`

- `1Q = 0.25mm`
    
- Krótsza niż `px`
    
- Popularna w CSS Battle do borderów
    

#### 🔹 Border jako kształt

- `border:32Q solid #ce6f4a`  
    → faktyczny „rysunek” to **obramowanie**, nie element
    

#### 🔹 Ujemne marginesy

```css
margin:-60 80 9% 0;
```

- Pozwalają **wyciągnąć element poza viewport**
    
- `%` w pionie liczone od **szerokości**, nie wysokości (ważny trick)
    

#### 🔹 `border-radius` w `vw`

- Skaluje się względem szerokości ekranu
    
- Daje „organiczny” kształt przy małej liczbie znaków
    

#### 🔹 Selector `&`

- **Niepoprawny CSS**
    
- Browser go ignoruje, ale CSS Battle parser **łyka go**
    
- Pozwala dodać _drugą warstwę stylów_ bez nowego selektora
    

---

## 2️⃣ Kod drugi

```css
<stYle>
*{
  border:32Q solid #ce6f4a;
  border-radius:21Q
}
&{
  border-width:30 0 120;
  margin:80 90;
  *{
    background:#0b2429;
    margin:-60 80 9%0
```

### Co tu się dzieje?

Ten kod jest **jeszcze bardziej agresywny bajtowo**.

#### 🔹 Mieszanie wielkości liter

```html
<stYle>
```

- HTML jest case-insensitive
    
- Pozwala ominąć filtry / skrócić zapis w niektórych przypadkach
    

#### 🔹 Brak zamknięć

- Brak `}` i `</style>`
    
- Browser **domyślnie domyka**
    
- CSS Battle to toleruje → oszczędność znaków
    

#### 🔹 Zagnieżdżony `*` (nielegalny CSS)

```css
&{
  ...
  *{
    background:#0b2429;
```

- Formalnie **nieważne**
    
- Parser CSS Battle interpretuje to jako kolejny globalny styl
    
- Bardzo „dirty trick”, ale skuteczny
    

#### 🔹 Przeniesienie `background` do środka

- Tło ustawiane **później**, nadpisuje wcześniejsze
    
- Pozwala skrócić deklaracje
    

---

## 🧠 Wspólne sztuczki (najważniejsze)

### ✅ 1. Rysowanie przez `border`

- Element jest tylko „nośnikiem”
    
- Faktyczny kształt = obramowanie
    

### ✅ 2. Jednostka `Q`

- Krótka
    
- Idealna do precyzyjnych borderów
    

### ✅ 3. Uniwersalny selektor `*`

- Zero HTML
    
- Maksymalna oszczędność bajtów
    

### ✅ 4. Ujemne marginesy

- Kontrola pozycji bez `position`
    
- Częsty trick topowych wyników
    

### ✅ 5. Ignorowanie poprawności CSS

- `&`
    
- brak zamknięć
    
- pseudo-zagnieżdżenia  
    ➡️ **CSS Battle ≠ prawdziwy CSS**
    

---

## ⚖️ Porównanie

|Cecha|Rozwiązanie 1|Rozwiązanie 2|
|---|---|---|
|Czytelność|❌ niska|❌❌ bardzo niska|
|Agresywność|⭐⭐⭐|⭐⭐⭐⭐|
|Ilość hacków|średnia|ekstremalna|
|Odporność na parser|większa|mniejsza|
|Styl „pro”|✔️|✔️✔️|

👉 **Drugie rozwiązanie** jest bardziej „battle-hardcore”  
👉 **Pierwsze** jest minimalnie „bezpieczniejsze”

---

## 🏁 Podsumowanie

Oba rozwiązania pokazują klasyczny styl topowych graczy CSS Battle:

- zero HTML
    
- border zamiast boxów
    
- nadużywanie parsera
    
- kreatywne jednostki
    
- świadome łamanie specyfikacji
    

