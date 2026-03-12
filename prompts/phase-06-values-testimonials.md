# Phase 06: Core Values + Testimonials

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-06-values.html`.

## OBJECTIVE
Build the core values strip and the testimonials carousel.

---

## OUTPUT FILE: `sections/section-06-values.html`

---

## 6A — Core Values Strip

### Structure
```html
<section id="values" class="section">
```

### Specs
- **Background:** var(--color-primary-dark)
- **Padding:** 80px 0 (slightly less than standard)
- **Header:** centered

### Header
1. **Overline:** "OUR VALUES" — `.overline`, centered
2. **H2:** "What We Stand For" — `.section-heading`, color: white, centered

### Values Layout
- Flex row, justify-content: center, flex-wrap: wrap, gap: 0
- 5 values in a single row on desktop, each separated by gold vertical dividers
- Each value card: flex-basis ~20%, padding: 30px 28px, text-align: center

### Each Value Card
1. **Icon:** Font Awesome, var(--color-primary-accent), 28px, margin-bottom 16px
2. **Title:** Inter, 16px, 600, white, margin-bottom 8px
3. **Description:** Inter, 14px, rgba(255,255,255,0.6), line-height 1.5

### Dividers
- Between each value: `border-right: 1px solid rgba(200,164,92,0.2)` on cards 1–4
- Last card has no right border

### The 5 Values
| # | Icon | Title | Description |
|---|------|-------|-------------|
| 1 | `fa-shield-halved` | Integrity First | Every recommendation backed by honesty and transparency. |
| 2 | `fa-database` | Research-Led | Data drives every step of your property journey. |
| 3 | `fa-user-check` | Client-First | Your goals guide our strategy. |
| 4 | `fa-spa` | Calm & Guided | Reducing stress, increasing clarity. |
| 5 | `fa-seedling` | Wealth Focused | Your future success is our priority. |

### Mobile (< 768px)
- Horizontal scroll: `overflow-x: auto; flex-wrap: nowrap;` on the container
- Each card: `min-width: 200px; flex-shrink: 0;`
- Hide scrollbar: `-webkit-overflow-scrolling: touch; scrollbar-width: none;`
- Add subtle scroll hint: fade gradient on right edge using `::after` on the container

---

## 6B — Testimonials Section

### Structure
```html
<section id="testimonials" class="section">
```

### Specs
- **Background:** var(--color-white)
- **Header:** centered

### Header
1. **Overline:** "CLIENT STORIES" — `.overline`, centered
2. **H2:** "Trusted by Property Buyers Across Australia" — `.section-heading`, centered

### Carousel Container
- `overflow: hidden`, max-width 800px, margin: 0 auto
- Inner track: `display: flex; transition: transform 0.5s ease;`
- Each slide: `min-width: 100%; flex-shrink: 0;`

### Each Testimonial Slide
- text-align: center
- padding: 40px 20px
1. **Gold quote icon:** `<i class="fas fa-quote-left">` — var(--color-primary-accent), 40px, opacity 0.4, margin-bottom 20px
2. **Stars:** 5× `<i class="fas fa-star">` — var(--color-primary-accent), 16px, flex row centered, gap 4px, margin-bottom 24px
3. **Quote text:** Playfair Display, 22px desktop / 18px mobile, italic, var(--color-secondary), line-height 1.6, max-width 600px, margin: 0 auto 28px
4. **Client name:** Inter, 16px, 600, var(--color-primary-dark)
5. **Client type:** Inter, 14px, var(--color-muted)

### The 3 Testimonials
1. Quote: "Guidestone made the entire process stress-free. Their research was thorough and we secured a property well below our budget."
   Name: "Priya & Raj" | Type: "First Home Buyers, Melbourne"
2. Quote: "As an interstate investor, I needed someone I could trust on the ground. Guidestone delivered beyond expectations."
   Name: "James T." | Type: "Property Investor, Sydney"
3. Quote: "The Guidestone Method gave us complete confidence. From strategy call to settlement, every step was handled professionally."
   Name: "Sarah & Mark" | Type: "Upgraders, Brisbane"

### Navigation
- **Dots:** 3 small circles below the carousel, 10px diameter, centered, gap 8px
  - Active: var(--color-primary-accent), opacity 1
  - Inactive: var(--color-muted), opacity 0.3
  - Cursor pointer, transition var(--transition-default)
- **Arrows (desktop only):** Left/right chevron buttons positioned absolute, vertically centered on the carousel
  - 44px circles, border: 1px solid var(--color-muted) at 30%, transparent bg
  - Icon: `fa-chevron-left` / `fa-chevron-right`, var(--color-muted)
  - Hover: border-color: var(--color-primary-accent), icon color: var(--color-primary-accent)
  - Hide on mobile

### JS (inside IIFE)
- Track current slide index
- `goToSlide(index)`: set transform: `translateX(-${index * 100}%)`
- Update active dot
- Auto-rotate every 5 seconds (clearInterval on manual interaction, restart after 10s idle)
- Arrow click handlers
- Dot click handlers
- Touch swipe support (track touchstart/touchend X, if delta > 50px, advance/retreat)
