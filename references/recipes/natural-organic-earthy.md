# Recipe: Organic, botanical and earthy palettes that are not the reflex cream (`natural-organic-earthy`)
Styles covered: organic-soft, botanical-natural, earthy
**Keep:** Rounded forms, gentle shadows, botanical photography, mossy greens, ochres and soil browns, a slow human tone.
**Avoid:** Cream background with terracotta accent and a serif display face by reflex; sage-green text on pale green; links that differ from body text only in a muted green; the same large radius on every element; leaf photography under text without a plate.
Keep the calm, rounded, plant-and-soil feeling. Take the ground colour from the subject (leaf mist, forest, soil) instead of cream with terracotta, vary radius by role with asymmetrical shapes only on images, and darken the greens and browns until text, links and field edges pass.
**While designing:** Pick the page ground from the subject (leaf-tinted mist, deep forest or soil) and run the cream test on it, use dark moss for text and links with underlines, give field edges 3:1, set different radii for controls, cards, tags and images, and put text over botanical imagery on a plate.
## Verified palette: Moss, mist and soil, computed
- ground-mist: #EEF2EA
- ink: #1F2A1C
- text-secondary: #4A5A40
- accent-moss: #3F5D3A
- accent-ochre: #8A5A00
- field-edge: #6B7A5E
- dark-ground-forest: #14231A
- dark-text: #E8EFE0
- dark-text-muted: #B9C8A8
- dark-button-lime: #B9D98A
- ground-soil: #2A1F18
- soil-accent-amber: #E0B15A
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on mist | #1F2A1C | #EEF2EA | 13.17:1 | 4.5:1 |
| moss-grey secondary text on mist | #4A5A40 | #EEF2EA | 6.55:1 | 4.5:1 |
| moss link on mist (underlined) | #3F5D3A | #EEF2EA | 6.53:1 | 4.5:1 |
| white on moss button | #FFFFFF | #3F5D3A | 7.4:1 | 4.5:1 |
| ochre accent text on mist | #8A5A00 | #EEF2EA | 5.23:1 | 4.5:1 |
| input edge on white field | #6B7A5E | #FFFFFF | 4.59:1 | 3:1 |
| input edge on mist | #6B7A5E | #EEF2EA | 4.05:1 | 3:1 |
| dark forest: leaf-white text on forest | #E8EFE0 | #14231A | 13.89:1 | 4.5:1 |
| dark forest: muted leaf text on forest | #B9C8A8 | #14231A | 9.25:1 | 4.5:1 |
| forest text on lime button | #14231A | #B9D98A | 10.39:1 | 4.5:1 |
| soil: leaf-white text on soil brown | #E8EFE0 | #2A1F18 | 13.65:1 | 4.5:1 |
| soil: amber accent on soil brown | #E0B15A | #2A1F18 | 8.11:1 | 4.5:1 |
| leaf-white text on 86% forest plate over the lightest leaf pixel (#2F402F composite, measured 9.42) | #E8EFE0 | #2F402F | 9.42:1 | 4.5:1 |
## Steps
### Choose ground from the subject (`nt-ground`) [craft-consensus · partly-verified]
Choose the page ground from the subject's world: leaf-tinted mist (#EEF2EA), deep forest (#14231A) or soil brown (#2A1F18), with moss (#3F5D3A) and ochre (#8A5A00) accents. If you do want cream with terracotta and a serif display face, record the subject reason in the direction file.
- How: The rule (advisory) reports three things together: a cream background (every channel at least 209, red at least green at least blue, red minus blue between 6 and 48), a terracotta or clay accent (hue about 10 to 30 degrees, moderate saturation) and a serif display face. We ran the rule's cream condition in code: mist #EEF2EA, forest and soil are not cream, while #F5EFE6, #F4EDE0 and #FAF6EE are. Moss is at about 111 degrees, ochre 39, lime 84 and amber 39, outside the terracotta band. An exception record can be one line: "Cream ground chosen because the product is a bakery; paper and flour are cream."
- Satisfies: distinct-palette-not-reflex-cream
- Verification note: Thresholds are practitioner detector values, and the alternative palettes are our suggestions; the colour arithmetic was computed.
### Darken natural colors until they pass (`nt-contrast`) [standard · verified]
Darken the natural colours until they pass, and keep sage for decoration. Ink #1F2A1C on mist is 13.17:1; secondary moss-grey #4A5A40 6.55:1; moss links #3F5D3A 6.53:1; white on a moss button 7.4:1; ochre #8A5A00 5.23:1. Sage #7A8A6C on mist is 3.26:1 and fails as text.
- How: A moss link against ink body text is 2.02:1, below the 3:1 needed to tell a link from surrounding text by colour alone, so underline links (WCAG technique G183 and failure F73). Computed colours of the demo's text, links, button and accent match the claimed pairs in Chrome.
- Satisfies: a11y-contrast-text, a11y-color-not-only
### Visible edges on soft fields (`nt-edges`) [standard · verified]
Soft rounded fields still need an edge: #6B7A5E at 2px is 4.59:1 on white and 4.05:1 on mist. Do not use a pale sage outline or a shadow as the only sign of a field.
- How: WCAG 1.4.11: 3:1 for visual information needed to identify a control. Measured: the rendered input border is #6B7A5E in the demo.
- Satisfies: a11y-non-text-contrast
### Shape and elevation per role (`nt-tokens`) [craft-consensus · partly-verified]
Vary shape by role: controls 12 px, cards 24 px, tags pill, and an asymmetrical organic radius on photographs only. Use two elevations (1px/2px small, 8px 24px soft) and never pair a hairline border with a blur of 32 px or more on a row of three cards.
- How: The rule fails a page where every role shares one radius of 16 px or more, which is the default look of soft UI. Measured in Chrome: button 12 px, card 24 px, tag 999 px, photo a four-value elliptical radius, card shadow blur 24 px with no border.
- Satisfies: distinct-radius-elevation-scale
- Verification note: Rule thresholds come from practitioner detectors; measured against the rule text only.
```css
:root { --r-control: 12px; --r-card: 24px; --r-pill: 999px; --r-blob: 58% 42% 55% 45% / 48% 58% 42% 52%;
  --sh-1: 0 1px 2px rgb(31 42 28 / .12); --sh-2: 0 8px 24px rgb(31 42 28 / .12); }
.photo { border-radius: var(--r-blob); }
```
### Plate under text on photos (`nt-plate`) [craft-consensus · verified]
Do not set text straight on leaf or garden photography. Put it on a plate: an 86% forest plate (#14231A) gave leaf-white text 9.42:1 against the worst pixel even over the lightest leaf colour in the test image.
- How: Method: hide the text, screenshot the plate, compute the WCAG ratio of the text colour against every pixel and report the smallest. The test image runs from #6FBF73 to #D7F5B1; replace it with your brightest real photograph and measure again.
- Satisfies: a11y-contrast-text
### Alt text for botanical photos (`nt-alt`) [standard · verified]
Write real alt text for botanical photography when it informs (species, a visible feature), and alt="" when it only decorates.
- How: NN/g and WebAIM: purpose from context, no "image of", empty alt for decoration. Chrome accessibility snapshot of the demo: the photo is exposed as a named image "Monstera deliciosa leaf with natural splits, held against a white wall".
- Satisfies: a11y-alt-text
### Dark natural theme colors (`nt-dark`) [craft-consensus · partly-verified]
For a dark natural theme use forest (#14231A) or soil (#2A1F18) with leaf-white text #E8EFE0 (13.89:1 on forest, 13.65:1 on soil), muted #B9C8A8 (9.25:1), lime button #B9D98A with forest text (10.39:1) and amber #E0B15A on soil (8.11:1).
- How: Define the dark values as their own tokens and recheck every pair. Chrome demo: under emulated dark scheme the tokens resolve to exactly these colours. Dark forest and soil are the natural-world answer to the near-black plus neon default.
- Satisfies: craft-dark-mode-reverify
- Verification note: Pairs are computed and rendered; the framing against near-black plus neon is our opinion.
### Cap image widths, wrap long words (`nt-reflow-200`) [standard · verified]
Fixed rem image widths need max-width: 100% (14rem is 448 px at 200%); put overflow-wrap: anywhere on body so long words cannot widen the page.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; img.photo was 448 px wide in a 320 px viewport plus a 24 px text-spacing overflow; both were gone after the change.
- Satisfies: a11y-reflow
### Caption strip, not nested card (`nt-plate-not-card`) [our-take · partly-verified]
Make a caption plate on a rounded photo frame a square-cornered full-width scrim strip along the bottom edge (let the frame's overflow: hidden round its corners); a rounded tinted plate inside a rounded frame counts as a nested card (distinct-no-nested-cards).
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; distinct-no-nested-cards failed with a rounded, tinted .plate inside .leafy and passed after the strip change; the check counts boxes with a radius of 4 px or more.
- Satisfies: distinct-no-nested-cards
- Verification note: Recorded from one audit run on one demo page; the audit check is a heuristic and the technique has no independent source.
