# Phase 03: Why Choose Us + Services

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-03-services.html`.

## OBJECTIVE
Build the "Why Choose Guidestone" two-column section and the services card grid.

---

## OUTPUT FILE: `sections/section-03-services.html`

---

## 3A — Why Choose Guidestone Property

### Structure
```html
<section id="why-us" class="section">
```

### Specs
- **Background:** var(--color-white)
- **Layout:** Two columns using CSS grid or flexbox
  - Left column: 55% — content
  - Right column: 45% — image
  - Gap: 60px
  - Vertically centered

### Left Column Content
1. **Overline:** "WHY GUIDESTONE" — use `.overline` class
2. **H2:** "Your Partner in Confident Property Decisions" — use `.section-heading` class
3. **Body:** "Buying property is one of the most significant financial decisions you'll ever make. At Guidestone Property, we remove uncertainty by providing the clarity and strategy you need." — use standard body text styles, margin-bottom 36px
4. **4 Benefit items** — each item is a flex row with:
   - Left: Gold icon in a 44px circle (gold bg at 10% opacity, gold icon)
     - `fa-shield-halved` — Strategic Guidance
     - `fa-chart-line` — Market Expertise
     - `fa-user` — Personalized Support
     - `fa-circle-check` — Stress-Free Experience
   - Right: content block
     - Title: Inter, 16px, 600 weight, var(--color-primary-dark)
     - Description: 14px, var(--color-muted), one line
       - "Clear, actionable insights to make informed choices."
       - "Local knowledge and investment analysis that maximizes results."
       - "Solutions tailored to your goals and lifestyle."
       - "From first viewing to settlement, we manage the details."
   - Left border: 3px solid var(--color-primary-accent) on each item, padding-left 20px
   - Margin-bottom: 20px between items
   - Apply `.fade-in-up` with staggered `data-delay` (0, 150, 300, 450)
5. **CTA link:** "Start Your Property Journey →" — var(--color-primary-accent), Inter 600, 15px, no underline default, underline on hover with transition

### Right Column — Image
- Image: `https://images.unsplash.com/photo-1560518883-ce09059eeffa?w=800&q=80`
- `alt="Modern Australian property exterior"`
- border-radius: 12px
- box-shadow: 0 20px 60px rgba(0,0,0,0.12)
- **Decorative frame:** Use `::before` pseudo-element on the image wrapper — 100% width/height, positioned offset by 20px bottom-right, border: 3px solid var(--color-primary-accent), border-radius: 12px, z-index: -1
- `.fade-in-up` on the image wrapper

### Mobile (< 768px)
- Stack vertically: image first (max-height 300px, object-fit cover), then content below
- Remove decorative frame on mobile
- Full width columns

---

## 3B — Services Section

### Structure
```html
<section id="services" class="section">
```

### Specs
- **Background:** var(--color-bg-light)
- **Text alignment:** centered header area

### Header
1. **Overline:** "WHAT WE DO" — `.overline`, centered
2. **H2:** "Tailored Services for Every Property Goal" — `.section-heading`, centered, max-width 600px, margin 0 auto
3. **Subtext:** "Whether you're buying your first home, growing an investment portfolio, or bidding at auction — we've got you covered." — `.section-subtext`, centered, margin: 0 auto 60px auto

### Cards Grid
- CSS Grid: `grid-template-columns: repeat(3, 1fr)` on desktop, `repeat(2, 1fr)` on tablet, `1fr` on mobile
- Gap: 30px
- Last row centering: if 5 cards in 3-col grid, the bottom 2 should be centered. Use flexbox fallback or CSS grid with justify-content center on wrapper.

### Each Service Card
- Background: var(--color-white)
- border-radius: 16px
- box-shadow: var(--shadow-card)
- padding: 40px 30px
- text-align: center
- transition: transform var(--transition-default), box-shadow var(--transition-default)
- **Hover:** transform: translateY(-6px), box-shadow: var(--shadow-card-hover), plus a gold top border appears (use `border-top: 3px solid var(--color-primary-accent)` — transition from transparent)
- Apply `.fade-in-up` with staggered delays

### Card Content (top to bottom)
1. **Icon circle:** 60px × 60px, background: var(--color-primary-accent), border-radius: 50%, centered, flex center center
   - White Font Awesome icon inside, 24px
2. **Service name:** Inter, 20px, 600 weight, var(--color-primary-dark), margin: 20px 0 12px
3. **Description:** Inter, 15px, var(--color-muted), line-height: 1.6
4. **Link:** "Learn More →" — var(--color-primary-accent), 14px, 600 weight, margin-top: 20px, inline-block, hover: underline

### The 5 Cards
| # | Icon | Name | Description |
|---|------|------|-------------|
| 1 | `fa-home` | HomePath Acquisition | Helping first-home buyers and upgraders secure the perfect property with minimal stress. |
| 2 | `fa-chart-line` | WealthTrack Strategy | Tailored investment plans to build property portfolios and long-term wealth. |
| 3 | `fa-piggy-bank` | SMSF Property Guidance | Strategic guidance for SMSF investors planning for retirement. |
| 4 | `fa-gavel` | Precision Bidding Service | Expert representation at auctions to secure your property at the right price. |
| 5 | `fa-handshake` | Complete Guided Purchase | From research to settlement, we manage every detail for a seamless experience. |
