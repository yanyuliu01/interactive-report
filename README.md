<div align="right">

**English** | [中文](README_zh.md)

</div>

<div align="center">

# Interactive Report

**Turn any analysis into a magazine-quality interactive HTML document.**

One prompt. One self-contained HTML file. Zero dependencies.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/yanyuliu01/interactive-report/pulls)

[Features](#features) · [Quick Start](#quick-start) · [Gallery](#gallery) · [Components](#components) · [Contributing](#contributing)

</div>

---

## Why this skill?

| Pain Point | What you do today | With Interactive Report |
|:---|:---|:---|
| Making a data dashboard | Tableau ($75/mo), Power BI, FineBI | One prompt → production-ready HTML |
| Writing a research report | Notion + manual charts + 2 hours | One prompt → editorial layout with interactive charts |
| SWOT / competitive analysis | Miro ($8/mo) + Google Docs | One prompt → interactive framework with linked strategies |
| Meeting summary | Plain text in Feishu/Slack | One prompt → topic tabs + action items + timeline view |
| Paper review | LaTeX or plain markdown | One prompt → concept diagrams + formula blocks + author cards |

**It's not a dashboard builder. It's an AI-native publishing tool.**

The output reads like *The Economist* or *McKinsey Quarterly* — single-column editorial flow, three-typeface typography, interactive widgets woven into narrative prose.

## Features

- **Single-file output** — One `.html` file, open anywhere, no server needed
- **7 scene types** — Framework analysis, data insight, meeting notes, competitive comparison, financial research, paper review, general
- **Two themes** — Warm (cream paper) for editorial content, Cool (dark) for tech/data
- **Rich component library** — KPI cards, Chart.js graphs, sortable tables, tabs, sliders, SVG diagrams, risk grids, timelines
- **Three-typeface system** — Serif headings + sans-serif body + monospace labels = instant visual hierarchy
- **Zero external dependencies** — Only optional CDN is Chart.js (`4.4.1`), everything else is vanilla HTML/CSS/JS
- **Composable** — Other skills can call it as a downstream rendering engine
- **CJK-ready** — Full Chinese/Japanese/Korean typography support out of the box

## Quick Start

### 1. Install

```bash
# Clone into your Claude Code skills directory
git clone https://github.com/yanyuliu01/interactive-report.git
cp -r interactive-report/.claude ~/
```

Or manually: copy the `.claude/skills/interactive-report/` folder into your project's `.claude/skills/` directory.

### 2. Use

Just tell Claude what you need — the skill triggers automatically on keywords like:

| Language | Trigger phrases |
|:---|:---|
| English | "summarize", "analyze", "generate a report", "compare X vs Y" |
| 中文 | "总结", "分析", "整理", "帮我梳理", "做一个分析", "生成报告" |

**Examples:**

```
帮我做一个黄金价格的监控报表

Analyze this sales data and generate an interactive report

对比一下 React, Vue, Svelte 三个框架

帮我精读这篇 Attention Is All You Need 论文

整理一下今天的会议纪要
```

### 3. Output

A single `.html` file lands in your project directory. Open it in any browser.

## Gallery

### Data Insight — Gold Price Monitor
> Prompt: *"帮我生成一个黄金价格的监控报表"*

KPI metric cards, Chart.js trend lines with tab switching, segmented driver analysis bar, SVG hub-spoke relationship diagram, sortable multi-channel price table, institutional forecast chart with risk grid.

### Framework Analysis — SWOT
> Prompt: *"帮我做个 SWOT 分析"*

Interactive four-quadrant cards with checkbox-driven strategy linkage, drag-and-drop priority sorting, custom SVG positioning diagram.

### Competitive Comparison
> Prompt: *"对比一下这三个产品"*

Radar chart, sortable star-rating matrix with expandable detail rows, tabbed scenario recommendations with verdict cards.

### Financial Research
> Prompt: *"分析一下平安保险"*

Metric card dashboard, segmented profit composition bar, Chart.js combo charts, PEV slider simulator, bull-vs-bear risk grid.

## Components

The skill ships with a complete design system and 20+ reusable components:

### Layout
| Component | Description |
|:---|:---|
| **Hero** | Title + subtitle + metadata tags |
| **Section Label** | Numbered dividers (`01 ·`, `02 ·`) for reading rhythm |
| **Widget Frame** | macOS-style dotted header wrapping any interactive element |
| **Footer + Watermark** | Source attribution + author credit |

### Content
| Component | Description |
|:---|:---|
| **Metric Cards** | Grid of highlight numbers with semantic colors |
| **Callout Box** | Accent / teal / amber / red variants for emphasis |
| **Segmented Bar** | Horizontal stacked bar for composition |
| **Badges** | Inline status labels (green / amber / red) |
| **Formula Block** | Dark-background code/math display |

### Interactive
| Component | Description |
|:---|:---|
| **Tabs** | Pill-style tab navigation, scoped to widget |
| **Sortable Table** | Click-to-sort headers + expandable detail rows |
| **Slider** | Range input with live-updating derived values |
| **Chart.js** | Bar, line, radar, doughnut, combo — with standard config |

### Cards & Diagrams
| Component | Description |
|:---|:---|
| **Comparison Grid** | A-vs-B cards with highlight border |
| **Risk Grid** | Bull-vs-bear two-column layout |
| **People Cards** | Avatar grid for team/authors |
| **Timeline** | Vertical dot timeline with major/minor events |
| **SVG Patterns** | 5 reusable diagram templates (hub-spoke, flow, block, triangle, comparison) |

## Project Structure

```
.claude/skills/interactive-report/
├── SKILL.md                          # Main skill definition
└── references/
    ├── design-system.md              # CSS variables, themes, typography
    ├── templates.md                  # Scene-specific assembly guides
    └── components/
        ├── INDEX.md                  # Component loading guide
        ├── layout.md                 # Hero, Section Label, Widget Frame, Footer
        ├── content.md                # Callout, Metrics, Badges, Segmented Bar
        ├── interactive.md            # Tabs, Slider, Sortable Table, Chart.js
        ├── cards.md                  # Comparison, Risk, People, Links, Verdict, Timeline
        └── svg-patterns.md           # 5 reusable SVG diagram patterns
```

## Design Philosophy

> **Content is the protagonist. Interaction is the supporting actor.**

This skill generates *publications*, not dashboards. The mental model is **typesetting a magazine article**, not building a web app.

Key principles:

1. **Single-column reading flow** (max 780px) — never a multi-panel dashboard
2. **Narrative arc** — Hero → Context → Analysis → Evidence → Conclusion
3. **Interactions embedded in prose** — a chart follows a paragraph that introduces it
4. **Custom SVG over generic charts** — when the concept is structural, draw it
5. **Every section has substance** — no widget without 2-3 sentences of context

## Customization

### Switch Theme

Tell Claude which theme you want:

- **Warm** (default) — cream paper, editorial feel → `#F7F5F0`
- **Cool** — dark background, tech feel → `#101117`

### Add Your Watermark

The footer automatically includes a watermark. Edit `.claude/skills/interactive-report/references/components/layout.md` to change the link:

```html
<div class="watermark">
  Made by <a href="https://github.com/your-username">@your-username</a>
</div>
```

### Extend Components

Add new component files to `references/components/` and register them in `INDEX.md`. The skill will pick them up automatically.

## Compatible Platforms

Works with any AI coding tool that supports Claude skills:

- **Claude Code** (CLI & VS Code extension)
- Cursor / Windsurf / VS Code + Claude
- Any tool supporting `.claude/skills/` convention

## Contributing

Contributions are welcome! Areas where help is especially appreciated:

- New scene type templates (e.g., product spec, changelog, tutorial)
- Additional SVG diagram patterns
- Accessibility improvements
- Internationalization (i18n) for more languages

Please open an issue first to discuss what you'd like to change.

## License

[MIT](LICENSE) — use it however you want.

---

<div align="center">

**If this skill saves you time, consider giving it a ⭐**

Made by [@yanyuliu01](https://github.com/yanyuliu01)

</div>
