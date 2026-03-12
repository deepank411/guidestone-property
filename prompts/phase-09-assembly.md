# Phase 09: Assembly + Responsive QA

## PREREQUISITE
Read `prompts/00-design-system.md` before starting.
This phase runs LAST, after ALL parallel section agents have completed.

## OBJECTIVE
Assemble all section partials into the final `index.html`, fix any conflicts, ensure full responsiveness, and perform quality assurance.

---

## STEP 1: Assemble Partials into index.html

### Read all partial files in order:
```
sections/section-02-hero.html
sections/section-03-services.html
sections/section-04-method.html
sections/section-05-coverage.html
sections/section-06-values.html
sections/section-07-contact.html
sections/section-08-footer.html
```

### Injection process:
1. Open `index.html` (created by Phase 01 scaffold)
2. For each partial file, extract:
   - `<style>` block → append to the main `<style>` block in `<head>` (after the global styles)
   - `<section>` / `<header>` / `<footer>` blocks → inject into `<body>` at the corresponding placeholder comment
   - `<script>` block → append to the main `<script>` block at end of body (after the global JS)
3. Remove all placeholder comments after injection
4. Ensure the final section order in `<body>` is:
   ```
   <header> (navbar)
   <main>
     <section id="hero">
     <section id="stats">
     <section id="why-us">
     <section id="services">
     <section id="method">
     <section id="coverage">
     <section id="founder">
     <section id="values">
     <section id="testimonials">
     <section id="contact">
     <section id="cta">
   </main>
   <footer id="footer">
   ```

---

## STEP 2: Fix CSS Conflicts

Check for and resolve:
1. **Duplicate CSS custom property definitions** — only one `:root` block should exist (from scaffold)
2. **Conflicting class names** — all section CSS should be prefixed with section IDs. If any agent used unprefixed selectors, add the section ID prefix
3. **Font Awesome version conflicts** — ensure only one FA CDN link exists
4. **Z-index stacking** — Navbar should be highest (1000), mobile nav overlay (999), everything else auto
5. **Transition conflicts** — if multiple sections define different `.fade-in-up` behavior, normalize to the scaffold's version

---

## STEP 3: Responsive Audit

Test at three breakpoints and fix issues:

### Desktop (1200px+)
- [ ] All two-column layouts render correctly
- [ ] Cards grids show 3 columns where specified
- [ ] Timeline alternates left/right
- [ ] Images have decorative elements visible
- [ ] Nav shows all links horizontally

### Tablet (768px – 1024px)
- [ ] Two-column layouts still work or gracefully collapse
- [ ] Card grids switch to 2 columns
- [ ] Font sizes reduced by ~15%
- [ ] Section padding reduced to ~80px
- [ ] Images scale proportionally

### Mobile (< 768px)
- [ ] All layouts stack to single column
- [ ] Hamburger nav works correctly
- [ ] Hero text: 36px heading, 16px body
- [ ] Section padding: 60px
- [ ] Cards: single column, full width
- [ ] Timeline: single column with line on left
- [ ] Contact form fields stack vertically
- [ ] Footer columns stack vertically
- [ ] All touch targets are at least 44px
- [ ] No horizontal overflow (check `overflow-x`)

---

## STEP 4: Performance Polish

1. **Images:** Verify all images have `loading="lazy"` and `decoding="async"` EXCEPT the hero background (which should load eagerly)
2. **Fonts:** Ensure `<link rel="preconnect" href="https://fonts.googleapis.com">` exists
3. **CSS variables:** Verify all color values throughout the file use CSS variables, not hardcoded hex values (except in variable definitions)
4. **JS:** Ensure all IntersectionObservers use `unobserve` after triggering to prevent re-fires
5. **Smooth scroll:** Verify `html { scroll-behavior: smooth; }` is set

---

## STEP 5: Accessibility Check

1. **Heading hierarchy:** Only ONE `<h1>` (in hero). Sections use `<h2>`. Cards use `<h3>`.
2. **Semantic HTML:** `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`, `<article>` where appropriate
3. **Alt text:** All `<img>` tags have descriptive `alt` attributes
4. **Focus styles:** All interactive elements (links, buttons, form inputs) have visible `:focus-visible` outlines
5. **ARIA labels:** Hamburger button needs `aria-label="Toggle navigation"`, carousel needs `aria-label="Testimonials"`
6. **Color contrast:** Verify text on dark backgrounds has sufficient contrast (white/gold on navy is fine)
7. **Form labels:** Contact form inputs should have associated `<label>` elements (can be visually hidden if using placeholders)

---

## STEP 6: Final JS Verification

1. **Nav scroll behavior:** Nav transitions from transparent to solid on scroll
2. **Scroll animations:** All `.fade-in-up` elements animate on scroll entry
3. **Counter animations:** Stats bar numbers count up when section enters viewport
4. **Testimonial carousel:** Auto-rotates, dots work, arrows work, touch swipe works
5. **Contact form:** Submit shows loading state then success message
6. **Mobile nav:** Hamburger opens/closes overlay, links close the overlay
7. **Smooth scroll:** Nav links scroll smoothly to their target sections

---

## STEP 7: Final Cleanup

1. Remove any leftover placeholder comments
2. Remove any `console.log` statements
3. Ensure no empty `<style>` or `<script>` blocks
4. Minify nothing — keep code readable for future editing
5. Add a final HTML comment at the top: `<!-- Guidestone Property | Built [current date] -->`

## OUTPUT
- Final `index.html` — complete, single-file, production-ready landing page
- Delete the `sections/` directory (partials are no longer needed)
