# Sub-Phase 2: Hero Section

> **Time:** ~30 min
> **Risk:** Medium (terminal demo is complex)
> **Depends on:** Phase 1 complete
> **Outcome:** Hero section shows Gemmra branding with score counters and thinking trace demo

---

## Session Prompt

```
I am transforming gitsetu-web into Gemmra — a drug safety AI landing page.

READ THESE FILES FIRST:
1. `gemmra-web/.transform/00_MASTER_PLAN.md` — Full context with ALL numbers
2. THIS FILE (`gemmra-web/.transform/03_phase2_hero.md`) — Exact steps

OBJECTIVE: Transform Hero.astro — change heading, subtext, badge, CTA buttons, and transform the TerminalDemo from a git CLI demo into a "thinking trace" animation that shows AI reasoning.

The key numbers for counters: 0.862 (composite), 0.995 (T1), 100% (format).

Run `npm run dev` after changes. Commit when this phase is complete.
```

---

## Steps

### Step 2.1: Update Hero.astro — Text Content
**File:** `src/components/Hero.astro`

#### Badge (top-left pill)
Change: `v1.1.0 — Enterprise Ready`
To: `TCS & AMD AI Hackathon 2026`

#### Main Heading
Change: `The Zero-Trust Identity Guard for Git.`
To: `Nidāna for Pharmacovigilance.`

Or a two-line approach:
```html
<h1>
  <span class="accent-text">Gemmra</span><br/>
  Nidāna for Pharmacovigilance.
</h1>
```

#### Subtext
Change the description paragraph to:
```
AI-powered drug safety review with auditable reasoning. One fine-tuned model that automates 4 critical pharmacovigilance tasks — from 30 minutes per case to 5 seconds.
```

#### Install Command → Score Counters
Replace the `curl -sL ... | bash` install command block with animated score counters:
```html
<div class="hero-stats">
  <div class="stat">
    <span class="counter" data-target="0.862">0</span>
    <label>Composite Score</label>
  </div>
  <div class="stat">
    <span class="counter" data-target="0.995">0</span>
    <label>Seriousness F1</label>
  </div>
  <div class="stat">
    <span class="counter" data-target="100">0</span>
    <label>Format Compliance %</label>
  </div>
</div>
```

Add client-side counter animation script:
```html
<script>
  function animateCounters() {
    document.querySelectorAll('.counter').forEach(counter => {
      const target = parseFloat(counter.dataset.target);
      const isPercent = target >= 1;
      const duration = 2000;
      const start = performance.now();
      
      function update(now) {
        const elapsed = now - start;
        const progress = Math.min(elapsed / duration, 1);
        const eased = 1 - Math.pow(1 - progress, 3);
        const current = target * eased;
        counter.textContent = isPercent 
          ? Math.round(current) + '%'
          : current.toFixed(3);
        if (progress < 1) requestAnimationFrame(update);
      }
      requestAnimationFrame(update);
    });
  }

  // Trigger when hero is visible
  const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        animateCounters();
        observer.disconnect();
      }
    });
  });
  observer.observe(document.querySelector('.hero-stats'));
</script>
```

Add styles for the stats:
```css
.hero-stats {
  display: flex;
  gap: var(--space-2xl);
  margin-top: var(--space-xl);
}

.stat {
  text-align: center;
}

.stat .counter {
  font-family: var(--font-mono);
  font-size: var(--text-4xl);
  font-weight: 700;
  color: var(--accent-primary);
  display: block;
}

.stat label {
  font-size: var(--text-sm);
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-top: var(--space-xs);
  display: block;
}
```

#### CTA Button
Change: `Read Docs →`
To: `View on GitHub →`
Link: `https://github.com/00bjxx/PharmaReview-AI`

### Step 2.2: Transform TerminalDemo.astro → ThinkingTrace Demo
**File:** `src/components/TerminalDemo.astro`

This is the most complex change. The terminal currently shows git commands auto-typing. We need to show a **pharmacovigilance thinking trace** — the AI reasoning through a drug safety case.

**Approach:** Keep the xterm.js terminal, but change the auto-demo content.

Find the auto-demo content/script (the text that gets typed). Replace the git commands with a pharmacovigilance thinking trace:

```
Input: 68-year-old male on Warfarin 5mg daily for atrial fibrillation.
Reported adverse event: GI haemorrhage. Outcome: Hospitalized.

<thinking>
Analyzing case against ICH E2A seriousness criteria...
→ Outcome "Hospitalized" maps to HO (Hospitalization)
→ GI haemorrhage is a known serious AE for anticoagulants
→ Warfarin is a high-risk narrow therapeutic index drug
Assessment: SERIOUS — criterion HO met
</thinking>

SERIOUS: YES
CRITERIA: HO
RATIONALE: Patient hospitalized for GI haemorrhage,
a known serious adverse event for Warfarin therapy.
```

**Key:** Change the terminal title from "gitsetu — bash" to "gemmra — inference"

Find the terminal title bar HTML and change it. The tab labels "Auto-Demo" / "Interactive" can stay — they describe the terminal modes well.

If the auto-demo is too complex to modify, a simpler approach:
- **Remove xterm.js entirely** from the terminal demo
- Replace with a CSS-only typing animation using the thinking trace text
- This eliminates the xterm dependency and is simpler

### Step 2.3: Update Hero.astro — Remove Copy Button
The install command had a copy-to-clipboard button. Since we replaced it with counters, make sure the copy button code is removed.

---

## Verification

1. `npm run dev` — no errors
2. Hero shows "Gemmra" heading with "Nidāna for Pharmacovigilance"
3. Badge shows "TCS & AMD AI Hackathon 2026"
4. Score counters animate from 0 → 0.862, 0 → 0.995, 0 → 100%
5. Terminal shows pharmacovigilance thinking trace (or CSS animation)
6. CTA button links to GitHub

## Commit Message

```
phase 2: hero — Gemmra heading, score counters, thinking trace demo

- Heading: "Gemmra / Nidāna for Pharmacovigilance"
- Badge: TCS & AMD AI Hackathon 2026
- Score counters: 0.862, 0.995, 100% with animation
- Terminal: PV thinking trace auto-demo
- CTA: View on GitHub
```
