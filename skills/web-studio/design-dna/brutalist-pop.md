# DNA Profile: Brutalist Pop

**Category:** Bold / Expressive  
**Mood:** Anti-design as design, raw energy, confrontational beauty, Y2K maximalism

---

## Emotional Target

The site makes you feel something immediately — often surprise or amusement. It violates expectations deliberately. The typography is aggressive. The colors clash intentionally. The user feels they've found a brand that doesn't follow rules.

Design references: Balenciaga, Palace Skateboards, SSENSE editorial, Craigslist if it were designed on purpose, Ganni digital

---

## Color System

**Option A — Violent Yellow:**
```
Background:    #f5f500 (pure electric yellow)
Surface:       #eee800
Border:        #1a1a1a
Foreground:    #1a1a1a
Muted:         #555555
Accent:        #1a1a1a (black is the accent)
Accent 2:      #ff0000 (emergency red, used < 3% coverage)
```

**Option B — Stark Black-White:**
```
Background:    #0a0a0a
Surface:       #111111
Border:        #f0f0f0 (white border on black)
Foreground:    #f0f0f0
Muted:         #888888
Accent:        #f5f500 (yellow)
Accent 2:      #ff0000 (red)
```

Choose based on context: Option A for brands targeting youth/fashion. Option B for digital-native/tech brands wanting edge.

---

## Typography

**Display:**
- Bebas Neue — all-caps, weight 400 (the canonical brutalist choice)
- Dharma Gothic E — extra-wide, dramatic
- Big Shoulders Display — weight 900
- Epilogue — weight 900 (more refined brutalism)

**Body:**
- Courier New / Courier Prime — monospace body text is on-brand
- Space Grotesk — weight 400 (modern but not generic for this context)

**Size system:**
```
Display:   clamp(80px, 15vw, 260px)   all-caps, tracking -0.02em
H1:        clamp(48px, 8vw, 120px)    all-caps
H2:        clamp(28px, 4vw, 56px)     all-caps
Body:      16px                        monospace or geometric sans
Label:     12px                        all-caps, no tracking (brutal)
```

**Anti-typography rules:**
- Mix type sizes radically (280px headline next to 12px caption)
- Break columns: text running into images, text at unexpected angles (CSS `rotate`)
- Stacking sans and mono in same section is encouraged

---

## Layout Principles

- Break the grid deliberately (elements outside the expected grid zone)
- Expose the grid structure visually (visible column lines, numbered columns)
- Collide elements: overlapping text/image combinations
- Asymmetry is mandatory: no centered layouts
- Thick borders (4px-8px) as primary design element
- Large negative space OR extreme density — no middle ground
- Tables and lists as design elements, not just content

**Grid:** CSS Grid with visible grid lines (debuggable, intentionally shown), columns 1-12 with overlap zones.

---

## Motion Profile

- **Speed:** Fast. Durations 0.2s-0.5s. Snap and punch.
- **Ease:** `power4.out` for entrances, `power4.in` for exits
- **Lenis lerp:** 0.15 — snappier scroll, less lag
- **Page load:** Instant. No preloader. Content crashes in on load.
- **Scroll reveals:** Immediate, sharp clip-path wipes. Text slams from direction.
- **Hover:** Color inversion (black/white swap), no smooth transitions on brutalist accents
- **Text scramble:** Heavy use of scramble effect for headings

---

## Art Direction

**Primary:** SVG geometric compositions — hard shapes, angular, bold  
**Secondary:** Exposed grid structures, typographic compositions as art

**No photography unless with heavy CSS treatment:**
```css
.brutalist-image {
  filter: contrast(2) grayscale(100%);
  mix-blend-mode: multiply;
  /* Or: */
  filter: contrast(1.8) saturate(0) brightness(1.2);
}
```

**Decorative elements:**
- Thick rules (8px) as horizontal dividers
- Grid crosshair markers at intersections
- Large numerals (100px+) as decorative section markers
- Exposed typographic anatomy (baseline grid, cap-height markers)

---

## Signature Elements

- **Marquee:** Fast-scrolling ticker with ALL-CAPS text, thick border above/below
- **Hover:** Color inversion on entire element
- **Cursor:** Large crosshair cursor in accent color
- **Error states:** Over-the-top, dramatic (full-screen 404 text at 400px)
- **Buttons:** Thick borders, no border-radius, brutal color swap on hover

---

## Anti-Patterns for This DNA

- **Never:** Rounded corners > 0px (unless a perfect circle)
- **Never:** Drop shadows (use solid color offsets instead: `box-shadow: 4px 4px 0 #000`)
- **Never:** Soft, muted color palettes
- **Never:** Serif fonts for headings
- **Never:** Smooth, slow animations
- **Never:** Centered text (rare exceptions for single impact statements)
- **Never:** A design that feels polished and safe

---

## Signature CSS Patterns

### Solid shadow (brutalist card)
```css
.brutal-card {
  border: 2px solid var(--color-fg);
  padding: 24px;
  position: relative;
  background: var(--color-bg);
  box-shadow: 6px 6px 0 var(--color-fg);
  transition: box-shadow 0.15s, transform 0.15s;
}
.brutal-card:hover {
  box-shadow: 10px 10px 0 var(--color-fg);
  transform: translate(-4px, -4px);
}
```

### Color inversion button
```css
.brutal-btn {
  border: 2px solid var(--color-fg);
  padding: 12px 28px;
  background: transparent;
  color: var(--color-fg);
  font-family: var(--font-display);
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  transition: background 0.15s, color 0.15s;
}
.brutal-btn:hover {
  background: var(--color-fg);
  color: var(--color-bg);
}
```
