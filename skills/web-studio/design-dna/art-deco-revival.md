# DNA Profile: Art Deco Revival

**Category:** Dark / Ornate  
**Mood:** Roaring twenties in a server rack, geometric opulence, gold on darkness

---

## Emotional Target

The site feels like walking into a restored 1920s ballroom that has been modernized without losing its soul. Geometric symmetry, gold accents, and ornamental patterns create a sense of occasion. Everything feels formal, considered, and slightly theatrical.

Design references: The Savoy hotel digital, Great Gatsby film aesthetics, Chrysler Building interior, NYPL digital archives, premium cocktail bar websites

---

## Color System

```
Background:    #1a1208 (very dark warm brown, like aged wood)
Surface:       #251a0e
Border:        #3d2c18
Foreground:    #f5e8c8 (warm parchment gold-white)
Muted:         #9a8060
Accent:        #c9a032 (antique gold)
Accent 2:      #e8c84a (bright gold for highlights)
```

---

## Typography

**Display:**
- Cormorant Garamond — Italic, weight 300 (elegant, period-appropriate)
- Freight Display Pro — weight 300 italic
- Playfair Display — weight 400 with Small Caps feature

**Utility/Labels:**
- Josefin Sans — all-caps, wide tracking (1920s geometric sans)
- Gill Sans — weight 300-400

**Size system:**
```
Display:   clamp(56px, 8vw, 120px)   italic, weight 300
H1:        clamp(40px, 5.5vw, 80px)  italic, weight 300
H2:        clamp(24px, 3vw, 40px)    small-caps, weight 400
Body:      17px                       weight 400, line-height 1.85
Label:     12px                       all-caps, tracking 0.25em, gold color
```

---

## Layout Principles

- Strict bilateral symmetry (radically different from modern asymmetric layouts)
- Centered compositions with geometric framing elements
- Ornamental borders: gold rules, corner flourishes (SVG)
- Architectural proportions: tall, narrow columns like 1920s building facades
- Stepped/chevron patterns as decorative dividers

---

## Motion Profile

- **Speed:** Stately. Durations 1.0s-1.8s.
- **Ease:** `power3.out`, `power4.inOut` — nothing jarring
- **Lenis lerp:** 0.07 — heavy, ceremonial scroll
- **Scroll reveals:** Curtain wipes from center (symmetric), gold accent lines draw
- **Art reveals:** SVG geometric patterns draw in on scroll (stroke-dashoffset animation)
- **Hover:** Gold glow, slight brightness increase

---

## Art Direction

**Primary:** Custom SVG geometric illustrations — sunburst patterns, geometric frames, stylized ornaments  
**Secondary:** Generative CSS art (radial gradients composing geometric shapes)

**Deco geometric SVG pattern:**
```html
<svg viewBox="0 0 400 400" class="deco-ornament">
  <!-- Sunburst radiating from center -->
  <g transform="translate(200,200)">
    <line x1="0" y1="0" x2="0" y2="-180" stroke="#c9a032" stroke-width="1" opacity="0.6"/>
    <!-- Repeat 24 times at 15deg intervals -->
    <circle r="20" fill="none" stroke="#c9a032" stroke-width="1"/>
    <circle r="60" fill="none" stroke="#c9a032" stroke-width="0.5" stroke-dasharray="4 4"/>
    <circle r="120" fill="none" stroke="#c9a032" stroke-width="0.5" opacity="0.4"/>
  </g>
</svg>
```

**Deco border pattern:**
```css
.deco-border {
  border: 1px solid var(--color-accent);
  position: relative;
  padding: 40px;
}
.deco-border::before,
.deco-border::after {
  content: '';
  position: absolute;
  border: 1px solid var(--color-accent);
}
.deco-border::before { inset: 6px; opacity: 0.4; }
```

---

## Signature Elements

- **Geometric decorative rules:** Double-line rules with diamond center point
- **Corner flourishes:** SVG art deco corner ornaments
- **Sunburst pattern:** Behind hero text, radiating gold lines
- **Stepped sections:** Each section steps inward (decreasing width) like a ziggurat
- **Monogram or crest:** Central geometric monogram as hero visual

---

## Anti-Patterns

- **Never:** Asymmetric layouts
- **Never:** Modern sans-serif display fonts
- **Never:** Bright, saturated colors beyond gold
- **Never:** Flat, icon-set icons
- **Never:** Generic hero with gradient blob

---

## Component Recipes

### Deco Section Divider
```html
<div class="deco-divider">
  <div class="deco-line"></div>
  <svg class="deco-diamond" viewBox="0 0 20 20">
    <rect x="5" y="5" width="10" height="10" transform="rotate(45,10,10)"
          fill="none" stroke="#c9a032" stroke-width="1"/>
  </svg>
  <div class="deco-line"></div>
</div>
```

```css
.deco-divider {
  display: flex;
  align-items: center;
  gap: 16px;
  margin: 64px auto;
  max-width: 400px;
}
.deco-line {
  flex: 1;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--color-accent), transparent);
}
.deco-diamond { width: 20px; height: 20px; }
```
