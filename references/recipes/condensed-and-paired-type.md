# Recipe: Condensed display type and serif-sans pairings (`condensed-and-paired-type`)
Styles covered: condensed, mixed-pairing
**Keep:** Narrow, tall display faces set large and tight; a deliberate serif and sans pairing; strong size and weight contrast.
**Avoid:** Whole headlines or buttons in capitals; capitals with no letter-spacing; a third or fourth family added for flavour; condensed faces used for paragraphs; fixed-height boxes that clip when users loosen text spacing; font swaps that move the layout.
Keep the tall, tight display lines and the contrast between two typefaces. Set condensed headlines in sentence case, limit capitals to short labels with real letter-spacing, stay at two families, and make sure fallback fonts do not shift the layout.
**While designing:** Set condensed headlines large in sentence case, use capitals only for short tracked labels, keep to two families, and tune the fallback font so the swap does not move the layout.
## Steps
### Sentence case for condensed headlines (`cp-sentence-case`) [craft-consensus · verified]
Set condensed headlines in sentence case and let the tall letterforms carry the style. Use text-transform: uppercase only for labels of three words or fewer that fit on one line. Buttons stay in sentence case.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a scan of the computed styles on a test page (condensed h1 and h2 in sentence case, a one-line uppercase label "Issue 04") found one uppercase element, one line and 8 characters; the audit snippet below lists every uppercase element with its line count and length so you can enforce the limits in CI. Butterick: capitals are fine for less than one line and wrong for whole paragraphs. UX Movement recommends sentence case for button labels and discourages all caps because the lack of word shape lowers readability.
- Satisfies: copy-no-all-caps-text, craft-caps-short-only, craft-heading-sentence-case
```js
// list uppercase elements with letter-spacing (em), rendered lines and length
[...document.querySelectorAll("body *")].filter(e => getComputedStyle(e).textTransform === "uppercase")
  .map(e => { const c = getComputedStyle(e);
    return { text: e.textContent.trim(), ls: +(parseFloat(c.letterSpacing) / parseFloat(c.fontSize)).toFixed(3),
             lines: Math.round(e.getBoundingClientRect().height / parseFloat(c.lineHeight)) }; });
```
### Track uppercase labels 0.05 to 0.12em (`cp-caps-tracking`) [craft-consensus · verified]
Give every uppercase or small-caps label letter-spacing between 0.05em and 0.12em (0.08em works). Keep body text at letter-spacing normal. A large condensed headline may be tightened slightly (about -0.01em); do not widen lowercase text.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the uppercase label computed to 0.08em; the h1 used -0.01em; the body paragraph stayed normal. Butterick recommends 5 to 12% extra space (0.05em to 0.12em in CSS) for capitals and small caps, and says lowercase letters do not ordinarily need letterspacing.
- Satisfies: craft-caps-letterspacing, craft-body-tracking-normal
```css
.label { font: 700 1rem/1 var(--display); text-transform: uppercase; letter-spacing: 0.08em; }
h1 { letter-spacing: -0.01em; }
body { letter-spacing: normal; }
```
### Rem clamp sizing for condensed h1 (`cp-fluid-size`) [craft-consensus · partly-verified]
Size condensed display type in rem stepped at breakpoints (no clamp() with vw, which cannot reach 200% under text enlargement), keep the h1 at 6rem or below, wrap it with text-wrap: balance, and use a tight line-height only on headlines (0.9 to 1.05). Choose a condensed family from the subject rather than the first one that comes to mind: Barlow Condensed (static cuts), Sofia Sans Extra Condensed (variable weight 1 to 1000), Archivo (variable width 62 to 125, so one file gives you condensed and regular) all exist in Google Fonts.
- How: Google Fonts metadata (fetched 2026-11-06) confirms the three families and the Archivo wdth axis (62 to 125) and Sofia Sans Extra Condensed wght axis (1 to 1000). Because condensed glyphs are narrow, an h1 can be larger before it wraps, but keep to the 6rem cap and about 45 characters per line. Stepped rem sizes (3rem, 4.5rem, 6rem: the small size is 50% of the large) follow the browser text-size setting and reach 200%; a clamp() with a vw term was measured not to (Roselli; type-zoom-2026-11-05).
- Satisfies: craft-fluid-type-rem-clamp, distinct-hero-headline-proportion, distinct-display-font-chosen, a11y-resize-text
- Verification note: Font availability and axes were read from metadata; the face names are examples chosen by us, not a ranking, and none was rendered. The 6rem cap and 45-character wrap come from the guidelines.
```css
h1 { font: 800 3rem/0.95 "Sofia Sans Extra Condensed", "Arial Narrow", sans-serif;
     letter-spacing: -0.01em; text-wrap: balance; max-inline-size: 18ch; overflow-wrap: anywhere; }
@media (min-width: 40em) { h1 { font-size: 4.5rem; } }
@media (min-width: 64em) { h1 { font-size: 6rem; } }
```
### Let headline blocks grow (`cp-text-spacing`) [craft-consensus · verified]
Leave condensed headline blocks to grow: no fixed height, no overflow: hidden on boxes that hold text, and tight line-height only on the headline itself. Test with the WCAG text-spacing override.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 320 px card with a 0.9 line-height condensed-style headline, then the WCAG 1.4.12 overrides injected (line-height 1.5, letter-spacing 0.12em, word-spacing 0.16em, paragraph spacing 2em): the card grew from 234 to 533 px and scrollHeight still equalled clientHeight, so nothing was clipped and the page did not scroll sideways (scrollWidth 320). The test used the fallback face (Arial Narrow or Arial), not a web font.
- Satisfies: a11y-text-spacing
```css
/* paste into devtools to test WCAG 1.4.12 */
* { line-height: 1.5 !important; letter-spacing: 0.12em !important; word-spacing: 0.16em !important; }
p { margin-bottom: 2em !important; }
```
### Exactly two type families (`cp-two-families`) [our-take · partly-verified]
For a serif and sans pairing, use exactly two families (plus mono for code if needed). Build hierarchy from size, weight, colour and case inside them: the display or headline face in one, the reading text in the other, and do not add a third face for pull quotes or buttons.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the audit below counted the first font-family of every rendered text element on a test page and returned two (Sofia Sans Extra Condensed and Newsreader). Pair for contrast in structure (a high-contrast serif with a plain sans, or a condensed display with a text serif) and make sure the two share a similar x-height at body size so the switch does not look accidental. Apple HIG and web.dev both point to a small number of families.
- Satisfies: craft-font-families-few, distinct-display-font-chosen
- Verification note: The two-family limit is a guideline we hold as our-take. The family count script was tested on a page whose web fonts were not loaded, so it reads the declared first family, which is what the guideline checks. No pairing quality claim was tested.
```js
// distinct first font families actually rendered (fails if more than 2)
new Set([...document.querySelectorAll("body *")]
  .filter(e => [...e.childNodes].some(n => n.nodeType === 3 && n.textContent.trim()))
  .map(e => getComputedStyle(e).fontFamily.split(",")[0].replace(/[\"']/g, "").trim()));
```
### Tune fallback metrics for swap (`cp-font-loading`) [craft-consensus · partly-verified]
Stop the swap from moving the layout: preload the one display file you need, use font-display: swap or optional, and tune the fallback face with size-adjust, ascent-override, descent-override and line-gap-override so its metrics match the web font. Keep CLS at 0.1 or below.
- How: web.dev (Optimize CLS): fonts can shift layout even while text is invisible because the fallback sets the layout; font-display: optional avoids a re-layout when the font is not ready; size-adjust and the related overrides reduce the size gap; a good CLS is 0.1 or less for at least 75% of visits. Compute the override values from the two fonts' metrics with a tool and measure CLS afterwards.
- Satisfies: a11y-coga-no-surprise-changes
- Verification note: The mechanism is from web.dev. No override values are given because they depend on the chosen pair, and a font-swap CLS measurement with real font files was not run.
```css
@font-face { font-family: "Display fallback"; src: local("Arial Narrow");
  size-adjust: /* from metrics */; ascent-override: /* from metrics */; }
h1 { font-family: "Sofia Sans Extra Condensed", "Display fallback", sans-serif; }
```
