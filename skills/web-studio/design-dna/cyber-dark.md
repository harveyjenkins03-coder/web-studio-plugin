# DNA Profile: Cyber Dark

**Category:** Dark / Technology  
**Mood:** Digital-native energy, hacker aesthetic, neon-on-void, the internet's dark heart

---

## Emotional Target

The site feels like it was built inside the terminal and then made beautiful. Technical capability radiates from every element. Neon on black isn't decoration — it's the native language of this aesthetic. The user feels they're looking at the future.

Design references: Linear.app dark mode, Vercel dashboard, Fig, Warp terminal, GitHub dark, shadcn/ui

---

## Color System

```
Background:    #050510 (near-black, deep blue-tinted)
Surface:       #0a0a1f
Border:        #1a1a3a
Foreground:    #e0e0ff (slightly blue-tinted white)
Muted:         #6060aa
Accent:        #00ffcc (electric teal — primary)
Accent 2:      #ff00aa (neon magenta — secondary, rare use)
```

**Always use a gradient body, not flat color:**
```css
body {
  background:
    radial-gradient(ellipse at 20% 50%, #0d0d2b 0%, #050510 60%),
    radial-gradient(ellipse at 80% 20%, #0a1020 0%, #050510 70%);
}
```

---

## Typography

**Display:**
- Neue Bit — pixel-adjacent, digital native
- Space Grotesk — weight 700 (technical feel)
- Geist — weight 700 (Vercel's font, native to this aesthetic)

**Body:**
- Space Grotesk — weight 400
- JetBrains Mono — for technical content (also acceptable as primary body)

**Monospace (code, specs, terminal):**
- JetBrains Mono
- Fira Code (with ligatures)
- Geist Mono

**Size system:**
```
Display:   clamp(48px, 7vw, 100px)   weight 700, letter-spacing -0.02em
H1:        clamp(32px, 4.5vw, 64px)  weight 700, letter-spacing -0.02em
H2:        clamp(20px, 2.5vw, 36px)  weight 600
Body:      16px                       line-height 1.7, letter-spacing 0.01em
Code:      14px mono                  line-height 1.6, teal accent for keywords
Label:     11px                       all-caps, tracking 0.15em, teal color
```

---

## Layout Principles

- Dark sections separated by subtle gradient shifts, not borders
- Code blocks as first-class visual elements (not tucked away)
- Technical specs presented in monospace tables
- Grid: typically 2-column (feature + code), or asymmetric (30% label + 70% content)
- Glow effects on CTA and key interactive elements
- Terminal-style components (command prompt aesthetic)

---

## Motion Profile

- **Speed:** Snappy. Durations 0.3s-0.6s.
- **Ease:** `power3.out` for reveals, `power4.out` for UI elements
- **Lenis lerp:** 0.10 — responsive, system-like
- **Page load:** Glitch animation on load (brief), then stable
- **Scroll reveals:** Fade + slight upward drift. Or clip-path from left (terminal typing feel)
- **Hover:** Neon glow adds on hover, subtle border glow
- **Text effect:** Scramble/glitch on headings that resolve to final text

---

## Art Direction

**Primary:** Generative code art — particle systems, wireframe geometry, abstract WebGL  
**Secondary:** Animated code snippets (highlighted syntax with cursor)

**Particle system (minimal, elegant):**
```js
// Sparse particle field — not chaotic, purposeful
const particles = new THREE.Points(geometry, new THREE.PointsMaterial({
  color: 0x00ffcc,
  size: 0.002,
  transparent: true,
  opacity: 0.4,
}));
```

**Neon glow effect:**
```css
.cyber-glow {
  text-shadow:
    0 0 10px var(--color-accent),
    0 0 40px color-mix(in srgb, var(--color-accent) 50%, transparent),
    0 0 80px color-mix(in srgb, var(--color-accent) 20%, transparent);
}
```

**Animated code block:**
```css
.code-block {
  background: rgba(10, 10, 31, 0.8);
  border: 1px solid rgba(0, 255, 204, 0.2);
  border-radius: 8px;
  font-family: var(--font-mono);
  font-size: 14px;
  backdrop-filter: blur(10px);
}
```

---

## Signature Elements

- **Glitch text effect** on hero headline (brief, then stable)
- **Code syntax highlighting** in teal/purple
- **Neon glow CTAs** with gradient border
- **Terminal prompt** (`>_`) as decorative section indicator
- **Animated cursor** (blinking underscore or block cursor style)

---

## Anti-Patterns for This DNA

- **Never:** Warm colors (orange, yellow, red — unless used as error states)
- **Never:** Serif typography
- **Never:** Light background sections
- **Never:** Soft, rounded UI (this is sharp and technical)
- **Never:** Photography (unless showing screens/code)
- **Never:** Generic SaaS icons (flat, colorful, friendly)

---

## Component Recipes

### Gradient Border Card
```css
.cyber-card {
  position: relative;
  background: rgba(10, 10, 31, 0.6);
  border-radius: 12px;
  backdrop-filter: blur(20px);
  padding: 28px;
}
.cyber-card::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 12px;
  padding: 1px;
  background: linear-gradient(135deg, rgba(0,255,204,0.4), rgba(255,0,170,0.2), transparent);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
}
```

### Neon CTA Button
```css
.cyber-btn {
  padding: 12px 32px;
  border: 1px solid var(--color-accent);
  background: transparent;
  color: var(--color-accent);
  border-radius: 6px;
  font-family: var(--font-mono);
  font-size: 14px;
  letter-spacing: 0.05em;
  position: relative;
  overflow: hidden;
  transition: color 0.3s, background 0.3s, box-shadow 0.3s;
}
.cyber-btn:hover {
  background: rgba(0, 255, 204, 0.1);
  box-shadow: 0 0 20px rgba(0, 255, 204, 0.3), inset 0 0 20px rgba(0, 255, 204, 0.05);
}
```
