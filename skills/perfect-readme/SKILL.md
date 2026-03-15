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

### 1. SVG with `<foreignObject>` — THE Key Technique

This is the PRIMARY tool for achieving website-like aesthetics. Create `.svg` files that contain full HTML + CSS inside `<foreignObject>`. This bypasses GitHub's CSS restrictions entirely.

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="800" height="400">
  <foreignObject width="100%" height="100%">
    <div xmlns="http://www.w3.org/1999/xhtml">
      <style>
        @import url('https://fonts.googleapis.com/css2?family=FONT_NAME&display=swap');

        * { margin: 0; padding: 0; box-sizing: border-box; }

        .banner {
          width: 800px; height: 400px;
          background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
          display: flex; align-items: center; justify-content: center;
          font-family: 'FONT_NAME', sans-serif;
          color: white; position: relative; overflow: hidden;
        }

        /* CSS animations work fully here */
        @keyframes float {
          0%, 100% { transform: translateY(0); }
          50% { transform: translateY(-20px); }
        }

        .title {
          font-size: 48px; font-weight: 900;
          animation: float 3s ease-in-out infinite;
        }

        /* Dark/light theme detection works inside SVG */
        @media (prefers-color-scheme: light) {
          .banner { background: linear-gradient(135deg, #f5f7fa, #c3cfe2); color: #1a1a2e; }
        }
      </style>
      <div class="banner">
        <div class="title">Project Name</div>
      </div>
    </div>
  </foreignObject>
</svg>
```

Then reference in README: `![Banner](./assets/banner.svg)`

**SVG Design Guidelines:**
- Use Google Fonts via `@import` for distinctive typography — NEVER default to system fonts
- CSS `@keyframes` animations auto-play — use for floating, pulsing, gradient shifts, typing effects
- SMIL `<animate>` and `<animateTransform>` also work for path animations
- `prefers-color-scheme` media query works — always support dark AND light themes
- Set explicit `width` and `height` on the SVG root
- `:hover` does NOT work (SVGs render as `<img>` elements, no interaction passes through)
- JavaScript does NOT work inside SVG on GitHub
- Keep SVG file sizes reasonable — under 100KB for fast loading

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
