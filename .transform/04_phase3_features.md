# Sub-Phase 3: Feature Sections (VisualCapabilities, CodeCompare, BentoGrid)

> **Time:** ~30 min
> **Risk:** Low (text-only changes, layout stays identical)
> **Depends on:** Phase 2 complete
> **Outcome:** All middle sections show Gemmra content — 4 PV tasks, manual vs AI comparison, architecture grid

---

## Session Prompt

```
I am transforming gitsetu-web into Gemmra — a drug safety AI landing page.

READ THESE FILES FIRST:
1. `gemmra-web/.transform/00_MASTER_PLAN.md` — Full context with ALL numbers
2. THIS FILE (`gemmra-web/.transform/04_phase3_features.md`) — Exact steps

OBJECTIVE: Transform 3 components — VisualCapabilities, CodeCompare, BentoGrid. Keep layouts intact, replace ALL text content. Add id attributes for nav scrolling.

Run `npm run dev` after each component. Commit when this phase is complete.
```

---

## Steps

### Step 3.1: Transform VisualCapabilities.astro → "4 Tasks, 1 Model"
**File:** `src/components/VisualCapabilities.astro`

Add `id="tasks"` to the section element for anchor scrolling.

#### Section Title
Change: "Visualizing Zero-Trust"
To: "Four Tasks. One Model."

#### Section Subtitle
Change to: "Gemmra performs all four critical ICSR assessment tasks with auditable reasoning — each one previously requiring 30 minutes of expert review."

#### Feature Cards
This component shows 2 visual profile cards (work vs oss identities). Transform them into the 4 pharmacovigilance tasks:

**Card 1: T1 — Seriousness Assessment**
- Icon: ⚠️ or a warning triangle SVG
- Title: "Seriousness Classification"
- Score: "0.995 F1"
- Description: "Classifies adverse events against ICH E2A seriousness criteria — death, hospitalization, disability, life-threatening."

**Card 2: T2 — MedDRA Coding**
- Icon: 🏷️ or a tag SVG
- Title: "MedDRA Coding"
- Score: "0.667 Weighted"
- Description: "Maps adverse event narratives to standardized MedDRA Preferred Terms from 80,000+ possibilities."

**Card 3: T3 — Labelling Check**
- Icon: 📋 or a checklist SVG
- Title: "Labelling Assessment"
- Score: "0.801 F1"
- Description: "Determines whether the adverse event is already listed in the drug's approved labelling."

**Card 4: T4 — Causality Assessment**
- Icon: 🔗 or a chain link SVG
- Title: "WHO-UMC Causality"
- Score: "0.986 Weighted"
- Description: "Assesses the causal relationship between drug and adverse event using WHO-UMC methodology."

If the current layout only supports 2 cards, restructure to a 2×2 grid:
```css
.tasks-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: var(--space-xl);
}

@media (max-width: 768px) {
  .tasks-grid {
    grid-template-columns: 1fr;
  }
}
```

### Step 3.2: Transform CodeCompare.astro → "Manual vs Gemmra"
**File:** `src/components/CodeCompare.astro`

This component shows side-by-side "Old Way" vs "GitSetu Way" code panels. Perfect for our comparison.

#### Section Title
Change: "The end of alias scripts."
To: "The end of manual case review."

#### Section Subtitle
Change to: "Stop spending 30 minutes per ICSR report. Gemmra processes each case in under 5 seconds with full audit trail."

#### Left Panel: "THE OLD WAY" → "MANUAL REVIEW"
Replace the SSH config code with a manual review description:
```
📋 Manual ICSR Review Process:

1. Read case narrative (~5 min)
2. Check ICH E2A seriousness criteria (~5 min)
3. Search MedDRA dictionary (~8 min)
4. Cross-reference drug label (~7 min)
5. Assess WHO-UMC causality (~5 min)
6. Write structured report (~10 min)

⏱ Total: ~30 minutes per case
📊 2,000,000 cases/year (FDA alone)
💰 $20 per case = $40M+/year
```

Bottom label: Change "Error-prone, leaks identities globally." to:
```
✗ Slow, inconsistent, unscalable.
```

#### Right Panel: "THE GITSETU WAY" → "THE GEMMRA WAY"
Replace with:
```
🧠 Gemmra AI Assessment:

Input: Case narrative
  ↓
<thinking>
  Analyzing ICH E2A criteria...
  Mapping to MedDRA ontology...
  Checking drug label database...
  Evaluating WHO-UMC causality...
</thinking>
  ↓
Output: 4 structured assessments
  with auditable reasoning trace

⏱ Total: ~5 seconds per case
💰 $0.005 per case = $10K/year
```

Bottom label: Change "Idempotent, Zero-Trust, Automatic." to:
```
✓ Fast. Auditable. 4,000× cheaper.
```

### Step 3.3: Transform BentoGrid.astro → "Technical Architecture"
**File:** `src/components/BentoGrid.astro`

Add `id="architecture"` to the section element.

#### Section Title
Change: "Engineered for the local machine."
To: "Engineered on AMD MI300X."

#### Section Subtitle
Change to: "Full bf16 precision, zero quantization, LoRA r=64. Every architectural choice leverages AMD's 192 GB HBM3 advantage."

#### Grid Cards (6 features → 6 innovations)
The current grid has: Cryptographic Sandboxing, Zero-Dependency Core, Hardware FIDO2, Pre-Commit Guard, Automated Key Lifecycle, Encrypted Profile Backup.

Replace with our 6 technical highlights:

**Card 1: bf16 LoRA Training**
- Code badge: `LoRA r=64`
- Description: "Full bf16 precision with LoRA rank 64 on MI300X. Zero quantization = zero gradient noise."

**Card 2: Extended Thinking Mode**
- Code badge: `enable_thinking=True`
- Description: "Gemma 4's native thinking mode generates visible reasoning traces — the audit trail regulators require."

**Card 3: Data-First Debugging**
- Code badge: `3.9× improvement`
- Description: "Our biggest gain came from fixing one data pipeline bug, not hyperparameter tuning. Data quality > model tricks."

**Card 4: Hierarchical Evaluation**
- Code badge: `Gemmra-Bench`
- Description: "Novel 4-level scoring: exact → synonym → fuzzy → SOC match. 3,560 decontaminated evaluation samples."

**Card 5: FAERS Pipeline**
- Code badge: `29 quarters`
- Description: "Automated ingestion of 29 quarters of FDA adverse event data (2019Q1–2026Q1) via DuckDB."

**Card 6: Published Negative Results**
- Code badge: `GRPO/DAPO/RAFT`
- Description: "We documented what didn't work. RL approaches failed due to reward variance collapse — adding scientific rigor."

---

## Verification

1. `npm run dev` — no errors
2. Scroll through site: 4 PV task cards visible
3. Manual vs Gemmra comparison shows correct numbers
4. Architecture grid shows 6 technical innovations
5. Navigation links (#tasks, #architecture) scroll correctly

## Commit Message

```
phase 3: feature sections — 4 PV tasks, manual vs AI, architecture grid

- VisualCapabilities: 4 pharmacovigilance task cards with scores
- CodeCompare: manual review (30 min/$20) vs Gemmra (5 sec/$0.005)
- BentoGrid: 6 technical innovations (bf16, thinking, data-first, etc.)
- Added section IDs for nav anchor scrolling
```
