# Analiza 7 rozwiązań CSSBattle (Daily Challenge -- 27.11.2025)

Poniżej znajduje się kompletna, techniczna analiza siedmiu golfowych
rozwiązań CSSBattle. Każde rozwiązanie jest rozbite na: - strukturę, -
kluczowe hacki, - wyjaśnienie, dlaczego działa, - rolę każdego fragmentu
kodu.

------------------------------------------------------------------------

# 📌 Wspólne fundamenty

## `*{ ... }`

Styluje każdy element na stronie.

## `* *{ ... }`

To selektor *potomek dowolnego elementu dowolnego elementu* -- czyli: -
styluje elementy zagnieżdżone **co najmniej dwa poziomy** głębokości, -
jest tańsze niż np. `div div`.

## `border-image: conic-gradient(...)`

Najważniejszy hack tych rozwiązań: - border-image nakłada gradient jako
grafikę granicy, - `conic-gradient` tworzy sektory (jak tort), - każda
krawędź (top/right/bottom/left) dostaje slice proporcjonalny do schematu
`/30%30%30%60%`, - efekt: **krawędzie stają się poziomymi lub pionowymi
blokami**, które renderują się jako cegły.

## `scale:-1`

Odbicie całości: - zamiast duplikować elementy, wystarczy jeden element
z odbiciem, - pozwala wykorzystać border-image tak, by tworzył „drugi
rząd" cegieł.

## Marginesy jako pozycjonowanie

Marginesy typu:

    margin:85 25%15
    margin:-70 0 70
    margin:70 0 -140

Manipulują: - przesunięciem warstw, - nakładaniem się granic, -
przesunięciem pozycji gradientu na border-image.

## Brak jednostek = px

W CSSBattle wolno pisać:

    margin:85
    height:60
    border-width:120

Bo przeglądarka automatycznie dodaje `px`.

------------------------------------------------------------------------

# 🔥 1. ROZWIĄZANIE NR 1

    <STYLE>*{margin:85 25%15;*{background:#D512;margin:-70 0 70;scale:-1}border-image:120/30%30%30%60%conic-gradient(#BE6565

## Struktura

-   Globalny selektor ustawia marginesy i border-image.
-   `*{... *{...} ...}` definiuje dodatkowy wewnętrzny blok dla
    potomków.

## Mechanika

1.  `margin:85 25%15`\
    Ustawia ciasne pola wokół elementów, wymuszając proporcje cegieł.

2.  `border-image:120/30%30%30%60%conic-gradient(#BE6565)`\
    Generuje ceglane bloki po bokach elementu.

3.  Wewnętrzne `*{background:#D512;margin:-70 0 70;scale:-1}`

    -   tło czerwone,
    -   margin ujemny przesuwa cegły pionowo,
    -   scale odbija układ i podwaja „rząd".

------------------------------------------------------------------------

# 🔥 2. ROZWIĄZANIE NR 2

    <style>*{margin:85+25%;border-image:conic-gradient(#BE6565)50%/30%30%30%60%/0 0 74q;*{margin:0;scale:-1;background:#d412

## Kluczowy hack

`85+25%` działa, bo parser CSSBattle traktuje `85+25%` jako niepoprawną
wartość...\
...ale ją akceptuje i w praktyce ustawia 85px oraz ignoruje `+25%`.

To tzw. **broken parser trick**.

## `74q`

Jednostka `q` = ćwierć milimetra → ekstremalnie krótka w zapisie.\
Tutaj użyta do manipulacji border-image width.

------------------------------------------------------------------------

# 🔥 3. ROZWIĄZANIE NR 3

    <stYle>*{margin:15 25%155;*{background:#d412;margin:70 0-140;scale:-1}border-image:100/30%60%30%30%conic-gradient(#be6565

## Najważniejsze różnice

-   Duży bottom margin: `155` → odsunięcie dolnych cegieł.
-   Niestandardowa kolejność slice: `30%60%30%30%` daje inne proporcje.

## `margin:70 0 -140`

Ten ujemny bottom tworzy efekt „podciągnięcia" bloków.

------------------------------------------------------------------------

# 🔥 4. ROZWIĄZANIE NR 4

    <style>*{margin:15 25%155;border-image:conic-gradient(#BE6565)50%/30%60%30%30%;*{background:#D412;scale:-1;margin:70 0-140

To samo co (3), tylko odwrócona kolejność deklaracji: - najpierw
border-image, - potem \*{...} potomków.

Parser CSS pozwala na takie układy bez średników --- mimo że formalnie
są błędne.

------------------------------------------------------------------------

# 🔥 5. ROZWIĄZANIE NR 5

    <hr><p><hr><p><style>&{background:#D412;* *{height:60;margin:15 92-5;border:solid#BE6565;border-width:0 120 0 60}p{scale:-1

Najdziwniejsze i najbardziej kreatywne.

## Hacki:

-   Tworzy **4 elementy `<hr>` i `<p>`**, które mają domyślne rozmiary →
    stos cegieł.

-   `&{background:#D412}`\
    W CSSBattle `&` działa jak `*`.

-   `* *{height:60;margin:15 92-5;border:solid#BE6565;border-width:0 120 0 60}`\
    Zewnętrzny border tworzy cegły.

## `p{scale:-1}`

Odbija drugi zestaw cegieł, tworząc pełną strukturę.

------------------------------------------------------------------------

# 🔥 6. ROZWIĄZANIE NR 6

    <style>*{margin:85 25%15;border-image:conic-gradient(#BE6565)50%/30%30%30%60%;*{background:#FAE7DF;margin:-70 0 70;scale:-1

Tu: - border-image = cegły (#BE6565), - tło cegieł = #FAE7DF (kolor tła
sceny), - marginesy przesuwają cegły wewnętrzne.

To klasyczny układ: border-image = cegły, child background = tło.

------------------------------------------------------------------------

# 🔥 7. ROZWIĄZANIE NR 7

    <style>*{margin:85 25%15;border-image:conic-gradient(#BE6565)50%/30%30%30%60%;*{background:#FAE7DF;margin:-35%0 70;scale:-1

Różnica z Nr 6:

`margin:-35%0 70`

-   zamiast `-70` użyto procentu,
-   przesunięcie dynamicznie zależne od szerokości viewportu,
-   w CSSBattle viewport = 400px → 35% = 140px,
-   dokładnie tyle, ile potrzeba do wyrównania cegieł.

------------------------------------------------------------------------

# ✔ PODSUMOWANIE

Wszystkie 7 rozwiązań opierają się na:

1.  **border-image z conic-gradient** jako generator cegieł,
2.  **marginesach** sterujących położeniem,
3.  **scale:-1** do podwojenia układu,
4.  \*\*\* \*{...}\*\* do stylowania potomków,
5.  **skracaniu wszystkiego**:
    -   brak jednostek,
    -   brak średników,
    -   brak zamykających tagów,
    -   zagnieżdżanie `*{ *{ ... } }`,
6.  **nadużyciach parsera CSSBattle**:
    -   `85+25%`,
    -   brak średników,
    -   & jako selektor globalny.

------------------------------------------------------------------------
