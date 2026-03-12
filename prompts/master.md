# Guidestone Property — Master Build Orchestrator
## Parallel Agent Architecture for Claude Code CLI

---

## HOW TO RUN THIS

From the project root directory, execute this prompt with Claude Code:

```bash
claude -p "Read prompts/master.md and execute the build plan described in it. Follow every instruction precisely."
```

Or in an interactive session:
```
> Read prompts/master.md and execute the full build plan.
```

---

## BUILD OVERVIEW

This build uses a **scaffold → parallel sections → assembly** pattern:

```
PHASE 1 (sequential)     → Scaffold base HTML + directories
                             ↓
PHASES 2–8 (parallel)    → 7 agents build section partials simultaneously
                             ↓
PHASE 9 (sequential)     → Assembly, conflict resolution, responsive QA
```

Each parallel agent reads the shared `prompts/00-design-system.md` for design tokens and conventions, then outputs a standalone HTML partial into the `sections/` directory. The final assembly agent merges everything into a single `index.html`.

---

## EXECUTION PLAN

### ═══ STAGE 1: SCAFFOLD (Sequential — must complete before Stage 2) ═══

**Read** `prompts/00-design-system.md` and `prompts/phase-01-scaffold.md`, then execute Phase 01.

This creates:
- `index.html` — base file with `<head>`, CDN links, CSS variables, shared classes, global JS utilities, and placeholder comments for section injection
- `sections/` — empty directory for partial files

**Verify:** Open `index.html` — blank page, no console errors, fonts + Font Awesome loaded.

---

### ═══ STAGE 2: PARALLEL SECTION BUILD (Spawn 7 agents simultaneously) ═══

After the scaffold is confirmed working, spawn **7 parallel sub-agents** using the Task tool. Each agent:
1. Reads `prompts/00-design-system.md` (MANDATORY — this is the shared contract)
2. Reads its assigned phase prompt file
3. Builds its section partial and writes it to the `sections/` directory

**IMPORTANT INSTRUCTIONS FOR SPAWNING:**
- Use exactly 7 Task tool calls in a SINGLE message to launch them in parallel
- Each agent prompt MUST start with: "Read prompts/00-design-system.md first. Then read prompts/phase-XX-YYYY.md. Execute the instructions to build the section partial. Write your output to sections/section-XX-YYYY.html. Do not modify index.html."
- Wait for ALL 7 agents to complete before proceeding to Stage 3

#### Agent 1 — Hero + Nav + Stats
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-02-hero.md. Build the navigation bar, hero section, and stats bar as described. Write the complete partial to sections/section-02-hero.html. Include a <style> block for section-specific CSS, the HTML sections, and a <script> block for section-specific JS. Do not create or modify index.html."
```

#### Agent 2 — Why Choose Us + Services
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-03-services.md. Build the Why Choose Us section and Services card grid as described. Write the complete partial to sections/section-03-services.html. Include a <style> block, the HTML sections, and a <script> block. Do not create or modify index.html."
```

#### Agent 3 — Guidestone Method Timeline
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-04-method.md. Build the 9-step Guidestone Method timeline with alternating cards and scroll animations as described. Write the complete partial to sections/section-04-method.html. Include a <style> block, the HTML sections, and a <script> block. Do not create or modify index.html."
```

#### Agent 4 — Coverage Map + Founder Story
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-05-coverage-founder.md. Build the Where We Buy state cards and Founder biography section as described. Write the complete partial to sections/section-05-coverage.html. Include a <style> block, the HTML sections, and a <script> block. Do not create or modify index.html."
```

#### Agent 5 — Core Values + Testimonials
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-06-values-testimonials.md. Build the core values strip and testimonials carousel as described. Write the complete partial to sections/section-06-values.html. Include a <style> block, the HTML sections, and a <script> block. Do not create or modify index.html."
```

#### Agent 6 — Contact Us
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-07-contact.md. Build the Contact Us section with contact method cards, social links, and contact form as described. Write the complete partial to sections/section-07-contact.html. Include a <style> block, the HTML sections, and a <script> block. Do not create or modify index.html."
```

#### Agent 7 — CTA Banner + Footer
```
Prompt: "Read prompts/00-design-system.md first for the shared design contract. Then read prompts/phase-08-cta-footer.md. Build the final CTA banner section and the site footer as described. Write the complete partial to sections/section-08-footer.html. Include a <style> block, the HTML sections (<section> for CTA, <footer> for footer), and a <script> block. Do not create or modify index.html."
```

---

### ═══ STAGE 3: ASSEMBLY + QA (Sequential — after all agents complete) ═══

**Verify** all 7 partial files exist:
```bash
ls -la sections/
# Expected:
# section-02-hero.html
# section-03-services.html
# section-04-method.html
# section-05-coverage.html
# section-06-values.html
# section-07-contact.html
# section-08-footer.html
```

If any file is missing, re-run the corresponding agent.

Then **read** `prompts/phase-09-assembly.md` and execute the assembly process:

1. Read each partial file
2. Extract `<style>`, `<section>`/`<header>`/`<footer>`, and `<script>` blocks
3. Inject into `index.html` at the correct positions
4. Run all conflict resolution checks
5. Run responsive audit
6. Run accessibility audit
7. Run JS verification
8. Clean up

**Final verification:** Open `index.html` in a browser and confirm:
- All 12 sections render in correct order
- Scroll animations fire
- Nav transitions on scroll
- Testimonial carousel auto-rotates
- Contact form shows success state on submit
- Mobile nav hamburger works
- No console errors
- No horizontal overflow on mobile

---

## FILE MAP (after build)

```
guidestone-property/
├── prompts/
│   ├── master.md                    ← THIS FILE (orchestrator)
│   ├── 00-design-system.md          ← Shared design contract
│   ├── phase-01-scaffold.md         ← Stage 1
│   ├── phase-02-hero.md             ← Stage 2 (parallel)
│   ├── phase-03-services.md         ← Stage 2 (parallel)
│   ├── phase-04-method.md           ← Stage 2 (parallel)
│   ├── phase-05-coverage-founder.md ← Stage 2 (parallel)
│   ├── phase-06-values-testimonials.md ← Stage 2 (parallel)
│   ├── phase-07-contact.md          ← Stage 2 (parallel)
│   ├── phase-08-cta-footer.md       ← Stage 2 (parallel)
│   └── phase-09-assembly.md         ← Stage 3
├── sections/                        ← Temporary partials (deleted after assembly)
│   ├── section-02-hero.html
│   ├── section-03-services.html
│   ├── section-04-method.html
│   ├── section-05-coverage.html
│   ├── section-06-values.html
│   ├── section-07-contact.html
│   └── section-08-footer.html
├── index.html                       ← FINAL OUTPUT
└── content.md                       ← Source content
```

---

## TROUBLESHOOTING

**If a section doesn't render:** Check that its `<section id="...">` tag matches the expected ID from the design system's section order table. Check the browser console for JS errors from that section's IIFE.

**If styles conflict:** Every section's CSS MUST be prefixed with its section ID. If you see unprefixed selectors like `.card` instead of `#services .card`, add the prefix during assembly.

**If animations don't fire:** Verify the scaffold's IntersectionObserver is running. Check that elements have the `fade-in-up` class. Check that the observer's threshold and rootMargin values allow triggering.

**If fonts look wrong:** Verify only ONE Google Fonts `<link>` tag exists. Check that CSS uses `var(--font-heading)` and `var(--font-body)`, not hardcoded font names.
