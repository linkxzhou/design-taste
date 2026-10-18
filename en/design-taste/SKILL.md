---
name: design-taste
description: Design-taste guide for making visual output look intentional, not templated "AI slop". Use to design, build, restyle, redesign, polish, critique or audit a UI (web page, landing page, dashboard, app screen, component), set up design tokens, pick colors/fonts/spacing, theme slides/docs, make a minimalist look, review/benchmark a live website URL, review or restyle images (photo, product, poster, banner, illustration, scientific figure, AI image — composition, palette, AI-artifact critique), review game art (screenshot, key art, Steam capsule, icon, HUD, concept, sprite/pixel; genre readability), or create a poster/cover. Chinese triggers include 设计界面, 美化页面, 界面评审, UI 审查, 重新设计, 改版, 设计规范, 配色, 字体搭配, 极简风格, 主题, 海报, 网站评审, 官网改版, 对标, 图片审美, 图片评审, 海报评审, 配色提取, 构图, 科研配图, AI 图片评价, 游戏美术, 游戏审美, 游戏 UI, RPG, MOBA, 二次元, 像素, 游戏截图评审. Not for backend logic or code cleanup with no visible change.
license: MIT
---

# Design Taste

Make deliberate visual decisions, then execute them consistently. Taste here means: **one clear direction, few well-chosen tokens, strong hierarchy, and no default-looking filler.**

Work through the steps below in order. Every mode runs Steps 0–2, then either the **build path (B3–B6)** or the **review path (R3–R6)**, then the **final report step**. Step labels are for your own tracking; don't paste them into the user's deliverable.

## Step 0 — Intake and mode

- **Do:** read the request and any artifacts (code, URL, image, screenshot). Pick one primary mode from the table, plus any style overlay.
- **Output:** primary mode, overlays, path (build or review), and the reference files to load.
- **Decision:** create/change something visible → build path; critique, score or benchmark only → review path. Redesign runs the review path's R3–R6 as its audit, then the build path. Overlays (Minimalist) never change the path; they are applied in Step 2 and checked in B5. If the request has no visible output (backend logic, cleanup only), stop: this skill doesn't apply.

| User intent | Mode | Path | Load | Mode-specific steps |
|---|---|---|---|---|
| Build a new page/app/component | **Create** | Build | `references/direction.md`, `references/principles.md`, `references/tokens.md` | B3–B6 as written |
| "Review / audit / what's wrong with this UI" | **Audit** | Review | `references/audit.md` | `audit.md` §1 checks → §2 checklist → §3 report |
| "Redesign / upgrade / polish / make it premium" | **Redesign** | Review → Build | `references/audit.md` then `references/redesign.md` | `redesign.md` Workflow 1–9 (R3–R6 = its step 2; B3–B6 = its steps 4–9) |
| "Minimal / clean / editorial / Notion-like" | **Minimalist** (style overlay) | Same as primary mode | `references/minimalist.md` | Apply the spec in Step 2 (tone) and B3 (tokens); check it in B5 |
| Slides, docs, reports, HTML handouts needing a look | **Theme** | Build | `references/theming.md` | Theme recipe in `theming.md` drives B3–B4 |
| Poster, cover, static art (PNG/PDF) | **Artifact** | Build | `references/artifacts.md` | Philosophy → canvas process in `artifacts.md` drives B4 |
| "Review / score / beautify this website URL", benchmark vs. competitors (评审网站, 网站美化, 对标) | **Site Review** | Review | `references/site-review.md`, `references/benchmarks.md`, run `scripts/review_site.py` | `site-review.md` §1 capture → §2 score → §3 compare → §4 report (§5 batch) |
| "Rate / critique / what's wrong with this image", poster or cover review, AI-image critique (图片审美, 图片评审, 海报评审, AI 图片评价, 构图) | **Image Review** | Review | `references/image-aesthetics.md`, run `scripts/review_image.py <img> --type …` | R3 script metrics (§6) → R4 8 dimensions × type weights (§1–2) + AI checklist (§4) → R6 severity (§3) → report (§7) |
| Game screenshot / key art / Steam capsule / icon / HUD / concept / sprite review, genre art direction (游戏美术, 游戏审美, 游戏 UI, 游戏截图评审, RPG, MOBA, 二次元, 像素) | **Game Art Review** | Review | `references/game-aesthetics.md`, `references/game-workflows.md`, run `scripts/review_image.py <img> --type game-screenshot\|key-art\|capsule\|icon\|game-ui\|concept\|sprite --genre <g>` | `game-workflows.md` §1 (step by step) → §2 report; fixes in §3 |
| "Make this photo a magazine page / product hero / poster", extract a palette, image-model prompts, scientific figures (配色提取, 科研配图) | **Image Restyle** | Build | `references/image-workflows.md` (+ `image-aesthetics.md` to score before/after) | `image-workflows.md` §1 4-step pipeline = B3–B4; §3 restyle loop = B6 |

Modes combine (e.g. Redesign + Minimalist). Read only the files you need.

## Step 1 — Gather context

- **Do:** find the stack, CSS approach, component library, existing tokens or design system, brand assets, and constraints (accessibility level, performance budget). Take a screenshot or run the mode's script to get baseline numbers: `scripts/review_site.py` for URLs, `scripts/review_image.py --type … [--genre …]` for images; add `--lang zh` when the user writes in Chinese.
- **Output:** a short context note plus baseline metrics (or "no tooling — visual judgment only").
- **Done when:** you know what exists and what you must preserve. If a required artifact is missing (no URL, no image, no code), ask for it before continuing.

## Step 2 — Decide a direction

- **Do:** write 3–5 lines (to yourself or the user) before building or scoring:
  1. **Purpose & audience** — what job does this screen do, for whom?
  2. **Tone** — choose one specific stance (e.g. editorial, brutalist, soft/organic, technical/dense, luxury/quiet, playful, retro-industrial). "Clean and modern" is not a direction. Apply overlays here.
  3. **Signature** — the one thing someone will remember (a type pairing, a bold color field, an unusual grid, a motion moment).
  4. **Constraints** — existing brand, framework, accessibility level, performance budget.
  5. **Density** — airy marketing vs. dense tool. Dashboards ≠ landing pages.
- **Review path:** write the direction *as perceived* (what the artifact seems to be going for) — that is the yardstick for scoring.
- **Output:** the direction block (template in `references/direction.md` §5).
- **Done when:** it names one tone and one signature. If the project already has a design system, the direction is *"follow it well"*; don't invent a second one.

## Build path (Create, Redesign, Theme, Artifact, Image Restyle)

### B3 — Tokens first
- **Do:** define a small named scale for color, type, spacing, radius, shadow, and motion as CSS variables / theme config (3-tier system in `references/tokens.md`). Redesign: consolidate existing literals into it. Minimalist: use `minimalist.md` values.
- **Output:** a token file or theme block.
- **Done when:** the counts fit the Constraints section (≈1 accent, 1–2 typefaces, ≤ 6–8 sizes, one radius family, ≤ 3 shadows).

### B4 — Execute
- **Do:** implement real, working code (or the artifact) in the user's stack, matching existing conventions. Build global layer → components (all states) → layouts, using only tokens. Match effort to direction: maximal designs need elaborate execution; minimal designs need precision in spacing and type. Follow the mode's steps from the table (`redesign.md` 5–8, theme recipe, artifact process, image pipeline).
- **Output:** changed files / rendered artifact.
- **Done when:** the whole requested scope is built; no literal colors or sizes outside tokens.

### B5 — Self-check against Constraints
- **Do:** walk the Constraints section below line by line (core rules + AI-slop tells), plus any overlay spec.
- **Output:** list of violations.
- **Decision:** any violation → fix it in B4 and re-check; none → B6.

### B6 — Verify
- **Do:** run the quick checks from `references/audit.md` (counts of hex colors, font sizes, radii; contrast; states; responsive at ~375/768/1280px). If you can render, take a screenshot and look at it. Run existing tests/build. For Redesign or Image Restyle, re-run the Step 1 script and compare before/after numbers.
- **Output:** check results with numbers.
- **Decision:** counts within limits, no contrast failures, no P0 issues, and nothing reads as generic or cluttered → final report. Otherwise → back to B4.

## Review path (Audit, Site Review, Image Review, Game Art Review; audit half of Redesign)

### R3 — Measure
- **Do:** run the mode's measurable checks: `audit.md` §1 grep counts, `review_site.py` metrics, or `review_image.py` metrics (+ grayscale/thumbnail tests for games).
- **Output:** a metrics table.
- **Done when:** every metric the mode's report template asks for has a number, or is marked "not measurable" with the reason.

### R4 — Score
- **Do:** look at the artifact yourself and score it with the mode's rubric: `audit.md` §2 checklist, `site-review.md` §2 (45/55), `image-aesthetics.md` 8 dimensions × type weights + AI checklist, or `game-aesthetics.md` G1–G11 × asset weights + genre profile. Combine metric and visual scores as the reference says (e.g. 0.4 metric + 0.6 visual for images).
- **Output:** per-dimension scores, each with concrete evidence ("six fingers on the lower-left hand", not adjectives).
- **Done when:** every dimension has a score and evidence; any P0 caps the total as the rubric specifies.

### R5 — Compare (Site Review and Game Art Review; others skip)
- **Do:** compare against `benchmarks.md` / `benchmarks.csv` or the genre profile and named competitors.
- **Output:** metrics vs. benchmark table and 2–3 takeaways.
- **Done when:** each gap names the benchmark value it misses.

### R6 — Prioritize
- **Do:** turn findings into P0/P1/P2 issues. Each issue gets: what, where (file:line, screen area, or image region), why it matters, and a concrete fix (token values, HEX, crop ratio, prompt).
- **Output:** prioritized issue list.
- **Done when:** every item has where/why/fix. Redesign → continue to B3; other review modes → final report.

## Final step — Report

- **Do:** write in the user's language. The scripts write `report.md` in English by default; pass `--lang zh` for a Chinese skeleton and replace every TODO.
  - Build path: the direction you chose and trade-offs in 2–4 lines, what changed, and verification numbers from B6.
  - Review path: the mode's report template (`audit.md` §3, `site-review.md` §4, `image-aesthetics.md` §7, `game-workflows.md` §2).
- **Output:** the deliverable message (plus report files/screenshots if produced).
- **Done when:** every claim is backed by a number or an observation from R3/R4 or B6; nothing unverified is presented as checked.

## Constraints (checked in B5)

### Core rules (always on)
- **Commit.** A bold minimal design and a maximal one are both fine; a timid average of everything is not.
- **Tokens, not literals.** Every color, size, radius, shadow, and duration comes from a small named scale (see `references/tokens.md`).
- **Restraint in counts:** ~1 accent color, 1–2 typefaces, ≤ 6–8 font sizes, one radius family, ≤ 3 shadow levels, one easing curve family.
- **Hierarchy through contrast** of size, weight, and space — not more boxes, borders, and colors.
- **Spacing on a grid** (4/8px base). Group related things tightly, separate groups generously.
- **Accessibility is part of taste:** text contrast ≥ 4.5:1 (3:1 large), visible focus, hit targets ≥ 44px on touch, respect `prefers-reduced-motion`.
- **Real content.** No "John Doe / Acme / Lorem ipsum", no "Elevate your workflow" copy, no emoji as icons.
- **Every state exists:** hover, focus, active, disabled, loading, empty, error.

### AI-slop fingerprint (avoid unless the brief explicitly calls for it)
- Purple→blue gradients on white; neon glows on dark; gradient text everywhere.
- Inter/Roboto/Arial by reflex; one weight for everything.
- Centered hero + three identical icon cards + generic CTA band.
- Cards nested in cards; every element in a rounded bordered box with a drop shadow.
- Glassmorphism for no reason; random decorative blobs.
- Uniform `rounded-2xl` + `shadow-lg` on everything; inconsistent radii.
- Fake metrics ("10x faster", "99.9%") and stock testimonials.
- Bouncy/elastic animation on everything; animating layout properties.

Details and alternatives: `references/principles.md`.

## Reference map

- `references/direction.md` — direction prompts, tone catalog, how to pick fonts/palettes per tone.
- `references/principles.md` — color, typography, spacing, radius, shadow, motion, layout rules + anti-patterns.
- `references/tokens.md` — 3-tier token system (primitive → semantic → component) with example.
- `references/audit.md` — P0/P1/P2 checklist, measurable checks, report format.
- `references/redesign.md` — safe upgrade workflow for existing projects.
- `references/minimalist.md` — warm-monochrome editorial style spec.
- `references/theming.md` — themes for slides/docs/reports; theme recipe.
- `references/artifacts.md` — posters and static visual pieces (philosophy → canvas).
- `references/site-review.md` — URL review workflow: capture → metrics → 45/55 score → P0/P1/P2 report.
- `references/benchmarks.md` — top-company homepage breakdowns, industry playbooks, metric targets, common mistakes.
- `scripts/review_site.py` — Playwright capture + metric score + report skeleton; `scripts/benchmarks.csv` — 147 scored sites.
- `references/image-aesthetics.md` — image rubric: 8 dimensions × type weights, P0/P1/P2, AI-artifact checklist, metric ranges.
- `references/image-workflows.md` — parse → palette → layout → enhance pipeline; zine/collage/product/palette/cover recipes; Nature-style figure checklist; anti-slop prompt templates.
- `scripts/review_image.py` — Pillow+numpy image metrics (palette, harmony, tone, sharpness, noise, colorfulness, thirds/centroid, whitespace) → metrics.json, palette.png, thirds-overlay.png, report.md.
- `references/game-aesthetics.md` — game rubric: 11 dims (readability, value, gameplay clarity, HUD, VFX…) × asset weights, 21 genre profiles, 9 asset rubrics, AI checks, metric ranges.
- `references/game-workflows.md` — grayscale/silhouette/thumbnail/2-second tests, metric interpretation by genre, P0/P1/P2 report, fix recipes, anti-slop game-art prompts.
- `scripts/review_image.py --type <game type> --genre <g>` — adds value bands, figure-ground, shape clarity, HUD coverage, color count, store-thumbnail readability → grayscale.png, thumbnail.png.
- `references/sources.md` — upstream skills, URLs, and licenses.
