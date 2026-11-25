# GSAP Patterns Library

Production-ready GSAP recipes for Phase 4 (Motion & Interaction). Every pattern here targets Awwwards/SVZ quality. Copy, adapt to design tokens, ship.

---

## Setup & Registration

Always register plugins before use. Load from CDN in this order:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/SplitText.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/CustomEase.min.js"></script>
```

```js
gsap.registerPlugin(ScrollTrigger, SplitText, CustomEase);

// Global defaults — run once at top of JS
gsap.defaults({ ease: 'power3.out', duration: 0.9 });

// Custom eases — define once, use everywhere
CustomEase.create('smooth', 'M0,0 C0.25,0.1 0.25,1 1,1');
CustomEase.create('snappy', 'M0,0 C0.5,0 0.5,1 1,1');
CustomEase.create('elastic-out', 'M0,0 C0.14,0 0.242,0.438 0.272,0.561 0.313,0.728 0.354,0.963 0.362,1 0.37,1.037 0.414,1.062 0.468,1.062 0.522,1.062 0.57,1.03 0.578,1 0.586,0.97 0.615,0.756 0.664,0.656 0.738,0.516 0.808,0.5 1,0.5');
CustomEase.create('magazine', '0.77, 0, 0.175, 1');
```

---

## Text Animations

### Hero Headline — Word Split Reveal
```js
function heroHeadlineReveal(selector) {
  const el = document.querySelector(selector);
  if (!el) return;

  const split = new SplitText(el, { type: 'words,chars', wordsClass: 'word', charsClass: 'char' });

  gsap.set(split.chars, { y: '120%', opacity: 0 });

  gsap.to(split.chars, {
    y: '0%',
    opacity: 1,
    duration: 1,
    ease: 'power4.out',
    stagger: { amount: 0.5, from: 'start' },
    delay: 0.2,
  });

  // Cleanup on destroy
  return () => split.revert();
}
```

### Scroll-Triggered Line Reveal (magazine-style)
```js
function lineReveal(selector) {
  const els = gsap.utils.toArray(selector);

  els.forEach(el => {
    const split = new SplitText(el, { type: 'lines', linesClass: 'line-inner' });

    // Wrap each line in a clip container
    split.lines.forEach(line => {
      const wrapper = document.createElement('div');
      wrapper.style.cssText = 'overflow:hidden;display:block;';
      line.parentNode.insertBefore(wrapper, line);
      wrapper.appendChild(line);
    });

    gsap.from(split.lines, {
      y: '100%',
      duration: 1,
      ease: 'power4.out',
      stagger: 0.08,
      scrollTrigger: {
        trigger: el,
        start: 'top 85%',
        toggleActions: 'play none none none',
      },
      onComplete: () => split.revert(),
    });
  });
}
```

### Scramble / Glitch Text (cyber-dark, retro-future DNA)
```js
function scrambleReveal(selector) {
  const els = gsap.utils.toArray(selector);
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*';

  els.forEach(el => {
    const original = el.textContent;
    let frame = 0;
    let resolved = 0;
    const totalFrames = 30;

    ScrollTrigger.create({
      trigger: el,
      start: 'top 85%',
      onEnter: () => {
        const interval = setInterval(() => {
          el.textContent = original.split('').map((char, i) => {
            if (char === ' ') return ' ';
            if (i < resolved) return original[i];
            return chars[Math.floor(Math.random() * chars.length)];
          }).join('');

          if (frame % 3 === 0) resolved++;
          frame++;

          if (resolved >= original.length) {
            el.textContent = original;
            clearInterval(interval);
          }
        }, 30);
      },
      once: true,
    });
  });
}
```

### Counting Numbers
```js
function countUp(selector) {
  const els = gsap.utils.toArray(selector);

  els.forEach(el => {
    const target = parseFloat(el.dataset.target || el.textContent);
    const prefix = el.dataset.prefix || '';
    const suffix = el.dataset.suffix || '';
    const decimals = el.dataset.decimals ? parseInt(el.dataset.decimals) : 0;

    gsap.to({ val: 0 }, {
      val: target,
      duration: 2,
      ease: 'power2.out',
      scrollTrigger: { trigger: el, start: 'top 85%', once: true },
      onUpdate: function() {
        el.textContent = prefix + this.targets()[0].val.toFixed(decimals) + suffix;
      },
    });
  });
}
```

---

## ScrollTrigger Patterns

### Parallax Section Backgrounds
```js
function parallaxBackground(selector, depth = 0.3) {
  gsap.utils.toArray(selector).forEach(el => {
    const bg = el.querySelector('[data-parallax-bg]') || el;

    gsap.to(bg, {
      yPercent: -30 * depth,
      ease: 'none',
      scrollTrigger: {
        trigger: el,
        start: 'top bottom',
        end: 'bottom top',
        scrub: true,
      },
    });
  });
}
```

### Horizontal Scroll Section
```js
function horizontalScroll(containerSelector) {
  const container = document.querySelector(containerSelector);
  if (!container) return;

  const panels = gsap.utils.toArray(container.children);

  gsap.to(panels, {
    xPercent: -100 * (panels.length - 1),
    ease: 'none',
    scrollTrigger: {
      trigger: container,
      pin: true,
      scrub: 1,
      snap: 1 / (panels.length - 1),
      end: () => '+=' + container.offsetWidth,
    },
  });
}
```

### Pinned Section with Progress
```js
function pinnedSection(triggerSelector, animationFn) {
  const tl = gsap.timeline({
    scrollTrigger: {
      trigger: triggerSelector,
      start: 'top top',
      end: '+=200%',
      pin: true,
      scrub: 1,
      anticipatePin: 1,
    },
  });

  animationFn(tl);
  return tl;
}

// Usage:
pinnedSection('.hero-section', tl => {
  tl.to('.hero-text', { yPercent: -50, opacity: 0 })
    .to('.hero-bg', { scale: 1.2 }, '<')
    .from('.next-section', { opacity: 0, y: 100 });
});
```

### Staggered Card Reveal
```js
function cardReveal(selector, staggerAmount = 0.12) {
  gsap.utils.toArray(selector).forEach((group, i) => {
    const cards = group.querySelectorAll ? group.querySelectorAll('[data-card]') : [group];

    gsap.from(cards, {
      y: 60,
      opacity: 0,
      duration: 0.8,
      ease: 'power3.out',
      stagger: staggerAmount,
      scrollTrigger: {
        trigger: group,
        start: 'top 80%',
        toggleActions: 'play none none none',
      },
    });
  });
}
```

### Clip-Path Reveal (image/section wipe)
```js
function clipReveal(selector, direction = 'left') {
  const origins = {
    left:   ['inset(0 100% 0 0)', 'inset(0 0% 0 0)'],
    right:  ['inset(0 0 0 100%)', 'inset(0 0 0 0%)'],
    top:    ['inset(100% 0 0 0)',  'inset(0% 0 0 0)'],
    bottom: ['inset(0 0 100% 0)',  'inset(0 0 0% 0)'],
  };

  const [from, to] = origins[direction] || origins.left;

  gsap.utils.toArray(selector).forEach(el => {
    gsap.fromTo(el,
      { clipPath: from },
      {
        clipPath: to,
        duration: 1.2,
        ease: 'power4.inOut',
        scrollTrigger: {
          trigger: el,
          start: 'top 80%',
          toggleActions: 'play none none none',
        },
      }
    );
  });
}
```

---

## Page Load Sequence

### Orchestrated Intro (with preloader)
```js
function pageLoadSequence(options = {}) {
  const {
    preloader = '.preloader',
    logo = '.nav-logo',
    nav = '.nav-items',
    hero = '.hero-headline',
    heroSub = '.hero-sub',
    heroCta = '.hero-cta',
  } = options;

  const tl = gsap.timeline({ defaults: { ease: 'power4.out' } });

  // 1. Preloader exit
  tl.to(preloader, { scaleY: 0, transformOrigin: 'top', duration: 0.8, ease: 'power4.inOut' })

  // 2. Nav slides down
    .from(logo, { y: -30, opacity: 0, duration: 0.5 }, '-=0.2')
    .from(nav, { y: -20, opacity: 0, duration: 0.5, stagger: 0.05 }, '-=0.4')

  // 3. Hero content rises
    .from(hero, { y: 80, opacity: 0, duration: 0.9 }, '-=0.2')
    .from(heroSub, { y: 40, opacity: 0, duration: 0.7 }, '-=0.6')
    .from(heroCta, { y: 20, opacity: 0, duration: 0.5 }, '-=0.5');

  return tl;
}
```

---

## Timeline Patterns

### Reveal-on-Enter (reusable)
```js
// Creates a from-animation tied to scroll trigger
function revealFrom(selector, fromVars, triggerOptions = {}) {
  return gsap.from(selector, {
    ...fromVars,
    scrollTrigger: {
      trigger: triggerOptions.trigger || selector,
      start: triggerOptions.start || 'top 85%',
      toggleActions: 'play none none reverse',
      ...triggerOptions,
    },
  });
}

// Usage
revealFrom('.feature-icon', { scale: 0, rotation: -45, duration: 0.6, stagger: 0.1 });
revealFrom('.stat-number', { y: 40, opacity: 0, duration: 0.8 });
```

### Section Transition (morph between states)
```js
function morphSection(fromEl, toEl) {
  const tl = gsap.timeline({ paused: true });

  tl.to(fromEl, { opacity: 0, y: -40, duration: 0.4, ease: 'power2.in' })
    .set(fromEl, { display: 'none' })
    .set(toEl, { display: 'block', opacity: 0, y: 40 })
    .to(toEl, { opacity: 1, y: 0, duration: 0.5, ease: 'power3.out' });

  return tl;
}
```

---

## Hover Effects

### Magnetic Button (GSAP version)
```js
function magneticButton(selector) {
  document.querySelectorAll(selector).forEach(btn => {
    const strength = parseFloat(btn.dataset.magnetStrength) || 0.4;

    btn.addEventListener('mousemove', e => {
      const { left, top, width, height } = btn.getBoundingClientRect();
      const x = (e.clientX - left - width / 2) * strength;
      const y = (e.clientY - top - height / 2) * strength;
      gsap.to(btn, { x, y, duration: 0.3, ease: 'power2.out' });
    });

    btn.addEventListener('mouseleave', () => {
      gsap.to(btn, { x: 0, y: 0, duration: 0.5, ease: 'elastic.out(1, 0.4)' });
    });
  });
}
```

### Image Tilt on Hover
```js
function tiltCard(selector) {
  document.querySelectorAll(selector).forEach(card => {
    card.addEventListener('mousemove', e => {
      const { left, top, width, height } = card.getBoundingClientRect();
      const xPct = (e.clientX - left) / width - 0.5;
      const yPct = (e.clientY - top) / height - 0.5;

      gsap.to(card, {
        rotationX: -yPct * 12,
        rotationY: xPct * 12,
        transformPerspective: 800,
        ease: 'power2.out',
        duration: 0.3,
      });
    });

    card.addEventListener('mouseleave', () => {
      gsap.to(card, { rotationX: 0, rotationY: 0, duration: 0.6, ease: 'elastic.out(1, 0.5)' });
    });
  });
}
```

---

## Reduced Motion

Always wrap animations:

```js
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

if (!prefersReducedMotion) {
  // All animations here
  pageLoadSequence();
  lineReveal('.section-heading');
  parallaxBackground('.hero');
} else {
  // Instant state for reduced motion
  gsap.set('.preloader', { display: 'none' });
}
```

---

## Performance Tips

1. **Always use `will-change: transform`** on elements that animate transform/opacity
2. **Prefer `transform` and `opacity`** — GPU composited, no layout recalc
3. **Use `gsap.quickTo()`** for mouse-follow animations (bypasses scheduler overhead)
4. **Kill ScrollTriggers on cleanup** — `ScrollTrigger.getAll().forEach(t => t.kill())`
5. **Batch DOM reads** before creating animations — avoids layout thrashing
6. **Use `lazy: false`** on ScrollTrigger for above-the-fold elements to avoid flash
