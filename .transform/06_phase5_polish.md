# Sub-Phase 5: CTA, Final Polish & Deploy Config

> **Time:** ~20 min
> **Risk:** Low
> **Depends on:** Phase 4 complete
> **Outcome:** CTA section updated, final text sweep, OG image, deploy-ready

---

## Session Prompt

```
I am transforming gitsetu-web into Gemmra — a drug safety AI landing page.

READ THESE FILES FIRST:
1. `gemmra-web/.transform/00_MASTER_PLAN.md` — Full context with ALL numbers
2. THIS FILE (`gemmra-web/.transform/06_phase5_polish.md`) — Exact steps

OBJECTIVE: Update CTA section, do a final sweep for ANY remaining GitSetu text, update OG image, verify build, and prepare for deployment.

This is the FINAL phase. After this, the site is ready to deploy.

Run `npm run dev` after changes. Then run `npm run build` to verify production build.
Commit when everything passes.
```

---

## Steps

### Step 5.1: Transform Cta.astro
**File:** `src/components/Cta.astro`

#### Headline
Change: "Deploy with Confidence"
To: "Explore Gemmra"

#### Subtext
Change to: "Fine-tuned Gemma 4 31B for pharmacovigilance. Open source. Built on AMD MI300X."

#### Buttons
Replace with:
```html
<a href="https://github.com/00bjxx/PharmaReview-AI" class="btn btn-primary">
  View on GitHub →
</a>
<a href="https://huggingface.co/bhaskarjha/gemmra-31b-lora" class="btn btn-secondary">
  Model on HuggingFace →
</a>
```

Remove: "Get Started Now" and "View on GitHub" (old links)

### Step 5.2: Final Text Sweep
Run a search across ALL .astro files for any remaining "GitSetu", "gitsetu", "git identity", "SSH", "credential", "zero-trust" text that wasn't caught in earlier phases.

Search command:
```bash
grep -ri "gitsetu\|zero-trust\|ssh\|credential\|identity guard\|setu" src/
```

Fix any remaining references.

### Step 5.3: Update README.md
**File:** `README.md`

Replace the entire contents with:
```markdown
# Gemmra Website

Landing page for **Gemmra — Nidāna for Pharmacovigilance**.

Built with [Astro](https://astro.build/).

## Development

```bash
npm install
npm run dev
```

## Build

```bash
npm run build
```

## Deploy

Deploy `dist/` to Cloudflare Pages or any static host.
Site URL: https://gemmra.bhaskarjha.dev
```

### Step 5.4: Update OG Image
**File:** `public/og-image.png`

The current OG image is for GitSetu. Options:
1. **Quick:** Delete it and remove the OG image meta tag (browser will use default)
2. **Better:** Create a simple OG image with text "Gemmra — Nidāna for Pharmacovigilance"
3. **Best:** Take a screenshot of the finished hero section and use that

For now, go with option 1 (delete and remove meta tag) or option 2 if time permits.

### Step 5.5: Update public/logo.png
**File:** `public/logo.png`

The current logo is GitSetu's. If there's no Gemmra logo ready:
- Option A: Delete logo.png and remove references (use text-only logo)
- Option B: Keep the file but it won't be displayed since we changed Navbar to text-only

Check if Navbar.astro references logo.png and remove the `<img>` tag if so.

### Step 5.6: Verify Production Build
```bash
cd gemmra-web
npm run build
```

Check:
- Build completes without errors
- `dist/` folder is created
- `dist/index.html` exists and contains "Gemmra"
- No references to "GitSetu" in `dist/index.html`

Final verification:
```bash
grep -i "gitsetu" dist/index.html
# Should return NOTHING
```

### Step 5.7: Clean Up .transform/ (Optional)
The `.transform/` folder served its purpose. You can either:
- **Keep it** — shows the transformation methodology (impressive for judges)
- **Delete it** — cleaner repo
- **Add to .gitignore** — keep locally but don't ship

Recommendation: Keep it — it shows systematic thinking.

---

## Verification

1. `npm run build` — builds without errors
2. `grep -i "gitsetu" dist/index.html` — returns nothing
3. Open `dist/index.html` in browser — complete Gemmra site
4. All sections render correctly
5. Navigation anchors work
6. Score counters animate
7. Responsive on mobile (resize browser)

## Final Commit Message

```
phase 5: CTA, polish, build verification — deployment ready

- Cta: "Explore Gemmra" with GitHub + HuggingFace links
- Final sweep: zero remaining GitSetu references
- README: updated for Gemmra
- OG image: cleaned up
- Build: verified, dist/ clean
- READY FOR DEPLOYMENT
```

---

## Post-Deployment

After all 6 phases are committed:

1. Create GitHub repo: `bhaskarjha-dev/gemmra-web` (or similar)
2. Push to GitHub
3. Set up Cloudflare Pages:
   - Connect to GitHub repo
   - Build command: `npm run build`
   - Output directory: `dist`
   - Custom domain: `gemmra.bhaskarjha.dev`
4. DNS: Add CNAME record `gemmra` → Cloudflare Pages URL

The site should be live within minutes of pushing.
