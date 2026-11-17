# Step: Design the homepage in full (`realize-design`, stage realize)
**Goal:** Design every section, state and breakpoint with real content.
**Your role:** Design the full homepage with real content: every section, state and breakpoint.
**Inputs:** direction-decision, design-tokens, structure-wireframes, content-inventory, headline-drafts  
**Output artifact:** homepage-design -> `design/06-realize/homepage-design.md`
## Procedure
1. Compose all sections from the structure step with the final copy and tokens. Check each section at 320, 390, 768, 1024, 1440 and 1920 px.
2. Design the states: hover, focus, active, disabled, loading, empty, error. Focus is visible and distinct. [Standard]
3. Check hierarchy (one h1, logical headings), grouping by proximity, spacing from the scale, alignment, image dimensions reserved, icon family consistent. [Craft]
4. Check rhythm: sections must not all share the same template (centered title, three cards). [Our take]
## Tools
- `get_recipe`: for the direction's styles
- `review_design`: after each major change
## Output template
```markdown
# Homepage design
Section list with content, tokens used and states.
Screenshots at 390 and 1440.
Known deviations from the tokens and why.
```
## Gates
Rules to satisfy: `craft-group-by-proximity`, `craft-image-dimensions-reserved`, `craft-icons-one-family`, `distinct-section-rhythm-varied`, `distinct-no-identical-card-grid`, `a11y-headings-labels`, `copy-no-placeholder-text` (read them with get_guidelines or rules/*.md).
- [ ] All content is real or marked as draft.
- [ ] States are designed, not only the default.
## Done when
- Every section exists at all breakpoints with states.
## Pitfalls
- Only designing at desktop width.
- Identical card grids repeated down the page.
