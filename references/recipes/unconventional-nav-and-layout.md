# Recipe: Unusual navigation, asymmetric and app-like layouts (`unconventional-nav-and-layout`)
Styles covered: unusual-nav, hamburger-only, command-palette, floating-dock, anchor-only, unconventional-layout, asymmetric, experimental, app-shell, split-screen
**Keep:** Expressive navigation, off-grid composition, dock and command-palette patterns, app-like shells.
**Avoid:** Hiding all navigation on desktop; reordering content visually without reordering the code; sticky elements that cover focus; keyboard-only shortcuts as the sole way in.
Spend your convention budget deliberately. Be unusual in looks and composition while keeping a visible way to reach the main sections, a logical code order, a skip link and a working keyboard path.
**While designing:** Be inventive in layout but keep visible primary links on desktop, a skip link first, code order equal to reading order, sticky elements that do not cover focus, a single-column reflow at 320 px, and a written reason for each unconventional choice.
## Steps
### Keep primary sections visible (`nv-visible-links`) [evidence · verified]
On desktop keep the primary sections visible as links, even in a compact or unusual form. On mobile show up to four directly; use a menu button for more, and add in-page links to key content.
- How: In the cited study navigation was used in 27% of desktop tasks when hidden versus 48% visible (2016, six sites). A command palette or hamburger can supplement visible links.
- Satisfies: ux-visible-navigation
### Skip link and landmarks (`nv-skip-and-landmarks`) [craft-consensus · verified]
Put a skip link first in the DOM, and use landmarks (header, nav, main, footer) with labels where there are several.
- How: A skip link (technique G1) should be the first focusable control; WCAG does not require it to be visible when it lacks focus, so one that appears on focus passes, though always visible is preferred. WebAIM: a hidden-until-focus link must become prominently visible on focus, and display:none or the hidden attribute must not be used. Landmarks (ARIA11) or headings (H69) also satisfy 2.4.1, and WebAIM notes a starting h1 or main region can meet it. Layering: give the skip link a z-index above positioned hero layers (a position:relative hero later in the DOM paints over an unpositioned skip link and hides it on focus); the recipe demo pages caught this in a real browser.
- Satisfies: a11y-bypass-blocks
### Disclosure buttons for dropdowns (`nv-menu-button`) [craft-consensus · verified]
Build site-navigation dropdowns as disclosure buttons, not ARIA menus: a real button with aria-expanded (aria-controls is optional in the pattern), Enter and Space toggle it, Escape closes the dropdown and returns focus to the button, and the link for the current page carries aria-current="page".
- How: APG's disclosure navigation example states it deliberately does not use the ARIA menu role, because typical site navigation does not need menu keyboard behavior. Tab moves through buttons and links; arrow keys, Home and End are optional additions. Test with a screen reader.
- Satisfies: a11y-keyboard
### Command palette as native dialog (`nv-palette-dialog`) [craft-consensus · verified]
Build a command palette as a native dialog opened with showModal(), containing a labelled combobox input, a listbox with tabindex=-1, a visible Close button and a role=status line for the result count. Opening moves focus to the input, Escape clears the text first and then closes, and closing returns focus to the button that opened it.
- How: Keyboard pass in Chrome 2026-11-06: Ctrl+K and Enter or Space on the Search buttons open it with focus in the input; typing filters and aria-activedescendant resolves to an option; Down and Up move it with wrap; Enter on an option closes the dialog, updates the hash and focuses the target section; the first Escape clears the text, the second closes and focus returns to the opener. Tab never reaches the page behind (native showModal makes it inert; the Tab after the last control goes to the browser UI, not the page). Pitfall measured: when the listbox has overflow:auto and its options overflow, Chrome makes the listbox itself a Tab stop (an extra stop between the input and the Close button); tabindex="-1" on the listbox removes it, which is correct here because the options are reached through aria-activedescendant. Options are plain role=option items, so the same destinations must also exist as real links elsewhere (the demo builds the palette from the footer site index).
- Satisfies: comp-dialog-focus, comp-dialog-semantics, comp-combobox-semantics, comp-combobox-keyboard, a11y-keyboard
### Keep DOM in reading order (`nv-dom-order`) [craft-consensus · verified]
Compose off-grid with CSS Grid areas and positioning while keeping the DOM in reading order. Avoid using order or absolute positioning to rearrange content that carries sequence.
- How: WCAG 1.3.2: failure F1 is CSS positioning that changes meaning; technique C27 makes the DOM order match the visual order. MDN: the CSS order property changes only the visual order, not the logical or tab order, and creates a mismatch for screen reader and keyboard users. Disabling CSS to read the order is a practical check (inferred; not described on WCAG's page).
- Satisfies: a11y-meaningful-sequence, a11y-focus-order
### Sticky bars must not hide focus (`nv-not-obscured`) [craft-consensus · verified]
Sticky docks, headers and banners must not hide the focused element; leave room with scroll padding.
- How: WCAG technique C43 (CSS scroll-padding) is the only sufficient technique listed for 2.4.11; failure F110 is a sticky header or footer that completely hides focused elements, and partial covering is allowed. A sticky banner can also pass by being modal, closing when it loses focus, or not overlapping content. MDN's scroll-padding page shows the fixed-header anchor case. Test with the keyboard at several viewport sizes.
- Satisfies: a11y-focus-not-obscured
```css
html { scroll-padding-top: var(--dock-height); }
```
### Bottom dock needs scroll padding (`nv-dock-bottom-padding`) [craft-consensus · verified]
A fixed bottom dock needs scroll-padding-bottom and matching body padding, not only scroll-padding-top. Make the dock fixed only when the viewport leaves room (for example min-width:20em and min-height:30em); below that let it sit in the page flow.
- How: Measured 2026-11-06 in Chrome with a real Tab pass over 28 stops of the demo page: with scroll-padding-bottom and body padding, no focused element was covered at 1440x900 or 390x844. Removing both left 2 stops partly covered at 1440x900 (one 4 of 5 sample points) and 11 stops partly covered at 390x844. The audit's own check only fails when a focus target is entirely covered, so these partial covers are invisible to it; WCAG 2.4.11 allows partial covering but a link 80% under the dock is not usable. A dock that stays fixed at 320x225 (400% zoom) would take about a third of the viewport, so below the size query it falls back to a static bar at the end of the page (checked: 0 covered stops at 320x225, 640x450, 390x844, 1440x900).
- Satisfies: a11y-focus-not-obscured, a11y-reflow
```css
.dock { margin: 1rem auto; }
@media (min-width: 20em) and (min-height: 30em) {
  html { scroll-padding-bottom: calc(var(--dock-h) + 1rem); }
  body { padding-bottom: var(--dock-h); }
  .dock { position: fixed; bottom: .75rem; left: 50%; transform: translateX(-50%); }
}
```
### Single-key shortcuts can be turned off (`nv-shortcuts`) [craft-consensus · verified]
Single-key shortcuts (for example "/" or "k") can be turned off or only work when their component has focus; the same actions are reachable by ordinary controls.
- How: List every single-key shortcut (letters, numbers, punctuation, symbols, including those needing Shift, and sequences such as G then A). Each must be able to be turned off, remapped to include a non-printable key, or be active only while its component has focus (technique G217; failure F99). Give each a visible button equivalent as good practice.
- Satisfies: a11y-char-shortcuts, a11y-keyboard
### Use a modifier for palette shortcut (`nv-modifier-shortcut-note`) [craft-consensus · partly-verified]
Use Ctrl or Command plus a key (for example Ctrl+K) for a palette shortcut and keep the visible button. Expect the audit to list the document-level keydown handler as 'check' for a11y-char-shortcuts; answer it by showing the shortcut needs a modifier.
- How: WCAG 2.1.4 covers shortcuts made of letters, numbers, punctuation or symbols only; a shortcut that needs a modifier such as Ctrl is not covered. Measured 2026-11-06: a single document keydown listener for Ctrl/Cmd+K makes the audit report a11y-char-shortcuts as 'check' (not a failure) because it cannot tell modifier shortcuts from single-key ones.
- Satisfies: a11y-char-shortcuts
- Verification note: audit behaviour measured; the claim that modifier shortcuts are outside 2.1.4 is from the WCAG understanding page
### Hide JavaScript-only controls (`nv-js-only-controls`) [craft-consensus · verified]
Controls that only work with JavaScript (the palette buttons) start with the hidden attribute and are revealed by the script that wires them. Add [hidden] { display: none !important } because author display rules such as display:flex override the attribute. All routes stay plain anchors so the page works with JavaScript off.
- How: Found with a JavaScript-off Playwright pass 2026-11-06: a .controls { display:flex } rule overrode the hidden attribute, so dead Previous and Next buttons stayed visible; adding the !important rule hid them. With JavaScript off the demo still reaches every section by Tab and Enter on the rail, the dock or the footer index.
- Satisfies: a11y-keyboard, ux-visible-navigation, perf-core-first
### Logo links home (`nv-logo-home`) [evidence · verified]
Keep the logo linking home in a findable place, even in an unusual layout.
- How: Conventional placement (top-left in left-to-right languages) is the safe default.
- Satisfies: ux-logo-home
### Collapse to one column at 320 px (`nv-reflow`) [craft-consensus · verified]
App shells and split screens collapse to a single column at narrow widths (320 CSS px) without two-dimensional scrolling.
- How: Check at 320 px wide and at 400% zoom.
- Satisfies: a11y-reflow
### Test reflow at 320 px and 200% (`nv-reflow-text-200`) [craft-consensus · verified]
Test reflow twice: at a 320 px viewport and at 320 px with the root font size raised to 200%. Let nav lists wrap, switch to multi-column grids only above a breakpoint (rem column gaps in a 12-column grid add up to more than 320 px at 200% text), and add overflow-wrap:anywhere to paragraphs that hold long strings such as email addresses and to headings and labels. Give a one-column form grid grid-template-columns: minmax(0, 1fr), or its inputs and buttons stretch it past the viewport (a heading that cannot break, 333 px in a 256 px column at 200% text, also overflowed).
- How: Measured 2026-11-06 with html { font-size: 200% } at a 320 px viewport: the first draft of the demo scrolled horizontally because (1) a 12-column hero grid with 1rem gaps needed 11 rem of gap (352 px at 200%), (2) the dock was one non-wrapping row of five 3.5 rem buttons, and (3) an email address could not break. After a grid that starts at 48em, a wrapping dock list, a static dock below the size query and overflow-wrap:anywhere, scrollWidth equalled clientWidth at 320 px for 100% and 200% text. The audit's reflow probe only checks 100% text, so none of this showed up there.
- Satisfies: a11y-reflow, a11y-resize-text
### Justify each unconventional choice (`nv-justify`) [our-take · judgement]
Write down why each unconventional choice earns its cost, and keep the rest of the page conventional.
- How: One or two surprises per page is a workable limit; this is a judgement, not a measured number.
- Satisfies: ux-conventional-layout
- Verification note: our judgement
### Menu role for action menus only (`unconventional-nav-and-layout--comp-menu-button-action-menu`) [craft-consensus · verified]
Use role=menu only for action menus and implement every key the APG lists, or use a disclosure instead.
- How: Keyboard-test: open with Enter, Space, Down; move with arrows (Home/End); Escape returns focus to the button; Tab closes. Check aria-expanded flips. (Derived from the rule; see its sources.)
- Satisfies: comp-menu-button-action-menu
### Site nav without menu roles (`unconventional-nav-and-layout--comp-site-nav-no-menu-role`) [craft-consensus · partly-verified]
Build header menus as nav > ul with a button[aria-expanded] per dropdown and plain links inside.
- How: In header nav: assert no [role=menu|menubar|menuitem]; submenus triggered by button[aria-expanded]; first link of an opened list follows the button in focus order; nav has accessible name when more than one. (Derived from the rule; see its sources.)
- Satisfies: comp-site-nav-no-menu-role
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Prefer native select (`unconventional-nav-and-layout--comp-listbox-select-semantics`) [craft-consensus · verified]
Prefer a native select; build a custom listbox only with full APG keys and short option labels.
- How: Inspect roles and states; keyboard test Up/Down/Home/End and typing a letter; scan options for nested a/button/input. (Derived from the rule; see its sources.)
- Satisfies: comp-listbox-select-semantics
### Combobox focus stays in the input (`unconventional-nav-and-layout--comp-combobox-semantics`) [craft-consensus · verified]
Keep DOM focus in the input and move aria-activedescendant through the options.
- How: Open the popup and assert on the input: role=combobox, aria-expanded=true, aria-controls resolves to a visible listbox, aria-activedescendant changes with Down arrow and resolves to an option; label via label/aria-labelledby. (Derived from the rule; see its sources.)
- Satisfies: comp-combobox-semantics
### Combobox keyboard keys per APG (`unconventional-nav-and-layout--comp-combobox-keyboard`) [craft-consensus · verified]
Implement Down, Up, Enter, Escape and Alt+Down exactly as the APG lists.
- How: Type, press Down, Enter, Escape, Tab in order and verify each outcome and that focus never leaves the input. (Derived from the rule; see its sources.)
- Satisfies: comp-combobox-keyboard
### Provide a second route (`unconventional-nav-and-layout--a11y-multiple-ways`) [craft-consensus · verified]
Provide main navigation and a second route (search, sitemap or footer index) on every multi-page site.
- How: Pick 3 inner pages and show two independent routes to each (nav + search, nav + sitemap, home page links + previous/next). Process pages (checkout steps, search results) are exempt. (Derived from the rule; see its sources.)
- Satisfies: a11y-multiple-ways
### Link text names the destination (`unconventional-nav-and-layout--copy-link-text-unique-destination`) [craft-consensus · partly-verified]
Write link text that names the destination and say 'PDF, 2 MB' or 'opens in a new window' when it applies.
- How: Collect all anchors with accessible names. Fail if two different hrefs share the same name, if a name matches /^(click here|here|more|read more|link|this)$/i or contains 'link', if an href ends in a document extension without format and size in the name, or if target=_blank lacks a notice placed after the main text. (Derived from the rule; see its sources.)
- Satisfies: copy-link-text-unique-destination
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Breakpoints where content breaks (`unconventional-nav-and-layout--craft-breakpoints-content-based`) [craft-consensus · partly-verified]
Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- How: Sweep the viewport from 320 to 1920 px in 40px steps. At each step assert no horizontal scrollbar (scrollWidth <= clientWidth), no element overlapping its sibling's box, and the measure rule still passes. Inspect media queries: list breakpoint values and flag any matching device presets (375, 414, 768 and 1024 px) written in px for review. (Derived from the rule; see its sources.)
- Satisfies: craft-breakpoints-content-based
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
