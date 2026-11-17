# Recipe: Illustration, hand-drawn and graphic-only art that stays accessible (`illustration-and-hand-drawn`)
Styles covered: illustration, illustrative, hand-drawn, graphics-only
**Keep:** Hand-drawn lines, doodles, marker highlights, hand lettering, flat or textured illustration, abstract graphic fields.
**Avoid:** Hero scenes assembled from div or SVG primitives in code; emoji or mixed-weight icons; pale pencil lines that carry meaning; headlines as images of text; the same artwork for light and dark grounds; draw-on animations that hide the art for reduced-motion users; abstract graphics as the only message.
Keep the drawn world: sketchy lines, hand lettering, abstract shapes and patterns. Use real authored artwork instead of code-assembled scenes, keep UI icons in one currentColor family, give informative art an alternative and decorative art none, keep meaningful lines at 3:1, and make draw-on animation end in a finished drawing.
**While designing:** Commission or draw the art and ship it as files, keep UI icons as one inline SVG family in currentColor, write alt text only for informative images, hold meaningful line art at 3:1 or better, set hand lettering as real text, and show the finished drawing when motion is reduced.
## Verified palette: Ink, paper and marker, computed
- paper: #FBF9F4
- ink: #1F1F23
- line-art: #595959
- line-art-lightest: #8C8C8C
- highlight: #FFE066
- annotation: #B3261E
- link: #1D4ED8
- dark-ground: #14141A
- dark-line-art: #E8E8EC
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on paper | #1F1F23 | #FBF9F4 | 15.61:1 | 4.5:1 |
| pencil line (meaningful) on paper | #595959 | #FBF9F4 | 6.66:1 | 3:1 |
| faintest meaningful line on paper | #8C8C8C | #FBF9F4 | 3.2:1 | 3:1 |
| ink on marker-yellow highlight | #1F1F23 | #FFE066 | 12.6:1 | 4.5:1 |
| red-pen annotation text on paper | #B3261E | #FBF9F4 | 6.21:1 | 4.5:1 |
| link on paper | #1D4ED8 | #FBF9F4 | 6.37:1 | 4.5:1 |
| dark mode: light line art on night ground | #E8E8EC | #14141A | 15.01:1 | 3:1 |
## Steps
### Use real authored illustration (`il-authored-art`) [our-take · judgement]
Make the illustration real: commissioned, drawn by you or licensed, exported as SVG, AVIF or PNG files and placed with img or picture. Do not build hero scenes out of div rectangles or a pile of inline SVG primitives, do not use placeholder image hosts, and do not use emoji as icons.
- How: The rule flags placeholder hosts (picsum, placehold, via.placeholder), product mock-ups made of div rectangles, hero-sized inline SVG scenes assembled from primitive shapes and emoji used as icons. An illustrator's exported file passes because it is a file, however many paths it has. Chrome demo scan: no emoji in buttons, links or headings, no inline SVG wider than half the viewport with five or more primitives, no placeholder hosts.
- Satisfies: distinct-real-imagery-and-icons
- Verification note: The rule comes from practitioner anti-slop detectors; the remedy (ship authored art as files) is our recommendation, not a standard.
### Separate UI icons from illustration (`il-icon-family`) [craft-consensus · verified]
Keep illustration and UI icons separate. Illustrations may use any palette; UI icons are one inline-SVG family at one stroke weight (24 px grid, stroke 2, round caps) with stroke="currentColor", sized with CSS, so hover, focus, dark mode and forced colours recolour them. Full-colour or raster icons are art, not controls.
- How: web.dev icons: inline SVG so CSS can style it; Apple HIG: one stroke weight across a set, matched to adjacent text. Measured in Chrome 156: the icon's computed stroke equals its button's computed colour on rest, on hover (#1D4ED8), in emulated dark scheme (#E8E8EC) and in forced colours (system colour), and the demo icons all use stroke-width 2.
- Satisfies: craft-icons-one-family, craft-icons-svg-currentcolor, distinct-real-imagery-and-icons
```html
<button class="btn"><svg class="icon" aria-hidden="true" viewBox="0 0 24 24" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 12h16M14 6l6 6-6 6"/></svg> Read the latest entry</button>
```
### Alt text by purpose of the art (`il-alt`) [standard · verified]
Decide for each drawing whether it informs or decorates. Informative art gets alt text that states its purpose in context (about 150 characters at most, no "image of", no repeating nearby text); decorative flourishes get alt="" or are CSS backgrounds; inline SVG that carries meaning gets role="img" and an accessible name; complex diagrams get a longer description in the page text.
- How: WCAG 1.1.1: pure decoration should be ignorable by assistive technology. NN/g and WebAIM alt text guidance. Measured in Chrome 156 with Playwright's accessibility snapshot of the demo: the hero sketch and the labelled scribble appear as named images, the alt="" flourish and the aria-hidden pattern do not appear, and the heading is exposed as a level 1 heading.
- Satisfies: a11y-alt-text
### Meaningful lines at 3:1 (`il-line-contrast`) [standard · verified]
Hold every line that carries meaning (diagram strokes, input outlines, chart axes, the outline of a character that explains something) at 3:1 against its ground. On paper #FBF9F4, pencil #595959 is 6.66:1 and the faintest usable line #8C8C8C is 3.2:1. Pale guide lines such as #BDBDBD (1.79:1) are decoration only.
- How: WCAG 1.4.11 asks 3:1 for graphics needed to understand content; 1.4.3 asks 4.5:1 for text. Ink text is 15.61:1 on paper, ink on a marker-yellow highlight #FFE066 is 12.6:1, a red-pen annotation #B3261E is 6.21:1, the link #1D4ED8 is 6.37:1. A sketchy look comes from line wobble and texture, not from pale strokes. Rendered stroke and text colours in the Chrome demo match these pairs.
- Satisfies: a11y-non-text-contrast, a11y-contrast-text
### Hand lettering as real text (`il-lettering`) [craft-consensus · partly-verified]
Set hand lettering as real text in a handwriting or brush webfont at large sizes in dark ink, specified in rem so 200% text zoom works, and keep body copy in a plain face. Lettering that has to be artwork is allowed only as a logotype or when the look is essential, and then it needs alt text with the same words.
- How: WCAG 1.4.5: use real text when the technology can achieve the presentation; the exceptions are customizable, essential and logotype. WCAG 1.4.4: text must reach 200%; viewport-unit-only sizing fails (F94). 24 px or larger counts as large text (3:1), but we advise 4.5:1 anyway for thin strokes. Demo: the h1 is a real heading at 48 px (3rem), no image inside it. That handwriting faces read poorly at small sizes is our observation and is not tested here; self-host the font rather than relying on system stacks.
- Satisfies: a11y-images-of-text, a11y-resize-text, a11y-contrast-text
- Verification note: The WCAG facts are verified; the advice about small handwriting text and the 4.5:1 habit for thin strokes is our judgement, and the 200% zoom was not re-measured for this demo.
### Draw-on animation ends finished (`il-draw-on`) [standard · verified]
Make the finished drawing the default state and animate toward it: the path is fully visible with no animation, and the draw-on keyframes run once, in under five seconds, from hidden to complete. Under prefers-reduced-motion: reduce, remove the animation so the finished art is shown.
- How: MDN: honour reduce by replacing large motion with gentler effects and do not lose what the animation conveys. WCAG 2.2.2 applies to movement that lasts more than five seconds; a single 2 s draw is under that. Measured in Chrome: one animation of 2 s, 1 iteration; with reduced motion emulated there is no animation and stroke-dashoffset computes to 0, so nothing is hidden. If you set the hidden state in the base CSS and rely on the animation to reveal it, no-JS and reduced-motion users get an empty box.
- Satisfies: a11y-reduced-motion, a11y-pause-stop-hide
```css
.draw path { stroke-dasharray: 1; stroke-dashoffset: 0; animation: draw 2s cubic-bezier(0, 0, 0.2, 1) 1 both; }
@keyframes draw { from { stroke-dashoffset: 1; } to { stroke-dashoffset: 0; } }
@media (prefers-reduced-motion: reduce) { .draw path { animation: none; } }
/* path uses pathLength="1" */
```
### Second artwork for dark grounds (`il-dark-art`) [craft-consensus · verified]
Do not reuse dark line art on a dark ground. Ink #1F1F23 on a #14141A ground is 1.12:1. Ship a second artwork through picture with a prefers-color-scheme: dark source, or draw line art as inline SVG with currentColor and a token (#E8E8EC on #14141A is 15.01:1).
- How: web.dev theming and Apple HIG dark mode: re-check contrast in each theme and dim or swap images rather than inverting. Measured in Chrome with the colour scheme emulated: the picture element's currentSrc switches to the dark artwork, and the line-art token resolves to #E8E8EC on #14141A.
- Satisfies: a11y-non-text-contrast
```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="hero-dark.svg">
  <img src="hero-light.svg" alt="Pen sketch of a looping river crossing a valley" width="600" height="400">
</picture>
```
### Pair abstract graphics with real content (`il-graphics-only`) [our-take · judgement]
When the page uses abstract shapes, gradients or patterns instead of pictures, make them decoration (CSS background or aria-hidden SVG) and pair them with something concrete on the first screen: the product, a real screenshot, a drawing of the actual subject. Abstract art alone cannot say what you sell.
- How: A pattern that carries no information should be ignorable by assistive technology (WCAG 1.1.1), so use a CSS background or aria-hidden. The rule also flags hero-size inline SVG scenes built from primitive shapes, so build generative fields in CSS, canvas with fallback content, or ship them as exported files. The demo's pattern is a repeating-linear-gradient on an aria-hidden block, and no inline SVG in it is larger than half the viewport.
- Satisfies: distinct-real-imagery-and-icons, a11y-alt-text
- Verification note: Pairing abstract art with a concrete subject is our recommendation; the decorative-versus-informative handling is verified in il-alt.
### Wrap long words in display fonts (`il-reflow-200`) [standard · verified]
Handwriting and display fonts are wide: give the h1 overflow-wrap: anywhere and a smaller rem size under 30rem so a single word such as 'sketchbook' (446 px at 200%) fits.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; span.mark right edge was 478 px at 320 px wide; after the fix 0 px of overflow.
- Satisfies: a11y-reflow
