# DNA Profile: Editorial Serif

**Category:** Light / Editorial  
**Mood:** Intellectual confidence, magazine authority, the print world made digital

---

## Emotional Target

The site feels like a premium print publication that has been born digital — not converted. The typography commands attention. White space is not negative space, it's punctuation. The reader feels the weight of considered thought.

Design references: The New York Times T Magazine, Kinfolk, Monocle, Cereal, It's Nice That

---

## Color System

```
Background:    #f5f1eb (warm parchment — not pure white)
Surface:       #ede8e0
Border:        #d4cdc3
Foreground:    #1a1814 (warm near-black)
Muted:         #7a7268
Accent:        #c41e3a (deep crimson — used sparingly)
Accent 2:      #1a1814 (black IS the secondary accent)
```

Light mode only. Dark mode for this profile would require a complete redesign — do not invert.

---

## Typography

**Display:**
- Canela (Text or Display) — weight 300-400, italic for pull quotes
- Freight Big Pro — weight 300-400
- Domaine Display — weight 300
- Playfair Display — weight 400 (free alternative)

**Body:**
- Tiempos Text — weight 400, line-height 1.8
- Freight Text Pro — weight 400
- Source Serif 4 — weight 400 (free alternative)

**Labels/Captions:**
- Suisse Int'l — 11px, all-caps, tracking 0.15em
- Or the display font at very small size for decorative labels

**Size system:**
```
Display:   clamp(64px, 9vw, 160px)   weight 300
H1:        clamp(44px, 5vw, 80px)    weight 400, line-height 1.1
H2:        clamp(28px, 3vw, 48px)    weight 400, line-height 1.2
Body:      18-20px                    weight 400, line-height 1.8
Caption:   13px                       muted, line-height 1.5
Label:     11px                       all-caps, tracking 0.15em
```

---

## Layout Principles

- Print-inspired column grid (often 3 or 5 columns, not just 12)
- Text columns break editorial convention: full-width headline, then 2-column body
- Images extend outside text column (margin-bleed)
- Rule lines used decoratively (1px, horizontal and vertical)
- Numbered sections (01, 02) as navigational indicators
- Drop caps for long-form body text
- Pull quotes enlarged and positioned asymmetrically

**Grid:** True editorial grid — 5 column preferred. Body text in columns 1-3, images overflow to 4-5, or full-bleed.

---

## Motion Profile

- **Speed:** Measured. Durations 0.8s-1.2s.
- **Ease:** `power3.out`, `power4.out` for reveals
- **Lenis lerp:** 0.08 — deliberate, like turning a magazine page
- **Page load:** No preloader — content loads directly, headline rises in
- **Scroll reveals:** Line-by-line text reveals, image fade + upward drift
- **Hover:** Link underline animates from left (scale-x), images subtly brighten
- **No:** Parallax on text, fast snap animations, 3D transforms

---

## Art Direction

**Primary:** Photography with editorial CSS treatment  
**Secondary:** Custom SVG illustrations (line art style)

**Image style:** High contrast, careful composition, significant empty space within frame. Not stock photo style — editorial photography style.

**CSS treatment:**
```css
.editorial-image {
  filter: contrast(1.05) brightness(0.95);
}

/* For black-and-white moments */
.editorial-image--mono {
  filter: grayscale(100%) contrast(1.1);
}
```

**Section dividers:** Thin horizontal rules with or without issue numbers:
```html
<div class="editorial-rule">
  <span class="issue-num">01</span>
  <hr />
</div>
```

---

## Signature Elements

- **Typography as hero:** The headline IS the visual — no background art needed
- **Numbered sections:** Two-digit section counters (01, 02...) in small sans
- **Drop cap:** First letter of feature articles set large (6-8 lines tall)
- **Pull quotes:** Oversized quote marks, offset from column grid
- **Hover:** Link underline grows from left, image captions slide up on image hover

---

## Anti-Patterns for This DNA

- **Never:** Dark backgrounds
- **Never:** Rounded corners (except profile photos, subtle 4px max)
- **Never:** Sans-serif display fonts (the whole point is the serif)
- **Never:** Drop shadows
- **Never:** Gradient backgrounds
- **Never:** Decorative icons or emoji
- **Never:** Bright, saturated accent colors for anything except a single CTA

---

## Component Recipes

### Hero (Long-Form Article Style)
```
Issue/category label: 11px, all-caps, crimson, tracking 0.2em
Headline: Full-width, display serif, weight 300-400
Deck (subtitle): 20px serif, muted, 2-col width
Thin rule below deck
Author + date: 13px sans, muted
Optional: One full-bleed image below, caption below image
```

### Feature Image
```
Full-width or column-overflow width
No border-radius
Caption below: 13px, muted, italic
Optional: image number (01 of 04) right-aligned
```

### Body Text Column
```
Max-width: 65ch
18-20px serif, line-height 1.8
First paragraph: drop cap, or bold first line
Pull quote: every 400-600 words, offset from column
```
