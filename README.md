# design-taste

**English** · [简体中文](README.zh-CN.md)

An agent skill that gives coding agents design taste: make deliberate visual decisions, keep the token set small, build strong hierarchy, and avoid the templated "AI slop" look. It also scores live websites, images and game art with bundled scripts and benchmark data.

Ships in two standalone editions with identical logic:

| Edition | Path | Report language (default) |
|---|---|---|
| English | [`en/design-taste/`](en/design-taste/) | English (`--lang zh` for Chinese) |
| 简体中文 | [`zh/design-taste/`](zh/design-taste/) | Chinese (`--lang en` for English) |

Install **one** edition per agent. Both use the skill name `design-taste`.

## What it does

| Mode | Use it for |
|---|---|
| **Create** | New pages, apps and components: direction first, then a 3-tier token system |
| **Audit** | Measurable UI review (color/font-size/radius/shadow counts, contrast, states) with P0/P1/P2 issues |
| **Redesign** | Upgrade an existing UI without breaking behavior, tokens first |
| **Minimalist** | Warm-monochrome editorial overlay (Notion/Linear-like calm) |
| **Theme** | Palettes and type pairings for slides, docs and reports |
| **Artifact** | Posters, covers and static art (philosophy → canvas) |
| **Site Review** | Capture a URL with Playwright, compute metrics, score 45% metric + 55% visual, benchmark against peers |
| **Image Review / Restyle** | Score photos, product shots, posters, figures and AI images; palette extraction, restyle recipes, anti-slop prompts |
| **Game Art Review** | Screenshots, key art, Steam capsules, icons, HUD, concept, sprites; 11-dimension rubric with 21 genre profiles |

## Highlights

- **Benchmarks from 147 company homepages** (global top-100 by market cap plus top-100 tech), scored with the same formula the script uses. Includes top-10 breakdowns, top-20 vs bottom-20 metric targets, industry playbooks and common mistakes (`references/benchmarks.md`, `scripts/benchmarks.csv`).
- **Game genre rubrics**: 11 dimensions × asset-type weights, 21 genre profiles (MOBA, shooter, gacha, pixel, wuxia, ink wash…), Steam/App Store rules, grayscale/silhouette/thumbnail tests.
- **Scripts with no network downloads of their own**:
  - `scripts/review_site.py`: Playwright capture (desktop + mobile), design metrics, hero-image analysis, `report.md` skeleton.
  - `scripts/review_image.py`: Pillow + numpy metrics (palette, harmony, tone, sharpness, noise, composition, whitespace) plus game metrics (value bands, figure-ground, HUD coverage, store-thumbnail readability).
- **Anti-slop checklists** for UI, images and game art.

## Quick usage

Ask your agent in plain language:

```text
Build a landing page for a specialty coffee roaster. Single HTML file.
Audit the UI quality of this React project under src/ and give me a P0/P1/P2 list.
Review https://example.com and benchmark it against Software/Cloud peers.
Rate this AI-generated poster (poster.png) and tell me what to fix.
Review this MOBA teamfight screenshot for readability and HUD clutter.
帮我评审一下这个官网，并和同行业对标。
```

Or run the scripts directly (paths relative to the skill folder):

```bash
# website review (one-time setup for Playwright)
pip install playwright && python3 -m playwright install chromium
python3 scripts/review_site.py https://example.com --industry Software/Cloud --mobile --out review-example

# image / game art review
pip install pillow numpy
python3 scripts/review_image.py poster.png --type poster
python3 scripts/review_image.py shot.png --type game-screenshot --genre moba
python3 scripts/review_image.py --list-genres
python3 scripts/review_image.py photo.jpg --lang zh   # Chinese report skeleton
```

## Install

Clone once, then copy (or symlink) **one** edition into your agent's skills folder. Replace `en` with `zh` for the Chinese edition.

```bash
git clone --depth 1 https://github.com/linkxzhou/design-taste.git ~/design-taste
```

| Agent | User-level (all projects) | Project-level |
|---|---|---|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| OpenAI Codex CLI | `~/.agents/skills/` (legacy `~/.codex/skills/` still read) | `.agents/skills/` |
| Cursor | `~/.cursor/skills/` or `~/.agents/skills/` (also reads `~/.claude/skills/`, `~/.codex/skills/`) | `.cursor/skills/` or `.agents/skills/` |
| CodeBuddy | `~/.codebuddy/skills/` | `.codebuddy/skills/` |
| Gemini CLI | `~/.gemini/skills/` or `~/.agents/skills/` | `.gemini/skills/` or `.agents/skills/` |
| Others (Agent Skills standard) | the agent's skills folder | — |

One-liners (user-level):

```bash
# Claude Code
mkdir -p ~/.claude/skills && cp -R ~/design-taste/en/design-taste ~/.claude/skills/
# OpenAI Codex CLI, and any agent that reads ~/.agents/skills (Cursor, Gemini CLI)
mkdir -p ~/.agents/skills && cp -R ~/design-taste/en/design-taste ~/.agents/skills/
# Cursor
mkdir -p ~/.cursor/skills && cp -R ~/design-taste/en/design-taste ~/.cursor/skills/
# CodeBuddy
mkdir -p ~/.codebuddy/skills && cp -R ~/design-taste/en/design-taste ~/.codebuddy/skills/
# Gemini CLI
mkdir -p ~/.gemini/skills && cp -R ~/design-taste/en/design-taste ~/.gemini/skills/
```

Use `ln -s ~/design-taste/en/design-taste ~/.claude/skills/design-taste` instead of `cp` to get updates with `git -C ~/design-taste pull`. Restart the agent (Codex, Cursor) or run `/skills reload` (Gemini CLI) after installing. Gemini CLI workspace skills only load in trusted folders.

### Claude Code plugin marketplace

This repo is also a Claude Code plugin marketplace with two plugins: `design-taste` (English) and `design-taste-zh` (Chinese).

```text
/plugin marketplace add linkxzhou/design-taste
/plugin install design-taste@design-taste        # or design-taste-zh@design-taste
```

Install only one of the two editions.

### skills.sh CLI

```bash
npx skills add https://github.com/linkxzhou/design-taste/tree/main/en/design-taste
```

Both editions share the skill name, so point at the edition path instead of using `--skill design-taste`.

## Requirements

- Python 3.9+ for the scripts.
- `review_site.py`: `playwright` and Chromium. `review_image.py`: `pillow` and `numpy` (OpenCV is used only if it is already installed).
- The instruction files need nothing extra.

## Credits and sources

The skill is an original synthesis written in our own words. It draws ideas from Anthropic's skills (frontend-design, canvas-design, theme-factory), taste-skill, impeccable, ui-ux-pro-max, oil-ui, ClaudeKit, research on image aesthetics (AVA, NIMA, LAION, Q-Align and others), and game-art guidance from Steamworks, Apple, Riot and GDC talks. Full list with URLs and licenses: [`en/design-taste/references/sources.md`](en/design-taste/references/sources.md).

Benchmark scores are heuristics from crawls done in October 2026. Websites change, so treat them as comparisons rather than absolute grades.

## License

[MIT](LICENSE) © 2026 linkxzhou. Third-party projects listed in `sources.md` keep their own licenses.
