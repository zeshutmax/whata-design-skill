# Recipe: Brutalist, neo-brutalist and edgy styles that stay usable (`brutalist-hard-edge`)
Styles covered: brutalism, neo-brutalist, edgy
**Keep:** Black outlines, hard offset shadows, flat saturated fills, default-looking underlined links, raw tables and tabs, heavy grotesque or monospace type, a blunt voice.
**Avoid:** Headings, paragraphs and buttons in all capitals; stretched or squashed images; tabs, accordions and tables built from bare divs; a thick coloured stripe on one side of a rounded card; error messages that mock the user; shadows or fills as the only sign of a boundary or a state.
Keep the thick outlines, hard offset shadows, flat saturated blocks, raw tables and a sharp voice. Make the roughness come from borders, type weight and layout, not from shouting capitals, stretched images, bare div widgets or a shadow that is the only boundary.
**While designing:** Use ink on flat fills with verified contrast, 3px solid borders and hard shadows with zero blur, sentence-case headings and uppercase only for short letterspaced labels, object-fit cover for every image, real tab, accordion and table markup, a blue focus ring, and neutral literal error text.
## Verified palette: Brutalist and edgy, computed
- paper: #FFFFFF
- ink: #111111
- fill-yellow: #FFD600
- fill-pink: #FF90E8
- fill-blue: #A3C4FF
- fill-green: #B8F2A0
- link: #1D2BFF
- focus: #1D2BFF
- error: #C00000
- text-muted: #6B6B6B
- edgy-background: #0A0A0A
- edgy-accent: #C6FF00
- edgy-error: #FF3B30
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on paper | #111111 | #FFFFFF | 18.88:1 | 4.5:1 |
| muted text on paper | #6B6B6B | #FFFFFF | 5.33:1 | 4.5:1 |
| ink on yellow button | #111111 | #FFD600 | 13.37:1 | 4.5:1 |
| ink on pink card | #111111 | #FF90E8 | 9.36:1 | 4.5:1 |
| ink on blue chip | #111111 | #A3C4FF | 10.7:1 | 4.5:1 |
| ink on green chip | #111111 | #B8F2A0 | 14.61:1 | 4.5:1 |
| underlined link on paper | #1D2BFF | #FFFFFF | 7.39:1 | 4.5:1 |
| link on yellow card | #1D2BFF | #FFD600 | 5.23:1 | 4.5:1 |
| 3px ink border against paper (UI boundary) | #111111 | #FFFFFF | 18.88:1 | 3:1 |
| focus ring on paper | #1D2BFF | #FFFFFF | 7.39:1 | 3:1 |
| focus ring on yellow | #1D2BFF | #FFD600 | 5.23:1 | 3:1 |
| error text on paper | #C00000 | #FFFFFF | 6.48:1 | 4.5:1 |
| edgy: white text on near-black | #FFFFFF | #0A0A0A | 19.8:1 | 4.5:1 |
| edgy: acid accent on near-black | #C6FF00 | #0A0A0A | 16.69:1 | 3:1 |
| edgy: near-black text on acid button | #0A0A0A | #C6FF00 | 16.69:1 | 4.5:1 |
| edgy: error red on near-black | #FF3B30 | #0A0A0A | 5.58:1 | 4.5:1 |
## Steps
### Flat fills with near-black ink (`bk-palette`) [standard · verified]
Set flat saturated fills with near-black ink on top and check every pair. Ink #111111 on paper is 18.88:1, on yellow #FFD600 13.37:1, pink #FF90E8 9.36:1, blue #A3C4FF 10.7:1, green #B8F2A0 14.61:1. Links #1D2BFF are 7.39:1 on paper and 5.23:1 on yellow. Never put white text on these fills.
- How: Choose the fill for its saturation, then set the text to ink or paper, whichever passes, and recompute. The 3px ink border is 18.88:1 against paper, far above the 3:1 UI minimum, which is why thick outlines solve the boundary problem that thin grey outlines create. Edgy dark variant: white on #0A0A0A is 19.8:1, acid #C6FF00 is 16.69:1 (use as large text, icons or a button fill with #0A0A0A text at 16.69:1), and error red #FF3B30 is 5.58:1 for text. Harsh contrast is the look here, so none of it needs lowering. Rendered and measured in a Chrome demo: the computed colours match the claimed pairs.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Shout with weight, not uppercase (`bk-caps`) [craft-consensus · verified]
Get the shouting look from weight, size and tight tracking on sentence-case text, and keep uppercase for labels of three words or fewer. Never uppercase a heading of more than three words, a paragraph or a button label. Every uppercase label gets letter-spacing of 0.05em to 0.12em. Do not put a tracked uppercase label directly above the hero heading (distinct-eyebrow-restraint): place it after the heading or leave it out. Step the h1 in rem (2.5rem, 3.5rem from min-width: 40rem, 5rem from 64rem) instead of clamp() with vw, and put overflow-wrap: anywhere on headings, paragraphs, chips and buttons: heavy words overflowed the page by 67 px at 320 px with 200% text and text spacing until we did.
- How: Practical Typography: caps work for text shorter than a line and need letter-spacing of about 5 to 12 percent; GOV.UK content guidance: no block capitals for large amounts of text. The 40-character cut-off in the rule is our own review threshold. In the Chrome demo the label measures 0.08em and no heading or button is uppercase. Large lowercase headlines at weight 900 with -0.02em tracking already read as blunt.
- Satisfies: copy-no-all-caps-text, craft-caps-short-only, craft-caps-letterspacing
```css
h1, h2, h3, .btn { text-transform: none; font-weight: 900; }
h1 { letter-spacing: -0.02em; }
.label { text-transform: uppercase; letter-spacing: 0.08em; font: 700 1rem/1 ui-monospace, monospace; }
```
### Raw photos without stretching (`bk-images`) [craft-consensus · verified]
Make photos look raw with filters, hard crops, borders and a slight rotation, never with a stretched aspect ratio. Fit every image with object-fit: cover and an object-position that keeps the subject in view.
- How: MDN: the default object-fit: fill distorts; cover crops and contain letterboxes. A grayscale(1) contrast(1.3) filter, a 3px border and rotate(-2deg) give the harsh look without changing the ratio. Measured in Chrome: a 400x300 source in a 300x300 box with object-fit: cover keeps its proportions (cropped), while the same image with the default fill is the distorting case. Check small screens for the subject with object-position. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; a fixed width: 300px photo overflowed a 272 px content box at 320 px (right edge 329 px); width: min(300px, 100%) with aspect-ratio fixes it.
- Satisfies: craft-image-no-distortion
```css
.photo { width: min(300px, 100%); height: auto; aspect-ratio: 1; object-fit: cover; object-position: 50% 30%;
  border: 3px solid #111; filter: grayscale(1) contrast(1.3); transform: rotate(-2deg); }
```
### Hard shadow snap on press (`bk-press-motion`) [craft-consensus · partly-verified]
Use the snap of the hard shadow as the interaction: on hover or press the button moves toward its shadow in about 100 ms with a decelerating curve, and returns with an accelerating one. Do not use linear easing on the transform.
- How: NN/g: about 100 ms for feedback, ease-out for things appearing, ease-in for leaving, exits shorter than entrances. Material motion tokens: decelerate for enter, accelerate for exit. Measured in Chrome: transition-duration 0.1s and cubic-bezier(0, 0, 0.2, 1) on transform. Mapping the pressed state to "entering" and release to "leaving" is our interpretation. The 3 to 6 px translation is small, but wrap larger movement in prefers-reduced-motion.
- Satisfies: craft-motion-easing-direction
- Verification note: Duration and easing guidance are from the sources read; treating press as an entrance and release as an exit is our reading of the rule.
```css
.btn { transition: transform 100ms cubic-bezier(0, 0, 0.2, 1), box-shadow 100ms cubic-bezier(0, 0, 0.2, 1); }
.btn:hover  { transform: translate(-3px, -3px); box-shadow: 6px 6px 0 #111; }
.btn:active { transform: translate(3px, 3px);  box-shadow: 0 0 0 #111; }
```
### Underlined links, bordered buttons (`bk-controls`) [craft-consensus · verified]
Keep the raw default look of links and make it explicit: underline every inline link, give every button a fill and a 3px border, and keep targets at least 44 px tall (WCAG minimum is 24 by 24).
- How: An underlined link in a different colour passes the "not colour alone" test; Chrome demo measures underline on inline links and 44 px tall buttons and tabs. Do a grayscale screenshot: every link and button should still be findable.
- Satisfies: a11y-coga-controls-recognizable, a11y-target-size, a11y-color-not-only
### Hard shadow only on pressables (`bk-shadow-affordance`) [our-take · judgement]
Reserve the hard offset shadow for things you can press. Static cards, chips and stickers get the flat 3px border and a fill, with no shadow.
- How: In this style the shadow is what reads as raised and pressable. If a decorative card carries the same shadow as a button, a visitor cannot tell the two apart. Check the grayscale screenshot for anything non-interactive that looks like a control.
- Satisfies: a11y-coga-controls-recognizable
- Verification note: Our recommendation; COGA asks that non-interactive items do not look clickable, the shadow-as-affordance reading is ours.
### Outline focus, borders for forced colors (`bk-focus-forced`) [craft-consensus · verified]
Draw focus with an outline in a colour that contrasts with both paper and fills, not with the hard shadow, and keep the 3px borders so boundaries survive forced colours. Add a prefers-contrast: more token that thickens borders and darkens muted text.
- How: MDN: in forced-colors mode border-color and outline-color are kept as system colours while box-shadow becomes none, and :focus-visible indicators need 3:1. Focus ring #1D2BFF is 7.39:1 on paper and 5.23:1 on yellow. Measured in Chrome 156 with forced colours emulated: the button shadow computes to none and the 3px solid borders remain; with contrast: more emulated the border token becomes 5px and muted text turns to ink. Keyboard focus measured as a 4px solid #1D2BFF ring with 3px offset.
- Satisfies: a11y-focus-visible, craft-contrast-preferences, a11y-non-text-contrast
```css
:focus-visible { outline: 4px solid var(--focus); outline-offset: 3px; }
@media (prefers-contrast: more) { :root { --border: 5px; --muted: #111; } }
```
### Radius and elevation per role (`bk-tokens`) [craft-consensus · partly-verified]
Define radius and elevation per role: cards and inputs 0, buttons 8 px, tags pill, images 0; shadows sm (3px 3px 0) and md (6px 6px 0) with zero blur. Mark emphasis with a fill or a full border, not a thick coloured stripe on one side of a rounded card.
- How: The rule fails a page where every role shares one radius of 16 px or more, where three or more adjacent cards pair a hairline border with a blur of 32 px or more, or where a rounded element has one thick coloured side. Hard shadows have zero blur, so they pass by construction. If you want a left bar on a callout, use radius 0 on that element. Chrome demo: the roles compute to different radii, no element has a single thick side border with a radius of 4 px or more.
- Satisfies: distinct-radius-elevation-scale, distinct-no-side-stripe-border
- Verification note: Thresholds come from practitioner detectors and articles (one is rated low weight in sources.json); we measured the demo against the rule text, not against a standard.
### Raw look, real semantics (`bk-semantics`) [standard · verified]
Raw does not mean unstructured. Style the real patterns: a tablist with role=tab buttons, aria-selected on exactly one, aria-controls and a labelled tabpanel; accordion headers as h3 containing one button with aria-expanded; tables with a caption and th scope. Wrap a wide table in a focusable scroll region: div role=region, aria-label, tabindex=0, overflow-x: auto. Controls that only work with script (tab buttons, accordion buttons) must not exist without it: leave every panel visible in the HTML, keep the tablist hidden (with [hidden] { display: none !important } so no author display rule overrides it) or build the accordion button from the plain heading in the script, and make call-to-action buttons real links or form submits.
- How: Follow the ARIA Authoring Practices tabs and accordion patterns and Inclusive Components for tables and collapsible sections. Chrome demo checks: every tab sits in a named tablist, one aria-selected=true, each panel points back with aria-labelledby, ArrowRight moves selection and focus, tabindex=-1 on inactive tabs; the accordion button is the only child of its heading, aria-expanded flips on click and the collapsed panel is display:none so its links are not focusable; the table has a caption, th scope=col and scope=row. Native details/summary is a reasonable alternative but the rule check expects a button inside a heading. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; at 200% root text and 320 px a three-column table overflowed by 133 px (219 px with text spacing applied); the scroll wrapper removed the page-level overflow and axe accepted the focusable region.
- Satisfies: comp-tabs-semantics, comp-accordion-markup, comp-data-table-semantics
```html
<h3><button type="button" aria-expanded="false" aria-controls="a1" id="ab1">Can I export my data?</button></h3>
<div id="a1" role="region" aria-labelledby="ab1" hidden>...</div>
```
### Attitude in marketing, literal elsewhere (`bk-voice`) [craft-consensus · verified]
Let attitude live in marketing lines and keep a plain statement of the offer on the first screen. Errors, checkout, security and deletion text stays neutral and literal: say what the system needs, no jokes, no apology, none of invalid, incorrect, please, sorry, oops. Chips that are not a live status must not read New, Live or Beta, and warning or error icons are inline SVG, not emoji.
- How: Mailchimp: voice stays constant while tone shifts with the reader's state; NN/g and GOV.UK: errors are specific, non-blaming, without humour. Pattern for an empty field is "Enter your email address", for a wrong value "Card number must be 16 digits". A blunt headline ("Send invoices that get paid") sits next to a plain offer line. Chrome demo greps its error strings for the banned list and exclamation marks: none found.
- Satisfies: copy-no-idioms-puns, copy-error-no-blame-words, copy-tone-fits-context, a11y-coga-plain-literal-language
