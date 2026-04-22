# Content Components

Static content blocks that present information. No JS needed.

## 1. Callout Box

Variants: default (accent purple), `.teal`, `.amber`, `.red`. Use teal for conclusions, amber for 
warnings/tips, red for risks, default for general emphasis.

```html
<div class="callout teal">
  <div class="callout-title">Title Text</div>
  Content text here. Can include <strong>bold</strong> and <code>code</code>.
</div>
```

```css
.callout {
  border-left: 3px solid var(--accent); background: var(--accent-light);
  padding: 16px 20px; border-radius: 0 8px 8px 0; margin: 20px 0; font-size: 14px;
}
.callout.teal { border-color: var(--teal); background: var(--teal-light); }
.callout.amber { border-color: var(--amber); background: var(--amber-light); }
.callout.red { border-color: var(--red); background: var(--red-light); }
.callout-title {
  font-weight: 700; font-size: 12px; letter-spacing: .05em;
  text-transform: uppercase; margin-bottom: 6px; color: var(--accent);
}
.callout.teal .callout-title { color: var(--teal); }
.callout.amber .callout-title { color: var(--amber); }
.callout.red .callout-title { color: var(--red); }
```

## 2. Formula Block

Dark-background block for math formulas or code snippets. Stands out visually from the reading flow.

```html
<div class="formula-block">
  Attention(Q, K, V) = <span class="fn">softmax</span>( Q·K<sup>T</sup> / <span class="kw">√d<sub>k</sub></span> ) · V
</div>
```

```css
.formula-block {
  background: #1C1A17; color: #E8E3DC;
  font-family: var(--mono); font-size: 15px; line-height: 1.6;
  padding: 18px 24px; border-radius: 10px; margin: 16px 0; text-align: center;
}
.formula-block .kw { color: #8B84FF; }
.formula-block .fn { color: #6ECCB0; }
.formula-block .cm { color: #7A756D; }
```

Inline code:
```css
code {
  font-family: var(--mono); font-size: 13px;
  background: var(--surface2); padding: 2px 6px; border-radius: 4px; color: var(--accent);
}
```

## 3. Metric Cards

Grid of highlight numbers. Adjust `grid-template-columns` to `repeat(N, 1fr)` for N cards.

```html
<div class="metric-grid">
  <div class="metric-card">
    <div class="metric-val mc-teal">28.4</div>
    <div class="metric-label">BLEU Score<br><span style="color:var(--teal)">+2.0 SOTA</span></div>
  </div>
  <div class="metric-card">
    <div class="metric-val mc-amber">3.5<span style="font-size:14px">天</span></div>
    <div class="metric-label">训练时间<br>8× P100</div>
  </div>
</div>
```

```css
.metric-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin: 16px 0; }
.metric-card { background: var(--surface2); border-radius: 10px; padding: 14px; text-align: center; }
.metric-val { font-family: var(--serif); font-size: 28px; line-height: 1.1; }
.metric-label { font-size: 11px; color: var(--muted); margin-top: 4px; line-height: 1.4; }
.mc-teal { color: var(--teal); }
.mc-amber { color: var(--amber); }
.mc-accent { color: var(--accent); }
.mc-red { color: var(--red); }
```

Reduce `font-size` on `.metric-val` to `20-22px` when using longer text (e.g., "1,329亿").

## 4. Badges

Inline labels used inside cards.

```html
<span class="badge badge-green">Positive Label</span>
<span class="badge badge-amber">Neutral Label</span>
<span class="badge badge-red">Negative Label</span>
```

```css
.badge { display: inline-block; font-size: 11px; padding: 3px 10px; border-radius: 99px; margin-top: 8px; font-weight: 500; }
.badge-green { background: var(--teal-light); color: var(--teal); }
.badge-amber { background: var(--amber-light); color: var(--amber); }
.badge-red { background: var(--red-light); color: var(--red); }
```

## 5. Segmented Bar

Horizontal stacked bar showing composition/proportion. Good for revenue breakdown, market share, etc.

```html
<div class="seg-bar">
  <div style="flex:55;background:var(--accent)">寿险 55%</div>
  <div style="flex:30;background:var(--teal)">银行 30%</div>
  <div style="flex:15;background:var(--amber)">15%</div>
</div>
<div class="seg-legend">
  <div class="seg-legend-item"><span class="seg-legend-dot" style="background:var(--accent)"></span>寿险</div>
  <div class="seg-legend-item"><span class="seg-legend-dot" style="background:var(--teal)"></span>银行</div>
  <div class="seg-legend-item"><span class="seg-legend-dot" style="background:var(--amber)"></span>其他</div>
</div>
```

```css
.seg-bar { display: flex; height: 28px; border-radius: 6px; overflow: hidden; margin: 12px 0; }
.seg-bar div { display: flex; align-items: center; justify-content: center; font-size: 10px; font-weight: 600; color: #fff; }
.seg-legend { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 8px; }
.seg-legend-item { display: flex; align-items: center; gap: 5px; font-size: 11px; color: var(--muted); }
.seg-legend-dot { width: 8px; height: 8px; border-radius: 2px; }
```

Hide percentage text for segments below `flex:8` — they're too narrow to show text.
