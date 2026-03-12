# Phase 04: The Guidestone Method (Process Timeline)

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-04-method.html`.

## OBJECTIVE
Build the 9-step Guidestone Method timeline — the premium centrepiece section of the page.

---

## OUTPUT FILE: `sections/section-04-method.html`

---

## Section Specs

### Structure
```html
<section id="method" class="section">
```

### Background & Feel
- **Background:** var(--color-primary-dark) — this is a dark section
- **All text colors:** white or gold
- **Section heading color override:** white (not the default dark)
- This section should feel premium and distinctive — it's the signature process

### Header (centered)
1. **Overline:** "OUR PROCESS" — `.overline` (gold by default, works on dark bg)
2. **H2:** "The Guidestone Method™" — `.section-heading`, color: white, centered
3. **Subtext:** "Our signature process ensures you make informed, confident property decisions every step of the way." — `.section-subtext`, color: rgba(255,255,255,0.7), centered, margin: 0 auto 70px auto

---

## Timeline Layout

### Desktop (> 768px) — Alternating Timeline
- Central vertical line: 2px wide, var(--color-primary-accent), runs the full height of the timeline area, centered horizontally
- The line uses `::before` pseudo-element on the timeline container, positioned absolute center
- **Line draw animation:** The line starts with `scaleY(0)` and transforms to `scaleY(1)` as user scrolls (use IntersectionObserver with progressive thresholds, or a simple scroll listener that calculates progress)
- Cards alternate left and right of the center line
  - Odd steps (1, 3, 5, 7, 9): card on the LEFT, content right-aligned toward center
  - Even steps (2, 4, 6, 8): card on the RIGHT, content left-aligned toward center
- Each step has a **numbered gold circle** (44px diameter) sitting ON the center line
  - Background: var(--color-primary-accent), color: var(--color-primary-dark), font: Inter 600 16px
  - Position: absolute, centered on the timeline
  - Subtle glow animation on viewport entry: `box-shadow: 0 0 0 0 rgba(200,164,92,0.4)` → `0 0 0 12px rgba(200,164,92,0)` — one pulse, 1s

### Mobile (< 768px) — Single Column
- Gold line on the LEFT side (20px from left edge)
- All cards stack vertically on the right of the line
- Numbered circles sit on the left line
- Cards get full width minus line space

### Each Step Card
- Background: var(--color-card-dark) — `#1e2d3f`
- Border: 1px solid rgba(200,164,92,0.15)
- border-radius: 16px
- padding: 30px
- margin-bottom: 24px (vertical gap between cards)
- Max-width: 420px per card (on desktop, each side)
- **Animation:** `.fade-in-up` — odd cards also add a slight `translateX(-30px)` start, even cards `translateX(30px)` start (slide from their respective side)

### Card Inner Content
1. **Icon:** Font Awesome icon, var(--color-primary-accent), 20px, margin-bottom 12px
2. **Step title:** Inter, 18px, 600 weight, white, margin-bottom 8px
3. **Description:** Inter, 15px, rgba(255,255,255,0.7), line-height 1.6

---

## The 9 Steps Data

| Step | Icon | Title | Description |
|------|------|-------|-------------|
| 1 | `fa-phone-alt` | Strategy Call | Personalized consultation to understand your goals, financial position, and property aspirations. |
| 2 | `fa-file-signature` | Retainer Payment | Confirm engagement and secure your dedicated strategy session with our team. |
| 3 | `fa-search-location` | Market Research & Targeting | Comprehensive suburb and property analysis based on your goals — growth potential, rental yield, and lifestyle fit. |
| 4 | `fa-list-check` | Property Shortlisting | Only properties matching your criteria are presented. Saves time and ensures strategic choices. |
| 5 | `fa-balance-scale` | Due Diligence & Negotiation | Review contracts, reports, and valuations. We handle negotiations to secure the right price. |
| 6 | `fa-clipboard-check` | Building & Pest Reports | Professional inspections ordered and interpreted, guiding you through every finding. |
| 7 | `fa-user-tie` | Property Manager Introduction | Trusted property manager recommendations for investors — rental setup and management sorted. |
| 8 | `fa-key` | Secure & Settle | Full support through settlement for a smooth handover and complete peace of mind. |
| 9 | `fa-chart-line` | Post-Purchase Support | Guidance on portfolio growth, refinancing, or further acquisitions. Your long-term wealth partner. |

---

## JS Requirements (inside IIFE)
1. **Timeline line draw:** IntersectionObserver on the timeline container. As the section scrolls into view, animate the center line's `scaleY` from 0 to 1 based on scroll progress through the section. A simple approach: use CSS transition + a `.line-visible` class toggled by observer.
2. **Step circle pulse:** Each numbered circle gets the glow pulse when it enters viewport.
3. **Card slide-in:** Cards use the standard `.fade-in-up` plus a per-card `translateX` offset that resolves to 0 when `.visible` is added.
