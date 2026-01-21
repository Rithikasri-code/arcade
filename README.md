<p align="center">
  <img src="assets/banner.svg" alt="Arcade Engine Banner" width="100%" />
</p>

<p align="center">
  <a href="https://github.com/Rithikasri-code/arcade"><img src="https://img.shields.io/badge/Engine-HTML5%20Canvas-facc15?style=flat-square&logo=html5&logoColor=black&labelColor=1e1136" alt="HTML5 Canvas" /></a>
  <img src="https://img.shields.io/badge/Standard-JavaScript%20ES6%2B-facc15?style=flat-square&logo=javascript&logoColor=black&labelColor=1e1136" alt="JavaScript" />
  <img src="https://img.shields.io/badge/Architecture-Fixed%20Step%2060FPS-c084fc?style=flat-square&labelColor=1e1136" alt="60 FPS" />
  <img src="https://img.shields.io/badge/Physics-2D%20Tilemap%20Collision-c084fc?style=flat-square&labelColor=1e1136" alt="Tilemap Collision" />
  <img src="https://img.shields.io/badge/Dependencies-Zero-green?style=flat-square&labelColor=1e1136" alt="Zero Dependencies" />
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square&labelColor=1e1136" alt="MIT License" /></a>
</p>

---

## 🕹️ Overview

**Arcade** is a lightweight, zero-dependency 2D arcade game engine and interactive simulation laboratory implemented directly in vanilla JavaScript and HTML5 Canvas.

Designed to demonstrate core computer graphics and game engineering principles without heavy frameworks, the repository features deterministic fixed-timestep game loops, 2D tilemap collision matrices, procedural sprite rendering, and autonomous enemy patrol AI.

---

## 🏗️ Engine Architecture

```mermaid
flowchart TD
    subgraph InputSubsystem["🎮 Input Subsystem"]
        Keys["Keyboard Event Buffer\n(Arrow Keys / WASD Buffer)"]
        NextDir["Buffered Heading Register\n(nextDx, nextDy)"]
    end

    subgraph SimulationLoop["⚙️ Deterministic 60 FPS Loop"]
        Tick["Fixed Timestep Clock\n(8-Tick Movement Quantization)"]
        Collision["Tile Matrix Evaluator\n(canMove(x, y) 22x22 Grid)"]
        GhostAI["Autonomous Ghost Agent\n(Random Heading / Intersection Branching)"]
        State["State Manager\n(Pellet Consumption, Lives, Score HUD)"]
    end

    subgraph RenderEngine["🎨 2D Canvas Rasterizer"]
        MazeDraw["Tilemap Wall Renderer\n(Stroke Rect & Palette)"]
        PelletDraw["Dot & Energizer Particle Draw"]
        SpriteDraw["Dynamic Vector Sprites\n(Mouth Arc Rotation & Ghost Eyes)"]
    end

    InputSubsystem --> NextDir
    NextDir --> Collision
    Tick --> Collision
    Collision --> GhostAI
    GhostAI --> State
    State --> RenderEngine
```

---

## ⚡ Technical Highlights

* **Deterministic Grid-Based Collision:** Movement operates on a 22×22 discrete integer tilemap matrix where entity bounding circles are clamped to coordinate axes, eliminating clipping through corners.
* **Heading Buffering (`nextDx`, `nextDy`):** Replicates genuine arcade responsiveness by caching directional inputs before corridor intersections, turning automatically the exact moment a turn opens.
* **Autonomous Enemy Agents:** Patrolling ghosts assess non-reversing valid neighbor tiles at intersections, creating fluid, non-blocking path exploration.
* **Procedural Vector Drawing:** Zero external raster images required for core mechanics. Pacman's animated mouth angles, pellet energizers, and ghost eyes are calculated using pure Canvas trigonometry.

---

## 📂 Laboratory Modules

* **`index.html`** — Self-contained, responsive browser arcade cabinet with CRT HUD styling, scoring, and lives tracking.
* **`Pacman/`** — In-depth map architecture definitions (`map-dir.xlsx`), comprehensive engine specifications (`PensPlace Pacman-doc.md`), and screen manifest hierarchies.
* **`Lava Lamp/`** — Procedural metaball and ambient liquid simulation demonstrating dynamic canvas particle physics.

---

## 🚀 Running the Arcade

No build tools, bundlers, or package managers are required.

### Instant Play
Simply open [`index.html`](index.html) in any modern web browser:
```bash
# Or serve locally using Python:
python -m http.server 3000
```
Navigate to `http://localhost:3000` to play.

### Controls
* **Steer:** `Arrow Keys` or `W`, `A`, `S`, `D`
* **Objective:** Clear all yellow pellets while evading ghost patrols.

---

## 📄 License

Distributed under the **MIT License**. See [LICENSE](LICENSE) for details.
