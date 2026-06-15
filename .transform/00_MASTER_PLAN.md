# Gemmra-Web: Complete Transformation Plan

> **Purpose:** Step-by-step guide for transforming gitsetu-web → gemmra-web.
> Designed so a smaller LLM can execute each sub-phase independently.
> Each sub-phase is self-contained, verified, and committed before moving on.
>
> **Source:** GitSetu website (Astro + custom CSS, 9.5/10 design quality)
> **Target:** Gemmra — Nidāna for Pharmacovigilance (drug safety AI landing page)

---

## Architecture Overview

```
gemmra-web/
├── astro.config.mjs          ← Site config (URL, build settings)
├── package.json               ← Dependencies (Astro, xterm)
├── src/
│   ├── pages/index.astro      ← Page composition (imports components)
│   ├── layouts/Layout.astro   ← HTML shell (head, meta, fonts, scripts)
│   ├── styles/global.css      ← Design tokens (CSS variables, colors, fonts)
│   └── components/            ← Self-contained .astro components
│       ├── Navbar.astro       ← Sticky header with nav links
│       ├── Hero.astro         ← Two-column hero + terminal demo
│       ├── VisualCapabilities.astro ← Feature cards (visualizing zero-trust)
│       ├── CodeCompare.astro  ← Side-by-side "Old Way vs GitSetu Way"
│       ├── BentoGrid.astro    ← Architecture features grid (6 cards)
│       ├── Comparison.astro   ← Competitor comparison table
│       ├── Philosophy.astro   ← Sanskrit meaning + design philosophy
│       ├── Roadmap.astro      ← Future vision (3 phases)
│       ├── Cta.astro          ← Call-to-action section
│       ├── Footer.astro       ← Footer links
│       ├── TerminalDemo.astro ← Interactive terminal (xterm.js)
│       └── CommandPalette.astro ← Ctrl+K search modal
├── public/                    ← Static assets (favicon, logo, OG image)
├── scripts/                   ← Build scripts (doc sync — DELETE)
└── docs/                      ← Build prompts (DELETE)
```

### Key Astro Concepts for the Implementing LLM
- `.astro` files = HTML templates with a `---` frontmatter block (JS) at top
- Each component has its own `<style>` block (scoped CSS)
- `<script>` tags in `.astro` run client-side JS
- `astro dev` starts the dev server at localhost:4321
- `astro build` creates static HTML in `dist/`

---

## Gemmra Content Reference (Numbers to Use)

| Key | Value | Use In |
|-----|-------|--------|
| Name | **Gemmra** | Hero heading, navbar, footer |
| Tagline | **Nidāna for Pharmacovigilance** | Hero subtitle |
| Model | Gemma 4 31B + bf16 LoRA r=64 | Architecture section |
| Composite Score | **0.862** | Hero counter, results table |
| T1 Seriousness | **0.995 F1** | Results table |
| T2 MedDRA Coding | **0.667** | Results table |
| T3 Labelling | **0.801 F1** | Results table |
| T4 Causality | **0.986** | Results table |
| Format Compliance | **100%** | Hero counter |
| Training Data | **28,265** pairs | Architecture section |
| Eval Data | **3,560** samples | Results table |
| Training Time | **~2 hours** | Architecture section |
| Hardware | AMD MI300X (192 GB HBM3) | AMD section |
| Cost Reduction | **4,000×** | Impact section |
| Speed Increase | **360×** (30 min → 5 sec) | Hero, impact |
| FAERS Coverage | 29 quarters (2019Q1-2026Q1) | Data pipeline section |
| Nidāna meaning | "In Ayurveda, Nidāna (निदान) is the systematic investigation of disease causation" | Philosophy section |
| Origin story | "We found it funny calling our solution Gemmra, and the name stuck." | Hero or philosophy |
| Hackathon | TCS & AMD AI Hackathon 2026 | Footer, hero badge |
| Website | gemmra.bhaskarjha.dev | Config, footer |
| GitHub | github.com/00bjxx/PharmaReview-AI | Footer, CTA |
| HuggingFace | bhaskarjha/gemmra-31b-lora | CTA |

---

## Color Palette Change

The GitSetu teal/blue accent works well but should shift slightly to a medical/pharma tone.

**Option A (Recommended): Keep teal — it reads as "medical technology"**
- Teal (#00c4cc) already feels medical/clinical
- Just change the comment from "GitSetu Teal" → "Gemmra Teal"
- Add AMD Red as a secondary accent: #ED1C24

**Option B: Shift to blue/purple (pharma feel)**
- Primary: #3B82F6 (blue)
- Secondary: #8B5CF6 (purple)
- This is more work for minimal gain

→ **Go with Option A. Keep the teal, add AMD Red.**

---

## Sub-Phase Execution Plan

### Sub-Phase 0: Cleanup & Config
### Sub-Phase 1: Global Branding (Layout, Navbar, Footer)
### Sub-Phase 2: Hero Section
### Sub-Phase 3: Feature Sections (VisualCapabilities, CodeCompare, BentoGrid)
### Sub-Phase 4: Data Sections (Comparison, Philosophy, Roadmap)
### Sub-Phase 5: CTA, Final Polish & Deploy Config

Each sub-phase has its own detailed file in `.transform/` folder.

---

## Section Mapping (GitSetu → Gemmra)

| # | GitSetu Component | → | Gemmra Purpose | Effort |
|---|---|---|---|:---:|
| 1 | `Navbar.astro` | → | Logo "Gemmra", links: Demo, Architecture, Results, GitHub | 10 min |
| 2 | `Hero.astro` | → | "Nidāna for Pharmacovigilance" + score counters + thinking trace demo | 30 min |
| 3 | `VisualCapabilities.astro` | → | "4 Tasks, 1 Model" — show the 4 PV tasks with cards | 20 min |
| 4 | `CodeCompare.astro` | → | "Manual Review vs Gemmra" — 30 min manual → 5 sec AI | 15 min |
| 5 | `BentoGrid.astro` | → | "Technical Architecture" — pipeline, innovations grid | 20 min |
| 6 | `Comparison.astro` | → | "Performance Results" — score table + base vs fine-tuned | 15 min |
| 7 | `Philosophy.astro` | → | "Nidāna (निदान)" — meaning + origin story | 5 min |
| 8 | `Roadmap.astro` | → | "Future Work" — MedDRA dict, RAG, signal detection | 10 min |
| 9 | `Cta.astro` | → | "Explore Gemmra" — GitHub, HuggingFace, Demo links | 10 min |
| 10 | `Footer.astro` | → | TCS & AMD Hackathon 2026 attribution | 5 min |
| 11 | `TerminalDemo.astro` | → | **Thinking Trace Demo** — show AI reasoning animation | 30 min |
| 12 | `CommandPalette.astro` | → | **DELETE** — not needed for hackathon site | 0 min |

**Total estimated effort: ~2.5 hours**
