<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/banner-light.svg">
  <img alt="PerfectReadme" src="./assets/banner-dark.svg" width="100%">
</picture>

<p align="center">
  <strong>A Claude Code skill that transforms plain README files into stunning, website-like experiences</strong>
</p>

<p align="center">
  <a href="#-what-it-does">What It Does</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="#-techniques">Techniques</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="#-installation">Installation</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="#-usage">Usage</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="#-examples">Examples</a>&nbsp;&nbsp;&bull;&nbsp;&nbsp;<a href="#-license">License</a>
</p>

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;What It Does

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/before-after.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/before-after.svg">
  <img alt="Before and After" src="./assets/before-after.svg" width="100%">
</picture>

<br>

PerfectReadme is a skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that generates GitHub-ready README files with **animated SVG banners**, **multi-column layouts**, **dark/light theme support**, and a **bold design philosophy** borrowed from the frontend-design skill.

It knows exactly what GitHub's markdown renderer allows and what it strips — so every technique it uses actually works in production.

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;Techniques

<table>
<tr>
<td width="50%" valign="top">

### SVG + foreignObject

The core technique. Full CSS inside SVG files — animations, custom Google Fonts, gradients, `prefers-color-scheme`. GitHub strips all CSS from markdown, but SVG files bypass this entirely.

```xml
<svg xmlns="..." width="800" height="200">
  <foreignObject width="100%" height="100%">
    <div xmlns="...">
      <style>
        @keyframes float { ... }
        .title { animation: float 3s infinite; }
      </style>
    </div>
  </foreignObject>
</svg>
```

</td>
<td width="50%" valign="top">

### Dark / Light Theme

Native `<picture>` element with `prefers-color-scheme` media queries. Serve different SVGs or images depending on the user's system theme — no JavaScript required.

```html
<picture>
  <source media="(prefers-color-scheme: dark)"
          srcset="./assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)"
          srcset="./assets/banner-light.svg">
  <img src="./assets/banner-dark.svg">
</picture>
```

</td>
</tr>
<tr>
<td width="50%" valign="top">

### Multi-Column Layouts

HTML tables with `width`, `align`, and `valign` attributes create responsive-ish multi-column layouts. Markdown renders inside `<td>` cells when separated by blank lines.

```html
<table>
<tr>
<td width="33%">Column 1</td>
<td width="33%">Column 2</td>
<td width="33%">Column 3</td>
</tr>
</table>
```

</td>
<td width="50%" valign="top">

### Interactive Accordions

`<details>` and `<summary>` create expandable sections — perfect for API docs, FAQs, and long content. Use `open` attribute for default-expanded sections.

```html
<details>
<summary>Click to expand</summary>

Full Markdown content inside,
including code blocks and images.

</details>
```

</td>
</tr>
</table>

<br>

<details>
<summary><strong>Full list of what GitHub allows &amp; strips</strong></summary>

<br>

**Allowed HTML:** `div`, `table`, `details`, `summary`, `picture`, `source`, `img`, `a`, `br`, `hr`, `kbd`, `sup`, `sub`, `code`, `pre`, `blockquote`, `p`, `span`, `h1`–`h6`, `ul`, `ol`, `li`, `dl`, `dt`, `dd`, `figure`, `figcaption`, `b`, `strong`, `i`, `em`, `del`, `ins`, `mark`, `small`, `abbr`, `time`, `ruby`, `rt`, `rp`

**Allowed attributes:** `href`, `src`, `alt`, `width`, `height`, `align`, `valign`, `colspan`, `rowspan`, `open`, `srcset`, `media`, `type`

**Stripped:** `style`, `class`, `id`, `<script>`, `<iframe>`, `<form>`, `<input>`, `<button>`, `<style>`, `<link>`, `<embed>`, `<object>`, `<audio>`, all event handlers, inline SVG

</details>

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;Installation

### From GitHub (as a Claude Code plugin)

```bash
claude plugin add --from-github YOUR_USERNAME/PerfectReadme
```

### Manual (local skill)

Copy the skill file to your Claude skills directory:

```bash
mkdir -p ~/.claude/skills/perfect-readme
cp skills/perfect-readme/SKILL.md ~/.claude/skills/perfect-readme/
```

The skill will be available in your next Claude Code session.

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;Usage

Once installed, use the skill by asking Claude Code to create a README:

```
Create a README for my project
```

```
/perfect-readme
```

```
Make a stunning GitHub profile README for my account
```

The skill will:

1. **Analyze** your project — code, dependencies, purpose
2. **Choose an aesthetic direction** — tone, palette, typography
3. **Generate SVG assets** — animated banners with dark/light theme support
4. **Build the README** — with multi-column layouts, accordions, badges, and navigation
5. **Deliver everything** — `README.md` + `assets/` directory, ready to push

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;Examples

<details open>
<summary><strong>Animated SVG Banner</strong></summary>

<br>

Banners use CSS `@keyframes` inside `<foreignObject>` — gradient shifts, floating elements, pulsing glows. Custom Google Fonts load via `@import`. Both dark and light variants are generated automatically.

This README's own banner is a live example — check [`assets/banner-dark.svg`](./assets/banner-dark.svg).

</details>

<details>
<summary><strong>Feature Grid</strong></summary>

<br>

```html
<table>
<tr>
<td align="center" width="33%">
<img src="./assets/icon.svg" width="48"><br>
<strong>Feature Name</strong><br>
<sub>Short description of the feature</sub>
</td>
<!-- repeat for each feature -->
</tr>
</table>
```

</details>

<details>
<summary><strong>API Documentation with Accordions</strong></summary>

<br>

```html
<details>
<summary><code>createReadme(options)</code></summary>

Generates a complete README with all assets.

| Parameter | Type | Description |
|-----------|------|-------------|
| `project` | `string` | Project name |
| `tone` | `string` | Aesthetic direction |

</details>
```

</details>

<details>
<summary><strong>Gradient Dividers</strong></summary>

<br>

Simple SVG files with a linear gradient — used between sections for visual rhythm. See [`assets/divider-dark.svg`](./assets/divider-dark.svg) for the implementation.

</details>

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;Project Structure

```
PerfectReadme/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata
├── skills/
│   └── perfect-readme/
│       └── SKILL.md          # The skill definition
├── assets/
│   ├── banner-dark.svg       # Animated banner (dark theme)
│   ├── banner-light.svg      # Animated banner (light theme)
│   ├── before-after.svg      # Visual comparison
│   ├── divider-dark.svg      # Section divider (dark)
│   └── divider-light.svg     # Section divider (light)
├── LICENSE
└── README.md                 # You are here
```

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;Design Philosophy

This skill adapts the [frontend-design](https://github.com/anthropics/claude-code-plugins) skill's philosophy to the README medium:

- **Bold aesthetic direction** — every README gets a unique visual identity, not a template
- **Typography matters** — distinctive Google Fonts loaded inside SVGs, never system defaults
- **Color with intent** — palettes matched to the project's domain and personality
- **Motion with purpose** — subtle CSS animations that add polish without distraction
- **Theme-aware** — every visual element supports both dark and light GitHub themes

<br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/divider-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="./assets/divider-light.svg">
  <img alt="" src="./assets/divider-dark.svg" width="100%">
</picture>

<br>

## &nbsp;License

[MIT](./LICENSE)

<br>

<p align="center">
  <a href="https://oxgeneral.github.io/PerfectReadme"><strong>View Landing Page &rarr;</strong></a>
</p>

<p align="center">
  <sub>Built with the skill itself. This README is a live demo.</sub>
</p>
