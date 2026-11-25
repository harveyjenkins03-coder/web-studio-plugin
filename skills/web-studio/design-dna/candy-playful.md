# DNA Profile: Candy Playful

**Category:** Light / Expressive  
**Mood:** Sugar rush creativity, Gen-Z maximalism, joyful chaos with hidden order

---

## Emotional Target

The site is fun — unabashedly, unapologetically fun. Colors pop. Shapes are friendly and bouncy. Interactions feel rewarding. The brand clearly doesn't take itself too seriously, and that's the point.

Design references: Duolingo, Headspace, Notion's playful mode, Superhi, early Mailchimp, Candy Crush brand aesthetics, illustration-heavy startups

---

## Color System

```
Background:    #fdf4ff (barely-there purple-white)
Surface:       #f0e4f8
Border:        #d4a8e8
Foreground:    #1a0828 (deep purple-black)
Muted:         #8060a0
Accent:        #c026d3 (fuchsia — Tailwind fuchsia-600)
Accent 2:      #06b6d4 (cyan — Tailwind cyan-500)
Accent 3:      #fb923c (orange — used sparingly for a third pop)
```

---

## Typography

**Display:**
- Syne — weight 700-800 (playful but structured)
- Clash Display — weight 600-700
- Quicksand — weight 700 (friendly, rounded)

**Body:**
- Plus Jakarta Sans — weight 400 (clean but with personality)
- Nunito — weight 400 (soft, rounded)

**Size system:**
```
Display:   clamp(48px, 7vw, 100px)   weight 800, slight tracking
H1:        clamp(32px, 4.5vw, 64px)  weight 700
H2:        clamp(22px, 3vw, 36px)    weight 700
Body:      16-17px                    line-height 1.65
Label:     12px                       semi-bold, friendly color
```

---

## Layout Principles

- Friendly rounded corners everywhere (20-32px on cards)
- Overlapping elements (cards, illustrations) for depth
- Bold color blocks as section backgrounds (alternating fuchsia, cyan, yellow)
- Large custom illustrations or 3D character art
- Sticker-like decorative elements (rotated, overlapping)
- Confetti, sparkle, or particle effects on interactions

---

## Motion Profile

- **Speed:** Energetic. Durations 0.4s-0.7s.
- **Ease:** `back.out(1.7)` for reveals (overshoot, springy), `elastic.out` for interactions
- **Lenis lerp:** 0.13 — bouncy scroll
- **Hover:** Elements grow (scale 1.05), shadow expands, color brightens
- **Confetti:** Released on important actions (completion, signup)
- **Characters/mascots:** Animate on hover or scroll enter

---

## Art Direction

**Primary:** Custom SVG illustrations — friendly characters, emoji-adjacent icons  
**Secondary:** Generative CSS art (confetti, bubble clusters)

**Bubble decoration:**
```css
.bubble-decoration {
  position: absolute;
  border-radius: 50%;
  background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.4), transparent);
}
.bubble-decoration--lg {
  width: 120px;
  height: 120px;
  background-color: rgba(192, 38, 211, 0.15);
  animation: bubble-float 6s ease-in-out infinite;
}
@keyframes bubble-float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50%       { transform: translateY(-20px) rotate(5deg); }
}
```

**Sticker elements (CSS blob shapes):**
```css
.sticker {
  display: inline-flex;
  padding: 8px 16px;
  border-radius: 100px;
  background: var(--color-accent);
  color: white;
  font-weight: 700;
  font-size: 13px;
  transform: rotate(-3deg);
  box-shadow: 0 4px 12px rgba(192, 38, 211, 0.3);
}
```

---

## Signature Elements

- **Mascot/character** that reacts to user interaction
- **Confetti burst** on important completion events
- **Bouncy button animations** (`elastic.out` on hover release)
- **Floating decorative elements** (blobs, stars, sparkles) with CSS animation
- **Color-block sections:** Alternating solid color backgrounds

---

## Anti-Patterns

- **Never:** Dark backgrounds (except deliberate color blocks)
- **Never:** Formal serif typography
- **Never:** Professional-neutral palettes
- **Never:** Understated, slow animations
- **Never:** Excessive whitespace (this profile fills its space)

---

## Component Recipes

### Playful Card
```css
.candy-card {
  background: white;
  border-radius: 24px;
  padding: 28px;
  border: 2px solid transparent;
  background-clip: padding-box;
  box-shadow:
    0 2px 0 var(--color-border),
    0 6px 24px rgba(192, 38, 211, 0.1);
  transition: transform 0.2s cubic-bezier(0.34,1.56,0.64,1),
              box-shadow 0.2s;
}
.candy-card:hover {
  transform: translateY(-4px) scale(1.01);
  box-shadow:
    0 2px 0 var(--color-border),
    0 12px 40px rgba(192, 38, 211, 0.2);
}
```

### Sparkle Button
```html
<button class="sparkle-btn">
  <span class="sparkle-btn-text">Get started</span>
  <span class="sparkle-icon" aria-hidden="true">✨</span>
</button>
```

```css
.sparkle-btn {
  padding: 14px 28px;
  border-radius: 100px;
  background: linear-gradient(135deg, #c026d3, #7c3aed);
  color: white;
  font-weight: 700;
  font-size: 16px;
  border: none;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: transform 0.2s cubic-bezier(0.34,1.56,0.64,1),
              box-shadow 0.2s;
  box-shadow: 0 4px 20px rgba(192, 38, 211, 0.35);
}
.sparkle-btn:hover {
  transform: translateY(-2px) scale(1.02);
  box-shadow: 0 8px 28px rgba(192, 38, 211, 0.45);
}
.sparkle-btn:active {
  transform: scale(0.97);
}
```
