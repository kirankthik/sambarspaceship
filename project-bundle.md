# Sambar Spaceship — Project Bundle

Hugo static site. Folder tree (excluding `.git`, `.DS_Store`, and the generated `public/` directory) followed by the contents of every source file.

Note: several template files (`baseof_old.html`, `list.html`, `single.html`, `partials/header.html`, `partials/footer.html`) and `static/css/style.css` are stored as Cocoa HTML / RTF exports on disk. The sections below show the de-escaped template source that those files actually contain. Images (`content/comics/first/comic.png`, `themes/.../static/images/logo.png`) are binary and omitted.

## Folder tree

```
sambarspaceship/
├── hugo.toml
├── archetypes/
│   └── default.md
├── assets/                          (empty)
├── content/
│   └── comics/
│       └── first/
│           ├── comic.png            (binary)
│           └── index.md
├── data/                            (empty)
├── i18n/                            (empty)
├── static/                          (empty)
├── themes/
│   └── sambar-on-a-spaceship/
│       ├── theme.toml
│       ├── assets/                  (empty)
│       ├── layouts/
│       │   ├── index.html
│       │   ├── _default/
│       │   │   ├── baseof.html
│       │   │   ├── baseof_old.html
│       │   │   ├── list.html
│       │   │   └── single.html
│       │   └── partials/
│       │       ├── footer.html
│       │       └── header.html
│       └── static/
│           ├── css/
│           │   ├── main.css
│           │   └── style.css
│           └── images/
│               └── logo.png         (binary)
└── public/                          (Hugo build output — omitted)
```

---

## `hugo.toml`

```toml
baseURL = "http://localhost:1313/"
languageCode = "en-us"
title = "Sambar Spaceship"
theme = "sambar-on-a-spaceship"
```

## `archetypes/default.md`

```md
+++
date = '{{ .Date }}'
draft = true
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
+++
```

## `content/comics/first/index.md`

```md
---
title: "My First Space Comic"
date: 2026-04-05
description: "The lifelong cooking struggle — from burning onions at age 8 to finally having an AI sous-chef at 34."
comicImage: "comic.png"
tags: ["cooking", "AI", "life"]
---

The lifelong cooking struggle — from burning onions at age 8 to finally getting an AI sous-chef at 34. It's not perfect, but it's mine and it's edible!
```

## `themes/sambar-on-a-spaceship/theme.toml`

```toml
name = "Sambar on a Spaceship"
license = "MIT"
description = "Maximalist cosmic comic theme"
```

## `themes/sambar-on-a-spaceship/layouts/index.html`

```html
{{ define "main" }}
<h2>Latest Comics</h2>
<ul>
  {{ range where .Site.RegularPages "Section" "comics" }}
    <li>
      <a href="{{ .RelPermalink }}">{{ .Title }}</a>
    </li>
  {{ end }}
</ul>
{{ end }}
```

## `themes/sambar-on-a-spaceship/layouts/_default/baseof.html`

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>{{ .Title }} | Sambar Spaceship</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Exo+2:wght@400;700;900&family=Press+Start+2P&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>

  <!-- COCKPIT DASHBOARD HEADER -->
  <header class="cockpit-header">
    <!-- Scanline overlay -->
    <div class="scanlines"></div>

    <!-- Top instrument panel -->
    <div class="instrument-bar top-bar">
      <div class="gauge gauge-left">
        <span class="gauge-label">FUEL</span>
        <div class="gauge-meter"><div class="gauge-fill fuel-fill"></div></div>
      </div>
      <div class="status-lights">
        <span class="light light-red blink-slow"></span>
        <span class="light light-amber blink-fast"></span>
        <span class="light light-green pulse"></span>
        <span class="light light-cyan pulse"></span>
        <span class="light light-amber blink-slow"></span>
      </div>
      <div class="gauge gauge-right">
        <span class="gauge-label">SAMBAR TEMP</span>
        <div class="gauge-meter"><div class="gauge-fill temp-fill"></div></div>
      </div>
    </div>

    <!-- Main logo area -->
    <div class="logo-bay">
      <div class="logo-glow"></div>
      <a href="/" class="logo-link">
        <img src="/images/logo.png" alt="Sambar Spaceship Studios" class="logo-img">
      </a>
    </div>

    <!-- Navigation as ship controls -->
    <nav class="ship-controls">
      <div class="control-panel">
        <a href="/" class="control-btn active">
          <span class="btn-icon">◈</span>
          <span class="btn-label">BRIDGE</span>
        </a>
        <a href="/comics/" class="control-btn">
          <span class="btn-icon">◉</span>
          <span class="btn-label">COMICS</span>
        </a>
        <a href="/about/" class="control-btn">
          <span class="btn-icon">◎</span>
          <span class="btn-label">CREW LOG</span>
        </a>
      </div>
    </nav>

    <!-- Bottom instrument readout -->
    <div class="instrument-bar bottom-bar">
      <div class="readout">
        <span class="readout-label">SECTOR:</span>
        <span class="readout-value">7G-SAMBAR</span>
      </div>
      <div class="readout">
        <span class="readout-label">STATUS:</span>
        <span class="readout-value status-online">OPERATIONAL</span>
      </div>
      <div class="readout">
        <span class="readout-label">COORDINATES:</span>
        <span class="readout-value">42.069 / 80.085</span>
      </div>
    </div>
  </header>

  <!-- MAIN VIEWPORT -->
  <main class="viewport">
    {{ block "main" . }}{{ end }}
  </main>

  <!-- FOOTER PANEL -->
  <footer class="hull-plate">
    <div class="hull-inner">
      <p class="hull-text">POWERED BY SAMBAR AND STARDUST ✨ &mdash; ALL SYSTEMS NOMINAL</p>
      <div class="hull-lights">
        <span class="hull-light"></span>
        <span class="hull-light"></span>
        <span class="hull-light"></span>
      </div>
    </div>
  </footer>

</body>
</html>
```

## `themes/sambar-on-a-spaceship/layouts/_default/baseof_old.html`

Stored on disk as a Cocoa-HTML export; the actual Hugo template it contains is:

```html
<!DOCTYPE html>
<html lang="{{ site.LanguageCode | default "en-us" }}">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ block "title" . }}{{ .Title }} | {{ site.Title }}{{ end }}</title>
    <link rel="stylesheet" href="{{ "css/style.css" | relURL }}">
</head>
<body>
    <div class="layout-grid">
        {{ partial "header.html" . }}

        <main>
            {{ block "main" . }}{{ end }}
        </main>

        {{ partial "footer.html" . }}
    </div>
</body>
</html>
```

## `themes/sambar-on-a-spaceship/layouts/_default/list.html`

Stored on disk as a Cocoa-HTML export; actual template:

```html
{{ define "main" }}
    <h1 style="font-size: 3rem; background: var(--cyber-turmeric); border: var(--line-thick); display: inline-block; padding: 10px; margin-bottom: 40px; box-shadow: var(--flat-shadow);">
        UPLOADING RECENT DATAPACKS...
    </h1>

    <div class="story-list">
        {{ range .Pages }}
        <article class="story-card">
            <h2><a href="{{ .RelPermalink }}" style="color: inherit; text-decoration: none;">{{ .Title }}</a></h2>
            <p style="margin-top: 15px; font-weight: bold;">
                {{ .Summary }}
            </p>
            <div style="margin-top: 20px;">
                <a href="{{ .RelPermalink }}" style="background: var(--plasma-pink); border: var(--line-thick); padding: 5px 10px; color: var(--space-black); text-decoration: none; font-weight: 900; text-transform: uppercase;">
                    Initialize Sequence >
                </a>
            </div>
        </article>
        {{ end }}
    </div>
{{ end }}
```

## `themes/sambar-on-a-spaceship/layouts/_default/single.html`

Stored on disk as a Cocoa-HTML export; actual template:

```html
{{ define "main" }}
    <article>
        <header style="border-bottom: var(--line-thick); padding-bottom: 20px; margin-bottom: 30px;">
            <h1 style="font-size: 4rem; text-transform: uppercase; line-height: 1; background: var(--hologram-cyan); display: inline-block; padding: 10px; border: var(--line-thick); box-shadow: var(--flat-shadow);">
                {{ .Title }}
            </h1>
            <div style="margin-top: 20px; font-weight: bold; background: var(--neon-banana); display: inline-block; padding: 5px; border: var(--line-thick);">
                LOG DATE: {{ .Date.Format "2006-01-02" }}
            </div>
        </header>

        <div class="svg-stage">
            {{ if .Params.svg_file }}
                {{ partial .Params.svg_file . }}
            {{ else }}
                <div style="color: var(--neon-banana); padding: 50px; text-align: center; font-family: monospace;">
                    [ AWAITING SVG VISUAL DATA FROM ORBITAL SATELLITE ]
                </div>
            {{ end }}
        </div>

        <div class="content-body">
            {{ .Content }}
        </div>
    </article>
{{ end }}
```

## `themes/sambar-on-a-spaceship/layouts/partials/header.html`

Stored on disk as a Cocoa-HTML export; actual template:

```html
<header>
    <div class="site-title">
        <a href="{{ site.Home.RelPermalink }}" style="color: inherit; text-decoration: none;">
            {{ site.Title | default "Sambar on a Spaceship" }}
        </a>
    </div>
    <nav>
        <a href="/">Terminal</a>
        <a href="/about">Crew Manifest</a>
    </nav>
</header>
```

## `themes/sambar-on-a-spaceship/layouts/partials/footer.html`

Stored on disk as a Cocoa-HTML export; actual template:

```html
<footer>
    <p>TRANSMITTING FROM LOW-EARTH ORBIT // POWERED BY FILTER KAAPI & HIGH-VOLTAGE DOSA BATTER</p>
    <p>&copy; {{ now.Year }} Sambar on a Spaceship</p>
</footer>
```

## `themes/sambar-on-a-spaceship/static/css/main.css`

833 lines — the active stylesheet loaded by `baseof.html`. Palette, animations, cockpit header, viewport, and comic page styles.

```css
/* ============================================================
   SAMBAR SPACESHIP — MAIN.CSS
   Aesthetic: HYPERMODERN SPACE — Bright, Colorful, Cosmic Joy
   Vivid gradients · Glass panels · Neon pops · Cosmic energy
   ============================================================ */

/* --- CUSTOM PROPERTIES --- */
:root {
  /* Vibrant palette from the logo */
  --orange: #FF8C00;
  --amber: #FFAA00;
  --yellow: #FFE700;
  --cyan: #00F0FF;
  --teal: #00CCA8;
  --magenta: #FF3DA6;
  --pink: #FF69B4;
  --red: #FF2244;
  --green: #39FF14;
  --violet: #8B5CF6;
  --indigo: #6366F1;
  --sky: #38BDF8;

  /* Bright backgrounds — deep space purple/blue, not black */
  --bg-space: #0F0A2E;
  --bg-nebula: #150D3A;
  --bg-panel: rgba(255, 255, 255, 0.04);
  --bg-glass: rgba(255, 255, 255, 0.07);
  --bg-glass-strong: rgba(255, 255, 255, 0.12);
  --bg-card: rgba(255, 255, 255, 0.06);

  /* Text */
  --text-bright: #F8FAFC;
  --text-mid: #CBD5E1;
  --text-muted: #94A3B8;

  /* Borders */
  --border-glow: rgba(255, 255, 255, 0.12);
  --border-bright: rgba(255, 255, 255, 0.2);

  /* Type */
  --font-display: 'Orbitron', 'Exo 2', sans-serif;
  --font-body: 'Exo 2', 'Segoe UI', sans-serif;
  --font-mono: 'Press Start 2P', monospace;
}

/* (full file — 833 lines — see static/css/main.css in the repo) */
```

The file is long; the full content is on disk at `themes/sambar-on-a-spaceship/static/css/main.css`. Sections it contains:
reset/base, background gradients + stars, keyframe animations (`float`, `pulse`, `glow-rotate`, `shimmer`, `blink-slow`, `blink-fast`, `gauge-pulse`, `border-rainbow`, `gradient-shift`, `scan-bright`, `text-glow`), `.scanlines`, `.cockpit-header`, `.instrument-bar`, `.gauge` + `.gauge-meter` + `.fuel-fill` / `.temp-fill`, `.status-lights` + `.light-*`, `.logo-bay` + `.logo-glow` + `.logo-img`, `.ship-controls` + `.control-panel` + `.control-btn` (+ `.active`), `.readout*`, `.viewport` (h2, ul, li a), single post `article` styles, `.hull-plate` footer + `.hull-lights`, `.comic-page` + `.comic-header` + `.comic-title` + `.comic-meta` + `.comic-frame` + `.frame-corner` + `.comic-art` + `.comic-body` + `.comic-nav` + `.nav-btn`, and responsive breakpoints at 700px and 400px.

## `themes/sambar-on-a-spaceship/static/css/style.css`

Stored on disk as RTF; the actual CSS it contains is:

```css
:root {
    /* South Indian Cyberpunk Palette */
    --neon-banana: #39FF14;
    --cyber-turmeric: #FFEA00;
    --plasma-pink: #FF00FF;
    --idli-white: #F4F4F5;
    --space-black: #09090B;
    --filter-kaapi: #5C4033;
    --hologram-cyan: #00FFFF;

    /* Ligne Claire Rules */
    --line-thick: 4px solid var(--space-black);
    --line-thin: 2px solid var(--space-black);
    --flat-shadow: 8px 8px 0px var(--space-black);
    --flat-shadow-hover: 12px 12px 0px var(--space-black);
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    background-color: var(--plasma-pink);
    /* A repeating neon kolam/grid pattern */
    background-image: linear-gradient(var(--space-black) 2px, transparent 2px),
                      linear-gradient(90deg, var(--space-black) 2px, transparent 2px);
    background-size: 40px 40px;
    font-family: 'Courier New', Courier, monospace;
    color: var(--space-black);
    line-height: 1.6;
    padding: 20px;
}

.layout-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    max-width: 1200px;
    margin: 0 auto;
}

/* --- HEADER & MAXIMALIST NAV --- */
header {
    background-color: var(--cyber-turmeric);
    border: var(--line-thick);
    box-shadow: var(--flat-shadow);
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    transform: rotate(-1deg);
}

.site-title {
    font-size: 3rem;
    font-weight: 900;
    text-transform: uppercase;
    background: var(--hologram-cyan);
    padding: 10px 20px;
    border: var(--line-thick);
    display: inline-block;
}

nav a {
    background: var(--neon-banana);
    color: var(--space-black);
    text-decoration: none;
    font-weight: bold;
    font-size: 1.2rem;
    padding: 10px 15px;
    border: var(--line-thick);
    box-shadow: 4px 4px 0px var(--space-black);
    transition: all 0.2s;
    text-transform: uppercase;
}

nav a:hover {
    transform: translate(-4px, -4px);
    box-shadow: var(--flat-shadow-hover);
    background: var(--plasma-pink);
}

/* --- MAIN CONTENT AREAS --- */
main {
    background-color: var(--idli-white);
    border: var(--line-thick);
    box-shadow: var(--flat-shadow);
    padding: 40px;
    margin-top: 20px;
}

/* --- STORY POSTS (Tiffin Carrier aesthetic) --- */
.story-card {
    background: var(--neon-banana);
    border: var(--line-thick);
    box-shadow: var(--flat-shadow);
    margin-bottom: 30px;
    padding: 20px;
    position: relative;
    transition: all 0.2s;
}

.story-card:hover {
    background: var(--hologram-cyan);
    transform: translate(-4px, -4px);
    box-shadow: var(--flat-shadow-hover);
}

.story-card h2 {
    font-size: 2rem;
    background: var(--idli-white);
    display: inline-block;
    padding: 5px 15px;
    border: var(--line-thick);
    margin-top: -40px;
}

/* --- SVG ANIMATION STAGE --- */
.svg-stage {
    background-color: var(--space-black);
    border: var(--line-thick);
    padding: 20px;
    margin: 30px 0;
    position: relative;
    overflow: hidden;
}

.svg-stage::before {
    content: "REC> [NEON-MADURAI-SECTOR-4]";
    position: absolute;
    top: 5px;
    left: 10px;
    color: var(--neon-banana);
    font-weight: bold;
    font-size: 0.8rem;
}

.svg-stage::after {
    content: "";
    position: absolute;
    bottom: 5px;
    right: 10px;
    width: 20px;
    height: 20px;
    background-color: red;
    border: 2px solid white;
    border-radius: 50%;
    animation: blink 1s infinite;
}

@keyframes blink { 0% { opacity: 1; } 50% { opacity: 0; } 100% { opacity: 1; } }

/* --- TYPOGRAPHY WITHIN POSTS --- */
.content-body p {
    font-size: 1.2rem;
    font-weight: bold;
    margin-bottom: 20px;
}

/* --- FOOTER --- */
footer {
    background-color: var(--filter-kaapi);
    color: var(--idli-white);
    border: var(--line-thick);
    padding: 20px;
    text-align: center;
    margin-top: 40px;
    font-weight: bold;
}
```

---

## Heads-up for the LLM you share this with

- `baseof.html` is the active base template and loads `main.css`. `baseof_old.html` and `style.css` belong to a previous design ("South Indian Cyberpunk") that the partials + `list.html` + `single.html` still reference (they use CSS variables like `--cyber-turmeric`, `--plasma-pink` that only exist in `style.css`). So rendered pages right now mix the new cockpit chrome from `baseof.html` with class hooks (`story-card`, `svg-stage`, etc.) that are unstyled under `main.css`.
- Several template files and `style.css` are saved as macOS TextEdit Cocoa-HTML / RTF exports rather than plain text. Hugo will still read them, but the rendered output will include `<!DOCTYPE ...Cocoa...>` and `<p class="p1">` wrappers around the escaped template source — this is almost certainly a bug. They should be re-saved as plain text using the de-escaped content shown above.
- `public/` is Hugo's build artifact and shouldn't need to be shared.
