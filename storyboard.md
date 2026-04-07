# Director's Treatment

## Director Brief
- Visual thesis: Knowledge emerges from fog — the page begins in atmospheric obscurity and progressively clarifies as the reader descends, mirroring both Arrival's fog-to-revelation arc and the wiki's journey from raw sources to compiled understanding.
- Signature technique 1: **Scale juxtaposition** — Monumental type (120px+) for chapter titles dissolving into intimate 16px body text, like the shell towering over tiny humans then cutting to Louise's hands on the glass.
- Signature technique 2: **Fog as transition device** — CSS radial gradients and opacity layers that thin between sections, creating the sense of walking deeper into the shell corridor where understanding awaits.
- Signature technique 3: **Circular logogram motif** — Radial/ring design elements representing wiki interconnections. Not decorative — structural. Each ring element maps to a knowledge concept (entities, concepts, cross-references).
- Motion rules: Slow, deliberate. All transitions 0.8s–1.2s with cubic-bezier(0.22, 1, 0.36, 1). No bounce, no spring. Scroll-triggered reveals only — no autoplay animation. Reduced-motion: instant reveals, no transitions.
- Typography rules: Serif for monumental headings (authority, permanence — like carved stone). Sans-serif for body (clarity, precision). Monospace for technical terms and code references (the language of the system). Maximum 3 type families.

## Site Cinematic Grammar
- Page-shell logic: **Corridor** — a single vertical passage with asymmetric margins that subtly narrow as the reader descends, creating compression then release. No sidebar. No multi-column nav.
- Navigation posture: Minimal floating indicator — a thin vertical progress line on the left edge, no traditional nav bar. Chapter titles appear as waypoints along the progress line. The page IS the navigation.
- Framing discipline: Content blocks framed by fog-gradient boundaries, never hard lines. Sections dissolve into each other. The only hard edges are on technical diagrams (HTML/CSS rendered).
- Density cadence: Expansive (hero) → Dense (architecture) → Rhythmic (processes) → Compressed (evidence) → Breathing (history) → Intimate (invitation) → Vast (loop)
- Recurring material layers: Fog radial gradients (thinning as depth increases), grain texture overlay at 3% opacity, warm amber glow accents on interactive/hover states
- Allowed composition families: Corridor, monolith, void
- What may repeat: Fog gradients, grain overlay, monospace labels, ring motifs
- What must vary page to page: N/A (single page)
- Demo uniqueness guardrail: No horizontal split hero, no card grids, no pill navigation, no SaaS layout patterns

## Page Arc

### Page: Home (Single-page report)
- Page-role scene: The viewer walks into the alien shell — a long, fog-filled corridor where each step deeper reveals more of the knowledge system's architecture, until at the end they understand the entire language.
- Page scene thesis: A contemplative descent from mystery to mastery.
- One big idea: **The Corridor of Understanding** — the page itself is a physical metaphor for the wiki's compilation process. Raw fog at the top, crystallized knowledge at the bottom.
- Hero dominance statement: A single monumental question floats in deep fog, backlit by a distant warm glow — the viewer faces the unknown exactly as Louise faces the shell for the first time.
- Restraint statement: No decorative illustrations. No colorful icons. No card shadows. No gradient buttons. Fog and type do all the work. Effects are earned, not scattered.
- Material thesis: Matte dark surfaces (#0E1117) with warm amber bleed-through (#C4956A at low opacity). Fog layers provide depth without glass or gloss. Grain gives texture without pattern.
- Typography thesis: Monumental serif headings at 96-120px create the sense of carved inscriptions. The type itself has weight and presence — it doesn't need decoration. Body text in clean sans at 18px with generous line-height (1.75) for readability.
- Narrative arc: Villeneuve Variant A (Arrival — puzzle mode), adapted for 8-chapter content
- Hero archetype: #2 Atmosphere Bath — Tier 1 for Villeneuve. Full-bleed fog environment, text floating in atmospheric depth.
- Signature composition: The Corridor Descent — content width progressively narrows from 90% at the top to 65% at the deepest content sections, then opens back to 90% for the closing loop. This compression creates physical tension and focus.
- Grid fallback test: If reduced to a standard centered column, the progressive narrowing (the entire spatial metaphor) would be lost, along with the fog depth layers and the sense of physical passage.
- Shared system holdback: N/A (single page, no shared system needed)
- UI exposure guardrail: No director names, film titles, chapter labels like "Scene 1", or calibration tags in the final HTML. Section headings use the teaching guide's own chapter titles.
- What this page must not inherit from previous demos: N/A (first demo)

### Scene Sequence

#### Scene 1 — The Promise (Hero)
- Beat: B3 The Promise
- Function: Hero (#2 Atmosphere Bath)
- Archetype: Atmosphere Bath — full-bleed fog with floating question
- Composition: Full viewport, fog radial gradient from center-bottom (warm amber #C4956A at 15% opacity) bleeding into deep slate (#0E1117). A single large question: "如果 LLM 幫你維護知識庫？" at 96px serif. Below: one-sentence answer at 20px sans.
- Camera ref: camera-shots #1 Slow fade from black — content materializes over 1.5s
- Interaction ref: interaction-effects #35 Parallax micro-shift — fog layers shift subtly on scroll
- Visual elements: Gradient fog layer (#15), grain texture overlay (#18), single ring motif (logogram echo) as subtle background element
- Why this exists: The viewer faces the unknown. Like Louise's first encounter with the shell, the question hangs in fog.

#### Scene 2 — Architecture Deep Dive
- Beat: B10 Deep Dive
- Function: Scroll Story (#41) + Animated Infographic (#44)
- Archetype: Sticky visual with scrolling content
- Composition: Three-layer architecture diagram rendered as a vertical stack of three connected blocks (HTML/CSS), with the active layer highlighted in warm amber as the reader scrolls. Text explains each layer beside the diagram.
- Camera ref: camera-shots #4 Crane down — content descends into view as scroll progresses
- Interaction ref: interaction-effects #28 Sticky spotlight — diagram stays pinned while text scrolls
- Visual elements: CSS-rendered architecture diagram with glow on active layer, thin connecting lines between layers
- Why this exists: The core system revealed. Like the first glimpse inside the shell — the structure is alien but logical.

#### Scene 3 — The Process (Ingest Flow)
- Beat: B11 The Tutorial
- Function: Process/Steps (#8)
- Archetype: Numbered sequence with visual flow
- Composition: 6-step Ingest process rendered as a horizontal flow (on desktop) or vertical cascade (mobile). Each step is a compact block with step number, title, and one-line description. Active step pulses with warm amber border. CSS arrows connect steps.
- Camera ref: camera-shots #30 Tracking shot lateral — steps reveal left-to-right on scroll
- Interaction ref: interaction-effects #12 Underline slide — hover on step reveals expanded description
- Visual elements: CSS flow arrows, step number circles (ring motif callback), code-block for directory structure example
- Why this exists: The mechanism explained. Like Louise learning to write her first logogram — each stroke matters.

#### Scene 4 — The Pivot (Query & Lint)
- Beat: B14 The Pivot
- Function: Tabbed Content (#18) + Comparison (#10)
- Archetype: Split-view with tab switch
- Composition: Two modes presented as a visual split — left: Query flow (knowledge going out), right: Lint flow (health checking). Both rendered as compact flowcharts in CSS. A subtle divider made of thinning fog separates them. Below: "知識複利" concept highlighted in a pullquote.
- Camera ref: camera-shots #7 Split diopter — two sides reveal simultaneously
- Interaction ref: interaction-effects #48 Tab morph — click toggles between Query and Lint detail views
- Visual elements: Two CSS flowcharts, pullquote with oversized quotation mark, fog divider
- Why this exists: The tonal shift. The wiki is not just a container — it grows, it heals, it compounds.

#### Scene 5 — Evidence Wall (RAG vs Wiki)
- Beat: B8 Evidence Wall
- Function: Comparison Table (#10) + Stats (#24)
- Archetype: Confrontation comparison
- Composition: Full-width comparison table: RAG (left, desaturated fog blue) vs LLM Wiki (right, warm amber glow). 5 dimensions stacked vertically. Each row animates in sequence. Below: a single powerful stat or quote about why maintenance is the real problem.
- Camera ref: camera-shots #20 Jump cut stagger — rows appear in rapid sequence (0.1s apart)
- Interaction ref: none (intentional — Villeneuve's restraint. The data speaks without effects.)
- Visual elements: Comparison table with color-coded columns, stat counter, Memex reference quote
- Why this exists: The evidence. Like the moment Louise proves the logograms are not linear — the data makes the case.

#### Scene 6 — Flashback (Toolchain & History)
- Beat: B13 Flashback
- Function: Category Map (#15) + Timeline (#7)
- Archetype: Tool ecosystem as constellation
- Composition: Tool diagram rendered as interconnected nodes (Obsidian at center, Git, LLM Agent, qmd as satellites). Nodes connected by thin lines with labels. Warm amber for core tools, muted for optional. Below: Memex (1945) → LLM Wiki timeline with 3 milestone points.
- Camera ref: camera-shots #8 Dolly zoom — nodes expand outward from center on scroll
- Interaction ref: interaction-effects #3 Color temperature shift — hover warms a node's connections
- Visual elements: CSS node diagram, timeline with 3 points, connecting lines
- Why this exists: Context. Where this idea came from. Like the memory flashes in Arrival — the past informs the present.

#### Scene 7 — The Invitation (Getting Started)
- Beat: B20 The Invitation
- Function: Process/Steps (#8) + Lead Magnet (#33)
- Archetype: Gentle step-by-step
- Composition: 5 steps to begin, presented as a compact vertical list with step numbers. Each step has a short title and one sentence. The visual density is much lighter than previous sections — generous whitespace, larger margins. The corridor opens back up.
- Camera ref: camera-shots #2 Fade from black — each step fades in gently
- Interaction ref: interaction-effects #38 Magnetic label — step numbers slightly attract the cursor
- Visual elements: Step numbers as ring elements (logogram callback), directory tree rendered as code block
- Why this exists: The gentle invitation. Not a CTA — an outstretched hand. "你是策展人，不是作者。"

#### Scene 8 — The Loop (Circular Close)
- Beat: B24 The Loop
- Function: Quote (#40) + Visual Break (#39)
- Archetype: Echo of the hero
- Composition: The same fog gradient from the hero section returns, but now the warm amber is dominant — the fog has cleared. A single circular logogram element (larger, more defined than the hero's version) contains the wiki's core principle: "Wiki 是持久化的編譯產物，不是即時的檢索結果。" The ring is complete.
- Camera ref: camera-shots #1 Slow fade — the quote materializes like the hero, but warmer
- Interaction ref: none (intentional silence — the film ends)
- Visual elements: Large ring element (#7 Floating Circle variant), fog gradient (inverted warmth), grain overlay
- Why this exists: Circular closure. Like Arrival's ending connecting to its beginning — understanding is complete, and the viewer realizes they knew the answer all along.

#### Scene 9 — The Farewell (Footer)
- Beat: B22 The Farewell
- Function: Footer (#48)
- Archetype: Minimal farewell
- Composition: Extremely minimal. Project title in small type, a single thin line, copyright or attribution. The fog dissolves to pure black. Credits-like silence.
- Camera ref: camera-shots #2 Fade from black (reversed — fade to black)
- Interaction ref: none
- Visual elements: Thin horizontal rule (#26), small type
- Why this exists: The end credits. Respect the ending.

## Prestige Calibration Review

1. What is the one thing the viewer remembers after 3 seconds? — The monumental question floating in fog, backlit by amber.
2. What is intentionally absent? — Card grids, decorative icons, gradient buttons, sidebar navigation, colorful badges, bouncy animations.
3. Which detail makes the page feel expensive rather than just decorative? — The progressive corridor narrowing. It's a spatial experience, not a visual treatment.
4. If you removed 30% of the effects, would the page become stronger? — Yes, and we already did. Only Scene 1 and Scene 6 have notable interactions. The rest are intentionally restrained.
5. Does this page feel like its own scene in the same film? — It IS the film. One continuous corridor.
6. Would the page still feel directed if palette and typography were stripped back to neutral values? — Yes. The corridor narrowing, fog-density progression, and section rhythm would still create a directed experience.
7. If this page were turned into a generic grid, what essential idea would break? — The entire spatial metaphor. The corridor IS the concept.
8. Does the page read like a standalone poster before shared design is added? — Yes. Single page, no shared system needed.
9. If styling were stripped away, would this still look too much like a previous demo? — N/A, first demo.
