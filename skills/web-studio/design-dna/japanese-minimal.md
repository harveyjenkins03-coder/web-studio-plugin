# DNA Profile: Japanese Minimal

**Category:** Light / Zen  
**Mood:** Ma (negative space), wabi-sabi acceptance, the beauty of restraint pushed further than Scandinavian minimal

---

## Emotional Target

The site achieves near-nothing and feels complete. Whitespace doesn't feel empty — it feels meditative. A single element placed with intention has more weight than ten elements placed carelessly. The user slows down involuntarily.

Design references: MUJI digital, Japanese architecture firms, Nendo, Kenya Hara's design philosophy, Comme des Garçons, 21_21 Design Sight

---

## Color System

```
Background:    #fafafa (almost-white — absolute purity)
Surface:       #f5f5f5
Border:        #e8e8e8 (almost invisible)
Foreground:    #1a1a1a (sumi-e ink black)
Muted:         #9a9a9a
Accent:        #1a1a1a (black — no chromatic accent)
Accent 2:      #c41e3a (used once, maximum, for the most important thing)
```

**Seasonal variant:** In Spring contexts, a very muted sakura pink:
```
Accent:   #e8a0a8 (pale sakura — 10% coverage maximum)
```

---

## Typography

**Display:**
- Hiragino Mincho ProN (Japanese only, web-safe)
- BIZ UDMincho (Google Fonts, Japanese)
- For Latin-only: Cormorant Garamond weight 300

**Body:**
- Noto Serif JP (Japanese)
- Noto Sans JP (Japanese, weight 300)
- For Latin-only: Literata weight 300

**If using Latin fonts only:**
```
Display:   Cormorant Garamond   weight 300
Body:      Lora                  weight 400 (generous line-height)
Labels:    IBM Plex Sans         weight 300, small-caps, wide tracking
```

**Size system:**
```
Display:   clamp(40px, 5vw, 80px)    weight 300, line-height 1.2
H1:        clamp(28px, 3.5vw, 52px)  weight 300, line-height 1.3
H2:        clamp(20px, 2.5vw, 32px)  weight 400
Body:      16-18px                    line-height 2.0 (very generous)
Label:     11px                       tracking 0.25em, small-caps
```

---

## Layout Principles

- **Ma (間):** Empty space is not absence — it is presence. Padding is measured in viewport height percentages, not pixels.
- Asymmetric but balanced: content placed with deliberate off-center positioning
- Single elements per viewport (one thing at a time)
- Content rarely exceeds 600px width, often narrower
- Vertical rhythm based on pure ratios (1:1.5, 1:2, 1:3)
- Thin lines (0.5px-1px) as the only decorative elements

---

## Motion Profile

- **Speed:** Very slow. Durations 1.2s-2.0s.
- **Ease:** `power2.inOut` — symmetrical, meditative
- **Lenis lerp:** 0.05 — the slowest profile, like breathing
- **Reveal:** Pure opacity — elements materialize from transparency
- **Parallax:** Very subtle (0.1 depth maximum)
- **No:** Any animation that announces itself

---

## Art Direction

**Primary:** Nothing. The whitespace is the art.  
**Secondary:** When imagery appears: a single, perfectly composed photograph or an ink-brushstroke SVG

**Single image principle:** If an image appears, it occupies its own viewport. The image is not competing with text. The text is not competing with the image.

```css
.zen-image-section {
  height: 100svh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.zen-image {
  max-width: 60vw;
  max-height: 70vh;
  filter: contrast(1.05);
}
```

**Ink brushstroke SVG:**
```html
<svg class="ink-stroke" viewBox="0 0 200 20">
  <path d="M0,10 Q50,2 100,10 Q150,18 200,10"
        stroke="#1a1a1a" stroke-width="1.5" fill="none" opacity="0.4"
        stroke-linecap="round"/>
</svg>
```

---

## Signature Elements

- **Excessive whitespace:** Section padding 200px minimum on desktop
- **One thing per scroll viewport:** Page sections contain one element
- **Thin horizontal line:** 0.5px, full-width, as the only section divider
- **Right-aligned navigation:** Sometimes vertical, right-fixed
- **Japanese numerals** as section markers: 一 二 三 (ichí, ni, san)

---

## Anti-Patterns

- **Never:** Multiple elements competing in one viewport
- **Never:** Bold or heavy font weights for body
- **Never:** Bright, saturated colors
- **Never:** Animations that move quickly
- **Never:** Drop shadows of any kind
- **Never:** Grid with more than 2 columns (usually 1)

---

## Component Recipes

### Zen Section
```css
.zen-section {
  min-height: 80svh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 160px 40px;
  text-align: center;
}

.zen-section h2 {
  font-size: clamp(28px, 3.5vw, 52px);
  font-weight: 300;
  line-height: 1.4;
  color: var(--color-fg);
  max-width: 16ch;
  letter-spacing: 0.02em;
}

.zen-section .zen-rule {
  width: 40px;
  height: 1px;
  background: var(--color-border);
  margin: 40px auto;
}
```

### Haiku Layout (three lines, decreasing size)
```html
<div class="haiku-text">
  <p class="haiku-line" style="font-size: 3em">The first moment</p>
  <p class="haiku-line" style="font-size: 2em; opacity: 0.7">passes into stillness</p>
  <p class="haiku-line" style="font-size: 1.2em; opacity: 0.4">after</p>
</div>
```
