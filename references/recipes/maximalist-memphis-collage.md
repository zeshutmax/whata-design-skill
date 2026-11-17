# Recipe: Maximalist, Memphis and collage layouts with order underneath (`maximalist-memphis-collage`)
Styles covered: maximalist, memphis-playful, collage
**Keep:** Many bright colours, geometric confetti, rotated cut-outs and stickers, layered shapes, big display type, dense compositions.
**Avoid:** Text directly on patterns or confetti; a link or error colour reused as decoration; more than two typefaces or ad hoc sizes and gaps; stretched cut-outs; dozens of equal-weight choices; cards that are a link wrapper around everything; modals built without dialog semantics; drifting shapes that never stop.
Keep the density, the confetti shapes, the clashing colours and the overlapping cut-outs. Put the noise in a decorative layer, keep text on solid plates, and hold a few quiet constants (two typefaces, a size scale, a spacing scale, a line length, one icon family) so the page reads as one loud system.
**While designing:** Choose a decorative palette separate from the link and error colours, put every line of text on a solid plate, fix two fonts, six to eight sizes and a 4 or 8 px spacing scale, cap text at 55ch inside a container of 1280px or less, and make the decorative layer aria-hidden, pausable and removed under reduced motion.
## Verified palette: Memphis maximalist, computed
- background: #FFFFFF
- band-lilac: #F4EEFF
- ink: #1A1033
- decor-yellow: #FFD23F
- decor-pink: #FF8FB8
- decor-teal: #7DE0D6
- decor-periwinkle: #B8A4FF
- decor-coral: #FF6B6B
- link: #2F27CE
- error: #B3261E
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on white | #1A1033 | #FFFFFF | 18.01:1 | 4.5:1 |
| ink text on lilac band | #1A1033 | #F4EEFF | 15.89:1 | 4.5:1 |
| ink on yellow plate | #1A1033 | #FFD23F | 12.47:1 | 4.5:1 |
| ink on pink plate | #1A1033 | #FF8FB8 | 8.47:1 | 4.5:1 |
| ink on teal plate | #1A1033 | #7DE0D6 | 11.58:1 | 4.5:1 |
| ink on periwinkle plate | #1A1033 | #B8A4FF | 8.4:1 | 4.5:1 |
| ink on coral chip (decor, small text) | #1A1033 | #FF6B6B | 6.49:1 | 4.5:1 |
| link text on white | #2F27CE | #FFFFFF | 9.12:1 | 4.5:1 |
| link text on lilac | #2F27CE | #F4EEFF | 8.04:1 | 4.5:1 |
| white on link-blue primary button | #FFFFFF | #2F27CE | 9.12:1 | 4.5:1 |
| error text on white | #B3261E | #FFFFFF | 6.54:1 | 4.5:1 |
## Steps
### Text on flat plates (`mx-plates`) [standard · verified]
Put the noise around the text, not under it. Every line of text sits on a flat plate or a plain band, and the shapes, stickers and patterns live in a decorative layer. Ink #1A1033 is 12.47:1 on yellow #FFD23F, 8.47:1 on pink #FF8FB8, 11.58:1 on teal #7DE0D6, 8.4:1 on periwinkle #B8A4FF, 6.49:1 on coral #FF6B6B, 18.01:1 on white.
- How: Never set text in a pastel on a pastel. Link blue #2F27CE is 9.12:1 on white and 8.04:1 on the lilac band. The decorative layer is a sibling element with position:absolute, z-index 0, pointer-events:none and aria-hidden="true". Rendered in Chrome: the computed colours of the demo's plates, bands, links and buttons match the claimed pairs.
- Satisfies: a11y-contrast-text
### Fix quiet constants first (`mx-tokens`) [craft-consensus · partly-verified]
Fix the quiet constants before adding colour: two font families (a display face and a body face), six to eight named type sizes, and a spacing scale on a 4 px base (4, 8, 12, 16, 24, 32, 48, 64, 96). Loudness comes from colour, shape and rotation, not from a new size or gap every time.
- How: Define the scales as custom properties and use only those. Measured in the Chrome demo: 5 distinct font sizes (14, 16, 20, 40, 64 px), 2 families, 7 distinct spacing values, every one a multiple of 4. The rule caps are 8 sizes, 2 families (advisory, our-take) and 12 spacing values.
- Satisfies: craft-type-scale-tokens, craft-font-families-few, craft-spacing-scale-tokens
- Verification note: Measured on a demo built to the scales; the two-family limit is an advisory our-take rule and the 8-size and 12-value caps are the rules' own thresholds, not studies.
```css
:root {
  --s1: 4px; --s2: 8px; --s3: 12px; --s4: 16px; --s5: 24px; --s6: 32px; --s7: 48px; --s8: 64px; --s9: 96px;
  --fs-xs: 1rem; --fs-sm: 1rem; --fs-md: 1.25rem; --fs-lg: 1.75rem; --fs-xl: 2.5rem; --fs-2xl: 4rem;
  --font-display: "Arial Black", Impact, sans-serif; --font-body: system-ui, sans-serif;
}
```
### Separate semantic and decorative palettes (`mx-colour-roles`) [craft-consensus · verified]
Keep two palettes apart. The semantic set (link, primary button, focus, error, success) is used only for those jobs; the decorative set (yellow, pink, teal, periwinkle, coral here) carries the Memphis energy. Link blue and error red never appear as a shape, border or text colour on non-interactive content.
- How: GOV.UK Design System: colours are assigned by function, and the focus colour is reserved. In the Chrome demo every element was scanned: link blue (#2F27CE) and error red (#B3261E) occur only on links, buttons and the error message; the five decorative colours appear on plates and shapes. Pick decorative hues that are visibly different from the link hue.
- Satisfies: craft-color-meaning-reserved
### 50ch text in a 1280 px container (`mx-measure-container`) [craft-consensus · verified]
Cap running text with max-inline-size around 50ch (not 55ch) and put the content in a centred container of 1280 px or less; let only the coloured band and decorative layer run edge to edge. Then count characters per line in the browser instead of trusting the number.
- How: Measured in Chrome 156 on macOS by counting characters on every rendered line: with max-inline-size 66ch, proportional faces gave 87 to 96 characters per line at most (system-ui and Georgia 96, Arial and Helvetica Neue 87), over the 75-character cap; 60ch gave 77 to 89, 55ch gave 69 to 83, 45ch gave 59 to 67, and 50ch gave a longest line of 67 to 74 (average 60 to 69). The reason is that 1ch is the width of the digit 0, wider than an average letter; only a monospace face gets about one character per ch. So 50ch is the safe value for system-ui, Arial, Georgia, Helvetica Neue and Arial Narrow; other platforms' fonts were not measured. In the demo the longest line is 70 characters at 768, 1280 and 1920 px and the container is 1280 px at a 1920 px viewport while the band is 1920 px wide.
- Satisfies: craft-measure-body, craft-container-max-width
```css
.prose { max-inline-size: 50ch; }          /* about 60-70 characters in proportional faces; verify */
.wrap  { max-inline-size: 1280px; margin-inline: auto; }  /* the band behind it is full-bleed */
```
### Tight inside groups, loose between (`mx-grouping`) [our-take · judgement]
Dense is not the same as unstructured. Keep the gap inside a group (heading to its content, 16 px) clearly smaller than the gap between groups (48 px), including across overlapping or rotated pieces.
- How: Proximity tells the eye what belongs together when colour and shape are all loud. Check each heading: margin above greater than margin below, and the internal gap of a card smaller than the gap to its neighbour. The demo measures 16 px inside groups against 48 px between them.
- Satisfies: craft-group-by-proximity
- Verification note: The rule is labelled our-take; Apple and Butterick support heading proximity but not the exact gaps.
### Dense page, about five choices (`mx-choices`) [craft-consensus · verified]
Let the page be visually dense while each viewport-height section offers one dominant action and at most about five choices in total. Move the rest to a footer or a titled "more" link.
- How: The COGA guidance and NN/g homepage principles favour one clearly dominant feature. The demo hero has five controls: one filled primary button, three secondary and one text link, counted in Chrome.
- Satisfies: a11y-coga-limit-choices-per-screen
### One icon family on one grid (`mx-icons`) [craft-consensus · verified]
Use one icon family at one stroke weight, corner style and fill treatment on a shared grid (24 px, stroke 2, round caps and joins, stroke currentColor). Stickers, confetti and illustrations are decoration, not icons, and may be as wild as you like. Status and warning icons are inline SVG from the same family, never emoji (distinct-real-imagery-and-icons).
- How: Apple HIG: same size, detail and stroke weight across a set, with stroke matched to adjacent text. web.dev: inline SVG so CSS can style it. Chrome demo: all three icons share stroke-width 2, round linecap and linejoin, no fill and a 24x24 viewBox.
- Satisfies: craft-icons-one-family
### Cards as list items with stretched link (`mx-cards`) [our-take · verified]
Make each card a list item with one heading level and one link inside the heading; stretch the click area with a ::after pseudo-element. Draw the focus indication on the link itself (a background and a thicker underline), and keep a ring on the card with :has(a:focus-visible) as a bonus. Decorative card images get alt="".
- How: Inclusive Components cards pattern. Tested in Chrome: each li has one link inside h3, clicking the lower part of the rotated card follows the link, and keyboard focus on the link draws a solid 3px outline on the card. A rotated card's bounding box is larger than the card, so click inside the shape when testing. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; a version that removed the link's outline and drew the ring only on the card through :has() failed a11y-focus-visible on 3 of 9 Tab stops, because the probe (and a person using forced colours) looks at the focused element itself; adding a background and underline change on the link itself fixed it.
- Satisfies: comp-card-single-primary-link
- Verification note: Behaviour tested in Chrome 156; the Inclusive Components page entry in sources.json has no notes, so the pattern details beyond the rule text are from our own testing.
```css
.card { position: relative; }
.card a::after { content: ""; position: absolute; inset: 0; }
.card:has(a:focus-visible) { outline: 3px solid var(--ink); outline-offset: 3px; }
.card a:focus-visible { outline: none; background: var(--yellow); text-decoration-thickness: 3px; }
```
### Native dialog with showModal (`mx-dialog`) [standard · verified]
Build modals with a native dialog opened by showModal(), named by aria-labelledby pointing at its visible title, with every control inside it. Style the dialog and ::backdrop as loudly as you like.
- How: ARIA Authoring Practices modal dialog: focus moves in, Tab stays inside, Escape closes, focus returns. Measured in Chrome 156: after showModal() the dialog matches :modal, focus is inside, the accessibility tree exposes a dialog named "Delivery details", six Tab presses stay inside, an outside button cannot take focus, and Escape returns focus to the opener. The demo also sets aria-modal="true" because the rule check looks for it; with showModal() the page behind is genuinely blocked, so the attribute is truthful.
- Satisfies: comp-dialog-semantics
```html
<dialog id="dlg" aria-labelledby="dlg-title" aria-modal="true">
  <h2 id="dlg-title">Delivery details</h2>
  <p>...</p>
  <button type="button" id="close">Close delivery details</button>
</dialog>
```
### Rotate and crop without stretching (`mx-images`) [craft-consensus · verified]
Rotate, overlap and crop cut-outs freely, but with transforms that only rotate or translate, and fit each image with object-fit: contain for cut-outs or cover for cropped photos, never fill.
- How: MDN object-fit: fill (the default) distorts. A transform of rotate() keeps scale at 1; measured in Chrome by decomposing the computed matrix of each collage image: scale 1 by 1 on both, object-fit contain and cover. Transparent PNG, AVIF or SVG cut-outs go in <img> with a real alt text when they carry meaning.
- Satisfies: craft-image-no-distortion
### Pausable confetti, reduced-motion off (`mx-motion`) [standard · verified]
Give drifting confetti an off switch and an off state: a visible "Pause decoration" toggle with aria-pressed, a prefers-reduced-motion block that removes the animation, and no flashing. Never let the movement run behind text without these.
- How: WCAG 2.2.2: automatically starting movement lasting more than five seconds beside other content needs pause, stop or hide. Chrome demo: three drifting shapes run on an infinite 8 s loop; the button pauses all three (playState paused, aria-pressed true); with reduced motion emulated no animation exists. The toggle keeps one stable label and uses aria-pressed.
- Satisfies: a11y-reduced-motion, a11y-pause-stop-hide
### Collage with CSS, not reordering (`mx-order`) [standard · verified]
Collage by CSS, not by reordering. Keep DOM order equal to reading order, use grid or absolute placement for overlap, avoid CSS order, row-reverse and positive tabindex, and let the layout collapse to one column at 320 px with no horizontal scroll. Give h1 to h3 overflow-wrap: anywhere and size grid tracks as minmax(min(14rem, 100%), 1fr), because large display words and fixed tracks overflow at 320 px when text is zoomed to 200%.
- How: MDN: CSS order changes only the visual order, not the logical or tab order; WCAG 1.3.2 and 1.4.10. Chrome demo: no element has order other than 0, flex-direction reverse or tabindex above 0, and document width equals viewport width at 320, 768, 1280 and 1920 px. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; with root text at 200% and 320 px the page scrolled 180 px sideways (the word 'patterns' at 4rem is about 594 px wide; a 12rem track is 384 px); it passed at 100% text.
- Satisfies: a11y-meaningful-sequence, a11y-reflow
### Loud shapes, literal copy (`mx-copy`) [craft-consensus · verified]
Memphis energy goes in colour and shape. Keep headlines, labels and buttons literal, errors neutral ("Enter a delivery postcode") and payment or account copy free of jokes; save the wordplay for a supporting line.
- How: Same sources and tests as the playful-quirky-voice recipe: NN/g error guidance (non-blaming, no humour), GOV.UK error wording, Mailchimp on tone shifting with the reader's state. The demo error string contains none of invalid, incorrect, please, sorry, oops or an exclamation mark.
- Satisfies: copy-no-idioms-puns, copy-error-no-blame-words, copy-tone-fits-context
