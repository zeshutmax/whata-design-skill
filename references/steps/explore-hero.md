# Step: Design hero concepts (`explore-hero`, stage explore)
**Goal:** Design the first screen for each direction, using the real headlines.
**Your role:** Design the first screen of each direction as something you can look at, with real copy, type and color.
**Inputs:** direction-matrix, type-color-studies, structure-wireframes, headline-drafts  
**Output artifact:** hero-concepts -> `design/04-explore/hero-concepts/`
## Procedure
1. Build each hero on the base kit (get_base: skip link, header, a hero skeleton) as a small HTML/CSS page using the direction's tokens, the real headline and the real action label; your own CSS adds only the lead idea. Run `pnpm --silent --filter @whata/audit cli widths <file>` and fix every problem before the sheet. Render it at 1440×900 and 390×844 and look at the screenshots.
2. The first screen must show: who/what, why it differs, the primary action, a cue that more follows, navigation. [Evidence: homepage principles]
3. Apply the direction's recipe steps while building (focus ring, reduced motion, contrast, media handling). [Standard + Craft]
4. Start from the gate 1 bundle sketches (design/03-references/bundles/): the concept for the owner's bundle and two others are refined here, not drawn again. With scope `Structure: rebuild`, draw each hero fresh: nothing of the old layout carries over except content.
5. Make each concept look like its references, not like a template with their colours. Two ways, pick per concept: (1) **Critique loop:** run compare_to_library on the concept with its anchor slugs (it measures scale contrast, section whitespace, lead-object share and motion against the anchors and lists the gaps), then put the concept beside its main reference at the same viewport (`cli sheet` with both files, or the reference's fold screenshot from storage/sites/), list the gaps in scale (display size against body, the largest element against the viewport), whitespace, imagery and the lead object, fix them, and repeat once more: two rounds before the owner sees it. Keep the two gap lists in notes.md. (2) **Reference rebuild:** when the owner picked a library site at gate 1, rebuild its hero as a structural re-skin (same grid, scale steps, spacing and object placement from get_design_brief and get_section), check the structure with `pnpm site score <slug> <file:// or http URL of your hero>` (the rebuild score compares section by section; read the hero section's score, the rest of the page is not built yet), then swap in this project's content, colours and imagery. Copy structure only: no text, logo, images or brand colours of the reference, and none of its audit failures. [Our take]
6. Presence of style, not only absence of slop: each concept needs a clear scale contrast (the display size several times the body size, or one element that fills much of the first screen), one lead object that carries the message, and deliberate whitespace. A concept that is type plus colour on an even grid is flat: fix it before the sheet. The library's heroes fill most of the first screen with their lead object, usually as a full-bleed backdrop (an image, video or code-made SVG behind the text); the kit's `hero-bleed` part does this with a scrim so text contrast holds, and get_backdrop draws the backdrop in code from the palette and the project's own content (aurora, a field of one mark per real item, contours, the brand word set huge; see content/kit/backdrops.html). An object in a column is fine when the brief needs it, but then say on the sheet that it is smaller than the references' and why. compare_to_library counts full-bleed backgrounds and judges a hero-only sketch on its first screen only. [Our take]
7. Order in the first screen: one clear headline, one line, one action and one lead object, with the niche cue and atmosphere around them; separate elements that compete for attention need a reason. Richness (pattern, motif, backdrop, texture) is not competition and stays. Check each concept with `pnpm --silent --filter @whata/audit cli types <file>`: every role takes one style and peers in a list match; the style and element counts it prints are information, not a target. [Our take]
8. Keep the heroes small; do not build the whole page yet.
9. Show each concept beside its library anchors: the concept's key frame and the fold screenshots of the two or three library sites it takes its visual language from, on one sheet (`imageSheet` in @whata/audit, or put the anchor folds from storage/sites/ next to the concept in `cli sheet`). Name what each anchor gives (canvas, type, the object, the motion). If the frame does not visibly belong next to them, it is not in the library's language yet: change the canvas, type, spacing or object, not the concept. [Our take]
10. Every frame a poster: the first frame of each concept is its best, with type, space and image composed on purpose; motion may only amplify it. Rough the signature moment in at least the concept you recommend (a still of its key frame is enough for the sheet), so the owner judges the idea, not a layout. [Our take, from the awwwards method]
11. Before the sheet, the option gate (protocol 4): each concept passes review_design with zero blockers and none of `distinct-hero-not-template`, `distinct-no-decorative-glow`, `distinct-no-accent-word-headline`, `distinct-eyebrow-restraint`, and one fresh critic scores each from its screenshots only (get_critic_brief). Fix and re-run a concept that fails; do not send it with a note.
12. Make the sheets and stop: render_sheet (or the audit CLI's `sheet` command) puts the three concepts side by side, labelled with name and north star, one image per size (1440x900 and 390x844), with review_design run on each concept first. Send both sheets to the owner and ask gate 2's question (explore-directions). Nothing from decide-tokens onward starts, and nothing is built in the site tree, until the owner's pick is recorded. Screenshots of a single concept: `pnpm --silent --filter @whata/audit cli shot <file|url> <out.png> <width> <height>`.
13. No photographs of a physical product? Follow the imagery plan in the direction matrix: build the live object (price, seats, dates, a calculator or booking control made of real HTML with real states and real numbers), or set a measurement, date or price large as real text, or leave the image out and mark the gap. Do not draw the product from shapes in code. A faint decorative gradient or texture that does not depict the product is ornament; one that starts to depict it (grooves that read as a wheel, a glaze) is an illustration and counts under `distinct-real-imagery-and-icons`. [Our take]
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- type-color-studies and structure-wireframes are replaced by the draft tokens and the skeleton and hero rows of direction-matrix.md. Build every hero from those draft tokens.
- A lower bar: three concepts, each a small page of about fifteen lines is enough, but each is rendered at 1440x900 and 390x844 and looked at. Run review_design on all three concepts when each audit takes under five minutes (it usually does): reviewing only the concept you expect to choose biases the comparison, and in a test the owner chose the one with the most blocker risk. Fix blocker findings on the one chosen. If time is short, say in notes.md which concept got the full review.
- Check the lead element and the primary action are inside the first viewport at both sizes by screenshot: the audit does not check that.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- type-color-studies and structure-wireframes are replaced by the draft tokens and the skeleton and hero rows of direction-matrix.md. Build every hero from those draft tokens.
- The same lighter bar as lean: three concepts, each a small page of about fifteen lines is enough, each rendered at 1440x900 and 390x844 and looked at. Run review_design on all three when each audit takes under five minutes; the concept you expect to choose is built on the real tokens, and decide-critique on Day 3 runs review_design on the others, whose findings are then about a small page, not a finished one. Record in notes.md which concepts got the full review.
- Check the lead element and the primary action are inside the first viewport at both sizes by screenshot; with an urgent-help band (recipe `urgent-help-route`) check that the band does not push the primary action below the fold at 390x844.
## Ask the owner (only what you cannot default)
- (With the sheets) Which concept? (a) [n], my recommendation (recommended) (b) another number or a mix (c) none: say why.
## Tools
- `get_recipe`: for the direction's styles
- `review_design`: path to the hero HTML; returns Quality Bar results
- `render_sheet`: the three concept files; writes directions-desktop.png and directions-mobile.png
- `compare_to_library`: each concept with its anchor slugs: gaps in scale contrast, whitespace, lead object and motion before the owner sees it
- `get_critic_brief`: one fresh critic scores each concept from its screenshots only before the sheet goes out
## Output template
```markdown
# Hero concepts
One folder per direction: hero-A/index.html, hero-A-desktop.png, hero-A-mobile.png, notes.md (decisions and which recipe steps were applied).
directions-desktop.png and directions-mobile.png: the three side by side, labelled, sent to the owner.
```
## Gates
Rules to satisfy: `ux-purpose-clear`, `ux-primary-cta-above-fold`, `ux-false-floor`, `distinct-hero-not-template`, `distinct-no-decorative-glow`, `distinct-no-accent-word-headline`, `distinct-eyebrow-restraint`, `craft-contrast-text-on-media` (read them with get_guidelines or rules/*.md).
- [ ] Option gate (protocol 4): every concept on the sheet passed review_design with zero blockers and none of `distinct-hero-not-template`, `distinct-no-decorative-glow`, `distinct-no-accent-word-headline`, `distinct-eyebrow-restraint`, and a fresh critic scored each from screenshots only.
- [ ] The first screen answers what it is and what to do within five seconds.
- [ ] Mobile and desktop screenshots exist, and the two side-by-side sheets were sent to the owner.
- [ ] Each concept went through two critique rounds beside its reference (or a scored reference rebuild), with the gap lists in notes.md.
- [ ] Each concept has a scale contrast and a lead object.
- [ ] review_design shows no blocker failures (lean and sprint: for the concept you expect to choose; say which).
## Done when
- Three hero concepts with screenshots and a clean blocker review (lean and sprint: three concepts with screenshots, one with the full review).
## Pitfalls
- Carrying on to tokens or a build before the owner has picked from the sheet.
- Flat concepts: type and colour on the old layout, no lead object, no scale contrast.
- Showing the owner a concept that was never put beside its reference.
- Placeholder text.
- Heroes that only work at one viewport.
- Template hero: centered stack with a generic gradient.
