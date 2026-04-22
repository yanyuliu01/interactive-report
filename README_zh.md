<div align="right">

[English](README.md) | **中文**

</div>

<div align="center">

# Interactive Report

**一句话生成杂志级交互式 HTML 报告**

一个 Prompt，一个自包含 HTML 文件，零依赖。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/yanyuliu01/interactive-report/pulls)

[为什么需要](#为什么需要) · [快速开始](#快速开始) · [效果展示](#效果展示) · [组件库](#组件库) · [贡献指南](#贡献指南)

</div>

---

## 为什么需要

| 你的痛点 | 现在的做法 | 用了这个 Skill 之后 |
|:---|:---|:---|
| 做数据看板 | Tableau ($75/月)、Power BI、帆软 FineBI | 一句话 → 生产级 HTML 报表 |
| 写研究报告 | Notion + 手画图表 + 2小时排版 | 一句话 → 杂志排版 + 交互图表 |
| SWOT / 竞品分析 | Miro ($8/月) + Google Docs | 一句话 → 交互框架 + 策略联动 |
| 整理会议纪要 | 飞书/钉钉里贴纯文本 | 一句话 → 议题标签页 + 待办追踪 + 时间线 |
| 论文精读 | LaTeX 或者纯 Markdown | 一句话 → 概念图 + 公式块 + 作者卡片 |

**它不是仪表盘生成器，而是一个 AI 原生的出版工具。**

输出效果对标《经济学人》和麦肯锡季刊 —— 单栏叙事排版、三字体视觉层级、交互组件嵌入阅读流。

## 特性

- **单文件输出** — 一个 `.html` 文件，浏览器直接打开，无需服务器
- **7 种场景模板** — 框架分析、数据洞察、会议纪要、竞品对比、财务研究、论文精读、通用
- **双主题切换** — Warm（奶白纸质感）适合研究内容，Cool（深色科技感）适合数据报告
- **20+ 组件库** — KPI 卡片、Chart.js 图表、可排序表格、标签页、滑块、SVG 结构图、风险矩阵、时间线
- **三字体系统** — 衬线标题 + 无衬线正文 + 等宽标签 = 自动视觉层级
- **零外部依赖** — 唯一可选 CDN 为 Chart.js (`4.4.1`)，其余全部 vanilla HTML/CSS/JS
- **可组合** — 支持被其他 Skill 作为下游渲染引擎调用
- **中文友好** — 原生支持中日韩排版，PingFang SC / Songti SC 字体栈

## 快速开始

### 1. 安装

```bash
# 克隆仓库，把 skill 复制到你的 Claude Code 目录
git clone https://github.com/yanyuliu01/interactive-report.git
cp -r interactive-report/.claude ~/
```

或者手动操作：把 `.claude/skills/interactive-report/` 文件夹复制到你项目的 `.claude/skills/` 目录下。

### 2. 使用

直接用自然语言告诉 Claude 你想做什么，Skill 会自动触发：

```
帮我做一个黄金价格的监控报表

帮我整理一下这份销售数据，生成分析报告

对比一下 React, Vue, Svelte 三个框架

帮我精读这篇 Attention Is All You Need 论文

总结一下今天的会议纪要

做一个 SWOT 分析
```

**触发关键词：** `总结` `分析` `整理` `梳理` `生成报告` `summarize` `analyze` `compare`

### 3. 输出

一个 `.html` 文件生成到项目目录，用任何浏览器打开即可。

## 效果展示

### 数据洞察 — 黄金价格监控
> Prompt: *"帮我生成一个黄金价格的监控报表"*

KPI 指标卡片、Chart.js 折线图（Tab 切换）、驱动因素分段条、SVG 关系图、可排序多渠道价格表、机构预测柱图 + 风险矩阵。

### 框架分析 — SWOT
> Prompt: *"帮我做个 SWOT 分析"*

四象限交互卡片，勾选驱动策略联动，拖拽排序优先级，自定义 SVG 定位图。

### 竞品对比
> Prompt: *"对比一下这三个产品"*

雷达图、可排序星级评分矩阵（行可展开看详情）、分场景推荐标签页 + 结论卡片。

### 财务研究
> Prompt: *"分析一下平安保险"*

财务快照指标卡、业务分段条、Chart.js 组合图、PEV 估值滑块模拟器、多空风险矩阵。

## 组件库

完整的设计系统 + 20+ 可复用组件：

### 布局组件
| 组件 | 说明 |
|:---|:---|
| **Hero** | 标题 + 副标题 + 元数据标签 |
| **Section Label** | 编号分隔线（`01 ·`、`02 ·`），创造阅读节奏 |
| **Widget Frame** | macOS 风格圆点标题栏，包裹所有交互元素 |
| **Footer + 水印** | 来源说明 + 作者署名 |

### 内容组件
| 组件 | 说明 |
|:---|:---|
| **Metric Cards** | 数字高亮卡片网格，语义化配色 |
| **Callout Box** | 强调框（紫色/绿色/琥珀色/红色四种变体） |
| **Segmented Bar** | 水平堆叠条，展示构成比例 |
| **Badges** | 行内状态标签 |
| **Formula Block** | 深色背景公式/代码展示块 |

### 交互组件
| 组件 | 说明 |
|:---|:---|
| **Tabs** | 胶囊式标签页导航，作用域隔离 |
| **Sortable Table** | 点击表头排序 + 行展开看详情 |
| **Slider** | 滑块输入，实时联动计算值 |
| **Chart.js** | 柱状图、折线图、雷达图、环形图、组合图 |

### 卡片与图表
| 组件 | 说明 |
|:---|:---|
| **Comparison Grid** | A vs B 对比卡片，高亮推荐项 |
| **Risk Grid** | 多空/风险 两列布局 |
| **People Cards** | 头像卡片网格（团队/作者） |
| **Timeline** | 垂直时间线（重大事件 + 普通事件） |
| **SVG Patterns** | 5 种可复用结构图模板（关系图、流程图、分层图、三角模型、对比图） |

## 项目结构

```
.claude/skills/interactive-report/
├── SKILL.md                          # Skill 主定义文件
└── references/
    ├── design-system.md              # CSS 变量、主题、排版规则
    ├── templates.md                  # 各场景组装指南
    └── components/
        ├── INDEX.md                  # 组件索引和加载指引
        ├── layout.md                 # Hero、Section Label、Widget Frame、Footer
        ├── content.md                # Callout、Metrics、Badges、Segmented Bar
        ├── interactive.md            # Tabs、Slider、Sortable Table、Chart.js
        ├── cards.md                  # 对比卡片、风险矩阵、人物卡片、链接卡片、时间线
        └── svg-patterns.md           # 5 种 SVG 结构图模板
```

## 设计理念

> **内容是主角，交互是配角。**

这个 Skill 生成的是*出版物*，不是仪表盘。正确的心智模型是**排版一篇杂志文章**，而不是搭建一个 Web 应用。

核心原则：

1. **单栏阅读流**（最大宽度 780px）— 绝不做多面板仪表盘
2. **叙事弧线** — Hero → 背景 → 分析 → 证据 → 结论
3. **交互嵌入叙事** — 图表跟在引出它的段落后面，而不是反过来
4. **结构用 SVG，数据用 Chart.js** — 概念性的关系、流程画 SVG；有数轴的数据用 Chart.js
5. **每个章节都有实质内容** — 没有 2-3 句上下文铺垫，就不放交互组件

## 自定义

### 切换主题

告诉 Claude 你想要哪个主题：

- **Warm**（默认） — 奶白纸质感，适合研究/咨询类内容 → `#F7F5F0`
- **Cool** — 深色背景，适合技术/数据类内容 → `#101117`

### 修改水印

Footer 会自动包含水印。编辑 `.claude/skills/interactive-report/references/components/layout.md` 修改链接：

```html
<div class="watermark">
  Made by <a href="https://github.com/your-username">@your-username</a>
</div>
```

### 扩展组件

在 `references/components/` 下新建组件文件，然后在 `INDEX.md` 中注册。Skill 会自动识别。

## 兼容平台

支持所有兼容 Claude Skills 的 AI 编码工具：

- **Claude Code**（CLI & VS Code 扩展）
- Cursor / Windsurf / VS Code + Claude
- 任何支持 `.claude/skills/` 约定的工具

## 贡献指南

欢迎贡献！以下方向特别需要帮助：

- 新场景模板（如产品说明书、更新日志、教程）
- 新 SVG 结构图模板
- 无障碍 (Accessibility) 改进
- 更多语言的国际化支持

请先开一个 Issue 讨论你想做的改动。

## 许可证

[MIT](LICENSE) — 随便用。

---

<div align="center">

**如果这个 Skill 帮到了你，欢迎点个 ⭐**

Made by [@yanyuliu01](https://github.com/yanyuliu01)

</div>
