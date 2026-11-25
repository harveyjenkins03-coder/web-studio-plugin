# Smart Photo Sourcing

Strategies for sourcing, treating, and integrating photography into Web Studio sites. All treatments use design token colors and pair with DNA profiles.

---

## A. Unsplash / Pexels URL Patterns

### Direct Image URLs

**Unsplash format:**
```
https://images.unsplash.com/photo-{PHOTO_ID}?w={WIDTH}&h={HEIGHT}&fit=crop&q=80
```

Parameters:
- `w` --- width in pixels
- `h` --- height in pixels (optional; omit for natural aspect ratio)
- `fit=crop` --- crops to exact dimensions (center-weighted)
- `q=80` --- JPEG quality (60-80 recommended for web)
- `auto=format` --- serves WebP when browser supports it
- `crop=faces` --- prioritizes face detection when cropping

**Pexels format:**
```
https://images.pexels.com/photos/{PHOTO_ID}/pexels-photo-{PHOTO_ID}.jpeg?auto=compress&cs=tinysrgb&w={WIDTH}&h={HEIGHT}&fit=crop
```

### Search-Based URLs (for prototyping)

**Unsplash Source (random image from search):**
```
https://source.unsplash.com/featured/{WIDTH}x{HEIGHT}/?{QUERY}
```
Example: `https://source.unsplash.com/featured/1920x1080/?dark,architecture`

> Note: Source URLs redirect and are slower. Use for prototyping only; replace with specific photo IDs for production.

### Size Recommendations

| Context | Width | Use Case |
|---------|-------|----------|
| Thumbnail | 640 | Cards, grid items, mobile hero |
| Standard | 1024 | Section backgrounds, tablet hero |
| Full-width | 1920 | Desktop hero, full-bleed sections |
| Retina hero | 2560 | High-DPI full-bleed backgrounds |

Always pair with `loading="lazy"` except for above-the-fold hero images.

---

## B. Aesthetic-Tuned Query Templates by DNA Category

### Dark Profiles (cyber-dark, editorial-dark, brutalist)

```
"dramatic shadows architecture"
"moody portrait high contrast"
"night city neon"
"dark texture concrete"
"low key studio lighting"
"industrial interior shadows"
"abstract dark smoke"
"noir street photography"
```

### Light Profiles (clean-tech, corporate-clean, coastal-minimal)

```
"soft natural light minimal"
"bright airy interior"
"pastel abstract texture"
"white marble surface"
"clean workspace overhead"
"light linen fabric texture"
"morning mist landscape"
"minimal architecture white"
```

### Bold Profiles (candy, retro-future)

```
"vivid color street art"
"bold geometric abstract"
"high saturation fashion"
"neon sign closeup"
"colorful food styling"
"pop art inspired"
"bright gradient abstract"
"vibrant tropical botanical"
```

### Organic Profiles (organic-soft, japanese-minimal)

```
"earth tones nature macro"
"warm botanical"
"handcraft texture closeup"
"ceramic pottery detail"
"dried flowers natural"
"wood grain texture warm"
"wabi sabi imperfect"
"linen cotton natural texture"
```

### Tech Profiles (clean-tech, cyber-dark)

```
"abstract technology dark"
"circuit board macro"
"data visualization"
"server rack lights"
"holographic texture"
"wireframe 3d render"
"code on screen dark"
"fiber optic abstract"
```

---

## C. CSS Treatment Recipes

### C1. Duotone Filter (mix-blend-mode approach)

Maps image to two colors using blend modes. Works on any image without SVG.

```css
.duotone-blend {
  position: relative;
  overflow: hidden;
}
.duotone-blend img {
  filter: grayscale(100%) contrast(1.2);
  width: 100%;
  display: block;
}
.duotone-blend::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom right,
    var(--color-accent),
    var(--color-accent2)
  );
  mix-blend-mode: color;
  pointer-events: none;
}
```

### C2. Duotone Filter (SVG feColorMatrix approach)

Precise duotone using SVG color matrix. More control over shadow and highlight mapping.

```html
<svg width="0" height="0" style="position:absolute;">
  <filter id="duotone-filter">
    <feColorMatrix type="matrix"
      values="0.2 0.2 0.2 0 0.06
              0.1 0.1 0.1 0 0.02
              0.08 0.08 0.08 0 0.15
              0 0 0 1 0" />
  </filter>
</svg>
```

```css
.duotone-svg img {
  filter: url(#duotone-filter);
}
```

**To generate a custom duotone matrix from two hex colors:**

```js
function duotoneMatrix(shadow, highlight) {
  const s = [
    parseInt(shadow.slice(1,3), 16) / 255,
    parseInt(shadow.slice(3,5), 16) / 255,
    parseInt(shadow.slice(5,7), 16) / 255,
  ];
  const h = [
    parseInt(highlight.slice(1,3), 16) / 255,
    parseInt(highlight.slice(3,5), 16) / 255,
    parseInt(highlight.slice(5,7), 16) / 255,
  ];
  return [
    h[0]-s[0], 0, 0, 0, s[0],
    0, h[1]-s[1], 0, 0, s[1],
    0, 0, h[2]-s[2], 0, s[2],
    0, 0, 0, 1, 0
  ].join(' ');
}
// Usage: duotoneMatrix('#0a0a2e', '#ff5722')
```

### C3. Grain Overlay (pseudo-element with noise)

Adds film grain texture over photos for editorial warmth.

```css
.photo-grain {
  position: relative;
}
.photo-grain::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0.3;
  mix-blend-mode: overlay;
  filter: url(#grain-filter);
}
```

```html
<svg width="0" height="0" style="position:absolute;">
  <filter id="grain-filter">
    <feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="4" stitchTiles="stitch" />
    <feColorMatrix type="saturate" values="0" />
  </filter>
</svg>
```

### C4. Desaturation + Contrast Boost

Muted, editorial look. Reduces color distraction while preserving form.

```css
.photo-desat {
  filter: saturate(0.3) contrast(1.3) brightness(0.95);
  transition: filter 0.5s ease;
}
/* Optional: restore on hover */
.photo-desat:hover {
  filter: saturate(1) contrast(1) brightness(1);
}
```

### C5. High Contrast Black & White

Classic monochrome treatment. Pairs with brutalist, editorial-serif, japanese-minimal.

```css
.photo-bw {
  filter: grayscale(100%) contrast(1.4) brightness(0.9);
}
/* Tinted B&W using accent color overlay */
.photo-bw-tinted {
  position: relative;
}
.photo-bw-tinted img {
  filter: grayscale(100%) contrast(1.2);
}
.photo-bw-tinted::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-accent);
  mix-blend-mode: multiply;
  opacity: 0.15;
  pointer-events: none;
}
```

### C6. Clip-Path Crops

Non-rectangular image framing using CSS `clip-path`.

```css
/* Circle crop */
.clip-circle {
  clip-path: circle(45% at 50% 50%);
}

/* Angled polygon */
.clip-angle {
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
}

/* Organic blob */
.clip-organic {
  clip-path: polygon(
    30% 0%, 70% 0%, 100% 30%, 100% 70%,
    70% 100%, 30% 100%, 0% 70%, 0% 30%
  );
  border-radius: 30% 70% 70% 30% / 30% 30% 70% 70%;
}

/* Diamond */
.clip-diamond {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
}

/* Rounded rectangle (with border-radius fallback) */
.clip-rounded {
  clip-path: inset(0 round 24px);
}
```

### C7. Color Overlay Blend

Layer a semi-transparent color over the image using blend modes.

```css
/* Multiply --- darkens image with color tint */
.overlay-multiply {
  position: relative;
}
.overlay-multiply::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-accent);
  mix-blend-mode: multiply;
  opacity: 0.6;
  pointer-events: none;
}

/* Overlay --- increases contrast with color wash */
.overlay-overlay::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-bg);
  mix-blend-mode: overlay;
  opacity: 0.4;
  pointer-events: none;
}

/* Soft light --- subtle warm/cool shift */
.overlay-softlight::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-accent2);
  mix-blend-mode: soft-light;
  opacity: 0.5;
  pointer-events: none;
}
```

### C8. Hover Reveal (heavy treatment to full color)

Image starts with heavy treatment, reveals full color on hover via CSS transition.

```css
.hover-reveal {
  position: relative;
  overflow: hidden;
}
.hover-reveal img {
  filter: grayscale(100%) contrast(1.2) brightness(0.8);
  transition: filter 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  width: 100%;
  display: block;
}
.hover-reveal:hover img {
  filter: grayscale(0%) contrast(1) brightness(1);
}

/* With color overlay that fades */
.hover-reveal::after {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--color-accent);
  mix-blend-mode: color;
  opacity: 0.7;
  transition: opacity 0.6s cubic-bezier(0.16, 1, 0.3, 1);
  pointer-events: none;
}
.hover-reveal:hover::after {
  opacity: 0;
}
```

**Combined treatment with scale zoom:**

```css
.hover-reveal-zoom {
  position: relative;
  overflow: hidden;
}
.hover-reveal-zoom img {
  filter: grayscale(80%) saturate(0.2);
  transform: scale(1.05);
  transition: filter 0.8s ease, transform 0.8s ease;
  width: 100%;
  display: block;
}
.hover-reveal-zoom:hover img {
  filter: grayscale(0%) saturate(1);
  transform: scale(1);
}
```

---

## D. Responsive Image Patterns

### srcset with Multiple Sizes

Serves the right image size based on viewport width.

```html
<img
  src="https://images.unsplash.com/photo-ID?w=1024&fit=crop&q=80"
  srcset="
    https://images.unsplash.com/photo-ID?w=640&fit=crop&q=80   640w,
    https://images.unsplash.com/photo-ID?w=1024&fit=crop&q=80  1024w,
    https://images.unsplash.com/photo-ID?w=1920&fit=crop&q=80  1920w,
    https://images.unsplash.com/photo-ID?w=2560&fit=crop&q=80  2560w
  "
  sizes="(max-width: 640px) 100vw, (max-width: 1024px) 100vw, 1920px"
  alt="Descriptive alt text"
  loading="lazy"
  decoding="async"
/>
```

### Picture Element with WebP + Fallback

Serves WebP when supported, JPEG as fallback.

```html
<picture>
  <source
    type="image/webp"
    srcset="
      https://images.unsplash.com/photo-ID?w=640&fit=crop&q=80&fm=webp   640w,
      https://images.unsplash.com/photo-ID?w=1024&fit=crop&q=80&fm=webp  1024w,
      https://images.unsplash.com/photo-ID?w=1920&fit=crop&q=80&fm=webp  1920w
    "
    sizes="(max-width: 640px) 100vw, (max-width: 1024px) 100vw, 1920px"
  />
  <source
    type="image/jpeg"
    srcset="
      https://images.unsplash.com/photo-ID?w=640&fit=crop&q=80   640w,
      https://images.unsplash.com/photo-ID?w=1024&fit=crop&q=80  1024w,
      https://images.unsplash.com/photo-ID?w=1920&fit=crop&q=80  1920w
    "
    sizes="(max-width: 640px) 100vw, (max-width: 1024px) 100vw, 1920px"
  />
  <img
    src="https://images.unsplash.com/photo-ID?w=1024&fit=crop&q=80"
    alt="Descriptive alt text"
    loading="lazy"
    decoding="async"
    width="1920"
    height="1080"
  />
</picture>
```

### Art Direction with Breakpoint-Specific Crops

Different crops or images at different breakpoints.

```html
<picture>
  <!-- Mobile: tighter crop, portrait orientation -->
  <source
    media="(max-width: 767px)"
    srcset="https://images.unsplash.com/photo-ID?w=640&h=800&fit=crop&crop=faces&q=80"
  />
  <!-- Tablet: square crop -->
  <source
    media="(max-width: 1023px)"
    srcset="https://images.unsplash.com/photo-ID?w=1024&h=1024&fit=crop&q=80"
  />
  <!-- Desktop: wide landscape -->
  <img
    src="https://images.unsplash.com/photo-ID?w=1920&h=1080&fit=crop&q=80"
    alt="Descriptive alt text"
    loading="lazy"
    width="1920"
    height="1080"
  />
</picture>
```

### Lazy Loading with Placeholder

Low-quality image placeholder (LQIP) pattern for smooth loading.

```css
.photo-container {
  position: relative;
  background-color: var(--color-surface);
  overflow: hidden;
}
.photo-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transition: opacity 0.5s ease;
}
.photo-container img.loaded {
  opacity: 1;
}
/* Tiny blurred placeholder inline as base64 */
.photo-container::before {
  content: '';
  position: absolute;
  inset: 0;
  background-size: cover;
  background-position: center;
  filter: blur(20px);
  transform: scale(1.1);
}
```

```js
document.querySelectorAll('.photo-container img').forEach(img => {
  if (img.complete) {
    img.classList.add('loaded');
  } else {
    img.addEventListener('load', () => img.classList.add('loaded'));
  }
});
```

---

## E. Treatment Pairing Guide

| DNA Profile | Primary Treatment | Secondary Treatment | Query Style |
|-------------|-------------------|---------------------|-------------|
| cyber-dark | C1 Duotone (blend) | C3 Grain | dark, dramatic |
| editorial-dark | C5 High-Contrast B&W | C3 Grain | moody, shadows |
| brutalist | C5 B&W + C4 Desat | C7 Multiply overlay | raw, industrial |
| clean-tech | C4 Desat + Contrast | C6 Clip circle | minimal, light |
| corporate-clean | C4 Slight desat | C8 Hover reveal | professional |
| coastal-minimal | C7 Soft-light overlay | C3 Grain | soft, natural |
| organic-soft | C7 Soft-light | C3 Grain | earthy, warm |
| japanese-minimal | C5 B&W tinted | C6 Clip organic | wabi-sabi |
| candy | C1 Duotone (vivid) | C8 Hover reveal | colorful, bold |
| retro-future | C2 Duotone (SVG) | C3 Grain | neon, retro |
| art-deco | C7 Multiply (gold) | C6 Diamond clip | luxurious |
| neo-swiss | C4 Desat | C6 Angle clip | geometric |
| editorial-serif | C5 B&W | C3 Grain + C8 Hover | editorial |
