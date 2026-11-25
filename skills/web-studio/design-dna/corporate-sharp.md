# DNA Profile: Corporate Sharp

**Category:** Light / Professional  
**Mood:** Authority and trust, enterprise-grade, serious money

---

## Emotional Target

The site communicates maturity, reliability, and importance. It's the digital equivalent of a tailored suit. Nothing is casual. Everything signals that this organization has been trusted with serious responsibilities.

Design references: McKinsey digital, Boston Consulting Group, JP Morgan brand, Deloitte Digital (well-executed), Palantir, Bloomberg Terminal's consumer cousin

---

## Color System

```
Background:    #ffffff (pure white — authority requires no warmth)
Surface:       #f8f9fa
Border:        #dee2e6
Foreground:    #212529 (Bootstrap's near-black — tested at scale)
Muted:         #6c757d
Accent:        #1d4ed8 (deep authoritative blue)
Accent 2:      #1e3a5f (navy — darker authority)
```

**Dark version for marketing sections:**
```
Background:    #0f172a (dark navy)
Surface:       #1e293b
Border:        #334155
Foreground:    #f1f5f9
Accent:        #3b82f6 (brighter blue on dark)
```

---

## Typography

**Display:**
- Neue Haas Grotesk Display — weight 700 (serious, Swiss precision)
- Graphik — weight 600-700
- Libre Baskerville — weight 700 (if serif authority is needed)

**Body:**
- Neue Haas Grotesk Text — weight 400
- Inter — weight 400 (acceptable — it reads as professional here)

**Size system:**
```
Display:   clamp(40px, 5vw, 80px)    weight 700, tracking -0.015em
H1:        clamp(28px, 3.5vw, 52px)  weight 700, tracking -0.01em
H2:        clamp(20px, 2.5vw, 36px)  weight 600
Body:      16px                        line-height 1.6
Caption:   13px                        muted
```

---

## Layout Principles

- Structured, predictable grid (no surprises)
- Navigation with all primary links visible (no hidden menus)
- Dense content sections (enterprise buyers want information)
- Data tables, logos, client lists as trust signals
- Case studies with quantified outcomes
- Footer with every possible link

---

## Motion Profile

- **Speed:** Restrained. Durations 0.4s-0.7s. Nothing flashy.
- **Ease:** `power2.out` — efficient, no drama
- **Lenis lerp:** 0.12 — responsive and professional
- **Reveal:** Gentle fade + 20px upward drift (barely noticeable)
- **Hover:** Blue accent appears, no transforms (professional elements don't jump)
- **No:** Parallax, rotation, playful effects

---

## Art Direction

**Primary:** Smart photo sourcing — diverse teams, board rooms, professional environments  
**Secondary:** Abstract geometric art (conservative — circles, lines, structured patterns)

**Photo style:** Authentic professional environments. Diverse teams. Real product/service in use. No stock-photo body language.

**CSS treatment:**
```css
.corporate-image {
  filter: contrast(1.05) brightness(1.02);
  /* No heavy treatment — let photos be professional */
}
```

**Data visualization as art:**
Charts, graphs, and metrics presented visually as section heroes.

---

## Signature Elements

- **Client logos:** Prominently displayed, good typographic presentation
- **Stats with context:** Not just "500%" but "500% increase in deployment speed"
- **Trust badges:** ISO, SOC 2, certifications displayed prominently
- **Quote attribution:** Full name, title, company — no anonymous testimonials
- **CTA specificity:** "Book a demo with our enterprise team" not "Get started"

---

## Anti-Patterns

- **Never:** Casual or playful typography
- **Never:** Warm or vibrant colors
- **Never:** Decorative elements without informational purpose
- **Never:** Animations that could be perceived as immature
- **Never:** Single-word CTAs ("Go!") — be specific

---

## Component Recipes

### Enterprise CTA Section
```css
.enterprise-cta {
  background: var(--color-accent);
  padding: 80px 0;
  text-align: center;
}
.enterprise-cta h2 {
  font-size: clamp(28px, 3.5vw, 48px);
  color: white;
  font-weight: 700;
  margin-bottom: 16px;
}
.enterprise-cta p {
  color: rgba(255,255,255,0.8);
  font-size: 18px;
  margin-bottom: 40px;
  max-width: 600px;
  margin-inline: auto;
}
.enterprise-cta-btn {
  padding: 14px 36px;
  background: white;
  color: var(--color-accent);
  border: none;
  border-radius: 6px;
  font-weight: 600;
  font-size: 16px;
}
```

### Testimonial (Corporate Style)
```html
<blockquote class="corporate-quote">
  <p>"Specific, measurable outcome. Numbers, timeline, result."</p>
  <footer>
    <strong>Sarah Chen</strong>
    <span>VP of Engineering, Fortune 500 Company</span>
  </footer>
</blockquote>
```

```css
.corporate-quote {
  border-left: 4px solid var(--color-accent);
  padding: 24px 32px;
  background: var(--color-surface);
  border-radius: 0 8px 8px 0;
}
.corporate-quote p {
  font-size: 20px;
  font-style: italic;
  line-height: 1.6;
  color: var(--color-fg);
  margin-bottom: 16px;
}
.corporate-quote footer strong {
  display: block;
  font-size: 15px;
  font-weight: 600;
}
.corporate-quote footer span {
  font-size: 13px;
  color: var(--color-muted);
}
```
