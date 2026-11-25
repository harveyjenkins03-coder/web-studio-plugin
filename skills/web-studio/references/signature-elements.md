# Signature Elements Library

12 premium interactive elements that elevate a site from "good" to "agency-level". Each includes complete, copy-ready code. These are Phase 4 additions — applied after core layout and motion are done.

Use sparingly: 2-3 signature elements per site. More than that and they compete for attention.

---

## 1. Custom Cursor

Replace the OS cursor with a branded, animated dot. Reveals personality immediately.

```html
<div class="cursor" id="cursor"></div>
<div class="cursor-follower" id="cursor-follower"></div>

<style>
  * { cursor: none; }

  .cursor {
    position: fixed;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--color-accent);
    pointer-events: none;
    z-index: 9999;
    mix-blend-mode: difference;
    transform: translate(-50%, -50%);
    transition: width 0.2s, height 0.2s, opacity 0.2s;
  }

  .cursor-follower {
    position: fixed;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 1px solid var(--color-accent);
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: width 0.3s, height 0.3s, opacity 0.3s;
    opacity: 0.5;
  }

  /* Expanded state on hoverable elements */
  .cursor.expanded { width: 60px; height: 60px; opacity: 0.3; }
  .cursor-follower.expanded { width: 80px; height: 80px; opacity: 0.1; }
</style>

<script>
  const cursor = document.getElementById('cursor');
  const follower = document.getElementById('cursor-follower');
  let mouseX = 0, mouseY = 0;
  let followerX = 0, followerY = 0;

  document.addEventListener('mousemove', e => {
    mouseX = e.clientX;
    mouseY = e.clientY;
    gsap.to(cursor, { x: mouseX, y: mouseY, duration: 0.1, ease: 'none' });
  });

  // Follower has lag
  function updateFollower() {
    followerX += (mouseX - followerX) * 0.12;
    followerY += (mouseY - followerY) * 0.12;
    gsap.set(follower, { x: followerX, y: followerY });
    requestAnimationFrame(updateFollower);
  }
  updateFollower();

  // Expand on interactive elements
  const hoverEls = document.querySelectorAll('a, button, [data-cursor-expand]');
  hoverEls.forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.classList.add('expanded');
      follower.classList.add('expanded');
    });
    el.addEventListener('mouseleave', () => {
      cursor.classList.remove('expanded');
      follower.classList.remove('expanded');
    });
  });
</script>
```

---

## 2. Smooth Preloader

Branded loading sequence before the page reveals.

```html
<div class="preloader" id="preloader">
  <div class="preloader-bar">
    <div class="preloader-fill" id="preloader-fill"></div>
  </div>
  <div class="preloader-count" id="preloader-count">0</div>
</div>

<style>
  .preloader {
    position: fixed;
    inset: 0;
    background: var(--color-bg);
    z-index: 10000;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 24px;
  }

  .preloader-bar {
    width: 200px;
    height: 1px;
    background: var(--color-border);
    position: relative;
    overflow: hidden;
  }

  .preloader-fill {
    position: absolute;
    top: 0; left: 0; bottom: 0;
    background: var(--color-accent);
    width: 0%;
    transition: width 0.05s linear;
  }

  .preloader-count {
    font-size: clamp(40px, 6vw, 80px);
    font-family: var(--font-display);
    font-weight: 700;
    color: var(--color-fg);
    font-variant-numeric: tabular-nums;
  }
</style>

<script>
  const fill = document.getElementById('preloader-fill');
  const count = document.getElementById('preloader-count');
  const preloader = document.getElementById('preloader');

  gsap.to({ val: 0 }, {
    val: 100,
    duration: 1.8,
    ease: 'power2.inOut',
    onUpdate() {
      const v = Math.round(this.targets()[0].val);
      count.textContent = v;
      fill.style.width = v + '%';
    },
    onComplete() {
      gsap.to(preloader, {
        yPercent: -100,
        duration: 0.8,
        ease: 'power4.inOut',
        onComplete: () => {
          preloader.remove();
          document.dispatchEvent(new Event('preloader:complete'));
        },
      });
    },
  });
</script>
```

---

## 3. Magnetic Buttons

Buttons that attract toward the cursor. Feels alive.

```html
<button class="magnetic-btn" data-magnet-strength="0.4">
  <span>Get Started</span>
</button>

<style>
  .magnetic-btn {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 16px 40px;
    border: 1px solid var(--color-accent);
    background: transparent;
    color: var(--color-accent);
    font-size: 15px;
    font-weight: 500;
    letter-spacing: 0.05em;
    border-radius: 100px;
    cursor: none;
    overflow: hidden;
    transition: color 0.3s;
  }

  .magnetic-btn::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--color-accent);
    border-radius: inherit;
    transform: scaleX(0);
    transform-origin: right;
    transition: transform 0.4s cubic-bezier(0.77, 0, 0.175, 1);
  }

  .magnetic-btn:hover::before { transform: scaleX(1); transform-origin: left; }
  .magnetic-btn:hover { color: var(--color-bg); }
  .magnetic-btn span { position: relative; z-index: 1; }
</style>

<script>
  document.querySelectorAll('.magnetic-btn').forEach(btn => {
    const strength = parseFloat(btn.dataset.magnetStrength) || 0.4;

    btn.addEventListener('mousemove', e => {
      const { left, top, width, height } = btn.getBoundingClientRect();
      const x = (e.clientX - left - width / 2) * strength;
      const y = (e.clientY - top - height / 2) * strength;
      gsap.to(btn, { x, y, duration: 0.3, ease: 'power2.out' });
    });

    btn.addEventListener('mouseleave', () => {
      gsap.to(btn, { x: 0, y: 0, duration: 0.7, ease: 'elastic.out(1, 0.4)' });
    });
  });
</script>
```

---

## 4. Text Scramble Effect

Text that resolves from random characters. Instant personality.

```js
class TextScramble {
  constructor(el, options = {}) {
    this.el = el;
    this.chars = options.chars || 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%';
    this.speed = options.speed || 30; // ms per frame
  }

  scramble(newText) {
    return new Promise(resolve => {
      let frame = 0;
      let resolved = 0;
      const length = newText.length;

      const interval = setInterval(() => {
        this.el.textContent = newText.split('').map((char, i) => {
          if (char === ' ') return ' ';
          if (i < resolved) return newText[i];
          return this.chars[Math.floor(Math.random() * this.chars.length)];
        }).join('');

        if (frame % 3 === 0) resolved++;
        frame++;

        if (resolved >= length) {
          this.el.textContent = newText;
          clearInterval(interval);
          resolve();
        }
      }, this.speed);
    });
  }
}

// Usage — cycle through phrases
const el = document.querySelector('.scramble-text');
const scrambler = new TextScramble(el);
const phrases = ['Digital Studio', 'Creative Agency', 'Made with Motion'];
let current = 0;

async function cycle() {
  await scrambler.scramble(phrases[current]);
  await new Promise(r => setTimeout(r, 2500));
  current = (current + 1) % phrases.length;
  cycle();
}
cycle();
```

---

## 5. Parallax Section Backgrounds

Multi-layer parallax for depth without Three.js.

```html
<section class="parallax-section" data-parallax-section>
  <div class="parallax-bg" data-parallax-depth="0.4"></div>
  <div class="parallax-mid" data-parallax-depth="0.2"></div>
  <div class="parallax-content">
    <!-- Content here stays fixed, no parallax -->
  </div>
</section>

<script>
  function initParallax() {
    const sections = document.querySelectorAll('[data-parallax-section]');

    sections.forEach(section => {
      const layers = section.querySelectorAll('[data-parallax-depth]');

      ScrollTrigger.create({
        trigger: section,
        start: 'top bottom',
        end: 'bottom top',
        onUpdate: self => {
          layers.forEach(layer => {
            const depth = parseFloat(layer.dataset.parallaxDepth) || 0.3;
            const y = self.progress * 100 * depth * -1;
            gsap.set(layer, { yPercent: y });
          });
        },
      });
    });
  }
  initParallax();
</script>
```

---

## 6. Image Reveal on Scroll

Images that wipe in with a clip-path curtain.

```html
<div class="reveal-image-wrap" data-reveal-direction="left">
  <img src="..." class="reveal-image" alt="..." />
  <div class="reveal-curtain"></div>
</div>

<style>
  .reveal-image-wrap {
    position: relative;
    overflow: hidden;
  }
  .reveal-curtain {
    position: absolute;
    inset: 0;
    background: var(--color-surface);
    transform-origin: right;
    z-index: 1;
  }
  .reveal-image { display: block; width: 100%; }
</style>

<script>
  gsap.utils.toArray('[data-reveal-direction]').forEach(wrap => {
    const dir = wrap.dataset.revealDirection || 'left';
    const curtain = wrap.querySelector('.reveal-curtain');
    const img = wrap.querySelector('img');

    const origins = { left: 'right', right: 'left', top: 'bottom', bottom: 'top' };
    const axes = { left: 'scaleX', right: 'scaleX', top: 'scaleY', bottom: 'scaleY' };

    gsap.set(curtain, { transformOrigin: origins[dir], [axes[dir]]: 1 });
    gsap.set(img, { scale: 1.15 });

    ScrollTrigger.create({
      trigger: wrap,
      start: 'top 80%',
      onEnter: () => {
        const tl = gsap.timeline();
        tl.to(curtain, { [axes[dir]]: 0, duration: 1, ease: 'power4.inOut' })
          .to(img, { scale: 1, duration: 1.2, ease: 'power3.out' }, '-=0.8');
      },
      once: true,
    });
  });
</script>
```

---

## 7. Infinite Marquee / Ticker

Smooth CSS infinite scroll. No JavaScript needed for basic version.

```html
<div class="marquee" aria-hidden="true">
  <div class="marquee-track">
    <span>Design Studio</span>
    <span aria-hidden>·</span>
    <span>Motion First</span>
    <span aria-hidden>·</span>
    <span>Typography Bold</span>
    <span aria-hidden>·</span>
    <!-- Duplicate for seamless loop -->
    <span>Design Studio</span>
    <span aria-hidden>·</span>
    <span>Motion First</span>
    <span aria-hidden>·</span>
    <span>Typography Bold</span>
    <span aria-hidden>·</span>
  </div>
</div>

<style>
  .marquee {
    overflow: hidden;
    white-space: nowrap;
    border-top: 1px solid var(--color-border);
    border-bottom: 1px solid var(--color-border);
    padding: 16px 0;
  }

  .marquee-track {
    display: inline-flex;
    gap: 40px;
    animation: marquee-scroll 20s linear infinite;
    font-size: clamp(18px, 2vw, 28px);
    font-family: var(--font-display);
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--color-fg-muted);
  }

  @keyframes marquee-scroll {
    from { transform: translateX(0); }
    to   { transform: translateX(-50%); }
  }

  @media (prefers-reduced-motion: reduce) {
    .marquee-track { animation: none; }
  }
</style>
```

---

## 8. Scroll Progress Line

Thin accent line at top of viewport showing scroll progress.

```html
<div class="scroll-progress-line" id="scroll-progress"></div>

<style>
  .scroll-progress-line {
    position: fixed;
    top: 0; left: 0;
    height: 2px;
    width: 100%;
    background: var(--color-accent);
    transform: scaleX(0);
    transform-origin: left;
    z-index: 10000;
  }
</style>

<script>
  const line = document.getElementById('scroll-progress');
  lenis.on('scroll', ({ progress }) => {
    gsap.set(line, { scaleX: progress });
  });
</script>
```

---

## 9. Hover Image Reveal (link + image popup)

Text links that reveal an image on hover — editorial portfolio effect.

```html
<a href="#" class="hover-reveal-link" data-image="./work-1.jpg">
  Branding Project
</a>

<div class="hover-reveal-img" id="hover-image">
  <img src="" id="hover-image-src" alt="" />
</div>

<style>
  .hover-reveal-img {
    position: fixed;
    width: 300px;
    height: 200px;
    pointer-events: none;
    opacity: 0;
    z-index: 9000;
    overflow: hidden;
    border-radius: 4px;
  }
  .hover-reveal-img img { width: 100%; height: 100%; object-fit: cover; }
</style>

<script>
  const hoverImg = document.getElementById('hover-image');
  const hoverImgSrc = document.getElementById('hover-image-src');

  document.querySelectorAll('.hover-reveal-link').forEach(link => {
    link.addEventListener('mouseenter', () => {
      hoverImgSrc.src = link.dataset.image;
      gsap.to(hoverImg, { opacity: 1, scale: 1, duration: 0.4, ease: 'power3.out' });
    });

    link.addEventListener('mousemove', e => {
      gsap.to(hoverImg, {
        x: e.clientX + 20,
        y: e.clientY - 100,
        duration: 0.3,
        ease: 'power2.out',
      });
    });

    link.addEventListener('mouseleave', () => {
      gsap.to(hoverImg, { opacity: 0, scale: 0.95, duration: 0.3, ease: 'power2.in' });
    });
  });
</script>
```

---

## 10. Sticky Section Counter

Shows "01 / 05" style section number in corner as user scrolls.

```html
<div class="section-counter">
  <span class="section-current" id="section-current">01</span>
  <span class="section-sep">/</span>
  <span class="section-total" id="section-total">05</span>
</div>

<script>
  const sections = document.querySelectorAll('[data-section]');
  const current = document.getElementById('section-current');
  const total = document.getElementById('section-total');

  total.textContent = String(sections.length).padStart(2, '0');

  sections.forEach((section, i) => {
    ScrollTrigger.create({
      trigger: section,
      start: 'top center',
      end: 'bottom center',
      onEnter: () => {
        gsap.to(current, {
          textContent: String(i + 1).padStart(2, '0'),
          duration: 0.4,
          ease: 'power2.inOut',
          snap: { textContent: 1 },
        });
      },
      onEnterBack: () => {
        gsap.to(current, {
          textContent: String(i + 1).padStart(2, '0'),
          duration: 0.4,
          ease: 'power2.inOut',
        });
      },
    });
  });
</script>
```

---

## 11. Fluid Cursor Trail

SVG-based cursor trail that follows and morphs.

```html
<svg class="cursor-trail" xmlns="http://www.w3.org/2000/svg" style="position:fixed;inset:0;width:100%;height:100%;pointer-events:none;z-index:9999;">
  <defs>
    <filter id="blob-filter">
      <feGaussianBlur in="SourceGraphic" stdDeviation="6" result="blur" />
      <feColorMatrix in="blur" mode="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 20 -8" result="goo" />
    </filter>
  </defs>
  <g filter="url(#blob-filter)" id="trail-dots"></g>
</svg>

<script>
  const trailDots = document.getElementById('trail-dots');
  const trail = [];
  const TRAIL_LENGTH = 12;

  for (let i = 0; i < TRAIL_LENGTH; i++) {
    const circle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
    circle.setAttribute('r', (TRAIL_LENGTH - i) * 1.5);
    circle.setAttribute('fill', getComputedStyle(document.documentElement).getPropertyValue('--color-accent'));
    circle.setAttribute('opacity', (1 - i / TRAIL_LENGTH) * 0.5);
    trailDots.appendChild(circle);
    trail.push({ el: circle, x: 0, y: 0 });
  }

  let mouseX = 0, mouseY = 0;
  document.addEventListener('mousemove', e => { mouseX = e.clientX; mouseY = e.clientY; });

  function updateTrail() {
    trail[0].x += (mouseX - trail[0].x) * 0.3;
    trail[0].y += (mouseY - trail[0].y) * 0.3;

    for (let i = 1; i < trail.length; i++) {
      trail[i].x += (trail[i-1].x - trail[i].x) * 0.3;
      trail[i].y += (trail[i-1].y - trail[i].y) * 0.3;
      trail[i].el.setAttribute('cx', trail[i].x);
      trail[i].el.setAttribute('cy', trail[i].y);
    }
    trail[0].el.setAttribute('cx', trail[0].x);
    trail[0].el.setAttribute('cy', trail[0].y);
    requestAnimationFrame(updateTrail);
  }
  updateTrail();
</script>
```

---

## 12. Animated Section Dividers

SVG wave/diagonal dividers between sections instead of flat lines.

```html
<!-- Wave divider -->
<div class="section-divider wave">
  <svg viewBox="0 0 1440 80" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
    <path d="M0,40 C360,80 1080,0 1440,40 L1440,80 L0,80 Z" fill="var(--color-bg-2)" />
  </svg>
</div>

<!-- Diagonal divider -->
<div class="section-divider diagonal">
  <svg viewBox="0 0 1440 60" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
    <polygon points="0,60 1440,0 1440,60" fill="var(--color-surface)" />
  </svg>
</div>

<!-- Animated wave (GSAP) -->
<script>
  const wavePath = document.querySelector('.wave path');
  if (wavePath) {
    gsap.to(wavePath, {
      attr: { d: 'M0,20 C360,60 1080,10 1440,50 L1440,80 L0,80 Z' },
      duration: 4,
      ease: 'sine.inOut',
      yoyo: true,
      repeat: -1,
    });
  }
</script>

<style>
  .section-divider {
    line-height: 0;
    margin-bottom: -2px; /* Prevent subpixel gap */
  }
  .section-divider svg { width: 100%; display: block; }
</style>
```
