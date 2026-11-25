# DNA Profile: Retro Future

**Category:** Light-Warm / Nostalgic-Forward  
**Mood:** NASA optimism, 1970s-80s tech catalog, warm analog + digital hybrid

---

## Emotional Target

The site evokes the optimistic futurism of the space age and early personal computing era — warm paper colors, orange and navy accents, bold sans-serifs with personality. It feels like a lovingly restored artifact from the future that never happened.

Design references: NASA Worm era graphics, Braun product catalogs, Letraset type sheets, vintage Radio Shack ads, The Wes Anderson aesthetic applied to tech

---

## Color System

```
Background:    #f0ede5 (warm off-white, like aged paper)
Surface:       #e8e4da
Border:        #c8c4b8
Foreground:    #1a1815 (warm near-black)
Muted:         #7a786e
Accent:        #f4520c (NASA tangerine orange)
Accent 2:      #1a3a5c (deep navy)
```

---

## Typography

**Display:**
- Grilli Type GT Pressura — weight 700 (geometric, slightly retro)
- DM Serif Display — weight 400 (editorial warmth)
- Optima — weight 400-700 (humanist, period-appropriate)

**Body:**
- Grilli Type GT Walsheim — weight 400
- DM Sans — weight 300-400

**Monospace (for data, specs):**
- IBM Plex Mono (IBM's own aesthetic fits perfectly)

**Size system:**
```
Display:   clamp(56px, 8vw, 120px)   weight 700, tracking -0.01em
H1:        clamp(40px, 5vw, 72px)    weight 700
H2:        clamp(24px, 3vw, 40px)    weight 400
Body:      17px                       weight 400, line-height 1.75
Label:     12px                       all-caps, tracking 0.12em
```

---

## Layout Principles

- Horizontal bands of alternating background colors (cream / navy / cream)
- Bold typographic blocks: large type as compositional element
- Data presented in table format (IBM-style)
- Geometric shapes (circles, squares) as section markers
- Dashes, rules, and grid lines as design elements
- Circular motifs (NASA influence)

---

## Motion Profile

- **Speed:** Decisive. Durations 0.5s-0.9s.
- **Ease:** `power3.out` — not slow, not snappy
- **Lenis lerp:** 0.10 — confident scroll
- **Reveal:** Bold type slams from left or top (fast reveal, then settles)
- **Hover:** Orange underline extends, navy background fills on buttons
- **Transitions:** Section backgrounds shift with smooth color transition

---

## Art Direction

**Primary:** Custom SVG geometric compositions — circles, chevrons, grid marks, NASA-style diagram aesthetics  
**Secondary:** Smart photo sourcing (warm-filtered, technical/industrial subjects)

**NASA diagram style:**
```html
<svg viewBox="0 0 400 300" class="retro-diagram">
  <!-- Technical diagram aesthetic -->
  <circle cx="200" cy="150" r="80" fill="none" stroke="#f4520c" stroke-width="1"/>
  <circle cx="200" cy="150" r="40" fill="none" stroke="#1a3a5c" stroke-width="0.5" stroke-dasharray="5 3"/>
  <line x1="0" y1="150" x2="400" y2="150" stroke="#1a1815" stroke-width="0.5" opacity="0.3"/>
  <line x1="200" y1="0" x2="200" y2="300" stroke="#1a1815" stroke-width="0.5" opacity="0.3"/>
  <!-- Crosshair markers -->
  <text x="210" y="145" font-size="10" fill="#f4520c" font-family="IBM Plex Mono">ORIGIN</text>
</svg>
```

**Photo treatment:**
```css
.retro-image {
  filter: sepia(15%) warm(0.05) brightness(1.05) contrast(0.95);
  /* Simulated: */
  filter: sepia(15%) brightness(1.05) contrast(0.95) saturate(0.9);
}
```

---

## Signature Elements

- **Section color bands:** Alternating warm-white and navy backgrounds
- **Bold type as art:** Single words at 200px+ as section backgrounds
- **Circle motifs:** Perfectly circular elements, orange or navy
- **Typewriter effect:** Text that types itself (IBM aesthetic)
- **Grid overlays:** Faint grid lines visible in dark sections

---

## Anti-Patterns

- **Never:** Cool grays or blue-whites
- **Never:** Dark backgrounds as primary (navy is used in bands, not full pages)
- **Never:** Electric neon colors (this is warm and analog)
- **Never:** Thin, delicate serifs
- **Never:** Organic, curved shapes (this is geometric)

---

## Component Recipes

### Color Band Section
```css
.retro-band {
  background: var(--color-accent-2); /* navy */
  color: var(--color-bg);
  padding: 80px 0;
}
.retro-band h2 { color: var(--color-accent); }  /* orange on navy */
.retro-band p  { color: rgba(240, 237, 229, 0.8); }
```

### NASA-Style Button
```css
.retro-btn {
  padding: 14px 32px;
  border: 2px solid var(--color-accent);
  background: transparent;
  color: var(--color-accent);
  font-family: var(--font-body);
  font-size: 13px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  border-radius: 0;
  position: relative;
  overflow: hidden;
  transition: color 0.3s;
}
.retro-btn::before {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-accent);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s cubic-bezier(0.77,0,0.175,1);
}
.retro-btn:hover { color: #f0ede5; }
.retro-btn:hover::before { transform: scaleX(1); }
.retro-btn span { position: relative; z-index: 1; }
```
