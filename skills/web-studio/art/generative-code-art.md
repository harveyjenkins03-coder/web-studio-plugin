# Generative Code Art

Production-ready recipes for code-generated visual art. Each recipe injects design token colors, pairs with specific DNA profiles, notes its performance cost, and describes Phase 4 animation integration.

**Token injection convention** used throughout: all recipes read CSS custom properties set from `design-tokens.json`:

```css
:root {
  --color-bg: #0a0a0a;
  --color-surface: #141414;
  --color-text: #f0f0f0;
  --color-muted: #888888;
  --color-accent: #ff5722;
  --color-accent2: #00bcd4;
}
```

---

## A. SVG Generative Patterns

### A1. Noise-Based Circle Grid

Randomized but harmonious grid of circles whose radii vary by a simple seeded noise function.

**DNA pairing**: neo-swiss, corporate-clean, clean-tech, japanese-minimal
**Performance**: Light --- static SVG, no runtime computation after initial render
**Phase 4 animation**: Stagger circle scale-in with `gsap.from` on each `<circle>`, delay by grid index.

```html
<div id="circle-grid-container"></div>

<script>
(function () {
  const COLS = 16;
  const ROWS = 10;
  const CELL = 48;
  const W = COLS * CELL;
  const H = ROWS * CELL;

  function noise(x, y, seed) {
    const n = Math.sin(x * 12.9898 + y * 78.233 + seed) * 43758.5453;
    return n - Math.floor(n);
  }

  const style = getComputedStyle(document.documentElement);
  const accent  = style.getPropertyValue('--color-accent').trim()  || '#ff5722';
  const accent2 = style.getPropertyValue('--color-accent2').trim() || '#00bcd4';
  const muted   = style.getPropertyValue('--color-muted').trim()   || '#888';

  const ns = 'http://www.w3.org/2000/svg';
  const svg = document.createElementNS(ns, 'svg');
  svg.setAttribute('viewBox', `0 0 ${W} ${H}`);
  svg.setAttribute('width', '100%');
  svg.setAttribute('height', '100%');
  svg.style.display = 'block';

  const seed = 42;
  for (let row = 0; row < ROWS; row++) {
    for (let col = 0; col < COLS; col++) {
      const n = noise(col, row, seed);
      const r = 2 + n * (CELL * 0.4);
      const cx = col * CELL + CELL / 2;
      const cy = row * CELL + CELL / 2;
      const circle = document.createElementNS(ns, 'circle');
      circle.setAttribute('cx', cx);
      circle.setAttribute('cy', cy);
      circle.setAttribute('r', r);
      const color = n > 0.85 ? accent : n > 0.7 ? accent2 : muted;
      circle.setAttribute('fill', color);
      circle.setAttribute('opacity', 0.15 + n * 0.65);
      svg.appendChild(circle);
    }
  }

  document.getElementById('circle-grid-container').appendChild(svg);
})();
</script>
```

---

### A2. Connected Dots / Constellation

Random points connected by lines when within a threshold distance.

**DNA pairing**: cyber-dark, clean-tech, editorial-dark, brutalist
**Performance**: Medium --- N^2 distance checks (keep points under 120)
**Phase 4 animation**: Animate positions with `gsap.to` on a tick loop, or parallax on `mousemove`.

```html
<div id="constellation-container" style="position:relative;width:100%;height:480px;overflow:hidden;"></div>

<script>
(function () {
  const container = document.getElementById('constellation-container');
  const W = container.offsetWidth;
  const H = container.offsetHeight;
  const NUM_POINTS = 80;
  const MAX_DIST = 120;

  const style = getComputedStyle(document.documentElement);
  const accent  = style.getPropertyValue('--color-accent').trim()  || '#ff5722';
  const accent2 = style.getPropertyValue('--color-accent2').trim() || '#00bcd4';
  const muted   = style.getPropertyValue('--color-muted').trim()   || '#888';

  const ns = 'http://www.w3.org/2000/svg';
  const svg = document.createElementNS(ns, 'svg');
  svg.setAttribute('viewBox', `0 0 ${W} ${H}`);
  svg.setAttribute('width', '100%');
  svg.setAttribute('height', '100%');
  svg.style.position = 'absolute';
  svg.style.inset = '0';

  let s = 7;
  function srand() { s = (s * 16807) % 2147483647; return (s - 1) / 2147483646; }

  const pts = [];
  for (let i = 0; i < NUM_POINTS; i++) {
    pts.push({ x: srand() * W, y: srand() * H });
  }

  for (let i = 0; i < pts.length; i++) {
    for (let j = i + 1; j < pts.length; j++) {
      const dx = pts[i].x - pts[j].x;
      const dy = pts[i].y - pts[j].y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < MAX_DIST) {
        const line = document.createElementNS(ns, 'line');
        line.setAttribute('x1', pts[i].x);
        line.setAttribute('y1', pts[i].y);
        line.setAttribute('x2', pts[j].x);
        line.setAttribute('y2', pts[j].y);
        line.setAttribute('stroke', muted);
        line.setAttribute('stroke-width', '0.5');
        line.setAttribute('opacity', 1 - dist / MAX_DIST);
        svg.appendChild(line);
      }
    }
  }

  pts.forEach((p, i) => {
    const circle = document.createElementNS(ns, 'circle');
    circle.setAttribute('cx', p.x);
    circle.setAttribute('cy', p.y);
    circle.setAttribute('r', 2 + srand() * 2);
    circle.setAttribute('fill', i % 7 === 0 ? accent : i % 11 === 0 ? accent2 : muted);
    svg.appendChild(circle);
  });

  container.appendChild(svg);
})();
</script>
```

---

### A3. Concentric Rings with Rotation Offset

Hypnotic rings, each slightly rotated via dashed strokes.

**DNA pairing**: art-deco, retro-future, editorial-serif, japanese-minimal
**Performance**: Light --- static SVG paths
**Phase 4 animation**: Animate `stroke-dashoffset` with CSS keyframes for slow spin, or use GSAP `rotation` per ring for staggered orbits.

```html
<svg id="concentric-rings" viewBox="0 0 400 400" width="400" height="400"
     style="display:block;margin:auto;">
</svg>

<script>
(function () {
  const svg = document.getElementById('concentric-rings');
  const ns = 'http://www.w3.org/2000/svg';
  const cx = 200, cy = 200;
  const RINGS = 14;

  const style = getComputedStyle(document.documentElement);
  const accent  = style.getPropertyValue('--color-accent').trim()  || '#ff5722';
  const accent2 = style.getPropertyValue('--color-accent2').trim() || '#00bcd4';
  const muted   = style.getPropertyValue('--color-muted').trim()   || '#888';

  for (let i = 1; i <= RINGS; i++) {
    const r = i * 13;
    const circle = document.createElementNS(ns, 'circle');
    circle.setAttribute('cx', cx);
    circle.setAttribute('cy', cy);
    circle.setAttribute('r', r);
    circle.setAttribute('fill', 'none');
    const color = i % 5 === 0 ? accent : i % 3 === 0 ? accent2 : muted;
    circle.setAttribute('stroke', color);
    circle.setAttribute('stroke-width', '1');
    const circumference = 2 * Math.PI * r;
    const dashLen = circumference / (4 + i);
    circle.setAttribute('stroke-dasharray', `${dashLen} ${dashLen * 0.6}`);
    circle.setAttribute('stroke-dashoffset', i * 15);
    circle.setAttribute('opacity', 0.3 + (i / RINGS) * 0.5);
    circle.setAttribute('transform', `rotate(${i * 12}, ${cx}, ${cy})`);
    svg.appendChild(circle);
  }
})();
</script>

<style>
  #concentric-rings circle {
    animation: ring-drift 20s linear infinite;
  }
  #concentric-rings circle:nth-child(even) {
    animation-direction: reverse;
    animation-duration: 30s;
  }
  @keyframes ring-drift {
    to { stroke-dashoffset: 1000; }
  }
</style>
```

---

### A4. Flow Field Visualization

Directional lines following noise-based vectors. Creates an organic, wind-like pattern.

**DNA pairing**: organic-soft, japanese-minimal, editorial-serif, coastal-minimal
**Performance**: Medium --- many path segments; keep grid resolution moderate (step 16-20px)
**Phase 4 animation**: Animate `stroke-dashoffset` for drawing-on effect, or slowly shift the noise seed over time with `requestAnimationFrame`.

```html
<canvas id="flow-field" width="960" height="540" style="width:100%;display:block;"></canvas>

<script>
(function () {
  const canvas = document.getElementById('flow-field');
  const ctx = canvas.getContext('2d');
  const W = canvas.width;
  const H = canvas.height;
  const STEP = 18;
  const LINE_LEN = 28;

  const style = getComputedStyle(document.documentElement);
  const accent = style.getPropertyValue('--color-accent').trim() || '#ff5722';
  const muted  = style.getPropertyValue('--color-muted').trim()  || '#888';
  const bg     = style.getPropertyValue('--color-bg').trim()     || '#0a0a0a';

  ctx.fillStyle = bg;
  ctx.fillRect(0, 0, W, H);

  function noise2d(x, y) {
    return (Math.sin(x * 0.03 + y * 0.02) + Math.sin(y * 0.05 - x * 0.01)) * 0.5;
  }

  for (let y = 0; y < H; y += STEP) {
    for (let x = 0; x < W; x += STEP) {
      const angle = noise2d(x, y) * Math.PI * 2;
      const ex = x + Math.cos(angle) * LINE_LEN;
      const ey = y + Math.sin(angle) * LINE_LEN;
      ctx.beginPath();
      ctx.moveTo(x, y);
      ctx.lineTo(ex, ey);
      const t = (Math.sin(x * 0.01) + 1) / 2;
      ctx.strokeStyle = t > 0.85 ? accent : muted;
      ctx.globalAlpha = 0.25 + t * 0.35;
      ctx.lineWidth = 1;
      ctx.stroke();
    }
  }
  ctx.globalAlpha = 1;
})();
</script>
```

---

## B. Canvas / WebGL Art

### B1. Gradient Mesh Background

Multiple layered radial gradients with slow positional shifts. Rich, deep background.

**DNA pairing**: cyber-dark, editorial-dark, art-deco, candy (with saturated colors)
**Performance**: Medium --- canvas redraw on animation frame; use `will-change: transform` on container
**Phase 4 animation**: Slowly move gradient centers with `requestAnimationFrame` and sine oscillation.

```html
<canvas id="gradient-mesh" style="position:fixed;inset:0;width:100%;height:100%;z-index:-1;"></canvas>

<script>
(function () {
  const canvas = document.getElementById('gradient-mesh');
  const ctx = canvas.getContext('2d');
  let W, H;

  function resize() {
    W = canvas.width = window.innerWidth;
    H = canvas.height = window.innerHeight;
  }
  resize();
  window.addEventListener('resize', resize);

  const style = getComputedStyle(document.documentElement);
  const bg      = style.getPropertyValue('--color-bg').trim()      || '#0a0a0a';
  const accent  = style.getPropertyValue('--color-accent').trim()  || '#ff5722';
  const accent2 = style.getPropertyValue('--color-accent2').trim() || '#00bcd4';
  const surface = style.getPropertyValue('--color-surface').trim() || '#141414';

  function hexToRgba(hex, alpha) {
    const r = parseInt(hex.slice(1, 3), 16);
    const g = parseInt(hex.slice(3, 5), 16);
    const b = parseInt(hex.slice(5, 7), 16);
    return `rgba(${r},${g},${b},${alpha})`;
  }

  const blobs = [
    { cx: 0.3, cy: 0.3, r: 0.5, color: accent,  speed: 0.0003, phase: 0 },
    { cx: 0.7, cy: 0.6, r: 0.4, color: accent2, speed: 0.0005, phase: 2 },
    { cx: 0.5, cy: 0.8, r: 0.6, color: surface, speed: 0.0002, phase: 4 },
  ];

  function draw(t) {
    ctx.fillStyle = bg;
    ctx.fillRect(0, 0, W, H);

    blobs.forEach(b => {
      const x = (b.cx + Math.sin(t * b.speed + b.phase) * 0.15) * W;
      const y = (b.cy + Math.cos(t * b.speed + b.phase) * 0.1) * H;
      const radius = b.r * Math.max(W, H);
      const grad = ctx.createRadialGradient(x, y, 0, x, y, radius);
      grad.addColorStop(0, hexToRgba(b.color, 0.35));
      grad.addColorStop(1, hexToRgba(b.color, 0));
      ctx.fillStyle = grad;
      ctx.fillRect(0, 0, W, H);
    });

    requestAnimationFrame(draw);
  }
  requestAnimationFrame(draw);
})();
</script>
```

---

### B2. Particle Field with Attraction / Repulsion

Physics-based particles that attract toward a point and repel from the mouse cursor.

**DNA pairing**: cyber-dark, clean-tech, retro-future, brutalist
**Performance**: Heavy --- runs every frame; cap particles at 200 and use `will-change: transform`
**Phase 4 animation**: Already animated; tie attraction point to scroll position for scroll-reactive behavior.

```html
<canvas id="particle-field" style="width:100%;height:480px;display:block;"></canvas>

<script>
(function () {
  const canvas = document.getElementById('particle-field');
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth;
  canvas.height = canvas.offsetHeight;
  const W = canvas.width;
  const H = canvas.height;
  const NUM = 150;

  const style = getComputedStyle(document.documentElement);
  const accent  = style.getPropertyValue('--color-accent').trim()  || '#ff5722';
  const accent2 = style.getPropertyValue('--color-accent2').trim() || '#00bcd4';
  const muted   = style.getPropertyValue('--color-muted').trim()   || '#888';
  const bg      = style.getPropertyValue('--color-bg').trim()      || '#0a0a0a';

  let mouse = { x: W / 2, y: H / 2 };
  canvas.addEventListener('mousemove', e => {
    const rect = canvas.getBoundingClientRect();
    mouse.x = e.clientX - rect.left;
    mouse.y = e.clientY - rect.top;
  });

  const particles = [];
  for (let i = 0; i < NUM; i++) {
    particles.push({
      x: Math.random() * W, y: Math.random() * H,
      vx: (Math.random() - 0.5) * 0.5, vy: (Math.random() - 0.5) * 0.5,
      r: 1 + Math.random() * 2,
      color: i % 6 === 0 ? accent : i % 9 === 0 ? accent2 : muted,
    });
  }

  const ATTRACT = { x: W / 2, y: H / 2 };
  const FRICTION = 0.98;

  function tick() {
    ctx.fillStyle = bg;
    ctx.fillRect(0, 0, W, H);
    particles.forEach(p => {
      p.vx += (ATTRACT.x - p.x) * 0.00005;
      p.vy += (ATTRACT.y - p.y) * 0.00005;
      const dxM = p.x - mouse.x, dyM = p.y - mouse.y;
      const distM = Math.sqrt(dxM * dxM + dyM * dyM);
      if (distM < 120 && distM > 0) {
        const force = (120 - distM) / 120 * 0.8;
        p.vx += (dxM / distM) * force;
        p.vy += (dyM / distM) * force;
      }
      p.vx *= FRICTION; p.vy *= FRICTION;
      p.x += p.vx; p.y += p.vy;
      if (p.x < 0) p.x = W; if (p.x > W) p.x = 0;
      if (p.y < 0) p.y = H; if (p.y > H) p.y = 0;
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fillStyle = p.color;
      ctx.globalAlpha = 0.6;
      ctx.fill();
    });
    ctx.globalAlpha = 1;
    requestAnimationFrame(tick);
  }
  requestAnimationFrame(tick);
})();
</script>
```

---

### B3. Noise Texture Generator

Generates a grain/texture overlay image on canvas, exported as a CSS background.

**DNA pairing**: ALL profiles benefit from grain. Especially: editorial-serif, organic-soft, brutalist, art-deco, japanese-minimal
**Performance**: Light --- renders once, then used as static background-image
**Phase 4 animation**: Optionally refresh grain every 100ms for film-grain flicker.

```html
<canvas id="noise-texture" width="256" height="256" style="display:none;"></canvas>

<script>
(function () {
  const canvas = document.getElementById('noise-texture');
  const ctx = canvas.getContext('2d');
  const W = canvas.width, H = canvas.height;
  const imageData = ctx.createImageData(W, H);
  const data = imageData.data;

  for (let i = 0; i < data.length; i += 4) {
    const v = Math.random() * 255;
    data[i] = data[i + 1] = data[i + 2] = v;
    data[i + 3] = 18;
  }
  ctx.putImageData(imageData, 0, 0);

  const dataUrl = canvas.toDataURL('image/png');
  const overlay = document.createElement('div');
  overlay.style.cssText =
    'position:fixed;inset:0;z-index:9999;pointer-events:none;' +
    'background-image:url(' + dataUrl + ');background-repeat:repeat;' +
    'opacity:0.4;mix-blend-mode:overlay;';
  document.body.appendChild(overlay);
})();
</script>
```

**Flickering film grain for Phase 4:**

```js
function refreshGrain(canvas) {
  const ctx = canvas.getContext('2d');
  const W = canvas.width, H = canvas.height;
  const imageData = ctx.createImageData(W, H);
  const data = imageData.data;
  for (let i = 0; i < data.length; i += 4) {
    const v = Math.random() * 255;
    data[i] = data[i + 1] = data[i + 2] = v;
    data[i + 3] = 18;
  }
  ctx.putImageData(imageData, 0, 0);
  return canvas.toDataURL('image/png');
}
// setInterval(() => { overlay.style.backgroundImage = 'url(' + refreshGrain(canvas) + ')'; }, 120);
```

---

### B4. Animated Aurora Wave

Sine-based undulating color bands that drift horizontally, creating an aurora / northern-lights feel.

**DNA pairing**: organic-soft, coastal-minimal, candy, editorial-dark
**Performance**: Medium --- canvas redraws every frame; keep band count under 8
**Phase 4 animation**: Already animated; tie wave amplitude to scroll progress for reactive intensity.

```html
<canvas id="aurora-wave" style="width:100%;height:320px;display:block;"></canvas>

<script>
(function () {
  const canvas = document.getElementById('aurora-wave');
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth * window.devicePixelRatio;
  canvas.height = canvas.offsetHeight * window.devicePixelRatio;
  ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
  const W = canvas.offsetWidth;
  const H = canvas.offsetHeight;

  const style = getComputedStyle(document.documentElement);
  const bg      = style.getPropertyValue('--color-bg').trim()      || '#0a0a0a';
  const accent  = style.getPropertyValue('--color-accent').trim()  || '#ff5722';
  const accent2 = style.getPropertyValue('--color-accent2').trim() || '#00bcd4';

  function hexToRgb(hex) {
    return [parseInt(hex.slice(1, 3), 16), parseInt(hex.slice(3, 5), 16), parseInt(hex.slice(5, 7), 16)];
  }

  const bands = [
    { color: hexToRgb(accent),  amp: 40, freq: 0.008, speed: 0.0008, yBase: H * 0.35 },
    { color: hexToRgb(accent2), amp: 30, freq: 0.012, speed: 0.0012, yBase: H * 0.50 },
    { color: hexToRgb(accent),  amp: 50, freq: 0.006, speed: 0.0006, yBase: H * 0.65 },
    { color: hexToRgb(accent2), amp: 25, freq: 0.015, speed: 0.0015, yBase: H * 0.45 },
  ];

  function draw(t) {
    ctx.fillStyle = bg;
    ctx.fillRect(0, 0, W, H);

    bands.forEach(b => {
      ctx.beginPath();
      ctx.moveTo(0, H);
      for (let x = 0; x <= W; x += 2) {
        const y = b.yBase + Math.sin(x * b.freq + t * b.speed) * b.amp
                          + Math.sin(x * b.freq * 0.5 + t * b.speed * 1.3) * b.amp * 0.4;
        ctx.lineTo(x, y);
      }
      ctx.lineTo(W, H);
      ctx.closePath();
      const grad = ctx.createLinearGradient(0, b.yBase - b.amp, 0, H);
      grad.addColorStop(0, 'rgba(' + b.color.join(',') + ',0.25)');
      grad.addColorStop(1, 'rgba(' + b.color.join(',') + ',0)');
      ctx.fillStyle = grad;
      ctx.fill();
    });

    requestAnimationFrame(draw);
  }
  requestAnimationFrame(draw);
})();
</script>
```

---

## C. CSS Generative Art

### C1. Layered Conic-Gradient Mesh

Multiple conic-gradient layers blended together for a rich, deep abstract background.

**DNA pairing**: art-deco, candy, retro-future, editorial-dark
**Performance**: Light --- pure CSS, hardware-composited
**Phase 4 animation**: Animate `background-position` or wrap in pseudo-element and rotate slowly.

```css
.gradient-mesh-bg {
  background:
    conic-gradient(from 45deg  at 30% 40%, var(--color-accent) 0%, transparent 25%),
    conic-gradient(from 180deg at 70% 60%, var(--color-accent2) 0%, transparent 20%),
    conic-gradient(from 270deg at 50% 80%, var(--color-muted) 0%, transparent 30%),
    var(--color-bg);
  background-blend-mode: screen, overlay, multiply;
}
```

**Full variant with blur and size control:**

```css
.gradient-mesh-bg-full {
  position: relative;
  background-color: var(--color-bg);
  overflow: hidden;
}
.gradient-mesh-bg-full::before {
  content: '';
  position: absolute;
  inset: -20%;
  background:
    conic-gradient(from 0deg   at 25% 35%, var(--color-accent)  0deg, transparent 90deg),
    conic-gradient(from 120deg at 75% 55%, var(--color-accent2) 0deg, transparent 90deg),
    conic-gradient(from 240deg at 50% 75%, var(--color-surface) 0deg, transparent 90deg);
  filter: blur(80px);
  opacity: 0.5;
}
```

---

### C2. Animated Gradient Shift

Smooth keyframe-based background color animation.

**DNA pairing**: candy, retro-future, organic-soft, coastal-minimal
**Performance**: Light --- CSS animation on `background-position`, GPU-composited
**Phase 4 animation**: Already animated; tie `animation-play-state` to viewport visibility via IntersectionObserver.

```css
.animated-gradient {
  background: linear-gradient(
    -45deg,
    var(--color-bg),
    var(--color-surface),
    var(--color-accent),
    var(--color-accent2)
  );
  background-size: 400% 400%;
  animation: gradient-shift 12s ease infinite;
}

@keyframes gradient-shift {
  0%   { background-position: 0% 50%; }
  25%  { background-position: 100% 0%; }
  50%  { background-position: 100% 100%; }
  75%  { background-position: 0% 100%; }
  100% { background-position: 0% 50%; }
}
```

**Scoped variant --- only animate when in view:**

```js
const el = document.querySelector('.animated-gradient');
const observer = new IntersectionObserver(([entry]) => {
  el.style.animationPlayState = entry.isIntersecting ? 'running' : 'paused';
}, { threshold: 0.1 });
observer.observe(el);
```

---

### C3. Grain Overlay

Subtle film grain using CSS pseudo-element with SVG filter or repeating gradient noise.

**DNA pairing**: ALL profiles --- grain adds analog warmth universally. Essential for: editorial-serif, organic-soft, brutalist, japanese-minimal
**Performance**: Light --- single pseudo-element, no JS
**Phase 4 animation**: Add `translate3d` animation to grain layer for film-flicker effect.

**Approach A --- SVG feTurbulence filter (best quality):**

```css
.grain-overlay {
  position: relative;
}
.grain-overlay::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0.35;
  mix-blend-mode: overlay;
  filter: url(#grain-filter);
  z-index: 10;
}
```

```html
<svg width="0" height="0" style="position:absolute;">
  <filter id="grain-filter">
    <feTurbulence type="fractalNoise" baseFrequency="0.75" numOctaves="4" stitchTiles="stitch" />
    <feColorMatrix type="saturate" values="0" />
  </filter>
</svg>
```

**Approach B --- CSS-only repeating gradient noise (no SVG needed):**

```css
.grain-overlay-css::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 10;
  background-image:
    repeating-linear-gradient(0deg,   transparent 0 2px, rgba(128,128,128,0.03) 2px 3px),
    repeating-linear-gradient(90deg,  transparent 0 2px, rgba(128,128,128,0.03) 2px 3px),
    repeating-linear-gradient(45deg,  transparent 0 3px, rgba(128,128,128,0.02) 3px 4px),
    repeating-linear-gradient(135deg, transparent 0 4px, rgba(128,128,128,0.02) 4px 5px);
  mix-blend-mode: overlay;
  opacity: 0.5;
}
```

**Phase 4 flicker animation:**

```css
@keyframes grain-flicker {
  0%, 100% { transform: translate3d(0, 0, 0); }
  25%      { transform: translate3d(-1px, 1px, 0); }
  50%      { transform: translate3d(1px, -1px, 0); }
  75%      { transform: translate3d(-1px, -1px, 0); }
}
.grain-overlay::after {
  animation: grain-flicker 0.3s steps(4) infinite;
}
```

---

### C4. Dot Grid Pattern

Repeating dot grid background using `radial-gradient` on `background-image`.

**DNA pairing**: neo-swiss, corporate-clean, clean-tech, japanese-minimal
**Performance**: Light --- pure CSS, no JS
**Phase 4 animation**: Animate `background-position` for slow drift, or fade in with `opacity` on scroll.

```css
.dot-grid {
  background-color: var(--color-bg);
  background-image: radial-gradient(var(--color-muted) 1px, transparent 1px);
  background-size: 24px 24px;
}
```

**Variant: accent-highlighted dot grid with two layers:**

```css
.dot-grid-accent {
  background-color: var(--color-bg);
  background-image:
    radial-gradient(var(--color-muted) 0.8px, transparent 0.8px),
    radial-gradient(var(--color-accent) 0.8px, transparent 0.8px);
  background-size: 24px 24px, 96px 96px;
  background-position: 0 0, 12px 12px;
}
```

**Variant: cross-dot pattern:**

```css
.cross-dot-grid {
  background-color: var(--color-bg);
  background-image:
    radial-gradient(var(--color-muted) 1px, transparent 1px),
    linear-gradient(var(--color-surface) 1px, transparent 1px),
    linear-gradient(90deg, var(--color-surface) 1px, transparent 1px);
  background-size: 24px 24px, 24px 24px, 24px 24px;
}
```

**Slow drift animation for Phase 4:**

```css
.dot-grid-animated {
  animation: dot-drift 60s linear infinite;
}
@keyframes dot-drift {
  to { background-position: 24px 24px; }
}
```

---

## Usage Reference

| Recipe | Category | Performance | Best DNA Profiles |
|--------|----------|-------------|-------------------|
| A1 Circle Grid | SVG | Light | neo-swiss, corporate-clean, clean-tech |
| A2 Constellation | SVG | Medium | cyber-dark, clean-tech, brutalist |
| A3 Concentric Rings | SVG | Light | art-deco, retro-future, japanese-minimal |
| A4 Flow Field | Canvas | Medium | organic-soft, japanese-minimal, editorial |
| B1 Gradient Mesh | Canvas | Medium | cyber-dark, art-deco, candy |
| B2 Particle Field | Canvas | Heavy | cyber-dark, clean-tech, retro-future |
| B3 Noise Texture | Canvas | Light | ALL (grain is universal) |
| B4 Aurora Wave | Canvas | Medium | organic-soft, coastal, candy |
| C1 Conic Mesh | CSS | Light | art-deco, candy, retro-future |
| C2 Gradient Shift | CSS | Light | candy, retro-future, organic-soft |
| C3 Grain Overlay | CSS | Light | ALL (essential for editorial / organic) |
| C4 Dot Grid | CSS | Light | neo-swiss, corporate, clean-tech |
