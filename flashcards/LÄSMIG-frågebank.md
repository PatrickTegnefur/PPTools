# Permanent frågebank för PT Minneskort

## Två filer, olika uppdateringstakt

| Fil | Innehåll | Ändras |
|---|---|---|
| `minneskort-data-begrepp.js` | Din stabila "grundutgåva" — begrepp för hela högstadiet, taggade årskurs + arbetsområde | Sällan |
| `minneskort-data-mattematchen.js` | Läxuppgifterna (Mattematchen 1–20) | Varje vecka |

Båda är helt valfria var för sig — saknas en av dem laddas bara den andra.
Vill du dela upp ytterligare (t.ex. en fil per ämne) går det bra: lägg till
fler `<script src="...">`-rader i `PT-Minneskort.html` där de andra två
står, och låt filen anropa `registerMinneskortBank({...})` precis som de
befintliga. Ordningen mellan filerna spelar ingen roll.

## Så funkar synken

Varje gång sidan öppnas läses filerna in och slås ihop med det som redan
finns sparat i webbläsaren:

- **Nytt kort/samling/ämne** (nytt id) → läggs till
- **Befintligt id, ändrat innehåll** → uppdateras, men elevens sparade
  trafikljus-status rörs aldrig
- **Kort du tar bort ur filen** → påverkas inte lokalt automatiskt; ta bort
  dem i appen (Redigera kort) om de verkligen ska försvinna för eleverna också

**Id:n är permanenta.** Byt aldrig ett korts `id` bara för att uppdatera
fråga/svar/bild — då tolkas det som ett nytt kort och kopplingen till
elevens tidigare status tappas.

## Delning med kollegor

Om kollegor besöker din hostade GitHub Pages-länk (istället för att ladda
ner egna lokala kopior) får de automatiskt dina senaste uppdateringar av
båda filerna varje gång de öppnar sidan — inget de behöver göra själva.

## Mappstruktur

```
Matte/verktyg/minneskort/
├── PT-Minneskort.html
├── minneskort-data-begrepp.js
├── minneskort-data-mattematchen.js
└── assets/
    └── img/
        ├── geometri/
        │   └── ratvinklig-triangel-hypotenusa.svg
        ├── mattematchen/
        │   ├── mm01-01.svg   ← platshållare, byt mot din skärmdump
        │   └── mm03-05.svg   ← platshållare, byt mot din skärmdump
        └── …
```

## Nomenklatur för Mattematchen-skärmdumpar

`mmNN-UU` — Mattematchen NN, Uppgift UU. Nollfyll båda talen (03 inte 3)
så sorteras filerna rätt i Utforskaren/VS Code — annars hamnar "10" före
"2". Låt bildfilens namn och kortets `id` vara identiska
(`mm03-05.png` ↔ `id: 'mm03-05'`) så slipper du hålla reda på en
översättning mellan de två.

**Arbetsflöde:**
1. Skärmdumpa läxans sida i Word/PDF.
2. Beskär till en uppgift i taget, spara som `mmNN-UU.png` i
   `assets/img/mattematchen/`.
3. Lägg till kortet i `minneskort-data-mattematchen.js` enligt mallen —
   kopiera en befintlig post och byt id, samling och bildsökväg.

## Övrigt värt att veta

- **SVG rekommenderas** för egenritade figurer (geometri m.m.) — skarpt i
  alla storlekar, litet i filstorlek, redigerbart som ren text.
  **PNG/JPG** för riktiga skärmdumpar av läxan, som i Mattematchen-exemplen.
- Bilder bäddas **inte** in i datafilerna — de ligger som separata filer
  och refereras med relativ sökväg, vilket håller filerna lätta att
  läsa/diffa i git.
- Har du redan pappersläxorna färdiga i t.ex. GeoGebra eller Word kan det
  ofta gå snabbare att exportera samma figur därifrån än att rita om den
  för hand.
