# Brand & Designguide — Tegnefurs Matte
> Levande dokument för Patrick Tegnefurs undervisningsplattform  
> Senast uppdaterad: 2026-09-08

---

## 1. Vision & syfte

En öppen, välkomnande matematiksajt för elever i årskurs 7–9 på Alfred Dalinskolan i Huskvarna. Sajten kombinerar:

- **Strukturerat innehåll** per arbetsområde och moment
- **Interaktiva simuleringar** och visuella stöd eleven kan utforska
- **Videogenomgångar** och förklaringar i text
- **Scaffolding** som successivt bygger förståelse
- **Spaced repetition** och interleaving inbyggt i upplägget

Inspirerat av [vidma.se](https://www.vidma.se) och [mrbartonmaths.com](https://www.mrbartonmaths.com) — men helt eget.

---

## 2. Designsystem — PT Ljus

### 2.1 Färgpalett

```css
/* Bakgrund & ytor */
--bg:        #f6f4ff;   /* Sidans bakgrund */
--surface:   #ffffff;   /* Kort, moduler */
--surface2:  #eae6ff;   /* Sekundär yta, badges, hover-states */
--border:    #ccc5f0;   /* Kanter, avgränsare */

/* Text */
--text:      #100e28;   /* Primärtext */
--muted:     #585078;   /* Sekundärtext, etiketter, metadata */

/* Accent */
--accent:    #306BF0;   /* Primär CTA, länkar, aktiva element */
--accent2:   #EC6095;   /* Highlight, badges, gamification */

/* Signaturgradienten — navbar, logotyp, accentelement */
--gradient:  linear-gradient(120deg, #66C7C2 0%, #F4A261 50%, #EC6095 100%);

/* Årskursfärger */
--ak7:       #66C7C2;   /* Teal/mint — Åk 7 */
--ak8:       #F4A261;   /* Orange/amber — Åk 8 */
--ak9:       #EC6095;   /* Pink/ros — Åk 9 */

/* Feedback */
--correct:   #18a348;
--wrong:     #e02020;

/* Skugga */
--shadow:    rgba(48, 107, 240, 0.12);
```

> **Navbar-regel:** `header`/topbar använder **alltid** `--gradient` som bakgrund på samtliga sidor. Text och ikoner i navbaren är alltid `#ffffff`. Detta är den visuella röda tråden som binder ihop hela sajten.

> **Årskursfärger:** Åk 7 = `#66C7C2` (teal), Åk 8 = `#F4A261` (orange), Åk 9 = `#EC6095` (rosa). Dessa färger används konsekvent i årskurskort, badges, tidslinjepunkter och progressbars.

> **Övrig regel:** Alla färger skrivs ut explicit i varje fil. Lita aldrig på webbläsarens/OS-temaarv.

### 2.2 Typografi

| Roll | Typsnitt | Användning |
|------|----------|------------|
| **Display / Storrubriker** | Montserrat | H1, logotyp — de stora, karaktärsfulla rubrikerna |
| **Komponentrubriker** | Montserrat | Kortrubriker, momentrubriker, grade-titles, numrering (G1, G2…) |
| **Brödtext / UI** | Sora | All övrig text, knappar, etiketter, metadata |

```css
/* Import */
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&family=Playfair+Display:ital,wght@0,600;0,700;1,600&family=Sora:wght@400;500;600&display=swap');

font-family: 'Sora', sans-serif;          /* body, UI */
font-family: 'Montserrat', sans-serif;   /* h1, logotyp */
font-family: 'Montserrat', sans-serif;    /* kortrubriker, momentrubriker, grade-titles */
```

### 2.3 Skuggor & radier

```css
--radius-sm:  8px;
--radius-md:  14px;
--radius-lg:  20px;
--radius-xl:  28px;

--shadow-sm:  0 2px 8px var(--shadow);
--shadow-md:  0 4px 20px var(--shadow);
--shadow-lg:  0 8px 40px var(--shadow);
```

### 2.4 Spacing (8px-grid)

Använd multiplar av 8px: `8 / 16 / 24 / 32 / 48 / 64 / 96px`

---

## 3. Informationsarkitektur

### Hierarki

```
Landningssida (index.html)
├── Årskurskort (Åk 7, Åk 8, Åk 9)  ← länk filtrerar arbetsområdessidan via ?ak=N
└── Arbetsområde (t.ex. Geometri)
    └── Momentsida med flikar
        ├── Startuppgift / Förförståelsetest
        ├── Introduktion
        ├── Lärarledda genomgångar (video)
        ├── Interaktiva övningar (med scaffolding)
        └── Fördjupning / Repetition
```

### Arbetsområden

| Slug | Titel | Åk |
|------|-------|-----|
| `taluppfattning` | Taluppfattning & tals användning | 7, 8 |
| `procent` | Procent | 8, 9 |
| `algebra` | Algebra | 7, 8, 9 |
| `geometri` | Geometri | 7, 8, 9 |
| `funk` | Samband & förändring | 8, 9 |
| `statistik` | Statistik & dataanalys | 7, 8, 9 |
| `sannolikhet` | Sannolikhet & kombinatorik | 7, 8, 9 |

### Taggstruktur

Varje arbetsområde märks med:
- **Årskurs:** `ak7` `ak8` `ak9`
- **Typ:** `interaktivt` `video` `övning` `test`

---

## 4. Komponentbibliotek

### 4.1 Navbar / Header

```css
header {
  background: linear-gradient(120deg, #66C7C2 0%, #F4A261 50%, #EC6095 100%);
  height: 64px;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 4px 24px rgba(0,0,0,0.18);
}
/* Logotyp och navknappar alltid #ffffff / rgba(255,255,255,0.85) */
```

### 4.2 Årskurskort (GradeCard) — landningssidan

Tre kort sida vid sida överst på `index.html`. Varje kort:
- Gradient-bakgrund baserad på årskursfärg
- Stort halvtransparent sifferdekorelement (bakgrund)
- Lista med klickbara ämnen för just den årskursen
- Länk skickar med `?ak=N` i URL för filtrering

```css
/* Åk 7 */
.grade-card.ak7 { background: linear-gradient(145deg, #3aada8 0%, #66C7C2 100%); }
/* Åk 8 */
.grade-card.ak8 { background: linear-gradient(145deg, #d4813a 0%, #F4A261 100%); }
/* Åk 9 */
.grade-card.ak9 { background: linear-gradient(145deg, #c43d75 0%, #EC6095 100%); }
```

Innehåll per kort:
- **Åk 7:** Taluppfattning, Algebra, Geometri, Statistik, Sannolikhet
- **Åk 8:** Taluppfattning, Procent, Algebra, Geometri, Samband & förändring, Statistik
- **Åk 9:** Algebra, Geometri, Samband & förändring, Sannolikhet & kombinatorik, Statistik

### 4.3 Arbetsområdeskort (AreaCard) — landningssidan

Används under årskurskorten. Innehåller:
- Färgad topstripe per arbetsområde
- Ikon, titel (Playfair Display), kortbeskrivning (Sora, muted)
- Badges för årskurs med rätt färg
- Progressbar
- CTA-länk

```css
.area-card {
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: var(--radius-lg);
  box-shadow: 0 2px 12px var(--shadow);
  padding: 24px;
  transition: box-shadow 0.2s, transform 0.2s;
}
.area-card:hover {
  box-shadow: 0 6px 28px var(--shadow);
  transform: translateY(-3px);
  border-color: var(--accent);
}
```

### 4.4 Arbetsområdessida — layout

Två-kolumns layout: `280px sidebar | 1fr content`

**Sidebar (sticky):**
- Tidslinje per årskurs med kollapsibara sektioner
- Varje moment = numrerad punkt längs en vertikal linje
- Punktens färg följer årskursfärgen
- Klick scrollar smidigt till momentet i huvudinnehållet

**Innehåll:**
- Grade-block per årskurs med rubrik + badge
- Momentkort: numrering (G1, G2…), titel, beskrivning, progressbar, status-pill, estimerad tid
- Filtrering via grade-tabs i sidans header (`?ak=N` eller klick)

```
Sidebar-tidslinje:
  ● Åk 7 (teal)
    — Geometri 1
    — Geometri 2
    — Geometri 3
  ● Åk 8 (orange)
    — Geometri 1
    — Geometri 2
    — Geometri 3
  ● Åk 9 (rosa)
    — Geometri 1
    — Geometri 2
    — Geometri 3
```

### 4.5 Momentkort (MomentCard)

```css
.moment-card {
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px 22px;
  display: flex;
  align-items: center;
  gap: 18px;
  transition: box-shadow 0.18s, transform 0.18s;
}
```

Status-pills: `done` (grön) / `ongoing` (teal) / `open` (accent) / `locked` (muted)

### 4.6 Badges / Taggar

```css
/* Uppdaterade badge-färger för att matcha årskursfärgerna */
.badge.ak7 { color: #2a9490; border-color: #66C7C2; background: #e8f7f7; }
.badge.ak8 { color: #b5621a; border-color: #F4A261; background: #fef3e8; }
.badge.ak9 { color: #b03070; border-color: #EC6095; background: #fde8f1; }
```

### 4.7 Knappar

```css
/* Primär */
.btn-primary {
  background: var(--accent);
  color: #fff;
  border-radius: var(--radius-sm);
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  padding: 12px 24px;
}
/* Sekundär */
.btn-secondary {
  background: var(--surface2);
  color: var(--accent);
  border: 1.5px solid var(--border);
}
/* Positiv feedback */
.btn-correct { background: var(--correct); color: #fff; }
/* Negativ feedback */
.btn-wrong   { background: var(--wrong);   color: #fff; }
```

---

## 5. Pedagogiskt ramverk

### 5.1 Momentstruktur (per flik)

Varje moment följer detta mönster:

| Fas | Innehåll | Kognitionsvetenskaplig grund |
|-----|----------|------------------------------|
| **Aktivering** | Startuppgift, förförståelsetest | Retrieval practice, prior knowledge |
| **Introduktion** | Problembaserad ingång | Variationsteori — kontrast |
| **Genomgång** | Video + text | Dual coding |
| **Guided practice** | Interaktiv övning med scaffolding | Worked examples → fading |
| **Independent practice** | Uppgifter med varierande representation | Interleaving |
| **Konsolidering** | Exit ticket, spaced repetition-påminnelse | Spacing effect |

### 5.2 Scaffolding-principer

- Börja med fullt stöd (alla ledtrådar synliga)
- Dölj successivt (variationsteori: håll konstant, variera en sak i taget)
- Ge omedelbar feedback
- Tillåt eleven att välja svårighetsgrad

### 5.3 Variationsteori i praktiken

- **Kontrast:** Visa vad något INTE är, bredvid vad det är
- **Generalisering:** Samma struktur, varierande tal/kontext
- **Separation:** Ändra en variabel i taget
- **Fusion:** Flera aspekter varierar samtidigt (avancerat)

---

## 6. Filstruktur (GitHub Pages)

```
patricktegnefur.github.io/Matte/
├── index.html              ← Landningssida (årskurskort + arbetsområdeskort)
├── brand.md                ← Detta dokument
├── assets/
│   ├── css/
│   │   └── PT-Ljus.css     ← Globalt designsystem
│   ├── fonts/              ← (om self-hosted)
│   └── icons/              ← SVG-ikonbibliotek
├── algebra/
│   └── index.html          ← Arbetsområdessida med sidebar-tidslinje
├── geometri/
│   └── index.html          ← Arbetsområdessida med sidebar-tidslinje
├── taluppfattning/
├── procent/
├── statistik/
├── sannolikhet/
└── funk/
```

---

## 7. URL-konventioner

- `?ak=7` / `?ak=8` / `?ak=9` — filtrerar arbetsområdessida på angiven årskurs
- Länkarna i årskurskorten på landningssidan skickar alltid med `?ak=N`
- Utan parameter visas alla årskurser

---

## 8. Responsivitet

- **Mobile-first** — primär målgrupp använder telefon
- Breakpoints: `480px` (sm) / `768px` (md) / `860px` (sidebar bryter) / `1100px` (lg)
- Knappar minst `44×44px` touch-target
- Sidebar-tidslinje: sticky på desktop, statisk och överst på mobil
- Stabila knappositioner (thumb-friendly, inga överraskande layoutskiftar)

---

## 9. Tillgänglighet (a11y)

- Kontrastförhållande ≥ 4.5:1 för all text
- Alla interaktiva element keyboard-navigerbara
- `aria-label` på ikonknappar
- Fokusring synlig och tydlig (`outline: 2px solid var(--accent)`)

---

## 10. Tonalitet & språk

- **Tilltal:** Du (eleven) — varmt, uppmuntrande, aldrig nedlåtande
- **Svårighetsord förklaras** — länk till ordlista eller tooltip
- **Feedback:** Alltid konstruktiv. "Inte riktigt — prova igen!" inte "Fel."
- **Gamification:** XP, streak, level-ups används men är aldrig det primära syftet

---

## 11. Checklista — ny komponent/sida

- [ ] Navbar använder `--gradient` som bakgrund, text/ikoner är `#ffffff`
- [ ] Använder PT Ljus-färger (explicit, ej ärvda)
- [ ] Sora för brödtext/UI, Playfair Display för H1/logotyp, Montserrat för kortrubriker & momentrubriker
- [ ] Åk 7-element är `#66C7C2`, Åk 8 är `#F4A261`, Åk 9 är `#EC6095`
- [ ] Mobile-first, testad på 375px bredd
- [ ] Knappar ≥ 44px, tumvänliga positioner
- [ ] Alla strängar på svenska
- [ ] Feedbackfärger: `#18a348` (rätt) / `#e02020` (fel)
- [ ] Inga externa beroenden utan godkännande (Google Fonts OK)
- [ ] Filen är självbärande HTML (allt inbakat om det är en övningsmodul)
- [ ] Arbetsområdessida: sidebar-tidslinje + `?ak=N` URL-filtrering

---

## 12. Verktygslauncher — "PT Verktyg"

En separat, fristående startsida (`index.html` i verktygsmappen, ej samma sak som Matematikportalens landningssida) som Patrick pinnar som app via Edge "Installera som app" för snabb åtkomst till klassrumsverktyg under lektion. Delar PT Ljus-paletten och gradienten i navbaren, men har egen kortstil (glasmorphism) och ett eget kategorisystem.

### 12.1 Verktygskategorier

Tre kategorier, filtrerbara via pillar högst upp på sidan. De återanvänder gradientens tre kulörer, men ger dem en ny betydelse här — verktygstyp istället för årskurs:

| Kategori | `data-category` | Färg (hex) | CSS-variabel | Vad den samlar |
|---|---|---|---|---|
| Klassrum | `klassrum` | `#3aada8` (teal) | `--cat-klassrum` | Allmänna, ej ämnesspecifika verktyg för lektionsledning — t.ex. timer, tärning, miniräknare |
| För läraren | `larare` | `#d4813a` (orange) | `--cat-larare` | Visuellt stöd Patrick själv använder under genomgångar — t.ex. tallinjen, laddningsmodellen, trippmätaren |
| För eleven | `elev` | `#c43d75` (rosa) | `--cat-elev` | Mängdträning/övningsverktyg eleverna själva använder — t.ex. multiplikationsruta, procentruta, DAH-ruta |

Filtreringen är ren klient-JS: pillarna sätter `aria-pressed` och visar/döljer kort baserat på deras `data-category`.

### 12.2 Kortdesign — glasmorphism

Till skillnad från elevportalens solida kort (`--surface: #fff`) använder verktygslauncherns kort ett glasat utseende:

```css
background: rgba(255, 255, 255, 0.55);
backdrop-filter: blur(18px) saturate(180%);
-webkit-backdrop-filter: blur(18px) saturate(180%);
border: 1px solid rgba(255, 255, 255, 0.7);
```

Tre suddiga, färgade "ambient"-cirklar (samma tre gradientkulörer, `filter: blur(70px)`, låg opacitet) ligger i `position: fixed` bakom innehållet, så glaseffekten har färg att bryta mot istället för att stå mot en platt bakgrund. Varje kort har kvar den 4px färgade topstripen från originaldesignen, plus en kategori-chip i kategorins färg.

### 12.3 Lägga till ett nytt verktyg

Kopiera ett helt kort-block i `#appGrid`. Byt:
- `data-category` till rätt slug (`klassrum` / `larare` / `elev`)
- `--tile-color` till motsvarande CSS-variabel (`var(--cat-klassrum)` osv.)
- ikon, titel och en kort beskrivande mening (vad verktyget gör, inte bara namnet)

Ingen extra kod behövs för filtreringen — den läser `data-category` automatiskt.
