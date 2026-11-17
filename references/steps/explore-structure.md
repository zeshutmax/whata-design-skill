# Step: Explore structure (`explore-structure`, stage explore)
**Goal:** Choose a page skeleton and sketch the section order for each direction.
**Your role:** Decide how the page is built: skeleton, section order and navigation, from the content inventory.
**Inputs:** brief, content-inventory, direction-matrix  
**Output artifact:** structure-wireframes -> `design/04-explore/structure-wireframes.md`
## Procedure
1. For each direction choose a page skeleton (taxonomy layout/macrostructure) and list the sections in order using section types (navbar, hero, logos, features, bento, works, reviews, pricing, faq, cta, footer...).
2. Map every must-have content block from the inventory to a section. Put the primary action in the first screen and repeat it where natural. [Evidence: most attention goes to the top of the page]
3. Choose navigation: visible primary links on desktop; on mobile four or fewer links visible, otherwise a disclosure menu. Unusual navigation needs a written reason and the recipe's safeguards. [Evidence]
4. Draw a low-fidelity wireframe (text or ASCII is enough) of each direction, with the code order equal to the reading order.
5. A list that is the content (the visitor's possible situations, a services list) is one choice, not many (`a11y-coga-limit-choices-per-screen` counts competing choices): keep it as one labelled list that is the dominant feature, group a long one under headings, and keep every other action visibly secondary. Record the call (the tensions in `rules/build.md`). An urgent route (recipe `urgent-help-route`) is placed first in reading order and must not push the primary action out of the first screen. [Our take]
## Tools
- `search_sites`: allOf: [skeleton slug] to see real examples of the chosen skeleton
- `get_recipe`: for unusual navigation or layout tags
## Output template
```markdown
# Structure and wireframes
## Direction A: skeleton [slug]
Sections in order: navbar > hero > ...
Navigation:
Where the primary action appears:
Wireframe (indented text block, four spaces):

```
## Gates
Rules to satisfy: `ux-primary-cta-above-fold`, `ux-visible-navigation`, `a11y-meaningful-sequence`, `a11y-multiple-ways`, `craft-breakpoints-content-based` (read them with get_guidelines or rules/*.md).
- [ ] Every must-have content block is placed.
- [ ] The primary action is in the first screen.
- [ ] Code order equals reading order in the wireframe.
## Done when
- Each direction has a skeleton, section order, navigation choice and wireframe.
## Pitfalls
- Hiding navigation on desktop without need.
- Layouts that only work if the visual order differs from the source order.
