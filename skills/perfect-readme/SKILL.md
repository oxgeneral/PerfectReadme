---
name: perfect-readme
description: "Create stunning, website-like GitHub README files with animated SVG banners, multi-column layouts, dark/light theme support, and bold visual design. Use when the user wants to create or redesign a README.md for a GitHub repository or profile. Triggers on: 'readme', 'README', 'profile readme', 'github profile', 'project documentation page'."
---

This skill creates distinctive, visually striking GitHub README files that look and feel like polished websites — while working within GitHub's markdown rendering constraints. Every README should be UNFORGETTABLE, not a generic template.

The user provides context about their project, profile, or repository. They may specify tone, audience, or technical details.

## Design Thinking (from frontend-design philosophy)

Before writing ANY markdown, commit to a BOLD aesthetic direction:

- **Purpose**: What does this project/profile communicate? Who reads it?
- **Tone**: Pick a clear direction — brutally minimal, retro-terminal, luxury/refined, playful/vibrant, editorial/magazine, cyberpunk/neon, organic/nature, corporate/clean, indie/handcrafted, scientific/data-driven. Use these for inspiration but design one true to the project's soul.
- **Differentiation**: What makes this README UNFORGETTABLE? What's the one thing someone will remember after scrolling through?
- **Signature Element**: Every great README has ONE hero element — an animated SVG banner, a striking layout, a clever visual metaphor. Decide this first.

**CRITICAL**: Generic READMEs with default badges and plain text are the equivalent of "AI slop" in frontend. Commit to a vision and execute with precision.

## GitHub Markdown Rendering — What Works

### Allowed HTML Tags
`<div>`, `<table>`, `<tr>`, `<td>`, `<th>`, `<details>`, `<summary>`, `<picture>`, `<source>`, `<img>`, `<a>`, `<br>`, `<hr>`, `<kbd>`, `<sup>`, `<sub>`, `<samp>`, `<code>`, `<pre>`, `<b>`, `<strong>`, `<i>`, `<em>`, `<del>`, `<ins>`, `<mark>`, `<small>`, `<blockquote>`, `<p>`, `<span>`, `<h1>`–`<h6>`, `<ul>`, `<ol>`, `<li>`, `<dl>`, `<dt>`, `<dd>`, `<figure>`, `<figcaption>`, `<ruby>`, `<rt>`, `<rp>`, `<abbr>`, `<dfn>`, `<time>`, `<wbr>`, `<video>` (GitHub-hosted only)

### Allowed Attributes (limited set)
- `<a>`: `href`
- `<img>`: `src`, `alt`, `height`, `width`, `align`
- `<td>`, `<th>`: `align`, `width`, `colspan`, `rowspan`
- `<p>`, `<div>`, `<h1>`–`<h6>`: `align`
- `<details>`: `open`
- `<source>`: `srcset`, `media`, `type`

### What Does NOT Work (stripped by GitHub sanitizer)
- `style=""` inline styles — STRIPPED
- `<style>` blocks — STRIPPED
- `class`, `id` attributes — STRIPPED
- `<script>`, `<iframe>`, `<form>`, `<input>`, `<button>` — STRIPPED
- `<embed>`, `<object>`, `<link>` — STRIPPED
- `onclick` and all JS event handlers — STRIPPED
- `<audio>` — NOT SUPPORTED
- Inline `<svg>` — STRIPPED (but SVG files via `<img>` work!)

## Power Techniques

### 1. Pure SVG with SMIL Animations — THE Key Technique

This is the PRIMARY tool for achieving website-like aesthetics. Create `.svg` files using native SVG elements with SMIL animations. GitHub proxies SVG images through `camo.githubusercontent.com` which **strips `<foreignObject>` and all CSS/HTML inside it**. Only pure SVG elements survive.

**CRITICAL: `<foreignObject>` does NOT work on GitHub.** GitHub's image proxy sanitizes it. Use native SVG only.

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 200" width="800" height="200">
  <defs>
    <!-- Gradients for colors -->
    <linearGradient id="bg" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#0a0a0f"/>
      <stop offset="100%" stop-color="#111127"/>
    </linearGradient>
    <linearGradient id="title-grad" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#a5b4fc"/>
      <stop offset="100%" stop-color="#22d3ee"/>
      <!-- Animated gradient shift -->
      <animate attributeName="x1" values="-100%;0%;-100%" dur="4s" repeatCount="indefinite"/>
      <animate attributeName="x2" values="0%;100%;0%" dur="4s" repeatCount="indefinite"/>
    </linearGradient>
    <!-- Glow filter -->
    <filter id="glow" x="-50%" y="-50%" width="200%" height="200%">
      <feGaussianBlur stdDeviation="40" result="blur"/>
      <feComposite in="blur" operator="over"/>
    </filter>
    <!-- Grid pattern -->
    <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
      <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#6366f1" stroke-opacity="0.06" stroke-width="1"/>
    </pattern>
  </defs>

  <!-- Background + grid -->
  <rect width="800" height="200" fill="url(#bg)"/>
  <rect width="800" height="200" fill="url(#grid)"/>

  <!-- Animated glow orbs -->
  <ellipse cx="200" cy="50" rx="150" ry="150" fill="#6366f1" opacity="0.15" filter="url(#glow)">
    <animate attributeName="cx" values="200;240;180;200" dur="8s" repeatCount="indefinite"/>
    <animate attributeName="opacity" values="0.15;0.22;0.15" dur="8s" repeatCount="indefinite"/>
  </ellipse>

  <!-- Title text with gradient fill -->
  <text x="400" y="105" text-anchor="middle" font-family="'Segoe UI', Arial, sans-serif"
        font-size="48" font-weight="800" fill="url(#title-grad)" letter-spacing="-2">
    Project Name
  </text>

  <!-- Animated decorative line -->
  <rect x="340" y="125" width="120" height="1" fill="#6366f1" rx="0.5">
    <animate attributeName="width" values="80;160;80" dur="3s" repeatCount="indefinite"/>
    <animate attributeName="x" values="360;320;360" dur="3s" repeatCount="indefinite"/>
    <animate attributeName="opacity" values="0.4;1;0.4" dur="3s" repeatCount="indefinite"/>
  </rect>
</svg>
```

Then reference in README: `![Banner](./assets/banner.svg)`

**SVG Design Guidelines:**
- Use ONLY native SVG elements: `<text>`, `<rect>`, `<circle>`, `<ellipse>`, `<path>`, `<polygon>`, `<line>`
- Use `<defs>` for `<linearGradient>`, `<radialGradient>`, `<pattern>`, `<filter>` definitions
- Use SMIL `<animate>` and `<animateTransform>` for animations — these survive GitHub's proxy
- Animate gradient `x1`/`x2` for shimmer effects, element `cx`/`cy` for floating, `opacity` for pulsing
- Use `<feGaussianBlur>` filters for glow effects
- Use `<pattern>` for grid/dot backgrounds
- Set `viewBox` and explicit `width`/`height` on the SVG root
- `<foreignObject>`, CSS `@keyframes`, `@import`, `<style>`, JavaScript — ALL stripped by GitHub
- `:hover` does NOT work (SVGs render as `<img>` elements)
- Keep SVG file sizes under 100KB for fast loading
- For dark/light themes — create TWO separate SVG files and use `<picture>` in README

### 2. Dark/Light Theme Images

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/logo-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/logo-light.svg">
  <img alt="Logo" src="./assets/logo-light.svg" width="200">
</picture>
```

Use this for ALL visual elements — banners, logos, diagrams, section headers. Always provide both themes.

### 3. Multi-Column Layouts via Tables

```html
<table>
<tr>
<td width="50%" valign="top">

**Left Column**

Content with full Markdown support inside table cells.

</td>
<td width="50%" valign="top">

**Right Column**

More content here.

</td>
</tr>
</table>
```

Use `width` percentages for responsive-ish columns. `align` and `valign` attributes work. Blank lines around Markdown content inside `<td>` are required for proper rendering.

### 4. Accordion Sections

```html
<details>
<summary><strong>Click to expand</strong></summary>

Hidden content with full Markdown support.

```code blocks work here too```

</details>
```

Use `<details open>` for default-expanded sections. Chain multiple `<details>` blocks for FAQ-style layouts.

### 5. Badges & Dynamic Elements

```markdown
<!-- Shields.io badges -->
![License](https://img.shields.io/github/license/user/repo?style=for-the-badge&color=blue)
![Stars](https://img.shields.io/github/stars/user/repo?style=for-the-badge)

<!-- GitHub Stats Cards -->
![Stats](https://github-readme-stats.vercel.app/api?username=USER&show_icons=true&theme=radical)

<!-- Custom badge with logo -->
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
```

Badge styles: `flat`, `flat-square`, `plastic`, `for-the-badge`, `social`. Choose ONE style consistently.

### 6. Navigation with Anchor Links

```markdown
<p align="center">
  <a href="#features">Features</a> •
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a> •
  <a href="#api">API</a> •
  <a href="#contributing">Contributing</a>
</p>
```

### 7. Keyboard Keys

```html
Press <kbd>Ctrl</kbd> + <kbd>C</kbd> to copy
```

### 8. Aligned Content

```html
<p align="center">Centered text or images</p>
<p align="right">Right-aligned content</p>
<div align="center">Block of centered content</div>
```

`align` is the ONLY layout attribute that works natively. Use it extensively.

## README Aesthetic Guidelines

Adapted from frontend-design philosophy for the README medium:

- **Typography (via SVG)**: Use distinctive Google Fonts — Clash Display, Cabinet Grotesk, Satoshi, General Sans, Syne, Space Mono, JetBrains Mono, Playfair Display, Instrument Serif, DM Serif Display. NEVER use Inter, Roboto, Arial, or system defaults. Pair a bold display font with a clean mono/body font.
- **Color Palettes**: Commit to a cohesive palette. Use 2-3 dominant colors with 1 sharp accent. Avoid generic purple-on-white gradients. Match colors to the project's domain — terminal green for CLI tools, warm earth tones for design tools, electric blue for dev tools, rich amber for data tools.
- **Motion (via SVG animations)**: Subtle, purposeful animations — floating elements, gradient shifts, pulsing glows, typing effects, waveforms. One well-crafted animation creates more impact than many scattered ones. Keep animations smooth (3-6s cycles) and non-distracting.
- **Visual Hierarchy**: Hero banner → badges → one-liner description → navigation → key sections. The first viewport (before scroll) must hook the reader.
- **Spacing**: Use `<br>` and blank lines generously. Dense walls of text are the enemy. Whitespace is a design tool.
- **Consistency**: One badge style throughout. One heading style. One code block style. Cohesion over variety.

**NEVER create generic READMEs with:**
- Plain text without visual elements
- Default GitHub formatting with no HTML enhancements
- Cookie-cutter badge rows with no design thought
- Walls of text without visual breaks
- Generic "Built with" sections that add no value
- Stock screenshot placeholders

## Output Structure

When creating a README, ALWAYS deliver:

1. **`README.md`** — the main file with all markup
2. **`assets/` directory** with:
   - `banner.svg` (or `header.svg`) — animated SVG hero banner with dark/light theme support
   - `banner-dark.svg` + `banner-light.svg` — if using `<picture>` approach instead
   - Any additional SVG section headers or visual elements
3. **Brief explanation** of the design choices made

## Workflow

1. **Gather context** — read the project's code, package.json, existing README, understand what it does
2. **Choose aesthetic direction** — based on project type, audience, and tone
3. **Design the hero banner SVG** — this is the signature element, spend the most creative energy here
4. **Structure the layout** — plan sections, navigation, columns, accordions
5. **Write content** — concise, scannable, with personality matching the aesthetic
6. **Add dynamic elements** — badges, stats, theme support
7. **Polish** — spacing, alignment, visual rhythm, consistency check

## Examples of Section Patterns

### Hero Section Pattern
```
[Animated SVG Banner with dark/light support]
[Centered one-liner tagline]
[Badge row — version, license, build status]
[Navigation links]
```

### Feature Grid Pattern
```html
<table>
<tr>
<td align="center" width="33%">
<img src="./assets/icon1.svg" width="48"><br>
<strong>Feature 1</strong><br>
<sub>Brief description</sub>
</td>
<td align="center" width="33%">
<img src="./assets/icon2.svg" width="48"><br>
<strong>Feature 2</strong><br>
<sub>Brief description</sub>
</td>
<td align="center" width="33%">
<img src="./assets/icon3.svg" width="48"><br>
<strong>Feature 3</strong><br>
<sub>Brief description</sub>
</td>
</tr>
</table>
```

### Quick Start Pattern
```
<details open>
<summary><h3>Quick Start</h3></summary>

\`\`\`bash
npm install package-name
\`\`\`

</details>
```

### API Reference Pattern (Accordion)
```
<details>
<summary><code>methodName(args)</code> — brief description</summary>

Full documentation with examples.

</details>
```

Remember: Claude is capable of extraordinary creative work. Don't hold back — show what can truly be created when committing fully to a distinctive vision. Every README should make the viewer stop scrolling and think "wow, this project clearly cares about quality."
