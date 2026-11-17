# Recipe: Editorial, newspaper and serif-led layouts that read easily (`editorial-serif-print`)
Styles covered: editorial, serif-editorial, serif-display, newspaper, editorial-feed
**Keep:** Large serif display type, multi-column text, rules between stories, pull quotes, mastheads, a lead story that is bigger than the rest, captions and bylines.
**Avoid:** Sentences over 25 words and grade-12 prose; justified text without hyphenation; kicker labels above every heading; a kicker above the main headline; dashes in headings; cream paper with a terracotta accent by reflex; thin serif cuts at body size; tables drawn as images or divs; a feed made of identical cards.
Keep the serif headlines, the columns, the rules and the front-page hierarchy. Hold body text at 18px or more, write in short plain sentences, keep tables as real tables, and give the page a paper colour that is not the default cream.
**While designing:** Serif headlines and real columns, body at 18px and 55ch, plain sentences with the summary first, a cool newsprint or subject-driven paper colour, real tables, one lead story and varied blocks.
## Verified palette: Newsprint, computed
- background: #EEF0F2
- text: #14171A
- text-muted: #4A5058
- rule: #6F767E
- accent: #8C1D2B
- link: #0B4FA3
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink on newsprint | #14171A | #EEF0F2 | 15.74:1 | 4.5:1 |
| muted caption on newsprint | #4A5058 | #EEF0F2 | 7.12:1 | 4.5:1 |
| oxblood accent text on newsprint | #8C1D2B | #EEF0F2 | 7.9:1 | 4.5:1 |
| link blue on newsprint | #0B4FA3 | #EEF0F2 | 6.9:1 | 4.5:1 |
| hairline rule on newsprint (UI, 3:1) | #6F767E | #EEF0F2 | 4.02:1 | 3:1 |
| white on oxblood button | #FFFFFF | #8C1D2B | 9.02:1 | 4.5:1 |
## Steps
### Body at 1.125rem, 55ch measure (`eds-body-measure`) [craft-consensus · verified]
Set running text at 1.125rem (18px) with line-height 1.55 and cap every text block at 55ch. Captions may drop to 0.875rem; nothing else goes below 1rem.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): on a test article the smallest computed size of p, li, td and th was 18px at both 320 and 1280 px viewports, with no horizontal overflow. Butterick advises 15 to 25 px for web body text and an average line length of 45 to 90 characters (66ch is the usual target). A rem size lets the user's browser setting scale the page.
- Satisfies: craft-body-size-min, craft-measure-body, craft-line-height-body, craft-relative-units-text
```css
body { font: 400 1.125rem/1.55 "Newsreader", Georgia, serif; }
.prose { max-inline-size: 55ch; }
figcaption { font-size: 0.875rem; }   /* captions only */
```
### Multi-column text with hairline rule (`eds-columns`) [craft-consensus · partly-verified]
Build newspaper columns with CSS multi-column (column-width, not a fixed count), a hairline column-rule, and column-span: all on headings. Keep text start-aligned; justify only with hyphens: auto and a lang attribute on html.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with columns: 22rem 3 the text ran in one 288 px column at 320 px and three 363 px columns at 1280 px, and scrollWidth equalled the viewport width at both. Computed hyphens was auto on the justified paragraphs. Source order is the reading order in multi-column, so keyboard and screen reader order stay meaningful. WCAG 1.4.12 needs layouts that survive user text-spacing overrides, so give columns no fixed height.
- Satisfies: craft-align-left-body, distinct-justified-exceptions, a11y-reflow, a11y-meaningful-sequence, a11y-text-spacing
- Verification note: The reflow, hyphens and no-overflow facts were measured and the rule exception (justified plus hyphens plus lang) comes from the guidelines. The 22rem minimum column width (about 40 characters at 18px) is our judgement; Butterick advises 45 to 90 characters and says justified text needs hyphenation and wide enough lines, so very narrow justified columns can still look gappy. Not tested with a screen reader.
```css
.cols { columns: 22rem 3; column-gap: 2rem; column-rule: 1px solid var(--rule); }
.cols h2 { column-span: all; }
.cols p { text-align: justify; hyphens: auto; }   /* needs <html lang="en"> */
@media (max-width: 40em) { .cols p { text-align: start; } }
```
### One type scale, three heading levels (`eds-scale`) [craft-consensus · verified]
Use one scale of body 1.125rem, h3 1.4rem, h2 1.75rem and an h1 stepped in rem (2.25rem, then 3.75rem from min-width: 48em); no clamp() with vw. Style at most three heading levels in articles, with at least one step of 1.25 or more.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): computed sizes were 18, 22.4, 28 and 36 px at 320 px (step ratios 1.24, 1.25, 1.29) and 18, 22.4, 28 and 60 px at 1280 px (the h1 step is 2.14); the figures were taken with an earlier clamp(2.25rem, 1.6rem + 3vw, 3.75rem) h1, and the stepped sizes in the sample give the same 36 and 60 px at the two ends. The stepped rem sizes (small 2.25rem is 60% of large) scale with the user's text-size setting, whereas a clamp with a vw term was measured not to reach 200% (type-zoom-2026-11-05). Keep the h1 under 6rem and use line-height 1.05 to 1.15 on wrapped headlines. Butterick advises at most three heading levels (two is better) with the smallest visible size increment between them, so the display h1 is the one big step and h2 and h3 differ by roughly 1.25.
- Satisfies: distinct-type-hierarchy-step, craft-heading-levels-limit, craft-fluid-type-rem-clamp, craft-heading-line-height, distinct-hero-headline-proportion
```css
:root { --s0: 1.125rem; --s1: 1.4rem; --s2: 1.75rem; --s3: 2.25rem; }
@media (min-width: 48em) { :root { --s3: 3.75rem; } }
h1 { font-size: var(--s3); line-height: 1.05; text-wrap: balance; overflow-wrap: anywhere; }
h2 { font-size: var(--s2); } h3 { font-size: var(--s1); }
```
### Serif with an optical-size axis (`eds-serif-cuts`) [craft-consensus · partly-verified]
Choose a serif with an optical-size axis for body and display (Newsreader, Source Serif 4 and Literata all have opsz and wght axes) and keep Light cuts (weight 300 or below) for display lines of 24px and up. Body and captions stay at weight 400 or heavier.
- How: Google Fonts metadata (fetched 2026-11-06) lists Newsreader (opsz 6 to 72, wght 200 to 800), Source Serif 4 (opsz 8 to 60, wght 200 to 900) and Literata (opsz 7 to 72, wght 200 to 900) as variable serifs, none on the overused-font list in the display-font rule (Fraunces and Instrument Serif are). With font-optical-sizing: auto the face draws sturdier letterforms at small sizes. Delicate high-contrast faces such as Cormorant Garamond (weights 300 to 700) and Bodoni Moda (wght 400 to 900, opsz 6 to 96) belong at display size.
- Satisfies: craft-weight-thin-limited, distinct-display-font-chosen
- Verification note: Font axes and ranges were read from Google Fonts metadata. The 300-or-lighter-at-24px-and-up limit comes from the guideline, whose Apple HIG source was only partly read. Sample rendering of each face was not checked.
```css
:root { font-optical-sizing: auto; }
h1, .display { font-weight: 300; }          /* only at 24px and up */
body, figcaption, td { font-weight: 400; }
```
### Pick paper color for the subject (`eds-paper`) [craft-consensus · verified]
Pick the paper colour for the subject. The palette above uses a cool newsprint grey (#EEF0F2) with near-black ink; if you want warm cream, record the subject reason and avoid pairing it with a terracotta accent and a serif display face by default.
- How: Computed with the WCAG 2 formula: ink on newsprint 15.74:1, muted captions 7.12:1, oxblood 7.9:1, link blue 6.9:1, white on oxblood 9.02:1. The rule colour #6F767E reaches 4.02:1 against the paper, so column rules and table lines that mark structure meet 3:1 (a lighter #8A9098 only reaches 2.81:1). Cream #F4F1EA matches the reflex-cream test (minimum channel 234, red at least green at least blue, red minus blue 10). Define every colour once as a role token.
- Satisfies: distinct-palette-not-reflex-cream, a11y-contrast-text, a11y-non-text-contrast, craft-color-role-tokens
### Limit kickers, arrows and dashes (`eds-chrome`) [craft-consensus · partly-verified]
Limit kickers (small tracked labels above headings) to ceil(sections / 3) per page, none above the main headline. Use numbers only for real sequences, at most two arrow-ended links, one dot-separated meta line, and keep em dashes out of headings and under one per 300 words. Write headings and navigation in sentence case; set bylines and dates with layout (a dl or flex gap), not middle dots.
- How: The limits are the rules' own thresholds. Butterick rejects title case and all caps for headings; GOV.UK says to write all headings in sentence case. A front page can still carry a masthead and a section label where the label adds information (a section name such as "Local news" does; a decorative "01 / Stories" does not).
- Satisfies: distinct-eyebrow-restraint, distinct-no-template-chrome, copy-em-dash-restraint, copy-sentence-case, craft-heading-sentence-case
- Verification note: Sentence case sources were read. The dash, arrow, kicker and middle-dot limits come from the detector-based guidelines, whose sources are partly read (impeccable-repo) or our-take (em dashes). Treat them as review thresholds.
### Short sentences and paragraphs (`eds-plain-copy`) [craft-consensus · partly-verified]
Write each sentence at 25 words or fewer, averaging 20 or fewer; paragraphs of one idea and at most five sentences (marketing pages three); open every article or long section with a one- or two-sentence summary that states the conclusion; choose the plain word; start with the first real fact instead of a filler opener.
- How: Sources: GOV.UK, NN/g and COGA agree on short sentences, one idea per paragraph, conclusion first; WCAG 3.1.5 asks for a summary or simpler version when text needs more than lower-secondary reading ability. A quick local check with a rough Flesch-Kincaid script (our own syllable heuristic, not an official tool, so use Hemingway or textstat for real scoring) gave grade 1.9 and a longest sentence of 12 words for a four-sentence news brief, against grade 27 and one 34-word sentence for the same news set as one long clause. Long-form voice is a craft choice: a literary feature may exceed grade 9, so open it with a plain-language standfirst and record the exception.
- Satisfies: copy-sentence-length, copy-paragraph-length, copy-reading-grade, copy-reading-level-companion, copy-plain-words, copy-summary-first, copy-no-filler-openers, a11y-reading-level-support, a11y-coga-short-paragraphs
- Verification note: The thresholds and sources were read. The grade figures came from our own approximate script and are illustrative; the exact scores depend on the tool. Whether a literary feature should be held to grade 9 is our judgement.
```js
// quick audit: flag sentences over 25 words
const long = [...document.querySelectorAll("main p")]
  .flatMap(p => p.textContent.split(/(?<=[.!?])\s+/))
  .filter(s => s.split(/\s+/).length > 25);
```
### Real lists and captioned tables (`eds-lists-tables`) [craft-consensus · verified]
Turn three or more parallel items and every procedure into ul or ol. Mark data (schedules, results, specs) as a table with a caption, th scope="col" and scope="row". If the table is wider than its container, scroll it inside a labelled container with tabindex="0".
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 4-column table in a 288 px container with overflow-x: auto and no tabindex was flagged by axe-core 4.14 as scrollable-region-focusable (serious); adding tabindex="0", role="region" and aria-labelledby pointing at the caption cleared it, and the page itself did not overflow (scrollWidth 320). WCAG 1.4.10 lets a data table scroll in its own container as a two-dimensional exception, while headings and paging around it must still reflow.
- Satisfies: copy-lists-for-parallel-items, comp-data-table-semantics, comp-data-table-overflow-focusable, a11y-semantic-structure, a11y-reflow
```html
<div class="scroll" tabindex="0" role="region" aria-labelledby="cap">
  <table>
    <caption id="cap">Opening hours, 2026</caption>
    <thead><tr><th scope="col">Day</th><th scope="col">Open</th></tr></thead>
    <tbody><tr><th scope="row">Sunday</th><td>11 to 3</td></tr></tbody>
  </table>
</div>
```
### Lead story and varied blocks (`eds-feed`) [craft-consensus · partly-verified]
For a front page or feed, make one story the lead (larger headline, more room), vary the layout of the next blocks (a list, a two-up, a rule-separated column), vary section padding, and keep the HTML in the order a reader should meet the stories. Each story is li > heading > one link; extend the click area with a stretched a::after, not a wrapping anchor.
- How: The stretched-link pattern comes from Inclusive Components (cards); the grid measurements for the same pattern (one tab stop per card, tab order equal to source order, no axe violations) are in the bento-and-card-grids recipe. The rhythm targets (no layout family for more than two consecutive sections, at least four families in eight sections, non-identical section padding) are the guideline thresholds.
- Satisfies: distinct-section-rhythm-varied, a11y-meaningful-sequence, comp-card-single-primary-link, distinct-no-identical-card-grid
- Verification note: Card markup was tested in a scratch page (see the bento recipe); the front-page rhythm advice is our judgement guided by the guideline thresholds, and its sources were partly read.
