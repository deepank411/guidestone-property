# Phase 07: Contact Us Section

## PREREQUISITE
Read `prompts/00-design-system.md` before starting. Your output file is `sections/section-07-contact.html`.

## OBJECTIVE
Build a comprehensive Contact Us section with all standard contact methods — phone, WhatsApp, email, contact form, social media links, and business hours.

---

## OUTPUT FILE: `sections/section-07-contact.html`

---

## Section Specs

### Structure
```html
<section id="contact" class="section">
```

### Background & Layout
- **Background:** var(--color-bg-light)
- **Layout:** Two columns
  - Left: 45% — contact information cards
  - Right: 55% — contact form
  - Gap: 60px
  - On mobile: stack vertically, info cards first, form below

### Header (full-width above the two columns)
1. **Overline:** "GET IN TOUCH" — `.overline`, centered
2. **H2:** "Let's Start Your Property Journey" — `.section-heading`, centered
3. **Subtext:** "Have a question or ready to take the next step? Reach out through any of the channels below, or fill in the form and we'll get back to you within 24 hours." — `.section-subtext`, centered, margin: 0 auto 60px auto

---

## Left Column — Contact Information

### Contact Method Cards
Stack 4 cards vertically, each with consistent styling:
- Background: var(--color-white)
- border-radius: 12px
- padding: 24px 28px
- margin-bottom: 16px
- box-shadow: var(--shadow-card)
- display: flex, align-items: center, gap: 20px
- transition: var(--transition-default)
- **Hover:** transform: translateX(6px), border-left: 3px solid var(--color-primary-accent)
- Apply `.fade-in-up` with staggered delays

### Card 1 — Phone
- Icon: `<i class="fas fa-phone-alt">` in a 48px gold circle (gold bg at 12% opacity, gold icon 20px)
- Title: "Call Us" — Inter, 16px, 600, var(--color-primary-dark)
- Value: "+61 4XX XXX XXX" — Inter, 15px, var(--color-secondary)
- Subtext: "Mon – Sat, 9am – 6pm AEST" — Inter, 13px, var(--color-muted)
- Wrap value in `<a href="tel:+614XXXXXXXX">` for click-to-call

### Card 2 — WhatsApp
- Icon: `<i class="fab fa-whatsapp">` in a 48px circle (background: rgba(37,211,102,0.1), icon color: #25D366)
- Title: "WhatsApp" — Inter, 16px, 600, var(--color-primary-dark)
- Value: "+61 4XX XXX XXX" — Inter, 15px, var(--color-secondary)
- Subtext: "Quick replies, usually within 1 hour" — Inter, 13px, var(--color-muted)
- Wrap value in `<a href="https://wa.me/614XXXXXXXX" target="_blank" rel="noopener">`

### Card 3 — Email
- Icon: `<i class="fas fa-envelope">` in a 48px gold circle
- Title: "Email Us" — Inter, 16px, 600, var(--color-primary-dark)
- Value: "hello@guidestoneproperty.com.au" — Inter, 15px, var(--color-primary-accent)
- Subtext: "We respond within 24 hours" — Inter, 13px, var(--color-muted)
- Wrap value in `<a href="mailto:hello@guidestoneproperty.com.au">`

### Card 4 — Location
- Icon: `<i class="fas fa-map-marker-alt">` in a 48px gold circle
- Title: "Our Base" — Inter, 16px, 600, var(--color-primary-dark)
- Value: "Melbourne, Victoria" — Inter, 15px, var(--color-secondary)
- Subtext: "Serving clients nationwide across Australia" — Inter, 13px, var(--color-muted)

### Social Media Links (below the cards)
- Heading: "Follow Us" — Inter, 14px, 600, uppercase, letter-spacing: 2px, var(--color-muted), margin: 28px 0 16px
- Row of 4 social icons, flex, gap: 12px
- Each icon: 44px circle, border: 1px solid rgba(200,164,92,0.3), centered icon
  - Default: icon color var(--color-muted)
  - Hover: background var(--color-primary-accent), icon color white, border-color var(--color-primary-accent), transform: translateY(-3px)
  - transition: var(--transition-default)
- The 4 platforms:
  1. `<i class="fab fa-linkedin-in">` — href="https://linkedin.com/company/guidestoneproperty" (placeholder)
  2. `<i class="fab fa-instagram">` — href="https://instagram.com/guidestoneproperty" (placeholder)
  3. `<i class="fab fa-facebook-f">` — href="https://facebook.com/guidestoneproperty" (placeholder)
  4. `<i class="fab fa-tiktok">` — href="https://tiktok.com/@guidestoneproperty" (placeholder)
- All links: `target="_blank" rel="noopener noreferrer"`

---

## Right Column — Contact Form

### Form Container
- Background: var(--color-white)
- border-radius: 16px
- padding: 48px 40px
- box-shadow: var(--shadow-card)
- `.fade-in-up`

### Form Header
- H3: "Send Us a Message" — Inter, 22px, 600, var(--color-primary-dark), margin-bottom 8px
- Subtitle: "Fill in your details and we'll be in touch shortly." — Inter, 15px, var(--color-muted), margin-bottom 32px

### Form Fields
Use `<form id="contact-form">` with the following fields:

1. **Row 1:** Two fields side by side (flex row, gap 16px, stack on mobile)
   - First Name — `<input type="text" required placeholder="First Name">`
   - Last Name — `<input type="text" required placeholder="Last Name">`

2. **Row 2:** Full width
   - Email — `<input type="email" required placeholder="Email Address">`

3. **Row 3:** Full width
   - Phone — `<input type="tel" placeholder="Phone Number (optional)">`

4. **Row 4:** Full width dropdown
   - Interest — `<select required>`
     - Options: "I'm looking to..." (disabled, selected), "Buy my first home", "Upgrade my home", "Invest in property", "Buy through SMSF", "Bid at auction", "Other"

5. **Row 5:** Full width textarea
   - Message — `<textarea rows="4" placeholder="Tell us about your property goals..."></textarea>`

6. **Row 6:** Submit button
   - "Send Message" — `.btn-primary`, full width, padding 18px, font-size 16px
   - Icon: `<i class="fas fa-paper-plane">` before text, margin-right 8px

### Input Styling (scoped to `#contact`)
```css
#contact input,
#contact select,
#contact textarea {
  width: 100%;
  padding: 16px 20px;
  border: 1.5px solid #e0ddd6;
  border-radius: 10px;
  font-family: var(--font-body);
  font-size: 15px;
  color: var(--color-secondary);
  background: var(--color-bg-light);
  transition: var(--transition-default);
  outline: none;
  margin-bottom: 16px;
}
#contact input:focus,
#contact select:focus,
#contact textarea:focus {
  border-color: var(--color-primary-accent);
  box-shadow: 0 0 0 3px rgba(200,164,92,0.15);
}
#contact input::placeholder,
#contact textarea::placeholder {
  color: var(--color-muted);
}
```

### JS (inside IIFE)
- Form submit handler: `preventDefault()`, show a success state
- On submit:
  1. Button text changes to "Sending..." with a spinner (`fa-spinner fa-spin`)
  2. After 1.5s (simulated), replace form contents with a success message:
     - Large gold checkmark: `<i class="fas fa-check-circle">` — 48px, var(--color-primary-accent)
     - Heading: "Message Sent!" — Inter, 22px, 600
     - Text: "Thank you for reaching out. We'll get back to you within 24 hours." — Inter, 15px, var(--color-muted)
  3. This is a front-end demo — no actual backend submission

### Mobile (< 768px)
- Stack columns vertically: contact info cards first, form below
- Form padding reduces to 32px 24px
- Row 1 (first/last name): stack vertically
- Social icons: centered
