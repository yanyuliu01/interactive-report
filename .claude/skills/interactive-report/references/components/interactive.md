# Interactive Components

Components with JS behavior. Put all JS in a single `<script>` block before `</body>`.

## 1. Tabs

Pill-style tab navigation. Can be nested inside widget-frame.

```html
<div class="tabs">
  <button class="tab-btn active" onclick="showTab('t1',this)">Tab 1</button>
  <button class="tab-btn" onclick="showTab('t2',this)">Tab 2</button>
  <button class="tab-btn" onclick="showTab('t3',this)">Tab 3</button>
</div>
<div class="tab-panel active" id="t1">Content 1</div>
<div class="tab-panel" id="t2">Content 2</div>
<div class="tab-panel" id="t3">Content 3</div>
```

```css
.tabs { display: flex; gap: 4px; margin-bottom: 20px; flex-wrap: wrap; }
.tab-btn {
  padding: 6px 16px; border-radius: 99px; font-size: 12px; font-family: var(--sans);
  border: 1px solid var(--border); background: transparent; color: var(--muted);
  cursor: pointer; transition: all .2s;
}
.tab-btn:hover { background: var(--surface2); }
.tab-btn.active { background: var(--accent); color: #fff; border-color: var(--accent); }
.tab-panel { display: none; }
.tab-panel.active { display: block; }
```

```js
function showTab(id, btn) {
  const frame = btn.closest('.widget-body') || btn.closest('.page');
  frame.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  frame.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  btn.classList.add('active');
}
```

**Important**: This `showTab` function scopes to the nearest `.widget-body` or `.page`, so multiple 
independent tab groups on the same page won't conflict. Use unique IDs for each tab panel.

## 2. Slider

Range input with live-updating display value. Pair with a JS update function that recomputes 
derived values (e.g., target price from PEV multiplier).

```html
<div class="slider-row">
  <span class="slider-label">Target PEV</span>
  <input type="range" min="50" max="120" value="70" step="5" oninput="updatePEV(this.value)">
  <span class="slider-val" id="pev-display">0.70×</span>
</div>
```

```css
.slider-row { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }
.slider-label { font-size: 12px; color: var(--muted); white-space: nowrap; }
.slider-row input[type=range] {
  flex: 1; height: 4px; border-radius: 99px;
  -webkit-appearance: none; appearance: none;
  background: var(--border); cursor: pointer; outline: none;
}
.slider-row input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none; width: 16px; height: 16px;
  border-radius: 50%; background: var(--accent); cursor: pointer;
}
.slider-val { font-family: var(--mono); font-size: 12px; font-weight: 500; min-width: 40px; text-align: right; }
```

**JS pattern** — slider that updates multiple dependent values:
```js
const ANCHOR = 82.45; // base value
function updatePEV(v) {
  const mult = v / 100;
  document.getElementById('pev-display').textContent = mult.toFixed(2) + '×';
  const price = (ANCHOR * mult).toFixed(1);
  document.getElementById('target-price').textContent = price + ' 元';
  // Compute upside, yield, etc.
}
```

## 3. Sortable Table

Data-driven table with click-to-sort headers and optional star-rating filter. Define data as JS 
arrays, render table dynamically.

**Data structure**:
```js
const PRODUCTS = [
  {
    name: 'Product A',
    color: '#3FB950',
    scores: { dim1: 5, dim2: 3, dim3: 4 },
    detail: { summary: '...', pros: '...', cons: '...' }
  },
  // ...
];
const DIMS = ['dim1', 'dim2', 'dim3'];
```

**State and helpers**:
```js
let sortCol = null, sortDir = 1, minStar = 0;

function stars(n) {
  return Array.from({length:5}, (_, i) =>
    `<span style="color:${i < n ? 'var(--amber)' : 'var(--border)'}">★</span>`
  ).join('');
}
```

**Sort and filter**:
```js
function doSort(col) {
  if (sortCol === col) sortDir *= -1;
  else { sortCol = col; sortDir = -1; }
  renderTable();
}

function setMin(n, btn) {
  minStar = n;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderTable();
}
```

**Render function** — rebuilds table from data on every sort/filter change:
```js
function renderTable() {
  const head = document.getElementById('mHead');
  head.innerHTML = '<th>产品</th>';
  DIMS.forEach(d => {
    const s = sortCol === d;
    head.innerHTML += `<th class="${s?'sorted':''}" onclick="doSort('${d}')">${d}<span class="arr">${s?(sortDir>0?'▲':'▼'):''}</span></th>`;
  });

  const body = document.getElementById('mBody');
  body.innerHTML = '';
  let sorted = [...PRODUCTS];
  if (sortCol) sorted.sort((a, b) => (a.scores[sortCol] - b.scores[sortCol]) * sortDir);

  sorted.forEach((p, i) => {
    const pass = DIMS.every(d => p.scores[d] >= minStar);
    if (!pass) return;
    // Main row
    const tr = document.createElement('tr');
    tr.innerHTML = `<td><div class="prod-name" onclick="toggleDet('det-${i}',this)">
      <span class="prod-dot" style="background:${p.color}"></span>${p.name}
      <span class="prod-expand">▸</span></div></td>
      ${DIMS.map(d => `<td>${stars(p.scores[d])}</td>`).join('')}`;
    body.appendChild(tr);
    // Detail row
    const dr = document.createElement('tr');
    dr.className = 'detail-row'; dr.id = 'det-' + i;
    dr.innerHTML = `<td colspan="${DIMS.length+1}"><div class="detail-inner">
      <h4>${p.name}</h4><p>${p.detail.summary}</p>
      <p class="detail-pro"><strong>✓ 优势：</strong>${p.detail.pros}</p>
      <p class="detail-con"><strong>✗ 不足：</strong>${p.detail.cons}</p>
    </div></td>`;
    body.appendChild(dr);
  });
}

function toggleDet(id, el) {
  const row = document.getElementById(id);
  row.classList.toggle('open');
  el.querySelector('.prod-expand').style.transform = row.classList.contains('open') ? 'rotate(90deg)' : '';
}
```

**Table CSS**:
```css
.matrix { width: 100%; border-collapse: collapse; font-size: 13px; }
.matrix th {
  padding: 10px 12px; text-align: left; font-size: 11px;
  font-family: var(--mono); letter-spacing: .04em;
  color: var(--muted); text-transform: uppercase;
  border-bottom: 1px solid var(--border);
  cursor: pointer; user-select: none; white-space: nowrap; transition: color .15s;
}
.matrix th:hover { color: var(--accent); }
.matrix th.sorted { color: var(--accent); }
.matrix td { padding: 10px 12px; border-bottom: 1px solid var(--border); vertical-align: middle; }
.matrix tr:last-child td { border-bottom: none; }

.prod-name { display: flex; align-items: center; gap: 8px; font-weight: 600; cursor: pointer; white-space: nowrap; }
.prod-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
.prod-expand { font-size: 10px; color: var(--muted); transition: transform .2s; }

.detail-row td { padding: 0; background: var(--surface2); }
.detail-inner { max-height: 0; overflow: hidden; transition: max-height .3s, padding .3s; padding: 0 16px; font-size: 13px; color: var(--muted); }
.detail-row.open .detail-inner { max-height: 500px; padding: 16px; }

.filter-row { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; margin-bottom: 16px; font-size: 12px; color: var(--muted); }
.filter-btn {
  padding: 4px 12px; border-radius: 99px; font-size: 12px;
  border: 1px solid var(--border); background: transparent; color: var(--muted);
  cursor: pointer; transition: all .15s; font-family: var(--sans);
}
.filter-btn:hover { background: var(--surface2); }
.filter-btn.active { background: var(--accent-light); border-color: var(--accent); color: var(--accent); }
```

## 4. Chart.js Configuration

**Only use for data with numerical axes** (bar, line, radar, doughnut). For structural diagrams 
(flows, relationships, comparisons), use SVG instead.

**CDN** (add to `<head>` only if charts are needed):
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
```

**Standard config constants** — adjust grid/tick colors for warm vs cool theme:
```js
// Warm theme
const FONT = { family: "-apple-system, PingFang SC, sans-serif", size: 11 };
const GRID = { color: '#E0D9D0' };
const TICK = { color: '#7A756D', font: FONT };

// Cool theme — change these two:
// const GRID = { color: '#2A2F42' };
// const TICK = { color: '#6C7393', font: FONT };
```

**Bar + Line combo chart (most common)**:
```js
new Chart(ctx, {
  type: 'bar',
  data: {
    labels: ['2020', '2021', '2022', '2023', '2024'],
    datasets: [
      { label: 'Revenue', data: [100,120,90,110,140], backgroundColor: 'rgba(83,64,196,.18)',
        borderColor: '#5340C4', borderWidth: 1.5, borderRadius: 4, order: 2 },
      { label: 'Net Profit', data: [20,25,15,22,30], type: 'line', borderColor: '#0A6B52',
        backgroundColor: 'rgba(10,107,82,.08)', borderWidth: 2.5, pointRadius: 4,
        pointBackgroundColor: '#0A6B52', tension: .3, fill: true, order: 1 }
    ]
  },
  options: {
    responsive: true, maintainAspectRatio: false,
    scales: {
      x: { grid: { display: false }, ticks: TICK },
      y: { grid: GRID, ticks: TICK, beginAtZero: true }
    },
    plugins: {
      legend: { labels: { font: FONT, usePointStyle: true, pointStyle: 'circle', padding: 16 } },
      tooltip: { backgroundColor: '#1C1A17', titleFont: { size: 12 }, bodyFont: { size: 11 }, padding: 10, cornerRadius: 8 }
    }
  }
});
```

**Radar chart** — replace `scales.x/y` with `scales.r`:
```js
scales: {
  r: {
    beginAtZero: true, max: 5,
    ticks: { stepSize: 1, color: '#6C7393', backdropColor: 'transparent', font: { size: 10 } },
    grid: { color: '#2A2F42' },
    angleLines: { color: '#2A2F42' },
    pointLabels: { color: '#9CA3C0', font: { size: 12, family: '-apple-system, PingFang SC, sans-serif' } }
  }
}
```

**Dual-axis chart** — add `yAxisID: 'y1'` to second dataset:
```js
datasets: [
  { label: 'Absolute', data: [...], yAxisID: 'y' },
  { label: 'Percentage', data: [...], type: 'line', yAxisID: 'y1' }
],
scales: {
  y: { grid: GRID, ticks: TICK, beginAtZero: true },
  y1: { position: 'right', grid: { display: false }, ticks: { ...TICK, callback: v => v + '%' } }
}
```

**Lazy chart rendering** — only create chart when its tab becomes visible:
```js
let chart1 = null;
function renderChart1() {
  if (chart1) return; // already created
  chart1 = new Chart(document.getElementById('canvas1'), { /* config */ });
}
// Call renderChart1() in the tab's onclick: onclick="showTab('ch1',this); renderChart1()"
```
