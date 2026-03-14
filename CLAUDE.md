# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Guidestone Property is a single-page marketing website for an Australian buyer's agency. The entire site lives in one file: `index.html` (~1700+ lines).

## Architecture

**Single-file site** — all CSS, HTML, and JS are in `index.html`:
- `<style>` block: CSS reset, custom properties, all section styles, responsive breakpoints
- `<body>`: Semantic HTML sections in order (#navbar, #hero, #brand-story, #stats, #why-us, #services, #pathway, #method, #coverage, #founder, #values, #contact, #cta, #footer)
- `<script>` blocks: Intersection Observer animations, navbar scroll behavior, mobile menu, stat counter, form handling

**No build tools, no bundler, no framework.** Just open `index.html` in a browser.

## Design System

- **Colors:** Navy `#1a2332`, Gold `#c8a45c`, Slate `#2c3e50`, Off-white `#f8f6f1`, defined as CSS custom properties on `:root`
- **Fonts:** Playfair Display (headings via `--font-heading`), Inter (body via `--font-body`) — loaded from Google Fonts
- **Icons:** Font Awesome 6.5.1 via CDN
- **Shared CSS classes:** `.section`, `.container`, `.overline`, `.section-heading`, `.section-subtext`, `.text-center`, `.btn-primary`, `.btn-secondary`, `.fade-in-up`

## Key Files

- `index.html` — the live site
- `index-backup.html` — pre-v2 backup of the original site
- `prompts/website-changes-v2.md` — detailed spec for the v2 redesign (agent-based parallel execution plan)

## Development

To preview, open `index.html` in a browser or use any local HTTP server:
```
python3 -m http.server 8000
```

## Editing Conventions

- When editing sections, locate by `id` attribute (e.g., `#method`, `#coverage`)
- CSS for each section is grouped under comment headers like `/* SECTION 02 — Navigation + Hero + Stats */`
- Responsive rules are at the end of each section's CSS block and also in global `@media` queries
- Animations use `.fade-in-up` class + Intersection Observer JS — new sections should include this class for consistency
- Contact details (email, phone, WhatsApp) appear in both `#contact` and `#footer` — keep them in sync
