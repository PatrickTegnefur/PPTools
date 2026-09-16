## 2.7 Logotyp & favicon

Logotypen ligger på en fast, rot-relativ sökväg som är samma oavsett hur djupt ett verktyg eller en sida ligger i mappstrukturen:

```
/brand/pt_logo.jpg
```

d.v.s. i en mapp `brand/` som ligger i roten av `patricktegnefur.github.io` (bredvid t.ex. `Matte/`), inte inuti respektive verktygsmapp.

### Standard-snippet för `<head>`

Klistras in i varje sidas/verktygs `<head>`, tillsammans med övriga meta-taggar:

```html
<link rel="icon" type="image/jpeg" href="/brand/pt_logo.jpg">
<link rel="apple-touch-icon" href="/brand/pt_logo.jpg">
```

- `rel="icon"` → flikikonen i webbläsaren
- `rel="apple-touch-icon"` → ikonen som visas om sidan sparas till hemskärmen på iOS/iPadOS

Eftersom sökvägen är rot-relativ (`/brand/...` med inledande snedstreck) fungerar den identiskt oavsett om filen som länkar till den ligger direkt i roten eller flera mappnivåer ner — ingen `../../`-räkning behövs.

### Att tänka på

- iOS beskär `apple-touch-icon` till en rundad kvadrat automatiskt — en jpg utan transparens (som `pt_logo.jpg`) fungerar utmärkt för det ändamålet.
- Om logotypen någon gång behöver visas *med* genomskinlig bakgrund (t.ex. flytande ovanpå en färgad yta någon annanstans än flikikonen) krävs en PNG-variant separat — `pt_logo.jpg` i sig kan inte vara transparent.
- Checklistan i avsnitt 11 kan med fördel få en rad: "Favicon/`apple-touch-icon` länkad till `/brand/pt_logo.jpg`".
