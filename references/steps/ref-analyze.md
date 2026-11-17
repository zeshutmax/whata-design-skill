# Step: Analyze references (`ref-analyze`, stage references)
**Goal:** Annotate what exactly works in each reference: structure, type, color, motion, copy.
**Your role:** Find out exactly what works in the strongest references so you can reuse the idea, not the surface.
**Inputs:** reference-board  
**Output artifact:** reference-notes -> `design/03-references/reference-notes.md`
## Procedure
1. Pick the 6 to 10 most useful references. For each call get_site and read its style record, palette roles, fonts, tags and audit.
2. Get the numbers before the impressions: get_craft with the slugs gives each site's scale contrast (headline over body), type scale step, section whitespace in body units, lead-object share of the first screen and motion timing, and the library's quartiles. Write them in the notes; they are what makes a page feel agency-grade, and compare_to_library checks your concepts against them later.
3. Annotate: page skeleton and section order, hero type, navigation, type scale and pairing, color roles and contrast, motion (what, when, how long), copy approach (headline structure, proof, CTA wording).
4. Write a 'why it works' sentence for each notable move and the reusable principle behind it. For motion use phases: trigger, start, move, settle. [Craft]
5. Use compare for two to four references that look alike on the surface to find what actually differs.
## Tools
- `get_site`: style record, palette roles, fonts, audit summary and failing rules
- `get_craft`: slugs; scale contrast, type step, whitespace, lead-object share and motion timing per site, with the library quartiles
- `get_design_system`: format markdown for the DESIGN.md of a reference
- `get_design_brief`: tokens, components, section map, image files and audit failures of a reference: enough to study or rebuild its structure without a screenshot
- `compare`: slugs of 2 to 4 references
## Output template
```markdown
# Reference notes
## [slug]
- Skeleton and section order:
- Hero and navigation:
- Type and color:
- Motion (trigger, start, move, settle):
- Copy approach:
- Why it works:
- Reusable principle:
- Do not copy (audit failures):
```
## Gates
Rules to satisfy: `distinct-customize-library-defaults` (read them with get_guidelines or rules/*.md).
- [ ] Every note states a reusable principle, not a surface feature.
- [ ] Audit failures are named, not ignored.
## Done when
- 6 to 10 references annotated with a principle each.
## Pitfalls
- Describing the look instead of explaining why it works.
- Treating a reference's accessibility failures as part of its style.
