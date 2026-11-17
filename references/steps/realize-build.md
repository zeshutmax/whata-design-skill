# Step: Build it (`realize-build`, stage realize)
**Goal:** Choose the platform and build so the core content works first and effects layer on top. Use an AI agent that reads the DESIGN.md if helpful.
**Your role:** Build the page. Meaning first, then presentation, then behavior; content must work when the enhancements fail.
**Inputs:** homepage-design, component-set, motion-spec, assets, design-tokens  
**Output artifact:** built-site -> `(the project's source tree)`
## Procedure
1. Do not build in the site tree before the owner has picked a direction (direction-decision.md has `Owner pick:`). If you find unpicked work there (a build of a direction the owner did not choose), do not carry it forward: say so and ask whether to discard it.
2. Restyling an existing site that uses a component library (for example shadcn with Tailwind)? Do not rebuild the components. Map the design's colour roles onto the library's own role variables inside one scoped class (such as a theme class on the section or header), keep new CSS in a cascade layer (`@layer components`) so the library's utilities still win (unlayered custom CSS beat Tailwind's `hidden` in a test). First grep the global CSS for unlayered `*`, `html` and `body` rules: an unlayered `* { border-color: ... }` beats every layered border colour and stops the library's own border utilities from applying, so where such a rule sets border-color or colour, do not layer that CSS, and change the library's component files only where a role cannot express the change.
3. After every CSS change, confirm the new rule is in the stylesheet the server actually sends (fetch it, or read the computed style in the browser) before trusting a review: a dev server that missed three edits made the audit judge stale CSS without any warning.
4. Re-theming library components (shadcn and similar) breaks text at 200% in the same few places: badges that clip text, `line-clamp`, fixed-height bars and rows, `grid-cols-N` without a mobile fallback, and flex rows that cannot wrap. Check those five before the first audit.
5. Write control borders and other colours the audit must read as plain hex or rgb; the audit cannot always read modern colour functions (`oklch()`, `lab()`) and may report a border that is not there.
6. Name your own classes so they cannot collide with the project's utility framework: in Tailwind projects a section class `table` became `display: table` and shrank every such section to its content, and a `spine` class restyled every list. Prefix page classes or scope them under one page class.
7. Studio build (get_studio engine, nextjs or astro, patterns, layout): compose each section with a different layout family and make the static page complete and beautiful with motion off; then add motion through the studio engine (one clock, page lifecycle, data attributes; copy it, do not rewrite it) and build the concept as one driver module (one variable, such as scroll progress or time, drives every visual that carries the concept). Design the reduced-motion and no-JS versions on purpose. Avoid, unless the concept demands it: an eyebrow label above every heading, glass everywhere, decorative 01/02/03 when the content is not a sequence, three equal cards.
8. New page or a rebuilt structure: start from the base kit parts (get_base) in the project's tokens, and adapt them to the stack (components in a framework, partials in a static site); keep their accessibility details (menu button states, form error wiring, 44 px targets, wrapping rows).
9. Choose the stack from the constraints. Write semantic HTML first (landmarks, headings, real links and buttons), then CSS from the tokens (no raw hex in components), then behavior as enhancement. [Craft: layers; progressive enhancement]
10. Apply the direction's recipe steps and the component patterns. Keep the DOM order equal to the reading order; add a skip link; keep focus visible.
11. Read the rule list for the build once before starting (get_guidelines topic: build) and keep generate_hints in mind; re-run review_design after each section and fix blockers immediately.
12. Commit in small steps (if the project allows version control); keep a CHANGELOG of decisions that deviate from the tokens.
13. Unconfirmed facts shown on the page (see protocol 3.2): mark each with the visible `.assumed` marker, never brackets, add a legend on the page, and list each in design/OPEN-QUESTIONS.md. For a marked phone number or address inside a link, follow the `<Assumed>` pattern in `rules/build.md` (a solid link underline plus an inner marker; one legend plus `aria-describedby`).
14. Public-service or crisis audience: build the urgent route from the recipe `urgent-help-route` (the emergency-services line once, a `tel:` link with hours and an out-of-hours route, contrast and text instead of red alone) and check at 390x844 that it does not push the primary action below the first screen. Forms: build every form from `form-no-backend-and-privacy` (labels, `type`, `inputmode` and `autocomplete`, native `required`, the no-backend `mailto:` fallback with its honest success text, the privacy line, and no promise that anything was sent). If the audience flags the COGA rules, build to them as majors (`rules/build.md` lists all fifteen). [Our take]
15. Legal, medical, financial or safety advice on the page: it stays under the draft marker and legend until a qualified person has reviewed it (`copy-expert-review-before-launch`); record the reviewer and the date or the open question in design/OPEN-QUESTIONS.md.
## Sections track (default)
Applies only when the owner and you chose the sections track. In full, sprint and lean tracks ignore this section.
- homepage-design, component-set, motion-spec, assets and design-tokens do not exist in this track. section-pick.md replaces all five: build from the picked library sections (get_library_section for each), in the picked order.
- Copy sections.css, roles.css and sections.js unchanged, then each section's markup. Put the design system's --ds-* tokens from section-pick.md on the page root together with the class ds, so every section takes its type, colour, buttons, radii, container and rhythm from the one system. Change only what each spec lists under Adaptation slots; never edit sections.css or roles.css per project (a missing role is added to the library's roles.css).
- A longer headline or a different object may need a slot the spec allows (for example the h1 stepping down until it fits one line). A change the spec does not allow is a change to the section: stop and ask the owner, or pin a new section (content/sections/HOW-TO-ADD.md).
- Every picture slot gets real media from the media plan. Code-drawn stand-ins for photos read as cheap.
- Before the checks: shoot each adapted section at 1440x900 and 390x844 and put it beside its source (sourceFold, or the live sourceUrl for a lower section). It must visibly belong next to it; if it does not, fix the adaptation before anything else.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- homepage-design, component-set, motion-spec and assets do not exist in lean. Build from direction-decision.md (the chosen direction), design-tokens (tokens.css, DESIGN.md), headline-drafts.md (the copy) and the chosen hero in hero-concepts/ (its markup is the first draft of the build: keep it, do not rebuild it).
- Native elements first; list each interactive component and its keyboard behaviour in the build notes. Take the motion and reduced-motion variants from the hero's notes.md. List assets, licences and alt text in the build notes. Check the sections at 320, 390, 768 and 1440 px while building.
- The page must keep the lead element and give it a second moment lower down, and the sections below the hero must differ in structure from each other (see realize-qa). Build the sections that way, not as a plain run of headings and paragraphs.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- homepage-design, component-set, motion-spec and assets do not exist in the sprint. The prototype from decide-prototype is the first draft of the build: keep it (promote it to the site root if it was built elsewhere, record the move in the build notes) and finish it from direction-decision.md, design-tokens (tokens.css, DESIGN.md), headline-drafts.md and the chosen hero in hero-concepts/. Do not rebuild it. This step runs after Day 5; the sprint is not over at decide-tokens.
- Native elements first; list each interactive component and its keyboard behaviour in the build notes. Take the motion and reduced-motion variants from the hero's notes.md. List assets, licences and alt text in the build notes. Check the sections at 320, 390, 768 and 1440 px while building, and design the states the prototype skipped (hover, focus, active, disabled, loading, empty, error).
- The page must keep the lead element and give it a second moment lower down, and the sections below the hero must differ in structure from each other (see realize-qa). Build the sections that way, not as a plain run of headings and paragraphs.
## Ask the owner (only what you cannot default)
- Which stack? (a) the project's current stack (recommended) (b) another: say which.
## Tools
- `get_studio`: engine plus the nextjs or astro adapter, patterns (driver module, static fallbacks), layout families, motion recipes
- `get_guidelines`: topic: build, plus the recipe rule ids
- `get_build_prompt`: a ready prompt with the rules and recipes for the chosen styles, if you want one to hand to another agent or builder
- `review_design`: after each section
- `check_contrast`: any new color pair
## Output template
```markdown
# Build notes
Stack and why. Deviations from tokens. Known gaps. How to run it.
```
## Gates
Rules to satisfy: `perf-core-first`, `a11y-native-first`, `a11y-semantic-structure`, `a11y-bypass-blocks`, `a11y-focus-visible`, `craft-relative-units-text` (read them with get_guidelines or rules/*.md).
- [ ] No raw hex values in components.
- [ ] Content and navigation work with JavaScript disabled.
- [ ] review_design shows no blocker failures.
## Done when
- The page runs locally, matches the tokens and passes the blocker review.
## Pitfalls
- Building in one giant pass without reviewing.
- Adding ARIA to compensate for non-semantic markup.
