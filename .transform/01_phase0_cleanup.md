# Sub-Phase 0: Cleanup & Config

> **Time:** ~10 min
> **Risk:** Low
> **Depends on:** Nothing
> **Outcome:** Clean project with no GitSetu dead code, correct domain config

---

## Session Prompt

```
I am transforming a cloned website (originally GitSetu) into Gemmra — a drug safety AI solution for TCS & AMD AI Hackathon 2026.

READ THESE FILES FIRST:
1. `gemmra-web/.transform/00_MASTER_PLAN.md` — Full context, content reference, architecture
2. THIS FILE (`gemmra-web/.transform/01_phase0_cleanup.md`) — Exact steps for this phase

OBJECTIVE: Remove all GitSetu-specific dead code and update config files. Do NOT change any visual content yet — that comes in later phases.

After each step, verify the dev server still works: `npm run dev` (in gemmra-web/).
Commit after ALL steps in this phase are done.
```

---

## Steps

### Step 0.1: Update package.json
**File:** `package.json`

Change:
```json
"name": "gitsetu-web"
```
To:
```json
"name": "gemmra-web"
```

Remove the `sync-docs` script and simplify `dev`/`build`:
```json
"scripts": {
  "dev": "astro dev",
  "build": "astro build",
  "preview": "astro preview"
}
```

### Step 0.2: Update astro.config.mjs
**File:** `astro.config.mjs`

Change:
```js
site: 'https://gitsetu.bhaskarjha.dev',
```
To:
```js
site: 'https://gemmra.bhaskarjha.dev',
```

### Step 0.3: Delete dead files
Delete these files/folders entirely:
- `scripts/` folder (doc sync scripts — not needed)
- `docs/` folder (PROMPTS.md — not needed)
- `src/pages/search.json.ts` (search index — not needed)
- `src/pages/og/[...slug].png.ts` (dynamic OG images for docs — not needed)
- `src/layouts/DocsLayout.astro` (docs layout — not needed)
- `src/components/CommandPalette.astro` (Ctrl+K search — not needed)

### Step 0.4: Remove CommandPalette import from Layout
**File:** `src/layouts/Layout.astro`

Find and remove the import and usage of `CommandPalette`:
- Remove: `import CommandPalette from '../components/CommandPalette.astro';`
- Remove: `<CommandPalette />` from the template

### Step 0.5: Remove unused dependencies from package.json
**File:** `package.json`

Remove these dependencies (used by deleted features):
- `@orama/orama` (search)
- `@resvg/resvg-js` (OG image generation)
- `satori` (OG image generation)
- `satori-html` (OG image generation)

Keep:
- `astro` (framework)
- `@xterm/xterm` and `@xterm/addon-fit` (terminal demo — we'll repurpose it)

### Step 0.6: Clean up public/_redirects
**File:** `public/_redirects`

Replace contents with:
```
/* /index.html 200
```

---

## Verification

1. Run `npm run dev` — site should start without errors
2. Open http://localhost:4321 — page should render (still with GitSetu content — that's OK)
3. No console errors about missing CommandPalette or search

## Commit Message

```
phase 0: cleanup — remove dead code, update config for gemmra

- package.json: name → gemmra-web, remove sync-docs scripts
- astro.config: site → gemmra.bhaskarjha.dev
- Delete: scripts/, docs/, CommandPalette, DocsLayout, search, OG gen
- Remove unused deps: orama, resvg, satori
- Keep: astro, xterm (for thinking trace demo)
```
