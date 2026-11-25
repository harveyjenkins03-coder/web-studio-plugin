# DNA Profile: Apple Minimal

**Category:** Dark / Product  
**Mood:** Clarity through restraint, product as protagonist, technical beauty

---

## Emotional Target

The site makes one thing feel inevitable: the product. Everything else — color, type, spacing — exists only to serve that presentation. The user feels they're looking at something engineered, not decorated.

Design references: Apple.com, Linear.app, Vercel, Raycast, Arc browser

---

## Color System

```
Background:    #000000 (pure black)
Surface:       #111111
Border:        #1d1d1d
Foreground:    #f5f5f7 (Apple's specific off-white)
Muted:         #86868b (Apple's gray)
Accent:        #0071e3 (Apple blue — exact)
Accent 2:      #2997ff (lighter blue for hover states)
```

**Light mode (for product feature sections):**
```
Background:    #ffffff
Surface:       #f5f5f7
Border:        #d2d2d7
Foreground:    #1d1d1f (Apple's near-black)
Muted:         #6e6e73
Accent:        #0066cc
```

Both modes are used within the same page (dark for hero/immersive, light for spec/feature sections).

---

## Typography

**Display:**
- SF Pro Display — weight 300-700 (Apple system font, available via -apple-system)
- Inter — weight 300-700 (cross-platform equivalent)

**Body:**
- SF Pro Text — weight 400
- Inter — weight 400

**Monospace (for code/specs):**
- SF Mono
- JetBrains Mono

**Note:** For Apple Minimal, Inter is an acceptable (even correct) choice because the aesthetic IS about system-quality interfaces, where Inter belongs.

**Size system:**
```
Display:   clamp(48px, 6vw, 96px)    weight 600, letter-spacing -0.025em
H1:        clamp(36px, 4.5vw, 72px)  weight 600, letter-spacing -0.02em
H2:        clamp(24px, 3vw, 48px)    weight 600, letter-spacing -0.015em
Body:      17px                       weight 400, line-height 1.6
Caption:   12px                       weight 400, letter-spacing 0.01em
```

Apple uses tight letter-spacing on display text — match this.

---

## Layout Principles

- Maximum whitespace around hero product imagery
- Section transitions from dark (hero) to light (feature details) to dark (CTA)
- Wide, centered single-column or symmetric two-column
- Product/screenshot always takes center stage — minimum 60% of section
- Specs and details in dense, compact tables
- No unnecessary decorative elements — every element has a purpose

**Grid:** Centered layout, 12 columns, minimal column usage. Content often spans only 6-8 of 12 columns, centered.

---

## Motion Profile

- **Speed:** Smooth. Durations 0.6s-1.0s.
- **Ease:** `power2.out` — no overshoot (like iOS UIKit animations)
- **Lenis lerp:** 0.10 — responsive, Apple-quality feel
- **Page load:** Content is present immediately; hero fades in with gentle opacity
- **Scroll reveals:** Parallax depth on product images (scroll up = product stays, content moves)
- **Pinned sections:** Product stays pinned as feature text scrolls alongside
- **Hover:** Blue tint on CTA, no transforms (Apple buttons don't lift)
- **3D transforms:** `perspective + rotateX` on device mockups on scroll

---

## Art Direction

**Primary:** Product screenshots and 3D device mockups as hero  
**Secondary:** Particle or glow effects (code art) for tech-forward sections

**Apple-style glow effect:**
```css
.product-glow {
  position: relative;
}
.product-glow::before {
  content: '';
  position: absolute;
  inset: -40px;
  background: radial-gradient(ellipse at 50% 100%, #0071e340 0%, transparent 70%);
  pointer-events: none;
}
```

**Screenshot presentation:**
```css
.device-frame {
  border-radius: 16px;
  box-shadow:
    0 0 0 1px rgba(255,255,255,0.08),
    0 32px 80px rgba(0,0,0,0.6);
  transform: perspective(1000px) rotateX(4deg);
  transform-origin: bottom;
}
```

---

## Signature Elements

- **Pinned product demo:** Product image stays while feature bullets scroll
- **Section mode switch:** Dark hero → light feature → dark CTA (Apple's standard page arc)
- **Spec table:** Clean, dense spec comparison (Apple's product page staple)
- **Animated number reveals:** "10x faster" — counts up on enter
- **Glow halos:** Subtle glow behind product screenshots

---

## Anti-Patterns for This DNA

- **Never:** Decorative typography (this is about readability, not type expression)
- **Never:** Complex animations (each transition serves navigation, not show)
- **Never:** Texture overlays or grain
- **Never:** Warm colors (this is always cool)
- **Never:** Borders around interactive elements (Apple UI doesn't use borders)
- **Never:** Rounded corners less than 8px or more than 24px (Apple's range)
- **Never:** Content without a clear visual hierarchy

---

## Component Recipes

### Pinned Scroll Feature Section
```html
<section class="feature-scroll">
  <div class="feature-device" data-gsap-pin>
    <img src="screenshot.png" class="device-frame" />
  </div>
  <div class="feature-content">
    <div class="feature-item" data-feature="1">
      <h3>Feature one</h3>
      <p>Description of the feature in 1-2 sentences.</p>
    </div>
    <div class="feature-item" data-feature="2">...</div>
  </div>
</section>
```

```js
// Pin device while features scroll
gsap.to('.feature-device', {
  scrollTrigger: {
    trigger: '.feature-scroll',
    start: 'top top',
    end: 'bottom bottom',
    pin: '.feature-device',
    pinSpacing: false,
  },
});
```

### Apple CTA Button
```css
.apple-cta {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 12px 22px;
  background: var(--color-accent);
  color: #fff;
  border-radius: 980px;
  font-size: 17px;
  font-weight: 400;
  text-decoration: none;
  transition: background 0.25s;
}
.apple-cta:hover { background: var(--color-accent-2); }
```
