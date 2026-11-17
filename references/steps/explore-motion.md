# Step: Explore motion and interaction (`explore-motion`, stage explore)
**Goal:** Decide where motion earns its place and which triggers and techniques fit the direction.
**Your role:** Decide where motion earns its place. Motion supports meaning; it is not decoration for its own sake.
**Inputs:** direction-matrix  
**Output artifact:** motion-notes -> `design/04-explore/motion-notes.md`
## Procedure
1. List candidate motions with the purpose of each (orient, give feedback, show relationship, express brand). Drop any without a purpose.
2. Motion follows the concept's motion verb (get_studio motion): one micro-interaction treatment per role (primary actions, navigation, work or product images) chosen from the verb, the signature moment, the continuity between states (intro, page to page), and an idle state that keeps the concept breathing at rest. Primary targets answer in the verb, not with a colour swap alone. One clock, one easing family; big things move slower than small things. [Our take, from the awwwards method]
3. Pick one lead motion idea for the direction and at most two supporting ones. Name triggers (scroll, hover, click, load) and techniques. [Our take: one lead idea beats five effects]
4. For each, define the reduced-motion variant (replace large movement with fades; keep what it conveyed) and the pause control for anything that starts automatically. [Standard]
5. Set budgets: animate transform and opacity only; no layout shift; no long main-thread tasks. [Craft]
## Tools
- `get_recipe`: motion-related tags: scroll-triggered, parallax, webgl, marquee, hero-video
## Output template
```markdown
# Motion notes
| Motion | Purpose | Trigger | Technique | Duration/easing | Reduced-motion variant | Pause control |
|---|---|---|---|---|---|---|
```
## Gates
Rules to satisfy: `a11y-reduced-motion`, `a11y-pause-stop-hide`, `ux-minimal-motion`, `craft-motion-duration-range`, `distinct-motion-authored`, `perf-inp` (read them with get_guidelines or rules/*.md).
- [ ] Every motion has a purpose, a reduced-motion variant and (if automatic) a pause control.
## Done when
- One lead motion idea and at most two supporting ones, each fully specified.
## Pitfalls
- Motion on every element.
- No reduced-motion variant.
