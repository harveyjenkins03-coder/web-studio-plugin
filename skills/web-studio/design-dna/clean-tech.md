# DNA Profile: Clean Tech

**Category:** Light / Precision  
**Mood:** Modern competence, data-forward, trustworthy efficiency

---

## Emotional Target

The site communicates capability without pretension. Clean layouts, precise typography, and blue-toned accents signal intelligence and reliability. This is the aesthetic of tools built by people who care about getting it right.

Design references: Stripe, Linear, Vercel light mode, Resend, PlanetScale, Railway, Clerk

---

## Color System

```
Background:    #f8fafc (Tailwind slate-50 — slight cool tint)
Surface:       #ffffff
Border:        #e2e8f0 (Tailwind slate-200)
Foreground:    #0f172a (Tailwind slate-900)
Muted:         #64748b (Tailwind slate-500)
Accent:        #2563eb (Tailwind blue-600)
Accent 2:      #7c3aed (Tailwind violet-600)
```

---

## Typography

**Display:**
- Geist — weight 700
- Inter — weight 600-700 (acceptable here — it's native to this context)
- Cal Sans — weight 400 (Cal.com's font, clean and slightly warm)

**Body:**
- Geist — weight 400
- Inter — weight 400

**Monospace:**
- JetBrains Mono
- Geist Mono

**Size system:**
```
Display:   clamp(40px, 5.5vw, 80px)   weight 700, tracking -0.025em
H1:        clamp(28px, 3.5vw, 52px)   weight 600, tracking -0.02em
H2:        clamp(20px, 2.5vw, 36px)   weight 600
Body:      15-16px                      line-height 1.65
Code:      14px mono
```

---

## Layout Principles

- Component-level thinking: each section is a card or component
- Alternating white and slate backgrounds between sections
- Code blocks as primary visual elements (not just utility)
- Side-by-side comparisons (before/after, code/UI)
- Metrics and statistics in compact dense format

---

## Motion Profile

- **Speed:** Efficient. Durations 0.3s-0.6s.
- **Ease:** `power2.out` — responsive, purposeful
- **Lenis lerp:** 0.12 — app-quality scroll
- **Reveal:** Fade + 20px upward drift (subtle)
- **Hover:** Blue accent appears on interactive elements (0.15s)
- **Code:** Syntax highlighting appears character-by-character (typing animation)

---

## Art Direction

**Primary:** Live code examples, API payloads, terminal output as visual art  
**Secondary:** Abstract geometric backgrounds (subtle, low-contrast)

**Code block as hero:**
```html
<div class="code-hero">
  <pre class="code-block">
    <code>
<span class="token-keyword">const</span> response = <span class="token-keyword">await</span> fetch(<span class="token-string">'/api/data'</span>);
<span class="token-keyword">const</span> { users } = <span class="token-keyword">await</span> response.json();
    </code>
  </pre>
</div>
```

**Grid pattern background:**
```css
.clean-grid-bg {
  background-image:
    linear-gradient(var(--color-border) 1px, transparent 1px),
    linear-gradient(90deg, var(--color-border) 1px, transparent 1px);
  background-size: 40px 40px;
  background-color: var(--color-bg);
}
/* Fade grid at edges */
.clean-grid-bg::after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse at center, transparent 40%, var(--color-bg) 90%);
}
```

---

## Signature Elements

- **Interactive code demos:** Syntax-highlighted, copyable
- **Grid dot pattern** or line grid backgrounds
- **Status badge system:** Green/yellow/red dot indicators
- **Metric blocks:** Dense data presentation (uptime %, response time, etc.)
- **API endpoint display:** `GET /api/v1/resource` formatted display

---

## Anti-Patterns

- **Never:** Serif fonts
- **Never:** Warm colors as primary
- **Never:** Heavy borders or drop shadows
- **Never:** Complex decorative elements
- **Never:** Slow animations

---

## Component Recipes

### Feature Grid Card
```css
.clean-card {
  background: white;
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: 24px;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.clean-card:hover {
  border-color: rgba(37, 99, 235, 0.3);
  box-shadow: 0 4px 20px rgba(37, 99, 235, 0.08);
}
.clean-card-icon {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  background: rgba(37, 99, 235, 0.08);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 16px;
  color: var(--color-accent);
}
```

### API Response Display
```css
.api-display {
  background: #0f172a;
  border-radius: 12px;
  padding: 20px;
  font-family: var(--font-mono);
  font-size: 13px;
  line-height: 1.6;
  overflow-x: auto;
}
.api-key   { color: #93c5fd; }
.api-string{ color: #86efac; }
.api-number{ color: #fdba74; }
.api-bool  { color: #f87171; }
```
