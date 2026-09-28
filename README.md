# 💖 Love Animation — Interactive Web Motion Graphics

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![mo.js](https://img.shields.io/badge/mo.js-Motion_Graphics-FF4081?style=for-the-badge)](https://mojs.github.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

A high-performance, interactive motion graphics animation built for web showcases and social media content creation (Reels / Shorts). The project features dynamic SVG path manipulation, custom motion timelines, particle burst dynamics, and browser-compliant Web Audio API sound synthesis.

---

## ✨ Features

- 🎭 **Custom SVG Vector Path Manipulation**: Precision typography rendering with SVG paths for smooth letter-by-letter compression and transform sequences.
- 🎆 **Particle Physics & Bursts**: Multi-layer geometric particle bursts (`mojs.Burst`) triggered dynamically during kinetic collisions.
- 💓 **Custom Motion Shapes**: Custom SVG heart shape geometry extended directly via `mojs.CustomShape`.
- 🔊 **Zero-Dependency Web Audio Synthesis**: Embedded Web Audio API engine providing instant, zero-latency pop sound effects without external audio file dependencies.
- 🌐 **Modern Autoplay Policy Compliance**: Automatic AudioContext initialization bound to user gestures (`pointermove`, `click`, `touchstart`, `keydown`).
- 📐 **Resolution Independent & Responsive**: Scalable SVG vector layout with CSS transform scaling.

---

## 🛠️ Tech Stack

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Markup** | HTML5 / SVG | Vector graphics container (`<svg viewBox="0 0 500 200">`) |
| **Styling** | CSS3 | Modern Flexbox layout, CSS variables & transform scaling |
| **Animation Engine** | [mo.js v0.288](https://mojs.github.io/) | Motion graphics library for web timelines & shape dynamics |
| **Sound Engine** | Web Audio API | Low-latency real-time sine-wave frequency ramps (`AudioContext`) |

---

## 📁 Project Structure

```bash
I Love You Animation/
├── index.html        # Main entry point & SVG path definitions
├── style.css         # Responsive layout, flexbox centering & vector styles
├── script.js         # Core animation timeline, custom shape & audio engine
├── LICENSE           # MIT License
├── .gitignore        # Git ignore specifications
└── README.md         # Project documentation
```

---

## 🚀 Quick Start

### Option 1: Direct Local Execution
1. Clone or download the repository to your local machine:
   ```bash
   git clone https://github.com/saklincodes/I-Love-You-Animation.git
   ```
2. Open `index.html` in any modern web browser.

### Option 2: Live Server (VS Code)
1. Open the project folder in **Visual Studio Code**.
2. Install the **Live Server** extension (if not already installed).
3. Right-click `index.html` and select **"Open with Live Server"**.

---

## ⚙️ How It Works (Animation Architecture)

### 1. Custom Heart Shape Extension
The heart shape is procedurally registered to `mo.js` by extending `mojs.CustomShape`:
```javascript
class Heart extends mojs.CustomShape {
  getShape() {
    return '<path d="M50,88.9C25.5,78.2,0.5,54.4,3.8,31.1S41.3,1.8,50,29.9c8.7-28.2,42.8-22.2,46.2,1.2S74.5,78.2,50,88.9z"/>';
  }
  getLength() { return 200; }
}
mojs.addShape("heart", Heart);
```

### 2. Timeline Coordination & Interpolation
The main animation sequence is orchestrated via `mojs.Timeline()`, synchronizing:
- Parallel movement of left and right bounding lines (`line--left` and `line--rght`).
- Sequential opacity fading and keyframe transforms on individual letter paths.
- Particle burst execution at precise collision timings (`crtBoom()`).
- Replay looping scheduled every `4300ms`.

### 3. Web Audio API Sound Generation
To comply with modern browser autoplay policies and ensure offline availability, audio is synthesized dynamically:
```javascript
const playSynthPop = (freq = 400) => {
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.type = "sine";
  osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
  osc.frequency.exponentialRampToValueAtTime(freq * 1.8, audioCtx.currentTime + 0.08);
  gain.gain.setValueAtTime(0.35, audioCtx.currentTime);
  gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.08);
  osc.connect(gain);
  gain.connect(audioCtx.destination);
  osc.start();
  osc.stop(audioCtx.currentTime + 0.08);
};
```

---

## 🎨 Customization

- **Adjust Canvas Scale**: Modify `transform: scale(1.45);` inside `style.css` under `.container` to scale the animation bounds up or down.
- **Change Primary Colors**: Update `colTxt` (`#763c8c`) and `colHeart` (`#fa4843`) in `script.js` or stroke/fill properties in `style.css`.
- **Modify Loop Delay**: Change the `setInterval` delay in `script.js` (default: `4300ms`).

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

<p align="center">Crafted with ❤️ for Web Motion Enthusiasts</p>
