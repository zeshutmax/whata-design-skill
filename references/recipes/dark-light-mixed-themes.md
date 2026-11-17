# Recipe: Dark, light and mixed-theme pages with their own checked palettes (`dark-light-mixed-themes`)
Styles covered: dark, light, mixed-theme
**Keep:** A dominant dark or light ground, or light and dark sections alternating; a strong accent colour; imagery that suits the ground.
**Avoid:** Making the dark theme by inverting the light one; reusing the light accent on a dark ground; a flash of the wrong theme at load; native controls and scrollbars in the wrong scheme; a dark band whose links use light-page tokens; a theme switch that renames itself.
Keep a dark page, a light page or alternating bands. Declare color-scheme, define each theme as its own token set with contrast checked, treat bands as local themes, and make any theme switch a labelled toggle that remembers its state. For neon and glow see dark-neon-contrast; for mode switches that rename things see big-type-and-modes.
**While designing:** Meta and CSS color-scheme, light-dark() role tokens, a separately checked dark palette, bands as local themes with their own tokens, and a labelled "Dark mode" toggle that persists.
## Verified palette: Light and dark token sets, each computed
- light-background: #FFFFFF
- light-text: #16181D
- light-accent: #1F4FD8
- dark-background: #12141A
- dark-text: #E8EAF0
- dark-accent: #8FB0FF
- dark-surface: #1B1E27
- dark-focus: #7FB3FF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| light: text on background | #16181D | #FFFFFF | 17.75:1 | 4.5:1 |
| light: muted text on surface | #4B5160 | #F3F4F7 | 7.21:1 | 4.5:1 |
| light: accent link on background | #1F4FD8 | #FFFFFF | 6.62:1 | 4.5:1 |
| light: border (UI) | #7A8190 | #FFFFFF | 3.91:1 | 3:1 |
| light: focus ring on surface | #0B5FFF | #F3F4F7 | 4.66:1 | 3:1 |
| dark: text on background | #E8EAF0 | #12141A | 15.3:1 | 4.5:1 |
| dark: muted text on surface | #A3AABB | #1B1E27 | 7.15:1 | 4.5:1 |
| dark: accent link on background | #8FB0FF | #12141A | 8.61:1 | 4.5:1 |
| dark: dark text on accent button | #0B1020 | #8FB0FF | 8.85:1 | 4.5:1 |
| dark: border (UI) | #6B7385 | #12141A | 3.87:1 | 3:1 |
| dark: focus ring on surface | #7FB3FF | #1B1E27 | 7.76:1 | 3:1 |
## Steps
### Declare schemes with light-dark() (`tm-scheme`) [craft-consensus · verified]
Declare the schemes the page supports in a meta tag placed before any CSS and in CSS on :root, define colours once as role tokens with light-dark(), and let prefers-color-scheme choose the default. A deliberately single-theme page may declare color-scheme: only light or only dark, knowing that this also opts the page out of the browser's automatic dark rendering.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with <meta name="color-scheme" content="light dark"> and :root { color-scheme: light dark } plus light-dark() tokens, emulating colorScheme light gave a white background and #16181D text, and dark gave rgb(18, 20, 26) and rgb(232, 234, 240); getComputedStyle(html).colorScheme was "light dark" in both; a native text input drew a dark background (rgb(59, 59, 59)) in the dark scheme. MDN: color-scheme changes canvas, scrollbars and form controls and is Baseline widely available since January 2022; the meta tag before CSS helps avoid a flash at load; it does not restyle your own content, so use prefers-color-scheme or light-dark() for that.
- Satisfies: craft-dark-mode-scheme, craft-color-role-tokens
```html
<meta name="color-scheme" content="light dark">
<style>
 :root { color-scheme: light dark;
   --bg: light-dark(#FFFFFF, #12141A); --text: light-dark(#16181D, #E8EAF0);
   --accent: light-dark(#1F4FD8, #8FB0FF); --focus: light-dark(#0B5FFF, #7FB3FF); }
 body { background: var(--bg); color: var(--text); }
</style>
```
### Separate dark tokens, check both themes (`tm-tokens`) [craft-consensus · verified]
Author the dark palette as its own set of tokens and check every pair in both themes: 4.5:1 for text, 3:1 for large text, borders, icons and focus rings. Use lighter, less saturated accents on dark grounds, and dark text on a light accent button.
- How: Computed with the WCAG 2 formula (table above): light text 17.75:1, dark text 15.3:1; light accent link 6.62:1 but reusing that same #1F4FD8 on the dark ground gives only 2.77:1, which fails, so the dark accent is the lighter #8FB0FF (8.61:1) with #0B1020 text on a button of that colour (8.85:1). Borders are 3.91:1 light and 3.87:1 dark; focus rings 4.66:1 on the light surface and 7.76:1 on the dark one. Prefer off-black (#12141A) to pure black for large areas; pure white on pure black is 21:1 but glaring. Axe's color-contrast rule reported no violations in either scheme on the test page.
- Satisfies: craft-dark-mode-reverify, a11y-contrast-text, a11y-non-text-contrast, craft-contrast-wcag2-authoritative
### Dim photos, dark logo variants (`tm-images`) [craft-consensus · partly-verified]
Do not invert or filter the whole page to get a dark theme. Dim bright photographs a little in dark mode, supply dark variants of logos and diagrams with transparent backgrounds through picture and a prefers-color-scheme media query, and keep photographs' colours.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): img { filter: brightness(.85) } inside @media (prefers-color-scheme: dark) computed to "brightness(0.85)" in dark and "none" in light. The 0.85 value is our choice. The guideline, built on Apple HIG dark mode and web.dev theming, asks for a palette authored for dark, not an inverted or filtered light one.
- Satisfies: craft-dark-mode-reverify
- Verification note: The media-query behavior was measured; the 0.85 strength is our judgement, not from a source, and no image was assessed visually.
```css
@media (prefers-color-scheme: dark) { img:not([data-keep]) { filter: brightness(0.85); } }
```
### Each band as a local theme (`tm-bands`) [craft-consensus · verified]
For alternating light and dark sections, make each band its own local theme: set color-scheme on the band and override the role tokens (background, text, accent, focus) with that theme's checked values. Components inside use only tokens, so a link or input in a dark band is correct without extra CSS. Give each band a heading so the bands are real sections.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a .band with color-scheme: dark and the dark token values, inside a light page, gave a link colour rgb(143, 176, 255) in both emulated schemes and a native input with the dark control background (rgb(59, 59, 59)) even when the page itself was light; axe color-contrast reported no violations in either page scheme. The dark accent on the dark ground is 8.61:1; the light accent #1F4FD8 would be 2.77:1 there. Keep the order, labels and positions of navigation and controls the same in every band.
- Satisfies: craft-dark-mode-scheme, craft-dark-mode-reverify, a11y-focus-visible, a11y-non-text-contrast, a11y-consistent
```css
.band-dark { color-scheme: dark; --bg: #12141A; --text: #E8EAF0; --muted: #A3AABB;
  --accent: #8FB0FF; --focus: #7FB3FF; background: var(--bg); color: var(--text); }
```
### Stable-name theme switch (`tm-switch`) [craft-consensus · verified]
If you offer a theme control, make it a button with aria-pressed named after the setting ("Dark mode") that never changes its name, place it in the header or footer in the same spot on every page, start from the system preference, and remember the choice. Set the stored theme on the html element from a small inline script in the head before first paint so there is no flash. Style the on state with more than colour.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a button named "Dark mode" with aria-pressed kept the same accessible name before and after toggling, exposed [pressed] after Space, and returned to unpressed after Enter (see the interaction recipe). The guideline, built on Inclusive Components' theme switcher, asks for a labelled toggle whose state persists. Store the choice in localStorage inside try/catch, since storage can be blocked.
- Satisfies: comp-theme-switcher-control, comp-switch-label-stable, comp-toggle-visual-state-not-color, a11y-name-role-value
```html
<script>
 try { const t = localStorage.getItem("theme"); if (t) document.documentElement.dataset.theme = t; } catch (e) {}
</script>
<button type="button" aria-pressed="false" id="theme">Dark mode</button>
```
### Honor contrast and forced colors (`tm-contrast-prefs`) [craft-consensus · partly-verified]
Respect the user's contrast preferences in either theme: under prefers-contrast: more strengthen borders and muted text, and make focus, borders and state survive forced-colors: active by using real borders and outlines, not shadows or background tints alone.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with contrast: "more" emulated, a border defined as var(--line) in a prefers-contrast: more block changed from #7A8190 to rgb(58, 65, 80). In forced-colors mode outline and border colours stay visible but box-shadow is removed (MDN), so draw focus rings with outline.
- Satisfies: craft-contrast-preferences, a11y-focus-visible
- Verification note: The prefers-contrast switch was tested in Chrome emulation; the forced-colors facts were read on MDN but forced-colors rendering was not emulated here.
```css
@media (prefers-contrast: more) { :root { --line: #3A4150; --muted: #2B3040; } }
```
