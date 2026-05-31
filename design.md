# design.md — System wizualny Pustkowiak

## Klimat
Pip-Boy 3000 z Fallout 4. Retro terminal, zielony monochromatyczny ekran CRT.

## Kolory (zmienne CSS)

```css
--green:      #5eff6a   /* główny kolor — tekst, akcenty */
--green-dim:  #2a7a30   /* drugi plan — ramki, przyciski nieaktywne */
--green-dark: #0d1f0f   /* tło elementów */
--amber:      #f5b942   /* ostrzeżenia */
--red:        #ff4f4f   /* błędy, niebezpieczeństwo */
--bg:         #0a1a0b   /* tło całej strony */
```

## Czcionki

```css
'VT323'          /* nagłówki, nawigacja, logo — styl retro terminal */
'Share Tech Mono' /* treść — czytelny monospace */
```
Importowane z Google Fonts — nie zmieniaj.

## Komponenty

### Tip box (zielony) — informacja
```html
<div class="tip-box">
  <span class="label">TYTUŁ</span>
  Treść wiadomości.
</div>
```

### Tip box ostrzegawczy (żółty)
```html
<div class="tip-box warn">
  <span class="label">TYTUŁ</span>
  Treść ostrzeżenia.
</div>
```

### Tip box niebezpieczeństwo (czerwony)
```html
<div class="tip-box danger">
  <span class="label">TYTUŁ</span>
  Treść.
</div>
```

### Lista punktowana
```html
<ul class="checklist">
  <li>Element listy</li>
</ul>
```
Marker: `>` w kolorze `--green`.

### Lista numerowana
```html
<ol class="priority-list">
  <li>Element</li>
</ol>
```
Format: `[1]`, `[2]` itd.

### Siatka zasobów
```html
<div class="resource-grid">
  <div class="res-card">
    <div class="res-name">NAZWA</div>
    <div class="res-formula">Szczegóły</div>
  </div>
</div>
```
Domyślnie 2 kolumny. Na tablet i desktop 4 kolumny (media query).

## Efekty CRT

Pseudoelementy na `.pipboy`:
- `::before` — poziome linie skanowania (scanlines)
- `::after` — winietowanie (ciemniejsze rogi)

Oba mają `pointer-events: none` i `z-index: 10/11` — nie kolidują z treścią.

## Animacje

Tylko jedna animacja: `blink` (migający kursor).
```css
@keyframes blink { 50% { opacity: 0; } }
```

## Breakpointy responsywne

| Zakres | Klasa | Opis |
|--------|-------|------|
| max 600px | Mobile | Układ pionowy, nav poziome |
| 601px–1024px | Tablet | Szerokość 860px, 4 kolumny grid |
| 1025px+ | Desktop | Układ dwukolumnowy, nav pionowe |

## Układ strony

### Mobile (do 600px)
```
.pipboy
├── header          (logo + podtytuł)
├── .stat-bar       (wersja, region, status)
├── nav             (zakładki — poziome)
└── .content        (aktywna sekcja)
    └── .section    (jedna na zakładkę)
footer
```

### Tablet (601px–1024px)
- `.pipboy`: max-width: 860px
- `.resource-grid`: 4 kolumny zamiast 2
- `nav button`: font-size: 1.2rem

### Desktop (1025px+) — układ dwukolumnowy
```
.pipboy
├── header
├── .stat-bar
└── .pipboy-body (display: flex)
    ├── .pipboy-nav (width: 200px, flex-shrink: 0)
    │   └── nav (flex-direction: column)
    │       └── button (text-align: left)
    └── .pipboy-main (flex: 1)
        └── .content
            └── .section
footer
```

Style dla desktop:
- `.pipboy`: max-width: 1400px, width: 95vw
- `.pipboy-nav`: border-right zamiast border-bottom
- `nav button`: text-align: left, padding: 14px 20px
- `.pip-logo`: font-size: 3rem
- `h2`: font-size: 2rem
- `.tip-box`: font-size: 0.9rem
