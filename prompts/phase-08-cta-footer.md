# Phase 08: Final CTA + Footer

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-08-footer.html`.

## OBJECTIVE
Build the full-bleed final CTA banner and the site footer.

---

## OUTPUT FILE: `sections/section-08-footer.html`

---

## 8A — Final CTA Section

### Structure
```html
<section id="cta" class="section">
```

### Specs
- **Background image:** `url('https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=1920&q=80')` — center/cover, fixed (parallax effect on desktop)
- **Overlay:** `::before` pseudo-element, `linear-gradient(135deg, rgba(26,35,50,0.9) 0%, rgba(26,35,50,0.75) 100%)`
- **Padding:** 120px 0 (more generous than standard sections)
- **Content:** centered, max-width 700px

### Content
1. **Overline:** "TAKE THE NEXT STEP" — `.overline`, centered
2. **H2:** "Ready to Make Your Next Property Move?" — Playfair Display, 44px desktop / 32px mobile, white, centered, line-height: 1.2
3. **Subtext:** "Book a free strategy call and let's discuss how we can guide you to smarter property decisions." — Inter, 18px, rgba(255,255,255,0.8), centered, margin: 20px auto 40px
4. **CTA Button:** "Book Your Free Strategy Call" — `.btn-primary`, large: padding 20px 50px, font-size 17px
   - **Pulsing shadow animation:** CSS keyframe, `box-shadow` oscillates between `0 0 0 0 rgba(200,164,92,0.4)` and `0 0 0 20px rgba(200,164,92,0)` every 2s, infinite
5. **Sub-text:** "No obligation. No pressure. Just clarity." — Inter, 14px, italic, rgba(255,255,255,0.5), margin-top: 20px

### Mobile
- H2 reduces to 32px
- Button padding: 18px 36px
- Remove `background-attachment: fixed` (no parallax on mobile — causes issues on iOS)

---

## 8B — Footer

### Structure
```html
<footer id="footer">
```

### Specs
- **Background:** var(--color-footer-dark) — `#111a25`
- **Top border:** 2px solid var(--color-primary-accent)
- **Padding:** 70px 0 0 0 (top padding only, bottom bar has its own)

### Layout — 4 columns on desktop
Use CSS grid: `grid-template-columns: 1.5fr 1fr 1fr 1.2fr;` gap: 40px
Max-width container, centered

### Column 1 — Brand
1. **Logo:** Same as nav — "GUIDESTONE `◆` PROPERTY" in Playfair Display, 18px, white
2. **Tagline:** "Guiding You to Smarter Property Decisions" — Inter, 14px, rgba(255,255,255,0.6), margin: 16px 0 24px, line-height 1.6
3. **Social icons:** Row, gap 10px
   - 3 icons: LinkedIn (`fab fa-linkedin-in`), Instagram (`fab fa-instagram`), Facebook (`fab fa-facebook-f`)
   - Each: 36px circle, border: 1px solid rgba(255,255,255,0.15), icon color rgba(255,255,255,0.5)
   - Hover: background var(--color-primary-accent), icon color white, border-color: var(--color-primary-accent)

### Column 2 — Quick Links
- **Heading:** "Quick Links" — Inter, 14px, 600, uppercase, letter-spacing: 2px, white, margin-bottom: 20px
- Links list (no bullets, flex column, gap 12px):
  - Services → `#services`
  - Our Method → `#method`
  - About Sonal → `#founder`
  - Where We Buy → `#coverage`
  - Contact → `#contact`
- Style: Inter, 14px, rgba(255,255,255,0.5), no underline, hover: var(--color-primary-accent)

### Column 3 — Services
- **Heading:** "Services" — same style as Column 2 heading
- Links list:
  - Home Buyers
  - Property Investors
  - SMSF Guidance
  - Auction Bidding
  - End-to-End Support
- Style: same as Quick Links (these don't need to link anywhere specific — use `href="#services"` for all)

### Column 4 — Contact Info
- **Heading:** "Contact" — same style as Column 2 heading
- Items (flex column, gap 16px):
  1. `<i class="fas fa-envelope">` + "hello@guidestoneproperty.com.au" — wrapped in `<a href="mailto:...">`
  2. `<i class="fas fa-phone-alt">` + "+61 4XX XXX XXX" — wrapped in `<a href="tel:...">`
  3. `<i class="fab fa-whatsapp">` + "WhatsApp Us" — wrapped in `<a href="https://wa.me/614XXXXXXXX">`
  4. `<i class="fas fa-map-marker-alt">` + "Melbourne, Australia — Serving Nationwide"
- Icon style: var(--color-primary-accent), 14px, margin-right: 10px
- Text style: Inter, 14px, rgba(255,255,255,0.5), hover: white on links

### Bottom Bar
- Full width, background: rgba(0,0,0,0.2), margin-top: 50px, padding: 20px 0
- Flex, space-between, centered container
- Left: "© 2026 Guidestone Property. All rights reserved." — Inter, 13px, rgba(255,255,255,0.35)
- Right: "Privacy Policy | Terms of Service" — Inter, 13px, rgba(255,255,255,0.35), links hover: white
  - Separator `|` with margin: 0 12px

### Mobile (< 768px)
- 4 columns → single column stack
- Each column: margin-bottom 40px
- Bottom bar: flex-direction column, text-align center, gap 8px
- Reduce padding
