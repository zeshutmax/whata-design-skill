# Step: Check inclusion and accessibility early (`decide-inclusive`, stage decide)
**Goal:** Check the leading directions for contrast, motion, readability and who might be excluded, before investing in detail.
**Your role:** Check, before investing in detail, whether the leading directions can be used by people with different abilities and devices.
**Inputs:** hero-concepts, type-color-studies, motion-notes  
**Output artifact:** inclusion-check -> `design/05-decide/inclusion-check.md`
## Procedure
1. Run review_design on the top two heroes and read the blocker and major findings.
2. Do the manual checks in a real browser: Tab through the page (visible focus, logical order, nothing hidden behind sticky elements); zoom text to 200%; view at 320 px wide; turn on reduced motion; check forced colors if you can; check color contrast of every state. [Standard + Craft]
3. List who might be excluded (low vision, motor, cognitive load, screen reader, slow network) and what the design does for them.
4. Fix what is cheap now; discard a direction whose core idea cannot pass (for example text that must sit on a busy video with no scrim).
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- type-color-studies is replaced by the draft tokens in direction-matrix.md; motion-notes by the motion and reduced-motion variant written in each hero's notes.md. Check the leading hero (and the runner-up if time allows), not all three.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- type-color-studies is replaced by the draft tokens in direction-matrix.md; motion-notes by the motion and reduced-motion variant written in each hero's notes.md. Check the leading hero and the runner-up (they are the two the prototype step may build).
## Tools
- `review_design`: path to each hero concept
- `check_contrast`: any pair you have not yet verified
## Output template
```markdown
# Inclusion and accessibility check
| Check | A | B | C |
|---|---|---|---|
| Keyboard path and visible focus | | | |
| Text at 200% | | | |
| 320 px reflow | | | |
| Reduced motion | | | |
| Contrast (text, UI, focus) | | | |
| Forced colors | | | |
## Who could be excluded and how the design responds
## Decisions (fix now / discard)
```
## Gates
Rules to satisfy: `a11y-keyboard`, `a11y-focus-visible`, `a11y-reflow`, `a11y-resize-text`, `a11y-reduced-motion`, `a11y-contrast-text`, `a11y-target-size` (read them with get_guidelines or rules/*.md).
- [ ] Every row is filled with a result, not 'ok'.
- [ ] Blocker failures are fixed or the direction is discarded.
## Done when
- The table is complete and no remaining direction has a blocker failure.
## Pitfalls
- Relying on automated results alone: automated tools miss errors.
