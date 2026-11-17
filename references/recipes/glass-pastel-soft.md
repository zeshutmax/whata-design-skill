# Recipe: Glass, pastel and soft palettes without washed-out text (`glass-pastel-soft`)
Styles covered: glassmorphism, pastel
**Keep:** Frosted panels, soft color fields, rounded forms.
**Avoid:** White text on a light translucent panel; pastel text on pastel backgrounds; glass borders as the only separator between controls and background.
Keep the translucency, blur and gentle colors. Decide the worst-case backdrop first, make the panel dark or light enough for that case, and use pastel as fills with dark text and visible borders.
**While designing:** Test text against the worst-case backdrop, add an opaque fallback, keep text dark on pastel fills, and make control borders at least 3:1.
## Verified palette: Pastel, verified
- background: #F7F1FF
- text: #2B1B45
- text-muted: #5B4B77
- button-fill: #CDB4FF
- input-border: #7A68A3
- link: #5A2FC2
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white text on 72% dark panel over #FFFFFF backdrop | #FFFFFF | #4f5154 | 7.96:1 | 4.5:1 |
| white text on 72% dark panel over #FFE066 backdrop | #FFFFFF | #4f482a | 9.16:1 | 4.5:1 |
| white text on 72% dark panel over #7CF2FF backdrop | #FFFFFF | #2b4d54 | 9.16:1 | 4.5:1 |
| text on pastel background | #2B1B45 | #F7F1FF | 14.11:1 | 4.5:1 |
| muted text on pastel background | #5B4B77 | #F7F1FF | 6.98:1 | 4.5:1 |
| dark text on pastel lilac button | #2B1B45 | #CDB4FF | 8.6:1 | 4.5:1 |
| input border on pastel background | #7A68A3 | #F7F1FF | 4.38:1 | 3:1 |
| link on pastel background | #5A2FC2 | #F7F1FF | 7.24:1 | 4.5:1 |
## Steps
### Test glass on the worst backdrop (`gp-worst-case`) [craft-consensus · partly-verified]
For glass, compute contrast against the worst backdrop the panel can sit on (white, a bright yellow, a bright cyan), not the average one. The verified panel is 72% near-black; white text on it stays above 4.5:1 over all three backdrops (see the table).
- How: Panel color rgba(11,13,18,0.72) with white text. The check uses pure white as the backdrop because a blur is a per-channel weighted average of the pixels behind it and so cannot be lighter than the lightest pixel; this bound assumes browsers composite in sRGB (general knowledge, not on a page read). Raise the opacity before lowering text contrast.
- Satisfies: a11y-contrast-text
- Verification note: bound rests on sRGB compositing and blur averaging (reasoning, not a read source)
### Opaque fallback for backdrop blur (`gp-fallback`) [craft-consensus · verified]
Provide an opaque fallback for browsers or settings where backdrop-filter does not apply, and do not rely on blur to separate text from a busy background.
- How: backdrop-filter is Baseline 2024 (newly available) and only affects content behind the element up to its backdrop root; an ancestor with opacity below 1 can stop it working. Write the opaque background first and enhance inside @supports (backdrop-filter: blur(1px)), or provide the fallback in @supports not (...). @supports is widely available since September 2015.
- Satisfies: a11y-contrast-text
### Dark text on pastel fills (`gp-pastel-fill`) [craft-consensus · verified]
Use pastel as a fill and keep dark text on it. Check muted text and links on the pastel background, not on white.
- How: Verified pairs: #2B1B45 on #F7F1FF, #5B4B77 on #F7F1FF, #2B1B45 on #CDB4FF, link #5A2FC2 on #F7F1FF.
- Satisfies: a11y-contrast-text
### Control edges at 3:1 (`gp-borders`) [craft-consensus · verified]
Give inputs, cards that act as controls and icon buttons a border or fill that reaches 3:1 against what surrounds them.
- How: Input border #7A68A3 on #F7F1FF is verified above 3:1.
- Satisfies: a11y-non-text-contrast
### Label the modal dialog (`glass-pastel-soft--comp-dialog-semantics`) [craft-consensus · verified]
Build modals with a titled dialog element or role=dialog plus aria-labelledby, and keep all its controls inside it.
- How: Open each dialog; query [role=dialog],[role=alertdialog],dialog[open]; assert accessible name is non-empty and that no interactive control needed by the dialog sits outside it. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-semantics
### Manage dialog focus and Escape (`glass-pastel-soft--comp-dialog-focus`) [craft-consensus · verified]
On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- How: Keyboard only: activate the opener, verify focus is inside; Tab through the whole dialog and confirm wrap; press Escape and confirm close and focus on the opener; confirm a visible close control exists. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-focus
### Make modal backgrounds inert (`glass-pastel-soft--comp-dialog-truly-modal`) [craft-consensus · verified]
Make the background inert and dimmed whenever the dialog is modal; for popovers that leave the page usable, do not set aria-modal.
- How: With the dialog open, try to Tab, click and screen-reader-navigate to background content. If any works, aria-modal must be absent. If aria-modal is present, confirm a dim or blur overlay covers the page. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-truly-modal
### Scrim behind text on media (`glass-pastel-soft--craft-contrast-text-on-media`) [craft-consensus · verified]
Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- How: Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (Derived from the rule; see its sources.)
- Satisfies: craft-contrast-text-on-media
### Re-check contrast in dark mode (`glass-pastel-soft--craft-dark-mode-reverify`) [craft-consensus · partly-verified]
Author the dark palette as its own set of tokens, check contrast in both themes, and dim bright images instead of inverting anything.
- How: Run the contrast audit (text 4.5:1, large 3:1, UI components 3:1) twice, once per emulated color scheme, over all pages and states (hover, focus, disabled excluded). Fail any pair that passes light but fails dark. Flag use of `filter: invert()` on the page root. (Derived from the rule; see its sources.)
- Satisfies: craft-dark-mode-reverify
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Small padding on nested glass (`gp-reflow-200`) [standard · verified]
Keep padding on nested glass panels small under 30rem (panel 1rem, backdrop 1rem) and give the panel heading overflow-wrap: anywhere with a smaller rem size; stacked padding inside a glass panel can leave a column of about 96 px at 200% text.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; a 72 px h1 in a 96 px column overflowed 17 px; after reducing padding and stepping the size down, there was no overflow.
- Satisfies: a11y-reflow
