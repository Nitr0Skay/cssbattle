
```
<style>*{color:492D01;margin:150 215 45 155;box-shadow:inset 1in 0,0 0 0 38em#F3AC3C,-96q 0,-45vw 0 0 32q;*{margin:-45-150 60 90;border-radius:1in;font:5%a
```
By https://cssbattle.dev/player/underdude

To rozwiązanie jest **typowym “high-level CSSBattle golfem”**, czyli ekstremalnie skróconym i sprytnym CSS-em, który **wykorzystuje luki w parserze CSS, nietypowe jednostki i side-effecty renderowania** 😄  
Poniżej rozkładam je na czynniki pierwsze.

---

## 1️⃣ Jednoelementowa konstrukcja (`*`)

```css
*{ ... *{ ... }
```

**Cały obrazek jest zrobiony jednym selektorem `*`**, bez HTML-a i bez pseudo-elementów.

Cechy:

- brak `<div>`ów
    
- brak `::before / ::after`
    
- wszystko rysowane **box-shadowami i marginami**
    

To jest **święty Graal CSSBattle** – im mniej elementów, tym mniej bajtów.

---

## 2️⃣ Brak jednostek w `margin`

```css
margin:150 215 45 155;
```

➡️ CSSBattle **akceptuje wartości bez jednostek** i interpretuje je jako `px`.

Normalny CSS → błąd  
CSSBattle → ✔️ działa

To pozwala:

- oszczędzić bajty (`px` = 2 znaki mniej × 4)
    
- szybciej “rzeźbić” pozycję
    

---

## 3️⃣ Kolor bez `#`

```css
color:492D01
```

To **nie jest poprawny CSS**, ale:

- parser CSSBattle **dopuszcza heksy bez `#`**
    
- `color` jest używany później jako **domyślny kolor cieni**
    

➡️ Jedna deklaracja koloru = wiele zastosowań

---

## 4️⃣ `box-shadow` jako narzędzie rysunkowe 🎨

```css
box-shadow:
 inset 1in 0,
 0 0 0 38em #F3AC3C,
 -96q 0,
 -45vw 0 0 32q;
```

To serce rozwiązania.

### Techniki:

- **wiele cieni = wiele kształtów**
    
- `inset` → wypełnianie wnętrza
    
- ogromne `spread-radius` → “malowanie tła”
    
- brak blur → ostre krawędzie
    

---

## 5️⃣ Egzotyczne jednostki: `in`, `em`, `vw`, `q`

```css
1in
38em
-45vw
-96q
```

### Dlaczego?

- `q` = **¼ mm** (prawie nikt tego nie używa)
    
- daje **precyzyjne przesunięcia za małą liczbę znaków**
    
- `vw` pozwala **rozciągnąć cień poza viewport**
    

➡️ Maksimum efektu przy minimum kodu

---

## 6️⃣ Zagnieżdżony `*{}` = drugi “element”

```css
*{
  ...
  *{
    margin:-45-150 60 90;
    border-radius:1in;
    font:5%a
```

To **hack parsera CSSBattle**:

- wewnętrzny `*{}` jest traktowany jak osobny blok stylów
    
- pozwala **zmienić styl w trakcie renderowania**
    
- symuluje drugi element bez HTML
    

---

## 7️⃣ Ujemne marginesy jako pozycjonowanie

```css
margin:-45-150 60 90;
```

- brak spacji = parser nadal ogarnia
    
- ujemne wartości = przesuwanie “bryły”
    
- zero `position:absolute`
    

---

## 8️⃣ `border-radius:1in`

- ogromny promień
    
- zawsze “okrągło”
    
- krótsze niż `999px`
    

---

## 9️⃣ `font:5%a` — klasyczny CSSBattle glitch 😈

```css
font:5%a
```

To:

- **niepoprawna składnia**
    
- ale powoduje:
    
    - ustawienie `font-size`
        
    - czasem wymuszenie renderu tekstu jako bloku
        
    - wpływ na box-model
        

➡️ Używane **tylko dla side-effectów**, nie dla fontów

---

## 🔥 Podsumowanie cech charakterystycznych

✔️ One-element solution  
✔️ Zero HTML  
✔️ Box-shadow art  
✔️ Parser exploits  
✔️ Egzotyczne jednostki (`q`, `in`)  
✔️ Brak `px`, brak `#`, brak spacji  
✔️ Maksymalna kompresja bajtów

To jest **rozwiązanie typowo podium-owe**, pisane bardziej _pod parser CSSBattle_ niż pod przeglądarkę.

