# DNA Profile: Dark Luxe

**Category:** Dark / Premium  
**Mood:** Understated power, nocturnal sophistication, old-money restraint

---

## Emotional Target

The site communicates wealth without announcing it. Nothing shouts. Everything is precisely placed. The user feels they've entered an exclusive space — like a private members' club where the most expensive item on the menu has no price.

Design references: Bottega Veneta digital, Loro Piana, The Connaught, Maison Margiela

---

## Color System

```
Background:    #080808 (pure near-black, slight warmth)
Surface:       #111111
Border:        #222222
Foreground:    #e8e4de (warm off-white, never pure white)
Muted:         #6a6560
Accent:        #c9a96e (antique gold)
Accent 2:      #8a7a64 (warm bronze — secondary, rare)
```

No blues. No teals. No electric colors. The entire chromatic world is warm, dark, and gold-tinted.

**Gradient:** Background subtly shifts from #0c0b09 (top) to #080808 (bottom) — imperceptible, adds depth.

---

## Typography

**Display:**
- Cormorant Garamond (Italic) — weight 300-400
- Freight Display Pro — weight 300
- EB Garamond — weight 300

**Body:**
- Cormorant (Roman) — weight 300, generous leading (1.8)
- Literata — weight 300-400

**Utility/Labels:**
- Suisse Int'l (weight 300, all-caps, very wide tracking: 0.2em+)
- Or custom letter-spacing on a neutral geometric sans

**Size system (mobile-first):**
```
Display:  clamp(60px, 10vw, 140px)  weight 300, italic
H1:       clamp(40px, 6vw, 80px)    weight 300
H2:       clamp(28px, 3vw, 44px)    weight 400
Body:     18px                       weight 300, line-height 1.9
Label:    11px                       all-caps, tracking 0.25em
```

---

## Layout Principles

- Wide left margins (12-20% of viewport width)
- Content rarely touches screen edges
- Generous section padding: min 120px top/bottom
- Line lengths capped at 55-65 characters for body copy
- Asymmetric: text offset left, images bleed right
- White space is the primary design element

**Grid:** 12-column, 4-column used maximum. Content in columns 2-9, imagery in 7-12 or full-bleed.

---

## Motion Profile

- **Speed:** Slow. Durations 1.0s-1.6s. Nothing snaps.
- **Ease:** `power3.out` exclusively. No bouncy eases, ever.
- **Lenis lerp:** 0.06 — ultra-slow scroll, heavy gravity
- **Page load:** Long preloader (2s count), slow hero reveal after
- **Scroll reveals:** Long line-by-line text unfurls, image wipes slow
- **Hover:** Subtle glow on accent elements (0.4s transition), no lifting
- **No:** Parallax that moves text, fast flashes, pop-in animations

---

## Art Direction

**Primary:** Generative code art — atmospheric gradient orbs, grain overlay  
**Secondary:** Photography with CSS treatment (monochrome, slight warm tint, subtle grain)

**Hero treatment:**
```css
.hero {
  background: radial-gradient(ellipse at 30% 60%, #1a140a 0%, #080808 70%);
}
/* + grain overlay at 4% opacity */
```

**Image treatment:**
```css
.dark-luxe-image {
  filter: sepia(20%) brightness(0.85) contrast(1.1);
  mix-blend-mode: luminosity;
}
```

---

## Signature Elements

- **Custom cursor:** Minimal 6px dot in #c9a96e, no follower ring
- **Preloader:** Slow numerical count (0→100) in display serif, gold counter
- **Section dividers:** 1px rules, 60% width, centered, gold (#c9a96e at 30% opacity)
- **CTA button style:** Ghost button, thin gold border, letter-spaced sans label
- **Navigation:** Minimal — wordmark left, 3-4 links right, ultra-light weight

---

## Anti-Patterns for This DNA

- **Never:** Rounded corners > 4px
- **Never:** Drop shadows (use subtle borders instead)
- **Never:** Saturated colors of any hue
- **Never:** Bold or black font weights for body
- **Never:** Cards with colored backgrounds
- **Never:** Gradient overlays in primary colors
- **Never:** Bounce or elastic easing

---

## Component Recipes

### Hero
```
Full-height, near-dark background with grain
Centered or left-aligned display serif (italic, weight 300)
One-line or two-line headline maximum
Thin rule below headline
Small sans-serif subtext (label style)
Ghost CTA button, bottom-left
```

### Navigation
```
Transparent on dark background
Wordmark in display serif (weight 300)
Links: 12px sans, all-caps, tracking 0.15em
No hamburger on desktop: always visible minimal nav
```

### Card
```
No background color — just a thin border (1px #222)
Generous internal padding (40px+)
Image takes 60% of card area
Text below, display font for headline, muted for metadata
```
