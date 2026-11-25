# DNA Profile: Warm Gradient

**Category:** Light / Vibrant  
**Mood:** Joyful energy, sunset warmth, creative abundance

---

## Emotional Target

The site feels alive — warm, energetic, generative. Color gradients breathe and shift. The user feels optimistic. This is not corporate warmth (beige) but vivid, expressive warmth (coral, amber, fuchsia).

Design references: Stripe.com (early gradient era), Linear.app light, Notion marketing, Framer, Loom

---

## Color System

```
Background:    #fef3e2 (warm cream)
Surface:       #fde8c8
Border:        #f4c89e
Foreground:    #1c0d00 (very dark warm brown)
Muted:         #a06040
Accent:        #e85d04 (burnt orange)
Accent 2:      #f72585 (hot pink)
```

**Gradient system (the signature):**
```css
--gradient-hero: linear-gradient(135deg, #ff9966 0%, #ff5e62 50%, #c026d3 100%);
--gradient-warm: linear-gradient(135deg, #fde8c8 0%, #fef3e2 100%);
--gradient-accent: linear-gradient(90deg, #e85d04, #f72585);
```

---

## Typography

**Display:**
- Clash Display — weight 600-700 (modern but with personality)
- Cabinet Grotesk — weight 700-800
- Syne — weight 700-800

**Body:**
- Satoshi — weight 400
- General Sans — weight 400

**Size system:**
```
Display:   clamp(56px, 8vw, 120px)   weight 700, letter-spacing -0.02em
H1:        clamp(40px, 5vw, 72px)    weight 700
H2:        clamp(24px, 3vw, 40px)    weight 600
Body:      17px                       line-height 1.7
```

---

## Layout Principles

- Gradient meshes as section backgrounds (not flat colors)
- Cards with gradient borders or subtle gradient fills
- Rounded corners throughout (16-24px)
- Playful asymmetry in image/text blocks
- Oversized section decorations (large blobs, circles)

---

## Motion Profile

- **Speed:** Fluid. Durations 0.7s-1.0s.
- **Ease:** `power3.out`, occasional `back.out(1.3)` for playful bounces
- **Lenis lerp:** 0.09 — smooth but energetic
- **Gradient animation:** Background gradients shift slowly (CSS @keyframes)
- **Hover:** Cards lift (8px) with expanded shadow, gradient border glows
- **Scroll:** Color zones shift as user progresses through page

---

## Art Direction

**Primary:** Generative gradient mesh art — animated CSS radial gradients  
**Secondary:** Smart photo sourcing with warm, vibrant treatment

**Animated gradient hero:**
```css
.gradient-hero {
  background: linear-gradient(-45deg, #e85d04, #f72585, #fde8c8, #e85d04);
  background-size: 400% 400%;
  animation: gradient-shift 12s ease infinite;
}
@keyframes gradient-shift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

**Gradient text:**
```css
.gradient-headline {
  background: var(--gradient-accent);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## Signature Elements

- **Animated gradient background** in hero — slow, breathing color shift
- **Gradient text** on key headlines
- **Rounded gradient cards** with color-shifting borders
- **Blob shapes** (CSS clip-path or SVG) as section decorations
- **Warm photo treatment** (boosted saturation, warm filter)

---

## Anti-Patterns

- **Never:** Dark backgrounds (this is always light)
- **Never:** Cold colors (blues/teals unless as tiny accents)
- **Never:** Hard edges, 0px border-radius
- **Never:** Monochrome or desaturated imagery
- **Never:** Formal, corporate typography

---

## Component Recipes

### Gradient Border Card
```css
.warm-card {
  background: white;
  border-radius: 20px;
  padding: 28px;
  position: relative;
  box-shadow: 0 8px 40px rgba(232, 93, 4, 0.12);
  transition: transform 0.3s, box-shadow 0.3s;
}
.warm-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 20px 60px rgba(232, 93, 4, 0.2);
}
.warm-card::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 20px;
  padding: 2px;
  background: var(--gradient-accent);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  opacity: 0;
  transition: opacity 0.3s;
}
.warm-card:hover::before { opacity: 1; }
```
