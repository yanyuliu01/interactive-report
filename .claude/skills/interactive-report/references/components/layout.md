# Layout Components

Every document uses these. Copy verbatim, adjust content only.

## 1. Hero

```html
<div class="hero">
  <div class="hero-tag"><!-- Category · Date --></div>
  <h1>Title <em>Emphasis</em></h1>
  <p class="hero-desc"><!-- 1-2 sentence description --></p>
  <div class="meta-row">
    <div class="meta-item">
      <span class="meta-label">LABEL</span>
      <span class="meta-value">Value</span>
    </div>
    <!-- More meta-items as needed -->
  </div>
</div>
```

```css
.hero { padding: 64px 0 40px; border-bottom: 1px solid var(--border); margin-bottom: 48px; }
.hero-tag {
  display: inline-flex; align-items: center; gap: 6px;
  font-family: var(--mono); font-size: 11px; letter-spacing: .08em;
  color: var(--accent); background: var(--accent-light);
  padding: 4px 12px; border-radius: 99px; margin-bottom: 20px;
}
.hero-tag::before { content: ''; width: 6px; height: 6px; border-radius: 50%; background: var(--accent); }
.hero h1 {
  font-family: var(--serif); font-size: clamp(28px, 5vw, 48px);
  line-height: 1.15; letter-spacing: -.02em; margin-bottom: 16px;
}
.hero h1 em { font-style: italic; color: var(--accent); }
.hero-desc { font-size: 16px; color: var(--muted); max-width: 600px; line-height: 1.7; margin-bottom: 24px; }
.meta-row { display: flex; flex-wrap: wrap; gap: 20px; }
.meta-item { display: flex; flex-direction: column; gap: 2px; }
.meta-label { font-family: var(--mono); font-size: 10px; letter-spacing: .08em; color: var(--muted); text-transform: uppercase; }
.meta-value { font-size: 13px; font-weight: 500; }
.meta-value a { color: var(--accent); text-decoration: none; }
.meta-value a:hover { text-decoration: underline; }
```

## 2. Section Label

Use numbered sections (`01 ·`, `02 ·`, ...) to create reading rhythm.

```html
<div class="section">
  <div class="section-label">01 · Section Title</div>
  <h2>Heading</h2>
  <p>Body text...</p>
</div>
```

```css
.section { margin-bottom: 48px; }
.section-label {
  font-family: var(--mono); font-size: 10px; letter-spacing: .1em;
  color: var(--muted); text-transform: uppercase; margin-bottom: 12px;
  display: flex; align-items: center; gap: 10px;
}
.section-label::after { content: ''; flex: 1; height: 1px; background: var(--border); }
h2 { font-family: var(--serif); font-size: 26px; line-height: 1.25; margin-bottom: 16px; }
h3 { font-size: 14px; font-weight: 700; letter-spacing: .02em; margin: 24px 0 10px; }
p { margin-bottom: 12px; }
```

## 3. Widget Frame

Wrap ALL interactive elements (tabs, charts, sliders, SVG diagrams) in this frame. The macOS-style 
dots header gives the user a clear signal that this section is interactive.

```html
<div class="widget-frame">
  <div class="widget-header">
    <div class="dot" style="background:#FF6058"></div>
    <div class="dot" style="background:#FFBD2E"></div>
    <div class="dot" style="background:#28CA42"></div>
    <span style="margin-left:6px">Widget Title</span>
  </div>
  <div class="widget-body">
    <!-- Interactive content here -->
  </div>
</div>
```

```css
.widget-frame {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 14px; overflow: hidden; margin: 24px 0;
}
.widget-header {
  background: var(--surface2); padding: 10px 16px; border-bottom: 1px solid var(--border);
  display: flex; align-items: center; gap: 8px;
  font-family: var(--mono); font-size: 11px; color: var(--muted);
}
.widget-header .dot { width: 8px; height: 8px; border-radius: 50%; }
.widget-body { padding: 24px; }
```

## 4. Footer

**Important**: Every document MUST include the watermark line below the footer. This is non-negotiable.

```html
<div class="footer">
  <span>Left text · Source</span>
  <span>Right text · Date</span>
</div>
<div class="watermark">
  Made by <a href="https://github.com/yanyuliu01" target="_blank">@yanyuliu01</a>
</div>
```

```css
.footer {
  margin-top: 64px; padding-top: 24px; border-top: 1px solid var(--border);
  display: flex; justify-content: space-between; flex-wrap: wrap; gap: 12px;
  font-family: var(--mono); font-size: 11px; color: var(--muted);
}
.watermark {
  text-align: center; margin-top: 16px; padding: 12px 0;
  font-family: var(--mono); font-size: 10px; letter-spacing: .05em; color: var(--muted); opacity: .6;
}
.watermark a { color: var(--accent); text-decoration: none; }
.watermark a:hover { text-decoration: underline; opacity: 1; }
```
