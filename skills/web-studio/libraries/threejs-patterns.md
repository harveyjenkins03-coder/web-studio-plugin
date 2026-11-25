# Three.js Patterns Library

Production-ready Three.js recipes for Phase 3-4. Use for hero backgrounds, interactive art, and immersive sections. All patterns use CDN imports and integrate with GSAP ScrollTrigger.

---

## Setup

```html
<script type="importmap">
  {
    "imports": {
      "three": "https://cdn.jsdelivr.net/npm/three@0.166/build/three.module.js",
      "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.166/examples/jsm/"
    }
  }
</script>

<script type="module">
  import * as THREE from 'three';
  // patterns below use this import
</script>
```

### Base Scene Template
```js
function createScene(canvas) {
  const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  renderer.setSize(canvas.clientWidth, canvas.clientHeight);

  const scene = new THREE.Scene();

  const camera = new THREE.PerspectiveCamera(75, canvas.clientWidth / canvas.clientHeight, 0.1, 100);
  camera.position.z = 3;

  // Resize handler
  const resizeObserver = new ResizeObserver(() => {
    renderer.setSize(canvas.clientWidth, canvas.clientHeight);
    camera.aspect = canvas.clientWidth / canvas.clientHeight;
    camera.updateProjectionMatrix();
  });
  resizeObserver.observe(canvas.parentElement);

  return { renderer, scene, camera };
}
```

---

## Pattern 1: Particle Field (dark-luxe, cosmic, cyber-dark)

A 3D point cloud that drifts gently. Responds to mouse position.

```js
import * as THREE from 'three';

function createParticleField(canvas, options = {}) {
  const {
    count = 3000,
    color = 0xffffff,
    size = 0.003,
    spread = 5,
    mouseStrength = 0.0003,
  } = options;

  const { renderer, scene, camera } = createScene(canvas);

  // Geometry
  const positions = new Float32Array(count * 3);
  for (let i = 0; i < count; i++) {
    positions[i * 3 + 0] = (Math.random() - 0.5) * spread;
    positions[i * 3 + 1] = (Math.random() - 0.5) * spread;
    positions[i * 3 + 2] = (Math.random() - 0.5) * spread;
  }

  const geometry = new THREE.BufferGeometry();
  geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));

  const material = new THREE.PointsMaterial({
    color,
    size,
    sizeAttenuation: true,
    transparent: true,
    opacity: 0.7,
  });

  const particles = new THREE.Points(geometry, material);
  scene.add(particles);

  // Mouse parallax
  let mouse = { x: 0, y: 0 };
  document.addEventListener('mousemove', e => {
    mouse.x = (e.clientX / window.innerWidth - 0.5) * 2;
    mouse.y = -(e.clientY / window.innerHeight - 0.5) * 2;
  });

  // Animation loop
  let frame;
  function animate() {
    frame = requestAnimationFrame(animate);
    particles.rotation.y += 0.0003;
    particles.rotation.x += 0.0001;
    camera.position.x += (mouse.x * 0.5 - camera.position.x) * mouseStrength * 60;
    camera.position.y += (mouse.y * 0.5 - camera.position.y) * mouseStrength * 60;
    renderer.render(scene, camera);
  }
  animate();

  return () => { cancelAnimationFrame(frame); renderer.dispose(); };
}
```

---

## Pattern 2: Gradient Mesh / Noise Plane (warm-gradient, organic-soft)

An animated plane displaced by noise — the Three.js "blob" pattern.

```js
import * as THREE from 'three';
import { SimplexNoise } from 'three/addons/math/SimplexNoise.js';

function createNoiseMesh(canvas, options = {}) {
  const {
    color1 = 0xff6030,
    color2 = 0x30a0ff,
    speed = 0.002,
    amplitude = 0.3,
  } = options;

  const { renderer, scene, camera } = createScene(canvas);
  camera.position.z = 2.5;

  const noise = new SimplexNoise();
  const geometry = new THREE.PlaneGeometry(4, 4, 64, 64);
  const positions = geometry.attributes.position;

  const material = new THREE.ShaderMaterial({
    uniforms: {
      uTime: { value: 0 },
      uColor1: { value: new THREE.Color(color1) },
      uColor2: { value: new THREE.Color(color2) },
    },
    vertexShader: `
      uniform float uTime;
      varying vec2 vUv;
      varying float vElevation;

      vec4 permute(vec4 x){ return mod(((x*34.0)+1.0)*x, 289.0); }
      float snoise(vec3 v) {
        const vec2 C = vec2(1.0/6.0, 1.0/3.0);
        const vec4 D = vec4(0.0, 0.5, 1.0, 2.0);
        vec3 i = floor(v + dot(v, C.yyy));
        vec3 x0 = v - i + dot(i, C.xxx);
        vec3 g = step(x0.yzx, x0.xyz);
        vec3 l = 1.0 - g;
        vec3 i1 = min(g.xyz, l.zxy);
        vec3 i2 = max(g.xyz, l.zxy);
        vec3 x1 = x0 - i1 + C.xxx;
        vec3 x2 = x0 - i2 + C.yyy;
        vec3 x3 = x0 - D.yyy;
        i = mod(i, 289.0);
        vec4 p = permute(permute(permute(i.z + vec4(0.0, i1.z, i2.z, 1.0)) + i.y + vec4(0.0, i1.y, i2.y, 1.0)) + i.x + vec4(0.0, i1.x, i2.x, 1.0));
        float n_ = 1.0/7.0;
        vec3 ns = n_ * D.wyz - D.xzx;
        vec4 j = p - 49.0 * floor(p * ns.z * ns.z);
        vec4 x_ = floor(j * ns.z);
        vec4 y_ = floor(j - 7.0 * x_);
        vec4 x = x_ * ns.x + ns.yyyy;
        vec4 y = y_ * ns.x + ns.yyyy;
        vec4 h = 1.0 - abs(x) - abs(y);
        vec4 b0 = vec4(x.xy, y.xy);
        vec4 b1 = vec4(x.zw, y.zw);
        vec4 s0 = floor(b0)*2.0 + 1.0;
        vec4 s1 = floor(b1)*2.0 + 1.0;
        vec4 sh = -step(h, vec4(0.0));
        vec4 a0 = b0.xzyw + s0.xzyw*sh.xxyy;
        vec4 a1 = b1.xzyw + s1.xzyw*sh.zzww;
        vec3 p0 = vec3(a0.xy, h.x);
        vec3 p1 = vec3(a0.zw, h.y);
        vec3 p2 = vec3(a1.xy, h.z);
        vec3 p3 = vec3(a1.zw, h.w);
        vec4 norm = inversesqrt(vec4(dot(p0,p0), dot(p1,p1), dot(p2,p2), dot(p3,p3)));
        p0 *= norm.x; p1 *= norm.y; p2 *= norm.z; p3 *= norm.w;
        vec4 m = max(0.6 - vec4(dot(x0,x0), dot(x1,x1), dot(x2,x2), dot(x3,x3)), 0.0);
        m = m * m;
        return 42.0 * dot(m*m, vec4(dot(p0,x0), dot(p1,x1), dot(p2,x2), dot(p3,x3)));
      }

      void main() {
        vUv = uv;
        vec3 pos = position;
        float elevation = snoise(vec3(pos.x * 1.5, pos.y * 1.5, uTime)) * ${amplitude};
        pos.z += elevation;
        vElevation = elevation;
        gl_Position = projectionMatrix * modelViewMatrix * vec4(pos, 1.0);
      }
    `,
    fragmentShader: `
      uniform vec3 uColor1;
      uniform vec3 uColor2;
      varying float vElevation;
      void main() {
        float t = (vElevation + ${amplitude}) / (${amplitude * 2});
        vec3 color = mix(uColor1, uColor2, t);
        gl_FragColor = vec4(color, 0.85);
      }
    `,
    transparent: true,
  });

  const mesh = new THREE.Mesh(geometry, material);
  mesh.rotation.x = -0.3;
  scene.add(mesh);

  let frame;
  function animate() {
    frame = requestAnimationFrame(animate);
    material.uniforms.uTime.value += speed;
    renderer.render(scene, camera);
  }
  animate();

  return () => { cancelAnimationFrame(frame); renderer.dispose(); };
}
```

---

## Pattern 3: Floating Geometry (neo-swiss, brutalist-pop)

Abstract geometric shapes floating in space. Good for landing pages needing 3D depth without full scenes.

```js
import * as THREE from 'three';

function createFloatingGeometry(canvas, options = {}) {
  const {
    shapes = ['box', 'torus', 'octahedron'],
    color = 0xff3d00,
    wireframe = false,
  } = options;

  const { renderer, scene, camera } = createScene(canvas);

  const geometries = {
    box:          new THREE.BoxGeometry(1, 1, 1),
    torus:        new THREE.TorusGeometry(0.6, 0.2, 16, 100),
    octahedron:   new THREE.OctahedronGeometry(0.7),
    icosahedron:  new THREE.IcosahedronGeometry(0.7, 0),
    tetrahedron:  new THREE.TetrahedronGeometry(0.8),
  };

  const material = new THREE.MeshNormalMaterial({ wireframe });

  const meshes = shapes.map((shape, i) => {
    const geo = geometries[shape] || geometries.box;
    const mesh = new THREE.Mesh(geo, material);
    mesh.position.set((i - shapes.length / 2) * 2, Math.sin(i) * 0.5, 0);
    scene.add(mesh);
    return mesh;
  });

  // Mouse orbit
  let mouse = { x: 0, y: 0 };
  canvas.parentElement.addEventListener('mousemove', e => {
    const rect = canvas.parentElement.getBoundingClientRect();
    mouse.x = ((e.clientX - rect.left) / rect.width - 0.5) * 2;
    mouse.y = -((e.clientY - rect.top) / rect.height - 0.5) * 2;
  });

  let frame;
  function animate(t) {
    frame = requestAnimationFrame(animate);
    meshes.forEach((mesh, i) => {
      mesh.rotation.x = t * 0.0003 + i * 0.5;
      mesh.rotation.y = t * 0.0004 + i * 0.3;
      mesh.position.y = Math.sin(t * 0.001 + i) * 0.3;
    });
    camera.position.x += (mouse.x * 0.5 - camera.position.x) * 0.05;
    camera.position.y += (mouse.y * 0.5 - camera.position.y) * 0.05;
    camera.lookAt(scene.position);
    renderer.render(scene, camera);
  }
  animate(0);

  return () => { cancelAnimationFrame(frame); renderer.dispose(); };
}
```

---

## DOM Integration — Scroll Scrub

Sync Three.js state with scroll progress using GSAP ScrollTrigger:

```js
ScrollTrigger.create({
  trigger: '.three-section',
  start: 'top top',
  end: 'bottom top',
  scrub: true,
  onUpdate: self => {
    // self.progress: 0 to 1
    mesh.rotation.y = self.progress * Math.PI * 2;
    camera.position.z = 3 - self.progress * 1.5;
    material.uniforms.uProgress.value = self.progress;
  },
});
```

---

## Performance Rules

1. **Limit draw calls** — merge static geometries with `BufferGeometryUtils.mergeGeometries()`
2. **Cap pixel ratio at 2** — `renderer.setPixelRatio(Math.min(devicePixelRatio, 2))`
3. **Dispose on unmount** — geometry.dispose(), material.dispose(), renderer.dispose()
4. **Use `alpha: true`** only when needed for CSS background to show through
5. **Prefer `MeshBasicMaterial`** for non-shaded scenes — no lighting calculations
6. **Throttle mouse events** — use `requestAnimationFrame` gate for mouse-follow logic
7. **Pause when off-screen** — use IntersectionObserver to stop animation loop
