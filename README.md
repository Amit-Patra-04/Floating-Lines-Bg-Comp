# ✨ Floating Lines — Interactive Background Component
A GPU-accelerated, interactive animated wave background built with React & Three.js.  A drop-in React component that renders beautiful, animated floating wave lines as a full-screen or container-bound background. Powered by custom GLSL shaders and Three.js for silky-smooth, GPU-accelerated performance. Supports mouse interactivity, parallax effects, multi-stop gradient coloring, and fine-grained control over every wave layer.

---

## 📷 Component Preview

![Component Preview] <img width="1857" height="845" alt="Image" src="https://github.com/user-attachments/assets/ec01a8f9-c6f2-4e09-9539-c367b20809f4" />

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Usage](#-usage)
- [Props Reference](#-props-reference)
- [How It Works](#-how-it-works)
- [Customization Examples](#-customization-examples)
- [Performance](#-performance)
- [Browser Support](#-browser-support)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

## 🚀 Features

| Feature | Description |
|---|---|
| **🎨 Custom GLSL Shaders** | Hand-written vertex & fragment shaders deliver smooth, organic wave animations entirely on the GPU |
| **🖱️ Mouse Interactivity** | Waves bend and react to cursor movement in real-time with configurable bend radius & strength |
| **🌊 Multi-Layer Waves** | Three independent wave layers (`top`, `middle`, `bottom`) — enable/disable any combination |
| **🎛️ Fine-Grained Control** | Per-wave line count, line spacing, position, and rotation for pixel-perfect layouts |
| **🌈 Gradient Coloring** | Supports up to 8-stop custom color gradients across wave lines via hex values |
| **📐 Parallax Effect** | Subtle depth illusion that follows cursor movement for an immersive 3D feel |
| **⚡ GPU Accelerated** | Entire animation runs on the GPU via WebGL — zero jank, minimal CPU overhead |
| **📱 Responsive** | Uses `ResizeObserver` to adapt seamlessly to any container size or viewport change |
| **🧹 Clean Lifecycle** | Proper disposal of WebGL contexts, geometries, materials, and event listeners on unmount |
| **🔀 Blend Modes** | CSS `mix-blend-mode` support for compositing over existing content |

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [React](https://react.dev/) | `19.x` | Component architecture & reactive UI |
| [Three.js](https://threejs.org/) | `r184` | WebGL rendering engine & shader pipeline |
| [Vite](https://vite.dev/) | `8.x` | Lightning-fast dev server & build tool |
| [Tailwind CSS](https://tailwindcss.com/) | `4.x` | Utility-first CSS framework |
| [ESLint](https://eslint.org/) | `10.x` | Code quality & linting |

---

## 📂 Project Structure

```
Floating-Lines-Bg-Comp/
├── public/
│   └── Images/
│       └── favIcon.png              # Favicon asset
├── src/
│   ├── FloatingLines.jsx            # ✨ Core component — shaders, Three.js setup, all logic
│   ├── App.jsx                      # Demo usage & prop configuration
│   ├── App.css                      # Tailwind CSS entry point
│   └── main.jsx                     # React DOM mount point
├── index.html                       # HTML entry with favicon & viewport meta
├── vite.config.js                   # Vite config with React & Tailwind plugins
├── eslint.config.js                 # ESLint flat config with React hooks rules
├── package.json                     # Dependencies & scripts
├── .gitignore                       # Standard exclusions
└── README.md                        # You are here
```

---

## ⚙️ Getting Started

### Prerequisites

- **Node.js** — `v18.0+` recommended
- **npm** — `v9.0+` (ships with Node.js)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Amit-Patra-04/Floating-Lines-Bg-Comp.git

# 2. Navigate into the project
cd Floating-Lines-Bg-Comp

# 3. Install dependencies
npm install

# 4. Start the development server
npm run dev
```

The app will be available at `http://localhost:5173` by default.

### Available Scripts

| Script | Command | Description |
|---|---|---|
| **Dev** | `npm run dev` | Start Vite dev server with HMR |
| **Build** | `npm run build` | Create production-optimized bundle in `dist/` |
| **Preview** | `npm run preview` | Locally preview the production build |
| **Lint** | `npm run lint` | Run ESLint across the project |

---

## 📖 Usage

### Basic Usage

Import the `FloatingLines` component and place it inside a container with defined dimensions:

```jsx
import FloatingLines from './FloatingLines';

function App() {
  return (
    <div style={{ width: '100%', height: '100vh', position: 'relative' }}>
      <FloatingLines />
    </div>
  );
}
```

### With Custom Props

```jsx
<FloatingLines
  enabledWaves={["top", "middle", "bottom"]}
  lineCount={8}
  lineDistance={8}
  bendRadius={8}
  bendStrength={-2}
  interactive
  parallax={true}
  animationSpeed={1}
  linesGradient={["#e945f5", "#6f6f6f", "#6a6a6a"]}
/>
```

### As a Background Layer

Overlay content on top of the animated background using absolute positioning:

```jsx
<div style={{ position: 'relative', width: '100%', height: '100vh' }}>
  {/* Animated Background */}
  <FloatingLines
    enabledWaves={["top", "middle", "bottom"]}
    lineCount={6}
    interactive
    parallax
    mixBlendMode="screen"
  />

  {/* Your Content */}
  <div style={{ position: 'absolute', inset: 0, zIndex: 10 }}>
    <h1>Your Content Here</h1>
  </div>
</div>
```

---

## 📋 Props Reference

### Core Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `enabledWaves` | `string[]` | `["top", "middle", "bottom"]` | Which wave layers to render. Options: `"top"`, `"middle"`, `"bottom"` |
| `lineCount` | `number \| number[]` | `[6]` | Number of lines per wave. Pass a single number for all waves, or an array matching `enabledWaves` order |
| `lineDistance` | `number \| number[]` | `[5]` | Spacing between lines. Same array/number behavior as `lineCount` |
| `animationSpeed` | `number` | `1` | Wave animation speed multiplier |

### Interactivity Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `interactive` | `boolean` | `true` | Enable mouse-reactive wave bending |
| `bendRadius` | `number` | `5.0` | Radius of the cursor influence zone (higher = wider area) |
| `bendStrength` | `number` | `-0.5` | Intensity of the bend effect (negative = push away, positive = pull) |
| `mouseDamping` | `number` | `0.05` | Smoothing factor for cursor tracking (`0` = instant, `1` = no smoothing) |

### Parallax Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `parallax` | `boolean` | `true` | Enable parallax depth effect on mouse move |
| `parallaxStrength` | `number` | `0.2` | Intensity of the parallax offset |

### Wave Position Props

Each wave layer's origin can be configured independently:

| Prop | Type | Default | Description |
|---|---|---|---|
| `topWavePosition` | `{ x, y, rotate }` | `{ x: 10.0, y: 0.5, rotate: -0.4 }` | Position and rotation of the top wave layer |
| `middleWavePosition` | `{ x, y, rotate }` | `{ x: 5.0, y: 0.0, rotate: 0.2 }` | Position and rotation of the middle wave layer |
| `bottomWavePosition` | `{ x, y, rotate }` | `{ x: 2.0, y: -0.7, rotate: -1.0 }` | Position and rotation of the bottom wave layer |

### Styling Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `linesGradient` | `string[]` | `undefined` | Array of hex color strings (up to 8 stops) for line coloring. When set, replaces the default background-based coloring |
| `mixBlendMode` | `string` | `"screen"` | CSS blend mode for compositing the canvas over parent content |

---

## 🔬 How It Works

### Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│                   React Component                   │
│  ┌───────────────────────────────────────────────┐  │
│  │  useEffect — initializes Three.js scene       │  │
│  │  ┌─────────────┐  ┌────────────────────────┐  │  │
│  │  │ WebGLRenderer│  │  OrthographicCamera    │  │  │
│  │  └──────┬──────┘  └────────────────────────┘  │  │
│  │         │                                     │  │
│  │  ┌──────▼──────────────────────────────────┐  │  │
│  │  │         ShaderMaterial                   │  │  │
│  │  │  ┌──────────┐  ┌─────────────────────┐  │  │  │
│  │  │  │  Vertex   │  │    Fragment Shader   │  │  │  │
│  │  │  │  Shader   │  │  ┌───────────────┐  │  │  │  │
│  │  │  │           │  │  │  Wave Layers   │  │  │  │  │
│  │  │  │           │  │  │  • Top         │  │  │  │  │
│  │  │  │           │  │  │  • Middle      │  │  │  │  │
│  │  │  │           │  │  │  • Bottom      │  │  │  │  │
│  │  │  │           │  │  └───────────────┘  │  │  │  │
│  │  │  └──────────┘  └─────────────────────┘  │  │  │
│  │  └─────────────────────────────────────────┘  │  │
│  │                                               │  │
│  │  Event Listeners                              │  │
│  │  • pointermove → cursor bend + parallax       │  │
│  │  • pointerleave → smooth influence fadeout     │  │
│  │  • ResizeObserver → responsive canvas resize   │  │
│  └───────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

### Rendering Pipeline

1. **Scene Setup** — A full-screen `PlaneGeometry(2, 2)` is created with an `OrthographicCamera`, filling the canvas with a single quad
2. **GLSL Fragment Shader** — The fragment shader calculates wave positions, applies sine-based oscillation, and renders anti-aliased glow lines
3. **Mouse Interaction** — Pointer events update uniform values with damped lerping for smooth cursor-following wave bends
4. **Parallax** — Cursor offset shifts the UV coordinate origin, creating a subtle depth illusion
5. **Gradient Coloring** — Up to 8 color stops are interpolated across each wave's line indices via GLSL `mix()`
6. **Animation Loop** — `requestAnimationFrame` drives the render loop; elapsed time is passed as a uniform for continuous animation

### Key Shader Uniforms

| Uniform | Type | Purpose |
|---|---|---|
| `iTime` | `float` | Elapsed time for animation |
| `iResolution` | `vec3` | Canvas pixel dimensions |
| `iMouse` | `vec2` | Current smoothed cursor position |
| `bendInfluence` | `float` | Smoothed 0→1 value for mouse influence fade-in/out |
| `lineGradient[8]` | `vec3[]` | Array of RGB color stops |
| `parallaxOffset` | `vec2` | Current smoothed parallax displacement |

---

## 🎨 Customization Examples

### Minimal — Single Wave

```jsx
<FloatingLines
  enabledWaves={["middle"]}
  lineCount={4}
  animationSpeed={0.5}
/>
```

### Neon Gradient

```jsx
<FloatingLines
  enabledWaves={["top", "middle", "bottom"]}
  lineCount={10}
  linesGradient={["#ff00ff", "#00ffff", "#ffff00"]}
  animationSpeed={1.5}
  interactive
/>
```

### Subtle Parallax Background

```jsx
<FloatingLines
  enabledWaves={["middle", "bottom"]}
  lineCount={[6, 8]}
  lineDistance={[3, 5]}
  parallax
  parallaxStrength={0.4}
  interactive={false}
  mixBlendMode="overlay"
/>
```

### High-Interactivity Hero Section

```jsx
<FloatingLines
  enabledWaves={["top", "middle", "bottom"]}
  lineCount={12}
  interactive
  bendRadius={3}
  bendStrength={-4}
  mouseDamping={0.08}
  linesGradient={["#e945f5", "#7c3aed", "#2563eb", "#06b6d4"]}
/>
```

---

## ⚡ Performance

| Aspect | Detail |
|---|---|
| **Rendering** | Entirely GPU-based via WebGL fragment shaders — no DOM manipulation per frame |
| **Pixel Ratio** | Capped at `2x` to balance visual quality and performance on high-DPI displays |
| **Resize** | Uses `ResizeObserver` (not `window.resize`) for accurate container-bound resizing |
| **Cleanup** | Full disposal of WebGL context, geometries, materials, and event listeners on component unmount |
| **Frame Budget** | Typically renders in under 2ms per frame on modern GPUs |

---

## 🌐 Browser Support

| Browser | Supported |
|---|---|
| Chrome 90+ | ✅ |
| Firefox 90+ | ✅ |
| Safari 15+ | ✅ |
| Edge 90+ | ✅ |
| Mobile Chrome/Safari | ✅ |

> **Note:** Requires WebGL 1.0+ support. Virtually all modern browsers and devices support this.

---

## 🤝 Contributing

Contributions are welcome! Here's how to get involved:

1. **Fork** the repository
2. **Create** a feature branch
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Commit** your changes with descriptive messages
   ```bash
   git commit -m "feat: add new wave animation mode"
   ```
4. **Push** to your branch
   ```bash
   git push origin feature/your-feature-name
   ```
5. **Open** a Pull Request against `main`

### Guidelines

- Follow existing code style and ESLint rules
- Test across multiple browsers before submitting
- Update documentation for any new or changed props

---

Built with ❤️ using React, Three.js & GLSL Shaders


