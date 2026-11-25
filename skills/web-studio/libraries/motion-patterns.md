# Motion Patterns — Choreography & System Design

How to design motion as a system, not a collection of animations. Covers page load sequencing, section transitions, scroll choreography, and the anti-patterns that produce generic AI sites.

---

## Motion Philosophy

Motion should feel like it's telling a story, not decorating a page. Every animation has a job:

- **Reveal:** "This content exists and deserves attention"
- **Guide:** "Look here next"
- **Confirm:** "Your action worked"
- **Express:** "This brand has this personality"

If an animation doesn't do one of these jobs, cut it.

---

## Page Load Sequence Architecture

Never start all animations at once. Build a reveal queue with deliberate timing:

```
Frame 0ms:    Body visible (no flash of unstyled content)
Frame 100ms:  Preloader/overlay starts exit
Frame 600ms:  Preloader exit complete
Frame 700ms:  Navigation items appear (stagger)
Frame 900ms:  Hero headline begins reveal
Frame 1100ms: Hero subtext appears
Frame 1300ms: Hero CTA fades up
Frame 1500ms: First scroll-trigger zone armed
```

**Rule:** Nothing scroll-triggered should fire until the page load sequence completes. Set `ScrollTrigger.normalizeScroll(true)` and delay arming by 1.5s.

### Preloader Patterns

#### Minimal count preloader
```js
class Preloader {
  constructor() {
    this.el = document.querySelector('.preloader');
    this.counter = document.querySelector('.preloader-count');
    this.count = 0;
    this.target = 100;
  }

  run() {
    return new Promise(resolve => {
      const tl = gsap.timeline({ onComplete: resolve });
      const increment = { val: 0 };

      tl.to(increment, {
        val: 100,
        duration: 1.8,
        ease: 'power2.inOut',
        onUpdate: () => {
          this.count = Math.round(increment.val);
          if (this.counter) this.counter.textContent = this.count;
        },
      })
      .to(this.el, {
        yPercent: -100,
        duration: 0.8,
        ease: 'power4.inOut',
      }, '-=0.2');
    });
  }
}

// Usage
const preloader = new Preloader();
preloader.run().then(() => {
  pageLoadSequence();
  ScrollTrigger.refresh();
});
```

#### Wipe preloader (left to right)
```js
gsap.to('.preloader', {
  clipPath: 'inset(0 100% 0 0)',
  duration: 0.8,
  ease: 'power4.inOut',
  onComplete: () => {
    document.querySelector('.preloader').remove();
    ScrollTrigger.refresh();
  },
});
```

---

## Section Transition System

### Sequential content reveal (scroll-based)
Every section should follow a consistent reveal order: background → headline → body → interactive.

```js
function setupSectionReveal(sectionSelector) {
  gsap.utils.toArray(sectionSelector).forEach(section => {
    const bg    = section.querySelector('[data-reveal="bg"]');
    const head  = section.querySelector('[data-reveal="head"]');
    const body  = section.querySelector('[data-reveal="body"]');
    const cta   = section.querySelector('[data-reveal="cta"]');

    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: section,
        start: 'top 70%',
        toggleActions: 'play none none none',
      },
    });

    if (bg)   tl.from(bg,   { opacity: 0, scale: 1.05, duration: 0.8, ease: 'power3.out' });
    if (head) tl.from(head, { y: 50, opacity: 0, duration: 0.7, ease: 'power3.out' }, '-=0.5');
    if (body) tl.from(body, { y: 30, opacity: 0, duration: 0.6, ease: 'power3.out' }, '-=0.5');
    if (cta)  tl.from(cta,  { y: 20, opacity: 0, duration: 0.5, ease: 'power3.out' }, '-=0.4');
  });
}
```

---

## Scroll Choreography — Narrative Arcs

Plan the full-page scroll story before implementing any individual animation.

### Arc: Dark Luxury (dark-luxe, art-deco-revival)
```
Section 1 — Hero:      Slow fade-up, weighted typography, gold accent pulse
Section 2 — About:     Image wipe left-to-right, text descends from above
Section 3 — Services:  Cards emerge from bottom at 20px stagger
Section 4 — Gallery:   Horizontal scroll panel, images clip-reveal
Section 5 — Testimonials: Crossfade carousel, text scramble
Section 6 — Contact:   Form elements cascade down, CTA glows
```

### Arc: Kinetic Energy (svz-kinetic, brutalist-pop)
```
Section 1 — Hero:      Text slams in (100ms, power4.out), background crash
Section 2 — Stats:     Numbers count up fast, borders draw on
Section 3 — Work:      Case study cards shear in diagonally
Section 4 — Process:   Timeline draws on scroll scrub
Section 5 — Contact:   Form revealed by clip-path wipe, fast
```

### Arc: Editorial Calm (editorial-serif, paper-ink)
```
Section 1 — Hero:      Line-by-line text unfurl, slow (2s)
Section 2 — Feature:   Image fades while text parallaxes
Section 3 — Grid:      Photos reveal in reading-order sequence
Section 4 — Quote:     Single word at a time, italic stagger
Section 5 — CTA:       Minimal fade, no transforms
```

### Arc: Organic Flow (organic-soft, warm-gradient)
```
Section 1 — Hero:      Gradient mesh morphs, text floats up softly
Section 2 — About:     Image has gentle parallax (0.2 depth)
Section 3 — Products:  Cards rise like bubbles (elastic ease)
Section 4 — Values:    Icons draw as SVG strokes on scroll
Section 5 — Contact:   Form fields reveal with spring physics
```

---

## Stagger Configuration Guide

| Context                    | stagger amount | ease            | Notes                          |
|----------------------------|----------------|-----------------|--------------------------------|
| Hero headline (chars)      | 0.015-0.025    | power4.out      | Fast, punchy                   |
| Hero headline (words)      | 0.06-0.1       | power3.out      | Deliberate                     |
| Nav items                  | 0.05           | power2.out      | Quick, utilitarian             |
| Cards in a grid (3-col)    | 0.1-0.14       | power3.out      | Reads as wave                  |
| Cards in a grid (4-col)    | 0.08-0.12      | power3.out      | Tighter to feel like one motion|
| List items                 | 0.06-0.09      | power2.out      | Reading pace                   |
| Icon set                   | 0.08           | back.out(1.5)   | Playful bounce                 |
| Stats/numbers              | 0.15           | power2.out      | Deliberate reveal              |
| Testimonial words          | 0.04           | power3.out      | Text-reading rhythm            |

### Stagger from options
```js
// From start (left to right, top to bottom)
stagger: { amount: 0.4, from: 'start' }

// From center outward
stagger: { amount: 0.4, from: 'center' }

// From end (right to left, bottom to top)
stagger: { amount: 0.4, from: 'end' }

// Random order
stagger: { amount: 0.4, from: 'random' }

// Grid-aware (for 2D layouts)
stagger: { amount: 0.5, from: 'center', grid: 'auto', axis: null }
```

---

## Duration Guide by DNA Profile

| DNA Profile        | Reveal duration | Hover duration | Ease family     |
|--------------------|-----------------|----------------|-----------------|
| dark-luxe          | 1.0-1.4s        | 0.4s           | power3-4.out    |
| editorial-serif    | 0.9-1.2s        | 0.3s           | power3.out      |
| brutalist-pop      | 0.3-0.5s        | 0.15s          | power4.out/in   |
| organic-soft       | 1.0-1.6s        | 0.5s           | power2.out      |
| neo-swiss          | 0.6-0.9s        | 0.25s          | power3.out      |
| apple-minimal      | 0.8-1.0s        | 0.3s           | power2.out      |
| cyber-dark         | 0.4-0.7s        | 0.2s           | power4.out      |
| candy-playful      | 0.5-0.8s        | 0.3s           | back.out(1.5)   |
| svz-kinetic        | 0.6-1.0s        | 0.25s          | power4.out      |
| japanese-minimal   | 1.0-1.5s        | 0.4s           | power2.inOut    |

---

## Reduced Motion System

```js
// Detect preference
const prefersReduced = window.matchMedia('(prefers-reduced-motion: reduce)');

// Conditional animation wrapper
function animate(target, vars, scrollVars) {
  if (prefersReduced.matches) {
    // Apply end state immediately — no motion
    gsap.set(target, {
      opacity: vars.opacity !== undefined ? 1 : undefined,
      y: vars.y !== undefined ? 0 : undefined,
      x: vars.x !== undefined ? 0 : undefined,
      scale: vars.scale !== undefined ? 1 : undefined,
    });
    return;
  }

  if (scrollVars) {
    return gsap.from(target, { ...vars, scrollTrigger: scrollVars });
  }
  return gsap.from(target, vars);
}

// Usage
animate('.headline', { y: 60, opacity: 0, duration: 0.9 }, {
  trigger: '.headline',
  start: 'top 80%',
});
```

**Rule:** Never use `@media (prefers-reduced-motion: reduce)` in CSS to hide content. Use it to switch to instant transitions (`transition-duration: 0.001ms`). The content must still be present and accessible.

---

## Anti-Patterns to Avoid

| Anti-Pattern | Why It's Wrong | Fix |
|---|---|---|
| Every element has opacity 0 on load | Page feels broken without JS | Show content, animate as enhancement |
| All animations start at `top 80%` | Feels mechanical and uniform | Vary `start` values per section rhythm |
| Same duration everywhere | No hierarchy of importance | Use longer durations for hero, shorter for supporting elements |
| Scroll-based transforms on text | Hard to read while scrolling | Parallax backgrounds only; text stays stable |
| Bounce ease on serious brands | Undermines credibility | Reserve `elastic/back` ease for playful DNA profiles only |
| Infinite looping animations | Distracting, no off-state | Animate on hover/enter, idle state is still |
| GSAP animating `width` or `height` | Triggers layout recalc | Use `scaleX`/`scaleY` with `transform-origin` |
