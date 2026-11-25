# DNA Profile: Cosmic

**Category:** Dark / Immersive  
**Mood:** Deep space wonder, the universe as interface, scientific beauty

---

## Emotional Target

The site feels like peering into a telescope at something vast and incomprehensible. Dark void backgrounds, violet and stellar blue accents, subtle motion that suggests deep-space distances. The user feels small and awed in the best possible way.

Design references: NASA JPL image libraries, Space.com premium, Kurzgesagt visual style, Apple's Astronomy app, stellarium.org

---

## Color System

```
Background:    #030010 (void-black with imperceptible purple tint)
Surface:       #0a0520
Border:        #1a0f40
Foreground:    #f0e8ff (warm light purple-white)
Muted:         #7060b0
Accent:        #8b5cf6 (violet)
Accent 2:      #38bdf8 (sky-cyan)
```

**Nebula gradient background:**
```css
body {
  background:
    radial-gradient(ellipse at 30% 40%, rgba(139, 92, 246, 0.12) 0%, transparent 60%),
    radial-gradient(ellipse at 70% 80%, rgba(56, 189, 248, 0.08) 0%, transparent 60%),
    #030010;
}
```

---

## Typography

**Display:**
- Ginto Nord — weight 700 (contemporary, slightly wide)
- Neue Haas Grotesk Display — weight 200-300 (weightlessness)
- Manrope — weight 800 (modern, clean)

**Body:**
- Manrope — weight 400
- Geist — weight 400

**Size system:**
```
Display:   clamp(48px, 7vw, 100px)   weight 800 or 200 (extremes)
H1:        clamp(32px, 4.5vw, 68px)  weight 700
H2:        clamp(22px, 2.8vw, 40px)  weight 600
Body:      16px                        line-height 1.75
Caption:   13px                        muted purple
```

---

## Layout Principles

- Full-height sections that feel like telescope fields of view
- Stars (small dots) scattered as decorative background elements
- Content centered against the void
- Violet/cyan glows behind key content blocks
- Numbers and statistics presented as "stellar data"
- Horizontal scrolling sections for exploration feel

---

## Motion Profile

- **Speed:** Slow, vast. Durations 1.0s-2.0s.
- **Ease:** `power3.out` — weight of celestial movement
- **Lenis lerp:** 0.06 — the heaviness of space
- **Parallax:** Deep parallax (stars move slower than content)
- **Particles:** Star field slowly drifts (Three.js)
- **Reveal:** Content emerges from void — opacity only, no position
- **No:** Fast snaps, mechanical timing

---

## Art Direction

**Primary:** Three.js particle systems — star fields, nebula glows  
**Secondary:** CSS generative art — cosmic gradients, star patterns

**CSS star field:**
```css
.star-field {
  position: absolute;
  inset: 0;
  background-image:
    radial-gradient(1px 1px at 10% 15%, rgba(255,255,255,0.8) 0%, transparent 100%),
    radial-gradient(1.5px 1.5px at 30% 40%, rgba(255,255,255,0.6) 0%, transparent 100%),
    radial-gradient(1px 1px at 60% 20%, rgba(255,255,255,0.9) 0%, transparent 100%),
    radial-gradient(2px 2px at 80% 70%, rgba(255,255,255,0.4) 0%, transparent 100%),
    radial-gradient(1px 1px at 50% 85%, rgba(255,255,255,0.7) 0%, transparent 100%);
  /* Repeat with many more star positions for full effect */
}
```

**Nebula glow effect:**
```css
.nebula-glow {
  background:
    radial-gradient(ellipse at center, rgba(139, 92, 246, 0.25) 0%, rgba(56, 189, 248, 0.1) 40%, transparent 70%);
  filter: blur(40px);
  position: absolute;
  inset: -100px;
  pointer-events: none;
}
```

---

## Signature Elements

- **Star particle system** (Three.js, 3000+ points)
- **Nebula glows** behind hero sections
- **Slow rotation** on hero decorative elements (transforms over 60s)
- **Distance typography:** Very small label + very large heading to convey scale
- **Data in stellar units:** "127 light-years · 4.2 megaparsecs" style formatting

---

## Anti-Patterns

- **Never:** Warm colors
- **Never:** Light backgrounds
- **Never:** Fast, snappy animations (nothing in space moves quickly)
- **Never:** Decorative elements that are "designed" rather than natural

---

## Component Recipes

### Stellar Stat
```html
<div class="stellar-stat">
  <span class="stellar-unit">×</span>
  <span class="stellar-number">10B</span>
  <span class="stellar-label">stars in the galaxy</span>
</div>
```

```css
.stellar-stat {
  display: grid;
  grid-template-rows: auto auto;
  text-align: center;
}
.stellar-number {
  font-size: clamp(64px, 10vw, 140px);
  font-weight: 200;
  color: var(--color-fg);
  letter-spacing: -0.03em;
  line-height: 0.9;
  background: linear-gradient(to bottom, var(--color-fg), var(--color-muted));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.stellar-label {
  font-size: 13px;
  color: var(--color-muted);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  margin-top: 12px;
}
```
