# Sub-Phase 1: Global Branding (Layout, Navbar, Footer)

> **Time:** ~15 min
> **Risk:** Low
> **Depends on:** Phase 0 complete
> **Outcome:** All global chrome says "Gemmra" — header, footer, meta tags, fonts

---

## Session Prompt

```
I am transforming gitsetu-web into Gemmra — a drug safety AI landing page.

READ THESE FILES FIRST:
1. `gemmra-web/.transform/00_MASTER_PLAN.md` — Full context with ALL content/numbers
2. THIS FILE (`gemmra-web/.transform/02_phase1_branding.md`) — Exact steps

OBJECTIVE: Update Layout.astro (meta tags, title), Navbar.astro (logo, nav links), Footer.astro (links, attribution), and global.css (color comment). NO content sections yet.

Run `npm run dev` after changes. Commit when this phase is complete.
```

---

## Steps

### Step 1.1: Update Layout.astro — Meta Tags
**File:** `src/layouts/Layout.astro`

Update the `<head>` section:
- `<title>` → "Gemmra — Nidāna for Pharmacovigilance"
- `<meta name="description">` → "AI-powered drug safety review with auditable reasoning. Fine-tuned Gemma 4 31B for pharmacovigilance on AMD MI300X."
- `<meta property="og:title">` → "Gemmra — Nidāna for Pharmacovigilance"
- `<meta property="og:description">` → same as description
- `<meta property="og:site_name">` → "Gemmra"
- Any `gitsetu` text → `gemmra`
- Keep the Google Fonts imports (Inter, Outfit, JetBrains Mono) — they're perfect

### Step 1.2: Update global.css — Comments Only
**File:** `src/styles/global.css`

Line 1-3: Change comment:
```css
/* ============================================================
   Gemmra Landing Page — Global Design System (Deep Space / Fluid)
   ============================================================ */
```

Line 33: Change comment:
```css
/* Brand accent (Gemmra Teal — medical technology) */
```

**Do NOT change any CSS values** — the design tokens are already excellent.

### Step 1.3: Update Navbar.astro
**File:** `src/components/Navbar.astro`

Replace the logo text "GitSetu" with "Gemmra".

Replace nav links. Find the navigation links and change them to:
```html
<a href="#tasks">Tasks</a>
<a href="#architecture">Architecture</a>
<a href="#results">Results</a>
```

Remove: Search button (Ctrl+K), Docs button.
Keep: GitHub link but update URL to `https://github.com/00bjxx/PharmaReview-AI`

Remove the `CommandPalette` trigger button if present.

### Step 1.4: Update Footer.astro
**File:** `src/components/Footer.astro`

Replace all footer links and text:
- Logo text: "Gemmra"
- Links: Docs → link to GitHub README, Architecture → #architecture, GitHub → repo URL
- Add: "TCS & AMD AI Hackathon 2026" attribution text
- Remove: MIT License text (or keep if you want)
- Remove: Roadmap link

### Step 1.5: Update or replace favicon
**File:** `public/favicon.svg`

Change the SVG content to something medical/AI themed. A simple option:
```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
  <rect width="32" height="32" rx="8" fill="#00c4cc"/>
  <text x="16" y="22" text-anchor="middle" font-family="system-ui" font-weight="700" font-size="18" fill="white">G</text>
</svg>
```

---

## Verification

1. `npm run dev` — no errors
2. Browser tab shows "Gemmra — Nidāna for Pharmacovigilance"
3. Navbar shows "Gemmra" logo with correct nav links
4. Footer shows "Gemmra" with hackathon attribution
5. Favicon shows "G" in teal

## Commit Message

```
phase 1: global branding — Gemmra identity across navbar, footer, meta

- Layout: title, description, OG tags all say Gemmra
- Navbar: logo → Gemmra, links → Tasks/Architecture/Results/GitHub
- Footer: attribution → TCS & AMD Hackathon 2026
- Favicon: G in teal circle
- global.css: updated comments (no value changes)
```
