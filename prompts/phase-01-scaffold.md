# Phase 01: Scaffold — Base HTML File

## PREREQUISITE
Read `prompts/00-design-system.md` before starting.

## OBJECTIVE
Create the foundational `index.html` file that all section partials will be assembled into. This phase runs FIRST, before any parallel agents.

## TASKS

### 1. Create directory structure
```
mkdir -p sections
```

### 2. Create `index.html` with:

#### `<head>` section:
- `<!DOCTYPE html>`, lang="en", UTF-8 charset, viewport meta
- `<title>Guidestone Property — Australia's Trusted Buyer's Agency</title>`
- Meta description: "Guidestone Property is a premium buyer's agency helping home buyers and investors make smarter property decisions across Australia."
- Open Graph tags (title, description, type: website, url: https://guidestoneproperty.com.au)
- Favicon: use a simple inline SVG favicon with a gold diamond shape
- Google Fonts preconnect + stylesheet: `Playfair Display:wght@400;700` and `Inter:wght@300;400;500;600;700`
- Font Awesome 6 CDN: `https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css`

#### `<style>` block — Global CSS:
- CSS Reset (box-sizing border-box, margin/padding 0, img max-width 100%)
- `html { scroll-behavior: smooth; }`
- ALL CSS custom properties from the design system (the `:root` block)
- ALL shared utility classes from the design system (`.section`, `.container`, `.overline`, `.section-heading`, `.section-subtext`, `.text-center`, `.btn-primary`, `.btn-secondary`, `.fade-in-up`, `.fade-in-up.visible`)
- Body: `font-family: var(--font-body); color: var(--color-secondary); line-height: 1.6; overflow-x: hidden;`
- Responsive overrides for `.section` padding and `.section-heading` font-size at tablet/mobile breakpoints

#### `<body>` structure:
Create empty placeholder comments where section partials will be injected:
```html
<body>
  <!-- NAV: Injected from phase-02 -->
  <main>
    <!-- SECTION: hero (phase-02) -->
    <!-- SECTION: stats (phase-02) -->
    <!-- SECTION: why-us (phase-03) -->
    <!-- SECTION: services (phase-03) -->
    <!-- SECTION: method (phase-04) -->
    <!-- SECTION: coverage (phase-05) -->
    <!-- SECTION: founder (phase-05) -->
    <!-- SECTION: values (phase-06) -->
    <!-- SECTION: testimonials (phase-06) -->
    <!-- SECTION: contact (phase-07) -->
    <!-- SECTION: cta (phase-08) -->
  </main>
  <!-- FOOTER: Injected from phase-08 -->
</body>
```

#### `<script>` block — Global JS (at end of body):
```javascript
// 1. Scroll-triggered fade-in observer
document.addEventListener('DOMContentLoaded', function() {
  const observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        const delay = entry.target.dataset.delay || 0;
        setTimeout(function() {
          entry.target.classList.add('visible');
        }, parseInt(delay));
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

  document.querySelectorAll('.fade-in-up').forEach(function(el) {
    observer.observe(el);
  });

  // 2. Counter animation utility
  window.animateCounter = function(element, target, duration) {
    duration = duration || 2000;
    var start = 0;
    var startTime = null;
    var suffix = element.dataset.suffix || '';
    function step(timestamp) {
      if (!startTime) startTime = timestamp;
      var progress = Math.min((timestamp - startTime) / duration, 1);
      var eased = 1 - Math.pow(1 - progress, 3);
      element.textContent = Math.floor(eased * target) + suffix;
      if (progress < 1) requestAnimationFrame(step);
    }
    requestAnimationFrame(step);
  };

  // 3. Counter observer
  var counterObserver = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        var target = parseInt(entry.target.dataset.target);
        window.animateCounter(entry.target, target);
        counterObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.3 });

  document.querySelectorAll('.count-up').forEach(function(el) {
    counterObserver.observe(el);
  });
});
```

### 3. Verify
Open `index.html` in browser — it should render a blank white page with no console errors. All fonts and Font Awesome should load (check Network tab).

## OUTPUT
- `index.html` — fully formed base file ready for section injection
- `sections/` — empty directory ready for partials
