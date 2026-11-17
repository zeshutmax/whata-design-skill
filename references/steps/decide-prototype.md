# Step: Prototype the strongest candidates (`decide-prototype`, stage decide)
**Goal:** Make a realistic clickable or coded version of the best one or two directions, with real content.
**Your role:** Make the strongest one or two directions real enough to test: full page skeleton, real content, working interaction.
**Inputs:** hero-concepts, critique-notes, headline-drafts, structure-wireframes  
**Output artifact:** prototype -> `design/05-decide/prototype/`
## Procedure
1. Build a coded prototype of the top one or two directions: all sections from the structure step, real copy, tokens as CSS custom properties, the recipe safeguards. Semantic HTML first; effects layered on top. [Craft: progressive enhancement]
2. Make it navigable and responsive (320 to 1920 px). Use real images or honest placeholders (marked).
3. Run review_design on the prototype and fix blocker failures before anyone sees it.
4. Only after the owner's pick: no prototype is built, and nothing is written in the site tree, until direction-decision.md records `Owner pick:` (protocol 4). A prototype of a direction the owner has not picked is wasted work and, in the site tree, uncommitted clutter.
5. Where it lives (build once): the prototype is the first draft of the build, so build it where the site will live (the project root or the source tree), not in a throwaway folder. Keep design/05-decide/prototype/ for notes.md (what is placeholder, which recipe steps were applied, known issues), the screenshots at 390 and 1440 and a one-line pointer to the site files. A second prototype of another direction, if you build one, lives inside that folder and is thrown away after the decision. realize-build then finishes the prototype instead of rebuilding it. [Our take]
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- structure-wireframes is replaced by the skeleton row of direction-matrix.md (the section order) and the Content inventory of brief-draft.md (what each section must say). Place every must-have block of the inventory and put the primary action in the first screen.
- In the sprint the prototype is the Day 4 deliverable and the first draft of the site: see `Where it lives` above. Day 5 tests it; realize-build and realize-qa follow after Day 5.
## Tools
- `review_design`: path to the prototype
- `get_recipe`: for the direction's styles
## Output template
```markdown
# Prototype
notes.md (what is placeholder, which recipe steps were applied, known issues, and where the prototype's files are), screenshots at 390 and 1440, and either the prototype itself (index.html + assets) or a pointer to the site files it was built in.
```
## Gates
Rules to satisfy: `perf-core-first`, `a11y-semantic-structure`, `a11y-name-role-value`, `copy-no-placeholder-text` (read them with get_guidelines or rules/*.md).
- [ ] The page content works with JavaScript disabled.
- [ ] review_design shows no blocker failures.
## Done when
- A prototype exists for each remaining direction with a clean blocker review.
## Pitfalls
- Prototyping all three directions in full (waste).
- Static screenshots only.
