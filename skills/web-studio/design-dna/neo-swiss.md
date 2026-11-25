# DNA Profile: Neo-Swiss

**Category:** Light / Systematic  
**Mood:** The grid as god, information architecture as beauty, Helvetica's children

---

## Emotional Target

This design radiates competence and order. Every element occupies exactly the space it deserves — not a pixel more. The typography is tight and authoritative. White space is structured, not incidental. The user feels they're in the presence of serious thinking made visible.

Design references: Müller-Brockmann posters, Neue Grafik magazine, Massimo Vignelli's NYC subway, Swiss passport, Bang & Olufsen, Braun product catalogs

---

## Color System

```
Background:    #ffffff (pure white — no warmth, no coolness)
Surface:       #f4f4f4
Border:        #e0e0e0
Foreground:    #000000 (pure black)
Muted:         #666666
Accent:        #e63329 (Helvetica red — specific, not generic)
Accent 2:      #000000 (black is the second accent)
```

**Alternative: Black Swiss**
```
Background:    #0a0a0a
Surface:       #141414
Border:        #2a2a2a
Foreground:    #f0f0f0
Accent:        #e63329 (same red, always)
```

The red is non-negotiable. Swiss design owns this specific red (Pantone 485 approximate).

---

## Typography

**Display:**
- Neue Haas Grotesk Display — weight 400, 700
- Aktiv Grotesk — weight 400, 700
- Neue Helvetica — weight 300, 400, 700
- Helvetica Now — weight 300, 700

**Body:**
- Neue Haas Grotesk Text — weight 400
- Aktiv Grotesk — weight 400

**Free alternatives:**
- IBM Plex Sans — weight 400, 700 (structurally similar to Helvetica)
- Work Sans — weight 400, 700

**Size system (strict, mathematical):**
```
Grid unit: 8px
Display:   128px (16 × 8)   weight 700, tracking -0.03em
H1:        64px  (8 × 8)    weight 700, tracking -0.02em
H2:        32px  (4 × 8)    weight 700
H3:        24px  (3 × 8)    weight 400
Body:      16px  (2 × 8)    weight 400, line-height 24px (3 × 8)
Caption:   12px  (1.5 × 8)  weight 400, muted
```

All measurements are multiples of 8. No exceptions.

---

## Layout Principles

- **The grid is visible** (in concept if not in rendering): columns are strict, alignment is exact
- Mathematical proportions: 1:√2 (A4 ratio), 1:1.618 (golden), or strict halves
- Text aligns to baseline grid at every level
- No decorative elements — every visual element carries information
- Column rules (thin 1px vertical lines) as structural decoration
- Large empty zones are intentional — the grid demands them

**Grid:** 12 columns, gutters = 24px (3 × 8), margins = 48px (6 × 8). All content aligns to columns exactly.

---

## Motion Profile

- **Speed:** Measured. Durations 0.4s-0.8s. Nothing lingers.
- **Ease:** `power2.out` — efficient, no overshoot
- **Lenis lerp:** 0.12 — responsive, crisp
- **Page load:** No preloader. Direct render, immediate structure.
- **Scroll reveals:** Grid elements slide in from their natural direction (horizontal for columns, vertical for rows)
- **Hover:** Red underline extends from left, no scale transforms
- **Transitions:** Instant color swaps (0.2s), no morphing

---

## Art Direction

**Primary:** No decorative art — the typography and grid ARE the art  
**Secondary:** When imagery is needed: technical diagrams, high-contrast black-and-white photography, geometric shapes that respect the grid

**Photography style:**
```css
.swiss-image {
  filter: grayscale(100%) contrast(1.2);
  /* Images in Swiss design are functional, not decorative */
}
```

**Geometric decoration:**
- Circles: perfectly circular, aligned to grid
- Rectangles: aligned to column width or multiples thereof
- Lines: 1px or 2px, never decorative stroke weights

**Never:** Gradient fills, organic shapes, texture overlays, illustrations that don't serve information.

---

## Signature Elements

- **Visible column structure:** CSS Grid with optional visible lines
- **Bold section numbers:** 01, 02, 03 — black, bold, left-aligned with body text
- **Red accent rule:** 2px, accent-colored horizontal rule for critical sections
- **Navigation:** Tab-based, all entries visible, no hamburger
- **Tables:** Exposed table design — this DNA profile loves actual HTML tables

---

## Anti-Patterns for This DNA

- **Never:** Rounded corners (except perfect circles)
- **Never:** Drop shadows (they're decorative, not structural)
- **Never:** Serif fonts (this is a grotesque-only aesthetic)
- **Never:** Gradient backgrounds
- **Never:** Decorative dividers (ornamental rule styles)
- **Never:** Animation that draws attention to itself
- **Never:** More than 3 font sizes in any single section

---

## Component Recipes

### Grid-Exposed Feature Section
```
Section background: white
Visible grid via CSS outline or box-shadow technique
Feature items: each in exactly 1 column
Item: large bold number (01), thin rule, heading, body
Red accent: only on the active/featured item
```

### Swiss Button
```css
.swiss-btn {
  display: inline-block;
  padding: 12px 24px;
  background: #000;
  color: #fff;
  font-family: var(--font-body);
  font-size: 14px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  border: none;
  border-radius: 0;
  transition: background 0.2s, color 0.2s;
}
.swiss-btn:hover {
  background: var(--color-accent); /* red */
  color: #fff;
}
```

### Statistics / Data Section
```
3-5 stats in a horizontal row
Each stat: bold number at 80px, label below at 12px, all-caps
Thin 1px vertical rules between stats
Strict column alignment
```
