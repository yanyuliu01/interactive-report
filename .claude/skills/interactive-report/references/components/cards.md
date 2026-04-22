# Card Components

Structured card layouts for comparisons, people, resources, and recommendations.

## 1. Comparison Grid

Two-column card grid for A-vs-B or Baseline-vs-Proposed comparisons. Use `.hl` class on the 
preferred/proposed card.

```html
<div class="cmp-grid">
  <div class="cmp-card">
    <div class="cmp-card-tag">Baseline</div>
    <div class="cmp-card-title">Title A</div>
    <div class="cmp-row">Detail row 1</div>
    <div class="cmp-row">Detail row 2</div>
    <span class="badge badge-amber">Neutral Label</span>
  </div>
  <div class="cmp-card hl">
    <div class="cmp-card-tag">Proposed</div>
    <div class="cmp-card-title">Title B</div>
    <div class="cmp-row">Detail row 1</div>
    <div class="cmp-row">Detail row 2</div>
    <span class="badge badge-green">Positive Label</span>
  </div>
</div>
```

```css
.cmp-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-top: 16px; }
.cmp-card { border: 1px solid var(--border); border-radius: 10px; padding: 16px; background: var(--surface); }
.cmp-card.hl { border-color: var(--teal); border-width: 1.5px; }
.cmp-card-tag { font-size: 10px; font-family: var(--mono); font-weight: 500; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
.cmp-card-title { font-size: 14px; font-weight: 700; margin-bottom: 10px; }
.cmp-row { font-size: 12px; color: var(--muted); padding: 5px 0; border-bottom: 1px solid var(--surface2); }
.cmp-row:last-of-type { border-bottom: none; }
```

## 2. Risk Grid

Bull-vs-bear or opportunity-vs-risk two-column layout with colored left borders.

```html
<div class="risk-grid">
  <div class="risk-card" style="border-color:var(--teal)">
    <h4><span style="color:var(--teal)">✦</span> 看多因素</h4>
    <div class="risk-item"><strong>Factor title</strong> · Description text</div>
    <div class="risk-item"><strong>Factor title</strong> · Description text</div>
  </div>
  <div class="risk-card" style="border-color:var(--red)">
    <h4><span style="color:var(--red)">✦</span> 风险因素</h4>
    <div class="risk-item"><strong>Factor title</strong> · Description text</div>
    <div class="risk-item"><strong>Factor title</strong> · Description text</div>
  </div>
</div>
```

```css
.risk-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 16px 0; }
.risk-card { padding: 16px; border-radius: 10px; border: 1px solid var(--border); background: var(--surface); }
.risk-card h4 { font-size: 13px; font-weight: 700; margin-bottom: 8px; display: flex; align-items: center; gap: 6px; }
.risk-item { font-size: 12px; color: var(--muted); padding: 4px 0; line-height: 1.5; border-bottom: 1px solid var(--surface2); }
.risk-item:last-child { border-bottom: none; }
```

## 3. People Cards

Grid of avatar cards for team members, authors, key figures.

```html
<div class="people-grid">
  <div class="person-card">
    <div class="person-avatar">AV</div>
    <div class="person-name">Full Name</div>
    <div class="person-role">Title or role</div>
  </div>
  <div class="person-card">
    <div class="person-avatar" style="background:var(--teal-light);color:var(--teal)">NS</div>
    <div class="person-name">Full Name</div>
    <div class="person-role">Title or role</div>
  </div>
</div>
```

Vary avatar background colors using the semantic light/color pairs (accent-light/accent, teal-light/teal, 
amber-light/amber, red-light/red) to add visual variety.

```css
.people-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-top: 16px; }
.person-card { background: var(--surface); border: 1px solid var(--border); border-radius: 10px; padding: 14px; text-align: center; }
.person-avatar {
  width: 40px; height: 40px; border-radius: 50%;
  background: var(--accent-light); color: var(--accent);
  font-weight: 700; font-size: 13px;
  display: flex; align-items: center; justify-content: center;
  margin: 0 auto 8px;
}
.person-name { font-size: 12px; font-weight: 700; margin-bottom: 2px; }
.person-role { font-size: 10px; color: var(--muted); line-height: 1.4; }
```

Use `repeat(3, 1fr)` for 3-column or `repeat(2, 1fr)` for 2-column based on count.

## 4. Link Cards

Clickable resource links in a two-column grid.

```html
<div class="links-grid">
  <a class="link-card" href="https://..." target="_blank">
    <div class="link-icon">📄</div>
    <div>
      <div class="link-title">Resource Title</div>
      <div class="link-desc">Brief description</div>
    </div>
  </a>
  <a class="link-card" href="https://..." target="_blank">
    <div class="link-icon">📓</div>
    <div>
      <div class="link-title">Resource Title</div>
      <div class="link-desc">Brief description</div>
    </div>
  </a>
</div>
```

```css
.links-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 16px; }
.link-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 10px; padding: 14px 16px; text-decoration: none; color: var(--text);
  display: flex; align-items: center; gap: 12px; transition: border-color .2s, background .2s;
}
.link-card:hover { border-color: var(--accent); background: var(--accent-light); }
.link-icon {
  width: 36px; height: 36px; border-radius: 8px; background: var(--surface2);
  display: flex; align-items: center; justify-content: center; font-size: 16px; flex-shrink: 0;
}
.link-title { font-size: 13px; font-weight: 700; }
.link-desc { font-size: 11px; color: var(--muted); }
```

## 5. Verdict Cards

Recommendation cards for "which should I choose" scenarios. Use within tabs.

```html
<div class="verdict-grid">
  <div class="verdict-card pick">
    <div class="verdict-tag">🏆 首选推荐</div>
    <div class="verdict-title" style="color:#3FB950">Product Name</div>
    <div class="verdict-desc">Why this is the top pick for this scenario. 2-3 sentences.</div>
    <span class="badge badge-green">Key advantage</span>
  </div>
  <div class="verdict-card">
    <div class="verdict-tag">备选方案</div>
    <div class="verdict-title" style="color:#A78BFA">Product Name</div>
    <div class="verdict-desc">Why this is a good alternative. 2-3 sentences.</div>
    <span class="badge badge-amber">Tradeoff note</span>
  </div>
</div>
```

```css
.verdict-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin: 16px 0; }
.verdict-card { border: 1px solid var(--border); border-radius: 10px; padding: 16px; background: var(--surface); }
.verdict-card.pick { border-color: var(--teal); }
.verdict-tag { font-size: 10px; font-family: var(--mono); font-weight: 600; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
.verdict-card.pick .verdict-tag { color: var(--teal); }
.verdict-title { font-size: 14px; font-weight: 700; margin-bottom: 6px; }
.verdict-desc { font-size: 12px; color: var(--muted); line-height: 1.5; }
```

## 6. Timeline

Vertical timeline with dot markers. Use `.major` class for milestone events.

```html
<div class="timeline">
  <div class="tl-item major">
    <div class="tl-year">2017.06</div>
    <div class="tl-text"><strong>Major Event</strong> — description of what happened</div>
  </div>
  <div class="tl-item">
    <div class="tl-year">2018.10</div>
    <div class="tl-text">Minor event description</div>
  </div>
</div>
```

```css
.timeline { position: relative; padding-left: 28px; margin-top: 16px; }
.timeline::before {
  content: ''; position: absolute; left: 8px; top: 8px; bottom: 8px;
  width: 2px; background: var(--border);
}
.tl-item { position: relative; padding-bottom: 20px; }
.tl-item::before {
  content: ''; position: absolute; left: -24px; top: 6px;
  width: 12px; height: 12px; border-radius: 50%; background: var(--accent);
  border: 2px solid var(--bg);
}
.tl-item.major::before { background: var(--teal); }
.tl-year { font-family: var(--mono); font-size: 11px; color: var(--muted); font-weight: 600; margin-bottom: 2px; }
.tl-text { font-size: 13px; line-height: 1.5; }
.tl-text strong { color: var(--accent); }
```
