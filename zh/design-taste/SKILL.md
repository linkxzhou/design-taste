---
name: design-taste
description: 设计审美指南，让视觉产出显得有意图，而不是模板化的“AI slop”。用于设计、搭建、重做风格、重新设计、打磨、点评或审查 UI（网页、落地页、仪表盘、App 界面、组件），建立设计 token，挑选配色/字体/间距，给幻灯片/文档做主题，做极简风格，评审/对标线上网站 URL，评审或重制图片（照片、产品图、海报、横幅、插画、科研配图、AI 图片——构图、配色、AI 痕迹），评审游戏美术（截图、主视觉、Steam 胶囊图、图标、HUD、概念图、精灵/像素图；品类可读性），或制作海报/封面。触发词：设计界面、美化页面、界面评审、UI 审查、重新设计、改版、设计规范、配色、字体搭配、极简风格、主题、海报、网站评审、官网改版、对标、图片审美、图片评审、海报评审、配色提取、构图、科研配图、AI 图片评价、游戏美术、游戏审美、游戏 UI、二次元、像素、游戏截图评审；English keywords - UI design, redesign, design tokens, website review, image critique, game art review, RPG, MOBA. 不用于没有可见变化的后端逻辑或代码清理。
license: MIT
---

# 设计审美（Design Taste）

先做有意图的视觉决策，再一致地执行。这里的“审美”指：**一个清晰的方向、少量精选的 token、强烈的层级、没有默认感的填充物。**

按顺序执行下面的步骤。所有模式都先走第 0–2 步，然后走**构建路径（B3–B6）**或**评审路径（R3–R6）**，最后是**报告步骤**。步骤编号只用于你自己跟踪进度，不要写进交付给用户的内容。

## 第 0 步 —— 接收需求，选择模式

- **做什么：** 读需求和现有材料（代码、URL、图片、截图），从下表选一个主模式，外加可选的风格叠加。
- **产出：** 主模式、叠加风格、路径（构建或评审）、要加载的参考文件。
- **判定：** 要创建或修改可见的东西 → 构建路径；只点评、打分或对标 → 评审路径。Redesign 先把评审路径 R3–R6 当作审查，再走构建路径。叠加风格（Minimalist）不改变路径，在第 2 步应用、在 B5 检查。需求没有可见产出（后端逻辑、纯代码清理）→ 停止，本技能不适用。

| 用户意图 | 模式 | 路径 | 加载 | 模式专属步骤 |
|---|---|---|---|---|
| 搭建新页面/应用/组件 | **Create（创建）** | 构建 | `references/direction.md`、`references/principles.md`、`references/tokens.md` | 按 B3–B6 执行 |
| “评审 / 审查 / 这个 UI 哪里不好” | **Audit（审查）** | 评审 | `references/audit.md` | `audit.md` §1 检查 → §2 清单 → §3 报告 |
| “重新设计 / 升级 / 打磨 / 做得高级点” | **Redesign（重设计）** | 评审 → 构建 | 先 `references/audit.md` 再 `references/redesign.md` | `redesign.md` 流程 1–9（R3–R6 = 其第 2 步；B3–B6 = 其第 4–9 步） |
| “极简 / 干净 / 编辑感 / 像 Notion” | **Minimalist（极简，风格叠加）** | 同主模式 | `references/minimalist.md` | 在第 2 步（调性）和 B3（token）应用规格，在 B5 检查 |
| 需要外观的幻灯片、文档、报告、HTML 讲义 | **Theme（主题）** | 构建 | `references/theming.md` | `theming.md` 的主题配方驱动 B3–B4 |
| 海报、封面、静态艺术（PNG/PDF） | **Artifact（视觉作品）** | 构建 | `references/artifacts.md` | `artifacts.md` 的“哲学 → 画布”流程驱动 B4 |
| “评审 / 打分 / 美化这个网站 URL”、与竞品对标（评审网站、网站美化、对标） | **Site Review（网站评审）** | 评审 | `references/site-review.md`、`references/benchmarks.md`，运行 `scripts/review_site.py` | `site-review.md` §1 抓取 → §2 评分 → §3 对比 → §4 报告（§5 批量） |
| “给这张图打分 / 点评 / 哪里不好”、海报或封面评审、AI 图片点评（图片审美、图片评审、海报评审、AI 图片评价、构图） | **Image Review（图片评审）** | 评审 | `references/image-aesthetics.md`，运行 `scripts/review_image.py <img> --type …` | R3 脚本指标（§6）→ R4 8 维度 × 类型权重（§1–2）+ AI 清单（§4）→ R6 严重度（§3）→ 报告（§7） |
| 游戏截图 / 主视觉 / Steam 胶囊图 / 图标 / HUD / 概念图 / 精灵图评审，品类美术方向（游戏美术、游戏审美、游戏 UI、游戏截图评审、RPG、MOBA、二次元、像素） | **Game Art Review（游戏美术评审）** | 评审 | `references/game-aesthetics.md`、`references/game-workflows.md`，运行 `scripts/review_image.py <img> --type game-screenshot\|key-art\|capsule\|icon\|game-ui\|concept\|sprite --genre <g>` | `game-workflows.md` §1（分步）→ §2 报告；修改配方见 §3 |
| “把这张照片做成杂志页 / 产品主图 / 海报”、提取配色、图像模型提示词、科研配图（配色提取、科研配图） | **Image Restyle（图片重制）** | 构建 | `references/image-workflows.md`（+ 用 `image-aesthetics.md` 做前后打分） | `image-workflows.md` §1 四步流程 = B3–B4；§3 重制循环 = B6 |

模式可以组合（如 Redesign + Minimalist）。只读你需要的文件。

## 第 1 步 —— 收集上下文

- **做什么：** 弄清技术栈、CSS 方案、组件库、现有 token 或设计系统、品牌资产和约束（无障碍等级、性能预算）。截图或运行对应脚本拿到基线数据：URL 用 `scripts/review_site.py`，图片用 `scripts/review_image.py --type … [--genre …]`。本中文版脚本默认生成中文报告；用户用英文时传 `--lang en`。
- **产出：** 一段简短的上下文记录 + 基线指标（或注明“无工具，仅凭目测”）。
- **完成条件：** 知道现有什么、哪些必须保留。缺少必需材料（没有 URL、图片或代码）时，先向用户要，再继续。

## 第 2 步 —— 确定方向

- **做什么：** 在构建或打分之前写 3–5 行（给自己或用户）：
  1. **目的与受众** —— 这个界面为谁完成什么任务？
  2. **调性** —— 选一个具体立场（如编辑、粗野主义、柔和/有机、技术/高密度、奢华/安静、活泼、复古工业）。“简洁现代”不是方向。叠加风格在这里应用。
  3. **记忆点** —— 让人记住的那一件事（一组字体搭配、一块大胆色域、一个不寻常的网格、一个动效瞬间）。
  4. **约束** —— 现有品牌、框架、无障碍等级、性能预算。
  5. **密度** —— 疏朗的营销页 vs. 密集的工具。仪表盘 ≠ 落地页。
- **评审路径：** 写出“感知到的方向”（作品看起来想达到什么），作为打分的标尺。
- **产出：** 方向块（模板见 `references/direction.md` §5）。
- **完成条件：** 写明了一个调性和一个记忆点。项目已有设计系统时，方向就是*“把它用好”*，不要再发明第二套。

## 构建路径（Create、Redesign、Theme、Artifact、Image Restyle）

### B3 —— 先定 token
- **做什么：** 为颜色、字体、间距、圆角、阴影、动效定义小的命名尺度，写成 CSS 变量 / 主题配置（三层体系见 `references/tokens.md`）。Redesign：把现有字面量收拢进来。Minimalist：用 `minimalist.md` 的数值。
- **产出：** token 文件或主题块。
- **完成条件：** 数量符合“约束”一节（约 1 个强调色、1–2 种字体、≤ 6–8 个字号、一个圆角族、≤ 3 级阴影）。

### B4 —— 执行
- **做什么：** 在用户的技术栈中实现真实可运行的代码（或作品），遵循既有约定。按全局层 → 组件（全部状态）→ 布局的顺序构建，只用 token。投入与方向匹配：繁复的设计需要精细的执行，极简的设计需要间距和字体上的精确。按表中模式专属步骤执行（`redesign.md` 5–8、主题配方、作品流程、图片流程）。
- **产出：** 改动的文件 / 渲染出的作品。
- **完成条件：** 需求范围全部完成；token 之外没有字面量颜色或尺寸。

### B5 —— 对照约束自检
- **做什么：** 逐条对照下面的“约束”一节（核心规则 + AI slop 指纹），以及叠加风格的规格。
- **产出：** 违规清单。
- **判定：** 有违规 → 回 B4 修正后再检查；没有 → B6。

### B6 —— 验证
- **做什么：** 运行 `references/audit.md` 中的快速检查（十六进制颜色、字号、圆角数量；对比度；状态；约 375/768/1280px 的响应式）。能渲染就截图看一看。运行现有测试/构建。Redesign 和 Image Restyle 重新运行第 1 步的脚本，对比前后数据。
- **产出：** 带数字的检查结果。
- **判定：** 数量在限制内、无对比度不合格、无 P0、看起来不普通也不杂乱 → 报告步骤；否则回 B4。

## 评审路径（Audit、Site Review、Image Review、Game Art Review；Redesign 的审查部分）

### R3 —— 测量
- **做什么：** 运行该模式的可量化检查：`audit.md` §1 的 grep 计数、`review_site.py` 指标，或 `review_image.py` 指标（游戏另加灰度/缩略图测试）。
- **产出：** 指标表。
- **完成条件：** 报告模板要求的每个指标都有数字，或注明“无法测量”及原因。

### R4 —— 打分
- **做什么：** 亲自看作品，用该模式的量表打分：`audit.md` §2 清单、`site-review.md` §2（45/55）、`image-aesthetics.md` 8 维度 × 类型权重 + AI 清单，或 `game-aesthetics.md` G1–G11 × 资产权重 + 品类档案。按参考文件的方式合成指标分与视觉分（如图片为 0.4 指标 + 0.6 视觉）。
- **产出：** 逐维度分数，每项附具体证据（“左下角手指 6 根”，而不是形容词）。
- **完成条件：** 每个维度都有分数和证据；有 P0 时按量表规定封顶总分。

### R5 —— 对比（仅 Site Review 和 Game Art Review；其他模式跳过）
- **做什么：** 对照 `benchmarks.md` / `benchmarks.csv` 或品类档案及指定竞品。
- **产出：** 指标 vs 基准表 + 2–3 条结论。
- **完成条件：** 每个差距都写明没达到的基准值。

### R6 —— 排优先级
- **做什么：** 把发现整理成 P0/P1/P2 问题。每条包含：是什么、在哪里（file:line、屏幕区域或图片区域）、为什么重要、具体修法（token 值、HEX、裁切比例、提示词）。
- **产出：** 按优先级排列的问题清单。
- **完成条件：** 每条都有位置/原因/修法。Redesign → 进入 B3；其他评审模式 → 报告步骤。

## 最后一步 —— 报告

- **做什么：** 用用户的语言写报告。本中文版脚本默认生成中文 `report.md`（传 `--lang en` 可得英文骨架），替换其中每个 TODO。
  - 构建路径：用 2–4 行说明所选方向和取舍、改了什么、B6 的验证数据。
  - 评审路径：用该模式的报告模板（`audit.md` §3、`site-review.md` §4、`image-aesthetics.md` §7、`game-workflows.md` §2）。
- **产出：** 交付消息（以及生成的报告文件/截图）。
- **完成条件：** 每个结论都有 R3/R4 或 B6 的数字或观察作支撑；没验证过的东西不说成已检查。

## 约束（B5 自检）

### 核心规则（始终生效）
- **坚持。** 大胆的极简和大胆的繁复都可以；把一切取平均的畏缩设计不行。
- **用 token，不用字面量。** 每个颜色、尺寸、圆角、阴影和时长都来自一个小的命名尺度（见 `references/tokens.md`）。
- **数量克制：** 约 1 个强调色、1–2 种字体、≤ 6–8 个字号、一个圆角族、≤ 3 级阴影、一个缓动曲线族。
- **用尺寸、字重和空间的对比建立层级** —— 而不是更多的框、边框和颜色。
- **间距落在网格上**（4/8px 基准）。相关的东西紧挨，组与组之间大方分开。
- **无障碍也是审美的一部分：** 文字对比度 ≥ 4.5:1（大字 3:1）、焦点可见、触屏点击区 ≥ 44px、尊重 `prefers-reduced-motion`。
- **真实内容。** 不要“张三 / Acme / Lorem ipsum”，不要“赋能你的工作流”式文案，不要用 emoji 当图标。
- **每种状态都存在：** 悬停、焦点、按下、禁用、加载、空、错误。

### AI slop 指纹（除非需求明确要求，否则避免）
- 白底上的紫→蓝渐变；深色上的霓虹发光；到处都是渐变文字。
- 条件反射地用 Inter/Roboto/Arial；所有东西一个字重。
- 居中 Hero + 三张一样的图标卡片 + 通用 CTA 色带。
- 卡片套卡片；每个元素都装在带投影的圆角描边盒子里。
- 无缘无故的毛玻璃；随机的装饰性色块。
- 统一的 `rounded-2xl` + `shadow-lg`；圆角不一致。
- 虚假指标（“快 10 倍”“99.9%”）和图库式用户评价。
- 处处弹跳/弹性动画；对布局属性做动画。

细节与替代方案：`references/principles.md`。

## 参考文件地图

- `references/direction.md` —— 方向提问、风格目录、按风格选字体/配色。
- `references/principles.md` —— 色彩、字体、间距、圆角、阴影、动效、布局规则 + 反模式。
- `references/tokens.md` —— 三层 token 体系（原始 → 语义 → 组件）及示例。
- `references/audit.md` —— P0/P1/P2 清单、可量化检查、报告格式。
- `references/redesign.md` —— 现有项目的安全升级流程。
- `references/minimalist.md` —— 暖色单色编辑风格规格。
- `references/theming.md` —— 幻灯片/文档/报告主题；主题配方。
- `references/artifacts.md` —— 海报与静态视觉作品（哲学 → 画布）。
- `references/site-review.md` —— URL 评审流程：抓取 → 指标 → 45/55 评分 → P0/P1/P2 报告。
- `references/benchmarks.md` —— 顶级公司官网拆解、行业打法、指标目标、常见错误。
- `scripts/review_site.py` —— Playwright 抓取 + 指标分 + 报告骨架；`scripts/benchmarks.csv` —— 147 个已评分站点。
- `references/image-aesthetics.md` —— 图片量表：8 个维度 × 类型权重、P0/P1/P2、AI 痕迹清单、指标区间。
- `references/image-workflows.md` —— 解析 → 配色 → 版式 → 增强流程；纸刊/拼贴/产品/配色/封面配方；Nature 风格配图清单；反 slop 提示词模板。
- `scripts/review_image.py` —— Pillow+numpy 图片指标（配色、和谐、影调、锐度、噪点、色彩丰富度、三分/重心、留白）→ metrics.json、palette.png、thirds-overlay.png、report.md。
- `references/game-aesthetics.md` —— 游戏量表：11 个维度（可读性、明度、玩法清晰度、HUD、特效…）× 资产权重、21 个品类档案、9 个资产量表、AI 检查、指标区间。
- `references/game-workflows.md` —— 灰度/剪影/缩略图/2 秒测试、按品类解读指标、P0/P1/P2 报告、修改配方、反 slop 游戏美术提示词。
- `scripts/review_image.py --type <游戏类型> --genre <g>` —— 增加明度分档、图底、形状清晰度、HUD 覆盖、色数、商店缩略图可读性 → grayscale.png、thumbnail.png。
- `references/sources.md` —— 上游技能、URL 与许可。
