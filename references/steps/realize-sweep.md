# Step: Look at every state and keep a papercut log (`realize-sweep`, stage realize)
**Goal:** Capture every state of every section and breakpoint, review the build's own trail for surprises, and record small issues in a log that carries into the next round.
**Your role:** Look at every state of the page once, on purpose, and keep a log of the small issues so they are fixed together instead of one reaction at a time.
**Inputs:** built-site, subtract-log  
**Output artifact:** state-sweep, papercut-log -> `design/06-realize/state-sweep.md`
## Procedure
1. Review the build's own trail first: the commit list, the build notes, the changelog of deviations, and any screenshots or logs the build produced. Look for anything you did not expect (a component you did not plan, a dependency, a new section, a changed token). A surprise means the brief or the direction was not understood: go back to the decision and the brief before polishing.
2. List every state the page can be in: each section; hover, focus, active and disabled controls; menus and dialogs opened; forms empty, filled, with an error, and submitted; loading and empty content; reduced motion; no JavaScript; dark scheme if present; widths 320, 390, 768, 1440; text at 200%.
3. Capture a screenshot of each state, grouped by section, and note any bug met on the way (broken link, overflow, wrong state, console error). Use a browser tool or Playwright; a state you cannot reach is listed as not seen, not skipped silently.
4. Skim the set once for surprises (not details): are these the screens you expected? Then go through it marking small, obvious fixes and fix them at once.
5. Anything small that is not obvious, or that touches the design (spacing rhythm, label wording, a colour that is a little off), goes in the papercut log instead of a spot fix. Spot fixes made one at a time drift the page away from its constraints.
6. Shared chrome changed (header, footer, navigation, a theme applied site-wide)? It touches every page and moves the done bar from one file to many (in a test, eleven edits outside the homepage): confirm with the owner up front that the done bar may touch it. Also audit one inner page, and list the accessibility problems that were already in the shared chrome (focus ring, small targets, controls dead without JavaScript) separately from the ones this work introduced, so old debts are visible and not mistaken for regressions. Compare with the baseline audit.
7. Detail pass (what separates agency-grade from cheap): no default-looking controls (style native date, select and file inputs; buttons with a clear primary, secondary and text hierarchy), small labels set deliberately (small caps or tracked caps, numerals for steps), hairline rules and frames that give structure, real images framed or cropped on purpose, illustration with fills and layers rather than single thin strokes, hover and focus states designed rather than inherited, and secondary text large enough to hold its own beside the display type. Compare each section with its anchor's section crop (get_section) and list the details the anchor has that the page lacks. In a real run the owner scored a page with restored richness 7/10 and said "still feels cheap, lack of details". [Our take]
8. Conversion pass: the capture named in the brief is in the first screen, repeated after each major section and in a closing band; the value exchange sits next to each form; the success and error states are honest; any proof is real (unconfirmed counts stay marked). [Our take]
9. Density check: count words and links per screen at 1440 and 390. More than about 150 words or 30 links in one screen is overloaded: move, group or cut, and say what you moved. [Our take]
10. Choose the crux surfaces named in direction-decision.md (the one or two the page stands or falls on, for example the hero and the booking path) and give them a longer pass: other variants, other copy, the details.
## Tools
- `review_design`: after the fixes
- `get_design_brief`: to compare a captured reference's states with yours, when a reference was used
## Output template
```markdown
# State sweep
## Surprises in the build's trail (and what they mean for the brief)
## States seen (section, state, width, screenshot file) and states not seen
## Bugs met on the way
## Fixed at once
## Crux surfaces: what was polished
## Papercut log (kept in design/papercuts.md; each: where, what, why it matters, date)
```
## Gates
- [ ] Every state in the list has a screenshot or is named as not seen.
- [ ] Bugs found on the way are listed, not only design notes.
- [ ] Small non-obvious issues are in design/papercuts.md, not fixed ad hoc.
- [ ] The crux surfaces are named and were polished.
## Done when
- The state sweep exists with screenshots, bugs and the papercut log; surprises were resolved or sent back to the brief.
## Pitfalls
- Checking only the default state at desktop width.
- Fixing each papercut the moment it is seen and drifting from the tokens.
- Skipping the trail review and polishing a feature nobody planned.
