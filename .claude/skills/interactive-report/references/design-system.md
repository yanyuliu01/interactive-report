# Design System Reference

## Table of Contents
1. [Theme: Warm (cream/paper)](#warm-theme)
2. [Theme: Cool (dark)](#cool-theme)
3. [Typography System](#typography)
4. [Base HTML Skeleton](#skeleton)
5. [Responsive Rules](#responsive)

---

## Warm Theme {#warm-theme}

Cream/paper background. Feels editorial, academic, magazine-like.

```css
:root {
  --bg: #F7F5F0;
  --surface: #FFFFFF;
  --surface2: #F1EDE6;
  --border: #E0D9D0;
  --text: #1C1A17;
  --muted: #7A756D;
  --accent: #5340C4;
  --accent-light: #EAE7FA;
  --teal: #0A6B52;
  --teal-light: #DFF2EC;
  --amber: #8A5200;
  --amber-light: #FDF0D8;
  --red: #A8200D;
  --red-light: #FBEAE8;
  --blue: #1D4ED8;
  --blue-light: #EEF2FF;
  --serif: Georgia, 'Songti SC', STSong, serif;
  --sans: -apple-system, 'PingFang SC', 'Microsoft YaHei', sans-serif;
  --mono: 'SF Mono', Consolas, 'Courier New', monospace;
}
```

## Cool Theme {#cool-theme}

Dark background. Feels technical, data-heavy, product-focused.

```css
:root {
  --bg: #101117;
  --surface: #181B25;
  --surface2: #1F2333;
  --border: #2A2F42;
  --text: #E2E4ED;
  --muted: #6C7393;
  --accent: #818CF8;
  --accent-light: rgba(129,140,248,.12);
  --teal: #34D399;
  --teal-light: rgba(52,211,153,.1);
  --amber: #FBBF24;
  --amber-light: rgba(251,191,36,.1);
  --red: #F87171;
  --red-light: rgba(248,113,113,.1);
  --blue: #60A5FA;
  --blue-light: rgba(96,165,250,.1);
  --serif: Georgia, 'Songti SC', serif;
  --sans: -apple-system, 'PingFang SC', 'Microsoft YaHei', sans-serif;
  --mono: 'SF Mono', Consolas, 'Courier New', monospace;
}
```

**Important**: Both themes share the same `--serif`, `--sans`, `--mono` font stacks and the same 
semantic color naming (accent, teal, amber, red, blue). Components written against these variable 
names work in BOTH themes without modification.

## Typography System {#typography}

The three-typeface system creates visual hierarchy without relying on weight or size alone.

| Role | Font | Usage |
|---|---|---|
| **Serif** (`var(--serif)`) | Georgia / Songti SC | `h1`, `h2`, metric values, hero title |
| **Sans** (`var(--sans)`) | System / PingFang SC | Body text, card content, tab labels, everything else |
| **Mono** (`var(--mono)`) | SF Mono / Consolas | Section labels, metadata labels, tags, code, badge text |

**Sizing scale**:
- Hero h1: `clamp(28px, 5vw, 48px)`, letter-spacing `-.02em`
- Section h2: `26px`, line-height `1.25`
- h3 (within widgets): `14px`, font-weight `700`
- Body: `15px`, line-height `1.8`
- Small labels: `11-12px`
- Micro labels (mono): `10px`, letter-spacing `.08-.1em`, `text-transform: uppercase`

## Base HTML Skeleton {#skeleton}

Every document starts with this exact structure. Copy it verbatim and fill in content.

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title><!-- Document title --></title>
<!-- If Chart.js needed: -->
<!-- <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script> -->
<style>
  /* Paste theme variables here */
  
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: var(--bg); color: var(--text);
    font-family: var(--sans); font-size: 15px; line-height: 1.8;
    -webkit-font-smoothing: antialiased;
  }
  .page { max-width: 780px; margin: 0 auto; padding: 0 24px 80px; }

  /* Paste component CSS here (from components.md) */
</style>
</head>
<body>
<div class="page">
  <!-- Hero -->
  <!-- Sections -->
  <!-- Footer -->
</div>
<script>
  /* All JS here */
</script>
</body>
</html>
```

## Responsive Rules {#responsive}

Add this media query at the end of your CSS. It collapses all grids to single column on mobile.

```css
@media (max-width: 600px) {
  .cmp-grid, .metric-grid, .links-grid, .people-grid, .risk-grid,
  .strategy-grid, .verdict-grid { grid-template-columns: 1fr; }
  .people-grid { grid-template-columns: 1fr 1fr; }
  body { padding: 16px; }
  .hero h1 { font-size: 28px; }
}
```
