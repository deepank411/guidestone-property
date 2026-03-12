# Phase 02: Navigation + Hero + Stats Bar

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-02-hero.html`.

## OBJECTIVE
Build the sticky navigation, full-viewport hero section, and social proof stats bar.

---

## OUTPUT FILE: `sections/section-02-hero.html`

---

## 2A — Sticky Navigation Bar

### Structure
```html
<header id="navbar" class="navbar">
```

### Specs
- **Position:** Fixed top, full width, z-index: 1000
- **Default state:** `background: transparent;` — sits over the hero image
- **Scrolled state (after 50px scroll):** `background: rgba(26, 35, 50, 0.97); backdrop-filter: blur(10px); box-shadow: var(--shadow-nav);` — Add class `.scrolled` via JS
- **Height:** 80px, vertically centered contents
- **Inner container:** max-width: var(--content-max-width), centered, flex, space-between, align-center

### Left — Logo
- Text-based logo: `<a>` tag
- "GUIDESTONE" in Playfair Display, 22px, bold, white, letter-spacing: 2px
- Gold diamond separator: `<span style="color: var(--color-primary-accent); margin: 0 6px;">◆</span>`
- "PROPERTY" in Playfair Display, 22px, font-weight 400, white, letter-spacing: 2px
- No text-decoration, hover: gold color on full text

### Center — Nav Links
- `<nav>` with `<ul>` containing links:
  - Services → `#services`
  - Our Method → `#method`
  - About → `#founder`
  - Where We Buy → `#coverage`
  - Contact → `#contact`
- Style: Inter, 13px, uppercase, letter-spacing: 1.5px, font-weight: 500, white, no underline
- Hover: color transitions to var(--color-primary-accent)
- Active link detection: JS adds `.active` class based on scroll position (optional, but nice)

### Right — CTA Button
- "Book a Strategy Call"
- Use `.btn-primary` styles but smaller: padding 12px 28px, font-size 13px
- Hover glow: `box-shadow: 0 0 20px rgba(200,164,92,0.4)`

### Mobile (< 768px)
- Hide nav links and CTA button
- Show hamburger icon (three gold lines, `<div>` based, animated to X on open)
- On tap: full-screen overlay, `background: var(--color-primary-dark)`, centered nav links (24px each), gold CTA button at bottom
- Overlay slides in from right with CSS transform transition

### JS for Nav (inside IIFE in script block)
- Scroll listener: add `.scrolled` class to `#navbar` when `window.scrollY > 50`
- Mobile toggle: toggle `.nav-open` class on body and hamburger
- Smooth scroll: click listeners on all nav links

---

## 2B — Hero Section

### Structure
```html
<section id="hero" class="hero-section">
```

### Specs
- **Height:** 100vh, min-height: 700px
- **Background:** `url('https://images.unsplash.com/photo-1514395462725-fb4566210144?w=1920&q=80')` — center/cover, no-repeat
- **Overlay:** `::before` pseudo-element, `linear-gradient(135deg, rgba(26,35,50,0.85) 0%, rgba(26,35,50,0.6) 100%)`
- **Ken Burns effect:** CSS animation on the background container — `scale(1)` → `scale(1.08)` over 20s, infinite alternate, ease-in-out
- **Content wrapper:** flex, column, center center, max-width 800px, centered, padding-top 80px (for nav clearance)

### Content (top to bottom)
1. **Overline:** "AUSTRALIA'S TRUSTED BUYER'S AGENCY" — use `.overline` class, white override (opacity 0.9)
2. **H1:** "Guiding You to Smarter Property Decisions" — Playfair Display, 56px desktop / 36px mobile, white, line-height 1.2, margin-bottom 24px
3. **Subtext:** "We are more than a buyers agency — we are your strategic partner, dedicated to helping you navigate the property market with confidence and achieve long-term wealth." — Inter, 18px desktop / 16px mobile, rgba(255,255,255,0.8), max-width 600px, line-height 1.7
4. **Button group:** flex row, gap 16px, margin-top 36px, wrap on mobile
   - Primary: "Book a Free Strategy Call" — `.btn-primary`, padding 18px 40px
   - Secondary: "See How We Work" — `.btn-secondary`, href="#method"
5. **Trust line:** "Trusted by 100+ clients across VIC, NSW, QLD, SA, WA & NT" — 14px, white at 60%, margin-top 32px, with `<i class="fas fa-map-marker-alt">` icon in gold before text

### Scroll indicator (bottom center)
- Bouncing chevron-down: `<i class="fas fa-chevron-down">`
- Position absolute, bottom 30px, centered
- CSS animation: translateY(0) → translateY(10px) every 1.5s, infinite
- Fades out on scroll (JS: opacity 0 when scrollY > 100)

### Page load animation
- Hero content starts with `opacity: 0; transform: translateY(30px);`
- On DOM ready, after 300ms delay, animate to `opacity: 1; transform: translateY(0);` over 1s

---

## 2C — Social Proof Stats Bar

### Structure
```html
<section id="stats" class="stats-bar">
```

### Specs
- **Background:** var(--color-primary-dark)
- **Padding:** 50px 0
- **Top & bottom border:** 2px solid var(--color-primary-accent)
- **Layout:** flex, justify-content: space-around, align-items: center, max-width container

### 4 Stats (with gold vertical dividers between)
Each stat is a flex column, centered:
- Number: 48px, Playfair Display, bold, white, class `count-up`, with `data-target` and `data-suffix`
  1. `data-target="100"` `data-suffix="+"` → "100+"  label: "Properties Secured"
  2. `data-target="6"` `data-suffix=""` → "6"  label: "States Covered"
  3. `data-target="98"` `data-suffix="%"` → "98%"  label: "Client Satisfaction"
  4. `data-target="3"` `data-suffix="+"` → "3+"  label: "Years Experience"
- Label: 13px, Inter, uppercase, letter-spacing: 2px, rgba(255,255,255,0.6), margin-top 8px
- Dividers: `border-right: 1px solid rgba(200,164,92,0.3)` on first three stats

### Mobile
- 2x2 grid instead of 4-column row
- Remove gold dividers
- Reduce number size to 36px
