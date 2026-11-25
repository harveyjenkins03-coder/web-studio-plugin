# DNA Profile: Glass Morph

**Category:** Dark / Modern  
**Mood:** iOS 16 lock screen, frosted glass, depth through translucency

---

## Emotional Target

The site feels like holding something precious — layers of depth, translucent surfaces, color glowing through glass. It's the most immediately "current" of all profiles, referencing native app aesthetics.

Design references: Apple iOS system UI, Windows 11 Acrylic, Figma's own website, Craft docs, Notion dark, Linear dark mode

---

## Color System

```
Background:    #0d1117 (GitHub dark — reliable, not too blue, not too black)
Surface:       rgba(22, 27, 34, 0.8) (glass surfaces are semi-transparent)
Border:        rgba(240, 246, 252, 0.1)
Foreground:    #f0f6fc
Muted:         #8b949e
Accent:        #58a6ff (sky blue)
Accent 2:      #3fb950 (green — secondary, rare)
```

**Background gradient (mandatory — flat color kills glass effect):**
```css
body {
  background:
    radial-gradient(ellipse at top left, #161b27 0%, transparent 50%),
    radial-gradient(ellipse at bottom right, #0d2137 0%, transparent 50%),
    #0d1117;
}
```

---

## Typography

**Display:**
- Geist — weight 600-700 (Vercel's font, designed for dark UIs)
- Inter — weight 600-700 (acceptable here, native to this aesthetic)
- SF Pro Display — weight 500-700

**Body:**
- Geist — weight 400
- Inter — weight 400

**Size system:**
```
Display:   clamp(40px, 5.5vw, 80px)   weight 700, letter-spacing -0.02em
H1:        clamp(28px, 3.5vw, 56px)   weight 600, letter-spacing -0.015em
H2:        clamp(20px, 2.5vw, 36px)   weight 600
Body:      15px                         line-height 1.6
Caption:   13px                         muted
```

---

## Layout Principles

- Glass cards floating over a blurred, gradient background
- Depth layers: background gradient → blur layer → glass cards → content
- Component-level design: each glass card is a distinct layer
- Sidebar-and-content layouts (app-like)
- Consistent border radius (12-16px) throughout

---

## Motion Profile

- **Speed:** Snappy. Durations 0.3s-0.6s.
- **Ease:** `power2.out` — responsive, native feel
- **Lenis lerp:** 0.12 — crisp, app-like
- **Hover:** Glass surface brightens (opacity increase), border glow appears
- **Modal/dialog:** Scale from 0.95 → 1.0 with opacity, native iOS spring

---

## Art Direction

**Primary:** Generative gradient mesh behind glass surfaces  
**Secondary:** Blurred background imagery visible through glass panels

**Glass surface CSS:**
```css
.glass-card {
  background: rgba(22, 27, 34, 0.7);
  backdrop-filter: blur(20px) saturate(1.8);
  -webkit-backdrop-filter: blur(20px) saturate(1.8);
  border: 1px solid rgba(240, 246, 252, 0.1);
  border-radius: 16px;
}

/* Glass with colored tint */
.glass-card--accent {
  background: rgba(88, 166, 255, 0.08);
  border-color: rgba(88, 166, 255, 0.2);
}
```

**Gradient mesh background (behind glass):**
```css
.glass-bg {
  position: fixed;
  inset: 0;
  background:
    radial-gradient(at 20% 20%, rgba(88, 166, 255, 0.15) 0px, transparent 50%),
    radial-gradient(at 80% 80%, rgba(63, 185, 80, 0.10) 0px, transparent 50%),
    radial-gradient(at 50% 50%, rgba(13, 17, 23, 1) 0px, transparent 100%);
  z-index: -1;
}
```

---

## Signature Elements

- **Layered depth:** 3+ distinct depth levels visible simultaneously
- **Frosted glass panels:** `backdrop-filter: blur()` on all surfaces
- **Gradient glow:** Color halos behind key glass panels
- **Status indicators:** Small colored dots (green/yellow/red) as system status
- **Command palette:** `Cmd+K` style search/navigation component

---

## Anti-Patterns

- **Never:** Flat, opaque cards on this profile
- **Never:** Warm colors (glass is cool)
- **Never:** Serif typography
- **Never:** Heavy border widths
- **Never:** Saturated color areas larger than 20% of any surface

---

## Component Recipes

### Elevated Glass Card
```css
.glass-elevated {
  background: rgba(22, 27, 34, 0.6);
  backdrop-filter: blur(24px) saturate(2);
  -webkit-backdrop-filter: blur(24px) saturate(2);
  border: 1px solid rgba(240, 246, 252, 0.08);
  border-radius: 16px;
  box-shadow:
    0 1px 1px rgba(0, 0, 0, 0.3),
    0 8px 32px rgba(0, 0, 0, 0.4),
    inset 0 1px 0 rgba(255, 255, 255, 0.06);
  transition: border-color 0.2s, box-shadow 0.2s;
}
.glass-elevated:hover {
  border-color: rgba(88, 166, 255, 0.25);
  box-shadow:
    0 1px 1px rgba(0, 0, 0, 0.3),
    0 8px 32px rgba(0, 0, 0, 0.4),
    0 0 0 1px rgba(88, 166, 255, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
}
```
