# 🕊️ CSS-Fågel med Spårande Effekt

Detta lilla projekt visar hur man skapar en flyganimerad fågel med ett spår (trail), genom att kombinera HTML, JavaScript, CSS-animationer och SASS.

---

## 🔍 Problemet

Vi ville skapa en visuell effekt där en fågel (`🐦`) flyger över en bakgrund och lämnar ett svansliknande spår efter sig – ungefär som en rörelse-eko. En vanlig `::after` räcker inte, eftersom vi vill ha flera spår som följer efter fågeln med olika fördröjning och opacitet.

---

## ✅ Lösningen

Vi löste detta genom att:

1. **Använda JavaScript** för att automatiskt skapa 9 klonade `<div>🐦</div>`-element (spår) för varje element med klassen `.with-trail`.
2. **Styling och animation** sker med CSS/SASS:
   - Alla spår är `position: absolute` så de startar på exakt samma plats som originalet.
   - Varje spår får olika `animation-delay`, `opacity` och `z-index` via en SASS-loop.
   - En keyframe-animation (`fly-around`) får fågeln att röra sig över ytan.

---

## 🧠 Vad är SASS?

**SASS (Syntactically Awesome Stylesheets)** är ett förprocessor-språk för CSS som gör det möjligt att skriva mer dynamisk, modulär och återanvändbar kod. **Det kompileras till vanlig CSS.**

---

### 🧵 Varför SASS är bättre än vanlig CSS

För att ge varje spår en unik `animation-delay`, `opacity` och `z-index`, hade vi behövt skriva detta i **vanlig CSS** så här:
```html
<div id="cute-bird" class="flyer with-trail" >🐦</div>
<div class="trail">🐦</div>
<div class="trail">🐦</div>
<div class="trail">🐦</div>
<div class="trail">🐦</div>
osv
```
```css
.trail:nth-child(2) {
  animation-delay: 0.2s;
  opacity: 0.9;
  z-index: 9;
}

.trail:nth-child(3) {
  animation-delay: 0.4s;
  opacity: 0.8;
  z-index: 8;
}
/* ... och så vidare upp till .trail:nth-child(11) */
```

😫 Redan vid 10 element börjar det bli riktigt mycket kod.

✅ Med SASS kunde vi istället skriva:
```scss
@for $i from 1 through 10 {
  .trail:nth-child(#{$i + 1}) { // i + 1 för att .flyer är första barnet
    animation-delay: #{0.2 * $i}s;
    opacity: #{1 - ($i * 1/10)};
    z-index: 10 - $i;
  }
}
```
💡 Det här är kortare, lättare att läsa och enkelt att ändra. Vill vi ha 20 spår i framtiden? Bara ändra through 20.

### 🛠️ Installera & använda SASS i VS Code
För att kompilera .scss till .css live i Visual Studio Code använde jag Live Sass Compiler.

#### 🔽 Steg för steg
##### Installera tillägget:
- Öppna VS Code
- Gå till Extensions
- Sök efter: Live Sass Compiler
- Klicka på “Installera”
- Skapa filerna:
- style.scss – Här skriver du din SASS/SCSS-kod
- När du sparar filen, genereras automatiskt en style.css i samma mapp

##### Starta kompilering:

Klicka på knappen Watch Sass längst ner i VS Code

Länka till CSS i HTML:
```html
<link rel="stylesheet" href="style.css">
```