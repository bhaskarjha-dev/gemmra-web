# Sub-Phase 4: Data Sections (Comparison, Philosophy, Roadmap)

> **Time:** ~20 min
> **Risk:** Low (text-only changes)
> **Depends on:** Phase 3 complete
> **Outcome:** Results table, Nidāna philosophy section, future work roadmap — all complete

---

## Session Prompt

```
I am transforming gitsetu-web into Gemmra — a drug safety AI landing page.

READ THESE FILES FIRST:
1. `gemmra-web/.transform/00_MASTER_PLAN.md` — Full context with ALL numbers
2. THIS FILE (`gemmra-web/.transform/05_phase4_data.md`) — Exact steps

OBJECTIVE: Transform 3 components — Comparison (results table), Philosophy (Nidāna meaning), Roadmap (future work). These are the bottom half of the page.

Run `npm run dev` after each component. Commit when this phase is complete.
```

---

## Steps

### Step 4.1: Transform Comparison.astro → "Performance Results"
**File:** `src/components/Comparison.astro`

Add `id="results"` to the section element.

This component currently shows a feature comparison table (GitSetu vs competitors). Transform it into the Gemmra performance results table.

#### Section Title
Change: "How GitSetu compares."
To: "How Gemmra performs."

#### Section Subtitle
Change to: "Evaluated on 3,560 decontaminated samples across 4 pharmacovigilance tasks. Full bf16 inference on AMD MI300X."

#### Table Headers
Change from: Feature / GitSetu / gitego / karn / gh CLI / GCM
To: Task / Metric / Score / Samples / Status

#### Table Rows
```
| T1 Seriousness    | F1 Score  | 0.995 | 890   | ✅ Near-perfect |
| T2 MedDRA Coding  | Weighted  | 0.667 | 890   | 🔶 Room to grow |
| T3 Labelling      | F1 Score  | 0.801 | 890   | ✅ Strong       |
| T4 Causality      | Weighted  | 0.986 | 890   | ✅ Near-perfect |
| Format Compliance  | All tasks | 100%  | 3,560 | ✅ Perfect      |
| **Composite**     | **Average** | **0.862** | **3,560** | ✅ **Shipped** |
```

#### Styling Notes
- Keep the existing table styling (dark cards, subtle borders)
- Make the "0.995" and "0.986" cells glow green (use --color-success)
- Make the "0.667" cell use warning color (--color-warning)
- Make "0.862" in the composite row larger/bold

### Step 4.2: Transform Philosophy.astro → "Nidāna"
**File:** `src/components/Philosophy.astro`

This is the most beautiful section swap — it already has Sanskrit!

#### First Quote
Change:
```
In Sanskrit, Setu (सेतु) means bridge —
connecting two shores without disturbing either.
```
To:
```
In Ayurveda, Nidāna (निदान) is the systematic
investigation of disease causation.
```

#### Second Quote
Change:
```
Good security should not require developer discipline.
The question of "Who committed this?" is no longer personal;
it is architectural.
```
To:
```
Drug safety should not depend on manual throughput.
The question of "Is this adverse event serious?"
is no longer subjective; it is computed.
```

#### Highlight Quote
Change:
```
A tool that demands your attention has failed.
GitSetu succeeds when you forget it exists.
```
To:
```
We found it funny calling our solution Gemmra,
and the name stuck.
```

The `glow-text` class on the last line will make "and the name stuck" glow in teal — perfect.

### Step 4.3: Transform Roadmap.astro → "Future Work"
**File:** `src/components/Roadmap.astro`

#### Section Title
Change: "The Universal Identity Fabric."
To: "The Future of Automated Pharmacovigilance."

#### Section Subtitle
Change to: "Gemmra is the beginning. These capabilities are on our research roadmap."

#### Phase Cards (3 phases)
The current roadmap has CI/CD Identity, Auto-Rotation, Agentic Identity. Replace with:

**Phase 1: MedDRA Dictionary Augmentation**
- Description: "Include all 80,000+ MedDRA Preferred Terms in training data. Add retrieval-augmented generation for real-time PT lookup during inference."
- Tag: "T2 Improvement"

**Phase 2: Multi-Source Signal Detection**
- Description: "Aggregate case-level assessments into population-level safety signals. Cross-reference FDA FAERS, EMA EudraVigilance, and PMDA databases."
- Tag: "Population Safety"

**Phase 3: Real-Time PV-as-a-Service**
- Description: "Production API with streaming thinking traces. Confidence-calibrated outputs with uncertainty estimation. Real-time monitoring dashboard."
- Tag: "Production Deployment"

---

## Verification

1. `npm run dev` — no errors
2. Results table shows all 4 task scores + composite
3. Philosophy section shows Nidāna (निदान) meaning
4. "and the name stuck" glows in teal
5. Roadmap shows 3 future work phases
6. Navigation #results anchor scrolls to table

## Commit Message

```
phase 4: data sections — results table, Nidāna philosophy, future work

- Comparison: 6-row performance table (T1-T4 + format + composite)
- Philosophy: Sanskrit swap — Setu → Nidāna (निदान), origin story
- Roadmap: 3 phases — MedDRA augmentation, signal detection, PV-as-a-Service
```
