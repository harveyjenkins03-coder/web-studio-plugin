# DNA Profile: SVZ Kinetic

**Category:** Dark / Cinematic  
**Mood:** Motion as the medium, every scroll is a scene change, agency-level craft

---

## Emotional Target

The site IS the portfolio. Every scroll delivers a new visual experience. Motion doesn't decorate — it communicates. The user is guided through a curated journey where timing, rhythm, and typography are as deliberate as a film director's choices.

Design references: SVZ.io, Active Theory, Resn, B-Reel, Unit9, Lusion, Yann Pissenem's work

---

## Color System

```
Background:    #0a0a0a (near-pure black — the cinema screen)
Surface:       #111111
Border:        #1f1f1f
Foreground:    #f0f0f0 (near-white)
Muted:         #666666
Accent:        #ff3d00 (kinetic orange-red)
Accent 2:      #f0f0f0 (white used as accent on hover states)
```

**Accent color context:** The orange-red is used sparingly — it's the brand mark, the kinetic energy signal. It appears on hover states, active indicators, and key CTA elements only.

---

## Typography

**Display:**
- Monument Extended — weight 800 (wide, cinematic)
- Grilli Type GT Sectra — weight 300 (editorial contrast to the heavy display)
- Neue Haas Grotesk Display — weight 700

**Body:**
- Grilli Type GT Sectra — weight 400 (unexpected serif body for this aesthetic — the contrast is the point)
- Or: Neue Haas Grotesk Text — weight 300-400

**Size system:**
```
Display:   clamp(64px, 10vw, 180px)   weight 800, tracking -0.02em, line-height 0.9
H1:        clamp(40px, 6vw, 96px)     weight 700, tracking -0.02em
H2:        clamp(24px, 3vw, 44px)     weight 400
Body:      18px                        weight 400, line-height 1.75
Label:     11px                        all-caps, tracking 0.2em
```

---

## Layout Principles

- Full-viewport sections — each section = one scene
- Horizontal scroll sequences (like SVZ's case study reveals)
- Typography at the extremes: very large OR very small, never medium
- Content lives in unexpected positions (bottom-left, top-right, center)
- The grid is felt but not seen
- Aspect-ratio-locked image treatments

---

## Motion Profile — The Most Complex Profile

**This is the profile that uses every motion tool:**

- **Speed:** Variable — slow (cinematic weight) to fast (impact moments). Range: 0.3s-2.0s
- **Ease:** Multiple custom eases. Primary: `magazine` (0.77, 0, 0.175, 1)
- **Lenis lerp:** 0.08 — cinematic, weighted
- **Page load:** Mandatory preloader with branded animation (logo reveal, countdown, etc.)
- **Scroll behavior:** Every section has its own motion personality
- **Text reveal:** SplitText word-by-word reveals are standard
- **Image reveal:** Clip-path wipes from multiple directions
- **Parallax:** Active parallax on all image elements (0.3-0.5 depth)
- **Pinned sections:** At least 2-3 pinned scroll sequences per page

### Full page load sequence:
```js
const pageLoad = gsap.timeline({
  onComplete: () => {
    ScrollTrigger.refresh();
    armsScrollTriggers();
  },
});

// 1. Preloader count (0-100)
pageLoad
  .to('.preloader-count', { textContent: 100, duration: 1.8, ease: 'power2.inOut',
      snap: { textContent: 1 }, onUpdate() {
        this.targets()[0].textContent = Math.round(this.targets()[0].textContent);
      }})

// 2. Preloader exit (vertical wipe)
  .to('.preloader', { yPercent: -100, duration: 0.8, ease: 'power4.inOut' })

// 3. Nav entrance
  .from('.nav', { y: -40, opacity: 0, duration: 0.5, ease: 'power3.out' }, '-=0.2')

// 4. Hero word-by-word reveal
  .from(heroWords, { y: '120%', duration: 1, ease: 'power4.out', stagger: 0.08 }, '-=0.3')

// 5. Hero sub-elements
  .from('.hero-sub', { opacity: 0, y: 20, duration: 0.6 }, '-=0.5')
  .from('.hero-cta', { opacity: 0, y: 20, duration: 0.5 }, '-=0.4');
```

---

## Art Direction

**Primary:** Generative code art — particle systems, noise terrain, WebGL shaders  
**Secondary:** Photography with extreme CSS/Three.js treatments (RGB split, glitch, distortion)

**RGB split glitch effect:**
```css
.glitch-image {
  position: relative;
}
.glitch-image::before,
.glitch-image::after {
  content: '';
  position: absolute;
  inset: 0;
  background: inherit;
  background-size: cover;
  opacity: 0;
  transition: opacity 0.1s;
}
.glitch-image:hover::before {
  opacity: 0.6;
  transform: translate(-3px, 0);
  filter: hue-rotate(90deg);
  mix-blend-mode: multiply;
}
.glitch-image:hover::after {
  opacity: 0.6;
  transform: translate(3px, 0);
  filter: hue-rotate(-90deg);
  mix-blend-mode: screen;
}
```

**Horizontal scroll case study sequence:**
```js
const panels = gsap.utils.toArray('.case-panel');
gsap.to(panels, {
  xPercent: -100 * (panels.length - 1),
  ease: 'none',
  scrollTrigger: {
    trigger: '.cases-container',
    pin: true,
    scrub: 1,
    snap: 1 / (panels.length - 1),
    end: () => `+=${panels.length * window.innerWidth}`,
  },
});
```

---

## Signature Elements

**All of them. This profile uses every signature element:**
- Custom cursor (branded, large, kinetic)
- Preloader (count-based, animated)
- Magnetic buttons (strong, 0.5 strength)
- Text scramble on project titles
- Parallax on all images
- Horizontal scroll sequence for work/projects
- Scroll progress counter (01 / 06)
- Image hover reveal on work links

---

## Anti-Patterns

- **Never:** Template layouts
- **Never:** More than 2-3 body typefaces
- **Never:** Motion that doesn't serve a purpose
- **Never:** Anything that feels like it was generated without intention

---

## Component Recipe: The Work Section

```html
<section class="work-section">
  <div class="work-header">
    <span class="label">Selected work</span>
    <span class="work-count">06 projects</span>
  </div>

  <div class="work-list">
    <a href="#" class="work-item" data-image="/project-1.jpg">
      <div class="work-num">01</div>
      <div class="work-info">
        <h3 class="work-title">Project Name</h3>
        <span class="work-tags">Branding · Motion · Web</span>
      </div>
      <div class="work-year">2024</div>
      <div class="work-arrow">→</div>
    </a>
    <!-- repeat -->
  </div>
</section>
```

```css
.work-item {
  display: grid;
  grid-template-columns: 48px 1fr auto 40px;
  align-items: center;
  gap: 24px;
  padding: 28px 0;
  border-bottom: 1px solid var(--color-border);
  text-decoration: none;
  color: var(--color-fg);
  transition: color 0.2s;
}
.work-item:hover { color: var(--color-accent); }
.work-item:hover .work-title { letter-spacing: 0.02em; }
.work-title { transition: letter-spacing 0.4s ease; }
.work-num { font-size: 12px; color: var(--color-muted); font-variant-numeric: tabular-nums; }
.work-tags { font-size: 12px; color: var(--color-muted); }
```
