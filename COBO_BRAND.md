# Cobo Brand Specification for HTML Slides

This file defines the complete visual identity for Cobo HTML presentations.
**Read this file in full before generating any slide.**

---

## Brand Identity

- **Company**: Cobo — "The trusted digital asset wallet platform"
- **Tagline**: Powering Your Crypto Ambitions
- **Website**: cobo.com
- **Tone**: Institutional, professional, Web3-native. Confident but not flashy.
- **Language**: Default Simplified Chinese. Match user's input language.

---

## Color Palette

```css
:root {
  /* === Core brand colors === */
  --bg:            #0d0d0d;   /* Near-black — primary slide background */
  --bg-card:       #161616;   /* Card background */
  --bg-card2:      #1c1c1c;   /* Card hover / secondary */
  --purple:        #7C7FE8;   /* PRIMARY ACCENT — matches cobo.com "trusted" */
  --purple-dim:    rgba(124,127,232,0.14);
  --purple-border: rgba(124,127,232,0.28);
  --blue-btn:      #3D50F5;   /* CTA button blue */
  --text:          #ffffff;
  --text-sec:      #888888;
  --text-muted:    #3a3a3a;
  --border:        rgba(255,255,255,0.07);
  --border-med:    rgba(255,255,255,0.11);

  /* === Layout === */
  --nav-h:      44px;   /* Fixed top nav height — ALL slides need padding-top: var(--nav-h) */

  /* === Typography scale (clamp = mobile → desktop) === */
  --title-size: clamp(1.6rem, 5vw, 4rem);
  --h2-size:    clamp(1.15rem, 2.8vw, 2.1rem);
  --h3-size:    clamp(0.9rem, 1.7vw, 1.28rem);
  --body-size:  clamp(0.7rem, 1.1vw, 0.92rem);
  --small-size: clamp(0.6rem, 0.88vw, 0.76rem);
  --label-size: clamp(0.53rem, 0.72vw, 0.66rem);

  /* === Spacing === */
  --pad:    clamp(1.4rem, 3.5vw, 4rem);
  --gap:    clamp(0.55rem, 1.3vw, 1.5rem);
  --gap-sm: clamp(0.28rem, 0.65vw, 0.75rem);

  /* === Animation === */
  --ease: cubic-bezier(0.16, 1, 0.3, 1);
  --dur:  0.6s;
}
```

---

## Typography

```
Logo font:  Varela Round 400       — circular rounded forms, approximates Cobo wordmark
Body font:  Plus Jakarta Sans      — 300 / 400 / 500 / 600 / 700 / 800
Source:     Google Fonts
```

**Google Fonts link (always include in `<head>`):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Varela+Round&family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet" />
```

**Type rules:**
- `h1` — 800 weight, letter-spacing -0.03em, line-height 1.07
- `h2` — 700 weight, letter-spacing -0.02em, line-height 1.15
- `h3` — 600 weight, line-height 1.3
- `p/li` — var(--body-size), color var(--text-sec), line-height 1.65
- Never use Inter, Roboto, Arial, or system fonts

---

## Cobo Logo

Use the official Cobo logo from the CDN. Add `filter:brightness(0) invert(1)` to make it white on dark backgrounds:
```html
<img src="https://www.cobo.com/cobo-logo.svg" alt="Cobo" style="height:20px;width:auto;filter:brightness(0) invert(1);">
```
Scale with `height` only (width: auto). Never distort.

---

## Fixed Top Navigation Bar

**Required on every presentation. Two-row design: row 1 = logo + deck title + counter; row 2 = per-slide chapter tabs.**

```
--nav-h: 78px   (row1=36px + row2=42px)
```

### HTML structure

```html
<nav class="top-nav" id="topNav">

  <!-- Row 1: Logo · deck title · slide counter -->
  <div class="tn-row1">
    <div class="tn-logo" onclick="goToSlide(0)">
      <img src="https://www.cobo.com/cobo-logo.svg" alt="Cobo" style="height:20px;width:auto;filter:brightness(0) invert(1);">
    </div>
    <div class="tn-divider"></div>
    <div class="tn-deck-title">[演示标题]</div>
    <div class="tn-counter" id="slideCounter">01 / N</div>
  </div>

  <!-- Row 2: one button per slide, data-start = data-end = that slide's 0-based index -->
  <div class="tn-row2">
    <button class="tn-ch" data-start="0" data-end="0">
      <span class="tn-ch-num">01</span>
      <span class="tn-ch-name">封面</span>
    </button>
    <button class="tn-ch" data-start="1" data-end="1">
      <span class="tn-ch-num">02</span>
      <span class="tn-ch-name">章节名称</span>
    </button>
    <!-- one <button> per slide; number = zero-padded slide number -->
  </div>

</nav>
<div class="progress-bar" id="progressBar"></div>
```

> **Rule**: Every slide gets its own button in `.tn-row2`. Set `data-start` and `data-end` to the same 0-based index. The number label (`tn-ch-num`) is the slide number zero-padded to 2 digits.

### CSS

```css
:root {
  --nav-h: 78px;  /* row1 36px + row2 42px */
}

/* ── Outer shell ── */
.top-nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 2000;
  height: var(--nav-h);
  background: rgba(13,13,13,0.92);
  backdrop-filter: blur(16px) saturate(120%);
  -webkit-backdrop-filter: blur(16px) saturate(120%);
  /* NEVER add border-bottom here — the progress-bar directly below acts as the bottom edge.
     Adding border-bottom creates two overlapping lines at the nav bottom. */
  display: flex; flex-direction: column;
}

/* ── Row 1: logo + title + counter ── */
.tn-row1 {
  display: flex; align-items: center;
  padding: 0 var(--pad); gap: clamp(0.8rem, 2vw, 2rem);
  height: 36px; flex-shrink: 0;
  border-bottom: 1px solid var(--border);
}
.tn-logo { display:flex; align-items:center; flex-shrink:0; cursor:pointer; }
.tn-divider { width:1px; height:16px; background:var(--border-med); flex-shrink:0; }
.tn-deck-title {
  flex: 1; font-size: clamp(0.6rem, 0.9vw, 0.76rem); font-weight: 500;
  color: var(--text-sec); letter-spacing: 0.03em;
  white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
}
.tn-counter {
  flex-shrink: 0; font-size: clamp(0.55rem, 0.78vw, 0.66rem); font-weight: 600;
  color: var(--text-sec); letter-spacing: 0.1em;
  background: rgba(255,255,255,0.04); border: 1px solid var(--border);
  padding: 2px 9px; border-radius: 20px; transition: color 0.3s;
}

/* ── Row 2: chapter tabs, one per slide ── */
.tn-row2 {
  display: flex; align-items: stretch;
  height: 42px; flex: 1;
}
.tn-ch {
  flex: 1; background: none; border: none;
  border-right: 1px solid var(--border);
  cursor: pointer; font-family: var(--font);
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  gap: 2px; padding: 0 clamp(4px, 0.8vw, 10px);
  position: relative; white-space: nowrap;
  transition: background 0.2s ease;
}
.tn-ch:last-child { border-right: none; }
.tn-ch-num {
  font-size: clamp(0.5rem, 0.65vw, 0.58rem); font-weight: 700;
  color: var(--text-muted); letter-spacing: 0.12em;
  transition: color 0.2s;
}
.tn-ch-name {
  font-size: clamp(0.58rem, 0.85vw, 0.72rem); font-weight: 500;
  color: var(--text-sec);
  transition: color 0.2s;
}
/* No ::after indicator line — active state uses background + text color only */
.tn-ch:hover { background: rgba(255,255,255,0.03); }
.tn-ch:hover .tn-ch-name { color: rgba(255,255,255,0.75); }
.tn-ch.active { background: rgba(124,127,232,0.08); }
.tn-ch.active .tn-ch-num { color: var(--purple); }
.tn-ch.active .tn-ch-name { color: var(--text); font-weight: 600; }

/* ── Progress bar (below nav) ── */
.progress-bar {
  position: fixed; top: var(--nav-h); left: 0; height: 2px;
  background: linear-gradient(90deg, var(--purple), #a5a8ff);
  width: 0%; z-index: 1999; transition: width 0.35s ease;
}
```

### JS — `updateChapters` (in SlidePresentation class)

```javascript
updateChapters(slideIndex) {
  document.querySelectorAll('.tn-ch').forEach(ch => {
    const s = parseInt(ch.dataset.start);
    const e = parseInt(ch.dataset.end);
    ch.classList.toggle('active', slideIndex >= s && slideIndex <= e);
  });
}
```

---

## Slide Structure

**Every slide:**
```css
.slide {
  width: 100vw; height: 100vh; height: 100dvh;
  overflow: hidden; scroll-snap-align: start;
  display: flex; flex-direction: column;
  position: relative; background: var(--bg);
  padding-top: var(--nav-h); /* CRITICAL — reserve space for fixed nav */
}
.slide-content {
  flex: 1; display: flex; flex-direction: column;
  justify-content: center; max-height: 100%;
  overflow: hidden; padding: var(--pad); gap: var(--gap);
}
```

---

## Component Library

### Chip / Category Tag
```html
<div class="chip">LABEL TEXT</div>
```
```css
.chip { display:inline-flex; align-items:center; font-size:var(--label-size); font-weight:600; letter-spacing:0.09em; text-transform:uppercase; color:var(--purple); border:1px solid var(--purple-border); background:var(--purple-dim); padding:2px 10px; border-radius:20px; }
```
Use at top of each content slide to label the section.

---

### Section Divider Slide
```html
<section class="slide slide-section" id="slide-N">
  <div class="section-bg-num">I</div>  <!-- Ghost roman numeral -->
  <div class="section-inner">
    <div class="chip reveal d1">Chapter 1</div>
    <h1 class="reveal d2">Chapter<br><span class="hl">Title Here</span></h1>
  </div>
</section>
```
```css
.slide-section { justify-content:center; align-items:center; }
.section-inner { display:flex; flex-direction:column; align-items:center; text-align:center; padding:var(--pad); position:relative; z-index:1; gap:var(--gap-sm); }
.section-bg-num { position:absolute; inset:var(--nav-h) 0 0 0; display:flex; align-items:center; justify-content:center; font-size:clamp(7rem,20vw,17rem); font-weight:800; color:rgba(255,255,255,0.022); user-select:none; pointer-events:none; letter-spacing:-0.05em; }
```

---

### Stat Cards (company facts)
```html
<div class="g2x4">  <!-- 4-column grid, 2 rows -->
  <div class="stat"><div class="stat-num">500+</div><div class="stat-lbl">机构客户</div></div>
  <!-- ...repeat × 8 -->
</div>
```
```css
.g2x4 { display:grid; grid-template-columns:repeat(4,1fr); gap:var(--gap-sm); }
.stat { background:var(--bg-card); border:1px solid var(--border); border-radius:10px; padding:clamp(0.55rem,1.1vw,0.95rem); text-align:center; }
.stat-num { font-size:clamp(1.1rem,2.2vw,1.85rem); font-weight:800; line-height:1.2; letter-spacing:-0.02em; }
.stat-lbl { font-size:var(--label-size); color:var(--text-sec); margin-top:3px; }
```

---

### Tier Cards (1.0 / 2.0 / 3.0 progression)
```html
<div class="g3">
  <div class="tier">
    <div class="tier-label">1.0 通道</div>
    <div class="tier-name">基础收付通道</div>
    <ul><li>功能点一</li><li>功能点二</li></ul>
  </div>
  <!-- ×3 -->
</div>
```
```css
.g3 { display:grid; grid-template-columns:repeat(3,1fr); gap:var(--gap-sm); }
.tier { background:var(--bg-card); border:1px solid var(--border); border-radius:10px; padding:clamp(0.75rem,1.5vw,1.2rem); position:relative; overflow:hidden; }
.tier::after { content:''; position:absolute; top:0; left:0; right:0; height:2px; background:linear-gradient(90deg,var(--purple),#a5a8ff); }
.tier-label { font-size:var(--label-size); font-weight:700; color:var(--purple); letter-spacing:0.08em; text-transform:uppercase; margin-bottom:5px; }
.tier-name { font-size:var(--h3-size); font-weight:700; margin-bottom:var(--gap-sm); }
```

---

### Capability Cards (4-column)
```html
<div class="g4">
  <div class="cap">
    <div class="cap-icon">📥</div>
    <div class="cap-t">收款</div>
    <ul><li>功能点</li></ul>
  </div>
  <!-- ×4 -->
</div>
```
```css
.g4 { display:grid; grid-template-columns:repeat(4,1fr); gap:var(--gap-sm); }
.cap { background:var(--bg-card); border:1px solid var(--border); border-radius:10px; padding:clamp(0.65rem,1.3vw,1.05rem); }
.cap-icon { font-size:clamp(1rem,1.7vw,1.4rem); margin-bottom:5px; }
.cap-t { font-size:var(--h3-size); font-weight:700; margin-bottom:5px; }
```

---

### Flow Diagram (process arrows)
```html
<div class="flow">
  <div class="flow-box">
    <div class="flow-title">步骤名称</div>
    <div class="flow-desc">说明文字</div>
  </div>
  <div class="flow-arrow">→</div>
  <!-- repeat boxes + arrows -->
</div>
```
```css
.flow { display:flex; align-items:center; gap:clamp(0.25rem,0.7vw,0.55rem); }
.flow-box { flex:1; background:var(--bg-card); border:1px solid var(--border); border-radius:8px; padding:clamp(0.45rem,0.9vw,0.75rem); text-align:center; }
.flow-title { font-size:var(--label-size); font-weight:600; color:var(--purple); margin-bottom:2px; }
.flow-desc { font-size:clamp(0.53rem,0.75vw,0.66rem); color:var(--text-sec); }
.flow-arrow { color:var(--text-muted); font-size:clamp(0.75rem,1.1vw,0.95rem); flex-shrink:0; }
```
Use for: payment flows, process steps, data pipelines.

---

### Architecture Layer Stack
```html
<div class="layers">
  <div class="layer">
    <div class="layer-lbl">用户操作层</div>
    <div class="layer-tags">
      <span class="ltag">API 接入</span>
      <span class="ltag">Portal 接入</span>
    </div>
  </div>
  <!-- repeat for each layer; highlight bottom layer with border-color:var(--purple-border) -->
</div>
```
```css
.layers { display:flex; flex-direction:column; gap:var(--gap-sm); }
.layer { background:var(--bg-card); border:1px solid var(--border); border-radius:8px; display:flex; align-items:center; gap:var(--gap); padding:clamp(0.45rem,0.9vw,0.7rem) clamp(0.7rem,1.3vw,1.1rem); }
.layer-lbl { font-size:var(--small-size); font-weight:600; color:var(--purple); white-space:nowrap; min-width:clamp(65px,10vw,100px); }
.layer-tags { display:flex; flex-wrap:wrap; gap:5px; }
.ltag { background:rgba(124,127,232,0.1); border:1px solid var(--purple-border); border-radius:4px; padding:2px 7px; font-size:clamp(0.53rem,0.75vw,0.65rem); color:var(--text-sec); }
```

---

### Module Grid (6 features, 3×2)
```html
<div class="mods">
  <div class="mod">
    <div class="mod-n">① 功能名</div>
    <div class="mod-t">功能标题</div>
    <div class="mod-d">功能说明，控制在2行以内</div>
  </div>
  <!-- ×6 -->
</div>
```
```css
.mods { display:grid; grid-template-columns:repeat(3,1fr); gap:clamp(0.35rem,0.75vw,0.65rem); }
.mod { background:var(--bg-card); border:1px solid var(--border); border-radius:8px; padding:clamp(0.5rem,1vw,0.85rem); }
.mod-n { font-size:var(--label-size); font-weight:700; color:var(--purple); margin-bottom:3px; letter-spacing:0.05em; }
.mod-t { font-size:clamp(0.62rem,0.95vw,0.8rem); font-weight:700; margin-bottom:3px; }
.mod-d { font-size:clamp(0.56rem,0.78vw,0.68rem); color:var(--text-sec); line-height:1.5; }
```

---

### Highlight Box (key callout)
```html
<div class="hbox">
  Cobo 提供 <strong>MPC 自托管技术</strong>，助力满足 <strong style="color:var(--purple);">MiCA 合规</strong>要求。
</div>
```
```css
.hbox { background:rgba(124,127,232,0.07); border:1px solid var(--purple-border); border-radius:8px; padding:clamp(0.55rem,1.1vw,0.9rem); font-size:var(--body-size); color:var(--text-sec); }
.hbox strong { color:var(--text); font-weight:600; }
```

---

### Case Study / Scenario Layout
```html
<div class="scenario">
  <div class="scenario-tier">
    <!-- Tier label (1.0/2.0/3.0) + bullet list -->
  </div>
  <div>
    <div class="hbox">Case description...</div>
    <div class="flow"><!-- Flow diagram --></div>
  </div>
</div>
```
```css
.scenario { display:grid; grid-template-columns:1fr 2.2fr; gap:var(--gap); align-items:start; }
.scenario-tier { background:linear-gradient(135deg,rgba(124,127,232,0.11),rgba(124,127,232,0.04)); border:1px solid var(--purple-border); border-radius:10px; padding:clamp(0.75rem,1.4vw,1.15rem); }
```

---

### Partner Chips
```html
<div class="partners">
  <span class="ptag hi">Chainalysis</span>
  <span class="ptag">and more...</span>
</div>
```
```css
.partners { display:flex; flex-wrap:wrap; gap:var(--gap-sm); align-items:center; }
.ptag { background:var(--bg-card); border:1px solid var(--border); border-radius:6px; padding:3px 10px; font-size:var(--small-size); color:var(--text-sec); white-space:nowrap; }
.ptag.hi { border-color:var(--purple-border); color:var(--text); }
```

---

### Cover Slide
```html
<section class="slide slide-cover" id="slide-1">
  <div class="cover-body">
    <div class="chip reveal d1">Cobo · 2025</div>
    <h1 class="cover-title reveal d2">
      演示标题<br><span class="hl">关键词高亮</span>
    </h1>
    <div class="cover-meta reveal d3">
      <strong>姓名</strong><br>职位，Cobo<br>日期
    </div>
  </div>
  <div class="cover-orb"></div>  <!-- Animated purple glow orb -->
</section>
```
```css
.slide-cover { background:var(--bg); }
.cover-body { flex:1; display:flex; flex-direction:column; justify-content:center; padding:var(--pad); max-width:65%; gap:var(--gap); }
.cover-title { font-size:clamp(1.8rem,5.2vw,4.2rem); font-weight:800; line-height:1.06; letter-spacing:-0.03em; }
.cover-meta { font-size:var(--body-size); color:var(--text-sec); line-height:1.9; }
.cover-meta strong { color:var(--text); font-weight:600; }
.cover-orb { position:absolute; right:6%; top:50%; transform:translateY(-50%); width:clamp(140px,26vw,340px); height:clamp(140px,26vw,340px); border-radius:50%; background:radial-gradient(circle,rgba(124,127,232,0.2) 0%,rgba(124,127,232,0.05) 55%,transparent 70%); border:1px solid rgba(124,127,232,0.16); animation:orb 5s ease-in-out infinite; }
@keyframes orb { 0%,100%{transform:translateY(-50%) scale(1);opacity:.7} 50%{transform:translateY(-50%) scale(1.06);opacity:1} }
```

---

### Quote / Closing Slides
```css
.slide-quote,.slide-thanks { justify-content:center; align-items:center; }
.quote-txt { font-size:clamp(2rem,6vw,5.2rem); font-weight:800; letter-spacing:-0.04em; text-align:center; line-height:1.08; }
.hl2 { background:linear-gradient(135deg,var(--purple) 0%,#a5a8ff 100%); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
```

---

### Animations

```css
/* Standard entrance animations */
.reveal       { opacity:0; transform:translateY(20px); transition:opacity var(--dur) var(--ease),transform var(--dur) var(--ease); }
.reveal-left  { opacity:0; transform:translateX(-22px); transition:opacity var(--dur) var(--ease),transform var(--dur) var(--ease); }
.reveal-scale { opacity:0; transform:scale(0.93); transition:opacity var(--dur) var(--ease),transform var(--dur) var(--ease); }

/* Add .visible to slide on scroll (via IntersectionObserver) */
.slide.visible .reveal,
.slide.visible .reveal-left,
.slide.visible .reveal-scale { opacity:1; transform:none; }

/* Stagger delays via .d1 → .d8 classes */
.slide.visible .d1 { transition-delay:0.04s; }
.slide.visible .d2 { transition-delay:0.11s; }
.slide.visible .d3 { transition-delay:0.18s; }
.slide.visible .d4 { transition-delay:0.25s; }
.slide.visible .d5 { transition-delay:0.32s; }
.slide.visible .d6 { transition-delay:0.39s; }
.slide.visible .d7 { transition-delay:0.46s; }
.slide.visible .d8 { transition-delay:0.53s; }
```

---

### Right Nav Dots
```css
.nav-dots { position:fixed; right:clamp(0.5rem,1.2vw,1rem); top:50%; transform:translateY(-50%); display:flex; flex-direction:column; gap:5px; z-index:1999; }
.nav-dot { width:4px; height:4px; border-radius:50%; background:var(--text-muted); cursor:pointer; transition:all 0.25s ease; border:none; }
.nav-dot.active { background:var(--purple); box-shadow:0 0 5px var(--purple); transform:scale(1.6); }
```

---

## Responsive Breakpoints (copy into every presentation)

```css
@media (max-height: 700px) {
  :root { --pad:clamp(0.7rem,2.8vw,1.8rem); --gap:clamp(0.3rem,0.9vw,0.85rem); --title-size:clamp(1.2rem,4vw,2.3rem); --h2-size:clamp(1rem,2.5vw,1.55rem); }
}
@media (max-height: 600px) {
  :root { --pad:clamp(0.5rem,1.8vw,1.1rem); --gap:clamp(0.2rem,0.65vw,0.55rem); --body-size:clamp(0.6rem,0.92vw,0.78rem); }
  .nav-dots, .tn-chapters { display:none; }
}
@media (max-height: 500px) {
  :root { --pad:clamp(0.35rem,1.3vw,0.75rem); --title-size:clamp(0.95rem,3.2vw,1.4rem); --h2-size:clamp(0.88rem,2.1vw,1.15rem); }
}
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration:0.01ms !important; transition-duration:0.2s !important; }
  html { scroll-behavior:auto; }
}
```

---

## Common Utility Classes

```css
.hl  { color:var(--purple); }
.hl2 { background:linear-gradient(135deg,var(--purple),#a5a8ff); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
.g2  { display:grid; grid-template-columns:repeat(2,1fr); gap:var(--gap); }
.g3  { display:grid; grid-template-columns:repeat(3,1fr); gap:var(--gap-sm); }
.g4  { display:grid; grid-template-columns:repeat(4,1fr); gap:var(--gap-sm); }
.card { background:var(--bg-card); border:1px solid var(--border); border-radius:10px; padding:clamp(0.65rem,1.3vw,1.05rem); transition:border-color 0.22s,background 0.22s; }
.card:hover { border-color:var(--purple-border); background:var(--bg-card2); }
.card-title { font-size:var(--h3-size); font-weight:700; margin-bottom:var(--gap-sm); }
.glow-line { width:clamp(32px,5vw,54px); height:2px; background:linear-gradient(90deg,var(--purple),#a5a8ff); border-radius:2px; }
ul { list-style:none; }
ul li { padding-left:1.1em; position:relative; }
ul li::before { content:'·'; position:absolute; left:0; color:var(--purple); font-weight:700; }
```

---

## Cobo Products Reference

When generating product content, use these accurate terms:

| Product | Description |
|---------|-------------|
| Cobo Portal | All-in-one web dashboard for wallet operations |
| Custodial Wallets | Cobo-managed, institutional-grade custody |
| MPC Wallets | Multi-party computation — no single point of failure |
| Smart Contract Wallets | EVM contract-based, programmable policies |
| Exchange Wallets | API-based exchange account management |
| Cobo Guard | Mobile app for transaction approval (MFA) |
| Cobo Payment SDK | Stablecoin payment integration toolkit |
| Tokenization App | One-click stablecoin / RWA issuance |
| OTC App | In-platform fiat settlement with OTC partners |
| WaaS 2.0 | Wallet-as-a-Service API platform |

**Partners (use as examples):** Alchemy Pay, Bitget, HashKey, AntPool, Galaxy, Wintermute, Chainalysis, Elliptic

---

## Certifications to mention when relevant

- ISO 27001 certified
- SOC 2 Type 1 & 2 certified
- Singapore-licensed (MAS)
- 8+ years zero security incident

---

## What NOT to do

- ❌ Use Inter, Roboto, or system fonts
- ❌ Use purple gradients on white backgrounds
- ❌ Add illustrations or icons beyond emoji
- ❌ Let slide content scroll
- ❌ Cram more than 6 bullet points per slide
- ❌ Show the style selection phase (always use Cobo Brand)
- ❌ Forget `padding-top: var(--nav-h)` on slides
- ❌ Negate CSS functions directly (`-clamp()` is invalid — use `calc(-1 * clamp(...))`)
- ❌ Add `border-bottom` to `.top-nav` — the progress bar sits flush below and serves as the bottom edge; a nav `border-bottom` creates two overlapping lines
