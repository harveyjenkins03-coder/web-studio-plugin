# DNA Profile: Concrete Industrial

**Category:** Dark / Raw  
**Mood:** Brutalist architecture, raw materials, post-industrial beauty, silent power

---

## Emotional Target

The site feels built, not designed. Like a concrete building with exposed rebar — functional, heavy, beautiful in its rawness. Nothing is decorative for decoration's sake. Materials are what they are.

Design references: Zaha Hadid Architects digital, Architecture firms, SOM, Raw concrete spaces, Detroit industrial revival branding

---

## Color System

```
Background:    #0f0f0e (near-black with slight warm tint)
Surface:       #1c1b19 (dark concrete)
Border:        #2d2c29
Foreground:    #e8e6e1 (warm light gray — like concrete dust)
Muted:         #6b6963
Accent:        #c8ff00 (electric chartreuse — extreme contrast with raw dark)
Accent 2:      #e8e6e1 (foreground as secondary accent)
```

The chartreuse accent is the signal that this isn't just dark — it's industrial with a mark. Alternatively: raw steel blue, safety orange.

---

## Typography

**Display:**
- Neue Haas Grotesk Display — weight 300 or 700 (no middle weights)
- Aktiv Grotesk — weight 300, 700
- Monument Extended — weight 800 (wide, monumental)

**Body:**
- Neue Haas Grotesk Text — weight 400
- Suisse Int'l — weight 300-400

**Size system:**
```
Display:   clamp(64px, 10vw, 160px)   weight 800 or 300 (extreme contrast)
H1:        clamp(40px, 6vw, 96px)     weight 700
H2:        clamp(24px, 3vw, 40px)     weight 400
Body:      16px                        weight 300, line-height 1.8
Label:     10px                        all-caps, tracking 0.3em
```

---

## Layout Principles

- Massive typography as primary architectural element
- Horizontal band sections with full-width content
- No rounded corners (ever)
- Exposed grid structure
- Thin horizontal rules at section boundaries
- Images shown as raw documentation, not styled photography

---

## Motion Profile

- **Speed:** Slow and heavy. Durations 1.0s-1.4s.
- **Ease:** `power4.out` — weight and impact
- **Lenis lerp:** 0.07 — concrete doesn't bounce
- **Reveal:** Text rises from below (long distance, 100px+), not fades
- **No:** Bouncy animations, rounded reveals, warm glow effects

---

## Art Direction

**Primary:** Generative code art — geometric patterns, wireframe structures, architectural section cuts  
**Secondary:** Photography of raw materials (concrete, steel, stone) with high contrast

**CSS concrete texture:**
```css
.concrete-bg {
  background:
    radial-gradient(circle at 25% 25%, #1e1d1a 0%, transparent 50%),
    radial-gradient(circle at 75% 75%, #141311 0%, transparent 50%),
    #0f0f0e;
  /* Noise overlay for texture */
}
```

**Photo treatment:**
```css
.industrial-image {
  filter: grayscale(80%) contrast(1.3) brightness(0.7);
}
```

---

## Signature Elements

- **Monumental type:** Single word at 200px fills entire viewport width
- **Thin rule dividers:** 1px rules, exact column width, chartreuse accent
- **Material counters:** 01 / 08 section numbers, architectural drawing style
- **No-hover state:** Elements change color on hover but NEVER move
- **Exposed dimensions:** Section labeled with pixel heights, architectural notation

---

## Anti-Patterns

- **Never:** Rounded corners
- **Never:** Gradient backgrounds (flat or textured only)
- **Never:** Serif or decorative fonts
- **Never:** Soft, friendly animations
- **Never:** Warm, cozy color palettes

---

## Component Recipes

### Industrial Section Header
```html
<div class="industrial-header">
  <span class="section-num">03 ——</span>
  <h2>Material</h2>
  <div class="section-rule"></div>
</div>
```

```css
.industrial-header {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: end;
  gap: 24px;
  border-bottom: 1px solid var(--color-border);
  padding-bottom: 24px;
  margin-bottom: 64px;
}
.section-num {
  font-size: 11px;
  color: var(--color-accent);
  text-transform: uppercase;
  letter-spacing: 0.3em;
  font-weight: 300;
}
.section-rule { height: 1px; background: var(--color-border); align-self: center; }
```
