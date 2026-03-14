# Guidestone Property — Website Changes V2
## Parallel Agent Execution Prompts for Claude Code

> **Architecture:** Single-file site (`index.html`, ~1723 lines). All CSS is in `<style>` block (lines 18-842), HTML body (lines 844-1415), JS scripts (lines 1420-1720).
> **Design System:** Navy (#1a2332), Gold (#c8a45c), Slate (#2c3e50), Off-white (#f8f6f1). Fonts: Playfair Display (headings), Inter (body). Font Awesome 6.5.1 for icons.
> **File path:** `index.html` in root directory.

---

## DEPENDENCY MAP

```
Phase 1 (Scaffold prep) → Phase 2 (Parallel Agents A-F) → Phase 3 (Assembly QA)
```

**Phase 2 agents are INDEPENDENT and can run in parallel.** Each agent targets a specific section ID and line range. No agent touches another agent's section.

---

## PHASE 1 — PRE-FLIGHT (Sequential, run first)

**Agent 0: Backup & Prep**

```
Create a backup copy of index.html as index-backup.html before any changes.
```

---

## PHASE 2 — PARALLEL AGENTS (Run all 6 simultaneously)

---

### AGENT A: Hero + Brand Story + Stats Overhaul
**Target sections:** `#hero` (lines 889-907), `#stats` (lines 912-931)
**CSS target:** Lines 344-521

**Changes:**

1. **Hero background image:** Replace the current Fed Square/trams Unsplash image (`photo-1514395462725-fb4566210144`) with a clean, simple Australian house exterior. Use this Unsplash image instead:
   `https://images.unsplash.com/photo-1600596542815-ffad4c1539a0?w=1920&q=80`
   (Modern house exterior, clean, warm — NOT an apartment or high-rise)

2. **Remove trust line:** Delete the entire `<p class="hero-trust">` block (lines 899-902) that says "Trusted by 100+ clients across VIC, NSW, QLD, SA & NT". Remove associated CSS for `.hero-trust` as well.

3. **Add Brand Story section:** Insert a NEW section immediately AFTER the `#hero` section and BEFORE the `#stats` section. This is a new `<section id="brand-story">` with:
   - Background: `var(--color-white)`
   - Centered layout, max-width 800px
   - Overline: "OUR PURPOSE"
   - Heading: "Why Guidestone Property Exists"
   - Two paragraphs of body text:
     - Paragraph 1: "Property decisions shape financial futures — but the path is often unclear and stressful. Guidestone Property was created to bring structure, insight, and confidence to that journey. Like a guiding marker that shows the way forward, we help our clients move with clarity, strategy, and certainty toward long-term wealth."
     - Paragraph 2: "We are more than a buyers agency — we are your strategic partner, dedicated to helping you navigate the property market with confidence and achieve long-term wealth. We guide home buyers and investors through every step of the property journey, combining strategy, research, and expertise to secure the right property with confidence."
   - Use existing design system classes: `.section`, `.container`, `.text-center`, `.overline`, `.section-heading`, `.section-subtext`, `.fade-in-up`
   - Add appropriate CSS for `#brand-story` following existing patterns (clean, minimal)
   - Optionally include a simple house icon (Font Awesome `fa-house-chimney`) centered above the overline, in gold color, 40px size

4. **Stats bar:** Replace the entire stats grid content. Keep ONLY ONE stat:
   - "60+" with label "Properties Secured Across Australia"
   - Remove all other stat items (States Covered, Client Satisfaction, Years Experience)
   - Center the single stat item. Update CSS: change `.stats-grid` from `display: flex; justify-content: space-around` to `display: flex; justify-content: center`
   - Remove the `border-right` styling on `.stat-item:not(:last-child)` since there's only one item
   - Update the `data-target` to `60` and `data-suffix` to `"+"`

**CSS additions needed:**
- `#brand-story` section styling (padding, centered text)
- `#brand-story .brand-icon` if adding the house icon
- `#brand-story .brand-paragraph` for body text paragraphs (use same style as `.section-subtext` but allow full width up to 800px, `color: var(--color-secondary)`, `line-height: 1.7`, `font-size: 17px`)
- Responsive rules for brand-story at 768px and 480px breakpoints

---

### AGENT B: Services Section + New Pathway Section
**Target sections:** `#services` (lines 987-1027)
**CSS target:** Lines 542-572

**Changes:**

1. **HomePath Acquisition card (first service card):** Update the description text from:
   "Helping first-home buyers and upgraders secure the perfect property with minimal stress."
   The word "upgraders" is already present, so just confirm it says "first-home buyers and upgraders". If not, add "and upgraders" after "first-home buyers". **Actually check current text — line 998 says "Helping first-home buyers and upgraders" — this is already correct. No change needed here.**

2. **Add NEW "Property Pathway" section:** Insert a NEW section AFTER `#services` and BEFORE `#method`. Create `<section id="pathway">` with:
   - Background: `var(--color-white)`
   - Centered header with overline "YOUR JOURNEY" and heading "A Structured Pathway to Smarter Property Decisions"
   - 6 pathway steps displayed as a horizontal timeline or vertical card list:

   **Step 1 — Foundation**
   - Subtitle: "Education & Goal Setting"
   - Description: "Learn the property fundamentals, market trends, growth opportunities, investment strategies and align it with your goals."
   - Icon: `fa-graduation-cap`

   **Step 2 — Clarity**
   - Subtitle: "Discovery & Strategy"
   - Description: "We refine your goals into a tailored property strategy."
   - Icon: `fa-compass`

   **Step 3 — Research**
   - Subtitle: "Market Insight & Opportunity Search"
   - Description: "Analyse markets, suburbs, and property opportunities."
   - Icon: `fa-magnifying-glass-chart`

   **Step 4 — Selection**
   - Subtitle: "Smart Shortlist & Negotiation"
   - Description: "Evaluate, shortlist, and negotiate for the right property."
   - Icon: `fa-list-check`

   **Step 5 — Acquisition**
   - Subtitle: "Contract to Settlement"
   - Description: "Manage inspections, finance, legal steps, and settlement."
   - Icon: `fa-file-contract`

   **Step 6 — Partnership**
   - Subtitle: "Ongoing Portfolio Support"
   - Description: "Post-settlement guidance, property management, and future growth planning."
   - Icon: `fa-handshake`

   **Design approach:** Use a 3-column grid (responsive to 2-col then 1-col) of cards. Each card should have:
   - A gold numbered circle (like the method section) or icon circle
   - Bold step name (e.g., "Foundation")
   - Subtitle in muted text
   - Description paragraph
   - Use `var(--color-bg-light)` card backgrounds with `border-radius: 16px`, the standard `var(--shadow-card)` and hover effect matching service cards
   - Gold left border or top border accent on hover

   **CSS needed:**
   - `#pathway` section, header, grid, cards
   - Responsive breakpoints at 1024px, 768px, 480px
   - `.fade-in-up` animations with staggered delays

---

### AGENT C: Guidestone Method Overhaul
**Target section:** `#method` (lines 1032-1114)
**CSS target:** Lines 574-624

**Changes:**

1. **Remove trademark symbol:** Change the heading from `The Guidestone Method&trade;` to just `The Guidestone Method` (remove `&trade;`)

2. **Add subtitle:** Change the subtitle/subtext from:
   "Our signature process ensures you make informed, confident property decisions every step of the way."
   To:
   "Our 9-Step Property Buying Journey"
   Keep it as the `.section-subtext` element but make it slightly bolder/larger — consider using `font-weight: 600` and `font-size: 20px` to make it feel like a true subtitle rather than body text.

3. **Replace ALL 9 method steps** with the following new content. Keep the exact same HTML structure (method-step, method-circle, method-card with icon/title/desc), just update the content:

   **Step 1 — Discovery Call**
   - Icon: `fa-phone-alt`
   - Title: "Discovery Call"
   - Description: "A complimentary consultation to understand your goals, budget, timeline, and property vision. This helps determine the best path forward for your purchase."

   **Step 2 — Engagement & Strategy Session**
   - Icon: `fa-file-signature`
   - Title: "Engagement & Strategy Session"
   - Description: "Once a working agreement is signed, a detailed strategy session to define the right approach. We align on your investment goals, target locations, property type, and criteria to ensure every decision supports your long-term outcomes."

   **Step 3 — Market Analysis**
   - Icon: `fa-search-location`
   - Title: "Market Analysis"
   - Description: "In-depth research into suburbs, market trends, growth drivers, and property fundamentals to identify opportunities aligned with your strategy and strong long-term potential."

   **Step 4 — Property Search & Due Diligence**
   - Icon: `fa-list-check`
   - Title: "Property Search & Due Diligence"
   - Description: "We actively search for suitable properties including both on-market and off-market opportunities, completing due diligence. A curated shortlist of high-quality properties is presented with insights and recommendations."

   **Step 5 — Negotiation & Secure**
   - Icon: `fa-balance-scale`
   - Title: "Negotiation & Secure"
   - Description: "We negotiate on your behalf to secure the property at the best possible price and favourable terms."

   **Step 6 — Contract Management**
   - Icon: `fa-clipboard-check`
   - Title: "Contract Management"
   - Description: "Managing the timelines from conditional to unconditional stage — coordinating building and pest inspections, finance — ensuring no hidden surprises and cost."

   **Step 7 — Property Manager Introduction**
   - Icon: `fa-user-tie`
   - Title: "Property Manager Introduction"
   - Description: "If the property is an investment, we introduce trusted property managers who can help maximise rental returns and manage the property effectively from day one."

   **Step 8 — Secure & Settle**
   - Icon: `fa-key`
   - Title: "Secure & Settle"
   - Description: "We liaise with your broker, conveyancer, and agents to ensure a smooth settlement process."

   **Step 9 — Ongoing Partnership**
   - Icon: `fa-chart-line`
   - Title: "Ongoing Partnership"
   - Description: "Our relationship doesn't end at settlement. We remain available to support you with portfolio guidance, future purchases, renovation insights, and ongoing property strategy."

**No CSS changes needed** — the timeline structure stays the same, just content updates.

---

### AGENT D: Coverage Section Simplification
**Target section:** `#coverage` (lines 1119-1157)
**CSS target:** Lines 629-677

**Changes:**

1. **Remove city descriptions from all coverage cards.** Each card should show ONLY the state abbreviation — remove the `<div class="coverage-card-cities">` element from every card, or set its content to empty/remove it.

   Final cards should be:
   - VIC (no cities listed)
   - NSW (no cities listed)
   - QLD (no cities listed)
   - SA (no cities listed)
   - WA (no cities listed)
   - NT (no cities listed)

2. **Update the subtext** to just: "Our team covers major property markets across six states and territories." (Remove "From Melbourne to Perth" prefix)

3. **Optionally** make the cards slightly more compact since they have less content — reduce padding from `32px 24px` to `24px 20px`.

---

### AGENT E: Remove Testimonials + Reviews
**Target sections:** `#testimonials` (lines 1229-1280)
**CSS target:** Lines 692-738
**JS target:** Lines 1621-1690 (testimonials carousel script)

**Changes:**

1. **Delete the ENTIRE `#testimonials` section** from the HTML (lines 1229-1280).
2. **Delete ALL CSS rules** scoped to `#testimonials` (lines 692-738 and responsive rules within media queries).
3. **Delete the entire testimonials carousel JS script block** (lines 1618-1690, the `<script>` block with carousel logic).
4. **Keep the `#values` section intact** — do NOT touch it.

---

### AGENT F: Contact, CTA & Footer Updates
**Target sections:** `#contact` (lines 1285-1338), `#cta` (lines 1343-1353), `#footer` (lines 1360-1415)
**CSS target:** Lines 740-841

**Changes:**

1. **Contact section heading:** The heading already says "Let's Start Your Property Journey" — keep it. But update the subtext to:
   "Let's start your property journey together. Reach out and we'll get back to you within 24 hours."

2. **Update contact details:**
   - **Email:** Change from `hello@guidestoneproperty.com.au` to `connect@guidestoneproperty.com.au` (update both the `href="mailto:..."` and display text) — do this in the contact card AND in the footer
   - **Phone:** Change from `+61 4XX XXX XXX` to `0433 674 084` — update `href="tel:+61433674084"` and display text `0433 674 084` — do this in the contact card, WhatsApp card (update WhatsApp link to `https://wa.me/61433674084`), AND in the footer
   - Remove the "Our Base" / location contact card entirely (the one with map-marker-alt showing "Melbourne, Victoria")

3. **CTA section:**
   - Change the background image from the current apartment/skyscraper image (`photo-1486406146926-c627a92ad1ab`) to a handshake or house keys image. Use:
     `https://images.unsplash.com/photo-1560518883-ce09059eeffa?w=1920&q=80`
     (House keys on a table — warm, property-relevant, no apartments)
   - Update heading to: "Ready to Start Your Property Journey?"
   - Keep the CTA button and disclaimer as-is

4. **Footer contact details:** Update email and phone to match the new values:
   - Email: `connect@guidestoneproperty.com.au`
   - Phone: `0433 674 084` with `href="tel:+61433674084"`
   - WhatsApp: `href="https://wa.me/61433674084"`

---

## PHASE 3 — ASSEMBLY QA (Sequential, run after all Phase 2 agents complete)

**Agent Z: Final Validation**

```
After all Phase 2 agents have completed their changes to index.html:

1. Open the file and verify HTML structure is valid — no unclosed tags, no duplicate section IDs
2. Verify the section order is now:
   - #navbar
   - #hero
   - #brand-story (NEW)
   - #stats
   - #why-us
   - #services
   - #pathway (NEW)
   - #method
   - #coverage
   - #founder
   - #values
   - (NO #testimonials — removed)
   - #contact
   - #cta
   - #footer
3. Verify no orphaned CSS rules for #testimonials remain
4. Verify no orphaned JS for testimonials carousel remains
5. Verify all contact details consistently show:
   - Email: connect@guidestoneproperty.com.au
   - Phone: 0433 674 084
6. Verify the Method section has NO trademark symbol
7. Verify coverage cards have NO city names
8. Verify stats bar shows only "60+" stat
9. Check that the #pathway section and #brand-story section have proper responsive CSS
10. Ensure nav links still work — update if any anchor targets changed
11. Update the nav bar to include a link to #pathway if desired, or leave navigation as-is
12. Run a quick visual check — load in browser if possible
```

---

## SUMMARY OF ALL CHANGES

| # | Change | Agent | Section |
|---|--------|-------|---------|
| 1 | Replace hero bg + add brand story section | A | #hero, NEW #brand-story |
| 2 | Remove "Trusted by 100+ clients" trust line | A | #hero |
| 3 | Stats: Only "60+ Properties Secured Across Australia" | A | #stats |
| 4 | Services: Confirm "upgraders" after first home buyers | B | #services |
| 5 | Add Pathway section (6 steps) under services | B | NEW #pathway |
| 6 | Remove TM from Guidestone Method | C | #method |
| 7 | Add subtitle "Our 9-Step Property Buying Journey" | C | #method |
| 8 | Update all 9 method step contents | C | #method |
| 9 | Coverage: State names only, no cities | D | #coverage |
| 10 | Remove entire testimonials section + CSS + JS | E | #testimonials |
| 11 | Update contact: email, phone | F | #contact |
| 12 | Update CTA: new image, new heading | F | #cta |
| 13 | Update footer: email, phone | F | #footer |
