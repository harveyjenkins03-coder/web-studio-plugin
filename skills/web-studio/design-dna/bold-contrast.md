# DNA Profile: Bold Contrast

**Category:** Dark / Impact  
**Mood:** Maximum contrast ratio, typographic aggression, the urgency of now

---

## Emotional Target

The design demands attention. Nothing is subtle. The typography is large, the contrast is extreme, the energy is high. It belongs to brands that have something important to say and refuse to be ignored.

Design references: Oatly packaging, MSCHF, Rick Owens digital, Nicce, anti-design brands, protest poster aesthetics

---

## Color System

```
Background:    #111111 (near-black — warm enough to not be harsh)
Surface:       #1a1a1a
Border:        #2d2d2d
Foreground:    #f5f5f5 (near-white)
Muted:         #777777
Accent:        #ff0044 (urgent red — Pantone 485 adjacent)
Accent 2:      #ffffff (white as second accent)
```

---

## Typography

**Display:**
- Monument Extended — weight 800 (ultra-wide, fills the screen)
- Druk Wide — weight 900 (ultimate impact)
- Bebas Neue — weight 400 (all-caps, fills space)
- Fjalla One — free alternative

**Body:**
- Anonymous Pro — monospace, typewriter feel
- Source Code Pro — technical clarity

**Size system:**
```
Display:   clamp(80px, 14vw, 240px)   weight 800, ALL CAPS
H1:        clamp(48px, 8vw, 120px)    weight 800
H2:        clamp(24px, 4vw, 56px)     weight 700
Body:      16px                        monospace, line-height 1.7
Label:     12px                        all-caps, tracking 0.2em
```

---

## Layout Principles

- Typography fills available width (vw-based sizing to edge)
- Extreme contrast between large and small elements
- Full-bleed sections with no side margins
- Content crashes against screen edges
- Dividing lines: full-width, heavy (2-4px)
- Numbers as huge decorative elements

---

## Motion Profile

- **Speed:** Fast and decisive. Durations 0.2s-0.5s.
- **Ease:** `power4.out` for reveals (slam in), `power4.in` for exits
- **Lenis lerp:** 0.14 — aggressive scroll weight
- **Reveal:** Text shears from off-screen, not fades
- **Hover:** Red fills element (0.15s), high contrast inversion

---

## Art Direction

**Primary:** Typography IS the art — no other art needed  
**Secondary:** High-contrast photography (duotone: red + black, or grayscale boosted)

**Duotone treatment:**
```css
.bold-duotone {
  filter: grayscale(100%) contrast(1.5) brightness(0.8);
  mix-blend-mode: multiply;
  background: var(--color-accent);
}
```

**SVG diagonal stripes (bold decoration):**
```css
.bold-stripes {
  background-image: repeating-linear-gradient(
    -45deg,
    transparent,
    transparent 10px,
    rgba(255, 0, 68, 0.15) 10px,
    rgba(255, 0, 68, 0.15) 20px
  );
}
```

---

## Signature Elements

- **Giant numbers:** Section numbers at 400px+ as background elements
- **Inversion sections:** Full-color-inverted sections (black on red/white)
- **Urgency typography:** "SALE ENDS IN" style countdown, monospace
- **Thick rule dividers:** 4px rules, full width
- **No-decoration CTA:** Button is just text with an underline — or fully filled block

---

## Anti-Patterns

- **Never:** Subtle anything
- **Never:** Serif fonts
- **Never:** Soft gradients
- **Never:** Small typography (everything is large or deliberately tiny)
- **Never:** Neutral palettes

---

## Component Recipes

### Impact Hero
```html
<section class="bold-hero">
  <div class="bold-hero-text">
    <p class="bold-label">BOLD CONTRAST</p>
    <h1 class="bold-headline">WE DO<br>THINGS<br>DIFFER<br>ENTLY</h1>
  </div>
</section>
```

```css
.bold-hero {
  min-height: 100svh;
  background: var(--color-bg);
  display: flex;
  align-items: flex-end;
  padding: 60px 0 40px;
}
.bold-headline {
  font-size: clamp(80px, 15vw, 220px);
  font-weight: 800;
  line-height: 0.88;
  text-transform: uppercase;
  letter-spacing: -0.02em;
  color: var(--color-fg);
}
.bold-headline em { color: var(--color-accent); font-style: normal; }
```

### Inversion CTA Section
```css
.inversion-section {
  background: var(--color-accent);
  color: var(--color-bg);
  padding: 120px 60px;
}
.inversion-section h2 {
  font-size: clamp(40px, 7vw, 100px);
  font-weight: 800;
  text-transform: uppercase;
  color: inherit;
}
.inversion-section a {
  color: inherit;
  text-decoration: underline;
  text-underline-offset: 6px;
  text-decoration-thickness: 2px;
}
```
