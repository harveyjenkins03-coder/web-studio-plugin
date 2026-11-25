# Lenis Smooth Scroll Patterns

Production-ready patterns for Lenis smooth scrolling. Covers setup, GSAP integration, scroll-to navigation, direction detection, enable/disable control, mobile handling, and common pitfalls.

---

## 1. Setup

### CDN (script tag)

```html
<script src="https://unpkg.com/lenis@1/dist/lenis.min.js"></script>
<link rel="stylesheet" href="https://unpkg.com/lenis@1/dist/lenis.css" />

<script>
  const lenis = new Lenis({
    lerp: 0.1,
    duration: 1.2,
    smoothWheel: true,
  });

  function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  }
  requestAnimationFrame(raf);
</script>
```

### Lerp Values by DNA Profile

| DNA Profile        | lerp  | Feel                              |
|--------------------|-------|-----------------------------------|
| dark-luxe          | 0.06  | Ultra-slow, heavy, luxurious      |
| editorial-serif    | 0.08  | Deliberate, magazine-like         |
| apple-minimal      | 0.10  | Smooth but responsive             |
| brutalist-pop      | 0.15  | Snappier, raw energy              |
| organic-soft       | 0.07  | Floating, dreamy                  |
| svz-kinetic        | 0.08  | Cinematic weight                  |
| clean-tech         | 0.12  | Efficient, crisp                  |
| candy-playful      | 0.14  | Bouncy, energetic                 |

---

## 2. GSAP ScrollTrigger Integration

Always sync Lenis with ScrollTrigger — without this, scroll-based animations will desync.

```js
const lenis = new Lenis({ lerp: 0.08, duration: 1.2, smoothWheel: true });

// Route Lenis scroll events to ScrollTrigger
lenis.on('scroll', ScrollTrigger.update);

// Use GSAP ticker instead of rAF for synchronized updates
gsap.ticker.add(time => lenis.raf(time * 1000));
gsap.ticker.lagSmoothing(0);
```

**Critical:** Remove any separate `requestAnimationFrame(raf)` loop when using GSAP ticker. Pick one or the other.

---

## 3. Scroll-To Navigation

### Smooth anchor links
```js
// Override all anchor clicks with Lenis scroll-to
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', e => {
    e.preventDefault();
    const target = document.querySelector(anchor.getAttribute('href'));
    if (target) {
      lenis.scrollTo(target, {
        offset: -80,       // account for sticky nav height
        duration: 1.5,
        easing: t => Math.min(1, 1.001 - Math.pow(2, -10 * t)),  // expo ease
      });
    }
  });
});
```

### Programmatic scroll
```js
// Scroll to element
lenis.scrollTo('#contact', { duration: 1.2 });

// Scroll to top
lenis.scrollTo(0, { duration: 1.0, immediate: false });

// Scroll to position
lenis.scrollTo(1200, { duration: 1.5 });

// Immediate (no animation)
lenis.scrollTo('#section', { immediate: true });
```

---

## 4. Scroll Direction Detection

Useful for show/hide nav, reverse animations, and directional reveals.

```js
let lastScrollY = 0;
let scrollDirection = 'down';

lenis.on('scroll', ({ scroll, direction }) => {
  // direction is 1 (down) or -1 (up) — use directly
  scrollDirection = direction === 1 ? 'down' : 'up';

  // Or compute from position
  scrollDirection = scroll > lastScrollY ? 'down' : 'up';
  lastScrollY = scroll;
});

// Hide nav on scroll down, show on scroll up
lenis.on('scroll', ({ direction }) => {
  const nav = document.querySelector('.nav');
  if (direction === 1) {
    gsap.to(nav, { yPercent: -100, duration: 0.4, ease: 'power2.in' });
  } else {
    gsap.to(nav, { yPercent: 0, duration: 0.4, ease: 'power2.out' });
  }
});
```

---

## 5. Enable / Disable Control

Disable Lenis during modals, menus, or carousels:

```js
// Disable scroll
function lockScroll() {
  lenis.stop();
}

// Re-enable scroll
function unlockScroll() {
  lenis.start();
}

// Menu open/close pattern
const menuToggle = document.querySelector('.menu-toggle');
const menu = document.querySelector('.menu');
let menuOpen = false;

menuToggle.addEventListener('click', () => {
  menuOpen = !menuOpen;

  if (menuOpen) {
    lenis.stop();
    gsap.to(menu, { opacity: 1, pointerEvents: 'all', duration: 0.4 });
  } else {
    lenis.start();
    gsap.to(menu, { opacity: 0, pointerEvents: 'none', duration: 0.3 });
  }
});
```

---

## 6. Scroll Progress Tracking

```js
// Get scroll progress (0 to 1) for a custom progress bar
const progressBar = document.querySelector('.scroll-progress');

lenis.on('scroll', ({ progress }) => {
  gsap.set(progressBar, { scaleX: progress, transformOrigin: 'left' });
});

// Percentage display
lenis.on('scroll', ({ scroll, limit }) => {
  const pct = Math.round((scroll / limit) * 100);
  document.querySelector('.scroll-pct').textContent = pct + '%';
});
```

---

## 7. Per-Element Smooth Scroll Override

```html
<!-- Disable Lenis on a specific scrollable container -->
<div data-lenis-prevent>
  <!-- This element uses native scroll -->
</div>

<!-- Prevent wheel from propagating to Lenis -->
<div data-lenis-prevent-wheel>
  <!-- Wheel events stop here -->
</div>
```

---

## 8. Mobile Handling

Lenis smooth scroll on mobile can feel wrong. Disable on touch devices:

```js
const isTouchDevice = window.matchMedia('(hover: none) and (pointer: coarse)').matches;

const lenis = new Lenis({
  lerp: 0.08,
  duration: 1.2,
  smoothWheel: !isTouchDevice,  // native scroll on mobile
  touchMultiplier: 2,
});
```

Or use the device check:
```js
if (navigator.maxTouchPoints === 0) {
  // Desktop: enable Lenis
  initLenis();
} else {
  // Mobile/tablet: native scroll, still add ScrollTrigger
  gsap.ticker.add(() => ScrollTrigger.update());
}
```

---

## 9. Parallax with Lenis

```js
// Lenis gives you the raw scroll value — use it for custom parallax
lenis.on('scroll', ({ scroll }) => {
  const parallaxEls = document.querySelectorAll('[data-parallax]');
  parallaxEls.forEach(el => {
    const depth = parseFloat(el.dataset.parallax) || 0.3;
    gsap.set(el, { y: scroll * depth });
  });
});
```

---

## 10. Common Pitfalls

| Problem | Cause | Fix |
|---------|-------|-----|
| ScrollTrigger fires at wrong positions | Lenis and ScrollTrigger not synced | Add `lenis.on('scroll', ScrollTrigger.update)` |
| Jerky scroll on page load | Lenis fighting GSAP ticker | Use `gsap.ticker.add()` not `requestAnimationFrame` |
| `position: sticky` not working | Lenis changes scroll container | Add `data-lenis-prevent` to sticky parent |
| Scroll doesn't stop at end | `lerp` too low, overshoots | Increase `lerp` to 0.12-0.15, or set `overscroll: false` |
| Mobile feels delayed | Too-low lerp on touch | Disable smooth scroll on touch, use `touchMultiplier` instead |
| Menu can still scroll behind it | Forgot to call `lenis.stop()` | Call `lenis.stop()` on menu open |
