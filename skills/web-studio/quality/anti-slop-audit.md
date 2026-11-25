# Anti-Slop Audit

A quality gate that catches the 10 most common patterns that make AI-generated websites look identical and generic. Run this audit at Phase 5 before finalizing.

**How to use:** Read through each pattern, inspect the generated code, and explicitly verify each checkpoint. If any FAIL, revise before delivering.

---

## The 10 Slop Patterns

### Pattern 1: The Gradient-to-Transparent Hero

**What it looks like:** A full-width section with a radial or linear gradient from one brand color to transparent, always in the top-left or center.

**Why it's slop:** Every AI-generated site does this. It's the default when no real art direction is applied. It fills space without communicating anything.

**Audit check:**
- [ ] Hero does NOT use a generic `radial-gradient(at top left, accent, transparent)` as its only visual treatment
- [ ] Hero has at least one of: real generative art, a positioned geometric composition, editorial typography as the primary visual, or a Three.js/canvas element

**Acceptable alternatives:**
- Full-bleed typographic hero where the type IS the art
- Procedurally generated SVG or canvas background with real visual interest
- Photograph with CSS treatment (not just a gradient overlay on solid color)
- Geometric grid composition that reflects the DNA profile

---

### Pattern 2: The 3-Card Feature Section

**What it looks like:** A 3-column grid of identical cards, each with: icon on top, bold heading, 1-2 sentence description. Appears in every SaaS template.

**Why it's slop:** This layout has been used so many times it communicates "template" before the user reads a word. It's design-by-default, not design-by-choice.

**Audit check:**
- [ ] If a 3-item feature section exists, it departs from the icon-heading-text card format
- [ ] Consider: horizontal list with large numbers, asymmetric grid, alternating text/image blocks, tabbed comparison, or staggered cards with size variation

**If 3 identical cards are the right solution** (which is rare), ensure they have: unusual proportions, typographically interesting content treatment, or asymmetric visual decoration.

---

### Pattern 3: Inter / Roboto as the Display Font

**What it looks like:** Page headings set in Inter, Roboto, or any system/generic sans-serif.

**Why it's slop:** These fonts are defaults. They communicate nothing. Typography is the loudest design choice on a text-heavy page.

**Audit check:**
- [ ] Display font (h1, h2 at large sizes) is NOT from the banned list: Inter, Roboto, Arial, Helvetica (standalone), Open Sans, Lato, Montserrat, Poppins, Nunito, Source Sans
- [ ] Display font is from the Font Vault or has been explicitly chosen with rationale
- [ ] Font pairing creates deliberate contrast (e.g., serif display + geometric sans body)

---

### Pattern 4: Identical Card Hover States

**What it looks like:** `transform: translateY(-4px)` with `box-shadow` increase on hover. On every card, every button, every tile.

**Why it's slop:** This hover effect is applied without thinking by every code generator. It adds no information and communicates no personality.

**Audit check:**
- [ ] Hover states are differentiated: at least 2 different hover approaches on the page
- [ ] At minimum 1 element uses a non-lift hover: clip-path animation, color swap, text scramble, magnetic pull, reveal of hidden content, or border animation

---

### Pattern 5: The Stats Section (3 large numbers)

**What it looks like:** "500+ clients", "10M users", "99.9% uptime" — three huge numbers in a row, usually in the hero or between sections.

**Why it's slop:** Not the content itself, but the presentation. Three equally-sized numbers in a row is a template pattern, not a design decision.

**Audit check:**
- [ ] Stats section (if present) has typographic hierarchy: not all stats at the same size
- [ ] OR stats are animated with countUp
- [ ] OR stats are integrated into the layout rather than isolated in their own section
- [ ] OR stat values use tabular-nums font feature with carefully chosen typeface

---

### Pattern 6: Testimonial Carousel

**What it looks like:** A full-width slider with avatar circle, quote text, name below. Standard testimonial carousel with left/right arrows.

**Why it's slop:** This is the second most copied UI component after the feature card grid. It communicates nothing about the brand.

**Audit check:**
- [ ] Testimonials are NOT a standard center-aligned carousel
- [ ] Acceptable alternatives: masonry grid of quote cards, large pull-quote typography, scrolling ticker with shorter quotes, alternating testimonial layout, embedded video testimonials

---

### Pattern 7: The Footer CTA Section

**What it looks like:** Full-width section just above the footer: centered headline "Ready to get started?", subtext, one big button. Always the same.

**Why it's slop:** Generic closing pattern. No personality, no surprise, no design decision.

**Audit check:**
- [ ] CTA section has at minimum one differentiating element: unusual typography sizing, animation, background treatment, asymmetric layout, or unique copy presentation
- [ ] OR CTA is integrated with another section rather than isolated

---

### Pattern 8: Rounded Corners Everywhere

**What it looks like:** `border-radius: 12px` or `border-radius: 24px` applied to every card, image, and container.

**Why it's slop:** Rounding everything is the visual language of generic SaaS templates. DNA profiles like brutalist-pop, neo-swiss, concrete-industrial, editorial-serif should be sharp or have deliberate radius choices.

**Audit check:**
- [ ] Border-radius is appropriate to the DNA profile:
  - Sharp profiles (brutalist, swiss, editorial, corporate): 0px or 2-4px max
  - Soft profiles (organic, warm, candy, glass): 12-24px OK
  - Minimal profiles (apple, japanese): 6-12px, never excessive
- [ ] NOT applying `border-radius: 12px` uniformly to all elements regardless of context

---

### Pattern 9: Blue Primary + White Background

**What it looks like:** `background: #ffffff`, primary `color: #3b82f6` (Tailwind blue-500), black text. The default palette of every SaaS template.

**Why it's slop:** This palette communicates nothing. It's the color scheme that emerges when no palette decision has been made.

**Audit check:**
- [ ] Palette was generated from the DNA profile, NOT derived from Tailwind defaults
- [ ] Background is NOT pure `#ffffff` with generic blue accent (unless that's deliberately part of the DNA profile, like neo-swiss)
- [ ] Accent color can be immediately associated with the DNA profile's emotional target

---

### Pattern 10: Animation Amnesia

**What it looks like:** Page has some animations, but they're inconsistent: some elements animate on scroll, some don't. Duration, easing, and stagger vary randomly. Some sections have motion, others have none.

**Why it's slop:** Motion without a system reads as arbitrary decoration. It makes the site feel unfinished.

**Audit check:**
- [ ] All sections have a consistent motion treatment (even if some are intentionally still)
- [ ] Easing functions are consistent within a section
- [ ] Stagger direction is deliberate (not random)
- [ ] Duration increases as content becomes more important (hero = longest, CTAs = shortest)

---

## 8 Pass Criteria

All 8 must pass before delivery:

**1. Typography is distinctive**
The display font would not appear in a generic template. It has character. Someone looked it up, chose it, paired it.

**2. Color palette has a story**
Every color in the palette has a reason. Background, text, accent, accent2 — each serves a function and together they communicate the DNA profile's personality.

**3. Hero section has real art direction**
The hero is not a template. It has a visual concept that reflects the brand and DNA profile.

**4. Motion is a system, not decoration**
Animation easing, duration, and stagger are consistent and intentional. Motion reveals content hierarchy.

**5. Layout surprises at least once**
Something in the layout departs from the expected grid. An asymmetric section, an unexpected scale relationship, an unusual content presentation.

**6. At least one signature element**
Custom cursor, preloader, magnetic button, marquee, scroll progress, image reveal — one premium interactive element that signals craftsmanship.

**7. Hover states have personality**
Interactive elements respond to cursor in ways that reflect the DNA profile. Not just `translateY(-4px)`.

**8. Passes the "could this be any brand" test**
Show the design to someone without the brand name. Can they tell what industry it's for? Does it have a distinct personality? A design that "could be any brand" has failed.

---

## Font Staleness Check

Fonts that have become overused specifically in AI-generated sites (as of 2025):

| Font | Symptom | DNA profiles where it's still OK |
|------|---------|-----------------------------------|
| Inter | Used as display font | Never — body only, and only for clean-tech, corporate-sharp |
| Montserrat | Every SaaS hero | corporate-sharp only, for historical reasons |
| Outfit | Emerging cliché | Avoid entirely |
| Plus Jakarta Sans | Already saturated | Avoid entirely |
| DM Sans | Overused in AI outputs | Avoid entirely |
| Space Grotesk | Overused for "techy" | cyber-dark, retro-future only as body |
| Syne | Overused for "creative" | Only if paired with something contrasting |
| Cabinet Grotesk | Becoming a cliché | Transition to alternatives |

If any of these appear as display fonts (h1, h2, hero text), replace before delivery.
