# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing site for Vivat (`vivatai.org`), an AI assistant platform for institutions with a network of branded locations. Positioning made fully generic 2026-09-09, no origin-network references in copy (see `vivat-bot/VIVAT.md`). No backend, no build step, no framework — plain HTML/CSS/JS served directly by GitHub Pages.

## Commands

- **Deploy:** `git push` to `main` — GitHub Pages serves the repo root directly, live in ~60s. No CI, no build pipeline.
- **Preview locally:** open any `.html` file directly in a browser, or `python3 -m http.server` from the repo root for relative-path/CNAME-accurate testing.
- No package manager, linter, or test suite in this repo.

## Architecture

- Four standalone pages, each fully self-contained: `index.html` (landing), `demo.html` (animated explainer), `data.html` (data & privacy summary), `privacy.html` (full policy). There is no shared CSS/JS file — each page duplicates its own `<style>` block and CSS custom properties. Changing a visual token (color, font) means editing all four files individually.
- Shared design tokens: navy/gold palette defined via `oklch()` custom properties (`--navy`, `--gold`, `--cream`, etc.), Fraunces (headings) + Inter (body) loaded per-page from Google Fonts.
- `demo.html` is the only page with inline JavaScript: a 6-scene animated explainer with a talking avatar built on the browser's native Web Speech API (`speechSynthesis` / `SpeechSynthesisUtterance`) — no external JS libraries or frameworks anywhere in the site.
- Icons: Tabler Icons webfont via jsdelivr CDN, used only on `data.html` and `demo.html`.
- Logo assets: `vivat-mark-real.png` / `vivat-logo-real.png` (+ `-small` variants) are the current in-use marks, sourced from the Keynote pitch deck. The `.svg` logo files (`vivat-logo-horizontal.svg`, `vivat-mark.svg`, etc.) are legacy and no longer referenced by any page.
- Lead capture is `mailto:` links with pre-filled subject/body (pilot request) — there is no form, no backend, no submission endpoint on this repo.
- Custom domain (`vivatai.org`) is wired via the `CNAME` file plus Namecheap DNS pointing at GitHub Pages IPs.
