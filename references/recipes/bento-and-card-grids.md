# Recipe: Bento, catalog and gallery grids that reflow and read in order (`bento-and-card-grids`)
Styles covered: bento-grid, catalog-grid, gallery-wall
**Keep:** Tiles of different sizes, rounded cards, dense product or image grids, a dominant lead tile.
**Avoid:** Spans that overflow at 320px; grid-auto-flow: dense or order used to move content out of source order; whole-card wrapper links with several tab stops; rows of identical icon cards; cards nested inside cards; ten equal choices on the first screen; images without reserved space.
Keep the mosaic of mixed-size tiles, the product grid and the image wall. Start from a one-column grid that needs no media query to fit 320px, add spans only on wide screens, keep the HTML in reading order, make each card one list item with one link, and let one item lead.
**While designing:** Use auto-fit minmax(min(100%, 15rem), 1fr) with spans only on wide screens, keep source order equal to reading order, li > heading > one link with a stretched ::after, and let one tile lead.
## Steps
### Auto-fit grid, spans in media query (`bg-reflow`) [craft-consensus · verified]
Base the grid on repeat(auto-fit, minmax(min(100%, 15rem), 1fr)) so every tile fits a 320px viewport with no media query. Add column and row spans only inside a min-width media query, set min-inline-size: 0 and overflow-wrap: anywhere on tiles, and wrap the grid in a centered container no wider than 1200 to 1400px.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 6-tile bento (one 2x2 lead, one 2-wide tile, four singles) in a 75rem container had scrollWidth 320 with one 288px column at a 320 px viewport, and four 288px columns with the lead spanning 592px at 1280 px. WCAG 1.4.10 requires content to work at 320 CSS px without two-dimensional scrolling. Switch to spans at 50em because that is where four tracks fit, not at a device width.
- Satisfies: a11y-reflow, craft-container-max-width, craft-breakpoints-content-based
```css
.bento { list-style: none; margin: 0; padding: 0; display: grid; gap: 1rem;
         grid-template-columns: repeat(auto-fit, minmax(min(100%, 15rem), 1fr)); }
.bento > li { min-inline-size: 0; overflow-wrap: anywhere; }
@media (min-width: 50em) {
  .bento { grid-template-columns: repeat(4, 1fr); }
  .lead { grid-column: span 2; grid-row: span 2; }
  .wide { grid-column: span 2; }
}
```
### HTML in reading order (`bg-order`) [craft-consensus · verified]
Write the HTML in the order you want read and tabbed, most important tile first. Do not use order or grid-auto-flow: dense to rearrange content that has a meaning order, and check with a script that visual order equals DOM order.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): three tiles (two spanning 2 columns, one spanning 1) in a 3-column grid had DOM order one, two, three and the same visual order by default. With grid-auto-flow: dense the third tile moved up beside the first, so the visual order became one, three, two while keyboard focus still went one, two, three. MDN: order and grid placement change visual order only, not the order assistive technology or tab navigation use, and style sheets that use them for logical reordering are non-conforming. In the 6-tile bento above (no dense) tab order equalled visual order at 320 and 1280.
- Satisfies: a11y-meaningful-sequence, a11y-focus-order
```js
// fails when visual reading order (row, then column) differs from DOM order
const items = [...document.querySelectorAll(".bento > li")];
const rects = items.map((li, i) => ({ i, ...li.getBoundingClientRect().toJSON() }));
const visual = [...rects].sort((a, b) => a.top - b.top || a.left - b.left).map(r => r.i);
console.assert(visual.every((v, i) => v === i), "visual order differs from DOM order");
```
### Card markup with stretched link (`bg-card-markup`) [craft-consensus · verified]
Mark each tile as li > heading > a, make the heading link the only tab stop, and extend the click area with a stretched a::after. Draw the focus ring on that ::after so it surrounds the whole card. Decorative images get alt=""; a "read more" cue is non-interactive text.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): each of six tiles held exactly one focusable element; Tab visited them in DOM order; axe-core 4.14 reported no violations at 320 and 1280 px. In a separate one-card page, the computed style on the focused link's ::after was outline: solid 3px rgb(11, 95, 255), a ring of 5.12:1 against white (5.12:1 computed). The ::after covers the whole tile, so the target is well above 24 by 24 px. Link text carries the purpose (the heading), as WCAG 2.4.4 asks.
- Satisfies: comp-card-single-primary-link, comp-card-limited-tab-stops, a11y-focus-visible, a11y-link-purpose, a11y-target-size
```css
.bento > li { position: relative; }
.bento a { color: inherit; }
.bento a::after { content: ""; position: absolute; inset: 0; border-radius: inherit; }
.bento a:focus-visible { outline: none; }
.bento a:focus-visible::after { outline: 3px solid #0B5FFF; outline-offset: 3px; }
```
### Lead tile takes the most space (`bg-lead-variety`) [craft-consensus · partly-verified]
Let the most important tile take the most space (2x2 or full width) and show it as a real example, not an icon. Size the other tiles to their content, not to fill a pattern. Group content inside a tile with space, rules and type, never with a second bordered card inside the first. Do not use emoji as tile icons.
- How: These follow the guideline checks: no section made mainly of three or more same-size icon-heading-sentence cards; no bordered or shaded container inside another; section order and block count driven by the buyer's questions. The bento above uses a 2x2 lead and a 2-wide tile so the widths differ.
- Satisfies: distinct-no-identical-card-grid, distinct-no-nested-cards, copy-section-content-drives-structure
- Verification note: The thresholds come from detector-style guidelines whose sources were partly read, and the our-take section-order rule; this is craft advice, not tested against user outcomes.
### One lead, about five choices (`bg-limit-choices`) [craft-consensus · partly-verified]
Show one dominant item and at most about five equal choices in each viewport-height section. For a catalog or gallery with many items, put the first row or two on screen, then use filters, a paged list or a real "show more" button; keep price, fees and key conditions on each product card. Reserve each image's space with width and height or aspect-ratio and crop with object-fit: cover and object-position, not by stretching.
- How: COGA: about five or fewer main choices per screen, one visually dominant feature, costs shown at the start. A shop grid necessarily lists many products, so the guidance is applied as hierarchy (one lead, filters, paging) rather than as a hard cap. The image-space and CLS measurement is in the hero-and-photography recipe: without width and height an image loading late gave CLS 0.0293 in Chrome and with them 0. Product images that show the product need alt text that names it; purely decorative tiles use alt="" (NN/g).
- Satisfies: a11y-coga-limit-choices-per-screen, a11y-coga-costs-up-front, craft-image-dimensions-reserved, craft-image-no-distortion, a11y-alt-text
- Verification note: The five-choice limit is COGA guidance, not a studied threshold, and a shop grid cannot meet it literally; the hierarchy approach is our judgement.
