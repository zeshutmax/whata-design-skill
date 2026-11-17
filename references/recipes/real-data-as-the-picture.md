# Recipe: Real data as the picture: the product's own true numbers as the hero or section visual (`real-data-as-the-picture`)
Styles covered: analytics-data, technical-diagram, specimen, product-screenshots
**Keep:** One composed picture made of the product's own data: a measured index, a ruler of real values, or a spec beside its screenshot, in the page's own type and tokens.
**Avoid:** Invented or rounded-up numbers; a row of three big numbers under the hero (the stats strip); data drawn as a raster image or as decoration with no labels; colour as the only key; count-up animations that hide the final value; a chart with no text alternative or source.
When the product's strongest image is something it measured or specifies, make that the visual: a measured index (every item placed by its real score), a ruler of real values (a type scale, spacing steps, prices, distances), or a spec set beside the screenshot it describes. The numbers are true, sourced and dated, set as real text in HTML or SVG, and the picture still works for people who cannot see it, at 320 px, at 200% text and without motion. It replaces the gradient glow and the row of three big numbers, it does not decorate them.
**While designing:** Use the product's own measured or specified numbers as the visual (an index, a ruler, a spec beside its screenshot), set as real text with a source and date, a text alternative and a table behind it; never a stats strip or a decorative chart.
## Steps
### Only true, sourced numbers (`rd-true-numbers-only`) [our-take · judgement]
Draw the picture only from numbers the product really has: a measurement you ran, a value in a source file, a published spec. Record where each comes from and when (a data-source attribute, a visible note under the picture, and the source in design/assets.md). Numbers you do not have are left out, never estimated or rounded up to look better.
- How: distinct-no-filler-copy fails round statistics with no data-source; the honesty rules in the protocol (3.2) forbid invented numbers and mark unconfirmed facts with the .assumed marker. Read the values from the file or tool that produced them at build time (a JSON the site already reads, a measurement script) so the picture cannot drift from the truth.
- Satisfies: distinct-no-filler-copy, distinct-real-imagery-and-icons
- Verification note: Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
### One composed picture, not a strip (`rd-one-picture-not-strip`) [our-take · judgement]
Compose the data as one picture with its own structure (items placed on a scale, ticks on a ruler, callouts beside a screenshot), large enough to be the lead object of the first screen or the section. Do not set three or four big numbers in a row under the headline: that is the stats strip of distinct-hero-not-template.
- How: The audit counts a row of three or more numbers at 28 px or 1.6 times body size or larger, below the h1 or in the next section, as a stock hero signal. A measured index or ruler reads as the product's own work; give it the space a product photo would take and no glow behind it.
- Satisfies: distinct-hero-not-template, distinct-no-decorative-glow
- Verification note: Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
### Labels and values as text (`rd-real-text`) [standard · partly-verified]
Set every label and value as real text: HTML, or SVG text elements in the page's fonts, never a raster image of the chart. Tick labels, values and units scale with the user's text size.
- How: WCAG 1.4.5 asks for text rather than images of text where the presentation can be achieved with text; text in HTML or in SVG text elements can be resized, translated and selected. Size SVG text in CSS units relative to the root size so it follows a 200% text setting, and check it with the audit's stress pass.
- Satisfies: a11y-images-of-text, a11y-resize-text
- Verification note: The requirement was read in the WCAG Understanding pages listed. Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
### Name the takeaway, keep the table (`rd-text-alternative`) [standard · partly-verified]
Give the picture a text alternative that states its takeaway in one sentence (role="img" with aria-labelledby on an SVG, or a figure with a figcaption), and make the underlying values available as a real table or list: visible below, or in a details element. Purely decorative ticks and gridlines are aria-hidden.
- How: WCAG 1.1.1 asks that non-text content has a text alternative that serves the same purpose; for a chart the purpose is the finding, and the data itself belongs in a table with th and scope (see comp-data-table-semantics). Write the takeaway, not a description of the shapes ("40 sites by measured contrast, from 2.1:1 to 17:1").
- Satisfies: a11y-alt-text, comp-data-table-semantics, copy-alt-text-writing
- Verification note: The requirement was read in the sources listed; the markup was not tested with a screen reader here. Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
```html
<figure>
  <svg role="img" aria-labelledby="idx-title" viewBox="0 0 1200 320">
    <title id="idx-title">40 library sites placed by measured headline-to-body contrast, from 2.1 to 9.4</title>
    <!-- one mark per real item; tick labels as <text> -->
  </svg>
  <figcaption>Measured on 2026-11-17 from the captured pages. <a href="#idx-table">The values as a table</a></figcaption>
</figure>
<details><summary>All 40 values</summary><table id="idx-table">...</table></details>
```
### Shape and label carry meaning (`rd-not-colour-alone`) [standard · partly-verified]
When marks fall into groups or one item is highlighted, tell them apart by label, shape or position as well as colour; marks that must be seen to read the picture reach 3:1 against their background and all text 4.5:1 (3:1 at large size).
- How: WCAG 1.4.1 forbids colour as the only visual means of conveying information, and 1.4.11 asks 3:1 for graphical objects required to understand the content. Check each mark and text colour against the background with check_contrast (role ui for marks, text for labels).
- Satisfies: a11y-color-not-only, a11y-non-text-contrast, a11y-contrast-text
- Verification note: The requirements were read in the sources listed. Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
### Reflow or scroll its region (`rd-reflow-320`) [standard · partly-verified]
At 320 px the picture either reflows (a horizontal ruler becomes vertical, an index becomes a ranked list) or scrolls inside its own labelled region; the page itself never scrolls sideways.
- How: WCAG 1.4.10 exempts content that needs two-dimensional layout for meaning, such as data tables and some charts, but the rest of the page must still reflow. A scrolling region needs tabindex="0", a role and an accessible name so keyboard users can scroll it. Check with the audit CLI's widths command at 320, 390 and 320 at 200% text.
- Satisfies: a11y-reflow, comp-data-table-overflow-focusable
- Verification note: The requirement was read in the source listed. Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
### Final values without motion (`rd-final-values-first`) [our-take · judgement]
The final values are in the HTML and visible without JavaScript and with reduced motion. If marks draw in or numbers count up, that runs once, briefly, only without prefers-reduced-motion, and never starts from zero in the markup.
- How: A count-up that starts from 0 in the HTML shows false numbers to crawlers, screen readers and anyone whose script fails. Render the true values server-side and animate from them only as an enhancement inside @media (prefers-reduced-motion: no-preference).
- Satisfies: a11y-reduced-motion, perf-core-first, distinct-motion-authored
- Verification note: Written 2026-11-17 from the owner's review of hero mock-ups (the tells were a centred stack with a stats strip, a glow, an accent word and decorative labels); not yet built as a demo or audited, so the markup is general engineering knowledge.
