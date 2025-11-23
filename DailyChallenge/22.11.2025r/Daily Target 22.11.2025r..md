
```
<div id="leftCircle"></div>
<p id="1"></p>
<p id="2"></p>
<p id="3"></p>
<div id="rightCircle"></div>
<style>
  body {
    background-color: #328FC1;
  }
  div {
    width: 222px;
    height: 222px;
    background: #328FC1;
    position: absolute;
    left: -144px;
    border-radius: 50%;
    border: 31px #F5D6B4 solid
  }
  #rightCircle {
    left: 288px; 
  }
  p {
    background-color: #F5D6B4;
    position: absolute;
    z-index: -1;
    width: 500px;
    height: 30px;
    top: 54px;
  }
  #2 {
    height: 60px;
    top: 108px;
   left: 0;
  }
</style>

<!-- OBJECTIVE -->
<!-- Write HTML/CSS in this editor and replicate the given target image in the least code possible. What you write here, renders as it is -->

<!-- SCORING -->
<!-- The score is calculated based on the number of characters you use (this comment included :P) and how close you replicate the image. Read the FAQS (https://cssbattle.dev/faqs) for more info. -->

<!-- IMPORTANT: remove the comments before submitting -->
```

Problem wynika z tego, że **ID nie może zaczynać się od cyfry**, jeśli chcesz go używać jako selektora CSS w normalnej postaci (`#2`).

HTML _technicznie pozwala_ na `id="2"`, ale **CSS traktuje takie identyfikatory jako nieprawidłowe**, dopóki nie zapiszesz ich w formie „ucieczonej”.

### Dlaczego #2 nie działa?

W CSS identyfikatory zaczynające się od cyfry muszą być **escapowane**, bo parser traktuje je jak liczby.

Dlatego `#2` jest niepoprawne, ale możesz napisać:

```css
#\32 {
  height: 60px;
  top: 108px;
  left: 0;
}
```

`32` to kod ASCII znaku `2`, a przed nim musi być spacja albo inny delimiter — CSS tego wymaga.

### Możesz to zapisać też tak:

```css
#\000032 {
  ...
}
```

### Najprostsze rozwiązanie

Po prostu **zmień ID tak, by nie zaczynało się od cyfry**, np.:

```html
<p id="p2">test</p>
```

I wtedy:

```css
#p2 { ... }
```

To najbardziej praktyczne, zwłaszcza poza środowiskiem typu CSSBattle.

---

W CSSBattle używanie cyfr jako `id` jest totalnie normalne — wszyscy tam robią takie rzeczy, bo **liczy się każdy znak**, a numerki są najkrótsze.  
Ale w normalnym kodzie… nope 😄

---

## 🔧 Co byś zrobił w realnym projekcie?

Masz trzy poziome paski — to **nie są semantyczne elementy tekstowe**, więc nie powinny być `<p>`.

Najbardziej „realne” opcje:

### 1) **Klasy** (najpopularniejsze)

```html
<div class="bar"></div>
<div class="bar bar--big"></div>
<div class="bar"></div>
```

I CSS:

```css
.bar { … }
.bar--big { … }
```

Skalowalne, czytelne, semantyczne.

---

### 2) **Role lub nazwy opisowe**

```html
<div id="top-bar"></div>
<div id="middle-bar"></div>
<div id="bottom-bar"></div>
```

Takie ID nikomu nie zrobią krzywdy.

---

### 3) **Użycie jednego elementu z :before / :after**

Często trzy paski to „hamburger menu”, wtedy robisz tylko jeden element:

```html
<div class="hamburger"></div>
```

```css
.hamburger,
.hamburger::before,
.hamburger::after {
  /* wspólne style */
}

.hamburger::before { top: -8px; }
.hamburger::after  { top: 8px; }
```

---

## 🔧 A w CSSBattle?

Zostaw cyfry — to normalne.

Tylko pamiętaj:

- W HTML możesz dać `id="2"`
    
- W CSS musisz pisać `#\32`
    

Większość top rozwiązujących po prostu **omija ID** i robi tak:

```html
<div></div><div></div><div></div>
```

I styluje po:

- `div`
    
- `div+div`
    
- `div+div+div`
    
- `:nth-child(2)`
    
- `:nth-child(3)`
    

To najkrótsze na battle.

---

