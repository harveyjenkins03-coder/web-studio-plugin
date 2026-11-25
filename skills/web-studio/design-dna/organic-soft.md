# DNA Profile: Organic Soft

**Category:** Light / Natural  
**Mood:** Warmth, handcraft, living things, the Sunday morning feeling

---

## Emotional Target

The site feels like a brand that cares — about materials, about people, about slowing down. Nothing is sharp or urgent. Colors feel like they came from nature. Typography has warmth. The user feels at ease.

Design references: Patagonia digital, Aesop, Kinfolk, Abel & Cole, Wild brand sites, artisan food brands

---

## Color System

```
Background:    #f8f5f0 (warm cream)
Surface:       #f0ebe3
Border:        #ddd5c8
Foreground:    #2a2318 (warm dark brown)
Muted:         #8a7c6e
Accent:        #5e8c61 (sage green)
Accent 2:      #c17f53 (terracotta)
```

**Seasonal variant (autumn):**
```
Accent:    #c17f53 (terracotta)
Accent 2:  #8b6914 (ochre)
```

**Extended palette for image treatments:**
```
Tint:  rgba(93, 79, 57, 0.05)  /* warm vignette */
```

---

## Typography

**Display:**
- Cormorant Garamond — weight 300-400, regular (not italic)
- Recoleta — weight 300-400 (warm, rounded serif)
- Lora — weight 400 (free, warm)

**Body:**
- Literata — weight 400, line-height 1.9
- Spectral — weight 400 (free alternative)

**Utility:**
- DM Sans — weight 300-400 (earthy, not corporate)
- Jost — weight 300

**Size system:**
```
Display:   clamp(48px, 6vw, 96px)    weight 300, line-height 1.1
H1:        clamp(36px, 4.5vw, 64px)  weight 400, line-height 1.2
H2:        clamp(24px, 2.5vw, 36px)  weight 400
Body:      18px                       line-height 1.9
Small:     14px                       line-height 1.6
```

---

## Layout Principles

- Breathing room: section padding 120px minimum
- Wide body text columns but not full-width (max 700px centered or left-aligned)
- Images take up space — no tiny thumbnails, at minimum 50% column width
- Organic shapes: clip-paths with gentle curves, not hard rectangles
- Intentional imperfection: slight rotations (2-4deg) on decorative elements
- Handwritten or textured elements as accents

**Grid:** Simple 2-column or single column. No complex grids — clarity is the point.

---

## Motion Profile

- **Speed:** Slow and gentle. Durations 0.9s-1.5s.
- **Ease:** `power2.out`, `sine.inOut` — smooth, no sharp edges in timing
- **Lenis lerp:** 0.07 — floating, dreamy scroll
- **Page load:** No preloader. Simple fade-in.
- **Scroll reveals:** Soft fade + upward drift (40px). No sharp wipes.
- **Hover:** Gentle brightening, slight scale-up (scale: 1.02), soft transition
- **No:** Fast snaps, rotation animations, jarring reveals

---

## Art Direction

**Primary:** Smart photo sourcing — natural light, human touch, material textures  
**Secondary:** Generative CSS art (noise-based texture overlays)

**Photo style:** Natural light only. Warm color temperature. Material textures (wood, stone, linen, ceramic). Human hands in frame where possible. Zero stock-photo posing.

**Unsplash query style for this DNA:**
```
"natural light ceramic bowl textured background"
"handmade linen textile close-up warm"
"sage plant morning light soft focus"
"artisan bread wooden table warm light"
```

**CSS image treatment:**
```css
.organic-image {
  filter: warm(0.1) brightness(1.02) saturate(0.9);
  /* Simulated warm filter: */
  filter: sepia(8%) brightness(1.02) saturate(0.92);
}

/* Wavy clip-path */
.organic-clip {
  clip-path: ellipse(90% 85% at 50% 50%);
}
```

**Noise texture (CSS, no image):**
```css
.organic-texture::after {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,...");
  opacity: 0.03;
  pointer-events: none;
}
```

---

## Signature Elements

- **Slightly rotated decorative elements** (2-4deg): Pull quotes, section labels
- **Organic shapes:** Circle and blob clip-paths on images instead of rectangles
- **Hand-drawn underlines:** SVG wave underline on key terms
- **Material texture overlay:** Subtle noise/grain on sections
- **Botanical line illustrations:** Simple SVG botanicals as decorative accents

---

## Anti-Patterns for This DNA

- **Never:** Hard edges with 0px border-radius on image containers
- **Never:** Dark backgrounds (this profile is always light)
- **Never:** Electric or neon accent colors
- **Never:** Sans-serif display fonts without warmth
- **Never:** Fast, aggressive animations
- **Never:** Stock photo body language (pointing at laptop, handshake)
- **Never:** Corporate visual language of any kind

---

## Component Recipes

### Product/Feature Card
```
Organic shape clip (ellipse or blob) on image top
Image: 200-300px tall, full card width
Padding: 28px
Category label: sage green, 12px, small-caps
Product name: display serif, 24px
Short description: 15px, muted, line-height 1.7
Price or CTA: terracotta accent, no border-radius button (gentle: 4px)
Thin 1px border in border color
```

### Section Layout (About / Philosophy)
```
Full-width, warm cream background
Large display serif pull quote, centered, weight 300
Below: 2-column layout — body text left, rotated image right
Image has organic clip-path (blob shape)
Thin terracotta rule at section top
```
