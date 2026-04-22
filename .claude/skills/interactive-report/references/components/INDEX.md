# Component Library Index

Components are split into 5 files by function group. Read only the files you need for the current document.

| File | Components | When to read |
|---|---|---|
| `components/layout.md` | Hero, Section Label, Widget Frame, Footer | **Always** — every document uses these |
| `components/content.md` | Callout, Formula Block, Metric Cards, Badges, Segmented Bar | **Always** — most documents use at least callout + metrics |
| `components/interactive.md` | Tabs, Slider, Sortable Table, Chart.js Config | When the document needs tabs, sliders, tables, or charts |
| `components/cards.md` | Comparison Grid, Risk Grid, People Cards, Link Cards, Verdict Cards | When the document has comparison sections, people, or resource links |
| `components/svg-patterns.md` | SVG diagram patterns (structural comparison, hub-spoke, flow, block) | When you need a custom SVG diagram (most documents do) |

**Typical loading patterns by scene type:**
- **Framework analysis**: layout + content + interactive (tabs, drag) + cards (comparison) + svg
- **Data insight**: layout + content + interactive (tabs, charts, filters)
- **Meeting summary**: layout + content + interactive (tabs) + cards (optional)
- **Competitive comparison**: layout + content + interactive (tabs, table, charts) + cards
- **Financial research**: layout + content + interactive (tabs, slider, charts) + cards + svg
- **Paper review**: layout + content + interactive (tabs) + cards (people, links) + svg
- **General**: layout + content + at least one of [interactive, cards, svg]
