# Step: Remove what the build does not need (`realize-subtract`, stage realize)
**Goal:** Take out the extra copy, lines, icons, metadata and decoration that building added, until every element earns its place.
**Your role:** Remove what the build does not need. Agents and first drafts add; this step only takes away.
**Inputs:** built-site, design-tokens  
**Output artifact:** subtract-log -> `design/06-realize/subtract-log.md`
## Procedure
1. List every element in each section of the built page at desktop and mobile: headings, lines of copy, icons, dividers, badges, labels, metadata, decorative shapes, hover effects, animations.
2. For each element ask: what job does it do for the visitor or the goal, and what is lost if it goes? Remove it if the answer is nothing, if another element already does the job, or if it only fills space. Prefer removing to restyling.
3. Watch for what builders add by habit: a second line of explanation under a clear heading, an icon on every list item, a divider between sections that already differ, metadata (dates, counts, tags) nobody asked for, a third button next to the primary action, repeated claims in different words.
4. Keep what the brief, the recipe or the quality bar requires (skip link, labels, alt text, legal lines), even if it looks like clutter. Removing a required element is a regression.
5. Never subtract the style. The lead object, the niche cue (motifs, pattern, palette), the atmosphere (backdrop, glow, texture) and the display type are what make the page look designed; they are not clutter. Remove habit-added extras and inconsistencies (a second style in one role, colliding parts, duplicate explanations), not richness. After subtracting, run compare_to_library and put the page beside its previous round: if the lead object shrank or the motifs went, put them back. In a real run a subtract-and-simplify round removed the florals, pattern and glow, and the owner's score fell from 6.5 to 5: "too simple, no style". [Our take]
6. Write the subtract log: each removal with a reason, and each element kept on the edge with the job it does. Re-run review_design: the removals must not have introduced failures.
## Tools
- `review_design`: after the removals, desktop and mobile
## Output template
```markdown
# Subtract log
| Section | Element | Job it did | Verdict (removed / kept) | Reason |
|---|---|---|---|---|
## Kept on the edge (what job it does)
## Review after removals (blockers, majors)
```
## Gates
Rules to satisfy: `distinct-swap-test` (read them with get_guidelines or rules/*.md).
- [ ] Every section was walked element by element, at both sizes.
- [ ] At least one thing was removed from each section, or the log says why nothing could go.
- [ ] No required element (skip link, label, alt text, legal line) was removed.
- [ ] review_design shows no new failures.
## Done when
- The subtract log exists and the page was re-reviewed after the removals.
## Pitfalls
- Restyling an unneeded element instead of removing it.
- Removing something the quality bar requires.
- Doing this only on the hero.
