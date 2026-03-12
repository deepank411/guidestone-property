# Phase 05: Where We Buy + Founder Story

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-05-coverage.html`.

## OBJECTIVE
Build the Australia coverage map section and the founder biography section.

---

## OUTPUT FILE: `sections/section-05-coverage.html`

---

## 5A — Where We Buy

### Structure
```html
<section id="coverage" class="section">
```

### Specs
- **Background:** var(--color-white)
- **Header:** centered

### Header
1. **Overline:** "OUR REACH" — `.overline`, centered
2. **H2:** "We Buy Across Australia" — `.section-heading`, centered
3. **Subtext:** "From Melbourne to Perth, our team covers major property markets across six states and territories." — `.section-subtext`, centered, margin: 0 auto 60px auto

### Layout — State Cards Grid
Use a clean 3×2 grid of state cards (this is more reliable and polished than an SVG map):

- CSS Grid: `grid-template-columns: repeat(3, 1fr)` desktop, `repeat(2, 1fr)` tablet, `1fr` mobile
- Gap: 24px
- Max-width: 900px, centered

### Each State Card
- Background: var(--color-bg-light)
- border-radius: 16px
- padding: 32px 24px
- text-align: center
- transition: var(--transition-default)
- **Hover:** transform: translateY(-4px), box-shadow: var(--shadow-card), border-bottom: 3px solid var(--color-primary-accent)

### Card Content
1. **Icon:** `<i class="fas fa-map-marker-alt">` — var(--color-primary-accent), 28px, margin-bottom 12px
   - Add a subtle pulsing dot animation behind the icon (CSS keyframe, gold circle at 20% opacity expanding)
2. **State abbreviation:** Playfair Display, 24px, 700, var(--color-primary-dark), margin-bottom 4px
3. **Key cities/regions:** Inter, 14px, var(--color-muted)

### The 6 States
| Abbrev | Full Name | Cities |
|--------|-----------|--------|
| VIC | Victoria | Melbourne, Geelong, Regional VIC |
| NSW | New South Wales | Sydney, Newcastle, Wollongong |
| QLD | Queensland | Brisbane, Gold Coast, Sunshine Coast |
| SA | South Australia | Adelaide, Regional SA |
| WA | Western Australia | Perth, Fremantle |
| NT | Northern Territory | Darwin, Alice Springs |

- Apply `.fade-in-up` with staggered delays on each card

---

## 5B — Founder Story

### Structure
```html
<section id="founder" class="section">
```

### Specs
- **Background:** var(--color-bg-light)
- **Layout:** Two columns, flex or grid
  - Left: 40% — portrait image
  - Right: 60% — biography content
  - Gap: 60px
  - Vertically centered

### Left Column — Portrait
- Image: `https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?w=600&q=80`
- `alt="Sonal, Founder of Guidestone Property"`
- border-radius: 12px
- box-shadow: 0 20px 60px rgba(0,0,0,0.1)
- **Decorative L-shape accent:** Use `::after` pseudo-element on the image wrapper
  - Position: absolute, bottom: -12px, left: -12px
  - Width: 80px, height: 80px
  - border-left: 4px solid var(--color-primary-accent)
  - border-bottom: 4px solid var(--color-primary-accent)
  - border-radius: 0 0 0 12px
  - z-index: -1 (behind image) — but wrapper needs `position: relative`
- `.fade-in-up` on wrapper

### Right Column — Content
1. **Overline:** "MEET THE FOUNDER" — `.overline`
2. **H2:** "Sonal — Founder, Guidestone Property" — `.section-heading`, font-size: 36px
3. **Pull quote block:**
   - Large gold quotation mark: `<i class="fas fa-quote-left">` — var(--color-primary-accent), 36px, opacity 0.5, margin-bottom 8px
   - Quote text: "Property has always been more than just an investment to me — it's a powerful tool to create freedom, security, and long-term wealth." — Playfair Display, 20px, italic, var(--color-primary-dark), line-height 1.5
   - Left border: 3px solid var(--color-primary-accent), padding-left 24px
   - Margin-bottom: 28px
4. **Paragraph 1:** "My journey into property began as an investor, driven by the belief that property can build long-term wealth and financial freedom. I stepped into the market myself, building a portfolio through buy-and-hold, renovations, subdivisions, and cash flow investing."
5. **Paragraph 2:** "Over three years in real estate, I've helped many clients secure investment properties aligned with their long-term goals — many returning to build further on their portfolios. This experience inspired Guidestone Property: a buyers agency dedicated to guiding clients toward smarter property decisions with clarity, confidence, and a strategy-first approach."
   - Both paragraphs: Inter, 16px, var(--color-secondary), line-height 1.7, margin-bottom 20px
6. **Signature:** "— Sonal" — Playfair Display, 18px, italic, var(--color-primary-dark), with a 40px gold underline (use `::after` pseudo-element, 2px height, gold)

### Mobile (< 768px)
- Stack vertically: image first (max-height 350px, object-fit cover, full width), content below
- Remove L-shape accent on mobile
- Pull quote font-size: 18px
