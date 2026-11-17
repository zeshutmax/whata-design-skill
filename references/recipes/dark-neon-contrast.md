# Recipe: Dark, neon and atmospheric palettes that stay readable (`dark-neon-contrast`)
Styles covered: dark-cyber, neon, gradient-aurora, grain-noise, monochrome
**Keep:** Dark canvas, neon accents, glow, grain and gradients as atmosphere.
**Avoid:** Neon text for body copy; accents as the only sign of state; thin low-contrast hairlines; strobing glows.
Keep the near-black canvas and the glowing accents. Make text sit on solid surfaces, use neon for large or graphical elements only, and give focus its own bright, high-contrast ring.
**While designing:** Choose a palette with named roles, assert every text/background pair meets 4.5:1 (3:1 for large text and UI), keep neon for accents on solid surfaces, add a dedicated focus color, and avoid any flashing.
## Verified palette: Dark neon, verified
- background: #0B0D12
- surface: #141821
- text: #E9ECF3
- text-muted: #A9B0C0
- accent-green: #39FF88
- accent-pink: #FF4DB8
- focus: #5CE1FF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| text on background | #E9ECF3 | #0B0D12 | 16.43:1 | 4.5:1 |
| muted text on surface | #A9B0C0 | #141821 | 8.17:1 | 4.5:1 |
| neon green accent on background (UI, large text) | #39FF88 | #0B0D12 | 14.65:1 | 3:1 |
| neon pink accent on background (UI, large text) | #FF4DB8 | #0B0D12 | 6.48:1 | 3:1 |
| dark text on neon green button | #0B0D12 | #39FF88 | 14.65:1 | 4.5:1 |
| focus ring cyan on background | #5CE1FF | #0B0D12 | 12.65:1 | 3:1 |
| focus ring cyan on surface | #5CE1FF | #141821 | 11.56:1 | 3:1 |
| white text on 55% black scrim over gradient stop #3B1E8F | #FFFFFF | #1b0d40 | 17.82:1 | 4.5:1 |
| white text on 55% black scrim over gradient stop #D946EF | #FFFFFF | #621f6c | 10.87:1 | 4.5:1 |
| white text on 55% black scrim over gradient stop #FDE68A | #FFFFFF | #72673e | 5.64:1 | 4.5:1 |
## Steps
### Name palette roles and check pairs (`dn-palette`) [craft-consensus · verified]
Define colors as named roles, and check every text and surface pairing before choosing accents. Body text and muted text use the first two roles; neon is for large text, icons, borders and buttons with dark text on top.
- How: Use the verified pairs in this recipe as the starting palette; change a color only after recomputing its contrast.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Solid scrim under text (`dn-scrim`) [craft-consensus · verified]
Put text on a solid or semi-opaque surface, never directly on a gradient, glow, grain or image. Grain and noise sit on the background layer only. Over a gradient, a 55% black scrim keeps white text at 4.5:1 or better on every tested stop (#3B1E8F, #D946EF, #FDE68A), where unscrimmed white on #FDE68A fails.
- How: Layer order: background gradient and grain, then a scrim or surface, then text.
- Satisfies: a11y-contrast-text
### Bright dedicated focus ring (`dn-focus`) [craft-consensus · verified]
Give focus a distinct bright ring that works on both background and surface, and never remove the outline without a replacement.
- How: Use :focus-visible (Baseline widely available since March 2022) so the browser decides when the ring shows. MDN: the indicator needs at least 3:1 contrast (WCAG 1.4.11) and must not simply be removed. In forced-colors mode outline-color and border-color are forced to system colors and stay visible, but box-shadow is forced to none, so draw the ring with outline (as below) and do not rely on box-shadow alone. MDN advises against building a separate forced-colors design; do not use forced-color-adjust to override users' colors. Cyan #5CE1FF measures 3:1 or better on both dark roles.
- Satisfies: a11y-focus-visible, a11y-non-text-contrast
```css
:focus-visible {
  outline: 3px solid var(--focus);   /* 3:1 or better on every background it sits on */
  outline-offset: 3px;
}
```
### Show state beyond color (`dn-state-not-color`) [craft-consensus · verified]
Show state (selected, error, success) with more than a color shift: an icon, underline, weight or text.
- How: WCAG techniques: put the information in text (G14) or add another visual cue (G182); failures include required or error fields identified by color alone (F81). Inline links need 3:1 against surrounding text or another cue. WCAG lists color-vision simulators for checking; a grayscale view is a quick approximation.
- Satisfies: a11y-color-not-only
### Keep glow static or slow (`dn-no-strobe`) [craft-consensus · verified]
Keep glow static or slow. Never flash: content passes WCAG 2.3.1 if it flashes no more than three times per second.
- How: WCAG 2.3.1: no more than three general or red flashes in any one second passes without a tool; otherwise the flashes must stay below the thresholds (opposing luminance change of at least 10% with the darker state below 0.80 is a general flash; area limit about 341×256 px at 1024×768). Prefer a still box-shadow glow; if you pulse, keep it slow and respect reduced motion.
- Satisfies: a11y-flashes
### Show toggle state beyond color (`dark-neon-contrast--comp-toggle-visual-state-not-color`) [craft-consensus · partly-verified]
Style toggles from [aria-pressed=true] and add a knob position or check icon, not only a color change.
- How: Grayscale screenshot of both states; confirm still distinguishable. Check CSS selectors key off aria-pressed/aria-checked/:checked. (Derived from the rule; see its sources.)
- Satisfies: comp-toggle-visual-state-not-color
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Scrim behind text on media (`dark-neon-contrast--craft-contrast-text-on-media`) [craft-consensus · verified]
Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- How: Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (Derived from the rule; see its sources.)
- Satisfies: craft-contrast-text-on-media
### Re-check contrast in dark mode (`dark-neon-contrast--craft-dark-mode-reverify`) [craft-consensus · partly-verified]
Author the dark palette as its own set of tokens, check contrast in both themes, and dim bright images instead of inverting anything.
- How: Run the contrast audit (text 4.5:1, large 3:1, UI components 3:1) twice, once per emulated color scheme, over all pages and states (hover, focus, disabled excluded). Fail any pair that passes light but fails dark. Flag use of `filter: invert()` on the page root. (Derived from the rule; see its sources.)
- Satisfies: craft-dark-mode-reverify
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Rem steps for display headings (`dn-reflow-200`) [standard · verified]
Give display headings overflow-wrap: anywhere and step the h1 down in a rem media query (max-width: 30rem), with less hero padding, so a word like 'terminal' at 96 px does not stretch the page; do not use clamp() with vw for this.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; the h1 at 3rem became 96 px at 200%; the word was 364 px wide in a 224 px column and widened the page; the media-query step-down removed the overflow and the a11y-resize-text probe no longer reported a fluid-type problem.
- Satisfies: a11y-reflow
