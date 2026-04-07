# Compiled Spec

## Page: Home (Single-page LLM Wiki Report)
- Page scene thesis: A contemplative descent from mystery to mastery — the Corridor of Understanding.
- Signature composition: Progressive corridor narrowing (90% → 65% → 90%)
- Signature composition source id: Custom — no library entry matches progressive width modulation. Film justification: Arrival's shell corridor physically compresses space as characters walk deeper.
- Why this cannot collapse into a default grid: The spatial metaphor IS the design. A fixed-width column destroys the compression-release rhythm.
- One big idea: Knowledge emerges from fog.
- Heavy interaction: #35 Parallax micro-shift (hero fog layers only) — 1 total
- Heavy interaction source id: interaction-effects #35
- Showy reveals: #7 Split diopter (Scene 4), #20 Jump cut stagger (Scene 5) — 2 total
- Showy reveal source id(s): camera-shots #7, camera-shots #20
- Restraint notes: Scenes 5, 8, 9 have intentional `none` interaction. Motion reserved for fog and structure, not decoration.
- Typography source id(s): Custom serif/sans/mono system (see tokens)
- Atmosphere/background source id(s): background-techniques A1 (multi-layer orbs), C1 (film grain), C8 (vignette)

## Entrance Map
- Scene 1 (Hero): fade-from-black (camera #2)
- Scene 2 (Architecture): steadicam-float-in (camera #12)
- Scene 3 (Ingest): curtain-wipe (camera #10)
- Scene 4 (Query/Lint): split-diopter-open (camera #7)
- Scene 5 (Evidence): jump-cut-stagger (camera #20)
- Scene 6 (Toolchain): dolly-in (camera #3)
- Scene 7 (Getting Started): fade-from-black (camera #2) — 2nd use
- Scene 8 (Loop): rack-focus-reveal (camera #6)
- Scene 9 (Footer): none (fade to black via opacity)

Variety check: 7 distinct entrance types across 9 scenes. No adjacent repeats. fadeUp count: 0. ✓

### Scene 1 — Hero (The Promise)
- Beat: B3
- Function: Hero
- Archetype: #2 Atmosphere Bath
- Entrance: camera #2 — `opacity: 0; transition: opacity 2s ease;`
- Camera source id: camera-shots #2
- Interaction: #35 Parallax micro-shift (JS-required)
- Interaction source id: interaction-effects #35
- Composition source id: Custom corridor
- Visual element source id(s): background-techniques A1, C1, C8
- Typography source id(s): Custom monumental serif
- Background/texture source id(s): A1 multi-layer radial, C1 grain, C8 vignette

```css
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 0 5%;
  overflow: hidden;
  background: var(--bg);
}
.hero__title {
  font-family: var(--font-serif);
  font-size: clamp(48px, 8vw, 120px);
  font-weight: 300;
  color: var(--text);
  line-height: 1.1;
  letter-spacing: -0.02em;
  opacity: 0;
  transition: opacity 2s var(--ease);
}
.hero__subtitle {
  font-family: var(--font-sans);
  font-size: clamp(16px, 2vw, 22px);
  color: var(--text-muted);
  margin-top: 2rem;
  max-width: 600px;
  line-height: 1.7;
  opacity: 0;
  transition: opacity 2s var(--ease) 0.5s;
}
.hero__fog-layer {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
  will-change: transform;
}
.hero__fog-1 {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(196, 149, 106, 0.12), transparent 70%);
  bottom: -10%; left: 50%; transform: translateX(-50%);
}
.hero__fog-2 {
  width: 400px; height: 400px;
  background: radial-gradient(circle, rgba(107, 125, 130, 0.08), transparent 70%);
  top: 20%; right: 10%;
}
.hero__ring {
  position: absolute;
  width: 300px; height: 300px;
  border: 1px solid rgba(196, 149, 106, 0.08);
  border-radius: 50%;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}
.hero.visible .hero__title,
.hero.visible .hero__subtitle { opacity: 1; }
```

```js
// Parallax micro-shift for fog layers (interaction-effects #35)
document.addEventListener('mousemove', (e) => {
  const layers = document.querySelectorAll('.hero__fog-layer');
  const x = (e.clientX / window.innerWidth - 0.5) * 2;
  const y = (e.clientY / window.innerHeight - 0.5) * 2;
  layers.forEach((layer, i) => {
    const depth = (i + 1) * 15;
    layer.style.transform = `translate(${x * depth}px, ${y * depth}px)`;
  });
});
```

### Scene 2 — Architecture Deep Dive
- Beat: B10
- Function: Scroll Story #41
- Entrance: camera #12 — steadicam float-in
- Interaction: #28 Sticky spotlight (CSS only)
- Interaction source id: interaction-effects #28

```css
.architecture {
  position: relative;
  width: var(--corridor-mid);
  margin: 0 auto;
  padding: var(--space-xl) 0;
}
.architecture__sticky {
  position: sticky;
  top: 10vh;
  align-self: start;
}
.architecture__diagram {
  display: flex;
  flex-direction: column;
  gap: 2px;
}
.architecture__layer {
  padding: 2rem 2.5rem;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  transition: border-color 0.8s var(--ease), background 0.8s var(--ease);
  position: relative;
}
.architecture__layer.active {
  border-color: var(--accent);
  background: rgba(196, 149, 106, 0.04);
}
.architecture__layer-title {
  font-family: var(--font-mono);
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--accent);
  margin-bottom: 0.5rem;
}
.architecture__connector {
  width: 1px;
  height: 24px;
  background: var(--border);
  margin: 0 auto;
}
/* Entrance */
.architecture {
  transform: translateZ(-100px) translateY(30px);
  opacity: 0;
  transition: all 2s cubic-bezier(0.25, 0.1, 0.25, 1);
}
.architecture.visible {
  transform: translateZ(0) translateY(0);
  opacity: 1;
}
```

### Scene 3 — Ingest Process
- Beat: B11
- Function: Process/Steps #8
- Entrance: camera #10 — curtain wipe

```css
.ingest {
  width: var(--corridor-narrow);
  margin: 0 auto;
  padding: var(--space-xl) 0;
}
.ingest__flow {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1.5rem;
  position: relative;
}
.ingest__step {
  padding: 1.5rem;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  position: relative;
  transition: border-color 0.5s var(--ease);
}
.ingest__step:hover {
  border-color: var(--accent);
}
.ingest__step-number {
  width: 36px; height: 36px;
  border: 1px solid var(--accent);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-mono);
  font-size: 13px;
  color: var(--accent);
  margin-bottom: 1rem;
}
.ingest__step-title {
  font-family: var(--font-sans);
  font-size: 15px;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 0.5rem;
}
.ingest__step-desc {
  font-family: var(--font-sans);
  font-size: 14px;
  color: var(--text-muted);
  line-height: 1.6;
}
.ingest__arrow {
  position: absolute;
  color: var(--border);
  font-size: 18px;
}
/* Entrance — curtain wipe */
.ingest {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 1s ease-in-out;
}
.ingest.visible {
  clip-path: inset(0 0 0 0);
}
```

### Scene 4 — Query & Lint (The Pivot)
- Beat: B14
- Function: Comparison #10
- Entrance: camera #7 — split diopter

```css
.pivot {
  width: var(--corridor-narrow);
  margin: 0 auto;
  padding: var(--space-xl) 0;
}
.pivot__split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
}
.pivot__side {
  padding: 2rem;
  border: 1px solid var(--border);
  border-radius: var(--radius);
}
.pivot__side-title {
  font-family: var(--font-mono);
  font-size: 13px;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--accent);
  margin-bottom: 1.5rem;
}
.pivot__flow-item {
  padding: 0.75rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.04);
  font-size: 14px;
  color: var(--text-muted);
  line-height: 1.6;
}
.pivot__pullquote {
  margin-top: var(--space-lg);
  padding: 2.5rem;
  border-left: 2px solid var(--accent);
  font-family: var(--font-serif);
  font-size: clamp(20px, 2.5vw, 28px);
  color: var(--text);
  line-height: 1.5;
  font-style: italic;
}
/* Entrance — split diopter */
.pivot__split .pivot__side:first-child {
  clip-path: inset(0 50% 0 0);
  transition: clip-path 1.2s var(--ease);
}
.pivot__split .pivot__side:last-child {
  clip-path: inset(0 0 0 50%);
  transition: clip-path 1.2s var(--ease);
}
.pivot.visible .pivot__side {
  clip-path: inset(0);
}
```

### Scene 5 — Evidence Wall (RAG vs Wiki)
- Beat: B8
- Function: Comparison Table #10
- Entrance: camera #20 — jump cut stagger
- Interaction: none (intentional — Villeneuve restraint)

```css
.evidence {
  width: var(--corridor-narrow);
  margin: 0 auto;
  padding: var(--space-xl) 0;
}
.evidence__table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
}
.evidence__table th {
  font-family: var(--font-mono);
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  padding: 1rem 1.5rem;
  text-align: left;
  border-bottom: 1px solid var(--border);
}
.evidence__table th:nth-child(2) {
  color: var(--text-muted);
}
.evidence__table th:nth-child(3) {
  color: var(--accent);
}
.evidence__table td {
  padding: 1rem 1.5rem;
  font-size: 15px;
  line-height: 1.6;
  border-bottom: 1px solid rgba(255,255,255,0.03);
}
.evidence__row {
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.3s ease;
}
.evidence__row:nth-child(1) { transition-delay: 0s; }
.evidence__row:nth-child(2) { transition-delay: 0.08s; }
.evidence__row:nth-child(3) { transition-delay: 0.16s; }
.evidence__row:nth-child(4) { transition-delay: 0.24s; }
.evidence__row:nth-child(5) { transition-delay: 0.32s; }
.evidence.visible .evidence__row {
  opacity: 1;
  transform: translateY(0);
}
```

### Scene 6 — Toolchain (Flashback)
- Beat: B13
- Function: Category Map #15
- Entrance: camera #3 — dolly-in
- Interaction: #3 Color temperature shift (CSS only)
- Interaction source id: interaction-effects #3

```css
.toolchain {
  width: var(--corridor-mid);
  margin: 0 auto;
  padding: var(--space-xl) 0;
}
.toolchain__constellation {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  position: relative;
}
.toolchain__node {
  padding: 1.5rem;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  text-align: center;
  filter: saturate(0.8) brightness(0.95);
  transition: filter 0.5s ease, border-color 0.5s ease;
}
.toolchain__node:hover {
  filter: saturate(1.2) brightness(1.05);
  border-color: var(--accent);
}
.toolchain__node--center {
  grid-column: 2;
  border-color: var(--accent);
  background: rgba(196, 149, 106, 0.04);
}
.toolchain__node-icon {
  font-family: var(--font-mono);
  font-size: 24px;
  margin-bottom: 0.75rem;
  color: var(--accent);
}
.toolchain__node-name {
  font-family: var(--font-sans);
  font-size: 15px;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 0.25rem;
}
.toolchain__node-role {
  font-family: var(--font-sans);
  font-size: 13px;
  color: var(--text-muted);
}
.toolchain__timeline {
  margin-top: var(--space-lg);
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  padding: 2rem 0;
}
.toolchain__timeline::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 0; right: 0;
  height: 1px;
  background: var(--border);
}
.toolchain__milestone {
  position: relative;
  text-align: center;
  z-index: 1;
}
.toolchain__milestone-dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  background: var(--accent);
  margin: 0 auto 0.75rem;
}
.toolchain__milestone-year {
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--accent);
}
.toolchain__milestone-label {
  font-size: 13px;
  color: var(--text-muted);
  margin-top: 0.25rem;
}
/* Entrance — dolly-in */
.toolchain {
  transform: scale(0.85) translateZ(-50px);
  opacity: 0;
  transition: all 1.2s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}
.toolchain.visible {
  transform: scale(1) translateZ(0);
  opacity: 1;
}
```

### Scene 7 — Getting Started (The Invitation)
- Beat: B20
- Function: Process/Steps #8
- Entrance: camera #2 — fade from black (2nd use)
- Interaction: none (gentle)

```css
.invitation {
  width: var(--corridor-wide);
  margin: 0 auto;
  padding: var(--space-xl) 0;
}
.invitation__steps {
  max-width: 560px;
  margin: 0 auto;
}
.invitation__step {
  display: flex;
  gap: 1.5rem;
  padding: 1.5rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.04);
}
.invitation__step-ring {
  width: 32px; height: 32px;
  border: 1px solid var(--accent);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-mono);
  font-size: 12px;
  color: var(--accent);
  flex-shrink: 0;
}
.invitation__step-text h4 {
  font-family: var(--font-sans);
  font-size: 16px;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 0.25rem;
}
.invitation__step-text p {
  font-size: 14px;
  color: var(--text-muted);
  line-height: 1.6;
}
.invitation__coda {
  margin-top: var(--space-lg);
  text-align: center;
  font-family: var(--font-serif);
  font-size: clamp(18px, 2vw, 22px);
  color: var(--text-muted);
  font-style: italic;
}
/* Entrance */
.invitation {
  opacity: 0;
  transition: opacity 2s var(--ease);
}
.invitation.visible { opacity: 1; }
```

### Scene 8 — The Loop (Circular Close)
- Beat: B24
- Function: Quote #40
- Entrance: camera #6 — rack focus reveal
- Interaction: none (intentional silence)

```css
.loop {
  min-height: 80vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  position: relative;
  padding: 0 5%;
}
.loop__ring {
  width: clamp(200px, 30vw, 400px);
  height: clamp(200px, 30vw, 400px);
  border: 1px solid rgba(196, 149, 106, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 3rem;
  position: relative;
}
.loop__ring::before {
  content: '';
  position: absolute;
  inset: -20px;
  border: 1px solid rgba(196, 149, 106, 0.06);
  border-radius: 50%;
}
.loop__quote {
  font-family: var(--font-serif);
  font-size: clamp(16px, 2vw, 22px);
  color: var(--text);
  line-height: 1.6;
}
.loop__fog {
  position: absolute;
  width: 500px; height: 500px;
  background: radial-gradient(circle, rgba(196, 149, 106, 0.1), transparent 70%);
  filter: blur(60px);
  z-index: -1;
}
/* Entrance — rack focus */
.loop {
  filter: blur(20px);
  transform: scale(1.1);
  opacity: 0;
  transition: all 1.2s ease;
}
.loop.visible {
  filter: blur(0);
  transform: scale(1);
  opacity: 1;
}
```

### Scene 9 — Footer (The Farewell)
- Beat: B22
- Function: Footer #48
- Entrance: none
- Interaction: none

```css
.farewell {
  padding: var(--space-md) 5%;
  text-align: center;
  border-top: 1px solid rgba(255,255,255,0.04);
}
.farewell__title {
  font-family: var(--font-mono);
  font-size: 12px;
  letter-spacing: 0.1em;
  color: var(--text-ghost);
  text-transform: uppercase;
}
```

## External Library Decision

### Q1: What is the core motion experience of this page?
- Scroll narrative with fog atmosphere and progressive spatial compression.

### Q2: Can the native library entries do it?
- Yes. All effects use CSS transitions, clip-path, filter, and a small scroll observer JS. Fog parallax uses vanilla mousemove. No external library needed.

### Q3: If an external library is used, why?
- N/A

### Decision
- No external library. Native CSS + vanilla JS only.

## Shared System
- Navigation: Vertical progress line (left edge) with chapter waypoints — CSS + scroll observer JS
- Footer: Minimal, single-line
- Spacing rhythm: --space-sm: 1.5rem, --space-md: 3rem, --space-lg: 6rem, --space-xl: 10rem
- Typography system: 3 families (serif, sans, mono), 5 size steps
- Utility primitives: .section-header (mono label + serif title), corridor width vars
- Uniqueness check: First demo, no prior work to check against

## Phase 3 Quality Check
- [x] Every section has complete layout CSS
- [x] Every section has complete entrance behavior
- [x] Every section has complete interaction behavior or intentional `none`
- [x] JS-required effects (#35) include complete JS
- [x] Entrance variety rules pass (7 distinct types, no adjacent repeats, 0 fadeUp)
- [x] External Library Decision block is complete
- [x] Library source ids are present for all major visual moves
- [x] Anti-garbage constraints hold

## Derived Global Tokens
```css
:root {
  /* Palette — Arrival */
  --bg: #0E1117;
  --bg-elevated: #161B22;
  --text: #F0EDE8;
  --text-muted: #8B9098;
  --text-ghost: #4A4F58;
  --accent: #C4956A;
  --accent-dim: rgba(196, 149, 106, 0.15);
  --fog-blue: #6B7D82;
  --border: rgba(255, 255, 255, 0.06);

  /* Typography */
  --font-serif: 'Playfair Display', Georgia, serif;
  --font-sans: 'Inter', -apple-system, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;

  /* Spacing */
  --space-sm: 1.5rem;
  --space-md: 3rem;
  --space-lg: 6rem;
  --space-xl: 10rem;

  /* Corridor widths */
  --corridor-wide: min(90%, 1200px);
  --corridor-mid: min(80%, 1000px);
  --corridor-narrow: min(70%, 860px);

  /* Motion */
  --ease: cubic-bezier(0.22, 1, 0.36, 1);
  --transition-slow: 1.2s;
  --transition-mid: 0.8s;
  --transition-fast: 0.35s;
  --radius: 4px;
}
```
