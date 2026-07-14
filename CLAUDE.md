# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is a static single-page marketing/menu website for "Blue Ice", a shisha lounge & bar in Köln (Cologne), Germany. Despite the parent folder name, this is **not** an Android project — it's plain HTML/CSS/JS with no build system, no package manager, and no dependencies.

The entire site is three files:
- `index.html` — all page content and structure (single page, in German)
- `styles.css` — all styling
- `script.js` — minimal vanilla JS for tab switching and mobile nav toggle

## Development

There is no build step, package manager, bundler, or test suite. To work on the site:
- Edit `index.html`, `styles.css`, `script.js` directly.
- Preview by opening `index.html` in a browser, or serve the directory locally, e.g. `python3 -m http.server` from the project root.
- There is no linting or formatting tooling configured; match the existing code style (2-space indentation, minified/compact inline styles kept on single lines for repeated card markup).

## Architecture

Single HTML page with anchor-linked sections, no routing/framework:

- **`#start`** — hero section.
- **`#karte`** ("Karte" = menu) — a tabbed interface. Each tab button calls `showTab(id, btn)` (in `script.js`), which toggles `.visible` on the matching `.menu-section` div and `.active` on the clicked `.tab-btn`. Tabs: Shisha, Softdrinks, Säfte, Cocktails, Longdrinks, Spirituosen, Bier, Kaffee & Tee, Snacks, Info. Each `.menu-section` must have an `id` matching the string passed to `showTab()` in its corresponding `onclick`.
- **`#ambiente`** — static descriptive/marketing content.
- **`#standort`** — location, opening hours, contact, and an embedded Google Maps iframe.

Menu items follow a consistent repeated markup pattern — `.drink-card` (name + optional `.drink-desc` + price + optional `.drink-vol`) inside a `.drink-list`, grouped under `.subcat` subheadings. Shisha items use a visually distinct `.shisha-card` pattern instead. When adding/editing menu items, follow the existing markup pattern exactly (including the price formatting `X,XX €` with a German comma decimal).

All navigation (`.nav-links`) uses in-page anchor links (`#start`, `#karte`, `#ambiente`, `#standort`) with `toggleNav()`/`closeNav()` in `script.js` controlling the mobile slide-out menu.

Styling is driven by CSS custom properties defined in `:root` in `styles.css` (colors, fonts) — reuse these variables (`--gold`, `--blue`, `--cream`, `--bg`, `--fd`/`--fb` fonts, etc.) rather than hardcoding new values.
