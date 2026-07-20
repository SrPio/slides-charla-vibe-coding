# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Working agreement

- **Do not open, screenshot, or exercise the deck in the Browser pane unless the user explicitly asks for it.** Verify HTML/CSS/JS changes by reading the code and reasoning about it (or with quick non-browser checks, e.g. grepping for a class, running a small Node script). Only drive the actual browser (navigate/screenshot/computer tool) when the user says so.
- When something needs installing, use **pnpm** (not npm/yarn/npx).

## What this project is

A single-file, offline HTML slide deck (`slides/vibe-coding-charla.html`) for a conference talk ("Vibe Coding con Google: De la idea al MVP en tiempo récord"), built with the `frontend-slides` skill's Neo-Grid Bold template, then heavily customized (dark/light purple theme, custom illustrations, charts, QR codes). There is no build step, package manager, bundler, or test suite — the deck is one HTML file that opens directly in a browser (`file://...`).

- `Charla.docx` / `Charla.md` — the original talk script (Word doc + its Markdown extraction). This is the source of truth for slide content/wording. `Charla.md` was produced by unzipping the `.docx` and extracting `word/document.xml` text (no `pandoc`/Python available in this environment) — reuse that approach if the script is edited and slides need re-syncing.
- `slides/vibe-coding-charla.html` — the entire presentation: markup, CSS, and JS in one file.
- `slides/imgs/yo.png` — the only external asset (speaker portrait), referenced via a relative path.

## Architecture of `vibe-coding-charla.html`

The file is organized top to bottom as: `<style>` (theme tokens → fixed-stage CSS → grid → panels → typography → chrome → reveal/stagger → icon badges → stat/chart components → flow/timeline components → deck controls) → inline SVG `<symbol>` icon library → the deck markup (`.deck-viewport > .deck-stage > section.slide × 34`) → deck-controls buttons → the `SlidePresentation` JS class. Each CSS block is marked with a `/* === SECTION NAME === */` header comment — use those to navigate instead of line numbers.

**Fixed 1920×1080 stage.** Every slide is authored at a fixed 1920×1080 canvas (`.deck-stage`), scaled as a whole via a JS transform (`setupStageScale`) to fit the viewport — never via responsive reflow. Slide content uses a 12-column × 8-row CSS grid (`.frame`) inset 40px, in the Neo-Grid Bold house style: panels span grid cells (`grid-column`/`grid-row`), and every `font-size` in the file is written as `calc(Npx * var(--text-scale))` so the presenter text-size control (`A−`/`A+` buttons, `-`/`+`/`0` keys) can scale all type uniformly without touching layout.

**Theme system.** `data-theme="dark"|"light"` on `<html>` switches CSS custom properties (`--surface-1`, `--text-1`, etc.), persisted to `localStorage`. Two things are intentionally theme-*independent* because they always sit on the same visual context regardless of toggle: `.panel.ink` (always a dark surface, used as a contrast block in both themes) and chart colors (`--accent`, `--chart-b`, `--chart-track`) — charts live inside `.panel.ink`, so their colors must stay legible against a permanently-dark background rather than flipping with the theme.

**Slide visibility / animation.** Slides are shown/hidden via `.active`/`.visible` classes (never `display`), toggled by `SlidePresentation.showSlide()`. Entrance animations (`.reveal`, `.frame`, `.parallax-orbs`, `.photo-portrait img`, `.radial-fill`, `.bar-fill`, `.qr-tile`) are all gated on `.slide.visible <selector>` and only animate for the currently-active slide. **This means `@media print` must separately force every one of those gated rules to its finished state** (see the print block near the top of `<style>`) — otherwise printing/exporting shows blank content for every slide except whichever was active in the browser. When adding a new animated component, add its finished-state override to the print block too.

**PDF export** is just `window.print()` (button in deck-controls) relying on that print CSS — no library, no server-side rendering.

**Icon library.** All brand/tool icons and the QR codes live as `<symbol id="ic-*">` / `<symbol id="qr-*">` defs in one hidden `<svg>` near the top of `<body>`, referenced elsewhere via `<use href="#id"/>`. Reuse this pattern for any new icon instead of inlining a fresh `<svg>` per usage.

**QR codes are baked in, not generated at runtime.** They were produced once at authoring time with `pnpm add qrcode` + `QRCode.toString(url, {type:'svg'})`, and the resulting static path data was pasted into the icon library as `qr-*` symbols. If a linked URL changes, regenerate that one QR the same way (scratch/temp dir, `pnpm`, `qrcode` package) rather than adding a client-side QR library to the deck.

**Reveal stagger quirk.** `.reveal:nth-of-type(n)` sets stagger delay, and CSS `nth-of-type` counts per **tag name** among siblings, not per class — so a `<div class="reveal">` and an `<a class="reveal">` at the same DOM depth are numbered independently. This is relied upon (not a bug) in a couple of slides; keep it in mind when reordering or changing element tags inside `.frame`.

**Slide count.** Every slide has a `.pagenum` div hardcoded as `NN / 34`. The JS progress counter (`#progressTag`) computes its own total dynamically, but the per-slide `.pagenum` text does not — if a slide is added/removed, update all `.pagenum` strings to match the new total (e.g. `sed -i 's#/ 34</div>#/ 35</div>#g'`).
