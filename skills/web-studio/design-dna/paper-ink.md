# DNA Profile: Paper & Ink

**Category:** Light / Ultra-Minimal  
**Mood:** Black ink on white paper, typography as the only art form needed

---

## Emotional Target

The site achieves presence through absence. No colors compete. The typography and spacing carry the entire emotional weight. It feels authoritative, literary, like something worth reading slowly.

Design references: Emigre magazine, Massimo Vignelli's books, The Paris Review, ACNE Studios, Celine digital, Craig & Karl typography

---

## Color System

```
Background:    #faf9f7 (not pure white — warm, like quality paper)
Surface:       #f0ede8
Border:        #e0dbd3
Foreground:    #141210 (ink-warm near-black)
Muted:         #8a8580
Accent:        #141210 (black IS the accent — no chromatic color)
Accent 2:      #c41e3a (only appears as a single, rare punctuation moment)
```

---

## Typography

**Display:**
- Canela — weight 300, sometimes Italic
- Domaine Display — weight 300
- Garamond Premier Pro — weight 400 Italic

**Body:**
- Mercury Text G4 — weight 400
- Freight Text Pro — weight 400
- Garamond Premier Pro — weight 400

**Utility:**
- Suisse Int'l — weight 300, very wide tracking

**Size system:**
```
Display:   clamp(72px, 12vw, 200px)   weight 300
H1:        clamp(48px, 6vw, 96px)     weight 300-400
H2:        clamp(24px, 3vw, 40px)     weight 400
Body:      18-20px                     weight 400, line-height 1.95
Footnote:  13px                        muted
```

---

## Layout Principles

- Maximum content width: 740px (books don't go full-screen)
- Generous margins carry the whitespace load
- One typeface family maximum (the type is the design)
- Long reading experiences: articles, essays, long-form copy
- Mathematical proportions from book design (3:5, 2:3 ratios)
- Punctuation and dashes as decorative elements (em dash —, ellipsis …)

---

## Motion Profile

- **Speed:** Slowest of all profiles. Durations 1.2s-2.0s.
- **Ease:** `power2.inOut` — symmetrical, like turning a page
- **Lenis lerp:** 0.06 — the page turns slowly
- **Reveal:** Pure opacity fades — no position transforms (text doesn't move)
- **No:** Parallax, rotation, scale, clip effects — the text simply appears

---

## Art Direction

**Art:** None. The typography is the art.  
**Decoration:** A single thin rule, a well-placed em dash, intentional whitespace.

If an image is used:
```css
.paper-image {
  filter: grayscale(100%) contrast(1.05);
  /* Full grayscale — images become ink, not photographs */
}
```

---

## Signature Elements

- **Oversized first paragraph initial** (not a drop cap — a large first word/letter treatment)
- **Chapter/section markers:** Roman numerals (I, II, III) or em dashes
- **Running margins:** Annotations in the margin gutter (small, muted text)
- **Footnotes:** Styled visually like actual academic footnotes
- **No hover effects:** Underline on links only, no color change needed

---

## Anti-Patterns

- **Never:** Chromatic colors (except the single crimson accent, rare)
- **Never:** Sans-serif display fonts
- **Never:** Motion that draws attention to itself
- **Never:** Cards, tiles, or grid layouts
- **Never:** Icons of any kind
- **Never:** Background colors except white/near-white

---

## Component Recipes

### Article/Essay Layout
```css
.article {
  max-width: 680px;
  margin: 0 auto;
  padding: 80px 24px;
}

.article h1 {
  font-family: var(--font-display);
  font-size: clamp(48px, 6vw, 80px);
  font-weight: 300;
  line-height: 1.1;
  margin-bottom: 0.5em;
}

.article .byline {
  font-size: 13px;
  color: var(--color-muted);
  text-transform: uppercase;
  letter-spacing: 0.12em;
  margin-bottom: 3em;
}

.article p {
  font-family: var(--font-body);
  font-size: 19px;
  line-height: 1.9;
  color: var(--color-fg);
  margin-bottom: 1.5em;
}

.article p + p { text-indent: 1.5em; }
```

### Margin Annotation
```html
<article class="article">
  <p class="has-annotation">
    The most important sentence in the paragraph.
    <span class="margin-note">This note appears in the margin</span>
  </p>
</article>
```

```css
@media (min-width: 1100px) {
  .article { position: relative; }
  .margin-note {
    position: absolute;
    left: calc(100% + 40px);
    width: 200px;
    font-size: 12px;
    color: var(--color-muted);
    line-height: 1.6;
    font-style: italic;
  }
}
```
