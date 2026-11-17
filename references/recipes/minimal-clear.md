# Recipe: Minimal and quiet-luxury pages that remain clear and usable (`minimal-clear`)
Styles covered: minimal, quiet-luxury, hero-type-only, poster
**Keep:** Whitespace, small type, few elements, muted palette.
**Avoid:** Light gray text, borderless inputs, placeholder-only labels, tiny icon links, a first screen that looks finished when it is not.
Keep the whitespace and restraint. Restraint must not remove contrast, borders, focus, hit areas, labels or the hint that more content exists.
**While designing:** Keep muted text at 4.5:1 or better, borders and controls at 3:1, show a clear focus ring, use 24 px minimum targets, visible labels, a one-line purpose with a primary action in the first viewport, and a cue that more content follows.
## Verified palette: Off-white minimal, verified
- background: #FAFAF7
- text: #1A1A18
- text-muted: #6A6A64
- input-border: #8C8C85
- focus: #1A1A18
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| text on off-white | #1A1A18 | #FAFAF7 | 16.67:1 | 4.5:1 |
| muted text on off-white | #6A6A64 | #FAFAF7 | 5.2:1 | 4.5:1 |
| input border on off-white | #8C8C85 | #FAFAF7 | 3.24:1 | 3:1 |
| focus ring on off-white | #1A1A18 | #FAFAF7 | 16.67:1 | 3:1 |
## Steps
### Keep muted text at 4.5:1 (`mn-contrast`) [craft-consensus · verified]
Keep secondary text at or above 4.5:1; #6A6A64 on #FAFAF7 is verified. Do not lighten muted text further for elegance.
- How: Check every gray in the palette against every background it touches.
- Satisfies: a11y-contrast-text
### Visible field edges at 3:1 (`mn-borders`) [craft-consensus · verified]
Give form fields and controls a visible edge at 3:1 or better; a hairline at #8C8C85 on #FAFAF7 is verified.
- How: A subtle fill is fine only if it meets 3:1 against the page.
- Satisfies: a11y-non-text-contrast
### Solid offset focus ring (`mn-focus`) [craft-consensus · verified]
Make focus obvious: a solid ring in the text color with an offset suits a minimal style.
- How: Use :focus-visible (Baseline widely available since March 2022) so the browser decides when the ring shows. MDN: the indicator needs at least 3:1 contrast (WCAG 1.4.11) and must not simply be removed. In forced-colors mode outline-color and border-color are forced to system colors and stay visible, but box-shadow is forced to none, so draw the ring with outline (as below) and do not rely on box-shadow alone. MDN advises against building a separate forced-colors design; do not use forced-color-adjust to override users' colors.
- Satisfies: a11y-focus-visible
```css
:focus-visible {
  outline: 3px solid var(--focus);   /* 3:1 or better on every background it sits on */
  outline-offset: 3px;
}
```
### Targets of at least 24 px (`mn-targets`) [craft-consensus · verified]
Keep targets at least 24 by 24 CSS pixels, or spaced so a 24 px circle around each fits without overlap; give small text links padding.
- How: WCAG spacing exception: a 24 px circle centered on each undersized target must not intersect another target or another undersized target's circle; WCAG's example is 20×20 px buttons with a 4 px gap passing, and with no gap failing. Other exceptions: an equivalent control, inline text links, user-agent controls, essential targets. Pad icon buttons and footer links rather than enlarging the glyph.
- Satisfies: a11y-target-size
### Visible label on every field (`mn-labels`) [craft-consensus · verified]
Keep a visible label on every field; use placeholders only for examples.
- How: Float labels are acceptable only if the label stays visible after input.
- Satisfies: ux-form-no-placeholder-label
### One line, one action, a cue (`mn-purpose-and-floor`) [our-take · verified]
Say what the page is and what to do in one line plus one primary action in the first viewport, and show a cut-off element or cue that more content follows.
- How: A restrained first screen is fine; an unexplained one is not. Let the next section peek in at the bottom edge.
- Satisfies: ux-purpose-clear, ux-primary-cta-above-fold, ux-false-floor
### Wire tabs to their panels (`minimal-clear--comp-tabs-semantics`) [craft-consensus · verified]
Give the tablist an aria-label, link every tab to its panel with aria-controls and aria-labelledby, and keep aria-selected in sync with the visible active state.
- How: Query the DOM: every [role=tab] is a child of [role=tablist]; exactly one tab has aria-selected=true; each tab aria-controls resolves to a [role=tabpanel] whose aria-labelledby resolves to that tab; tablist has aria-label or aria-labelledby. Confirm with a screen reader that the selected state is announced. (Derived from the rule; see its sources.)
- Satisfies: comp-tabs-semantics
### Accordions as heading plus button (`minimal-clear--comp-accordion-markup`) [craft-consensus · partly-verified]
Write accordions as h3 > button[aria-expanded] followed by a div that gets the hidden attribute when collapsed.
- How: For each toggle: tagName is BUTTON, parent is h1-h6 (or role=heading with aria-level), the button is the heading's only child, aria-expanded is 'true' or 'false' and flips on click, the hidden panel is display:none or [hidden] when collapsed. (Derived from the rule; see its sources.)
- Satisfies: comp-accordion-markup
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Prefer visible labels over tooltips (`minimal-clear--comp-tooltip-not-sole-label-no-interactive`) [craft-consensus · partly-verified]
Prefer visible labels; if a tooltip is unavoidable, trigger on hover and focus, allow Escape, and keep it text only.
- How: Hover and Tab to each tooltip trigger; press Escape; move the pointer onto the bubble; check aria-describedby; check the bubble DOM for a, button, input. (Derived from the rule; see its sources.)
- Satisfies: comp-tooltip-not-sole-label-no-interactive
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Show toggle state beyond color (`minimal-clear--comp-toggle-visual-state-not-color`) [craft-consensus · partly-verified]
Style toggles from [aria-pressed=true] and add a knob position or check icon, not only a color change.
- How: Grayscale screenshot of both states; confirm still distinguishable. Check CSS selectors key off aria-pressed/aria-checked/:checked. (Derived from the rule; see its sources.)
- Satisfies: comp-toggle-visual-state-not-color
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Short words, check reading grade (`minimal-clear--copy-reading-grade`) [craft-consensus · partly-verified]
Use short, common words and one clause per sentence, then check the grade score before finishing.
- How: Run Flesch-Kincaid grade (Hemingway, Word, or a script) on the concatenated body copy of each page, excluding proper names and titles. Fail above 9 for general audiences unless the brief names an expert audience. (Derived from the rule; see its sources.)
- Satisfies: copy-reading-grade
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Spell out acronyms and brand names (`minimal-clear--copy-jargon-acronyms`) [craft-consensus · partly-verified]
Write the full phrase the first time and in every heading or button, and describe each branded name in plain words next to it.
- How: Extract all-caps tokens of 2 or more letters and capitalised product names from headings, nav and buttons; confirm each is expanded or described adjacent. Confirm first body use is expanded. Whitelist PDF, FAQ, URL. (Derived from the rule; see its sources.)
- Satisfies: copy-jargon-acronyms
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headline as one buyer's result (`minimal-clear--copy-headline-swap-test`) [craft-consensus · partly-verified]
Write the headline as the result one named buyer gets, using a noun or number only this product can claim.
- How: Read the H1 and subhead alone. (1) Does it say what is offered and for whom? (2) Paste it with a competitor's name: does it still read true? If yes, fail. (3) Fail if it matches the template 'The [AI-powered|modern|all-in-one] [noun] for [teams|businesses|everyone]'. (Derived from the rule; see its sources.)
- Satisfies: copy-headline-swap-test
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headings that state the finding (`minimal-clear--copy-heading-informative`) [craft-consensus · partly-verified]
Write each heading as the finding of its section, so the headings alone tell the story.
- How: Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (Derived from the rule; see its sources.)
- Satisfies: copy-heading-informative
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Buttons labelled verb plus object (`minimal-clear--copy-button-verb-label`) [craft-consensus · partly-verified]
Label each button with a verb plus its object ('Book a demo', 'Download the price list').
- How: Collect text of button, [role=button], input[type=submit] and .btn-like links. Fail if the first word is not a verb (use a verb list), if the word count is over 4, or if the label matches the blocklist: submit, ok, click here, learn more, get started, go, continue (unless a save step is stated). (Derived from the rule; see its sources.)
- Satisfies: copy-button-verb-label
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Link text names the destination (`minimal-clear--copy-link-text-unique-destination`) [craft-consensus · partly-verified]
Write link text that names the destination and say 'PDF, 2 MB' or 'opens in a new window' when it applies.
- How: Collect all anchors with accessible names. Fail if two different hrefs share the same name, if a name matches /^(click here|here|more|read more|link|this)$/i or contains 'link', if an href ends in a document extension without format and size in the name, or if target=_blank lacks a notice placed after the main text. (Derived from the rule; see its sources.)
- Satisfies: copy-link-text-unique-destination
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Specific, actionable error text (`minimal-clear--copy-error-specific-actionable`) [craft-consensus · partly-verified]
Start empty-field errors with a verb ('Enter your email address') and wrong-value errors with the field name plus 'must be'.
- How: Trigger every validation and failure state (empty, wrong format, too long, network failure, server error). Fail any message that does not name the problem and a fix, matches the generic list, or shows a raw code. Automated part: grep message strings for the generic list. (Derived from the rule; see its sources.)
- Satisfies: copy-error-specific-actionable
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Facts instead of adjectives (`minimal-clear--copy-specific-over-abstract`) [craft-consensus · partly-verified]
For every adjective, write the fact that made you choose it and use the fact instead.
- How: Grep for the abstract-adjective list. For each hit, require a number, a named object or a verifiable example in the same sentence, otherwise rewrite. Check that no three feature cards share the same structure of icon, two-word title and filler sentence. (Derived from the rule; see its sources.)
- Satisfies: copy-specific-over-abstract
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Cap line length near 55ch (`minimal-clear--craft-measure-body`) [craft-consensus · partly-verified]
Wrap every block of running text in a container with max-inline-size of about 45ch to 55ch for proportional fonts (never wider than 60ch), and let the container, not the viewport, decide the line length; then count characters per line in the browser.
- How: Measured 2026-11-06 in Chrome on macOS: ch is the width of the digit 0, wider than an average letter, so 66ch gave 87 to 96 characters per line (system-ui, Georgia, Arial, Helvetica Neue), 60ch gave 77 to 89, 55ch gave 69 to 83, 50ch gave 67 to 74 and 45ch gave 59 to 67. Use 50ch to 55ch and verify the real count with the audit. Other platforms' fonts were not measured.
- Satisfies: craft-measure-body
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Body text at 1rem or larger (`minimal-clear--craft-body-size-min`) [craft-consensus · partly-verified]
Set the body size to 1rem (16px) or larger, sized up (17-20px) for long reading, and use smaller sizes only for captions and legal lines.
- How: At 320 and 1280 px, collect computed font-size of every text node inside p, li, td, label, input, textarea, select, button. Fail when any is under 16px, unless the node is inside figcaption, small, footer legal text or a caption. List every text node under 14px for manual review (14px is our review threshold, not from a source). (Derived from the rule; see its sources.)
- Satisfies: craft-body-size-min
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Stepped rem sizes for headings (`minimal-clear--craft-fluid-type-rem-clamp`) [craft-consensus · verified]
Set headline sizes in rem and step them at em/rem media queries (for example 3rem, 4rem, 7rem), keeping the smallest at least 40% of the largest; do not use clamp(rem + vw) for text that must scale; test at 200% zoom and 320 px.
- How: Measured in Chrome 2026-11-05 (content/learn/measurements/type-zoom-2026-11-05.json): clamp(rem + vw) and vw sizes did not reach 200% at 200% zoom; stepped rem with small >= 40% of large did. See also step bt-scalable in big-type-and-modes.
- Satisfies: craft-fluid-type-rem-clamp
### Breakpoints where content breaks (`minimal-clear--craft-breakpoints-content-based`) [craft-consensus · partly-verified]
Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- How: Sweep the viewport from 320 to 1920 px in 40px steps. At each step assert no horizontal scrollbar (scrollWidth <= clientWidth), no element overlapping its sibling's box, and the measure rule still passes. Inspect media queries: list breakpoint values and flag any matching device presets (375, 414, 768 and 1024 px) written in px for review. (Derived from the rule; see its sources.)
- Satisfies: craft-breakpoints-content-based
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Wrap headings and button links (`mn-reflow-200`) [standard · verified]
Give display headings overflow-wrap: anywhere (a 3rem h1 is 96 px at 200% text and a word such as 'Furniture' is about 400 px wide) and give button-like links max-width: 100% with overflow-wrap: anywhere.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; the page scrolled 215 px sideways at 320 px with 200% text and a link collapsed to 12 px under the text-spacing overrides; both were gone after the change.
- Satisfies: a11y-reflow
