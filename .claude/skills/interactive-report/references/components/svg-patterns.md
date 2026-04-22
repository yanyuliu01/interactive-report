# SVG Diagram Patterns

Use custom SVG for structural concepts (relationships, flows, comparisons). 
Use Chart.js only for numerical data with axes.

## General SVG Rules

1. Always use `viewBox` (not fixed width/height) — the SVG will scale responsively
2. Set `width: 100%; height: auto; display: block` in CSS via the `svg` selector
3. Use inline styles in SVG elements (CSS `var()` works in most but not all browsers for SVG)
   - For broad compatibility, reference CSS variables via `style="fill:var(--teal)"` on rect/circle
   - For text, use `style="font-size:12px;fill:var(--muted);font-family:sans-serif"`
4. Keep font sizes between 10-13px for labels
5. Use `text-anchor="middle"` for centered text
6. Use `stroke-dasharray="6 3"` for grouping/container borders
7. Standard viewBox: `"0 0 680 300"` (adjust height as needed, keep width at 680)

## Pattern 1: Structural Comparison (Left vs Right)

For comparing two approaches, architectures, or states side by side.

```html
<svg viewBox="0 0 680 320">
  <!-- Left side label -->
  <text x="170" y="26" text-anchor="middle"
    style="font-size:12px;fill:var(--muted);font-weight:600;font-family:sans-serif">Approach A</text>

  <!-- Left boxes (stacked vertically) -->
  <rect x="60" y="42" width="220" height="40" rx="7" fill="var(--surface2)" stroke="var(--border)" stroke-width="0.8"/>
  <text x="170" y="67" text-anchor="middle" style="font-size:13px;fill:var(--text);font-family:sans-serif">Layer 1</text>

  <rect x="60" y="100" width="220" height="40" rx="7" fill="var(--surface2)" stroke="var(--border)" stroke-width="0.8"/>
  <text x="170" y="125" text-anchor="middle" style="font-size:13px;fill:var(--text);font-family:sans-serif">Layer 2</text>

  <!-- Vertical arrows between layers -->
  <line x1="170" y1="82" x2="170" y2="98" stroke="var(--muted)" stroke-width="1.2"/>

  <!-- Bottom label for left side -->
  <rect x="68" y="160" width="204" height="28" rx="6" fill="var(--amber-light)" stroke="var(--amber)" stroke-width="0.8"/>
  <text x="170" y="178" text-anchor="middle" style="font-size:11px;fill:var(--amber);font-weight:600;font-family:sans-serif">⚠ Limitation</text>

  <!-- Center divider -->
  <line x1="340" y1="20" x2="340" y2="200" stroke="var(--border)" stroke-width="0.8" stroke-dasharray="5 4"/>

  <!-- Right side (same structure, different colors for emphasis) -->
  <text x="510" y="26" text-anchor="middle"
    style="font-size:12px;fill:var(--muted);font-weight:600;font-family:sans-serif">Approach B</text>

  <rect x="400" y="42" width="220" height="40" rx="7" fill="var(--accent-light)" stroke="var(--accent)" stroke-width="0.8"/>
  <text x="510" y="67" text-anchor="middle" style="font-size:13px;fill:var(--text);font-family:sans-serif">Layer 1</text>

  <!-- Bottom label for right side -->
  <rect x="408" y="160" width="204" height="28" rx="6" fill="var(--teal-light)" stroke="var(--teal)" stroke-width="0.8"/>
  <text x="510" y="178" text-anchor="middle" style="font-size:11px;fill:var(--teal);font-weight:600;font-family:sans-serif">✓ Improvement</text>
</svg>
```

## Pattern 2: Hub and Spoke (Central Entity + Surrounding Nodes)

For ecosystems, organizational structures, entity relationships.

```html
<svg viewBox="0 0 680 340">
  <!-- Central circle -->
  <circle cx="340" cy="170" r="52" fill="var(--accent-light)" stroke="var(--accent)" stroke-width="1.5"/>
  <text x="340" y="162" text-anchor="middle" style="font-size:12px;font-weight:700;fill:var(--accent);font-family:sans-serif">Central</text>
  <text x="340" y="180" text-anchor="middle" style="font-size:10px;fill:var(--accent);font-family:sans-serif">Entity</text>

  <!-- Node 1 (top-left) -->
  <circle cx="140" cy="80" r="40" fill="var(--teal-light)" stroke="var(--teal)" stroke-width="1"/>
  <text x="140" y="76" text-anchor="middle" style="font-size:11px;font-weight:700;fill:var(--teal);font-family:sans-serif">Node A</text>
  <text x="140" y="92" text-anchor="middle" style="font-size:9px;fill:var(--muted);font-family:sans-serif">Detail</text>
  <!-- Connecting line -->
  <line x1="178" y1="96" x2="292" y2="154" stroke="var(--border)" stroke-width="1.2"/>

  <!-- Node 2 (top-right) -->
  <circle cx="540" cy="80" r="40" fill="var(--amber-light)" stroke="var(--amber)" stroke-width="1"/>
  <text x="540" y="76" text-anchor="middle" style="font-size:11px;font-weight:700;fill:var(--amber);font-family:sans-serif">Node B</text>
  <line x1="502" y1="96" x2="388" y2="154" stroke="var(--border)" stroke-width="1.2"/>

  <!-- More nodes at bottom-left, bottom, bottom-right as needed -->

  <!-- Floating labels (pill badges on the connections) -->
  <rect x="218" y="110" width="90" height="22" rx="11" fill="var(--accent)" opacity=".9"/>
  <text x="263" y="125" text-anchor="middle" style="font-size:10px;fill:#fff;font-weight:600;font-family:sans-serif">Key Stat</text>
</svg>
```

## Pattern 3: Horizontal Flow (Process Steps)

For pipelines, conversion funnels, sequential transformations.

```html
<svg viewBox="0 0 680 100">
  <!-- Step 1 -->
  <rect x="20" y="20" width="120" height="40" rx="6" fill="var(--accent-light)" stroke="var(--accent)" stroke-width="1"/>
  <text x="80" y="45" text-anchor="middle" style="font-size:12px;font-weight:600;fill:var(--accent);font-family:sans-serif">Step 1</text>
  <text x="80" y="78" text-anchor="middle" style="font-size:10px;fill:var(--muted);font-family:sans-serif">Annotation</text>

  <!-- Arrow -->
  <text x="165" y="44" text-anchor="middle" style="font-size:16px;fill:var(--muted)">→</text>

  <!-- Step 2 -->
  <rect x="185" y="20" width="120" height="40" rx="6" fill="var(--amber-light)" stroke="var(--amber)" stroke-width="1"/>
  <text x="245" y="45" text-anchor="middle" style="font-size:12px;font-weight:600;fill:var(--amber);font-family:sans-serif">Step 2</text>

  <!-- Arrow -->
  <text x="330" y="44" text-anchor="middle" style="font-size:16px;fill:var(--muted)">→</text>

  <!-- Step 3 -->
  <rect x="350" y="20" width="120" height="40" rx="6" fill="var(--teal-light)" stroke="var(--teal)" stroke-width="1"/>
  <text x="410" y="45" text-anchor="middle" style="font-size:12px;font-weight:600;fill:var(--teal);font-family:sans-serif">Step 3</text>

  <!-- Arrow -->
  <text x="495" y="44" text-anchor="middle" style="font-size:16px;fill:var(--muted)">→</text>

  <!-- Step 4 (final) -->
  <rect x="515" y="20" width="140" height="40" rx="6" fill="var(--surface)" stroke="var(--border)" stroke-width="1"/>
  <text x="585" y="45" text-anchor="middle" style="font-size:12px;font-weight:600;fill:var(--text);font-family:sans-serif">Output</text>
</svg>
```

## Pattern 4: Block Diagram (Grouped Layers)

For architectures with grouped components, like encoder-decoder, multi-module systems.

```html
<svg viewBox="0 0 680 280">
  <!-- Block A (dashed border = grouping container) -->
  <rect x="30" y="36" width="180" height="200" rx="12" fill="var(--accent-light)"
    stroke="var(--accent)" stroke-width="1" stroke-dasharray="6 3" opacity=".5"/>
  <text x="120" y="58" text-anchor="middle"
    style="font-size:12px;font-weight:700;fill:var(--accent);font-family:sans-serif">Group A</text>

  <!-- Layers inside Block A -->
  <rect x="50" y="72" width="140" height="32" rx="5" fill="var(--surface)" stroke="var(--border)" stroke-width="0.7"/>
  <text x="120" y="92" text-anchor="middle" style="font-size:12px;fill:var(--text);font-family:sans-serif">Sub-component 1</text>

  <rect x="50" y="116" width="140" height="32" rx="5" fill="var(--surface)" stroke="var(--border)" stroke-width="0.7"/>
  <text x="120" y="136" text-anchor="middle" style="font-size:12px;fill:var(--text);font-family:sans-serif">Sub-component 2</text>

  <!-- Arrow between blocks -->
  <line x1="212" y1="136" x2="268" y2="136" stroke="var(--amber)" stroke-width="2.5"/>
  <text x="240" y="124" text-anchor="middle"
    style="font-size:10px;fill:var(--amber);font-weight:600;font-family:sans-serif">Connection</text>

  <!-- Block B -->
  <rect x="270" y="36" width="180" height="200" rx="12" fill="var(--teal-light)"
    stroke="var(--teal)" stroke-width="1" stroke-dasharray="6 3" opacity=".5"/>
  <!-- ... similar internal structure ... -->
</svg>
```

## Pattern 5: Triangle / Triad

For three-factor models, competitive positioning, triple constraints.

```html
<svg viewBox="0 0 680 300">
  <!-- Outer triangle (dashed) -->
  <polygon points="340,32 120,260 560,260" fill="none" stroke="var(--border)" stroke-width="1.2" stroke-dasharray="6 3"/>
  <!-- Inner triangle (filled) -->
  <polygon points="340,80 200,230 480,230" fill="var(--accent-light)" opacity=".4" stroke="var(--accent)" stroke-width="1"/>

  <!-- Vertex nodes -->
  <circle cx="340" cy="32" r="28" fill="var(--teal-light)" stroke="var(--teal)" stroke-width="1.5"/>
  <text x="340" y="37" text-anchor="middle" style="font-size:11px;font-weight:700;fill:var(--teal);font-family:sans-serif">Factor A</text>

  <circle cx="120" cy="260" r="28" fill="var(--accent-light)" stroke="var(--accent)" stroke-width="1.5"/>
  <text x="120" y="265" text-anchor="middle" style="font-size:11px;font-weight:700;fill:var(--accent);font-family:sans-serif">Factor B</text>

  <circle cx="560" cy="260" r="28" fill="var(--amber-light)" stroke="var(--amber)" stroke-width="1.5"/>
  <text x="560" y="265" text-anchor="middle" style="font-size:11px;font-weight:700;fill:var(--amber);font-family:sans-serif">Factor C</text>

  <!-- Center label -->
  <text x="340" y="170" text-anchor="middle" style="font-size:13px;font-weight:700;fill:var(--accent);font-family:sans-serif">Subject</text>

  <!-- Edge labels (rotated) -->
  <text x="218" y="138" text-anchor="middle" style="font-size:10px;fill:var(--muted);font-family:sans-serif"
    transform="rotate(-50 218 138)">Edge Label AB</text>
</svg>
```

## When to use SVG vs Chart.js

| Use SVG | Use Chart.js |
|---|---|
| Relationships between entities | Time series data |
| Architecture / system diagrams | Bar/column comparisons |
| Process flows | Radar/spider charts |
| Venn / overlap concepts | Pie/doughnut composition |
| Positioning maps | Scatter plots |
| Custom conceptual illustrations | Any chart with numerical axes |
