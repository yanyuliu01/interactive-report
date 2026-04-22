# Scene Templates & Assembly Guides

Each template defines the recommended section structure and component selection for a scene type.
These are starting points — adapt based on actual content needs.

## Table of Contents
1. [Framework Analysis](#framework)
2. [Data Insight](#data-insight)
3. [Meeting Summary](#meeting)
4. [Competitive Comparison](#comparison)
5. [Financial Research](#research)
6. [Paper Review](#paper)
7. [General / Catch-all](#general)

---

## 1. Framework Analysis (SWOT, Porter, BCG, etc.) {#framework}

**Typical length**: 5-6 sections

**Section blueprint**:
```
Hero: framework name, analysis target, date
01 · 分析背景: 1-2 paragraphs of context + callout with reading guide
02 · 框架四象限/五要素: widget-frame with collapsible cards per quadrant/force
    - Each card: clickable header → expandable body with point items
    - Point items: checkbox (for strategy linking) + drag handle (for priority sorting)
03 · 格局图解: custom SVG diagram showing the key insight visually
    - Example: "differentiation triangle", "competitive position map"
04 · 交叉策略矩阵: strategy cards that dynamically highlight based on checkbox selections
    - Use JS: track checked IDs → filter strategy rules → render matched strategies
05 · 核心判断: callout.teal with 3-4 sentence strategic conclusion
Footer
```

**Key components**: collapsible cards, checkboxes with JS linkage, drag-and-drop (HTML5 native), 
custom SVG, strategy grid with dynamic highlighting.

**JS pattern for checkbox-strategy linkage**:
```js
let checked = new Set();
function toggleCheck(id, el) {
  checked.has(id) ? checked.delete(id) : checked.add(id);
  el.classList.toggle('checked');
  renderStrategy(); // rebuild strategy section based on checked set
}
function renderStrategy() {
  // For each strategy rule, check if rule.need items overlap with checked set
  // Highlight fully-matched rules (all needs met) vs partially-matched
}
```

**Drag-and-drop pattern**: Use HTML5 `draggable="true"` with `dragstart`, `dragover`, `drop`, `dragend` 
events. Keep it within the same container (quadrant). Update rank numbers after drop.

---

## 2. Data Insight Dashboard {#data-insight}

**Typical length**: 4-5 sections

**Section blueprint**:
```
Hero: dataset description, time range, key dimensions
01 · 核心发现: 3-4 metric cards with key numbers + trend arrows
02 · 数据可视化: widget-frame with Chart.js
    - Tab 1: trend chart (line/bar)
    - Tab 2: composition chart (doughnut/stacked area)
    - Tab 3: comparison chart (grouped bar/radar)
    - Include filter controls (buttons, not dropdowns) above charts
    - After each chart, 1-2 sentence "洞察" callout
03 · 归因分析: comparison grid or risk grid showing drivers
04 · 结论与建议: callout.teal with actionable summary
Footer
```

**Key components**: metric cards, Chart.js (multiple chart types), filter buttons, callout boxes.

**Filter pattern**: Use button group with `.active` toggle. On click, update Chart.js datasets' 
`hidden` property and call `chart.update()`. Do NOT destroy and recreate charts for filters — 
use the built-in show/hide API.

**Chart.js tips for cross-model consistency**:
- Always provide the exact `new Chart(ctx, {...})` config pattern from components.md
- Set `responsive: true, maintainAspectRatio: false` and a fixed `height` on the canvas
- Use the FONT, GRID, TICK constants defined in components.md
- For dual-axis charts: define `yAxisID: 'y1'` on second dataset, add `y1` scale with `position: 'right'`

---

## 3. Meeting Summary {#meeting}

**Typical length**: 3-4 sections

**Section blueprint**:
```
Hero: meeting name, date, attendees, topic count + action item count
View toggle: [议题视图] [时间线视图] — two top-level views
  View A (议题视图):
    Tab nav: one tab per topic + "待办事项" tab
    Each topic tab: topic-card with discussion items (speaker + speech) and conclusion-box
    待办 tab: todo items with checkboxes, assignee, deadline, progress bar
  View B (时间线视图):
    timeline component with tags: [讨论] [决议] [待办]
Footer
```

**Key components**: view toggle (two buttons switching entire view), tabs, discussion items, 
conclusion boxes, todo checkboxes with progress tracking, timeline.

**View toggle pattern**:
```js
function switchView(view) {
  document.querySelectorAll('.view-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('view-tabs').style.display = view === 'tabs' ? '' : 'none';
  document.getElementById('view-timeline').style.display = view === 'timeline' ? '' : 'none';
}
```

**Meeting-specific CSS additions**:
```css
.discussion-item {
  display: flex; gap: 12px; padding: 10px 0;
  border-bottom: 1px solid var(--surface2); font-size: 14px;
}
.speaker { flex-shrink: 0; width: 56px; font-weight: 600; font-size: 13px; color: var(--accent); }
.speech { flex: 1; }
.conclusion-box {
  margin-top: 14px; padding: 12px 16px;
  background: var(--accent-light); border-radius: 8px; border-left: 3px solid var(--accent);
}
.todo-item {
  display: flex; align-items: flex-start; gap: 12px;
  padding: 14px 16px; background: var(--surface); border: 1px solid var(--border);
  border-radius: 8px; margin-bottom: 10px; transition: all .2s;
}
.todo-item.done { opacity: .55; background: var(--surface2); }
.todo-item.done .todo-text { text-decoration: line-through; }
```

---

## 4. Competitive Comparison {#comparison}

**Typical length**: 5-6 sections

**Section blueprint**:
```
Hero: what's being compared, how many products, dimension count
01 · 市场概况: brief context + one metric card per product (each product's #1 strength)
02 · 评分矩阵: widget-frame with sortable table
    - Filter controls: minimum star rating buttons
    - Sortable columns: click header to sort asc/desc
    - Expandable rows: click product name to show detail (pros/cons)
03 · 雷达图: widget-frame with Chart.js radar
    - Custom legend with click-to-toggle visibility
04 · 场景化推荐: widget-frame with tabs (one tab per use case)
    - Each tab: verdict-grid with "首选推荐" + "备选方案"
05 · 核心判断: callout.teal with balanced conclusion
Footer
```

**Key components**: sortable table, star ratings, filter buttons, Chart.js radar, tabs with 
verdict cards, custom legend.

**Product color convention**: Assign each product a distinct color. Use these consistently 
across the table, radar chart, and legends.

**Sortable table JS pattern**:
```js
let sortCol = null, sortDir = 1, minStar = 0;
function doSort(col) {
  if (sortCol === col) sortDir *= -1;
  else { sortCol = col; sortDir = -1; } // default: descending
  renderTable();
}
function setMin(n, btn) {
  minStar = n;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderTable();
}
```

---

## 5. Financial / Equity Research {#research}

**Typical length**: 6-7 sections

**Section blueprint**:
```
Hero: company name (with <em>), stock code, industry, key stat (total assets / market cap)
01 · 核心财务快照: 2 rows of metric cards (operating metrics + valuation metrics)
02 · 业务全景: segmented bar (profit composition) + tabs for each business line
    - Each tab: h3 title + paragraph + cmp-grid with key data and strategic direction
03 · 财务趋势: widget-frame with Chart.js
    - Tab 1: revenue + net income (bar + line combo)
    - Tab 2: business-specific metric trend (e.g., NBV for insurance, GMV for e-commerce)
04 · 商业生态/产业链: custom SVG hub-and-spoke diagram
05 · 估值分析: widget-frame with slider (e.g., PEV/PE simulator)
    - Slider adjusts target metric → dynamically computes target price, upside, yield
    - Below slider: scenario comparison cards (conservative vs optimistic)
06 · 风险与机会: risk-grid (bullish factors vs risk factors)
07 · 核心判断: callout.teal with investment thesis summary
Footer (with disclaimer: 不构成投资建议)
```

**Key components**: metric cards (2 rows), segmented bar, tabs, Chart.js (combo chart), 
custom SVG, slider simulator, risk grid, callout.

**PEV/PE slider pattern**:
```js
const ANCHOR_VALUE = 82.45; // e.g., embedded value per share
function updateSlider(v) {
  const multiplier = v / 100;
  const targetPrice = (ANCHOR_VALUE * multiplier).toFixed(1);
  const currentPrice = ANCHOR_VALUE * 0.70; // current market implied multiplier
  const upside = ((targetPrice - currentPrice) / currentPrice * 100).toFixed(1);
  // Update DOM elements
}
```

**Important**: Always include the disclaimer callout and footer note for financial content.

---

## 6. Paper Review / Summary {#paper}

**Typical length**: 5-6 sections

**Section blueprint**:
```
Hero: paper title (with <em> on key term), arXiv/venue, authors, key stat
01 · 要解决的问题: context paragraphs + SVG diagram showing the problem visually
    - callout.amber with the paper's core insight
02 · 核心方法: widget-frame with multi-tab deep dive
    - Tab per key concept: architecture diagram (SVG), mechanism explanation, formula
    - SVG diagrams should be CUSTOM to the paper's concepts, not generic
03 · 实验结果: metric cards + widget-frame with slider or comparison grid
    - If applicable: interactive parameter simulator
04 · 影响/后续: timeline showing the paper's influence on the field
05 · 作者: people-grid with brief bios
06 · 延伸阅读: links-grid to paper, code, related resources
Footer
```

**Key components**: custom SVG concept diagrams, formula blocks, tabs, metric cards, 
timeline, people cards, link cards.

**Paper-specific guidance**:
- The SVG diagrams are the most important part. A paper review without custom diagrams 
  explaining the core idea is just a text summary. Invest effort here.
- Formula blocks should show the paper's key equations, not generic math.
- The "影响" timeline should trace the paper's influence forward in time, not just 
  summarize the paper's related work section.

---

## 7. General / Catch-all {#general}

**Typical length**: 3-5 sections

For requests that don't cleanly fit the above categories, use this minimal structure:

```
Hero: topic, context tag, date
01 · 背景: 1-2 paragraphs setting the stage
02 · 核心内容: the main analysis/summary, using whichever components best fit:
    - Tabs for multi-faceted topics
    - Comparison grid for A-vs-B situations
    - Timeline for chronological narratives
    - Metric cards for quantitative highlights
    - SVG for relational/structural concepts
03 · 总结: callout.teal with key takeaway
Footer
```

The general template is intentionally flexible. The key constraint is maintaining the 
editorial reading flow — single column, narrative prose between components, numbered 
section labels.
