# Step: Check accessibility, performance and SEO (`realize-qa`, stage realize)
**Goal:** Test contrast (WCAG 2.2 AA: 4.5:1 for normal text, 3:1 for large), keyboard use, reduced-motion behavior, Core Web Vitals (LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1 at the 75th percentile), metadata and responsiveness.
**Your role:** Prove the build against the Quality Bar. Automated results are a baseline, not a verdict.
**Inputs:** built-site, success-criteria  
**Output artifact:** qa-report -> `design/06-realize/qa-report.md`
## Procedure
1. Measure a production build behind compression: a static export served by a plain local server sends files uncompressed, and on a throttled phone that read as a 5 to 6 s first paint for a page that paints in 1.4 s with gzip. Serve it with `pnpm --silent --filter @whata/audit serve <out dir> [port]` (gzip, like a CDN), or measure the deployed preview.
2. Critic pass (get_critic_brief): build for production, shoot desktop, mobile, reduced motion and keyboard states, and give a fresh subagent the critic brief and the screenshots only. Every category (Design, Usability, Creativity, Content) must reach 8 with evidence; its fix list is the next pass, and its one-line reading of the idea must match the concept. At least two passes; a new critic each time. Finish with 'remove one accessory'. Record the scores in design/06-realize/critic.md as a model's scores.
3. Run review_design (or the audit CLI) on desktop and mobile; list every failure and every rule that needs a person. A rule the audit did not evaluate is not a pass: the audit lists the rules it skipped, and '0 failures' only means none of the rules it did check failed. Serve the build over http (not file://) so stylesheets load.
4. State and keyboard checks are owned by realize-sweep when it ran (states, widths, 200% text, reduced motion, no-JS): link to its state-sweep.md instead of repeating them, and do here only the checks the sweep does not cover (screen reader or accessibility tree, forced colours, performance, the rest of this list).
5. Do the manual list. Owned by realize-sweep when it ran, so link and do not repeat: keyboard-only pass, text at 200%, 320 px reflow, reduced motion, dark mode, no-JS load. Owned here: a screen reader smoke test (VoiceOver: headings, landmarks, links, forms, dialogs; if you cannot run a screen reader, read the accessibility tree with Playwright's `page.accessibility.snapshot()` or `locator.ariaSnapshot()` for headings, landmarks, names, roles and states, and record the result as `accessibility tree only, not a screen reader test`: it is not a substitute and the owner should have someone run VoiceOver or NVDA); zoom 400%; text spacing override; forced colors; slow network. When the sweep did not run, do the owned-by-sweep checks here as well. [Standard + Craft]
6. Give the audit an absolute path for a local file (in the pilot a relative path was resolved from the audit package folder, not from the working folder, the page did not load, and fake findings were printed); if the report says the page failed to load, its findings are not about your page: fix the path and run again.
7. Reflow and text stress: if the audit lists a 320 px or 200% text overflow (a sideways scroll at 320 px, at 200% text size or with text spacing) as `check` ("needs a person"), do not read it as a pass: a measured overflow is a failure of `a11y-reflow`. Fix it (grid `minmax(0, 1fr)`, `overflow-wrap`, wrapping flex rows) or justify the exception in writing with the measured width, then run the audit again. [Our take]
8. Reflow culprit: the audit names the first element that overflows, not the cause, and the named element can change while the overflow width stays the same. Find the cause by bisecting: hide sections one at a time until the overflow drops, then hide inside that section. Typical culprits are a long word in a footer paragraph, a heading in a wide display face, a table and a field row.
9. Audit a production build when one is possible: the dev server's overlay or indicator can widen the page at 200% text and show up as a false overflow. If the build cannot run (no disk, no secrets), say so, run typecheck, lint and a dev-server render, name any dev-only indicator as a known false source, and mark performance `unmeasured`.
10. Gaps the audit may leave: read the audit's `not evaluated` list. If it lists `ux-primary-cta-above-fold` (a major rule), check the first viewport by screenshot at 390x844 and 1440x900 and confirm the primary action is fully visible without scrolling at both: a page can pass every automated check and still have its button below the fold on a phone. Do the same by hand for any of these the audit lists as not evaluated: `craft-body-size-min` (computed font size of running text, at 320 and 1280 px; 14 px is our review threshold, not a standard) and `craft-breakpoints-content-based` (sweep the width from 320 to 1920 px in steps of about 40 px and look for horizontal scroll, overlaps and clipped text). Record each as a manual check with the method.
11. `--verified` entries: say in `by` whether a person or a model verified the rule (for example `model: <name>` or `person: <name>`). A model's check is a model review, not a person's; rules that need real people (screen reader, test with people) cannot honestly be verified this way and stay open.
12. Lead element and the page below it: confirm the lead element is in the first viewport at both sizes, and describe in two or three sentences what the page looks like below the hero. The lead element must also recur or be answered lower on the page (a second moment), and the sections below the hero must differ in structure from each other (not a plain run of headings and paragraphs, not the same card repeated). If the page below the hero is a plain sequence, say so and fix it or record it as an open issue. Automated checks cannot see this. [Our take]
13. Check performance (lab Web Vitals: LCP 2.5 s, CLS 0.1; INP needs field data), page weight, fonts, images.
14. Frequency and absolute words ('every week', 'daily', 'always', 'never', 'all') are claims too: check each against the data (post dates, release logs, order counts) and use the measured wording ('most weeks', 'about 1.5 a week').
15. Check copy against the copy rules (specific, plain, consistent) and distinctiveness (swap test, defaults justified).
16. Inherited or new: before you change anything, save an audit of the current page (`pnpm --silent --filter @whata/audit cli <url> --out design/00-baseline/audit.json`), then run review_design with `baseline` set to that file so the report splits failures into new, inherited and fixed. Inherited failures in shared chrome (header, footer, global tokens) are listed separately with whether need-constraints allows you to change them; they are not passes, and new failures are yours to fix.
17. Type census and header: run `pnpm --silent --filter @whata/audit cli types <url>` (one style per role, peers in a list alike, first-screen counts) and `cli widths <url>` (now 320, 390, 768, 1024, 1280, 1440 and 320 at 200% text, with overlapping text caught). Look at screenshots of the header at 1440, 1280, 1100, 1024 and 390: shared chrome that passes every rule can still collide between breakpoints. When the chrome is in scope and broken, the kit header (get_base) is the replacement.
18. Content coverage (when need-statement's scope keeps any content): run `pnpm --silent --filter @whata/audit cli coverage <old url> <new url>`. Every block it lists as missing or partly kept must be explained by content-map.md (moved, reworked in scope, or dropped by the owner); with `SEO: keep`, every SEO field must be `same` and no internal link lost. Paste the summary line into the QA report.
19. Count the unconfirmed facts still on the page (the `.assumed` marks) and list them in the QA report; they are open issues, not passes.
20. Fix blockers and majors; list the rest with owners.
21. Say honestly what the result is. With no owner sign-off, no user test and no screen-reader run, the status is `built, audited, not approved`, with the list of what was not done.
## Sections track (default)
Applies only when the owner and you chose the sections track. In full, sprint and lean tracks ignore this section.
- success-criteria is replaced by the Success section of the brief.
- Check the design system held: `pnpm --silent --filter @whata/audit cli types <url>` reports no mixed role group (a display-size closing line is the one allowed exception), and the page uses one section ground, at most two corner radii for controls and media, and only the primary and secondary buttons. Fix through tokens or roles.css, never per section.
- The audits are checks on a finished look, not a source of it. Fix every blocker. Where a fix would change a section's pinned design, prefer the accessible version and record the deviation in that section's spec under 'Accessibility changes from the source'; where the design is the source's and the rule is a heuristic (small text inside decorative product UI, a nested panel), record it as justified with the reason.
- Close with the owner's score (record_taste type score, round = the section ids). Below the previous round: compare section by section with the sources before changing anything; never add rules to rescue a section.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- realize-qa is not optional in the sprint: the prototype had only a blocker review before the Day 5 test. Run the whole step on the finished build, and report the status honestly (`built, audited, not approved` with no owner and no test). Day 5's `UNTESTED` stays in the report.
## Tools
- `review_design`: the built page; use an absolute file path or an http URL; desktop and mobile
- `get_critic_brief`: the brief and rubric for a fresh critic subagent; 8 or above in every category
## Output template
```markdown
# QA report
- Automated: blockers [n], majors [n], needs a person [n]
## Manual checks (result per check; method and who: person or model)
## Lead element and below the hero (above the fold at 390x844 and 1440x900? second moment? do the sections differ?)
## Content coverage (scope, coverage %, unexplained missing blocks, SEO fields changed, links lost)
## Inherited failures (shared chrome; may change? yes / no)
## Unconfirmed facts still on the page
## Status (built, audited, not approved | approved by [name, date])
## Performance (lab)
## Copy and distinctiveness
## Open issues (severity, owner)
```
## Gates
Rules to satisfy: `a11y-test-manually`, `a11y-test-with-people`, `perf-lcp`, `perf-cls`, `distinct-swap-test` (read them with get_guidelines or rules/*.md).
- [ ] Zero blocker failures remain.
- [ ] Every manual check has a recorded result and says whether a person or a model did it.
- [ ] The primary action is checked in the first viewport at 390x844 and 1440x900 (by screenshot when the audit does not evaluate it).
- [ ] The lead element is above the fold and recurs lower; the sections below the hero differ in structure.
## Done when
- No blocker failures; majors fixed or accepted by the owner in writing.
## Pitfalls
- Stopping at a green automated run.
- Reading the audit's `0 failures` when the page never loaded or the rule was not evaluated.
- Calling a model's check `verified by hand` without saying a model did it.
- A strong hero over a plain typographic sequence.
