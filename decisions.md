# Design Decisions

- Entry mode: Surprise me
- Genre: Sci-Fi
- Director: Denis Villeneuve
- Film: Arrival (2016)
- Niche: LLM Wiki 教學報告 — 知識架構與編譯系統的技術教學指南
- Pages: Single page (homepage only)
- Major page roles: Report homepage — 8 章節的技術教學內容展示
- Image placeholders: None — all diagrams rendered with HTML/CSS
- Sub-agent delegation plan: Parallel research (completed), sequential build

## Why This Director × Film

Arrival 是一部關於**語言如何重塑認知**的電影。Louise Banks 透過學習外星語言，改變了自己理解時間和知識的方式。這與 LLM Wiki 的核心主張完全平行：

- **語言即結構**：Heptapod 的環形文字 = Wiki 的互相連結頁面
- **知識是編譯而非檢索**：Louise 不是查字典，她是逐步建構理解 = Ingest 不是索引，是編譯
- **霧中逐漸清晰**：電影的視覺語言從迷霧到清明 = 從 raw sources 到結構化 wiki
- **時間的非線性**：知識複利讓過去的理解影響未來的查詢

## Demo Uniqueness Audit

- Previous-work audit: No prior HTML demos exist in this project. First build.
- Recurring traits to avoid: N/A (first demo)
- Shell-ban list:
  - Generic SaaS hero (centered headline + subtitle + CTA button)
  - Left-copy right-mockup split hero
  - Standard three-column feature cards
  - Dark luxury palette with thin gold borders
  - Top horizontal nav with pill links
  - Repeating rounded card grids
- Primary composition family: **Corridor** — a vertical passage that narrows and deepens as the reader descends, mirroring both the shell's gravity-defying corridor in Arrival and the progressive depth of the teaching guide (overview → architecture → details → practice)
- Why this family differs from the most recent output: First demo; chosen to avoid the most common fallback (full-bleed stage or stacked framed panels)
- Wireframe-level uniqueness test: The corridor composition uses asymmetric margin shifts, fog-density gradients, and progressive reveal that would be structurally distinct even with neutral colors and default fonts

## Research Notes

### Research Boundary
- Film research is observational input, not a spec: Arrival's visual language is source material for atmosphere, rhythm, and emotional arc — not a UI kit
- What is being translated into web language: Fog diffusion, silhouette framing, scale juxtaposition (vast ↔ intimate), the circular logogram motif, and the stillness-to-revelation rhythm
- What must not be flattened into product-template logic: The film's sense of approaching the unknown — the page should feel like walking into the shell, not like browsing a documentation site

### Research Sources
- Director source: directors-200.md — "Extreme minimalism+immersion+colossal scale"
- Film source: Web research on Bradford Young's cinematography, production design
- Secondary analysis: Color palette extraction, rhythm/pacing pattern analysis
- Niche source 1: Stripe Docs — generous whitespace, monospaced code, restrained accent system
- Niche source 2: Linear — dark UI, high-contrast type, cinematic hero sections

### Film Palette
- Primary: Fog blue-grey #6B7D82 → #4A5859 (exterior, the unknown)
- Secondary: Warm amber #C4956A → #E8B87A (memory, knowledge already compiled)
- Accent: Shell white #E0E4E8 (revelation, the chamber of understanding)
- Shadow: Deep slate #1A1E22 (the void before knowledge)
- Text: Off-white #F0EDE8 (warm paper tone, human-readable)

### Director Signatures
1. **Scale juxtaposition**: Tiny figures against colossal shell → Massive typography headers against dense body text; monumental section openings that compress into intimate detail
2. **Fog as narrative device**: Atmosphere that obscures then reveals → CSS gradient fog layers that thin as the reader progresses deeper into the page
3. **Circular logogram motif**: The heptapod's ink-ring language → Circular/radial design elements for knowledge connections, cross-references, and the wiki's interconnected structure

### Film Translation Notes
- Framing: Silhouette-first — content blocks framed against lighter backgrounds, figures (diagrams) backlit by ambient glow
- Rhythm: Long stillness → brief revelation → emotional density. Sections alternate between spacious breathing room and compressed information
- Lighting: Top-light dominance (the shell corridor). Gradient light sources from above, content illuminated from top-center
- Space: Massive negative space in transitions between chapters, compressed density within content sections
- Materiality: Fog diffusion layers, matte surfaces (no gloss/glass), ink-on-paper texture for text areas
- What should stay ambiguous or restrained: No sharp borders or heavy dividers — sections dissolve into each other through fog gradients

### Niche References
- Stripe Docs: Whitespace discipline, monospaced code containers, two-color accent restraint
- Linear: Dark atmospheric hero, disciplined motion, content-density contrast

### Reference Decomposition
- Stripe contributes: Spacing rhythm, code block styling, information hierarchy
- Linear contributes: Dark atmospheric opening, type scale confidence, subtle motion
- Arrival contributes: Emotional arc, fog materiality, scale drama, circular motifs
- What will not be copied: Stripe's sidebar navigation, Linear's SaaS product framing, any generic documentation layout
