# Recipe: Swiss grids, utilitarian interfaces and corporate-clean pages that are not generic (`swiss-utilitarian-corporate`)
Styles covered: swiss-grid, utilitarian, corporate-clean
**Keep:** A visible column grid, neutral grotesque type, strong alignment, small labels, rules, tables, system-UI details, blue accents, product screenshots and clear sections.
**Avoid:** Inter, Helvetica or Arial as the display face by default; table cells under 16px; a label above every heading; arrow and middle-dot chrome on every link and meta line; library defaults (radius, colours, font) left as shipped; div-built product mock-ups; a hero that would read the same with a competitor's logo.
Keep the strict grid, the plain type, the dense tables and the blue-and-white product look. Choose a display face that is not the default, keep table text at 16px, use labels sparingly, and show the real product so the page does not pass the swap test.
**While designing:** Keep a visible 12-column grid and plain type; choose a display face that is not the default; table text at 16px; show the real product; set your own tokens; verify blue and grey contrast.
## Verified palette: Corporate clean and Swiss, computed
- background: #FFFFFF
- text: #1F2937
- text-muted: #4B5563
- surface: #F3F4F6
- rule: #767676
- accent: #1D4ED8
- focus: #0B5FFF
- swiss-red: #C40500
- ink: #111111
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| body text on white | #1F2937 | #FFFFFF | 14.67:1 | 4.5:1 |
| muted text on surface | #4B5563 | #F3F4F6 | 6.86:1 | 4.5:1 |
| blue link on white | #1D4ED8 | #FFFFFF | 6.7:1 | 4.5:1 |
| white on blue button | #FFFFFF | #1D4ED8 | 6.7:1 | 4.5:1 |
| structural rule on white (UI, 3:1) | #767676 | #FFFFFF | 4.54:1 | 3:1 |
| focus ring on white | #0B5FFF | #FFFFFF | 5.12:1 | 3:1 |
| focus ring on surface | #0B5FFF | #F3F4F6 | 4.65:1 | 3:1 |
| Swiss red text on off-white | #C40500 | #F2F2F0 | 5.56:1 | 4.5:1 |
| white on Swiss red | #FFFFFF | #C40500 | 6.23:1 | 4.5:1 |
| ink on off-white | #111111 | #F2F2F0 | 16.84:1 | 4.5:1 |
## Steps
### Pick a neutral grotesque (`su-display-face`) [craft-consensus · partly-verified]
Pick a neutral grotesque that is not on the overused list (Inter, Roboto, Open Sans, Lato, Montserrat, Arial, Helvetica, Geist, Plus Jakarta Sans, Space Grotesk and others) unless it is the brand's own face. Candidates present in Google Fonts: Hanken Grotesk, Schibsted Grotesk, Albert Sans, Familjen Grotesk, Public Sans, Archivo, IBM Plex Sans. Write the choice and the reason in the direction file.
- How: Google Fonts metadata (fetched 2026-11-06) lists each of the seven families as sans serif; Hanken Grotesk, Albert Sans, Familjen Grotesk and Public Sans are variable in weight, Archivo and IBM Plex Sans in weight and width. Neutral Swiss character comes from even stroke, closed apertures and tight, regular spacing; judge it by setting your real headline in two or three candidates. If the brand owns a face, use it and record the exception.
- Satisfies: distinct-display-font-chosen, distinct-written-direction
- Verification note: Availability was verified from metadata. The overused list comes from the guideline, whose sources were mostly read but whose detector is partly read. Which candidate feels most Swiss is our judgement; none was rendered.
### Twelve-column grid with fixed gutter (`su-grid`) [craft-consensus · verified]
Build the grid as 12 equal columns with a fixed gutter in a centered container no wider than 1200 to 1400px. Place items by column span at wide viewports and let every item take the full width (grid-column: 1 / -1) at narrow ones. Add overflow-wrap: anywhere to grid children so long strings cannot push the page sideways.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 12-column grid (repeat(12, minmax(0, 1fr)), 1rem gutters, 75rem max) with a heading spanning 4 columns and text spanning 8 had scrollWidth 320 at a 320 px viewport and 1280 at 1280 px, with a long unbroken string inside. Without overflow-wrap: anywhere the same string pushed scrollWidth to 471 at 320 px. Place by source order; if you place items on explicit lines, keep the DOM in reading order. The guideline cites GOV.UK layout and USWDS spacing units for capping the page container at 1400px or less.
- Satisfies: craft-container-max-width, a11y-reflow, a11y-meaningful-sequence
```css
.grid { max-inline-size: 75rem; margin-inline: auto; padding-inline: 1rem;
        display: grid; grid-template-columns: repeat(12, minmax(0, 1fr)); column-gap: 1rem; }
.grid > * { grid-column: 1 / -1; overflow-wrap: anywhere; }
@media (min-width: 48em) { .a { grid-column: 1 / span 4; } .b { grid-column: 5 / span 8; } }
```
### Hierarchy by ratio and weight gap (`su-hierarchy`) [craft-consensus · partly-verified]
Make hierarchy visible with size and weight: pick a ratio of 1.25 to 1.333 between roles (body 1rem, h3 1.333rem, h2 1.777rem, h1 2.369rem at ratio 1.333) and a weight gap of at least 200 between headings and body (400 body, 700 headings). Define the scale as tokens.
- How: The ratios are computed (1.333 compounding gives 1, 1.333, 1.777, 2.369). The guideline needs one step of at least 1.25 between neighbours and a weight gap of at least 200 for 80% of headings. Swiss typography relies on a few sizes and weights with strict alignment rather than on colour or ornament. Limit article headings to three levels (Butterick).
- Satisfies: distinct-type-hierarchy-step, craft-type-scale-tokens, craft-heading-levels-limit
- Verification note: The scale values are arithmetic and the thresholds come from the guideline (detector sources partly read). Whether 1.333 suits a given brand is a craft choice; the Swiss style does not require it.
```css
:root { --step-0: 1rem; --step-1: 1.333rem; --step-2: 1.777rem; --step-3: 2.369rem; }
body { font-weight: 400; } h1, h2, h3 { font-weight: 700; }
```
### Density from layout, not tiny type (`su-labels-and-tables`) [craft-consensus · verified]
Keep information density in the layout, not in tiny type: table cells, list items and form text stay at 1rem (16px) or above, and you get density from tight row padding and a 12-column grid. Use labels (captions, table headers, metadata) only where they add information, at 1rem unless they are true captions, at most ceil(sections / 3) labels above headings, and give capital labels 0.05 to 0.12em letter-spacing.
- How: The body-size rule counts table cells and form text as running text: only captions, footnotes and legal text may be smaller than 16px. Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a pricing-style table at 1rem with 0.75rem cell padding stayed inside its scrolling region at 320 px with no page overflow; axe flagged the scroller without tabindex="0" and passed it with tabindex, role="region" and aria-labelledby on the caption. See the editorial recipe for the markup. Letter-spacing of 0.05em to 0.12em on capitals is Butterick's range.
- Satisfies: craft-body-size-min, distinct-eyebrow-restraint, craft-caps-letterspacing, comp-data-table-semantics, comp-data-table-overflow-focusable
### Plain labels, few arrows and dots (`su-no-chrome`) [craft-consensus · partly-verified]
Write plain link and button labels. No more than two links or buttons end in an arrow, no more than one meta string uses middle dots (separate dates, authors and tags with layout: a dl in a grid, or a flex gap), em dashes stay rare, and no icon-plus-heading-plus-sentence card row is the main section.
- How: These are the guideline thresholds. GOV.UK link guidance asks for descriptive link text: say what happens, not an arrow. The system-UI feel of a utilitarian page comes from real controls (native selects, tables, rules, monospace data) rather than from decorative glyphs.
- Satisfies: distinct-no-template-chrome, distinct-eyebrow-restraint, distinct-no-identical-card-grid
- Verification note: The numeric limits come from detector-based guidelines whose sources are partly read. Our-take on style: use them as review thresholds.
### Blue and grays that pass contrast (`su-palette-focus`) [craft-consensus · verified]
Use blue as a text and button colour only where it passes: #1D4ED8 on white, with white text on a blue button. Mute secondary text no lighter than #4B5563 on a light grey surface. Draw structural rules at #767676 or darker. Give focus its own ring (#0B5FFF, 3px outline, 2px offset).
- How: Computed with the WCAG 2 formula: blue link on white 6.7:1; white on blue 6.7:1; body 14.67:1; muted 6.86:1 on #F3F4F6; a #6B7280 muted grey is only 4.83:1 on white, close to the line; rule #767676 4.54:1; focus ring 5.12:1 on white and 4.65:1 on surface. For a Swiss red, #E10600 on white reaches 4.96:1 while #C40500 reaches 6.23:1 and 5.56:1 on off-white, with white text on it at 6.23:1.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast, a11y-focus-visible, craft-color-role-tokens
```css
:focus-visible { outline: 3px solid var(--focus); outline-offset: 2px; }
```
### Prove the page is this company's (`su-swap-test`) [our-take · judgement]
Prove the page is this company's. Show the real product (a captured screen with alt text, real data, not a rectangle mock-up), build the first two viewports around one idea only this subject could carry, set your own radius, colour and type tokens before using any component library, then run the swap test: replace the logo with a competitor's and ask a reviewer who did not build it which site it is.
- How: This is the guideline's own manual check. To customise library defaults, change the radius, primary colour and font variables to your tokens and record them in the direction file; do not leave the library's init values in the shipped CSS. A corporate-clean page is allowed to be conventional in structure; the distinctiveness comes from the content, the imagery and the one idea.
- Satisfies: distinct-swap-test, distinct-customize-library-defaults, distinct-real-imagery-and-icons, distinct-hero-not-template
- Verification note: Craft opinion. The checks come from guidelines labeled our-take or built on partly read sources; no experiment shows the swap test predicts anything.
