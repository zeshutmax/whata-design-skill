# Recipe: Oversized and expressive type, and theme switching (`big-type-and-modes`)
Styles covered: oversized-type, expressive-type, mode-switching
**Keep:** Huge headlines, lettering, theme or mode changes.
**Avoid:** Type sized only in viewport units; headlines as images; lettering that is the only place the page states its purpose; mode switches that rename things.
Keep the giant, characterful type. Size it in a way that still scales with the user's settings, keep headings real headings, and keep switches between modes predictable.
**While designing:** Use fluid type that includes a rem component, keep headings as real text, and keep mode switches predictable and announced.
## Steps
### Big type in rem, not viewport units (`bt-scalable`) [craft-consensus · verified]
Size big type in rem or em, stepped at breakpoints, with no viewport units in font-size. Keep the smallest-breakpoint size at least 40% of the largest so a high page zoom can still reach twice the 100% size. Keep the largest hero size at 6rem (96 px) or less and the hero headline under 40 characters: the audit's distinct-hero-headline-proportion fails a hero above 96 px, and one of 72 px or more with 40 or more characters.
- How: Measured 2026-11-05 in headless Chrome (see content/learn/measurements/type-zoom-2026-11-05.json): at 100% the sizes were 118 (clamp with vw), 112 (stepped rem) and 102 px (8vw). Under 200% text-only enlargement: stepped rem doubled to 224 px; clamp with vw grew only to 134 px (1.14×); 8vw did not change (1.0×). Under 200% page zoom the breakpoint shrank the sizes: stepped rem showed 80 and 96 device px against 112 at 100%. WCAG accepts shrinking at small breakpoints if 200% is still reachable; computed at the 500% browser maximum, a 2.5rem small size reaches 200 px (1.79×, short) and a 3rem small size reaches 240 px (2.14×). WCAG lists viewport-unit misuse as failure F94. Measured 2026-11-06: at 7rem the audit reported '112 px is over 96 px, 112 px and 61 characters'; at 6rem with a 38-character h1 no failure (small size 3rem is 50% of the large).
- Satisfies: a11y-resize-text
```css
h1 { font-size: 3rem; }                        /* small size ≥ 40% of the largest */
@media (min-width: 48em) { h1 { font-size: 4rem; } }
@media (min-width: 80em) { h1 { font-size: 6rem; overflow-wrap: anywhere; } }
```
### Wrap everything, check 320 px at 200% (`bt-scalable-wrap-everything`) [craft-consensus · verified]
Put overflow-wrap:anywhere on h1, h2 and paragraphs, and let nav lists wrap, then check a 320 px viewport with the root font size at 200%.
- How: Measured 2026-11-06 at 320 px with html { font-size: 200% }: h1 was 96 px and did not scroll the page (overflow-wrap:anywhere), but the nav list (display:flex without wrap) scrolled it to 461 px, and long words such as 'pavement.' overflowed their cards (price text at 64 px inside 144 px of content). After flex-wrap:wrap and overflow-wrap:anywhere on p, no element extended beyond the viewport.
- Satisfies: a11y-resize-text, a11y-reflow
### Smallest size at half the largest (`bt-scalable-reach-by-400`) [our-take · judgement]
If 200% must be reachable at 400% page zoom (not only at the 500% browser maximum), keep the smallest breakpoint size at or above half of the largest (for example 3.5rem against 7rem) instead of 40%.
- How: Measured 2026-11-06 on the demo (h1 3rem, 4rem at 48em, 7rem at 80em; 1280 px screen): device pixels of the h1 were 112 at 100%, 96 at 200% (0.86x), 144 at 300%, 192 at 400% (1.71x) and 240 at 500% (2.14x). Under text-only enlargement (root font size 200%) it was 224 (2.00x). So the 40% rule from bt-scalable gives 2x only at about 500%. Raising the small size to 3.5rem would give 224 device px at 400% (computed, not rendered).
- Satisfies: a11y-resize-text
- Verification note: the 3.5rem figure is arithmetic from the measured sizes; a person must judge whether 56 px headings still fit a 320 px column
### Headlines as real heading text (`bt-real-text`) [craft-consensus · verified]
Headlines and key labels are real text in real heading elements, even if they are drawn with a custom face; avoid images of text.
- How: WCAG 1.4.5: use real text when the technology can achieve the look. Images of text are allowed only for logotypes, when the presentation is essential, or when users can customize them. Repeating the heading as real text next to decorative lettering is a common mitigation but is not a listed exception.
- Satisfies: a11y-headings-labels, a11y-images-of-text
### Predictable mode switch (`bt-mode-predictable`) [craft-consensus · verified]
A theme or mode switch keeps the same labels, order and positions across modes, remembers the choice, starts from the system preference, and announces its state.
- How: Use a toggle button with aria-pressed and a label that does not change (for example "Dark mode"), or a button whose label changes ("Switch to dark" / "Switch to light") without aria-pressed; do not combine them (APG button pattern). Read prefers-color-scheme (Baseline widely available since January 2020) for the initial state. MDN's page does not cover manual overrides, so store the user's choice yourself.
- Satisfies: a11y-consistent
### Light, dark and system radios (`bt-theme-three-state`) [craft-consensus · verified]
For Light, Dark and System, use a fieldset with a legend and three native radios (labels never change), an inline script in the head that applies a saved explicit choice before first paint, CSS that follows prefers-color-scheme unless data-theme says otherwise (with color-scheme set), a role=status line stating the current theme, and the switch hidden until JavaScript runs. Choosing System removes the saved value.
- How: Playwright keyboard pass 2026-11-06 with the OS set to dark: the page starts as System and dark; Tab lands once on the checked radio; ArrowLeft selects Dark then Light (background changes, localStorage written, status text updates); the choice survives reload; labels and positions are identical in light and dark; choosing System clears the value and follows a live OS change from dark to light; with JavaScript off the page follows the OS and the switch is hidden. axe-core found no violations or incompletes in light, in dark through the OS setting, in dark through data-theme, and with data-theme=light over an OS dark setting.
- Satisfies: a11y-consistent, comp-theme-switcher-control, comp-switch-label-stable, perf-core-first
```css
:root { --bg:#FBF7EF; --text:#17130F; color-scheme: light; }
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) { --bg:#14110E; --text:#F5EFE4; color-scheme: dark; }
}
:root[data-theme="dark"] { --bg:#14110E; --text:#F5EFE4; color-scheme: dark; }
```
### Name toggles after the setting (`big-type-and-modes--comp-switch-label-stable`) [craft-consensus · partly-verified]
Name toggles after the setting ('Dark mode') and flip only aria-pressed or aria-checked.
- How: Toggle each control and assert its accessible name is identical before and after, aria-checked/aria-pressed/checked is explicit 'true' or 'false', and Space toggles it. (Derived from the rule; see its sources.)
- Satisfies: comp-switch-label-stable
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headline as one buyer's result (`big-type-and-modes--copy-headline-swap-test`) [craft-consensus · partly-verified]
Write the headline as the result one named buyer gets, using a noun or number only this product can claim.
- How: Read the H1 and subhead alone. (1) Does it say what is offered and for whom? (2) Paste it with a competitor's name: does it still read true? If yes, fail. (3) Fail if it matches the template 'The [AI-powered|modern|all-in-one] [noun] for [teams|businesses|everyone]'. (Derived from the rule; see its sources.)
- Satisfies: copy-headline-swap-test
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headings that state the finding (`big-type-and-modes--copy-heading-informative`) [craft-consensus · partly-verified]
Write each heading as the finding of its section, so the headings alone tell the story.
- How: Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (Derived from the rule; see its sources.)
- Satisfies: copy-heading-informative
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Cap line length near 55ch (`big-type-and-modes--craft-measure-body`) [craft-consensus · partly-verified]
Wrap every block of running text in a container with max-inline-size of about 50ch to 55ch (never above 60ch) and let the container, not the viewport, decide the line length.
- How: At widths 320, 768, 1280 and 1920 px, find every paragraph/list-item/blockquote with more than two lines of text. Compute characters per line (text length divided by rendered line count, or compute container inline-size divided by the width of one '0' glyph, i.e. in ch). Fail if any exceeds 75. For the lower bound, where the viewport allows it (>= 768px), flag single-column text below 45 characters per line for manual review. (Derived from the rule; see its sources.)
- Satisfies: craft-measure-body
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Stepped rem sizes for headings (`big-type-and-modes--craft-fluid-type-rem-clamp`) [craft-consensus · verified]
Set headline sizes in rem and step them at em/rem media queries (for example 3rem, 4rem, 7rem), keeping the smallest at least 40% of the largest; do not use clamp(rem + vw) for text that must scale; test at 200% zoom and 320 px.
- How: Measured in Chrome 2026-11-05 (content/learn/measurements/type-zoom-2026-11-05.json): clamp(rem + vw) and vw sizes did not reach 200% at 200% zoom; stepped rem with small >= 40% of large did. See also step bt-scalable in big-type-and-modes.
- Satisfies: craft-fluid-type-rem-clamp
