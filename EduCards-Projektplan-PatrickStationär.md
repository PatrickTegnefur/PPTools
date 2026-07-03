# EduCards -- Projektplan

## Vision

Bygga ett öppet, webbaserat klassrumssystem inspirerat av Plickers men
med fokus på: - Snabb avläsning av hela klassen. - Minskad möjlighet att
kopiera grannens svar. - Lokal körning i webbläsaren (GitHub Pages). -
Integration med övriga PPTools.

## Designmål

-   Kameran läser 30--35 kort på 1--2 sekunder.
-   Kvadratiska kort.
-   Robust mot böjda papper.
-   Ingen installation krävs.
-   Resultat visas direkt.

## Teknik

### Markörer

Använd ArUco-markers istället för QR-koder eftersom de är optimerade för
flera samtidiga markörer och ger ID + rotation.

### Kort

-   Kvadratiskt format.
-   Unikt ArUco-ID i mitten.
-   Fyra sidor används för svar.

## Svarssystem

Varje kort har en egen kodning av A/B/C/D. Programmet vet vilken
orientering som motsvarar vilket svar för varje kort, vilket gör att
elever inte kan läsa av varandras svar.

På sikt kan systemet utökas till: - 8 svarslägen. - Säkerhetsgrad
(säker/osäker). - Ja/Nej. - Skattningsskalor.

## Kortadministration

Första versionen: - Ett klass-set med ca 35 kort. - Kort delas ut efter
platsnummer.

Senare: - Koppling mellan kort, elev och klasslista. - Export till
Excel/CSV.

## Webbapplikation

Moduler: 1. Frågor. 2. Kameravy. 3. Realtidsanalys. 4. Resultat. 5.
Statistik.

## Framtida funktioner

-   Närvaroregistrering.
-   Heatmap över obesvarade kort.
-   PowerPoint-integration.
-   Frågebank.
-   Statistik över tid.
-   PPTools Live.

## Utvecklingsplan

### Fas 1 -- Proof of Concept

-   Läsa ArUco-markörer.
-   Identifiera ID.
-   Läsa rotation.
-   Visa svarsfördelning.

### Fas 2 -- MVP

-   Elevregister.
-   Spara resultat.
-   Export.

### Fas 3

-   Statistik.
-   Frågebank.
-   Integration med övriga PPTools.

## Nästa steg

Börja med kameradelen. Om vi kan läsa många markörer snabbt är resten
huvudsakligen mjukvarulogik.
