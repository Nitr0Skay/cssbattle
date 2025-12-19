```
Poniżej zamieszczę dwa Najkrótsze Golfowe podejścia do tego CSS Battle Daily:
https://cssbattle.dev/play/GsEMtYqgRk2sQ3588dPj

1.
<style>*{margin:45 105;box-shadow:inset 74q 0#08331B,inset 2in 0#1D7B47;*{margin:70 0;background:#F0CD48;scale:-1

By https://cssbattle.dev/player/levito

2.
<stYle>*{background:#f0cd48;box-shadow:inset 74Q 0#08331b,inset 9in 0#1d7b47;margin:45 105;*{margin:70 0;scale:-1

By https://cssbattle.dev/player/emohdaziz
```


Świetne golfy — oba są bardzo „cssbattle’owe”. Poniżej znajdzie się **porównanie 1 vs 2**, a potem **pełną listę technik oszczędzania bajtów**, które tu występują (jawnie lub pośrednio).

---

## 1️⃣ Porównanie obu rozwiązań

### Różnice istotne bajtowo

|Element|Wersja 1|Wersja 2|Wniosek|
|---|---|---|---|
|`background`|tylko w drugim `*{}`|w pierwszym `*{}`|**Wersja 2 lepsza** – unika powtarzania|
|Jednostka|`2in`|`9in`|neutralne (oba 2 znaki)|
|Litery|`#08331B`|`#08331b`|neutralne – CSS case-insensitive|
|Kolejność|margin → box-shadow|background → box-shadow → margin|neutralne|
|Czytelność|mniejsza|większa|nieistotne w golfie|

📌 **Wersja 2 jest minimalnie lepsza koncepcyjnie**, bo:

- ustawia `background` globalnie
    
- unika ponownego tła w zagnieżdżonym `*`
    

---

## 2️⃣ Techniki obniżania liczby bajtów (pełna lista)

### 🔹 1. Universal selector `*`

```css
*{...}
```

- 1 bajt zamiast `body`, `div`, itd.
    
- Działa na wszystko → idealne do CSSBattle
    

---

### 🔹 2. Zagnieżdżony `*{*{}}`

```css
*{...;*{...}}
```

- **Jedna para klamer mniej**
    
- Brak potrzeby kolejnego selektora
    
- Działa, bo parser CSSBattle to akceptuje
    

---

### 🔹 3. Brak jednostek przy `margin`

```css
margin:45 105
```

- CSSBattle akceptuje unitless values
    
- Oszczędzasz **2–4 bajty** na każdej wartości
    

---

### 🔹 4. Egzotyczne jednostki: `q`, `in`

```css
74q
2in
```

- `q` = ¼ mm → **krótka jednostka**
    
- `in` często daje duże przesunięcie jednym tokenem
    
- Lepsze niż `px` przy dużych wartościach
    

---

### 🔹 5. Stackowanie `inset` w `box-shadow`

```css
box-shadow:inset 74q 0#08331b,inset 9in 0#1d7b47
```

- **Jedna właściwość zamiast wielu elementów**
    
- Brak spacji przed kolorami
    
- Brak blur/spread (domyślne `0`)
    

---

### 🔹 6. Brak spacji tam, gdzie parser pozwala

```css
0#08331b
```

zamiast:

```css
0 #08331b
```

✔ legalne  
✔ oszczędza bajt za każdą spację

---

### 🔹 7. `scale:-1` zamiast transformów

```css
scale:-1
```

- Krótsze niż:
    

```css
transform:scaleX(-1)
```

- Obraca cały layout „za darmo”
    

---

### 🔹 8. Wspólne tło na najwyższym poziomie

```css
*{background:#f0cd48}
```

- Jedno tło zamiast powtarzania
    
- Dziedziczy się na wszystko
    

---

### 🔹 9. Case-insensitivity CSS

```css
<stYle>
#08331b
```

- Wielkość liter **nie ma znaczenia**
    
- Można używać najkrótszych wariantów
    

---

### 🔹 10. Brak średników na końcu

```css
scale:-1
```

- Ostatnia deklaracja **nie potrzebuje `;`**
    
- Standardowy trik golfowy
    

---

### 🔹 11. Brak zamknięcia `</style>`

- CSSBattle **nie wymaga poprawnego HTML**
    
- Każde `</style>` to **8 bajtów straty**
    

---

### 🔹 12. Użycie `background` zamiast `background-color`

```css
background:#f0cd48
```

- 10 vs 16 bajtów
    

---

## 3️⃣ Podsumowanie

Te rozwiązania wykorzystują **praktycznie pełen arsenał CSS-golfu**:

✔ jednostki niszowe  
✔ universal selector  
✔ zagnieżdżony `*`  
✔ brak spacji i średników  
✔ box-shadow jako „rysowanie”  
✔ transformacje przez `scale`  
✔ globalne tło

