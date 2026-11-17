# Step: Frame three directions (`explore-directions`, stage explore)
**Goal:** Combine art style, mood, typography and color into three distinct directions with a one-line north star each.
**Your role:** Converge the sketches into three genuinely different directions the owner could choose between.
**Inputs:** brief, design-principles, reference-board, idea-sketches  
**Output artifact:** direction-matrix -> `design/04-explore/direction-matrix.md`
## Procedure
1. The option gate (protocol 4) comes before the owner sees anything: draft the three with propose_directions and show them only as render_sheet sheets; each concept passes review_design with zero blockers and none of `distinct-hero-not-template`, `distinct-no-decorative-glow`, `distinct-no-accent-word-headline`, `distinct-eyebrow-restraint`; one fresh critic scores each from its screenshots only (get_critic_brief), recorded as a model's scores beside the sheet; and the owner's 1 to 10 score for every option is recorded with record_taste (type score, round `gate 2: <direction>`). Hand-made mock-ups never go to the owner, whata.design's own pages included. [Our take]
2. Show the directions to an owner who is not at your keyboard as one side-by-side sheet per size (desktop and mobile, the three concepts in a row, each labelled with its name and one-line north star) saved as image files, plus the north-star lines in your message. That worked better than links or prose.
3. Cluster the sketches and pick three directions that differ in at least two of: art-style family, mood, type class (serif, grotesque, mono, display), palette mood, page skeleton.
4. Concept first (studio method, get_studio concepts): write three concepts from different territories (the subject's name or story, its material, its place or culture, a metaphor for how it works, a formal or typographic system). Each has one sentence, its anchor (the specific fact about this subject it depends on), the signature moment, the emotion of the first 3 seconds, the motion verb and the frame people would screenshot; score originality, fit, feasibility and portability (could it move to another brand? lower is better). Each direction below is one concept dressed in an art direction from the library; a library style alone is not a direction. [Our take, from the awwwards method]
5. Span a range of ambition: one **safe** direction (closest to the owner's taste anchors from the reference board), one **stretch** (a visibly stronger look taken from the library's most distinctive sites), one **wildcard** (an unexpected combination). Anchor each on named library sites with one stated take per site ("butter-video's type scale with makingsoftware-com's ledger"). propose_directions drafts this from the brief and the owner's taste slugs and checks the spread; it is a starting point, not the answer. Three variations of one idea fail the gate.
6. For each, write a one-line north star ('Calm editorial finance with serif display type'), the taxonomy tags (art style up to 3, mood up to 2), the page skeleton, hero type, and the reference sites it draws on.
7. For each direction call get_recipe for its art styles (at most 3 tags per call, canonical slugs from list_tags such as `hand-drawn`, not invented ones such as `illustration-hand-drawn`: with 8 tags a pilot got over 60 KB of JSON, and unknown tags come back with empty rule lists) to learn upfront which Quality Bar rules it collides with and how to keep the look and pass the rules. Write those risks in the matrix. [Our take: surface accessibility risk before falling in love with a direction]
8. Check the three against the swap test and the niche's default look from the landscape audit: at least one direction must clearly depart from the default.
9. Name each direction's niche cue: what in the look says, in one second, which kind of site this is (a motif, a palette, a shape, a material). Avoiding the niche's clichés (blush, florals, script for weddings) is not the same as dropping its legitimate vocabulary: in a real run an elegant editorial direction with a timeline said nothing about weddings, and the owner asked for "more pink, patterns and graphics". Draw the cue from the niche references on the board. [Our take]
10. Pick each direction's lead element from the catalogue of recurring moves where one fits (get_moves: oversized type plus object, pinned scene, chaptered story, data as image, product showcase, 3D hero ...): each move lists the library sites that show it, so study them with get_section before you draw. One lead move per direction.
11. Name each direction's lead element: the one thing (a hero object, a layout idea, a type move, an interaction) that the niche's default page does not have and that carries the brief's message. A new skeleton is not required, but a lead element is. Read the slop versions in `trends.md` and the rules in `rules/distinct.md` (get_guidelines distinct) before you fix the three directions, so none of them is the probable default (for example cream and terracotta, a split hero with a product card, a three-column icon grid). Copy that is specific on a generic skeleton still reads as generic. [Our take]
12. A lead element above the fold is not enough. Write down where the lead element recurs or is answered lower on the page (a second moment: the same object in a new state, the same type move as a section break, the same interaction as the close), and make the sections below the hero differ in structure from each other (not a run of heading plus paragraphs, not the same card repeated). A page with a strong hero and a plain typographic sequence below it is still the default page. [Our take]
13. No photography exists (physical goods with no photos yet: a studio, a shop, a food or craft business; or a service with no photographs, or none you may use: advice, a clinic, a helpline, a firm)? The imagery rules were written with software in mind, which has an interface to show. Choose one of three, in this order, and write it in the matrix (graphics drawn in code from the page's real content, such as a data graph or a process diagram in the tokens, can serve any of them; see protocol 6 and plan_graphics): (1) the offer itself is the live object: price, seats, dates, sizes or a booking interactive built from real HTML controls with real states and real numbers (it works only when the offer has state to show: seats, slots, sizes, bundles); (2) type as image: a measurement, a date, a price or a name set large as the visual, as real text, not as an image of text; (3) leave imagery out and mark the gap in the matrix and in OPEN-QUESTIONS.md, because real photographs have to be commissioned before launch. A pieces-only catalogue has no state to show: say that, and treat the missing photographs as a launch risk. Illustrations assembled from shapes in code (a drawn bowl, a cross-section) stay out (`distinct-real-imagery-and-icons`). For a service the live object is something it really has state for (opening hours, free slots, a waiting time, a self-check or calculator), and type as image can be the fact that answers the first question (a phone number and its hours, a fee, "free and independent"); photographs of people need their consent. Which recipe steps apply to a service: `np-offer-live-object` (when there is state to show), `np-live-object-accessible` (if you build one), `np-type-as-image`, `np-mark-the-gap` and `np-commission-later`; `np-menu-and-run-sheet` only when the service has rows to list (a fee table, opening hours, the steps of a process); `np-pieces-only-limit` is for goods. Recipe: `no-photography-physical-goods`. [Our take]
14. Public service, advice or crisis audience (people who may be in danger, in debt, ill or facing a deadline)? Decide before you design the hero what the urgent route is and where it sits: read the recipe `urgent-help-route` (what goes first, a phone number as a `tel:` link with hours and an out-of-hours route, the emergency-services boundary stated once, not relying on red alone, and how the band stacks with the primary action at 390x844) and write the choice in the matrix. If the page also takes personal data in a form, read `form-no-backend-and-privacy`. An audience with these flags usually also means the COGA rules are major (protocol 5). Read the trend records `plain-language-public-service-pages`, `charity-emotional-template` and `law-firm-authority-template` in `trends.md`: the last two are the slop versions to depart from. [Our take]
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- design-principles and idea-sketches are skipped. Read the tone words and three anti-goals from brief-draft.md, and write six one-line, unjudged ideas at the top of direction-matrix.md before you converge. Read the landscape note at the top of reference-board.md as the landscape audit.
- Three directions are still required, but three short columns are enough: north star, art style, type class, palette mood, skeleton and hero, lead element and its second moment, recipe and the rules it collides with. Choose the recipe with get_recipe (at most 3 tags per call).
- Draft tokens live here in lean: add rows for up to two type families with roles (see the font sourcing advice in explore-type-color and decide-tokens) and 5 to 7 colour roles per direction, with contrast pairs checked by check_contrast. explore-hero and decide-tokens read them from the matrix.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- idea-sketches (explore-sketch) and design-principles (ref-principles) exist in the sprint: use them. need-landscape, explore-type-color and explore-structure are skipped: read the five-line landscape note at the top of reference-board.md as the landscape audit, and write the draft tokens and the structure into the matrix instead.
- Three directions are still required, but three short columns are enough: north star, art style, type class, palette mood, skeleton and hero, lead element and its second moment, recipe and the rules it collides with. Choose the recipe with get_recipe (at most 3 tags per call).
- Draft tokens live here in the sprint: add rows for up to two type families with roles (see the font sourcing advice in explore-type-color and decide-tokens) and 5 to 7 colour roles per direction, with contrast pairs checked by check_contrast, plus the section order of the page. explore-hero, decide-inclusive, decide-prototype and decide-tokens read them from the matrix.
## Ask the owner (only what you cannot default)
- (Gate 2, with the desktop and mobile sheets) Which direction? (a) [n], my recommendation, for [one reason] (recommended) (b) another number or a mix ("1's type with 3's colour") (c) none: say why.
## Tools
- `get_studio`: topic concepts (three concepts, anchor, signature, motion verb), art-direction, typography
- `get_moves`: the catalogue of recurring moves with the library sites that show each; one lead move per direction
- `propose_directions`: brief and the owner's taste slugs; returns safe, stretch and wildcard drafts with per-site anchors, recipes and Quality Bar collisions, and reports when the three are too alike
- `render_sheet`: the three hero concept files; writes one labelled side-by-side sheet per size (1440x900 and 390x844) to show the owner
- `review_design`: each concept before the sheet goes out: zero blockers and none of the option-gate minors (protocol 4)
- `get_critic_brief`: the brief for one fresh critic who scores each option from screenshots only, before the owner sees the sheet
- `record_taste`: type score per option (round `gate 2: <direction>`, score 1 to 10, the owner's words, slugs shown), then type pick for the choice
- `get_recipe`: at most 3 tags per call (canonical slugs from list_tags); returns keep, avoid, steps; long JSON with many tags
- `recommend`: optionally, to sanity-check one direction against the brief
- `list_tags`: to use canonical slugs
## Output template
```markdown
# Direction matrix
| | Direction A | Direction B | Direction C |
|---|---|---|---|
| North star | | | |
| Concept (one sentence) and its anchor fact | | | |
| Signature moment and motion verb | | | |
| Range (safe / stretch / wildcard) | | | |
| Library anchors (slug: what it takes) | | | |
| Art style (<=3) | | | |
| Mood (<=2) | | | |
| Type class | | | |
| Palette mood | | | |
| Page skeleton / hero | | | |
| Reference sites | | | |
| Recipe(s) | | | |
| Rule collisions to manage | | | |
| Lead element (not in the niche default) | | | |
| Niche cue: what tells a visitor in one second which kind of site this is (motif, palette, shape, material) | | | |
| Where the lead element recurs lower on the page; how the sections below differ from each other | | | |
| Imagery plan (photos, live object, type as image, or gap marked) | | | |
| Draft tokens (lean and sprint: two type families, 5 to 7 colour roles, checked pairs; sprint also the section order) | | | |
| Difference from the niche default | | | |
```
## Gates
Rules to satisfy: `distinct-swap-test`, `distinct-written-direction` (read them with get_guidelines or rules/*.md).
- [ ] Each direction carries a concept with an anchor fact and a portability score, a signature moment and a motion verb; no direction is a library style alone.
- [ ] Each direction names a niche cue: avoiding the niche's clichés must not drop its vocabulary (a wedding site still needs something that says wedding).
- [ ] The directions differ in at least two dimensions and span safe, stretch and wildcard, each anchored on named library sites with a stated take.
- [ ] Option gate (protocol 4): the options came from propose_directions and render_sheet; each passed review_design with zero blockers and none of `distinct-hero-not-template`, `distinct-no-decorative-glow`, `distinct-no-accent-word-headline`, `distinct-eyebrow-restraint`; a fresh critic scored each from screenshots only; the owner's 1 to 10 score per option is recorded with record_taste.
- [ ] The owner was shown the desktop and mobile sheets (made in explore-hero) and their pick is recorded, or the pick is the one blocking question in OPEN-QUESTIONS.md and work has stopped (protocol 4).
- [ ] Each names its recipe and collision risks.
- [ ] Each names a lead element and a second moment lower on the page; at least one direction departs from the niche default.
- [ ] Each states how its sections below the hero differ in structure from each other.
- [ ] Each states its imagery plan; with no photographs it names the live object, the type move or the marked gap.
## Done when
- A complete matrix for three distinct directions.
## Pitfalls
- Three variations of one idea.
- Showing the owner hand-made mock-ups that skipped propose_directions, render_sheet, review_design and the critic: a centred stack with a stats strip, a soft glow, one accent-coloured italic word and corner labels is what read as AI-made on 2026-11-17.
- Choosing for the owner and marking it ASSUMED: taste is never defaulted.
- Three palettes on one layout (not three directions).
- Ignoring the accessibility risks of a favorite style.
- A distinctive hero on top of a plain sequence of heading-and-paragraph sections.
- Drawing the product from shapes in code because there are no photographs.
