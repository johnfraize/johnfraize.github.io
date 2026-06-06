# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static personal/booking website for John Fraize (musician) served by GitHub Pages at `johnfraize.github.io`. There is **no build system, no dependencies, no tests, and no tooling** — every page is a self-contained `.html` file with inline `<style>` and inline `<script>`.

## Development & deploy

- To preview, open any `.html` directly in a browser, or run a static server from the repo root: `python3 -m http.server` then visit `http://localhost:8000`.
- Deployment is automatic: push to `main` and GitHub Pages serves it. There is no CI step.

## Architecture & conventions

- **Pages:** `index.html` (home), `rates.html`, `repertoire.html`, `performances.html` are the four nav-linked pages. `poster.html` is a standalone printable/shareable poster, not in the nav.
- **Shared design system is duplicated, not imported.** Each page repeats the same CSS block inline: `JF-8.jpg` fixed cover background, dark overlay via `body::before`, fixed `.top-tabs` nav, `Cormorant Garamond` (Google Fonts) headings, frosted `section` cards. When changing the look, the edit must be applied to **every** page — there is no shared stylesheet.
- **Navigation is hand-maintained in each file.** The `<nav class="top-tabs">` block is copied into every page; the current page gets `class="active"` on its own link. Adding/renaming a page means editing the nav in all pages.
- **Contact details are hard-coded throughout:** phone `508 868 4846` (as `sms:5088684846` links) and `mailto:johnfraize@gmail.com`. They appear on multiple pages — update all occurrences together.

## Repertoire data (gotcha)

`repertoire.html` renders a song table from CSV at runtime via inline JS. There are **two** copies of the data:
- The inline `<script type="text/csv" id="repertoire-csv">` block inside `repertoire.html` — **this is what actually renders.**
- The standalone `repertoire.csv` file — only used as a `fetch()` fallback if the inline block is empty.

To edit the song list, change the inline `<script type="text/csv">` block in `repertoire.html`. Keep `repertoire.csv` in sync if you want the fallback accurate. The parser handles quoted fields (use quotes around songs containing commas).

## Resume

`resume/` holds the same résumé in three formats: `john_fraize_resume.md` (source), `.html`, and `.pdf`. Edit the Markdown as the source of truth, then regenerate/update the HTML and PDF to match.
