# Guidestone Property — Design System Reference
## SHARED CONTRACT: Every phase agent MUST read this file before writing any code.

---

## PROJECT CONTEXT

**Company:** Guidestone Property — premium buyer's agency serving property investors and home buyers across Australia.
**Domain:** guidestoneproperty.com.au
**Tone:** Premium, trustworthy, calm. High-end financial advisory meets modern real estate.
**Target Audience:** Property investors and home buyers in Australia.

---

## FILE ARCHITECTURE

Each phase agent writes its section into a **standalone partial HTML file** at:
```
sections/section-{phase-number}-{name}.html
```

Each partial contains ONLY:
1. One or more `<section id="...">` blocks with all content markup
2. A `<style>` block at the top with ALL CSS for that section (scoped with section ID prefix)
3. A `<script>` block at the bottom with section-specific JS (scoped to that section)

**DO NOT** include `<html>`, `<head>`, `<body>`, `<!DOCTYPE>`, or CDN links. Those live in the scaffold only.

### Example partial structure:
```html
<style>
  #services .services-card { ... }
  #services .services-grid { ... }
</style>

<section id="services" class="section">
  <!-- section content -->
</section>

<script>
(function() {
  // section-specific JS, self-contained IIFE
})();
</script>
```

---

## CSS CUSTOM PROPERTIES (defined in scaffold, use everywhere)

```css
:root {
  /* Colors */
  --color-primary-dark: #1a2332;
  --color-primary-accent: #c8a45c;
  --color-secondary: #2c3e50;
  --color-bg-light: #f8f6f1;
  --color-white: #ffffff;
  --color-muted: #6b7b8d;
  --color-success: #2ecc71;
  --color-footer-dark: #111a25;
  --color-card-dark: #1e2d3f;

  /* Typography */
  --font-heading: 'Playfair Display', Georgia, serif;
  --font-body: 'Inter', -apple-system, sans-serif;

  /* Spacing */
  --section-padding: 100px;
  --section-padding-mobile: 60px;
  --content-max-width: 1200px;
  --content-padding: 0 24px;

  /* Transitions */
  --transition-default: 0.3s ease;
  --transition-smooth: 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94);

  /* Shadows */
  --shadow-card: 0 4px 20px rgba(0,0,0,0.06);
  --shadow-card-hover: 0 12px 40px rgba(0,0,0,0.12);
  --shadow-nav: 0 2px 20px rgba(0,0,0,0.15);
}
```

---

## SHARED CSS CLASSES (defined in scaffold, reuse in partials)

```css
/* Layout */
.section           → padding: var(--section-padding) 0;
.container         → max-width: var(--content-max-width); margin: 0 auto; padding: var(--content-padding);

/* Typography */
.overline          → font-family: var(--font-body); text-transform: uppercase; letter-spacing: 3px; font-size: 12px; color: var(--color-primary-accent); margin-bottom: 16px;
.section-heading   → font-family: var(--font-heading); color: var(--color-primary-dark); font-size: 42px; line-height: 1.2; margin-bottom: 20px;
.section-subtext   → font-family: var(--font-body); color: var(--color-muted); font-size: 17px; line-height: 1.7; max-width: 650px;
.text-center       → text-align: center; (also centers .section-subtext and .overline within)

/* Buttons */
.btn-primary       → background: var(--color-primary-accent); color: var(--color-primary-dark); font-family: var(--font-body); font-weight: 600; font-size: 15px; padding: 16px 36px; border-radius: 50px; border: none; cursor: pointer; transition: var(--transition-default);
.btn-primary:hover  → transform: translateY(-2px); box-shadow: 0 8px 25px rgba(200,164,92,0.35);
.btn-secondary     → background: transparent; color: white; border: 2px solid rgba(255,255,255,0.5); padding: 16px 36px; border-radius: 50px; font-family: var(--font-body); font-weight: 500; font-size: 15px; cursor: pointer; transition: var(--transition-default);
.btn-secondary:hover → border-color: white; background: rgba(255,255,255,0.1);

/* Animations */
.fade-in-up        → opacity: 0; transform: translateY(30px); transition: opacity 0.8s var(--transition-smooth), transform 0.8s var(--transition-smooth);
.fade-in-up.visible → opacity: 1; transform: translateY(0);
```

---

## SHARED JS UTILITIES (defined in scaffold, available globally)

```js
// Scroll-triggered fade-in observer — use by adding class "fade-in-up" to elements
// The scaffold registers a global IntersectionObserver that adds class "visible"
// Stagger: add data-delay="150" (ms) for staggered children

// Counter utility — use by adding class "count-up" and data-target="100"
// The scaffold provides window.animateCounters() triggered by IntersectionObserver
```

**To use in your section:** Simply add `class="fade-in-up"` to any element you want animated on scroll. The scaffold handles the rest. For staggered children, add `data-delay="0"`, `data-delay="150"`, `data-delay="300"` etc.

---

## TYPOGRAPHY RULES

| Element | Font | Size (desktop) | Size (mobile) | Weight | Color |
|---------|------|----------------|---------------|--------|-------|
| H1 (hero only) | Playfair Display | 56px | 36px | 700 | white |
| H2 (section headings) | Playfair Display | 42px | 32px | 700 | var(--color-primary-dark) |
| H3 (card titles) | Inter | 20px | 18px | 600 | var(--color-primary-dark) |
| Body | Inter | 16px | 15px | 400 | var(--color-secondary) |
| Overline | Inter | 12px | 11px | 600 | var(--color-primary-accent) |
| Small/meta | Inter | 14px | 13px | 400 | var(--color-muted) |

---

## SECTION ORDER & IDs (for nav linking)

| Order | Section ID | Phase File | Background |
|-------|-----------|------------|------------|
| 1 | `#hero` | phase-02 | Dark (image overlay) |
| 2 | `#stats` | phase-02 | `--color-primary-dark` |
| 3 | `#why-us` | phase-03 | `--color-white` |
| 4 | `#services` | phase-03 | `--color-bg-light` |
| 5 | `#method` | phase-04 | `--color-primary-dark` |
| 6 | `#coverage` | phase-05 | `--color-white` |
| 7 | `#founder` | phase-05 | `--color-bg-light` |
| 8 | `#values` | phase-06 | `--color-primary-dark` |
| 9 | `#testimonials` | phase-06 | `--color-white` |
| 10 | `#contact` | phase-07 | `--color-bg-light` |
| 11 | `#cta` | phase-08 | Dark (image overlay) |
| 12 | `#footer` | phase-08 | `--color-footer-dark` |

**IMPORTANT:** Background colors alternate light/dark to create visual rhythm. Do not deviate from this table.

---

## IMAGE URLS (real Unsplash URLs — use directly)

- **Hero background:** `https://images.unsplash.com/photo-1514395462725-fb4566210144?w=1920&q=80`
- **Why Us property image:** `https://images.unsplash.com/photo-1560518883-ce09059eeffa?w=800&q=80`
- **Founder portrait:** `https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?w=600&q=80`
- **CTA background:** `https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=1920&q=80`
- **Contact section background:** `https://images.unsplash.com/photo-1497366216548-37526070297c?w=1920&q=80`

All images: `loading="lazy"` and `decoding="async"` (except hero which loads eagerly).

---

## RESPONSIVE BREAKPOINTS

```css
/* Tablet */
@media (max-width: 1024px) { ... }

/* Mobile */
@media (max-width: 768px) { ... }

/* Small mobile */
@media (max-width: 480px) { ... }
```

Every section partial MUST include its own responsive overrides inside its scoped `<style>` block.

---

## CONSISTENCY RULES FOR PARALLEL AGENTS

1. **ALWAYS prefix CSS selectors** with the section ID: `#services .card` not `.card`
2. **ALWAYS wrap JS** in an IIFE: `(function(){ ... })();`
3. **NEVER redefine** CSS custom properties or shared classes
4. **USE the shared classes** (`.overline`, `.section-heading`, `.section-subtext`, `.container`, `.btn-primary`, `.fade-in-up`) — do not recreate them
5. **DO NOT add** Google Fonts or Font Awesome `<link>` tags — the scaffold handles this
6. **All Font Awesome icons** use the `<i class="fas fa-icon-name"></i>` pattern (Font Awesome 6 solid)
7. **Heading hierarchy:** Only ONE `<h1>` exists (in hero). All section headings are `<h2>`. Sub-items use `<h3>`.
8. **Gold accent lines:** Use `border` or `::after` pseudo-element, 2px solid var(--color-primary-accent)
9. **Card patterns:** Always 16px border-radius, var(--shadow-card) default, var(--shadow-card-hover) on hover
10. **Link/CTA color:** Gold text links use `color: var(--color-primary-accent)` with underline on hover
