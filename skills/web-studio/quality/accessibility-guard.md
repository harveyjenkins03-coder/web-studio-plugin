# Accessibility Guard

WCAG AA compliance checklist for Web Studio outputs. Run at Phase 5. Every item must pass before delivery.

---

## 1. Color Contrast

### Text contrast requirements (WCAG AA)

| Text type | Minimum ratio | Target ratio |
|-----------|--------------|--------------|
| Body text (16px+) | 4.5:1 | 7:1 |
| Large text (24px+ or 18.5px+ bold) | 3:1 | 4.5:1 |
| UI components (buttons, inputs, focus rings) | 3:1 | 4.5:1 |
| Decorative text / disabled | Exempt | N/A |

### Critical pairs to check

For every DNA profile, verify these specific pairs:

```
1. Body text color on background color
2. Muted/subtitle text on background color
3. Accent text (links, labels) on background color
4. White/light text on accent-colored buttons
5. Text on gradient backgrounds (check the lightest and darkest points)
6. Text on image overlays (check multiple crop positions)
```

### Implementation

```css
/* Always use CSS custom properties — they're testable */
.body-text { color: var(--color-fg); }           /* check fg on bg */
.muted-text { color: var(--color-fg-muted); }    /* check muted on bg */
.link { color: var(--color-accent); }             /* check accent on bg */

/* For gradient text — accessibility exception: must not convey unique information */
/* Screen readers see the underlying text color, not the gradient */
/* Safe: gradient text for decorative headings */
/* Unsafe: gradient text for body content or important labels */
```

### Quick check ratios (use browser DevTools or axe)
- Open DevTools → Elements → Accessibility tab → Show contrast ratio
- Or use `document.querySelector('p').style.color` and paste into contrast checker

---

## 2. Keyboard Navigation

### All interactive elements must be keyboard-accessible

```html
<!-- ✅ Correct: native button is keyboard-accessible -->
<button class="magnetic-btn">Get Started</button>

<!-- ❌ Wrong: div with click handler is not keyboard-accessible -->
<div class="magnetic-btn" onclick="handleClick()">Get Started</div>

<!-- If you must use a div for styling reasons: -->
<div class="magnetic-btn" role="button" tabindex="0"
     onclick="handleClick()"
     onkeydown="if(event.key==='Enter'||event.key===' ')handleClick()">
  Get Started
</div>
```

### Focus indicators must be visible

```css
/* Never remove outline without replacement */

/* ❌ Wrong */
:focus { outline: none; }
:focus-visible { outline: none; }

/* ✅ Correct: custom focus style */
:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  border-radius: 2px;
}

/* ✅ For elements that already have a visible focus style */
button:focus-visible {
  box-shadow: 0 0 0 3px var(--color-accent-30);
  outline: none;  /* OK because box-shadow provides visible indicator */
}
```

### Keyboard interaction requirements by component

| Component | Required keys |
|-----------|--------------|
| Links, buttons | Enter |
| Checkboxes, radio | Space to toggle |
| Select/dropdown | Arrow keys, Enter, Escape |
| Modal/dialog | Escape to close, Tab to cycle |
| Carousel | Arrow keys for prev/next |
| Tab component | Arrow keys to switch tabs |
| Menu | Arrow keys, Escape, Home/End |

### Custom cursor: keyboard-only users need visible focus
```css
/* When using custom cursor, ensure keyboard users still see focus */
:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 4px;
}

/* The custom cursor (pointer: cursor: none) only applies to mouse users */
@media (pointer: coarse) {
  * { cursor: auto; }
  .cursor, .cursor-follower { display: none; }
}
```

---

## 3. Semantic HTML

### Heading hierarchy
```html
<!-- ✅ Correct: one h1, hierarchical h2/h3 -->
<h1>Main page title</h1>
  <h2>Section title</h2>
    <h3>Subsection title</h3>
  <h2>Another section</h2>

<!-- ❌ Wrong: skip heading levels for visual size -->
<h1>Main page title</h1>
<h4>Big-looking subheading (just wanted it bigger)</h4>
<!-- Fix: use h2 and control size with CSS -->
```

### Landmark regions
```html
<header role="banner">
  <nav role="navigation" aria-label="Main">
    <!-- navigation links -->
  </nav>
</header>

<main role="main">
  <!-- Primary content -->
</main>

<aside role="complementary">
  <!-- Sidebar content -->
</aside>

<footer role="contentinfo">
  <!-- Footer content -->
</footer>
```

### Decorative vs. informative images
```html
<!-- Decorative (background, decoration) — empty alt -->
<img src="decorative-pattern.svg" alt="" aria-hidden="true" />

<!-- Informative (content) — descriptive alt -->
<img src="product-photo.jpg" alt="Matte black ceramic coffee mug with minimal handle" />

<!-- SVG icons used inline -->
<svg aria-hidden="true" focusable="false"><!-- decorative icon --></svg>

<!-- SVG with meaning -->
<svg role="img" aria-label="Success checkmark">
  <title>Success checkmark</title>
  <!-- paths -->
</svg>
```

---

## 4. Reduced Motion

### Respect `prefers-reduced-motion`

```css
/* ✅ CSS approach — instant transitions */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.001ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.001ms !important;
    scroll-behavior: auto !important;
  }
}
```

```js
/* ✅ JavaScript approach — conditional GSAP */
const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

if (!prefersReduced) {
  // All motion — parallax, scroll animations, GSAP
  initAnimations();
  initParallax();
  initLenis();
} else {
  // Instant reveal of all elements — no motion
  gsap.set('[data-reveal]', { opacity: 1, y: 0, x: 0, scale: 1, clipPath: 'inset(0%)' });
  // Standard browser scroll
}
```

**What to keep for reduced-motion users:**
- Static display of all content (nothing hidden behind animation)
- Hover states (short, subtle transitions are OK: < 200ms, no transforms)
- Color changes on hover (not translate/scale/rotate)

**What to remove:**
- Scroll-triggered reveals (show content immediately)
- Parallax effects
- Auto-playing carousels and marquees
- Looping background animations
- GSAP sequences and timelines

---

## 5. ARIA Labels & Roles

### Navigation
```html
<!-- Multiple nav landmarks need labels -->
<nav aria-label="Main navigation"><!-- ... --></nav>
<nav aria-label="Breadcrumb"><!-- ... --></nav>
<nav aria-label="Pagination"><!-- ... --></nav>
```

### Buttons without visible text
```html
<!-- Icon-only buttons MUST have accessible names -->
<button aria-label="Close dialog">
  <svg aria-hidden="true"><!-- X icon --></svg>
</button>

<button aria-label="Toggle menu">
  <svg aria-hidden="true"><!-- Hamburger icon --></svg>
</button>
```

### Custom interactive widgets
```html
<!-- Accordion -->
<button aria-expanded="false" aria-controls="panel-1">
  FAQ Question Text
</button>
<div id="panel-1" aria-hidden="true" hidden>
  Answer content
</div>

<!-- Tab panel -->
<div role="tablist" aria-label="Product categories">
  <button role="tab" aria-selected="true" aria-controls="panel-design">Design</button>
  <button role="tab" aria-selected="false" aria-controls="panel-dev">Development</button>
</div>
<div role="tabpanel" id="panel-design" tabindex="0"><!-- content --></div>
```

---

## 6. Form Accessibility

```html
<!-- ✅ Always associate label with input -->
<div class="form-group">
  <label for="email">Email address</label>
  <input type="email" id="email" name="email"
         autocomplete="email"
         aria-required="true"
         aria-describedby="email-hint" />
  <p id="email-hint" class="form-hint">We'll never share your email.</p>
</div>

<!-- ✅ Error states -->
<input type="email" id="email" aria-invalid="true" aria-describedby="email-error" />
<p id="email-error" role="alert">Please enter a valid email address.</p>

<!-- ❌ Never use placeholder as the only label -->
<input type="email" placeholder="Email address" />  <!-- no label = inaccessible -->
```

---

## Pass Checklist

- [ ] Body text contrast ratio ≥ 4.5:1 on all backgrounds
- [ ] Muted text contrast ratio ≥ 4.5:1 on all backgrounds
- [ ] All links and buttons keyboard-operable (Enter/Space)
- [ ] Visible focus indicator on all interactive elements
- [ ] One `<h1>` per page, heading hierarchy is sequential (no skips)
- [ ] Landmark regions present: `<header>`, `<main>`, `<footer>`, `<nav>`
- [ ] All images have alt text (empty string `""` for decorative)
- [ ] `prefers-reduced-motion` handled — content visible without animation
- [ ] Icon-only buttons have `aria-label`
- [ ] Forms have associated `<label>` for every input
- [ ] Custom cursor falls back gracefully (touch devices, keyboard-only)
- [ ] No information conveyed by color alone (icons + text supplement color coding)
