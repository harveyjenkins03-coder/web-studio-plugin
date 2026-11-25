# Performance Budget

Performance targets and implementation patterns for Web Studio outputs. Heavy animation libraries require deliberate loading strategies. Every pattern here protects Core Web Vitals.

---

## Targets

| Metric | Target | Critical Threshold |
|--------|--------|-------------------|
| LCP (Largest Contentful Paint) | < 2.5s | < 4.0s |
| FID / INP | < 100ms | < 200ms |
| CLS (Cumulative Layout Shift) | < 0.1 | < 0.25 |
| Total JS (parsed + executed) | < 400KB gzip | < 700KB gzip |
| Total CSS | < 50KB gzip | < 100KB gzip |
| Font files | < 150KB total | < 250KB |
| Images above fold | Properly sized + format | No unoptimized JPEGs |
| Time to Interactive | < 3.5s | < 5.0s |

---

## Library Loading Strategy

### Load order matters

```html
<!-- 1. Critical CSS inline (only above-fold styles) -->
<style>
  /* Inline only: CSS custom properties, body/html, nav, hero */
  /* Everything else loads from stylesheet */
</style>

<!-- 2. Main stylesheet — async or early in head -->
<link rel="stylesheet" href="styles.css" />

<!-- 3. Preconnect to CDN hosts early -->
<link rel="preconnect" href="https://cdnjs.cloudflare.com" />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link rel="preconnect" href="https://unpkg.com" />

<!-- 4. Fonts — preload the display font to prevent FOIT -->
<link rel="preload" as="font" type="font/woff2"
      href="https://fonts.gstatic.com/s/[font-file].woff2" crossorigin />

<!-- 5. GSAP core — in head for above-fold animations -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>

<!-- 6. GSAP plugins — defer until after parse -->
<script defer src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script defer src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/SplitText.min.js"></script>

<!-- 7. Lenis — defer -->
<script defer src="https://unpkg.com/lenis@1/dist/lenis.min.js"></script>

<!-- 8. Three.js — loaded as module, imported only in sections that need it -->
<!-- Don't load globally — import in the specific script that needs it -->

<!-- 9. Main JS — defer, last -->
<script defer src="main.js"></script>
```

### Three.js: Load only when visible

```js
// Don't load Three.js on page load — load when the 3D section enters viewport
const threeSection = document.querySelector('.three-section');

const observer = new IntersectionObserver((entries) => {
  if (entries[0].isIntersecting) {
    observer.disconnect();

    // Dynamically import Three.js only when needed
    import('https://cdn.jsdelivr.net/npm/three@0.166/build/three.module.js').then(THREE => {
      initThreeScene(THREE, threeSection.querySelector('canvas'));
    });
  }
}, { rootMargin: '200px' });  // Start loading 200px before visible

observer.observe(threeSection);
```

---

## Font Loading

### Critical font path
```html
<!-- Step 1: preconnect to font CDN -->
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />

<!-- Step 2: load font with display=swap -->
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap" rel="stylesheet" />
```

### CSS font stack with fallback
```css
/* Always include a stack — text renders immediately with fallback, swaps when loaded */
--font-display: 'Bebas Neue', 'Arial Black', system-ui;
--font-body:    'DM Sans', system-ui, -apple-system, sans-serif;
--font-mono:    'JetBrains Mono', 'Fira Code', monospace;

body {
  font-family: var(--font-body);
  /* Size-adjust prevents layout shift on font swap */
  font-display: swap;
}
```

### Font subsetting (if self-hosting)
```css
/* Load only Latin characters — reduces font file size by 60-80% */
@font-face {
  font-family: 'Custom Font';
  src: url('/fonts/custom-latin.woff2') format('woff2');
  font-display: swap;
  unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}
```

### Prevent layout shift from font loading (CLS fix)
```css
/* Reserve exact line-height space before font loads */
h1 {
  font-size: clamp(48px, 8vw, 120px);
  line-height: 1;
  min-height: 1lh;  /* Reserve space before font loads */
}
```

---

## Animation Performance

### GPU-composited properties only
```css
/* ✅ These properties use GPU compositing — no layout recalc */
transform: translateX() translateY() scale() rotate() perspective()
opacity: 0 to 1

/* ❌ These trigger layout recalc — avoid in animations */
width, height, margin, padding, top, left, right, bottom
font-size, line-height
display, position
```

### will-change for animated elements
```css
/* Add before animation starts, remove after */
.animating {
  will-change: transform, opacity;
}

/* In JavaScript */
el.style.willChange = 'transform, opacity';
// After animation:
el.style.willChange = 'auto';
```

### IntersectionObserver for lazy animation arming
```js
// Don't arm all ScrollTriggers at once — arm as sections enter viewport
function lazyArmAnimations() {
  const sections = document.querySelectorAll('.animate-section');

  const io = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        armSectionAnimations(entry.target);
        io.unobserve(entry.target);
      }
    });
  }, { rootMargin: '100px' });

  sections.forEach(section => io.observe(section));
}
```

### Throttle mouse events
```js
// Mouse-follow effects need throttling — mousemove fires 60-120/sec
let mouseFrame;
document.addEventListener('mousemove', e => {
  if (mouseFrame) return;  // Skip if last frame not rendered
  mouseFrame = requestAnimationFrame(() => {
    updateCursorPosition(e.clientX, e.clientY);
    mouseFrame = null;
  });
});

// For GSAP quickTo — preferred over addEventListener for mouse
const xTo = gsap.quickTo('.cursor', 'x', { duration: 0.2, ease: 'power2.out' });
const yTo = gsap.quickTo('.cursor', 'y', { duration: 0.2, ease: 'power2.out' });
document.addEventListener('mousemove', e => { xTo(e.clientX); yTo(e.clientY); });
```

---

## Image Optimization

### Always include width and height attributes (CLS prevention)
```html
<!-- ✅ Prevents CLS — browser reserves space before load -->
<img src="hero.jpg" width="1200" height="800" alt="..." loading="lazy" />

<!-- ❌ No dimensions — causes layout shift -->
<img src="hero.jpg" alt="..." />
```

### Above-fold images: preload
```html
<link rel="preload" as="image" href="hero.webp" />
<img src="hero.webp" width="1200" height="800" alt="..." />
```

### Below-fold images: lazy load
```html
<img src="section-photo.webp" width="800" height="600" alt="..."
     loading="lazy" decoding="async" />
```

### Modern formats
```html
<!-- Prefer WebP with JPEG fallback -->
<picture>
  <source srcset="image.webp" type="image/webp" />
  <source srcset="image.jpg" type="image/jpeg" />
  <img src="image.jpg" width="800" height="600" alt="..." />
</picture>
```

### Responsive images
```html
<img
  srcset="image-400.webp 400w, image-800.webp 800w, image-1200.webp 1200w"
  sizes="(max-width: 600px) 400px, (max-width: 1000px) 800px, 1200px"
  src="image-800.webp"
  width="1200"
  height="800"
  alt="..."
/>
```

---

## SVG and CSS Art Performance

SVGs generated inline have no network cost. Prioritize them for decorative elements.

```html
<!-- ✅ Inline SVG: renders immediately, fully styleable, zero network -->
<svg viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg">
  <!-- complex paths here -->
</svg>

<!-- ✅ CSS art: pure GPU, no assets -->
.hero-orb {
  background: radial-gradient(...);
  border-radius: 50%;
  filter: blur(80px);
}
```

### Canvas / WebGL performance
```js
// Always limit pixel ratio
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

// Pause when off-screen
const io = new IntersectionObserver(([entry]) => {
  if (entry.isIntersecting) {
    startAnimationLoop();
  } else {
    stopAnimationLoop();
  }
});
io.observe(canvas);

// Dispose resources on destroy
function cleanup() {
  geometry.dispose();
  material.dispose();
  renderer.dispose();
  io.disconnect();
}
```

---

## Critical Rendering Path

### Above-the-fold CSS must be fast
1. CSS custom properties (tokens): < 1KB
2. Reset/base styles: < 3KB
3. Header + nav: < 5KB
4. Hero section: < 8KB
5. Total above-fold CSS: < 20KB

### JS execution order
```
Page load:
  1. HTML parses
  2. CSS loads (render blocking — keep small)
  3. Fonts preconnect
  4. GSAP core loads (in <head> for above-fold animations)
  5. HTML renders
  6. Deferred scripts execute: ScrollTrigger, SplitText, Lenis, main.js
  7. DOMContentLoaded: init animations, arm ScrollTriggers
  8. Load event: ScrollTrigger.refresh()
```

```js
// Always refresh ScrollTrigger after all content loads
window.addEventListener('load', () => {
  ScrollTrigger.refresh();
});

// And after fonts load (prevents wrong positions)
document.fonts.ready.then(() => {
  ScrollTrigger.refresh();
});
```

---

## Performance Audit Checklist

- [ ] No render-blocking resources (all JS is defer or async except critical)
- [ ] Display font is preloaded with `<link rel="preload">`
- [ ] All images have `width` and `height` attributes
- [ ] Above-fold images have no `loading="lazy"` (they should load immediately)
- [ ] Below-fold images all have `loading="lazy" decoding="async"`
- [ ] Three.js loads only when 3D section enters viewport
- [ ] `will-change` applied to animated elements, removed after
- [ ] Mouse-following effects use `requestAnimationFrame` throttle or `gsap.quickTo()`
- [ ] Canvas/WebGL animation pauses when off-screen
- [ ] `ScrollTrigger.refresh()` called after `window.load` and `document.fonts.ready`
- [ ] No CSS transitions on `width`, `height`, `margin`, `padding`, `top/left/bottom/right`
- [ ] Canvas pixel ratio capped at 2
