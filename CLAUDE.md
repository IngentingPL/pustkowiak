# CLAUDE.md — Pustkowiak

## Co to jest
Interaktywny poradnik do Fallout 4 w stylu Pip-Boya.
Hostowany na GitHub Pages: https://ingentingpl.github.io/pustkowiak/

## Struktura projektu
```
pustkowiak/
├── fallout4-kolonie.html   # Poradnik do kolonii
├── frakcje.html            # Poradnik do frakcji
├── kompani.html            # Poradnik do kompanów
├── CLAUDE.md               # Ten plik
└── design.md               # System wizualny
```

## Zasady pracy z kodem

### Zawsze przed zmianami
- Przeczytaj plik który edytujesz (`read`)
- Nie zmieniaj struktury HTML jeśli nie jest to wymagane
- Nie dodawaj zewnętrznych bibliotek JS

### Jeden plik = wszystko
Cały projekt to jeden plik HTML. CSS i JS są wewnątrz `<style>` i `<script>`.
Nie rozdzielaj na osobne pliki.

### Zakładki — jak działają
Każda zakładka to:
1. Przycisk `<button>` w `<nav>` z `onclick="show('id', this)"`
2. Sekcja `<div class="section" id="id">` w `.content`

Dodając nową zakładkę — dodaj oba elementy.

### Polskie znaki
Plik musi mieć `<meta charset="UTF-8">` — jest już ustawiony. Pisz polskie znaki bezpośrednio (ą, ę, ó itd.), nie używaj encji HTML.

### Responsywność
- Telefon: `max-width: 600px`
- Tablet: `max-width: 900px`
- Desktop: `min-width: 900px`
Media queries na końcu sekcji `<style>`.

## Czego nie robić
- Nie usuwaj efektu CRT (pseudoelementy `::before` i `::after` na `.pipboy`)
- Nie zmieniaj zmiennych CSS w `:root` bez potrzeby
- Nie dodawaj animacji innych niż `blink`
- Nie zmieniaj funkcji `show()` w JavaScript
