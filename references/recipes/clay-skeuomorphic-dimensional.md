# Recipe: Clay, skeuomorphic and dimensional UI with real edges and legible text (`clay-skeuomorphic-dimensional`)
Styles covered: claymorphism, skeuomorphic, dimensional
**Keep:** Inflated rounded shapes, soft raised and inset shadows, tactile buttons, material textures, knobs and switches.
**Avoid:** Shadow as the only boundary of an input or control; text directly on a texture; cards inside cards inside cards; one radius for every role; raster or fixed-colour icons for controls; state shown only by a colour shift on a pressed button.
Keep the puffy shapes, soft light, materials and knobs. Let the shadow be mood, not the boundary: give controls a transparent border that survives forced colours and an edge colour that reaches 3:1, put text on opaque plates, flatten groups so cards do not nest, and vary radius and elevation by role.
**While designing:** Define radius and shadow tokens per role, give inputs a 3:1 edge and every raised surface a transparent 2px border, keep text on solid fills, put the metal or leather texture on a base colour and measure its worst pixel, use outline for focus, and show toggle state with knob position and text.
## Verified palette: Clay and metal, computed
- canvas: #E6F0EC
- surface: #F3F9F6
- ink: #1E2B27
- text-muted: #44524D
- button-peach: #FFB8A3
- button-primary: #2F5BEA
- edge: #5E7A70
- metal-light: #E4E7EA
- metal-dark: #B9BEC3
- metal-ink: #1B1F23
- dark-canvas: #14191A
- dark-surface: #1D2426
- dark-ink: #E8F0EC
- dark-muted: #A9B8B2
- dark-edge: #7E948B
- dark-button: #7FD1B9
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on canvas | #1E2B27 | #E6F0EC | 12.61:1 | 4.5:1 |
| ink text on clay surface | #1E2B27 | #F3F9F6 | 13.77:1 | 4.5:1 |
| muted text on clay surface | #44524D | #F3F9F6 | 7.69:1 | 4.5:1 |
| ink on peach clay button | #1E2B27 | #FFB8A3 | 8.84:1 | 4.5:1 |
| white on primary-blue button | #FFFFFF | #2F5BEA | 5.52:1 | 4.5:1 |
| input edge on clay surface (UI boundary) | #5E7A70 | #F3F9F6 | 4.38:1 | 3:1 |
| input edge on canvas | #5E7A70 | #E6F0EC | 4.01:1 | 3:1 |
| ink on brushed-metal plate, worst rendered pixel (measured) | #1B1F23 | #B3B7BB | 8.22:1 | 4.5:1 |
| dark: ink on dark clay surface | #E8F0EC | #1D2426 | 13.59:1 | 4.5:1 |
| dark: muted on dark clay surface | #A9B8B2 | #1D2426 | 7.64:1 | 4.5:1 |
| dark: input edge on dark surface (UI boundary) | #7E948B | #1D2426 | 4.87:1 | 3:1 |
| dark: dark text on mint button | #1E2B27 | #7FD1B9 | 8.2:1 | 4.5:1 |
## Steps
### Real edges on controls (`dm-edges`) [standard · verified]
Treat shadows as mood and give anything the user must find a real edge or fill. Inputs get a 2px edge in #5E7A70 (4.38:1 on the clay surface, 4.01:1 on the canvas); buttons get a label in dark ink on a coloured fill, not a surface-coloured pill that only a shadow separates from the page.
- How: Clay surface #F3F9F6 on canvas #E6F0EC is only 1.09:1, which is a fine look and no boundary. Text pairs: ink #1E2B27 on surface 13.77:1, muted #44524D on surface 7.69:1, ink on peach #FFB8A3 8.84:1, white on blue #2F5BEA 5.52:1. WCAG 1.4.11 asks 3:1 for visual information needed to identify a control. Rendered colours in the Chrome demo match every claimed pair.
- Satisfies: a11y-non-text-contrast, a11y-contrast-text
### Transparent borders and outline focus (`dm-forced-focus`) [craft-consensus · verified]
Give every raised surface and control a 2px transparent border, and draw keyboard focus with outline. In forced-colors mode the soft shadows disappear and the transparent border becomes a visible system-colour edge; the outline stays.
- How: MDN: in forced-colors mode box-shadow is forced to none while border-color and outline-color are kept as system colours. Measured in Chrome 156 with forced colours emulated: card and button box-shadow compute to none, the transparent border computes to rgb(0, 0, 0) at 2px, and a pixel row across the card edge shows black pixels against white where the normal rendering had a soft shadow with no hard edge; keyboard focus is a solid 3px outline in both modes. Normal mode is unchanged because a transparent border draws nothing.
- Satisfies: a11y-focus-visible, craft-contrast-preferences, a11y-non-text-contrast
```css
.card, .btn { border: 2px solid transparent; box-shadow: var(--raise); }
:focus-visible { outline: 3px solid var(--ink); outline-offset: 3px; }
```
### Radius and elevation per role (`dm-tokens`) [craft-consensus · partly-verified]
Name a radius per role (control 14, input 10, card 28, media 20, badge pill) and an elevation per state (raise, inset, press) and use each one the same way everywhere. Keep card-row shadow blur modest (14 px here) and do not combine a visible hairline border with a blur of 32 px or more on three or more adjacent cards.
- How: The rule fails a page where every role shares one radius of 16 px or more, or where three adjacent cards pair a visible 1px border with a blur of 32 px or more. Chrome demo: card, button, input and badge compute to 28, 14, 10 and 999 px; the three cards in the row have a 14 px blur and a transparent border. Soft clay shadows read well at 12 to 20 px.
- Satisfies: distinct-radius-elevation-scale
- Verification note: Thresholds are from practitioner detectors and articles; we measured the demo against the rule text only.
### No raised boxes inside clay cards (`dm-no-nesting`) [craft-consensus · partly-verified]
Let a clay card hold unboxed content: headings, paragraphs and list rows separated by spacing, with no raised or inset container inside it other than interactive controls. If a skeuomorphic panel needs a recessed well, make the well the panel instead of a box inside another box.
- How: Rule: no bordered, shadowed or tinted card container inside another. We implemented that check for non-interactive containers with radius of 4 px or more and ran it in Chrome: the demo has no nested container, and a deliberately nested card inserted by the test is flagged. Buttons, inputs and badges are controls, not containers, so they are exempt in our check; the rule text does not say so explicitly.
- Satisfies: distinct-no-nested-cards
- Verification note: Our implementation of the check treats controls as exempt, which is an interpretation; the underlying rule is from practitioner sources.
### Inline SVG icons with currentColor (`dm-icons`) [craft-consensus · verified]
Draw UI icons as inline SVG with stroke or fill set to currentColor so hover, dark mode and forced colours recolour them. Keep realistic or 3D icon renderings for illustration (decorative, alt="" or named) and never as the only control icon.
- How: web.dev icons: inline SVG so CSS can style it. Measured in Chrome: the Reset icon's computed stroke equals its button colour in light and in emulated dark scheme, and the stroke attribute is currentColor.
- Satisfies: craft-icons-svg-currentcolor
### Measure text over textures (`dm-texture-text`) [craft-consensus · verified]
Put realistic textures (brushed metal, leather, paper) on a solid base colour and measure the worst pixel under each line of text. The demo plate has a #E4E7EA to #B9BEC3 gradient with fine stripes; ink #1B1F23 measured 8.22:1 against its worst rendered pixel (#B3B7BB).
- How: Method: hide the text, screenshot the text box, read every pixel and compute the WCAG ratio against the text colour; the smallest ratio is the one to report. The gradient end alone would be 8.85:1, the stripes lower the darkest pixel and the result is 8.22:1. Keep textures subtle at the text and strong around the edges of the plate.
- Satisfies: a11y-contrast-text
### Toggle state by shape and text (`dm-toggle-state`) [craft-consensus · partly-verified]
Make pressed, on and selected states differ by shape and text, not by a colour shift: a switch knob that moves, an inset shadow that changes, and a label that says On or Off, with aria-pressed (or a native checkbox) carrying the state.
- How: Inclusive Components toggle button and the ARIA switch pattern; WCAG 1.4.1. Chrome demo: aria-pressed flips from false to true, the knob moves 18 px and the text changes from "Eco mode off" to "Eco mode on". The label text changes with the state here, so aria-pressed is not used together with a label that already says the opposite; if you keep the label fixed, keep aria-pressed.
- Satisfies: comp-toggle-visual-state-not-color, a11y-color-not-only
- Verification note: Behaviour measured in Chrome; the label-versus-aria-pressed point follows the Button pattern note from an earlier verification pass and was not re-read.
### Lighter surfaces instead of dark shadows (`dm-dark`) [our-take · judgement]
In dark mode, replace dark drop shadows with lighter surfaces and a thin inset highlight, and re-pick the edge colour: ink #E8F0EC on surface #1D2426 is 13.59:1, muted #A9B8B2 7.64:1, edge #7E948B 4.87:1, dark text on mint #7FD1B9 8.2:1.
- How: Apple HIG dark mode and web.dev theming: define dark tokens separately and re-check contrast per theme. Chrome demo: under emulated dark scheme the tokens resolve to exactly these colours and the raise shadow becomes an inset highlight plus a dark drop. Whether this elevation reads well is a visual judgement; the numbers are measured.
- Satisfies: craft-dark-mode-reverify
- Verification note: Contrast values are computed; the elevation treatment for dark clay is our design judgement.
### Min() grids and wrapping cards (`cl-reflow-200`) [standard · verified]
Write every auto-fit or auto-fill grid as repeat(auto-fit, minmax(min(15rem, 100%), 1fr)); use overflow-wrap: anywhere on cards and max-inline-size: 100% on buttons; cut card and page padding to 1rem under 30rem.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; minmax(15rem,1fr) is 480 px at 200% text and made the page scroll 192 px sideways at 320 px; with min(15rem,100%) and reduced padding the overflow was 0.
- Satisfies: a11y-reflow
