# design-taste

[English](README.md) · **简体中文**

一个给编程 Agent 的“设计审美”技能：先做有意图的视觉决策，控制 token 数量，建立强层级，避开模板化的 “AI slop” 观感。同时附带脚本和基准数据，可以给线上网站、图片和游戏美术打分。

提供两个可独立使用、逻辑一致的版本：

| 版本 | 路径 | 默认报告语言 |
|---|---|---|
| English | [`en/design-taste/`](en/design-taste/) | 英文（`--lang zh` 输出中文） |
| 简体中文 | [`zh/design-taste/`](zh/design-taste/) | 中文（`--lang en` 输出英文） |

每个 Agent 只安装**一个**版本。两个版本的技能名都是 `design-taste`。

## 功能

| 模式 | 用途 |
|---|---|
| **Create（创建）** | 新页面、应用、组件：先定方向，再建三层 token 体系 |
| **Audit（审查）** | 可量化的 UI 评审（颜色/字号/圆角/阴影计数、对比度、状态），输出 P0/P1/P2 |
| **Redesign（重设计）** | 在不破坏行为的前提下升级现有 UI，token 先行 |
| **Minimalist（极简）** | 暖色单色编辑风格叠加层（Notion/Linear 式的沉静） |
| **Theme（主题）** | 幻灯片、文档、报告的配色与字体搭配 |
| **Artifact（视觉作品）** | 海报、封面、静态艺术（哲学 → 画布） |
| **Site Review（网站评审）** | 用 Playwright 抓取 URL、计算指标，按 45% 指标 + 55% 视觉打分并与同行对标 |
| **Image Review / Restyle（图片评审/重制）** | 给照片、产品图、海报、科研配图、AI 图片打分；配色提取、重制配方、反 slop 提示词 |
| **Game Art Review（游戏美术评审）** | 截图、主视觉、Steam 胶囊图、图标、HUD、概念图、精灵图；11 维量表 + 21 个品类档案 |

## 亮点

- **147 家公司官网的基准数据**（全球市值前 100 + 科技前 100），使用与脚本相同的公式打分。包含前 10 拆解、前 20 vs 后 20 指标目标、行业打法和常见错误（`references/benchmarks.md`、`scripts/benchmarks.csv`）。
- **游戏品类量表**：11 个维度 × 资产类型权重、21 个品类档案（MOBA、射击、二次元抽卡、像素、武侠、水墨…）、Steam/App Store 规则、灰度/剪影/缩略图测试。
- **脚本自身不做任何下载**：
  - `scripts/review_site.py`：Playwright 抓取（桌面 + 移动）、设计指标、首屏主图分析、`report.md` 骨架。
  - `scripts/review_image.py`：Pillow + numpy 指标（配色、和谐、影调、锐度、噪点、构图、留白）以及游戏指标（明度分档、图底、HUD 覆盖、商店缩略图可读性）。
- 针对 UI、图片和游戏美术的**反 slop 清单**。

## 快速使用

直接用自然语言告诉 Agent：

```text
帮我做一个精品咖啡烘焙店的落地页，单个 HTML 文件。
帮我审查一下这个 React 项目 src 目录下的 UI 质量，给出 P0/P1/P2 清单。
评审一下 https://example.com，并和 Software/Cloud 行业对标。
帮我评审一下这张 AI 生成的海报 poster.png，告诉我该怎么改。
帮我做一下这张 MOBA 团战截图的美术评审，重点看可读性和 HUD。
```

也可以直接运行脚本（路径相对于技能目录）：

```bash
# 网站评审（Playwright 一次性安装）
pip install playwright && python3 -m playwright install chromium
python3 scripts/review_site.py https://example.com --industry Software/Cloud --mobile --out review-example

# 图片 / 游戏美术评审
pip install pillow numpy
python3 scripts/review_image.py poster.png --type poster
python3 scripts/review_image.py shot.png --type game-screenshot --genre moba
python3 scripts/review_image.py --list-genres
python3 scripts/review_image.py photo.jpg --lang en   # 英文报告骨架
```

## 安装

先克隆一次，再把**一个**版本复制（或软链接）到 Agent 的技能目录。下面以中文版 `zh` 为例，英文版把 `zh` 换成 `en`。

```bash
git clone --depth 1 https://github.com/linkxzhou/design-taste.git ~/design-taste
```

| Agent | 用户级（所有项目） | 项目级 |
|---|---|---|
| Claude Code | `~/.claude/skills/` | `.claude/skills/` |
| OpenAI Codex CLI | `~/.agents/skills/`（旧路径 `~/.codex/skills/` 仍可读取） | `.agents/skills/` |
| Cursor | `~/.cursor/skills/` 或 `~/.agents/skills/`（也会读取 `~/.claude/skills/`、`~/.codex/skills/`） | `.cursor/skills/` 或 `.agents/skills/` |
| CodeBuddy | `~/.codebuddy/skills/` | `.codebuddy/skills/` |
| Gemini CLI | `~/.gemini/skills/` 或 `~/.agents/skills/` | `.gemini/skills/` 或 `.agents/skills/` |
| 其他（遵循 Agent Skills 标准） | 对应 Agent 的技能目录 | — |

一行命令（用户级）：

```bash
# Claude Code
mkdir -p ~/.claude/skills && cp -R ~/design-taste/zh/design-taste ~/.claude/skills/
# OpenAI Codex CLI，以及所有读取 ~/.agents/skills 的 Agent（Cursor、Gemini CLI）
mkdir -p ~/.agents/skills && cp -R ~/design-taste/zh/design-taste ~/.agents/skills/
# Cursor
mkdir -p ~/.cursor/skills && cp -R ~/design-taste/zh/design-taste ~/.cursor/skills/
# CodeBuddy
mkdir -p ~/.codebuddy/skills && cp -R ~/design-taste/zh/design-taste ~/.codebuddy/skills/
# Gemini CLI
mkdir -p ~/.gemini/skills && cp -R ~/design-taste/zh/design-taste ~/.gemini/skills/
```

把 `cp` 换成 `ln -s ~/design-taste/zh/design-taste ~/.claude/skills/design-taste`，之后用 `git -C ~/design-taste pull` 即可更新。安装后重启 Agent（Codex、Cursor），Gemini CLI 中执行 `/skills reload`。Gemini CLI 的工作区技能只在受信任的目录中加载。

### Claude Code 插件市场

本仓库同时是一个 Claude Code 插件市场，包含两个插件：`design-taste`（英文）和 `design-taste-zh`（中文）。

```text
/plugin marketplace add linkxzhou/design-taste
/plugin install design-taste-zh@design-taste      # 英文版：design-taste@design-taste
```

两个版本只装一个。

### skills.sh CLI

```bash
npx skills add https://github.com/linkxzhou/design-taste/tree/main/zh/design-taste
```

两个版本技能名相同，因此请指向具体版本的路径，而不是用 `--skill design-taste`。

## 环境要求

- 脚本需要 Python 3.9+。
- `review_site.py`：`playwright` 与 Chromium。`review_image.py`：`pillow` 与 `numpy`（仅在已安装时使用 OpenCV）。
- 说明文档本身无需任何依赖。

## 致谢与来源

本技能是用我们自己的话写成的原创综合。思路来自 Anthropic 的技能（frontend-design、canvas-design、theme-factory）、taste-skill、impeccable、ui-ux-pro-max、oil-ui、ClaudeKit，图片审美研究（AVA、NIMA、LAION、Q-Align 等），以及 Steamworks、Apple、Riot 和 GDC 演讲中的游戏美术指导。完整列表（含 URL 与许可）：[`zh/design-taste/references/sources.md`](zh/design-taste/references/sources.md)。

基准分数是 2026 年 10 月抓取得到的启发式结果。网站会变化，请把它们当作横向比较，而不是绝对评级。

## 许可

[MIT](LICENSE) © 2026 linkxzhou。`sources.md` 中列出的第三方项目保留各自的许可。
