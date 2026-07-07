# 🌌 Gravitational Lensing

> Schwarzschild black hole gravitational lensing simulator built with Three.js + WebGL fragment shader

Real-time photon ray-marching through the Schwarzschild metric renders an Einstein ring, photon sphere, and the iconic black hole shadow as the renderer integrates light paths around the singularity.

[🇰🇷 한국어](./README.md) · [🇺🇸 English (default)](#)

---

## 🎬 Live Demo

> **👉 [https://gravitational-lensing-flax.vercel.app/](https://gravitational-lensing-flax.vercel.app/)** — Run instantly in any modern browser (WebGL required)

| | |
|---|---|
| ![Live](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Fgravitational--lensing-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/gravitational-lensing) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Three.js%20%2B%20WebGL-000000?style=flat-square&logo=three.js&logoColor=white) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-1_CDN-9CA3AF?style=flat-square) |

### ⚡ Quick Start
1. Click the demo link above → page opens in browser
2. **Drag** — orbit the camera around the black hole
3. **Scroll** — zoom in / out
4. **4 sliders** — Schwarzschild radius / camera distance / star density / lensing strength
5. **한 / EN button** — toggle UI between Korean and English

---

## 🤖 Generation Info

This project's code was generated automatically using the model and prompt below.

| Item | Value |
|---|---|
| **Model** | MiniMax-M3 (MiniMax) |
| **Environment** | OpenCode CLI |
| **Repository** | [`sigco3111/gravitational-lensing`](https://github.com/sigco3111/gravitational-lensing) |
| **License** | MIT |
| **Dependencies** | 1 (Three.js 0.160.0 — unpkg CDN ES module) |

### 📝 Prompt Used (Original)

```
Build an interactive gravitational lensing simulator that shows starlight
bending around a Schwarzschild black hole of about 10 solar masses — the
Einstein ring, photon sphere, and black hole shadow. Provide sliders for
Schwarzschild radius, star density, and camera distance, and let users
orbit the camera by mouse drag.

Implementation Advice: Use Three.js + WebGL fragment shader for real-time
photon ray-marching through the Schwarzschild metric. Compute the critical
impact parameter bc = (3√3/2)·rs in GLSL for the photon sphere.
Package all dependencies in a single HTML file.
```

---

## ✨ Features

- 🌀 **Schwarzschild Ray Tracing** — real-time photon path integration in the fragment shader
- 🎯 **Einstein Ring / Photon Sphere** — critical impact parameter `bc = (3√3)/2 ≈ 2.598` computed to 8 decimals
- 🌑 **Black Hole Shadow** — event horizon + photon capture region visualized
- 🎛️ **4 Live Sliders** — `r_s` / camera distance / star density / lensing strength
- 🌍 **Procedural Galaxy Background** — GLSL FBM noise + nebula color blending (no texture files)
- 🌐 **Built-in Korean/English Toggle** — instant UI switch + localStorage persistence
- 📦 **Single HTML** — 35 KB ES module + Three.js CDN

---

## 🚀 Quick Start

### Method 1: Open directly in browser (WebGL enabled)
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### Method 2: Local server (recommended — avoids ES module CORS issues)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

### Method 3: Live Demo
Open the Vercel alias URL above — no install required.

---

## 🎮 Controls

| Input | Effect |
|---|---|
| **Drag** | Orbit the camera |
| **Scroll** | Zoom in / out |
| **Touch drag** | Same on mobile |
| **R key** | Reset view (`θ=0.3, φ=0.25, dist=5.0, r_s=0.5`) |
| **r_s slider** | Schwarzschild radius (event horizon size) |
| **Camera distance slider** | Distance from camera to black hole |
| **Star density slider** | Background star count / distribution |
| **Lensing strength slider** | Photon refraction multiplier |
| **한 / EN button** | UI language toggle |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Rendering** | Three.js 0.160.0 + WebGL fragment shader |
| **Physics** | Schwarzschild metric ray-marching |
| **Shader** | GLSL FBM noise + Schwarzschild integrator |
| **Camera** | Spherical coordinates (`θ`, `φ`, `distance`) |
| **Precision** | `CRITICAL_IMPACT_FACTOR.toFixed(8)` injected into GLSL |
| **Dependencies** | 1 (Three.js, unpkg CDN) |

### Key Constants

| Constant | Value | Meaning |
|---|---|---|
| `BH_CENTER` | `(0, 0, 0)` | Black hole position (origin) |
| `CRITICAL_IMPACT_FACTOR` | `(3√3)/2 ≈ 2.598076211` | Critical impact parameter for photon capture |
| `state.rs` (default) | `0.5` | Schwarzschild radius |
| `state.cameraDistance` (default) | `5.0` | Camera distance |
| `state.lensingStrength` (default) | `1.0×` | Lensing strength multiplier |
| `state.cameraTheta / Phi` (default) | `0.3 / 0.25` | Initial viewing angles |

---

## 📂 Project Structure

```
gravitational-lensing/
├── index.html      # Single HTML containing all code (~35KB)
├── README.md       # 한국어 (default)
├── README.en.md    # English
└── LICENSE         # MIT
```

---

## 🎨 Design Decisions

Five choices made during brainstorming:

| Decision Point | Choice | Rationale |
|---|---|---|
| **Rendering** | GPU fragment shader ray-marching | Stable 60fps vs. CPU integration |
| **Ray Integration** | Direct Schwarzschild metric calculation | Accurate Einstein ring + photon sphere |
| **Critical Coefficient** | `(3√3)/2` injected via `.toFixed(8)` into GLSL | Avoids JS IEEE 754 drift; shader sees fixed-precision |
| **Galaxy Background** | GLSL FBM noise + nebula color blend | Procedural stars/dust, zero texture dependencies |
| **i18n** | Built-in toggle + localStorage | Instant ko/en switch, persists across reloads |

### Customization

Tune the `i18n` object and shader constants in `index.html`:

```js
const i18n = {
  ko: { pageTitle: '중력 렌즈 — 슈바르츠실트 블랙홀', /* ... */ },
  en: { pageTitle: 'Gravitational Lensing — Schwarzschild Black Hole', /* ... */ }
};

const CRITICAL_IMPACT_FACTOR = (3.0 * Math.sqrt(3.0)) / 2.0;  // photon capture threshold
```

Advanced: tweak the GLSL fragment shader's `vec3 bg`, `galNormal`, and nebula color constants to alter the cosmic backdrop.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

This project was generated by the **MiniMax-M3** model in the OpenCode CLI environment. Prompt engineering and design decisions were made directly by the repository owner.