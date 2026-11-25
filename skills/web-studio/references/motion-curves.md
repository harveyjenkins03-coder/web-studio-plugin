# Motion Curves Reference

Named library of easing curves with exact cubic-bezier values, GSAP equivalents, duration recommendations, and DNA profile mappings. Every curve here is production-tested and intentionally selected to avoid the generic `ease-in-out` default that plagues AI-generated motion.

---

## 1. Cinematic Curves

Slow, dramatic curves for luxury, editorial, and immersive experiences. Long durations, heavy deceleration, deliberate pacing. The viewer should feel like they are watching a film, not clicking through a website.

### 1a. Cinematic Glide

```
cubic-bezier(0.22, 1, 0.36, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power3.out"` |
| Duration range | 0.8 - 1.4s |
| Use case | Hero text reveals, section fade-ins, page transitions |
| Character | Slow start, long smooth coast to stop. The workhorse cinematic ease. |

**DNA profiles**: Dark Luxe, Warm Editorial, Obsidian Mono, Coastal Serenity

```css
.hero-title {
  transition: transform 1.2s cubic-bezier(0.22, 1, 0.36, 1),
              opacity 1.2s cubic-bezier(0.22, 1, 0.36, 1);
}
```

```javascript
gsap.from('.hero-title', {
  y: 80,
  opacity: 0,
  duration: 1.2,
  ease: 'power3.out',
});
```

### 1b. Cinematic Dramatic

```
cubic-bezier(0.65, 0.01, 0.05, 0.99)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `CustomEase.create("dramatic", "M0,0 C0.65,0.01 0.05,0.99 1,1")` |
| Duration range | 1.0 - 1.8s |
| Use case | Full-screen transitions, curtain reveals, hero image parallax |
| Character | Holds tension in the middle, then releases. Creates a "breath" in the motion. |

**DNA profiles**: Dark Luxe, Noir Cinema, Velvet Night

```javascript
gsap.to('.curtain', {
  yPercent: -100,
  duration: 1.4,
  ease: CustomEase.create("dramatic", "M0,0 C0.65,0.01 0.05,0.99 1,1"),
});
```

### 1c. Cinematic Drift

```
cubic-bezier(0.16, 1, 0.3, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"expo.out"` |
| Duration range | 0.9 - 1.5s |
| Use case | Parallax layers, floating elements, ambient background motion |
| Character | Fast initial impulse that drifts to a gentle stop. Feels weightless. |

**DNA profiles**: Coastal Serenity, Warm Editorial, Ethereal Light, Soft Gradient

```javascript
gsap.from('.parallax-layer', {
  y: 120,
  duration: 1.3,
  ease: 'expo.out',
  scrollTrigger: {
    trigger: '.parallax-section',
    start: 'top 80%',
  },
});
```

### 1d. Cinematic Slow Burn

```
cubic-bezier(0.37, 0, 0.63, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power1.inOut"` |
| Duration range | 1.2 - 2.0s |
| Use case | Background color transitions, theme toggles, ambient loops, image crossfades |
| Character | Symmetrical, meditative. No dramatic acceleration or deceleration. Feels like breathing. |

**DNA profiles**: Warm Editorial, Coastal Serenity, Ethereal Light, Zen Minimal

```javascript
gsap.to('.ambient-orb', {
  scale: 1.15,
  duration: 2.0,
  ease: 'power1.inOut',
  repeat: -1,
  yoyo: true,
});
```
---

## 2. Snappy Curves

Fast, responsive curves for hovers, micro-interactions, and interface feedback. The site should feel alive and reactive under the cursor. Sub-second durations, sharp deceleration.

### 2a. Snappy Standard

```
cubic-bezier(0.25, 0.46, 0.45, 0.94)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power1.out"` |
| Duration range | 0.2 - 0.4s |
| Use case | Button hovers, link underlines, nav highlights, tooltip reveals |
| Character | Light and quick. The default snappy ease for any hover state. |

**DNA profiles**: Neon Brutalist, SVZ Kinetic, Tech Carbon, Startup Pop

```css
.btn {
  transition: transform 0.25s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              background 0.25s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}
.btn:hover {
  transform: translateY(-2px);
}
```

### 2b. Snappy Sharp

```
cubic-bezier(0.33, 1, 0.68, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power2.out"` |
| Duration range | 0.15 - 0.35s |
| Use case | Dropdown menus, accordion toggles, tab switches, chip selections |
| Character | Faster initial punch than Standard. Feels decisive and confident. |

**DNA profiles**: Tech Carbon, SVZ Kinetic, Swiss Grid, Corporate Edge

```javascript
gsap.to('.dropdown', {
  height: 'auto',
  opacity: 1,
  duration: 0.3,
  ease: 'power2.out',
});
```

### 2c. Snappy Flick

```
cubic-bezier(0.23, 1, 0.32, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power3.out"` (short duration variant) |
| Duration range | 0.15 - 0.3s |
| Use case | Toggle switches, checkbox ticks, icon swaps, mobile menu triggers |
| Character | Explosive start that settles fast. Like flicking a switch. |

**DNA profiles**: Neon Brutalist, Startup Pop, SVZ Kinetic, Retro Arcade

```css
.toggle-knob {
  transition: transform 0.2s cubic-bezier(0.23, 1, 0.32, 1);
}
.toggle--active .toggle-knob {
  transform: translateX(24px);
}
```

### 2d. Snappy Punch

```
cubic-bezier(0.5, 1.25, 0.75, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"back.out(1.2)"` |
| Duration range | 0.2 - 0.4s |
| Use case | Notification badges, toast popups, like/favorite animations, count increments |
| Character | Overshoots slightly before settling. Adds playful energy without being bouncy. |

**DNA profiles**: Startup Pop, Retro Arcade, Neon Brutalist, Playful Geo

```javascript
gsap.from('.notification-badge', {
  scale: 0,
  duration: 0.35,
  ease: 'back.out(1.2)',
});
```
---

## 3. Elastic Curves

Bouncy, spring-like curves that create organic, playful motion. Requires careful control: too much bounce feels cheap, too little defeats the purpose. CSS cubic-bezier can only approximate true elastic behavior; GSAP CustomEase provides the real thing.

### 3a. Elastic Gentle

**CSS approximation:**
```
cubic-bezier(0.68, -0.55, 0.27, 1.55)
```

**GSAP (true elastic):**
```javascript
gsap.to(el, { ease: 'elastic.out(1, 0.5)', duration: 1.0 });
// amplitude: 1, period: 0.5 (gentle, 1-2 oscillations)
```

| Property | Value |
|----------|-------|
| Duration range | 0.8 - 1.2s |
| Use case | Modal popups, card entrances, floating action buttons |
| Character | One soft bounce before resting. Friendly but not cartoonish. |

**DNA profiles**: Playful Geo, Startup Pop, Soft Gradient, Warm Editorial

```javascript
// Modal entrance
gsap.from('.modal', {
  scale: 0.85,
  opacity: 0,
  duration: 0.9,
  ease: 'elastic.out(1, 0.5)',
});
```

### 3b. Elastic Snappy

**CSS approximation:**
```
cubic-bezier(0.68, -0.6, 0.32, 1.6)
```

**GSAP (true elastic):**
```javascript
gsap.to(el, { ease: 'elastic.out(1, 0.3)', duration: 0.8 });
// amplitude: 1, period: 0.3 (tighter, snappier oscillation)
```

| Property | Value |
|----------|-------|
| Duration range | 0.6 - 1.0s |
| Use case | Button press release, magnetic cursor snap-back, drag-and-drop settle |
| Character | Two quick bounces then done. Energetic and satisfying. |

**DNA profiles**: Retro Arcade, Neon Brutalist, SVZ Kinetic, Startup Pop

```javascript
// Magnetic button snap-back on mouseleave
btn.addEventListener('mouseleave', () => {
  gsap.to(btn, {
    x: 0,
    y: 0,
    duration: 0.7,
    ease: 'elastic.out(1, 0.3)',
  });
});
```

### 3c. Elastic Wobbly

**CSS approximation (limited):**
```
cubic-bezier(0.5, -1, 0.5, 2.5)
```

**GSAP (true wobble):**
```javascript
gsap.to(el, { ease: 'elastic.out(1.2, 0.2)', duration: 1.2 });
// amplitude: 1.2, period: 0.2 (exaggerated, multiple oscillations)
```

| Property | Value |
|----------|-------|
| Duration range | 1.0 - 1.5s |
| Use case | Error shake, attention-grab animations, playful mascot/character motion |
| Character | Pronounced wobble. Use sparingly or the whole site feels like jelly. |

**DNA profiles**: Retro Arcade, Playful Geo

```javascript
// Error shake on invalid input
gsap.to('.input--error', {
  x: 10,
  duration: 0.6,
  ease: 'elastic.out(1.2, 0.2)',
});
```

### 3d. Elastic Spring

**CSS approximation:**
```
cubic-bezier(0.5, 1.8, 0.5, 0.8)
```

**GSAP (spring physics):**
```javascript
gsap.to(el, {
  ease: CustomEase.create("spring", "M0,0 C0.12,0.75 0.24,1.2 0.38,1.08 0.52,0.96 0.64,1.02 0.76,1 0.88,0.99 1,1"),
  duration: 0.8,
});
```

| Property | Value |
|----------|-------|
| Duration range | 0.6 - 1.0s |
| Use case | Draggable elements settling, scroll-snapped cards, carousel transitions |
| Character | Physics-based feel. Overshoots, corrects, settles. Like a real spring. |

**DNA profiles**: Playful Geo, Startup Pop, Soft Gradient

```javascript
// Scroll-snap card settle
gsap.to('.card', {
  x: targetX,
  duration: 0.8,
  ease: CustomEase.create("spring", "M0,0 C0.12,0.75 0.24,1.2 0.38,1.08 0.52,0.96 0.64,1.02 0.76,1 0.88,0.99 1,1"),
});
```
---

## 4. Smooth Curves

Apple-like refined curves. Buttery, precise, invisible. The user should never consciously notice these transitions; they should simply feel "right." These curves power interfaces where the design disappears and the content speaks.

### 4a. Smooth Material

```
cubic-bezier(0.4, 0, 0.2, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power2.out"` (close match) |
| Duration range | 0.3 - 0.5s |
| Use case | Page element transitions, card reorders, list item shifts, layout changes |
| Character | Google Material Design standard. Slightly more aggressive than Apple but universally safe. |

**DNA profiles**: Swiss Grid, Corporate Edge, Tech Carbon, Zen Minimal

```css
.card {
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1),
              box-shadow 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}
```

### 4b. Smooth Apple

```
cubic-bezier(0.25, 0.1, 0.25, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power1.out"` (approximate) |
| Duration range | 0.3 - 0.6s |
| Use case | iOS-style sheet presentations, nav bar transitions, scroll container snapping |
| Character | The Apple ecosystem default. Calm, assured, invisible. Never calls attention to itself. |

**DNA profiles**: Zen Minimal, Coastal Serenity, Ethereal Light, Soft Gradient

```css
.sheet {
  transition: transform 0.5s cubic-bezier(0.25, 0.1, 0.25, 1);
}
.sheet--open {
  transform: translateY(0);
}
```

### 4c. Smooth Silk

```
cubic-bezier(0.19, 1, 0.22, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"expo.out"` |
| Duration range | 0.5 - 0.9s |
| Use case | Large panel slides, image gallery transitions, tab content swaps |
| Character | Fast departure, ultra-smooth landing. Like sliding on silk. Premium feel without drama. |

**DNA profiles**: Dark Luxe, Warm Editorial, Coastal Serenity, Obsidian Mono

```javascript
gsap.to('.gallery-panel', {
  xPercent: -100,
  duration: 0.7,
  ease: 'expo.out',
});
```

### 4d. Smooth Linear-ish

```
cubic-bezier(0.35, 0, 0.65, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"sine.inOut"` |
| Duration range | 0.3 - 0.6s |
| Use case | Progress bars, loading indicators, scroll-linked transforms, continuous motion |
| Character | Almost linear but with just enough curve to avoid mechanical harshness. For motion that should feel effortless. |

**DNA profiles**: Swiss Grid, Zen Minimal, Tech Carbon, Corporate Edge

```css
.progress-bar {
  transition: width 0.5s cubic-bezier(0.35, 0, 0.65, 1);
}
```
---

## 5. Sharp Curves

Aggressive, high-energy curves inspired by SVZ.io, Awwwards showcases, and motion-heavy portfolio sites. Quick acceleration, abrupt stops. These curves announce themselves. Use when the motion IS the content.

### 5a. Sharp Slam

```
cubic-bezier(0.7, 0, 0.3, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power2.inOut"` |
| Duration range | 0.3 - 0.6s |
| Use case | Section wipes, horizontal scroll snaps, split-screen transitions |
| Character | Balanced aggression. Accelerates hard, decelerates hard. Like slamming a book shut. |

**DNA profiles**: SVZ Kinetic, Neon Brutalist, Noir Cinema, Tech Carbon

```javascript
gsap.to('.section-wipe', {
  xPercent: -100,
  duration: 0.5,
  ease: 'power2.inOut',
  scrollTrigger: {
    trigger: '.wipe-container',
    scrub: 0.5,
    pin: true,
  },
});
```

### 5b. Sharp Snap

```
cubic-bezier(0.85, 0, 0.15, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power4.inOut"` |
| Duration range | 0.25 - 0.5s |
| Use case | Page route transitions, modal entrances, full-viewport animations |
| Character | Extreme ease-in-out. Almost nothing happens in the middle; all action is at start and end. Razor-sharp. |

**DNA profiles**: SVZ Kinetic, Neon Brutalist, Noir Cinema

```javascript
// Page transition
gsap.timeline()
  .to('.page-current', {
    xPercent: -100,
    duration: 0.4,
    ease: 'power4.inOut',
  })
  .from('.page-next', {
    xPercent: 100,
    duration: 0.4,
    ease: 'power4.inOut',
  }, '<');
```

### 5c. Sharp Whip

```
cubic-bezier(0.9, 0, 0.1, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"expo.inOut"` |
| Duration range | 0.3 - 0.6s |
| Use case | Horizontal scroll-jacking, viewport-snapped section transitions, dramatic reveals |
| Character | The sharpest ease-in-out available in CSS. Motion holds still, then SNAPS. Like cracking a whip. |

**DNA profiles**: SVZ Kinetic, Noir Cinema

```javascript
gsap.to('.horizontal-section', {
  xPercent: -100,
  duration: 0.5,
  ease: 'expo.inOut',
  scrollTrigger: {
    trigger: '.horizontal-track',
    start: 'top top',
    end: '+=200%',
    scrub: 0.3,
    pin: true,
  },
});
```

### 5d. Sharp Kick

```
cubic-bezier(0.8, 0, 0, 1)
```

| Property | Value |
|----------|-------|
| GSAP equivalent | `"power4.out"` |
| Duration range | 0.2 - 0.5s |
| Use case | Element entrances that need authority, text slams, image reveals with impact |
| Character | Explosive start that decelerates sharply. The element arrives with force. Like a door being kicked open. |

**DNA profiles**: SVZ Kinetic, Neon Brutalist, Retro Arcade, Tech Carbon

```javascript
gsap.from('.headline', {
  y: 100,
  opacity: 0,
  duration: 0.4,
  ease: 'power4.out',
  stagger: 0.06,
});
```
---

## 6. Custom GSAP Eases

These eases require GSAP and have no direct CSS cubic-bezier equivalent. Use them when the project loads GSAP (which is most Web Studio projects).

### Back Eases

```javascript
// back.out(1.7) -- default overshoot
// Element overshoots its target, then settles back.
gsap.from('.card', { y: 60, ease: 'back.out(1.7)', duration: 0.6 });

// back.out(2.5) -- exaggerated overshoot
// Pronounced overshoot. Use for attention-grabbing entrances.
gsap.from('.badge', { scale: 0, ease: 'back.out(2.5)', duration: 0.5 });

// back.out(1.2) -- subtle overshoot
// Barely perceptible. Adds organic feel without obvious bounce.
gsap.from('.tooltip', { y: 10, opacity: 0, ease: 'back.out(1.2)', duration: 0.3 });

// back.inOut(1.7) -- overshoot on both ends
// Use for elements that need to "wind up" before moving.
gsap.to('.slider-thumb', { x: 200, ease: 'back.inOut(1.7)', duration: 0.5 });
```

### Elastic Eases

```javascript
// elastic.out(1, 0.3) -- tight spring
// 2-3 oscillations. The standard bouncy ease.
gsap.from('.modal', { scale: 0.8, ease: 'elastic.out(1, 0.3)', duration: 0.8 });

// elastic.out(1, 0.5) -- gentle spring
// 1-2 oscillations. Softer, more refined.
gsap.from('.panel', { x: -100, ease: 'elastic.out(1, 0.5)', duration: 1.0 });

// elastic.out(1.2, 0.2) -- aggressive spring
// 3-4 oscillations. Cartoonish energy. Use sparingly.
gsap.to('.error-icon', { rotation: 10, ease: 'elastic.out(1.2, 0.2)', duration: 0.6 });

// elastic.out(0.7, 0.4) -- dampened spring
// Low amplitude, few oscillations. Almost smooth but with a live feel.
gsap.from('.notification', { y: -30, ease: 'elastic.out(0.7, 0.4)', duration: 0.7 });
```

### Expo Eases

```javascript
// expo.out -- extreme deceleration
// The fastest out-ease in GSAP. Rockets out, feather landing.
gsap.from('.hero-img', { scale: 1.3, ease: 'expo.out', duration: 1.2 });

// expo.inOut -- sharp in, sharp out
// Aggressive symmetrical ease. Great for scrubbed scroll animations.
gsap.to('.wipe', { xPercent: -100, ease: 'expo.inOut', duration: 0.6 });

// expo.in -- slow start, explosive finish
// Builds tension, then releases. Use for exit animations.
gsap.to('.exiting-element', { y: -200, opacity: 0, ease: 'expo.in', duration: 0.5 });
```

### Power Eases

```javascript
// power4.out -- very strong deceleration
// Almost as aggressive as expo.out but slightly softer.
gsap.from('.slide-in', { x: 200, ease: 'power4.out', duration: 0.8 });

// power3.out -- strong deceleration
// The versatile workhorse. Good for most scroll-triggered reveals.
gsap.from('[data-reveal]', { y: 60, opacity: 0, ease: 'power3.out', duration: 0.9 });

// power2.inOut -- balanced emphasis
// Clean and professional. Suitable for layout animations.
gsap.to('.accordion-content', { height: 'auto', ease: 'power2.inOut', duration: 0.4 });

// power4.inOut -- dramatic emphasis
// Holds at both ends. Use for viewport transitions and section wipes.
gsap.to('.page-transition', { xPercent: -100, ease: 'power4.inOut', duration: 0.5 });
```

### Steps Ease

```javascript
// steps(n) -- stepped/frame-based motion
// Jumps between n discrete positions. Retro/mechanical feel.
gsap.to('.sprite', { x: 500, ease: 'steps(10)', duration: 1.0 });

// Use case: pixel art animations, typewriter effects, clock ticks
gsap.to('.counter', { textContent: 100, ease: 'steps(100)', duration: 2.0, snap: { textContent: 1 } });
```
---

## 7. Stagger Timing Guide

Stagger values control the delay between each item in a group animation. Too fast and items blur together. Too slow and the sequence drags. These values are calibrated for perceived rhythm.

| Item Count | Stagger Delay | Total Sequence | Example |
|------------|---------------|----------------|---------|
| 2-3 items | 0.10 - 0.15s | 0.2 - 0.45s | Nav links, CTA pair, icon row |
| 4-6 items | 0.06 - 0.10s | 0.24 - 0.6s | Feature cards, logo row, grid items |
| 7-10 items | 0.03 - 0.06s | 0.21 - 0.6s | List items, gallery thumbnails, stat counters |
| 11-20 items | 0.02 - 0.04s | 0.22 - 0.8s | Large grid, portfolio mosaic, tag cloud |
| 20+ items | 0.01 - 0.02s | 0.2 - 0.6s | Character-by-character text, particle-like cascades |

### Rules of Thumb

- **Total sequence should rarely exceed 0.8s**. Even with 50 items, the cascade should feel like a wave, not a slideshow.
- **Group staggers** for large counts: instead of staggering all 20 items, stagger 5 groups of 4.
- **Direction matters**: left-to-right feels natural for reading cultures. Bottom-to-top feels like growth. Center-out feels like explosion. Random feels chaotic (intentionally).

```javascript
// Standard cascade -- 6 feature cards
gsap.from('.feature-card', {
  y: 40,
  opacity: 0,
  duration: 0.7,
  ease: 'power3.out',
  stagger: 0.08,
});

// Grid stagger -- items reveal from top-left corner
gsap.from('.grid-item', {
  y: 30,
  opacity: 0,
  duration: 0.6,
  ease: 'power3.out',
  stagger: {
    amount: 0.6,
    grid: [4, 3],
    from: 'start',
  },
});

// Center-out stagger -- items reveal from the middle
gsap.from('.nav-link', {
  y: 20,
  opacity: 0,
  duration: 0.5,
  ease: 'power2.out',
  stagger: {
    each: 0.08,
    from: 'center',
  },
});

// Random stagger -- organic, non-linear reveal
gsap.from('.particle', {
  scale: 0,
  opacity: 0,
  duration: 0.4,
  ease: 'back.out(1.7)',
  stagger: {
    each: 0.03,
    from: 'random',
  },
});
```
---

## 8. Duration Guide

Duration depends on what is moving, how far it moves, and the emotional register of the site. These ranges are starting points; always tune by feel.

### By Element Type

| Element | Duration Range | Notes |
|---------|---------------|-------|
| **Hover states** | 0.15 - 0.35s | Must feel instant. User is waiting for feedback. |
| **Button press** | 0.08 - 0.15s | Scale down (active state) should be near-instant. |
| **Tooltip show** | 0.15 - 0.25s | Fast in, slightly slower out (0.2 - 0.3s). |
| **Dropdown open** | 0.2 - 0.35s | Fast enough to not block the user. |
| **Tab/accordion** | 0.25 - 0.4s | Height animations feel best slightly slower. |
| **Modal entrance** | 0.3 - 0.5s | Scale + fade. Must feel deliberate, not sluggish. |
| **Modal exit** | 0.2 - 0.3s | Exits should always be faster than entrances. |
| **Toast / notification** | 0.3 - 0.5s | Slide + fade. Must grab attention without startling. |
| **Page transition** | 0.4 - 0.7s | Full viewport animation. Long enough to register. |
| **Text reveal (word split)** | 0.6 - 1.0s | Per-word stagger duration. Total depends on word count. |
| **Text reveal (char split)** | 0.8 - 1.4s | Per-character stagger duration. Longer sequences need faster individual timing. |
| **Section scroll reveal** | 0.6 - 1.0s | The main content entrance. The most common duration. |
| **Parallax (scrubbed)** | Tied to scroll | No fixed duration; use scrub values (see Section 9). |
| **Hero entrance** | 0.8 - 1.5s | The big reveal. Can afford to be slow and dramatic. |
| **Background color shift** | 0.8 - 1.5s | Slow transitions prevent jarring color jumps. |
| **Theme toggle** | 0.3 - 0.5s | Fast enough to feel responsive, slow enough to see the change. |
| **Loading / skeleton** | 1.0 - 2.0s | Pulse or shimmer loop cycle duration. |
| **Infinite marquee** | 15 - 40s | Full cycle. Speed depends on content length and viewport width. |

### By Motion Personality

| Personality | Base Duration Multiplier | Notes |
|-------------|--------------------------|-------|
| Cinematic-slow | 1.5x - 2.0x | Everything takes its time. Luxurious pacing. |
| Snappy-fast | 0.6x - 0.8x | Everything is quick. Responsive, energetic. |
| Organic-fluid | 1.0x - 1.3x | Natural timing. Not rushed, not lingering. |
| Mechanical-precise | 0.8x - 1.0x | Exact durations. No easing excess. |
| Sharp-aggressive | 0.7x - 1.0x | Short durations, extreme easing makes them feel intense. |

### Exit vs. Entrance Rule

**Exits should always be faster than entrances.** Typically 60-75% of the entrance duration.

```javascript
// Entrance: 0.5s
gsap.from('.modal', { scale: 0.9, opacity: 0, duration: 0.5, ease: 'power3.out' });

// Exit: 0.3s (60% of entrance)
gsap.to('.modal', { scale: 0.95, opacity: 0, duration: 0.3, ease: 'power2.in' });
```
---

## 9. Scroll Speed Ratios

Parallax multipliers control how fast elements move relative to the natural scroll speed. A multiplier of 1.0x means the element scrolls at normal speed (no parallax). Values above 1.0x move faster than scroll. Values below 1.0x move slower.

### Layer Speed Reference

| Layer | Speed Multiplier | GSAP scrub Value | Use Case |
|-------|-----------------|------------------|----------|
| **Deep background** | 0.2x - 0.3x | `scrub: true` | Nebula, gradient mesh, distant texture |
| **Background** | 0.3x - 0.5x | `scrub: true` | Hero images, ambient shapes, grain overlay |
| **Mid-background** | 0.5x - 0.7x | `scrub: true` | Decorative SVGs, floating icons, secondary images |
| **Content (default)** | 1.0x | N/A | Text, cards, buttons -- normal scroll speed |
| **Foreground accent** | 1.1x - 1.3x | `scrub: true` | Overlapping badges, pull quotes, accent shapes |
| **Fast foreground** | 1.3x - 1.6x | `scrub: true` | Parallax text overlays, counters, edge decorations |

### GSAP scrub Values

The `scrub` property in ScrollTrigger controls how tightly the animation follows the scroll position.

| scrub Value | Behavior | Use Case |
|-------------|----------|----------|
| `true` (or `1`) | Locked 1:1 to scroll position | Precise parallax, progress indicators |
| `0.3` - `0.5` | Tight follow with slight smoothing | Standard parallax layers, image reveals |
| `0.5` - `1.0` | Moderate smoothing | Floating elements, decorative shapes |
| `1.0` - `2.0` | Loose, laggy follow | Ambient background motion, dreamy drift |
| `3.0` - `5.0` | Very loose, heavy lag | Background gradients, subtle mood shifts |

### Implementation Patterns

```javascript
// Multi-layer parallax scene
gsap.to('.bg-deep', {
  yPercent: -15,
  ease: 'none',
  scrollTrigger: {
    trigger: '.parallax-scene',
    start: 'top bottom',
    end: 'bottom top',
    scrub: true,  // locked to scroll
  },
});

gsap.to('.bg-mid', {
  yPercent: -30,
  ease: 'none',
  scrollTrigger: {
    trigger: '.parallax-scene',
    start: 'top bottom',
    end: 'bottom top',
    scrub: 0.5,  // slight smoothing
  },
});

gsap.to('.fg-accent', {
  yPercent: -60,
  ease: 'none',
  scrollTrigger: {
    trigger: '.parallax-scene',
    start: 'top bottom',
    end: 'bottom top',
    scrub: 0.3,  // tight follow, fast foreground
  },
});
```

```javascript
// Horizontal parallax (elements shift laterally on scroll)
gsap.to('.lateral-element', {
  xPercent: -20,
  ease: 'none',
  scrollTrigger: {
    trigger: '.section',
    start: 'top bottom',
    end: 'bottom top',
    scrub: 1.0,
  },
});
```

```javascript
// Scale-based depth (element grows as you scroll toward it)
gsap.fromTo('.depth-element', 
  { scale: 0.85 },
  {
    scale: 1,
    ease: 'none',
    scrollTrigger: {
      trigger: '.depth-section',
      start: 'top bottom',
      end: 'center center',
      scrub: 0.5,
    },
  }
);
```

### Depth Perception Rules

- **Never move more than 3 layers** at different speeds in the same viewport. More than 3 creates visual chaos.
- **Background layers move DOWN** relative to scroll (yPercent negative = moves up slower = appears to recede).
- **Foreground layers move UP** relative to scroll (yPercent more negative = moves up faster = appears to advance).
- **Keep total parallax offset under 30%** of the element's height to avoid content misalignment.
- **Disable parallax on mobile** (or reduce to 2 layers max). Parallax on touch scroll feels wrong.
---

## 10. Motion Personality Map

Every DNA profile maps to a motion personality that governs curve selection, timing, stagger behavior, and scroll intensity. Use this map during Phase 1 (Design DNA Extraction) to select the right motion curve from the catalog above.

| # | DNA Profile | Motion Personality | Primary Curve | Stagger | Duration Multiplier | Scroll Intensity |
|---|------------|-------------------|---------------|---------|---------------------|-----------------|
| 1 | **Dark Luxe** | cinematic-slow | Cinematic Glide `(0.22, 1, 0.36, 1)` | 0.08 - 0.10s | 1.5x | Low (subtle parallax) |
| 2 | **Warm Editorial** | cinematic-smooth | Cinematic Drift `(0.16, 1, 0.3, 1)` | 0.08 - 0.12s | 1.3x | Low-medium |
| 3 | **Neon Brutalist** | sharp-aggressive | Sharp Kick `(0.8, 0, 0, 1)` | 0.04 - 0.06s | 0.7x | High (fast reveals) |
| 4 | **SVZ Kinetic** | sharp-aggressive | Sharp Whip `(0.9, 0, 0.1, 1)` | 0.03 - 0.05s | 0.7x | Very high (scrub-heavy) |
| 5 | **Coastal Serenity** | smooth-gentle | Smooth Apple `(0.25, 0.1, 0.25, 1)` | 0.10 - 0.14s | 1.4x | Minimal |
| 6 | **Swiss Grid** | mechanical-precise | Smooth Material `(0.4, 0, 0.2, 1)` | 0.06 - 0.08s | 1.0x | Low |
| 7 | **Tech Carbon** | snappy-controlled | Snappy Sharp `(0.33, 1, 0.68, 1)` | 0.05 - 0.07s | 0.8x | Medium |
| 8 | **Retro Arcade** | elastic-playful | Elastic Snappy (GSAP `elastic.out(1, 0.3)`) | 0.04 - 0.06s | 0.9x | Medium-high |
| 9 | **Noir Cinema** | cinematic-dramatic | Cinematic Dramatic `(0.65, 0.01, 0.05, 0.99)` | 0.10 - 0.14s | 1.8x | Low (tension-driven) |
| 10 | **Startup Pop** | snappy-bouncy | Snappy Punch `(0.5, 1.25, 0.75, 1)` | 0.06 - 0.08s | 0.8x | Medium |
| 11 | **Ethereal Light** | smooth-gentle | Smooth Silk `(0.19, 1, 0.22, 1)` | 0.10 - 0.14s | 1.4x | Minimal |
| 12 | **Obsidian Mono** | cinematic-smooth | Cinematic Glide `(0.22, 1, 0.36, 1)` | 0.08 - 0.10s | 1.3x | Low |
| 13 | **Playful Geo** | elastic-playful | Elastic Gentle (GSAP `elastic.out(1, 0.5)`) | 0.06 - 0.10s | 1.0x | Medium |
| 14 | **Corporate Edge** | smooth-precise | Smooth Material `(0.4, 0, 0.2, 1)` | 0.06 - 0.08s | 0.9x | Low |
| 15 | **Velvet Night** | cinematic-dramatic | Cinematic Dramatic `(0.65, 0.01, 0.05, 0.99)` | 0.10 - 0.12s | 1.6x | Low |
| 16 | **Soft Gradient** | smooth-gentle | Smooth Apple `(0.25, 0.1, 0.25, 1)` | 0.08 - 0.12s | 1.2x | Minimal |
| 17 | **Zen Minimal** | mechanical-precise | Smooth Linear-ish `(0.35, 0, 0.65, 1)` | 0.08 - 0.10s | 1.1x | None (static preferred) |
| 18 | **Industrial Raw** | sharp-aggressive | Sharp Slam `(0.7, 0, 0.3, 1)` | 0.03 - 0.06s | 0.8x | High |
| 19 | **Candy Pop** | elastic-playful | Elastic Spring (GSAP CustomEase) | 0.05 - 0.08s | 0.9x | Medium |
| 20 | **Monochrome Type** | cinematic-smooth | Cinematic Drift `(0.16, 1, 0.3, 1)` | 0.06 - 0.10s | 1.2x | Low-medium |

### Reading the Map

- **Motion Personality**: The overall feel. Determines which curve family to start with.
- **Primary Curve**: The default easing curve for section reveals and major animations. Use this as the `motion.curve` value in `design-tokens.json`.
- **Stagger**: The recommended stagger range for grouped element reveals. Use as `motion.stagger` in tokens.
- **Duration Multiplier**: Multiply against the base durations in Section 8. A 1.5x multiplier turns a 0.6s section reveal into a 0.9s reveal.
- **Scroll Intensity**: How much scroll-driven animation the DNA expects. "Very high" means scrubbed horizontal scrolling, aggressive parallax, and pinned sections. "None" means prefer time-triggered animations over scroll-triggered ones.

### Personality-to-Curve Quick Reference

```
cinematic-slow     -> Cinematic family (Section 1)     -> 0.8-1.5s base
cinematic-smooth   -> Cinematic + Smooth blend          -> 0.7-1.3s base
cinematic-dramatic -> Cinematic Dramatic specifically    -> 1.0-1.8s base
smooth-gentle      -> Smooth family (Section 4)         -> 0.3-0.6s base
smooth-precise     -> Smooth Material specifically      -> 0.3-0.5s base
snappy-controlled  -> Snappy family (Section 2)         -> 0.15-0.4s base
snappy-bouncy      -> Snappy + slight overshoot         -> 0.2-0.4s base
sharp-aggressive   -> Sharp family (Section 5)          -> 0.2-0.6s base
elastic-playful    -> Elastic family (Section 3)        -> 0.6-1.2s base
mechanical-precise -> Smooth Linear-ish + steps         -> 0.3-0.6s base
```

---

## Quick Selection Cheatsheet

When you know the vibe but need the exact values fast:

| If the site feels like... | Use this curve | At this duration | With this GSAP ease |
|---------------------------|----------------|------------------|---------------------|
| Apple product page | `(0.25, 0.1, 0.25, 1)` | 0.4 - 0.6s | `power1.out` |
| Luxury fashion brand | `(0.22, 1, 0.36, 1)` | 1.0 - 1.4s | `power3.out` |
| SaaS startup | `(0.33, 1, 0.68, 1)` | 0.25 - 0.4s | `power2.out` |
| SVZ/Awwwards portfolio | `(0.9, 0, 0.1, 1)` | 0.3 - 0.5s | `expo.inOut` |
| Playful consumer app | `(0.68, -0.55, 0.27, 1.55)` | 0.7 - 1.0s | `elastic.out(1, 0.5)` |
| Editorial magazine | `(0.16, 1, 0.3, 1)` | 0.8 - 1.2s | `expo.out` |
| Tech/developer tools | `(0.4, 0, 0.2, 1)` | 0.3 - 0.5s | `power2.out` |
| Film/cinema promotion | `(0.65, 0.01, 0.05, 0.99)` | 1.2 - 1.8s | CustomEase |
| Kids/gaming | `(0.5, -1, 0.5, 2.5)` | 0.8 - 1.2s | `elastic.out(1.2, 0.2)` |
| Minimalist gallery | `(0.35, 0, 0.65, 1)` | 0.4 - 0.7s | `sine.inOut` |
