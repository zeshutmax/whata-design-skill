# Recipe: Drag interactions and horizontal scrolling (`drag-and-horizontal-scroll`)
Styles covered: drag-interaction, horizontal-scroll
**Keep:** Draggable galleries, swipe rows, horizontally scrolling sections.
**Avoid:** Drag as the only way to move; scroll containers that keyboards cannot reach; horizontal scroll that cannot reflow; gestures that need two fingers.
Keep the tactile, sideways-moving feel. Add buttons and keys that do the same thing, make sure a single tap works, and let narrow screens stack the content.
**While designing:** Every drag or swipe gets visible buttons and arrow-key support, works with a single tap, and stacks vertically at narrow widths.
## Steps
### Previous and next buttons (`dh-buttons`) [craft-consensus · verified]
Provide previous and next buttons (visible, labelled, 24 px or larger) for every draggable or swipeable row; dragging stays as a bonus.
- How: Single pointer, no drag required (technique G219). WCAG's own carousel example has forward and back buttons that may be visually hidden but must be pointer-operable. At either end, mark the button aria-disabled="true" (and style it as disabled) rather than hiding it or using the disabled attribute, which can drop keyboard focus when the pressed button disables itself (our judgement; Chrome behaviour with disabled not measured).
- Satisfies: a11y-dragging, a11y-pointer-gestures
### Mouse-only drag that keeps taps (`dh-mouse-drag-safe`) [craft-consensus · verified]
Add mouse drag only for pointerType 'mouse', without pointer capture, and keep taps working: ignore moves under 5 px, set pointer-events:none on links while a drag is in progress, call preventDefault on dragstart, switch scroll-snap off during the drag and back on after it, and add scroll-padding-inline equal to the scroller's padding so the first card snaps to scrollLeft 0. Leave touch and pen to native scrolling (no two-finger gesture).
- How: Playwright 2026-11-06: a 200 px mouse drag moved the strip one card (292 px) and left the URL hash empty; a drag that started on a card link did not follow the link; a plain click on a link followed it; a CDP touch swipe scrolled the strip natively (288 px). Without scroll-padding-inline the first card snapped at scrollLeft 4, which left Previous enabled at the start.
- Satisfies: a11y-pointer-gestures, a11y-dragging
### aria-disabled at either end (`dh-buttons-aria-disabled`) [our-take · partly-verified]
Give Previous and Next visible text (an SVG arrow with aria-hidden is fine) and use aria-disabled="true" rather than the disabled attribute at either end, ignoring clicks while it is set, so a keyboard user who presses Next to the end keeps focus on the button.
- How: Measured 2026-11-06: pressing Enter on Next 12 times left document.activeElement on Next at the end (aria-disabled). Icon-only buttons whose text was an arrow character made axe report color-contrast and label-content-name-mismatch as 'incomplete' (non-text characters, unverifiable label); visible words Previous and Next with an aria-hidden SVG produced no axe violations or incompletes. Not measured: what Chrome does with focus when a focused button gets the disabled attribute; the aria-disabled choice is our judgement about avoiding that.
- Satisfies: a11y-dragging, a11y-pointer-gestures, a11y-keyboard, a11y-label-in-name
- Verification note: focus staying on an aria-disabled button measured; the alternative with disabled was not measured
### Keyboard-scrollable row (`dh-keyboard`) [craft-consensus · partly-verified]
Make sure keyboard users can reach and scroll the row: if the items are focusable, the browser scrolls focus into view; if the scroller has no focusable children, the scroller itself must be focusable.
- How: Chrome makes scrollers with no focusable children keyboard-focusable by default (announced for 130, rollout delayed to 132); with focusable children, Tab goes to the children. Deque's axe rule: make the scroller or a static element inside it focusable (tabindex="0"); a region whose only content is tabindex="-1" controls fails. Avoid tabindex="-1" on a scroller users need. Accessible names for scrollers are not addressed by the Chrome or Deque pages; MDN says a bare div cannot take aria-label, so a name would need a role that supports one.
- Satisfies: a11y-keyboard
- Verification note: naming a focusable scroller is not covered by any page read
### Inert cards that are mostly off-screen (`dh-offscreen-inert`) [craft-consensus · verified]
Make the scroller a labelled region with tabindex=0 and set inert on cards that are less than half visible (IntersectionObserver rooted at the scroller), except a card that contains focus. Without JavaScript every card link stays focusable and the browser scrolls it into view.
- How: Measured 2026-11-06 in Chrome at 1280 px: scroll-snap-type:x mandatory with a focused scroller scrolled by arrow keys (scrollLeft 4, 292, 580: one card per press), so no custom key handler was needed; Home and End did not scroll it. With inert on off-screen cards, Tab from the scroller reached only the 4 visible card links of 8 and each landed inside the scroller box. With JavaScript off, ArrowRight scrolled the scroller and Tab reached the last card link (scrollLeft 1176). This resolves the tension between dh-keyboard (focusable items scroll into view) and the content-slider rule (hidden slides' links not focusable): use inert when JavaScript runs and leave the links focusable when it does not.
- Satisfies: a11y-keyboard, comp-content-slider-no-autoplay
### Stack items on narrow screens (`dh-reflow`) [craft-consensus · verified]
Below a narrow width, stack the items in a single vertical column or let the row wrap, instead of requiring horizontal scrolling for the whole page.
- How: WCAG Reflow: vertically scrolling content at 320 CSS px wide and horizontally scrolling content at 256 CSS px tall, without two-dimensional scrolling. A horizontal carousel passes if each panel fits within 320 px (G225); a table in its own scrollable container passes if the surrounding content reflows; exceptions cover maps, diagrams, video, games, presentations, data tables and toolbar-in-view interfaces.
- Satisfies: a11y-reflow
### Check stacked layout at 200% text (`dh-reflow-text-200`) [craft-consensus · verified]
Check the stacked layout at a 320 px viewport with the root font size at 200% as well: let nav lists wrap and add overflow-wrap:anywhere to paragraphs that contain long strings such as email addresses and to headings, and give flex children that hold a heading min-width:0.
- How: Measured 2026-11-06 with html { font-size: 200% } at 320 px: the nav list (display:flex without wrap) and an email link in the help section scrolled the page horizontally. flex-wrap:wrap and overflow-wrap:anywhere fixed both; afterwards no body descendant extended beyond the viewport.
- Satisfies: a11y-reflow, a11y-resize-text
### Script-revealed prev and next (`dh-js-only-hidden`) [craft-consensus · verified]
Previous and Next start with the hidden attribute and are revealed by the script that wires them, with [hidden] { display: none !important } in the CSS. Hide them too in the stacked layout where there is nothing to scroll.
- How: JavaScript-off Playwright pass 2026-11-06: the author rule .controls { display:flex } overrode the hidden attribute and left dead buttons on screen; the !important rule fixed it. Stacked widths 320, 390 and 640 px had no horizontal scroll and the strip had no overflow.
- Satisfies: a11y-keyboard, perf-core-first
### Use a native range input (`drag-and-horizontal-scroll--comp-slider-semantics`) [craft-consensus · verified]
Prefer input type=range; add output text next to it and aria-valuetext when units matter.
- How: Inspect value attributes; keyboard test arrows/Home/End/PageUp/PageDown; check aria-valuetext shows units; test with VoiceOver on iOS or TalkBack. (Derived from the rule; see its sources.)
- Satisfies: comp-slider-semantics
### Scroll-snap sliders without autoplay (`drag-and-horizontal-scroll--comp-content-slider-no-autoplay`) [craft-consensus · partly-verified]
Build sliders as scroll-snap lists with labelled prev/next buttons and no autoplay.
- How: Load the page for 30 seconds without input: nothing moves. Tab through: arrows reachable, scroller focusable with visible focus, hidden slides' links not focusable. Check prev/next buttons have names. (Derived from the rule; see its sources.)
- Satisfies: comp-content-slider-no-autoplay
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Breakpoints where content breaks (`drag-and-horizontal-scroll--craft-breakpoints-content-based`) [craft-consensus · partly-verified]
Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- How: Sweep the viewport from 320 to 1920 px in 40px steps. At each step assert no horizontal scrollbar (scrollWidth <= clientWidth), no element overlapping its sibling's box, and the measure rule still passes. Inspect media queries: list breakpoint values and flag any matching device presets (375, 414, 768 and 1024 px) written in px for review. (Derived from the rule; see its sources.)
- Satisfies: craft-breakpoints-content-based
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Name the strip so audits check it (`dh-audit-probe-note`) [our-take · judgement]
Name the strip with a 'carousel' class (or any element the audit's carousel selector matches) so the audit raises the drag and pointer-gesture rules for human review instead of marking them not applicable.
- How: The audit's gesture probe counts draggable=true attributes, range inputs, canvases and carousel library classes. A strip that uses only pointer events and has no matching class is reported as 'not applicable' for a11y-dragging and a11y-pointer-gestures, which hides the one place a drag alternative must be checked. Measured by reading the probe source and by the 'check' status the demo received once its wrapper used the class carousel.
- Satisfies: a11y-dragging, a11y-pointer-gestures
- Verification note: about the audit tool, not WCAG; the real fix is a better probe
