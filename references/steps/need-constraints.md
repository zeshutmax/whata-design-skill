# Step: List the constraints (`need-constraints`, stage need)
**Goal:** Capture brand assets, budget, deadline, platform, content, legal and accessibility limits.
**Your role:** Record everything that limits the design so later steps treat limits as inputs, not surprises.
**Inputs:** need-statement  
**Output artifact:** constraints -> `design/01-need/constraints.md`
## Procedure
1. Ask for or find: brand assets (logo, colors, fonts, voice), existing site and its analytics, stack and hosting, CMS, deadline and budget, content that exists, legal needs (cookie consent, claims, regulated language), languages.
2. Set defaults unless the user says otherwise and write them down: accessibility target WCAG 2.2 Level AA [Standard]; Core Web Vitals targets LCP at most 2.5 s, INP at most 200 ms, CLS at most 0.1 at the 75th percentile [Standard]; support the current evergreen browsers and common mobile sizes (320 to 1920 px wide).
3. List explicit 'must not' items (words, colors, competitors' looks, technologies).
4. Shared chrome: list the shared components that render on this page (header, footer, navigation, cookie banner, region or language switcher, global tokens and base styles) and ask whether you may change them. The homepage's done bar (zero blockers) often cannot be met without them: in a real run the failures were a low-contrast button in the footer, 12 to 14 px footer text, an icon-only switcher with no name and a light input border token, all shared. Record the answer as `Shared chrome: may change [list] / must not change [list]`, and in realize-qa report their failures as inherited, not new.
## Ask the owner (only what you cannot default)
- Brand assets I must use? (a) the logo, colours and fonts on the current site (recommended) (b) new or different ones: send them.
- Stack and deadline? (a) the current project's stack, no fixed deadline (recommended) (b) another stack or a date: say which.
- Anything the page must not say or look like? (a) nothing beyond the brief's anti-goals (recommended) (b) yes: list it.
- May I change the shared header, footer and global styles to fix problems on this page? (a) yes, and I audit one inner page too (recommended) (b) no, this page only.
## Output template
```markdown
# Constraints
- Brand assets:
- Stack / platform / hosting:
- Deadline and budget:
- Content available:
- Legal / compliance:
- Languages:
- Accessibility target: WCAG 2.2 AA (default)
- Performance targets: LCP <= 2.5 s, INP <= 200 ms, CLS <= 0.1 (default)
- Must not:
- Shared chrome (header, footer, nav, switchers, global tokens): may change [list] / must not change [list]
```
## Gates
Rules to satisfy: `perf-lcp`, `perf-inp`, `perf-cls` (read them with get_guidelines or rules/*.md).
- [ ] Accessibility and performance targets are written down, even if they are the defaults.
## Done when
- Brand, stack, time, content, legal, accessibility, performance and shared-chrome lines are all present.
## Pitfalls
- Leaving accessibility and performance unstated so they become optional.
