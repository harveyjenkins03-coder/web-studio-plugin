# SVG Illustrations

Inline SVG recipes, style vocabulary by DNA personality, animation integration, and theme-aware techniques for the Web Studio pipeline.

---

## A. SVG Style Vocabulary by DNA Personality

### Geometric (brutalist, neo-swiss, corporate-clean)

- **Lines**: Sharp, straight, precise. No curves unless mathematically defined (arcs, not beziers).
- **Shapes**: Rectangles, triangles, circles, hexagons. Perfect geometry.
- **Stroke**: Uniform weight, crisp endpoints (`stroke-linecap: butt`).
- **Fill**: Flat color, no gradients. High contrast between shapes.
- **Composition**: Grid-aligned, symmetrical or deliberately asymmetric by grid offset.
- **Spacing**: Consistent gaps, mathematical ratios (golden ratio, rule of thirds).

### Organic (organic-soft, japanese-minimal)

- **Lines**: Flowing curves, varying stroke width, hand-drawn feel.
- **Shapes**: Irregular blobs, leaf forms, natural silhouettes.
- **Stroke**: Tapered or variable width (`stroke-linecap: round`).
- **Fill**: Soft gradients, muted tones, subtle opacity layers.
- **Composition**: Asymmetric, flowing, breathing whitespace.
- **Spacing**: Irregular but balanced, negative space is intentional.

### Technical (cyber-dark, clean-tech)

- **Lines**: Circuit-like paths, right angles with small radius corners.
- **Shapes**: Rectangles, data-viz shapes (bar segments, arc segments), node-edge diagrams.
- **Stroke**: Thin (0.5-1px), precise, often dashed or dotted.
- **Fill**: Minimal fill, stroke-dominant. Glow effects via filter.
- **Composition**: Node-graph layouts, radial from center, grid with connections.
- **Details**: Small circles at intersections (nodes), arrow terminals.

### Decorative (art-deco, editorial-serif)

- **Lines**: Symmetrical, ornamental. Thin outer strokes with thick inner.
- **Shapes**: Fan shapes, sunbursts, chevrons, scallops, arches.
- **Stroke**: Varied weight for emphasis. Double-line borders.
- **Fill**: Metallic gradients (gold/silver), pattern fills.
- **Composition**: Bilateral symmetry, centered focal point, framed.
- **Details**: Repeating motifs, corner ornaments, divider flourishes.

### Playful (candy, retro-future)

- **Lines**: Rounded, bouncy, exaggerated proportions.
- **Shapes**: Rounded rectangles, pill shapes, stars, squircles.
- **Stroke**: Thick (2-4px), `stroke-linecap: round`, `stroke-linejoin: round`.
- **Fill**: Vivid solid colors, occasional playful gradients.
- **Composition**: Scattered, overlapping, slight rotation for dynamism.
- **Details**: Shadow layers offset, dotted accents, emoji-like simplicity.

---

## B. Inline SVG Recipes

### B1. Abstract Hero Composition

Overlapping geometric shapes using token colors. Designed as a hero section visual.

```html
<svg viewBox="0 0 800 600" fill="none" xmlns="http://www.w3.org/2000/svg"
     role="img" aria-label="Abstract decorative composition"
     style="width:100%;max-width:800px;">

  <!-- Large background circle -->
  <circle cx="350" cy="280" r="220" fill="var(--color-accent)" opacity="0.12" />

  <!-- Overlapping rectangle -->
  <rect x="280" y="120" width="320" height="280" rx="4"
        fill="var(--color-surface)" stroke="var(--color-muted)" stroke-width="1" opacity="0.6" />

  <!-- Accent diagonal line -->
  <line x1="200" y1="500" x2="600" y2="100"
        stroke="var(--color-accent)" stroke-width="2" opacity="0.5" />

  <!-- Small accent circle -->
  <circle cx="520" cy="200" r="60" fill="var(--color-accent2)" opacity="0.25" />

  <!-- Grid of dots -->
  <g opacity="0.3" fill="var(--color-muted)">
    <circle cx="100" cy="100" r="2" /><circle cx="130" cy="100" r="2" />
    <circle cx="160" cy="100" r="2" /><circle cx="190" cy="100" r="2" />
    <circle cx="100" cy="130" r="2" /><circle cx="130" cy="130" r="2" />
    <circle cx="160" cy="130" r="2" /><circle cx="190" cy="130" r="2" />
    <circle cx="100" cy="160" r="2" /><circle cx="130" cy="160" r="2" />
    <circle cx="160" cy="160" r="2" /><circle cx="190" cy="160" r="2" />
  </g>

  <!-- Accent stroke ring -->
  <circle cx="600" cy="420" r="80" fill="none"
          stroke="var(--color-accent)" stroke-width="1.5" stroke-dasharray="8 6" opacity="0.4" />

  <!-- Small filled square -->
  <rect x="150" y="400" width="40" height="40"
        fill="var(--color-accent2)" opacity="0.5" transform="rotate(15 170 420)" />
</svg>
```

---

### B2. Section Dividers (4 Variants)

**Wave divider:**

```html
<svg viewBox="0 0 1440 80" preserveAspectRatio="none" style="width:100%;display:block;">
  <path d="M0,40 C360,80 720,0 1080,40 C1260,60 1380,20 1440,40 L1440,80 L0,80 Z"
        fill="var(--color-surface)" />
</svg>
```

**Diagonal divider:**

```html
<svg viewBox="0 0 1440 80" preserveAspectRatio="none" style="width:100%;display:block;">
  <polygon points="0,80 1440,0 1440,80" fill="var(--color-surface)" />
</svg>
```

**Torn paper divider:**

```html
<svg viewBox="0 0 1440 60" preserveAspectRatio="none" style="width:100%;display:block;">
  <path d="M0,30 L60,28 L120,35 L180,25 L240,32 L300,20 L360,34 L420,26
           L480,38 L540,22 L600,30 L660,24 L720,36 L780,28 L840,33
           L900,21 L960,35 L1020,27 L1080,31 L1140,23 L1200,37 L1260,29
           L1320,34 L1380,26 L1440,30 L1440,60 L0,60 Z"
        fill="var(--color-surface)" />
</svg>
```

**Zigzag divider:**

```html
<svg viewBox="0 0 1440 40" preserveAspectRatio="none" style="width:100%;display:block;">
  <path d="M0,20 L48,0 L96,20 L144,0 L192,20 L240,0 L288,20 L336,0
           L384,20 L432,0 L480,20 L528,0 L576,20 L624,0 L672,20
           L720,0 L768,20 L816,0 L864,20 L912,0 L960,20 L1008,0
           L1056,20 L1104,0 L1152,20 L1200,0 L1248,20 L1296,0
           L1344,20 L1392,0 L1440,20 L1440,40 L0,40 Z"
        fill="var(--color-surface)" />
</svg>
```

**Usage**: Place between sections. Set `fill` to the next section background color. Add `transform: rotate(180deg)` for flipped orientation.

---

### B3. Decorative Border / Frame

Geometric and organic border variants for framing content.

**Geometric corner frame:**

```html
<svg viewBox="0 0 600 400" fill="none" style="position:absolute;inset:0;width:100%;height:100%;pointer-events:none;">
  <!-- Top-left corner -->
  <path d="M0,40 L0,0 L40,0" stroke="var(--color-accent)" stroke-width="2" />
  <!-- Top-right corner -->
  <path d="M560,0 L600,0 L600,40" stroke="var(--color-accent)" stroke-width="2" />
  <!-- Bottom-right corner -->
  <path d="M600,360 L600,400 L560,400" stroke="var(--color-accent)" stroke-width="2" />
  <!-- Bottom-left corner -->
  <path d="M40,400 L0,400 L0,360" stroke="var(--color-accent)" stroke-width="2" />
</svg>
```

**Organic flowing frame:**

```html
<svg viewBox="0 0 600 400" fill="none" style="position:absolute;inset:0;width:100%;height:100%;pointer-events:none;">
  <path d="M50,0 C150,-10 450,-10 550,0 C610,100 610,300 550,400
           C450,410 150,410 50,400 C-10,300 -10,100 50,0 Z"
        stroke="var(--color-accent)" stroke-width="1" opacity="0.3" />
</svg>
```

---

### B4. Icon Set Template

Consistent viewBox, stroke width, and sizing for a matching icon set.

```html
<!-- Base icon container: 24x24 viewBox, 1.5px stroke -->
<!-- All icons use currentColor so they inherit text color -->

<!-- Arrow right -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M5 12h14M12 5l7 7-7 7" />
</svg>

<!-- Menu / hamburger -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="1.5" stroke-linecap="round">
  <line x1="4" y1="7" x2="20" y2="7" />
  <line x1="4" y1="12" x2="20" y2="12" />
  <line x1="4" y1="17" x2="20" y2="17" />
</svg>

<!-- Close / X -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="1.5" stroke-linecap="round">
  <line x1="6" y1="6" x2="18" y2="18" />
  <line x1="18" y1="6" x2="6" y2="18" />
</svg>

<!-- External link -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <path d="M18 13v6a2 2 0 01-2 2H5a2 2 0 01-2-2V8a2 2 0 012-2h6M15 3h6v6M10 14L21 3" />
</svg>

<!-- Check / checkmark -->
<svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
     stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
  <polyline points="20 6 9 17 4 12" />
</svg>
```

**CSS for consistent icon styling:**

```css
.icon {
  width: 1.25em;
  height: 1.25em;
  vertical-align: -0.15em;
  stroke: currentColor;
  flex-shrink: 0;
}
.icon--sm { width: 1em; height: 1em; }
.icon--lg { width: 1.5em; height: 1.5em; }
.icon--accent { stroke: var(--color-accent); }
```

---

### B5. Background Pattern (SVG Pattern Element)

Repeating tile patterns using SVG `<pattern>` for seamless backgrounds.

**Dot grid pattern:**

```html
<svg width="100%" height="100%" style="position:absolute;inset:0;">
  <defs>
    <pattern id="dot-pattern" x="0" y="0" width="24" height="24" patternUnits="userSpaceOnUse">
      <circle cx="12" cy="12" r="1" fill="var(--color-muted)" opacity="0.4" />
    </pattern>
  </defs>
  <rect width="100%" height="100%" fill="url(#dot-pattern)" />
</svg>
```

**Cross-hatch pattern:**

```html
<svg width="100%" height="100%" style="position:absolute;inset:0;">
  <defs>
    <pattern id="crosshatch" width="16" height="16" patternUnits="userSpaceOnUse">
      <path d="M0,0 L16,16 M16,0 L0,16"
            stroke="var(--color-muted)" stroke-width="0.5" opacity="0.15" />
    </pattern>
  </defs>
  <rect width="100%" height="100%" fill="url(#crosshatch)" />
</svg>
```

**Diagonal lines pattern:**

```html
<svg width="100%" height="100%" style="position:absolute;inset:0;">
  <defs>
    <pattern id="diag-lines" width="8" height="8" patternUnits="userSpaceOnUse" patternTransform="rotate(45)">
      <line x1="0" y1="0" x2="0" y2="8"
            stroke="var(--color-muted)" stroke-width="0.5" opacity="0.2" />
    </pattern>
  </defs>
  <rect width="100%" height="100%" fill="url(#diag-lines)" />
</svg>
```

---

### B6. Abstract Data Visualization

Decorative chart-inspired shapes. Not functional charts --- purely aesthetic elements.

```html
<svg viewBox="0 0 400 200" fill="none" style="width:100%;max-width:400px;"
     role="img" aria-label="Decorative abstract chart">

  <!-- Bar chart silhouette -->
  <rect x="20"  y="120" width="30" height="80" rx="2" fill="var(--color-accent)" opacity="0.2" />
  <rect x="60"  y="80"  width="30" height="120" rx="2" fill="var(--color-accent)" opacity="0.35" />
  <rect x="100" y="40"  width="30" height="160" rx="2" fill="var(--color-accent)" opacity="0.5" />
  <rect x="140" y="60"  width="30" height="140" rx="2" fill="var(--color-accent)" opacity="0.4" />
  <rect x="180" y="20"  width="30" height="180" rx="2" fill="var(--color-accent)" opacity="0.65" />

  <!-- Trend line -->
  <polyline points="35,120 75,80 115,40 155,60 195,20"
            stroke="var(--color-accent2)" stroke-width="2" stroke-linecap="round"
            stroke-linejoin="round" />

  <!-- Data points -->
  <circle cx="35"  cy="120" r="4" fill="var(--color-accent2)" />
  <circle cx="75"  cy="80"  r="4" fill="var(--color-accent2)" />
  <circle cx="115" cy="40"  r="4" fill="var(--color-accent2)" />
  <circle cx="155" cy="60"  r="4" fill="var(--color-accent2)" />
  <circle cx="195" cy="20"  r="4" fill="var(--color-accent2)" />

  <!-- Donut chart segment -->
  <circle cx="320" cy="100" r="60" fill="none"
          stroke="var(--color-surface)" stroke-width="20" />
  <circle cx="320" cy="100" r="60" fill="none"
          stroke="var(--color-accent)" stroke-width="20"
          stroke-dasharray="220 157" stroke-dashoffset="0"
          transform="rotate(-90 320 100)" />
  <circle cx="320" cy="100" r="60" fill="none"
          stroke="var(--color-accent2)" stroke-width="20"
          stroke-dasharray="80 297" stroke-dashoffset="-220"
          transform="rotate(-90 320 100)" />
</svg>
```

---

## C. Animation Integration

### Path Drawing (stroke-dasharray)

Animates SVG paths as if being drawn. Works with any `<path>`, `<line>`, `<polyline>`, or `<circle>`.

```css
.draw-in {
  stroke-dasharray: 1000;
  stroke-dashoffset: 1000;
  animation: draw-path 2s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
@keyframes draw-path {
  to { stroke-dashoffset: 0; }
}
```

**GSAP version (more control, dynamic path lengths):**

```js
document.querySelectorAll('.draw-in').forEach(el => {
  const length = el.getTotalLength();
  gsap.set(el, { strokeDasharray: length, strokeDashoffset: length });
  gsap.to(el, {
    strokeDashoffset: 0,
    duration: 2,
    ease: 'power3.out',
    scrollTrigger: {
      trigger: el.closest('svg'),
      start: 'top 80%',
    }
  });
});
```

### GSAP Morphing (Shape Transformation)

Smoothly morph between two SVG paths. Requires `MorphSVGPlugin` (GSAP Club) or `flubber` library.

**With flubber (free alternative):**

```html
<script src="https://unpkg.com/flubber@0.4.2/flubber.min.js"></script>
<script>
  const path1 = 'M10,80 Q95,10 180,80 Q95,150 10,80 Z';  // Leaf
  const path2 = 'M10,95 L95,10 L180,95 L95,180 Z';        // Diamond

  const interpolator = flubber.interpolate(path1, path2);
  const pathEl = document.getElementById('morph-target');

  gsap.to({ t: 0 }, {
    t: 1,
    duration: 1.5,
    ease: 'power2.inOut',
    onUpdate: function() {
      pathEl.setAttribute('d', interpolator(this.targets()[0].t));
    },
    scrollTrigger: {
      trigger: pathEl.closest('svg'),
      start: 'top center',
      end: 'bottom center',
      scrub: true,
    }
  });
</script>
```

### Staggered Fade-In

Animate SVG child elements one by one with GSAP stagger.

```js
gsap.from('#hero-svg > *', {
  opacity: 0,
  y: 20,
  scale: 0.8,
  duration: 0.6,
  stagger: 0.08,
  ease: 'power3.out',
  scrollTrigger: {
    trigger: '#hero-svg',
    start: 'top 80%',
  }
});
```

**CSS-only stagger (no JS needed, limited control):**

```css
#hero-svg > * {
  opacity: 0;
  animation: svg-fade-in 0.6s ease forwards;
}
#hero-svg > *:nth-child(1) { animation-delay: 0s; }
#hero-svg > *:nth-child(2) { animation-delay: 0.08s; }
#hero-svg > *:nth-child(3) { animation-delay: 0.16s; }
#hero-svg > *:nth-child(4) { animation-delay: 0.24s; }
#hero-svg > *:nth-child(5) { animation-delay: 0.32s; }
#hero-svg > *:nth-child(6) { animation-delay: 0.40s; }

@keyframes svg-fade-in {
  from { opacity: 0; transform: translateY(10px) scale(0.9); }
  to   { opacity: 1; transform: translateY(0) scale(1); }
}
```

### Scroll-Driven Progression

Tie SVG animation progress to scroll position.

```js
// Draw a path as user scrolls through the section
const path = document.getElementById('progress-path');
const length = path.getTotalLength();

gsap.set(path, { strokeDasharray: length, strokeDashoffset: length });

gsap.to(path, {
  strokeDashoffset: 0,
  ease: 'none',
  scrollTrigger: {
    trigger: '#progress-section',
    start: 'top top',
    end: 'bottom bottom',
    scrub: 0.5,
  }
});
```

**Reveal shapes on scroll with clip-path:**

```js
gsap.from('.scroll-reveal-svg', {
  clipPath: 'inset(100% 0% 0% 0%)',
  duration: 1,
  ease: 'power3.out',
  scrollTrigger: {
    trigger: '.scroll-reveal-svg',
    start: 'top 80%',
  }
});
```

---

## D. Theme Awareness

### Using CSS Custom Properties in SVG

SVGs can read CSS custom properties via `var()` in inline SVG attributes and via `currentColor`.

**Direct var() usage (inline SVG only):**

```html
<svg viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="40" fill="var(--color-accent)" />
  <rect x="10" y="10" width="80" height="80" fill="none"
        stroke="var(--color-muted)" stroke-width="1" />
</svg>
```

**currentColor inheritance:**

```html
<style>
  .themed-icon { color: var(--color-accent); }
  .themed-icon svg { stroke: currentColor; fill: none; }
</style>

<span class="themed-icon">
  <svg width="24" height="24" viewBox="0 0 24 24" stroke-width="1.5">
    <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5" />
  </svg>
</span>
```

### Dark/Light Theme Switching

SVG elements that adapt when the theme changes:

```css
:root {
  --color-bg: #f8f8f8;
  --color-text: #1a1a1a;
  --color-accent: #2563eb;
}
:root[data-theme="dark"] {
  --color-bg: #0a0a0a;
  --color-text: #f0f0f0;
  --color-accent: #60a5fa;
}
```

Since inline SVGs use `var()`, they automatically update when custom properties change. No JavaScript needed for theme switching --- just toggle `data-theme` on `<html>`.

**For external SVG files** (which cannot read CSS vars), use CSS filters:

```css
[data-theme="dark"] .external-svg {
  filter: invert(1) hue-rotate(180deg);
}
```

### Accessibility

Always include accessibility attributes on decorative and informative SVGs:

```html
<!-- Decorative (ignored by screen readers) -->
<svg aria-hidden="true" focusable="false">...</svg>

<!-- Informative (announced by screen readers) -->
<svg role="img" aria-label="Company growth chart showing 40% increase">
  <title>Growth Chart</title>
  ...
</svg>
```

---

## E. Recipe Pairing by DNA Profile

| DNA Profile | Hero Composition | Divider | Pattern | Icons | Animation |
|-------------|-----------------|---------|---------|-------|-----------|
| brutalist | Sharp overlapping rects | Diagonal | Cross-hatch | Thick stroke, butt cap | Instant reveal |
| neo-swiss | Precise circles + lines | None (clean break) | Dot grid | Thin stroke, precise | Draw-in path |
| corporate-clean | Subtle geometric shapes | Wave | Dot grid | Standard weight | Fade stagger |
| cyber-dark | Glowing circuit nodes | Zigzag | Diagonal lines | Thin + glow filter | Draw-in + pulse |
| clean-tech | Minimal shapes, lots of space | Wave | Dot grid | Thin stroke, round cap | Soft fade |
| organic-soft | Flowing blob shapes | Torn paper | None | Round cap, varied weight | Morph + float |
| japanese-minimal | Single stroke, max whitespace | None | None | Hairline stroke | Slow draw-in |
| art-deco | Symmetrical sunburst | Zigzag | Cross-hatch | Decorative, varied | Stagger reveal |
| editorial-serif | Thin lines + typography | Diagonal | Diagonal lines | Thin stroke | Draw-in path |
| candy | Rounded, colorful shapes | Wave | Dot grid (large) | Thick, round, bouncy | Bounce stagger |
| retro-future | Neon-style stroke shapes | Zigzag | Diagonal lines | Thick + glow | Pulse + draw |
