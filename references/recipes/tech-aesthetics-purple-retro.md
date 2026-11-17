# Recipe: Futuristic, purple-led and retro-computing looks without the default tells (`tech-aesthetics-purple-retro`)
Styles covered: futuristic-tech, hue-purple, retro-computing
**Keep:** Thin lines, grids, data motifs, a committed purple, pixel type, terminal windows, phosphor colours, stepped animation.
**Avoid:** Violet-to-blue gradients and cyan on near-black as defaults; chromatic zero-offset glow; pulsing Live or New or version pills that report nothing; endless blinking cursors and CRT flicker; scanline overlays that eat text contrast; hairlines that carry meaning below 3:1.
Keep the precision, the single bold hue and the terminal nostalgia. Pick an accent from the brand instead of violet or cyan, replace glow with hairlines and flat fills, show status only when it is true, and make pixel and CRT effects finite, measured and motion-safe.
**While designing:** State the accent hue and why in the direction file, use flat accents on graphite (orange, lime, amber, green) or a solid committed purple with an exception record, draw depth with hairlines and neutral shadows, bind any status text to real data, and measure the contrast of text under scanlines.
## Verified palette: Graphite signal, committed purple and phosphor, computed
- graphite: #0E0F11
- panel-surface: #15161A
- text: #F4F4F5
- text-muted: #9A9AA2
- meaningful-line: #6B6B75
- decorative-grid: #2A2A30
- accent-signal-orange: #FF5B1F
- purple-deep: #4C1D95
- purple-text-on-white: #5B21B6
- purple-partner-sun: #FFE45E
- purple-soft-text: #E9D5FF
- phosphor-amber: #FFB000
- phosphor-amber-ground: #1A1100
- phosphor-green: #33FF66
- phosphor-green-ground: #001A0A
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| futuristic: text on panel surface | #F4F4F5 | #15161A | 16.45:1 | 4.5:1 |
| futuristic: muted text on panel surface | #9A9AA2 | #15161A | 6.47:1 | 4.5:1 |
| futuristic: signal-orange accent on panel surface (large text, icons, UI) | #FF5B1F | #15161A | 5.83:1 | 3:1 |
| futuristic: graphite text on signal-orange button | #0E0F11 | #FF5B1F | 6.18:1 | 4.5:1 |
| futuristic: input edge on panel surface (UI boundary) | #6B6B75 | #15161A | 3.43:1 | 3:1 |
| purple brand: white on deep purple | #FFFFFF | #4C1D95 | 10.95:1 | 4.5:1 |
| purple brand: sun-yellow on deep purple | #FFE45E | #4C1D95 | 8.61:1 | 4.5:1 |
| purple brand: pale lilac text on deep purple | #E9D5FF | #4C1D95 | 8.05:1 | 4.5:1 |
| purple brand: purple link on white | #5B21B6 | #FFFFFF | 8.98:1 | 4.5:1 |
| purple brand: deep purple on yellow button | #4C1D95 | #FFE45E | 8.61:1 | 4.5:1 |
| retro: amber phosphor on dark brown-black | #FFB000 | #1A1100 | 10.2:1 | 4.5:1 |
| retro: green phosphor on dark green-black | #33FF66 | #001A0A | 13.57:1 | 4.5:1 |
## Steps
### Flat accent from the brand (`ft-accent`) [craft-consensus · partly-verified]
Take the accent hue from the brand or subject and state it in the direction file. On graphite #0E0F11 use a flat signal colour instead of violet gradients or cyan: orange #FF5B1F (5.83:1 on the #15161A panel, graphite text on an orange button 6.18:1), lime #C8F169 (14.83:1), amber or phosphor green.
- How: The rule flags any gradient stop or primary accent with a hue of 260 to 310 degrees and a cyan accent on a near-black ground, unless the brand is that colour and the direction file says so. We ran that hue test in code over the demo's accents: orange is at 16 degrees, so nothing is flagged. Orange is not a neutral choice either: pick the hue because it is the brand or the subject, not because it avoids the check.
- Satisfies: distinct-no-ai-palette
- Verification note: The hue band and the cyan-on-black condition come from practitioner detectors and articles (some rated low weight); contrast and hue arithmetic were computed.
### Purple as a solid, not gradient (`ft-purple`) [our-take · judgement]
If purple is the brand, commit to it as a solid, not a gradient, and record the exception. Deep purple #4C1D95 gives white 10.95:1, sun yellow #FFE45E 8.61:1 and pale lilac #E9D5FF 8.05:1; on white the link purple #5B21B6 is 8.98:1 and deep purple on a yellow button is 8.61:1. Pair it with a warm partner (yellow), not a blue or pink gradient.
- How: The rule exempts a purple that is the brand when the direction file says so. The demo section is a flat #4C1D95 (hue 264, inside the 260 to 310 band), computed background-image none, which is why it needs the record. Example record: "Primary colour #4C1D95. Purple chosen because the studio's riso inks are violet and yellow; no gradients." The tag hue-purple only describes that purple is dominant; the exception is what stops it reading as the default. Note: the audit's distinct-no-ai-palette reports purple text pairs in the 260 to 310 degree hue band as a minor even when the exception is recorded in direction.md; accept that minor in writing, it is not a failure of the recipe.
- Satisfies: distinct-no-ai-palette, a11y-contrast-text
- Verification note: Contrast figures are computed; the advice to commit to a flat purple with a warm partner and to write the exception record is our judgement.
```text
direction.md
Accent: #4C1D95 (violet), partner #FFE45E (yellow).
Exception to distinct-no-ai-palette: purple is the brand (violet riso ink). Flat fills only, no violet-to-blue gradient.
```
### Hairlines and flat fills, not glow (`ft-no-glow`) [craft-consensus · partly-verified]
Build the precise, technical feel from hairlines, grids and flat fills instead of glow. Use a 1px border (#2A2A30 on graphite for decoration), a neutral shadow such as 0 1px 0 rgb(0 0 0 / .4), and keep any coloured halo only where it encodes a state. Draw focus as an outline, not a glow.
- How: The rule flags a chromatic box-shadow or text-shadow with zero offset and blur of 3 px or more, and a saturated radial-gradient halo behind a hero on a dark page. We implemented that check in Chrome: the demo has no such shadow or radial gradient, and a deliberately added 0 0 12px #39FF88 shadow is flagged. A glow that shows selection or error is allowed by the rule; here state is shown by outlines and text.
- Satisfies: distinct-no-decorative-glow
- Verification note: Rule thresholds are from practitioner detectors; verified only against the rule text on a demo page.
### Only true, current status labels (`ft-status`) [craft-consensus · partly-verified]
Show a status label only when it reports something true and current: render the release line from the release record at build time with a real date, link it to the changelog, and drop pulsing dots and "Live", "New" or "Beta" pills that nothing updates.
- How: The rule flags pulsing status dots, pills reading new, live, beta or a version number in the first viewport unless bound to a data attribute or release record, and a pill chip above the hero heading. Chrome demo: no element under 1.5 aspect ratio has an infinite animation, no pill matches, and the release line carries a data-source attribute and a time element with a datetime. If something really is live, use role="status" on the text that changes.
- Satisfies: distinct-no-fake-status-badges
- Verification note: Rule is from practitioner sources; the data-binding pattern is our implementation of the rule's exception.
```html
<p class="status" data-source="releases.json#latest">Release 2.4.1 · <time datetime="2026-10-28">28 October 2026</time></p>
```
### Meaningful thin lines at 3:1 (`ft-lines`) [standard · verified]
Thin and technical must still be legible: hold lines that carry meaning (input edges, chart axes, dividers that separate controls) at 3:1, and keep decorative grids below that. The input edge #6B6B75 is 3.43:1 on the panel and 3.64:1 on graphite; the decorative grid #2A2A30 is not meant to be seen as content. Text: #F4F4F5 16.45:1 and muted #9A9AA2 6.47:1 on the panel.
- How: WCAG 1.4.11 for UI components and graphics; the Enhanced Contrast Understanding page notes that thin fonts render fainter, so use heavier weights or exceed the minimum. Use font-weight 400 or above for small light-on-dark text. Computed colours of the demo's text, accent, button and input edge match the claimed pairs in Chrome.
- Satisfies: a11y-non-text-contrast, a11y-contrast-text
### Skip link and main in terminal layouts (`ft-bypass`) [standard · verified]
Terminal and retro-computer layouts built from stacked panels still need a skip link as the first focusable element and a main landmark around the content; panels are sections with headings, not bare divs.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; the demo page failed a11y-bypass-blocks with 'no skip link and no main landmark' until a Skip to content link (visible on focus, high contrast) and main id=main were added.
- Satisfies: a11y-bypass-blocks
### Self-hosted pixel face at grid multiples (`rc-pixel-type`) [our-take · judgement]
Self-host the pixel face and set it in rem at whole multiples of its design grid (an 8 px font at 16 or 24 px), use it for headings and labels, and keep long text in a plain monospace or sans face. Draw pixel art as images with image-rendering: pixelated at integer scales (an 8 px sprite shown at 64 px), with alt text or alt="".
- How: WCAG 1.4.4 asks for 200% resize and lists viewport-unit-only sizing as a failure (F94), so size in rem. Integer multiples keep pixel edges crisp; that advice and the legibility of pixel fonts for body text are our judgement and were not measured. Chrome computes image-rendering: pixelated for the demo sprite. The MDN image-rendering page is not in sources.json.
- Satisfies: a11y-resize-text, a11y-contrast-text
- Verification note: Resize rule is verified from WCAG pages; the pixel-grid multiples and body-text advice are our judgement.
### Phosphor colors that pass contrast (`rc-phosphor`) [standard · verified]
Use phosphor colours on dark grounds that pass: amber #FFB000 on #1A1100 is 10.2:1 and green #33FF66 on #001A0A is 13.57:1. Skip cyan on near-black; for dim secondary text keep at least 4.5:1 (for example #9A7A33 on #1A1100 is 4.63:1).
- How: Amber (hue 41) and green (hue 135) are outside the 260 to 310 band and are not cyan. Rendered colours in the Chrome demo match the claimed pairs.
- Satisfies: a11y-contrast-text, distinct-no-ai-palette
### Finite CRT and cursor effects (`rc-crt-blink`) [standard · verified]
Keep CRT and cursor effects finite, static where possible and measured. Blink the cursor for four 1 s cycles with steps(1) and leave it visible; run a typed reveal once as a clip-path inset() animation with steps(), never by animating a fixed width with overflow:hidden and white-space:nowrap (that clips under WCAG text spacing and overflows at 200% text); skip flicker; remove all of it under prefers-reduced-motion. A scanline overlay is pointer-events:none and aria-hidden; 12% black stripes cost amber text only down to 7.88:1.
- How: WCAG 2.2.2 covers blinking that lasts more than five seconds beside other content (4 s here); WCAG 2.3.1 passes at no more than three flashes per second (1 per second here). Measured in Chrome 156: the cursor animation computes to 1s, 4 iterations, steps(1); with reduced motion emulated no animation exists. A solid block of text colour under the overlay rendered at rgb(224,155,0) for amber and rgb(45,224,90) for green, against the plain backgrounds 7.88:1 and 10.35:1. Computed: at 30% stripes amber text falls to 5.12:1 and at 20% it is 6.56:1, so keep the overlay at 20% or less. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; the width/overflow:hidden/nowrap typed reveal failed a11y-text-spacing (1 element at 1440 px, 1 more at 320 px) and overflowed by 280 px at 200% text; the clip-path version passed.
- Satisfies: a11y-pause-stop-hide, a11y-flashes, a11y-reduced-motion
```css
.cursor { animation: blink 1s steps(1, end) 4; }
@keyframes blink { 50% { opacity: 0; } }
.typed { overflow-wrap: anywhere; animation: type 1.2s steps(24, end) 1 both; }
@keyframes type { from { clip-path: inset(0 100% 0 0); } to { clip-path: inset(0); } }
.term::after { content: ""; position: absolute; inset: 0; pointer-events: none;
  background: repeating-linear-gradient(0deg, rgb(0 0 0 / .12) 0 1px, transparent 1px 3px); }
@media (prefers-reduced-motion: reduce) { .cursor, .typed { animation: none; } }
```
### Easing for windows, steps for sprites (`rc-easing`) [craft-consensus · partly-verified]
Keep the 8-bit snap where it belongs and use proper easing for the windows: a window opens in 150 ms with a decelerating curve and closes in 100 ms with an accelerating one; reserve steps() for frame-by-frame sprites and typed text, never linear on a moving window.
- How: NN/g and Material motion: enter with ease-out, leave with ease-in, exits shorter than entrances; linear is for non-spatial or looping motion. Measured in Chrome: open state computes to 0.15s cubic-bezier(0, 0, 0.2, 1) and the closed state to 0.1s cubic-bezier(0.4, 0, 1, 1); the typed reveal is steps(24). Whether stepped easing on a revealed width counts as spatial linear motion is not settled by the rule; steps() is not "linear", so the rule check passes.
- Satisfies: craft-motion-easing-direction
- Verification note: Durations and curve directions match the sources; the treatment of steps() under the rule is our reading.
```css
.win { transition: transform 100ms cubic-bezier(.4, 0, 1, 1), opacity 100ms cubic-bezier(.4, 0, 1, 1); }
.win.open { transition-duration: 150ms; transition-timing-function: cubic-bezier(0, 0, .2, 1); }
.typed { animation: type 1.2s steps(24, end) 1 both; }
```
### OS window chrome from real controls (`rc-os-window`) [standard · verified]
Make OS-window chrome out of real controls: buttons with accessible names ("Close window", not an X glyph alone), at least 44 px square, with a visible focus outline, inside a labelled dialog or region.
- How: Tiny title-bar buttons are the usual retro-computing target-size failure. Chrome demo: the close button is a button with aria-label "Close window", measures at least 44 by 44 px once its open transition finishes and shows a solid 3px outline on keyboard focus. WCAG 2.5.8 requires 24 by 24 px or spacing.
- Satisfies: a11y-focus-visible, a11y-target-size, a11y-name-role-value
