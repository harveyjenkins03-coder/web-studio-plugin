# Color Systems Reference

This reference governs palette generation during Phase 1 (Design DNA Extraction) and palette application during Phase 3 (Typography, Color, Skin & Art). Every palette produced by Web Studio must follow these rules to achieve production-quality, cohesive color systems that avoid generic AI aesthetics.

---

## 1. Palette Generation Strategies

Every palette begins with a **base hue** (0-360 on the HSL wheel). From that single hue, derive all six token roles: `bg`, `surface`, `text`, `muted`, `accent`, `accent2`. The strategy determines how hues relate to each other.

### Monochromatic

All colors share the same hue. Variation comes from saturation and lightness shifts. Produces the most cohesive, restrained palettes. Best for luxury, editorial, and minimalist DNA profiles.

**Derivation from base hue (H = 220, deep navy):**

| Token    | Rule                                      | Example       |
|----------|-------------------------------------------|---------------|
| bg       | H, low saturation (8-15%), very low L     | `#0d1117`     |
| surface  | H, low saturation (8-12%), L +8-12%       | `#161b22`     |
| text     | H, very low saturation (3-6%), high L     | `#e6edf3`     |
| muted    | H, low saturation (6-10%), mid L          | `#7d8590`     |
| accent   | H, high saturation (60-80%), mid-high L   | `#58a6ff`     |
| accent2  | H, moderate saturation (40-55%), offset L | `#a5d6ff`     |

The accent is the same hue pushed to high saturation. The accent2 is a lighter or desaturated variant of the accent. The entire palette breathes in one color family.

### Complementary

Two hues 180 degrees apart on the wheel. High contrast, high energy. The complement becomes the accent. Best for bold, confident, high-impact DNA profiles.

**Derivation from base hue (H = 25, warm amber):**

| Token    | Rule                                         | Example       |
|----------|----------------------------------------------|---------------|
| bg       | H, low saturation, very low L                | `#120e0a`     |
| surface  | H, low saturation, L +10%                    | `#1c1612`     |
| text     | H, very low saturation, high L (warm white)  | `#f5efe8`     |
| muted    | H, low saturation, mid L                     | `#8a7e72`     |
| accent   | H+180 (205), high saturation, mid-high L     | `#3b9edb`     |
| accent2  | H, high saturation, mid-high L               | `#e8923a`     |

The background and text live in the warm family. The accent is the cool complement that pops against the warmth. The accent2 is a saturated version of the base hue for secondary emphasis.

### Split-Complementary

The base hue plus two hues flanking its complement (complement +/- 30 degrees). More nuanced than pure complementary, less likely to clash. Best for vibrant but sophisticated DNA profiles.

**Derivation from base hue (H = 160, teal-green):**

| Token    | Rule                                           | Example       |
|----------|-------------------------------------------------|---------------|
| bg       | H, low saturation, very low L                  | `#0a1210`     |
| surface  | H, low saturation, L +8%                       | `#121e1b`     |
| text     | H, very low saturation, high L                 | `#e8f0ed`     |
| muted    | H, low saturation, mid L                       | `#6d8a82`     |
| accent   | H+150 (310), high saturation, mid-high L       | `#d946a8`     |
| accent2  | H+210 (10), high saturation, mid-high L        | `#e85d45`     |

The two accents are warm-spectrum hues (magenta and coral-red) flanking the complement of the cool-spectrum base. This creates a warm-accent-on-cool-background dynamic that feels rich without clashing.

### Analogous

Three hues adjacent on the wheel (base +/- 30 degrees). Harmonious and soothing. Best for calm, nature-inspired, editorial DNA profiles.

**Derivation from base hue (H = 35, warm gold):**

| Token    | Rule                                      | Example       |
|----------|-------------------------------------------|---------------|
| bg       | H, low saturation, very low L             | `#12100a`     |
| surface  | H, low saturation, L +8%                  | `#1e1a12`     |
| text     | H, very low saturation, high L            | `#f2ede5`     |
| muted    | H, low saturation, mid L                  | `#8a8070`     |
| accent   | H-30 (5), high saturation, mid L          | `#c44230`     |
| accent2  | H+30 (65), moderate saturation, mid-high L| `#b8a44a`     |

All three active hues (red-orange, gold, yellow-green) sit within a 60-degree arc. The palette feels warm and unified. Analogous palettes need careful lightness variation to maintain hierarchy since the hues alone do not create strong contrast.

### Triadic

Three hues evenly spaced 120 degrees apart. Balanced, colorful, energetic. Best for playful, creative, youthful DNA profiles. Requires discipline to prevent carnival chaos.

**Derivation from base hue (H = 0, red):**

| Token    | Rule                                          | Example       |
|----------|-----------------------------------------------|---------------|
| bg       | H+240 (240), very low saturation, very low L  | `#0c0c14`     |
| surface  | H+240 (240), very low saturation, L +8%       | `#14141e`     |
| text     | H+240 (240), very low saturation, high L      | `#eae8f0`     |
| muted    | H+240 (240), low saturation, mid L            | `#7a788a`     |
| accent   | H (0), high saturation, mid-high L            | `#e84545`     |
| accent2  | H+120 (120), moderate saturation, mid L       | `#3ab858`     |

The background lives in the blue family (quietest of the three). Red and green become the two accents. One accent should dominate (70/30 usage split) to prevent visual competition.

---

## 2. Color Ratio Rules

Color distribution determines visual hierarchy. The ratios below dictate how much visual area each color occupies across the full page.

### Dark Themes

```
Background (bg):     85% of total visual area
Text (text + muted): 10% of total visual area
Accent (accent):      5% of total visual area
```

Dark themes are dominated by their background. The darkness IS the design. Text sits on the darkness. Accent punctuates sparingly. The 5% accent rule is critical: if accent color covers more than 5% of the viewport at any scroll position, it stops being an accent and becomes a second background. Reduce usage.

**Where the 5% lives:**
- CTA buttons (1-2 per viewport)
- Link underlines and hover states
- Active navigation indicators
- Progress bars and loaders
- Icon highlights and badge dots
- Border accents on featured cards (top or left edge only, not full border)

**Where accent should NOT appear in dark themes:**
- Full-width section backgrounds
- Large illustration fills
- Background gradients covering more than 20% of a section
- Every heading (use text color for headings, accent for emphasis within text)

### Light Themes

```
Background (bg):     70% of total visual area
Text (text + muted): 20% of total visual area
Accent (accent):     10% of total visual area
```

Light themes can afford more accent coverage because the lighter background has less visual weight. The eye tolerates larger color areas against light surfaces. The text takes more visual area because dark text on light surfaces has higher visual weight than light text on dark surfaces.

**Additional light theme budget:**
- Section dividers and decorative rules can use accent
- Card borders and outlines can carry accent tints
- Background tints (accent at 5-8% opacity) for featured sections
- Accent2 can fill illustration areas and decorative shapes

### Dual Theme Distribution

When a design supports both themes, define separate ratios and respect the shift in accent tolerance:

```
Dark mode:
  bg: 85%  |  text: 10%  |  accent: 5%

Light mode:
  bg: 70%  |  text: 20%  |  accent: 10%
```

The accent color itself may also need adjustment between modes. An accent that looks restrained at 5% coverage in dark mode may look aggressive at 10% coverage in light mode even though 10% is the budget. Desaturate or shift the accent lightness when switching modes to maintain equivalent visual weight.

### Surface Allocation

Surface sits between bg and text in the hierarchy. Its allocation comes from the bg budget:

```
Dark theme:  bg 70% + surface 15% = 85% total dark area
Light theme: bg 55% + surface 15% = 70% total light area
```

Surface should appear on:
- Navigation bars and sticky headers
- Card backgrounds
- Modal and dialog backgrounds
- Dropdown menus
- Code blocks and blockquotes
- Sidebar backgrounds

---

## 3. Accent Color Psychology

The accent color is the emotional signature of the design. It communicates mood, energy, and intent before the user reads a single word. Select accents based on the DNA profile's emotional target.

### Warm Accents (Hue 0-60, 330-360)

**Colors:** Reds, oranges, corals, ambers, warm pinks

**Psychological signals:** Energy, urgency, passion, action, warmth, appetite, excitement

**Best matched to DNA profiles that target:**
- E-commerce and conversion-focused sites (red/orange CTAs convert higher in A/B tests)
- Food, restaurant, and hospitality brands
- Entertainment, gaming, and media platforms
- Fitness, sports, and high-energy brands
- Startup landing pages that need aggressive CTAs
- Personal brands with a bold, confident voice

**Specific accent recommendations:**

| Accent Hex | Name           | Best for                           |
|------------|----------------|------------------------------------|
| `#e85d45`  | Burnt coral    | Premium warmth without aggression  |
| `#ff6b35`  | Tangerine      | Energetic, playful, startup energy |
| `#c44230`  | Brick red      | Serious warmth, editorial gravitas |
| `#e8923a`  | Amber          | Approachable, friendly, inviting   |
| `#d4594e`  | Dusty rose-red | Subtle warmth, fashion, lifestyle  |
| `#f0a050`  | Marigold       | Optimistic, creative, artisanal    |

### Cool Accents (Hue 180-270)

**Colors:** Blues, teals, cyans, indigos, blue-violets

**Psychological signals:** Trust, calm, professionalism, technology, intelligence, stability, depth

**Best matched to DNA profiles that target:**
- SaaS, developer tools, and technology platforms
- Financial services, insurance, and B2B enterprise
- Healthcare and wellness brands
- Corporate and institutional sites
- Data visualization and analytics platforms
- Communication and productivity tools

**Specific accent recommendations:**

| Accent Hex | Name           | Best for                            |
|------------|----------------|-------------------------------------|
| `#58a6ff`  | Sky blue       | Dev tools, open source, tech        |
| `#3b9edb`  | Ocean blue     | SaaS, corporate, trust              |
| `#00b4d8`  | Cyan           | Innovation, modern tech, startups   |
| `#4ea8a6`  | Teal           | Wellness, calm tech, sustainability |
| `#6366f1`  | Indigo         | Creative tech, design tools, AI     |
| `#0ea5e9`  | Bright cerulean| Communication, social, connectivity |

### Neutral / Earth Accents (Hue 30-50 desaturated, or achromatic)

**Colors:** Golds, taupes, warm grays, champagne, bronze, olive

**Psychological signals:** Luxury, sophistication, timelessness, natural, organic, understated confidence

**Best matched to DNA profiles that target:**
- Luxury brands, high-end fashion, premium goods
- Architecture, interior design, real estate
- Wine, spirits, and gourmet food brands
- Art galleries, museums, cultural institutions
- Personal portfolio sites for creatives seeking understatement
- Editorial and literary publications

**Specific accent recommendations:**

| Accent Hex | Name           | Best for                              |
|------------|----------------|---------------------------------------|
| `#c9a96e`  | Antique gold   | Luxury, premium, timeless             |
| `#a0845c`  | Bronze         | Warm sophistication, craft, artisanal |
| `#8b8578`  | Warm taupe     | Ultra-minimal, Scandinavian, gallery  |
| `#b5a48c`  | Champagne      | Fashion, beauty, editorial            |
| `#7a8450`  | Sage olive     | Organic, sustainable, nature-aligned  |
| `#9b8e7e`  | Greige         | Architectural, modern, restrained     |

### Green / Yellow-Green Accents (Hue 90-170)

**Colors:** Greens, limes, emeralds, mints, chartreuse

**Psychological signals:** Growth, nature, success, health, freshness, permission, go-signal

**Best matched to DNA profiles that target:**
- Sustainability and environmental brands
- Health, nutrition, and organic products
- Finance and fintech (money / growth associations)
- Agriculture and outdoor brands
- Success states and positive feedback UI

**Specific accent recommendations:**

| Accent Hex | Name           | Best for                              |
|------------|----------------|---------------------------------------|
| `#3ab858`  | Leaf green     | Success, growth, positive action      |
| `#10b981`  | Emerald        | Fintech, health tech, modern green    |
| `#84cc16`  | Lime           | Energy, youth, bold freshness         |
| `#22c55e`  | Vivid green    | CTAs, confirmation, go-states         |
| `#6b8f5e`  | Moss           | Natural, organic, earthy              |
| `#a3e635`  | Chartreuse     | High-energy creative, nightlife, bold |

### Purple / Magenta Accents (Hue 270-330)

**Colors:** Purples, violets, magentas, fuchsias, plums

**Psychological signals:** Creativity, imagination, mystery, spirituality, premium, unconventional

**Best matched to DNA profiles that target:**
- Creative agencies and design studios
- Music, art, and entertainment brands
- Spiritual, wellness, and mindfulness platforms
- Premium and exclusive memberships
- Gen-Z and youth-oriented brands
- Unconventional or counter-cultural brands

**Specific accent recommendations:**

| Accent Hex | Name           | Best for                              |
|------------|----------------|---------------------------------------|
| `#a855f7`  | Amethyst       | Creative tech, design tools           |
| `#d946a8`  | Hot magenta    | Bold creative, fashion, nightlife     |
| `#8b5cf6`  | Violet         | Premium, mysterious, imaginative      |
| `#c084fc`  | Lavender       | Gentle creativity, wellness           |
| `#9333ea`  | Deep purple    | Luxury, exclusive, premium            |
| `#e879a8`  | Rose pink      | Beauty, lifestyle, feminine energy    |

---

## 4. Dark Theme Rules

Dark themes are the default premium aesthetic. They convey sophistication, focus, and modern sensibility. But dark themes are easy to get wrong. Follow these rules precisely.

### Never Use Pure Black or Pure White

Pure `#000000` black is harsh, unnatural, and creates excessive contrast that fatigues the eye. Pure `#ffffff` white on a dark background creates a halation effect where light text appears to bleed outward, reducing readability.

```
BANNED:  #000000 as background
BANNED:  #ffffff as text color
BANNED:  #000 shorthand anywhere in dark themes
BANNED:  #fff shorthand anywhere in dark themes
```

### Warm Darks Are Premium, Cold Darks Are Clinical

The temperature of the dark background sets the entire mood.

**Warm darks** (slight red/orange/yellow undertone):
```css
/* These feel premium, inviting, luxurious */
--color-bg: #0a0908;  /* warm near-black, barely perceptible amber */
--color-bg: #0f0d0b;  /* dark chocolate undertone */
--color-bg: #100e0c;  /* espresso warmth */
--color-bg: #0d0b09;  /* charred wood */
```

**Cool darks** (slight blue/green undertone):
```css
/* These feel technical, focused, digital */
--color-bg: #0a0c10;  /* ink blue-black */
--color-bg: #0b0d12;  /* deep navy void */
--color-bg: #0d1117;  /* GitHub-style dark slate */
--color-bg: #0c0e14;  /* midnight */
```

**Neutral darks** (no hue bias, balanced):
```css
/* These feel clean, modern, gallery-like */
--color-bg: #0a0a0a;  /* near-black, no undertone */
--color-bg: #111111;  /* slightly lifted black */
--color-bg: #0e0e0e;  /* charcoal void */
```

Choose temperature based on the DNA profile. Warm darks for editorial, luxury, and lifestyle. Cool darks for tech, data, and corporate. Neutral darks when the design needs to disappear behind the content.

### Surface Contrast: The 10-15% Rule

Surface must be visibly distinct from background but not dramatically so. The human eye needs just enough contrast to perceive the elevation change.

```css
/* If bg is #0a0a0a (L ~3.5% in HSL): */
--color-surface: #141414;  /* L ~7.8%, delta ~4.3% -- GOOD */
--color-surface: #181818;  /* L ~9.4%, delta ~5.9% -- GOOD */
--color-surface: #1a1a1a;  /* L ~10.2%, delta ~6.7% -- MAX for subtle */
--color-surface: #222222;  /* L ~13.3%, delta ~9.8% -- too much, card pops out */
--color-surface: #0d0d0d;  /* L ~5.1%, delta ~1.6% -- too subtle, card invisible */
```

For **hover states**, add another step:
```css
--color-surface-hover: #1e1e1e;   /* surface + 5-8% lightness */
--color-surface-active: #242424;  /* surface + 10-12% lightness */
```

For **borders**, use low-opacity white:
```css
--color-border: rgba(255, 255, 255, 0.06);  /* barely visible divider */
--color-border: rgba(255, 255, 255, 0.10);  /* visible but subtle */
--color-border: rgba(255, 255, 255, 0.15);  /* clear division */
```

### Text Should Be Warm Off-White

Pure white (#fff) on dark backgrounds creates glare. Warm off-whites are easier on the eyes and feel more intentional.

```css
/* GOOD -- warm off-whites */
--color-text: #f5f0eb;  /* cream-tinted, warm and soft */
--color-text: #ede8e3;  /* parchment white */
--color-text: #e8e4df;  /* slightly warm, very readable */
--color-text: #f0ece7;  /* subtle warmth */

/* GOOD -- cool off-whites (for tech/clinical DNA profiles) */
--color-text: #e6edf3;  /* blue-tinted off-white */
--color-text: #dde4ec;  /* steel off-white */
--color-text: #e2e8f0;  /* slate-tinted off-white */

/* GOOD -- neutral off-whites */
--color-text: #e5e5e5;  /* pure gray off-white, no tint */
--color-text: #ebebeb;  /* slightly lighter neutral */

/* BAD */
--color-text: #ffffff;  /* too harsh, causes halation */
--color-text: #f0f0f0;  /* acceptable but lacks character */
--color-text: #cccccc;  /* too dim for primary text, use for muted */
```

### Muted Text Hierarchy

Muted text must be distinct from primary text AND still legible against the background. It occupies the middle of the contrast range.

```css
/* Muted on dark backgrounds */
--color-muted: #7a7a7a;  /* neutral gray, safe */
--color-muted: #8a8078;  /* warm muted, matches warm bg */
--color-muted: #7d8590;  /* cool muted, matches cool bg */
--color-muted: #6b6b6b;  /* darker muted, more separation from text */
```

Check WCAG contrast: muted text must achieve at least 4.5:1 against the background for body-sized text, or 3:1 for text 18px+ / bold 14px+.

### Accent Desaturation for Dark Themes

Fully saturated accent colors on dark backgrounds create a neon-on-void effect that looks cheap and aggressive. Desaturate accents by 10-20% from their pure form.

```css
/* Too saturated for dark themes -- neon harshness */
--color-accent: #ff0000;  /* pure red -- NO */
--color-accent: #00ff00;  /* pure green -- NO */
--color-accent: #0088ff;  /* vivid blue -- borderline */

/* Properly desaturated -- premium feel */
--color-accent: #e85d45;  /* red pulled toward coral */
--color-accent: #3ab858;  /* green pulled toward sage */
--color-accent: #58a6ff;  /* blue pulled toward steel */
--color-accent: #a78bfa;  /* purple pulled toward lavender */
```

To desaturate: reduce the S value in HSL by 10-20 points, or blend with 10-15% gray. The accent should still be clearly colored but should not vibrate against the dark background.

---

## 5. Light Theme Rules

Light themes require different discipline than dark themes. The challenge is not darkness management but avoiding the sterile, template-like flatness that makes light sites look generic.

### Off-Whites Are Mandatory

Pure `#ffffff` as a background looks like an unstyled HTML page. Off-whites with subtle tint communicate intentional design.

```css
/* Warm off-whites -- inviting, editorial, lifestyle */
--color-bg: #faf8f5;  /* warm cream, barely perceptible */
--color-bg: #f8f5f0;  /* parchment, slightly more visible warmth */
--color-bg: #faf9f7;  /* lightest warm, very subtle */
--color-bg: #f5f0eb;  /* stronger cream, editorial warmth */

/* Cool off-whites -- tech, corporate, clean */
--color-bg: #f0f2f5;  /* cool gray-blue tint */
--color-bg: #f5f7fa;  /* icy off-white, technical precision */
--color-bg: #eef1f5;  /* slate-tinted, data-focused */
--color-bg: #f2f4f8;  /* steel off-white */

/* Neutral off-whites -- gallery, minimal, Swiss */
--color-bg: #f5f5f5;  /* pure light gray, no tint */
--color-bg: #fafafa;  /* near-white, lifted just enough */
--color-bg: #f8f8f8;  /* slightly lighter neutral */

/* BAD */
--color-bg: #ffffff;  /* unstyled, flat, generic */
--color-bg: #e0e0e0;  /* too dark for a primary bg, reads as disabled */
```

Match the off-white temperature to the overall palette. Warm palettes get warm off-whites. Cool palettes get cool off-whites. Mixing (warm text colors on cool off-white) creates subtle tension that can work for edgy or contrast-driven DNA profiles.

### Text Should Be Near-Black, Not Pure Black

```css
/* GOOD -- near-blacks */
--color-text: #1a1a1a;  /* standard near-black, reliable */
--color-text: #171717;  /* slightly darker, more authority */
--color-text: #1e1e1e;  /* slightly lighter, softer */
--color-text: #2a2420;  /* warm near-black, matches warm bg */
--color-text: #1a1e24;  /* cool near-black, matches cool bg */

/* BAD */
--color-text: #000000;  /* too harsh against off-whites */
--color-text: #333333;  /* too light for primary text, reads as muted */
```

### Saturated Accents Work on Light Backgrounds

Light backgrounds absorb saturation visually. Colors that would look neon on dark backgrounds appear balanced and rich on light backgrounds. You can push saturation 10-20% higher in light mode than in dark mode.

```css
/* Dark mode accent  -->  Light mode accent (more saturated) */
/* #e85d45           -->  #dc3520  */
/* #58a6ff           -->  #2563eb  */
/* #a78bfa           -->  #7c3aed  */
/* #3ab858           -->  #16a34a  */
```

The increased saturation compensates for the lighter surrounding context, maintaining equivalent visual weight.

### Surface Colors Must Have Tint

On light themes, surface (cards, nav, panels) should NOT be pure gray. Add the same hue tint as the background, just shifted in lightness.

```css
/* Warm light theme */
--color-bg: #faf8f5;
--color-surface: #ffffff;     /* white surface on off-white bg -- ACCEPTABLE */
--color-surface: #f5f2ed;     /* slightly darker warm surface -- BETTER */

/* Cool light theme */
--color-bg: #f0f2f5;
--color-surface: #ffffff;     /* white surface on cool bg -- ACCEPTABLE */
--color-surface: #e8ecf2;     /* slightly darker cool surface -- BETTER */
```

The surface can be lighter OR darker than bg. On light themes, white (`#ffffff`) cards on off-white backgrounds is a classic pattern that works well because the pure white reads as elevated / illuminated.

### Border Treatment on Light Themes

```css
--color-border: rgba(0, 0, 0, 0.06);   /* ghost border, barely visible */
--color-border: rgba(0, 0, 0, 0.10);   /* subtle divider */
--color-border: rgba(0, 0, 0, 0.15);   /* clear division */
```

Prefer `rgba` black with low opacity over solid gray hex values. It adapts better to tinted backgrounds.

### Muted Text on Light Themes

```css
/* Light theme muted */
--color-muted: #6b6b6b;  /* neutral gray muted */
--color-muted: #736a5e;  /* warm muted, matches warm bg */
--color-muted: #64748b;  /* cool slate muted, matches cool bg */
--color-muted: #757575;  /* slightly lighter, more secondary feel */
```

Muted text on light themes must still pass WCAG AA contrast against the background. Test every combination.

---

## 6. Dual Theme Derivation

When the design tokens specify `hasDualTheme: true`, generate both dark and light variants. This is NOT a simple color inversion. Each theme is a deliberate re-interpretation of the same aesthetic identity.

### The Derivation Principles

1. **Preserve emotional tone.** A luxurious dark palette becomes a luxurious light palette, not a clinical one.
2. **Shift lightness, preserve hue.** Background and text swap ends of the lightness spectrum. Accent hues remain the same family but adjust saturation and lightness for the new context.
3. **Adjust accent saturation.** Accents desaturate for dark (avoid neon), saturate for light (compensate for wash-out).
4. **Re-derive surface.** Surface is always relative to its theme's background, never carried over.
5. **Re-derive muted.** Muted is always the midpoint between text and background in its own theme.

### Example 1: Dark Luxe --> Warm Cream

A rich, warm dark palette transforms into a refined cream-toned light palette.

**Dark variant:**
```css
[data-theme="dark"] {
  --color-bg:       #0f0d0b;
  --color-surface:  #1a1714;
  --color-text:     #f5f0eb;
  --color-muted:    #8a8078;
  --color-accent:   #c9a96e;
  --color-accent2:  #e85d45;
  --color-border:   rgba(255, 255, 255, 0.08);
}
```

**Light variant:**
```css
[data-theme="light"] {
  --color-bg:       #faf7f2;
  --color-surface:  #ffffff;
  --color-text:     #2a2420;
  --color-muted:    #736a5e;
  --color-accent:   #a0845c;
  --color-accent2:  #c44230;
  --color-border:   rgba(0, 0, 0, 0.08);
}
```

**What changed:**
- bg flipped from warm near-black to warm cream (same hue family, opposite lightness)
- surface became white (elevated against cream)
- text became warm near-black (inherits the warmth from the dark theme's bg)
- muted darkened to maintain its middle-ground position
- accent darkened and desaturated slightly (gold -> bronze, richer against light bg)
- accent2 darkened (coral -> brick red, more weight against light)

### Example 2: Cyber Dark --> Steel Light

A tech-focused dark palette with blue undertones transforms into a clean, cool-gray light palette.

**Dark variant:**
```css
[data-theme="dark"] {
  --color-bg:       #0b0d12;
  --color-surface:  #151820;
  --color-text:     #e6edf3;
  --color-muted:    #7d8590;
  --color-accent:   #58a6ff;
  --color-accent2:  #3ab858;
  --color-border:   rgba(255, 255, 255, 0.06);
}
```

**Light variant:**
```css
[data-theme="light"] {
  --color-bg:       #f0f2f5;
  --color-surface:  #ffffff;
  --color-text:     #1a1e24;
  --color-muted:    #64748b;
  --color-accent:   #2563eb;
  --color-accent2:  #16a34a;
  --color-border:   rgba(0, 0, 0, 0.08);
}
```

**What changed:**
- bg flipped from ink-blue-black to steel-tinted off-white (same cool undertone)
- text became the cool near-black (inheriting the dark theme's blue bias)
- accent shifted from bright sky blue to deeper royal blue (more saturated, darker, avoids wash-out on light)
- accent2 shifted from medium green to vivid green (stronger presence on light)

### Example 3: Neon Brutalist --> Stark White

An aggressive, high-contrast dark palette transforms into a stark, bold light palette.

**Dark variant:**
```css
[data-theme="dark"] {
  --color-bg:       #0a0a0a;
  --color-surface:  #141414;
  --color-text:     #ebebeb;
  --color-muted:    #6b6b6b;
  --color-accent:   #ff3b3b;
  --color-accent2:  #ffe03b;
  --color-border:   rgba(255, 255, 255, 0.12);
}
```

**Light variant:**
```css
[data-theme="light"] {
  --color-bg:       #f5f5f5;
  --color-surface:  #ffffff;
  --color-text:     #0a0a0a;
  --color-muted:    #6b6b6b;
  --color-accent:   #dc2626;
  --color-accent2:  #ca8a04;
  --color-border:   rgba(0, 0, 0, 0.12);
}
```

**What changed:**
- bg flipped from neutral near-black to neutral light gray (brutalist stays neutral, no tint)
- text became the darkest possible near-black (brutalist aggression preserved)
- muted stayed nearly the same (midpoint gray works in both contexts for neutral palettes)
- accent red darkened (neon -> deep red, maintains intensity without screaming)
- accent2 yellow darkened significantly to amber/gold (yellow on white is illegible, must darken)
- border opacity stayed the same at 0.12 (brutalist likes visible structure)

### Example 4: Coastal Editorial --> Ocean Light

A blue-green editorial dark palette transforms into a breezy, coastal light palette.

**Dark variant:**
```css
[data-theme="dark"] {
  --color-bg:       #0a100f;
  --color-surface:  #131c1a;
  --color-text:     #e8f0ed;
  --color-muted:    #6d8a82;
  --color-accent:   #4ea8a6;
  --color-accent2:  #e8923a;
  --color-border:   rgba(255, 255, 255, 0.07);
}
```

**Light variant:**
```css
[data-theme="light"] {
  --color-bg:       #f4f8f7;
  --color-surface:  #ffffff;
  --color-text:     #1a2825;
  --color-muted:    #5a7a72;
  --color-accent:   #0d9488;
  --color-accent2:  #c2751e;
  --color-border:   rgba(0, 0, 0, 0.07);
}
```

**What changed:**
- bg flipped from dark teal-black to teal-tinted off-white (ocean feeling preserved)
- text became deep teal-black (the dark bg color repurposed as text)
- accent teal deepened and saturated (lighter context allows richer color)
- accent2 amber darkened to deep amber (maintains warmth against cool-tinted light bg)

---

## 7. CSS Custom Property Convention

All Web Studio palettes use these exact custom property names. Never rename or restructure them. Every component, every utility class, and every animation references these tokens.

### Core Palette Properties

```css
:root {
  /* Primary palette */
  --color-bg:              /* page background */
  --color-surface:         /* elevated surfaces (cards, nav, modals) */
  --color-text:            /* primary text */
  --color-muted:           /* secondary text, captions, metadata */
  --color-accent:          /* primary accent (CTAs, links, highlights) */
  --color-accent2:         /* secondary accent (complementary/contrast) */

  /* Functional tokens */
  --color-link:            /* link text color, often equals accent */
  --color-border:          /* dividers, card edges, separators */

  /* Interactive states */
  --color-surface-hover:   /* surface on pointer hover */
  --color-surface-active:  /* surface on click/active */
}
```

### Theme Scoping Pattern

The scoping pattern uses `data-theme` attributes for explicit control and `prefers-color-scheme` for automatic OS-level matching.

```css
/* === Dark theme (default) === */
:root {
  --color-bg: #0f0d0b;
  --color-surface: #1a1714;
  --color-text: #f5f0eb;
  --color-muted: #8a8078;
  --color-accent: #c9a96e;
  --color-accent2: #e85d45;
  --color-link: #c9a96e;
  --color-border: rgba(255, 255, 255, 0.08);
  --color-surface-hover: #221f1a;
  --color-surface-active: #2a2620;
}

/* === Light theme (explicit toggle) === */
[data-theme="light"] {
  --color-bg: #faf7f2;
  --color-surface: #ffffff;
  --color-text: #2a2420;
  --color-muted: #736a5e;
  --color-accent: #a0845c;
  --color-accent2: #c44230;
  --color-link: #a0845c;
  --color-border: rgba(0, 0, 0, 0.08);
  --color-surface-hover: #f2ede6;
  --color-surface-active: #ebe5dc;
}

/* === Light theme (OS preference, no explicit toggle) === */
@media (prefers-color-scheme: light) {
  :root:not([data-theme="dark"]) {
    --color-bg: #faf7f2;
    --color-surface: #ffffff;
    --color-text: #2a2420;
    --color-muted: #736a5e;
    --color-accent: #a0845c;
    --color-accent2: #c44230;
    --color-link: #a0845c;
    --color-border: rgba(0, 0, 0, 0.08);
    --color-surface-hover: #f2ede6;
    --color-surface-active: #ebe5dc;
  }
}
```

**Priority order:**
1. `[data-theme="dark"]` or `[data-theme="light"]` on `<html>` -- always wins
2. `@media (prefers-color-scheme: ...)` -- applies when no explicit `data-theme` is set
3. `:root` defaults -- the fallback, should be the design's default theme

### Theme Toggle Implementation

```javascript
function initThemeToggle() {
  const toggle = document.querySelector('[data-theme-toggle]');
  const root = document.documentElement;

  // Restore saved preference
  const saved = localStorage.getItem('theme');
  if (saved) {
    root.setAttribute('data-theme', saved);
  }

  toggle?.addEventListener('click', () => {
    const current = root.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    root.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
  });
}
```

### Derived Utility Properties

For components that need opacity variants or tinted versions, derive from the core tokens:

```css
:root {
  /* Accent at various opacities (useful for backgrounds, borders) */
  --color-accent-10: color-mix(in srgb, var(--color-accent) 10%, transparent);
  --color-accent-20: color-mix(in srgb, var(--color-accent) 20%, transparent);
  --color-accent-50: color-mix(in srgb, var(--color-accent) 50%, transparent);

  /* Text at various opacities */
  --color-text-50: color-mix(in srgb, var(--color-text) 50%, transparent);
  --color-text-70: color-mix(in srgb, var(--color-text) 70%, transparent);
}
```

If browser support for `color-mix()` is a concern, use explicit `rgba()` fallbacks.

---

## 8. Premium Gradient Recipes

### Mesh Gradient (Modern, No Library)
Simulates the mesh gradient tool using layered radial gradients. Works in all modern browsers.

```css
.mesh-gradient {
  background-color: var(--color-bg);
  background-image:
    radial-gradient(at 20% 30%, color-mix(in srgb, var(--color-accent) 30%, transparent) 0px, transparent 50%),
    radial-gradient(at 80% 70%, color-mix(in srgb, var(--color-accent-2) 20%, transparent) 0px, transparent 50%),
    radial-gradient(at 50% 10%, color-mix(in srgb, var(--color-text) 5%, transparent) 0px, transparent 60%),
    radial-gradient(at 10% 80%, color-mix(in srgb, var(--color-accent) 10%, transparent) 0px, transparent 40%);
}
```

Adjust the `at X% Y%` positions to move the color pools. Add more layers for more complexity. Keep opacity low (10-30%) to avoid the "cheap gradient" look.

### Animated Gradient (Breathing Background)
Use for hero sections on warm-gradient, organic-soft, and candy-playful DNA profiles.

```css
.animated-gradient {
  background: linear-gradient(-45deg,
    var(--color-bg),
    color-mix(in srgb, var(--color-accent) 15%, var(--color-bg)),
    color-mix(in srgb, var(--color-accent-2) 12%, var(--color-bg)),
    var(--color-bg)
  );
  background-size: 400% 400%;
  animation: gradient-breathe 12s ease infinite;
}

@keyframes gradient-breathe {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}
```

### Aurora (Dark Profiles — cosmic, cyber-dark, dark-luxe)
```css
.aurora-bg {
  background: var(--color-bg);
  position: relative;
  overflow: hidden;
}
.aurora-bg::before {
  content: '';
  position: absolute;
  inset: 0;
  background: conic-gradient(
    from 180deg at 50% 70%,
    var(--color-accent) 0deg,
    transparent 60deg,
    var(--color-accent-2) 180deg,
    transparent 240deg,
    var(--color-accent) 360deg
  );
  opacity: 0.12;
  filter: blur(80px);
  animation: aurora-rotate 24s linear infinite;
}
@keyframes aurora-rotate {
  to { transform: rotate(360deg); }
}
```

### Gradient Text
```css
.gradient-text {
  background: linear-gradient(
    135deg,
    var(--color-text) 0%,
    var(--color-accent) 50%,
    var(--color-accent-2) 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Animated gradient text */
.gradient-text-animated {
  background: linear-gradient(
    90deg,
    var(--color-text),
    var(--color-accent),
    var(--color-accent-2),
    var(--color-text)
  );
  background-size: 200% auto;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradient-text-flow 4s linear infinite;
}
@keyframes gradient-text-flow {
  to { background-position: 200% center; }
}
```

Note: Gradient text is accessibility-sensitive. Screen readers see the underlying text color. Ensure the fallback text color passes contrast requirements.

### Frosted Glass Surface
```css
.glass-surface {
  background: color-mix(in srgb, var(--color-bg) 50%, transparent);
  backdrop-filter: blur(20px) saturate(1.8);
  -webkit-backdrop-filter: blur(20px) saturate(1.8);
  border: 1px solid color-mix(in srgb, var(--color-text) 10%, transparent);
}
```

Glass effects require a non-flat background behind them. Always ensure the parent or body has a gradient or image — glass on flat color looks broken.

### Gradient Border (No Outline)
```css
.gradient-border {
  position: relative;
  border-radius: inherit;
}
.gradient-border::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px;
  background: linear-gradient(135deg, var(--color-accent), var(--color-accent-2));
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

### Grain Overlay (Texture Without Images)
```css
/* SVG-based noise — works everywhere, no external image */
.grain-overlay::after {
  content: '';
  position: fixed;
  inset: -50%;
  width: 200%;
  height: 200%;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  opacity: 0.04;
  pointer-events: none;
  z-index: 9999;
  animation: grain-drift 0.5s steps(1) infinite;
}
@keyframes grain-drift {
  0%  { transform: translate(0, 0); }
  25% { transform: translate(-1%, -1%); }
  50% { transform: translate(1%, 0); }
  75% { transform: translate(0, 1%); }
}
```

Grain opacity guidelines: 3-5% for subtle texture, 6-8% for visible texture (editorial/organic profiles), 10%+ for intentional film-grain look (dark-luxe, retro-future).

---

## 9. Anti-Patterns

These color decisions consistently make AI-generated sites look generic or broken. Avoid all of them.

### Anti-Pattern 1: Pure White + Generic Blue
**#ffffff background + #3b82f6 accent (Tailwind blue-500)** is the default palette of every scaffolded SaaS template. The moment this combination appears without intention, the site reads as "generated."

Fix: Even if the target aesthetic is clean-tech or corporate-sharp, choose a deliberate blue (not the Tailwind default), and add a slight tint to the background (#f8fafc, not #ffffff).

### Anti-Pattern 2: Flat Dark + Neon Green
**#000000 or #1a1a1a background + #00ff00 accent** is the first thing generated when someone asks for a "hacker aesthetic." The pure green reads as terminal cosplay, not design.

Fix: Use a more specific neon that fits the DNA profile. For cyber-dark: #00ffcc (teal) or #ff00aa (magenta). For concrete-industrial: #c8ff00 (chartreuse). Never pure #00ff00.

### Anti-Pattern 3: Gradient on Every Section
Using a different colorful gradient as the background of every content section. The eye has no place to rest and every section competes with every other section.

Fix: Gradients should appear in 1-2 locations maximum per page. The other sections use flat or subtly tinted backgrounds. The gradient sections become the accent moments.

### Anti-Pattern 4: Low-Contrast Muted Text on Muted Background
```
/* This fails WCAG AA */
color: #9ca3af;  /* gray-400 */
background: #f3f4f6;  /* gray-100 */
/* Contrast ratio: ~2.0:1 — well below the 4.5:1 requirement */
```

Fix: Muted text still needs to pass contrast. Use the contrast checker before setting muted/caption text colors. Dark mode profiles are especially prone to this failure.

### Anti-Pattern 5: Same Color for All States
Using the same accent color for hover, active, focus, and default states. No visual feedback.

Fix: Default state uses accent. Hover darkens by 10-15% lightness (oklch). Active darkens by 20-25%. Focus adds outline, not color change.

```css
.btn {
  background: var(--color-accent);                                           /* default */
}
.btn:hover {
  background: color-mix(in srgb, var(--color-accent) 85%, black);           /* darker */
}
.btn:active {
  background: color-mix(in srgb, var(--color-accent) 70%, black);           /* darkest */
}
.btn:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
}
```

### Anti-Pattern 6: Warm and Cool Fighting
Mixing warm background tones (#f5f1eb, parchment) with cool accent colors (#3b82f6, blue) without a bridge. The colors feel unrelated because they live in different temperature families.

Fix: Either stay in one temperature family, or use the complementary color strategy deliberately — if background is warm, accent should be cool AND the relationship should be the intentional design decision, not an accident.

### Anti-Pattern 7: Dark Mode = Just Invert
Implementing dark mode by naively inverting all colors. This produces neon-green text, blindingly bright borders, and inverted image colors.

Fix: Dark mode needs its own token values. The background darkens (L goes from 95 to 8). The text lightens (L goes from 10 to 92). But the accent may stay similar or shift slightly in saturation/lightness for the new background context. Images should never be CSS-inverted — use `filter: invert(1) hue-rotate(180deg)` only on icons/illustrations, never photos.
