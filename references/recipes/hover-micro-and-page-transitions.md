# Recipe: Hover effects, micro-interactions and page transitions that work without a mouse (`hover-micro-and-page-transitions`)
Styles covered: hover-effects, micro-interactions, page-transitions
**Keep:** Hover lifts and reveals, animated toggles and buttons, success feedback, smooth cross-fades and shared-element route changes.
**Avoid:** Content that exists only on hover; tooltips that vanish when the pointer moves onto them or cannot be dismissed; tabs or menus that open only on hover; feedback over 200ms or that blocks the next click; overshoot easing; a toast as the only record of an action; toggles that rename themselves; page transitions that drop focus, keep the old title, ignore reduced motion or run for seconds.
Keep the hover reactions, the small animated feedback and the animated route changes. Make hover only an enhancement with a keyboard and touch equivalent, keep feedback under 200ms and out of the way of input, mirror every toast on the page, and run transitions only for users who allow motion, with focus, title and status handled.
**While designing:** Hover effects only as enhancements inside (hover: hover) with focus and touch parity; 100 to 200ms ease-out feedback; toggles as aria-pressed buttons with fixed names; toasts mirrored on the page; view transitions only for no-preference motion, with focus, title and status handled.
## Steps
### Hover reveals as enhancement only (`ix-hover-parity`) [craft-consensus · verified]
Make every hover reveal an enhancement. Show the content by default, and only inside @media (hover: hover) hide it until the card is hovered or contains focus (:hover and :focus-within together). On touch devices and keyboards the content is simply there.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a card with an extra line hidden only inside @media (hover: hover) had opacity 0 at rest on a desktop context, 1 after hover (and 0 again after leaving), and 1 after Tab moved focus to the link; in a touch context (hasTouch and isMobile, where (hover: hover) was false) the line was visible at rest with no hover. MDN: the hover media feature reports whether the primary input can hover conveniently; devices that only emulate hover on long tap report none, so hover must not be the only way to reach important content; hybrid devices report only the primary input, so keyboard and focus parity is still needed.
- Satisfies: a11y-coga-hierarchy-visible-no-hover-reveal, a11y-keyboard, a11y-hover-focus-content
```css
.card .more { display: block; }                       /* default: visible */
@media (hover: hover) {
  .card .more { opacity: 0; transition: opacity 150ms ease-out; }
  .card:hover .more, .card:focus-within .more { opacity: 1; }
}
```
### Accessible tooltips when needed (`ix-tooltips`) [craft-consensus · verified]
Prefer a visible text label to a tooltip. If you need a tooltip, show it on hover and keyboard focus, link it with aria-describedby, keep it text only, let Escape dismiss it without moving focus, and keep it visible while the pointer is over the bubble. For help that must work on touch, use a click-activated toggletip: a real button plus an empty role="status" region that you fill on click.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the tooltip appeared when the button received focus, disappeared on Escape while focus stayed on the button, reappeared on the next hover, and stayed visible while the pointer moved onto the bubble. The toggletip button had no aria-describedby, and after Enter the status region held "Billed monthly in US dollars, excluding tax."; Escape cleared it. WCAG 1.4.13 requires such content to be dismissible, hoverable and persistent; native title tooltips are excluded because the browser controls them.
- Satisfies: comp-tooltip-not-sole-label-no-interactive, a11y-hover-focus-content, comp-toggletip-click-live-region, comp-no-title-attribute-reliance
```html
<span class="tipwrap"><button type="button" aria-describedby="t1">Save</button>
  <span role="tooltip" id="t1" class="tip">Saves a draft</span></span>

<button type="button" aria-label="Billing help">i</button><span role="status"></span>  <!-- filled on click -->
```
### Hover-driven tabs follow the tabs pattern (`ix-hover-tabs`) [craft-consensus · verified]
When a hover effect also drives tabs or a menu, build it as the tabs pattern: only the selected tab is in the Tab order, arrow keys move between tabs, Home and End jump to the ends, and a panel that starts with non-focusable content has tabindex="0". Hover may preview a tab, but selection and content come from click and keys.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a three-tab list with role=tablist, aria-selected, aria-controls and roving tabindex: Tab entered on the selected tab (tabindexes 0, -1, -1), ArrowRight moved to the next, End went to the last, ArrowRight wrapped to the first, Home returned to the first, and Tab from the tablist landed on the panel (tabindex 0). Do not use tabs for site navigation (use links).
- Satisfies: comp-tabs-keyboard, comp-tabs-semantics, a11y-coga-hierarchy-visible-no-hover-reveal
```js
tab.addEventListener("keydown", e => {
  const k = { ArrowRight: (i + 1) % n, ArrowLeft: (i + n - 1) % n, Home: 0, End: n - 1 }[e.key];
  if (k !== undefined) { e.preventDefault(); select(tabs[k], true); }   // select sets tabindex 0 / -1
});
```
### Feedback timing of 100 to 400 ms (`ix-timing`) [craft-consensus · verified]
Time interface feedback: hover, press and toggle transitions 100 to 200ms (150ms is a good default), other functional transitions at most 400ms and never over 500ms. Use ease-out for things entering and ease-in for things leaving, no overshoot curves, and keep the control usable during the animation. Under prefers-reduced-motion: reduce, drop transforms and movement and keep a plain colour or opacity change.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): transitions computed to 0.1s (press scale) and 0.15s (colour) on buttons and 0.2s on a checkmark, with cubic-bezier(0.2, 0.8, 0.2, 1) (no y value outside 0 to 1); three rapid clicks on a button during its transition were all counted (the count rose by 3), so input was not blocked; with reducedMotion: "reduce" emulated, the card reveal transition computed to 0s. NN/g and Apple HIG motion guidance support short UI transitions; prefers-reduced-motion is Baseline widely available since January 2020 and MDN advises replacing large movement with gentler effects such as fades rather than removing the information.
- Satisfies: craft-motion-duration-range, craft-motion-frequent-quick, craft-motion-easing-direction, craft-reduced-motion-replace, a11y-reduced-motion, distinct-motion-authored
```css
:root { --ease-out: cubic-bezier(0.2, 0.8, 0.2, 1); }
button { transition: transform 100ms var(--ease-out), background-color 150ms var(--ease-out); }
button:active { transform: scale(0.97); }
@media (prefers-reduced-motion: reduce) { button { transition: background-color 150ms linear; } button:active { transform: none; } }
```
### Animated toggles from ARIA state (`ix-toggle`) [craft-consensus · verified]
Build animated toggles from a native button with aria-pressed (or a checkbox, or role="switch" with aria-checked) and a fixed name such as "Dark mode". Drive the visual state from the ARIA attribute in CSS so look and state cannot diverge, show state with more than colour (a check, a knob position or text), and keep Space and Enter working.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the button's accessible name was "Dark mode" before and after, with [pressed] added by aria-pressed="true" after Space and removed after Enter; the checkmark animated through a stroke-dashoffset transition selected by button[aria-pressed=true]; axe-core found no violations. Do not change the label as well as aria-pressed (APG button pattern).
- Satisfies: comp-switch-label-stable, comp-toggle-visual-state-not-color, a11y-name-role-value
```css
button[aria-pressed="true"] { background: #14171A; color: #fff; }
button[aria-pressed="true"] .check { stroke-dashoffset: 0; }   /* visible check, not only colour */
```
### Immediate feedback with status region (`ix-feedback`) [craft-consensus · verified]
After every action show immediate visible feedback and mirror any toast in persistent page state. Put an empty role="status" region in the page at load and write the message into it, update an on-page count or list (the cart total, the saved list), and let a toast be a convenience, not the only record. Do not use a toast for information needed to finish a task.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): clicking "Add to cart" updated the visible count (0 to 1, then 4 after three rapid clicks) and filled the status region with "Added to cart. 1 items in cart." (fix the plural in real copy). The live region existed before the message, which is what lets assistive technology announce it without moving focus (WCAG 4.1.3). Keep at most one signature motion moment and let other animations answer an action.
- Satisfies: comp-notification-recoverable, a11y-coga-action-feedback, a11y-status-messages, comp-live-region-exists-before-content, distinct-motion-authored
```html
<p>Cart: <span id="count">0</span> items</p>
<div id="live" role="status"></div>   <!-- present at load, empty -->
```
### Cross-document view transitions (`ix-vt-mpa`) [craft-consensus · verified]
For multi-page sites, opt in to cross-document view transitions in CSS on both pages, inside a prefers-reduced-motion: no-preference block, and keep the animation short (about 250ms). Treat it as progressive enhancement: Firefox does not run it and the pages must work without it. Both pages must be same-origin.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome") (Chrome 156): with @media (prefers-reduced-motion: no-preference) { @view-transition { navigation: auto } } on two local pages, a link click produced a ViewTransition on the destination (pagereveal event had viewTransition set); with reducedMotion: "reduce" emulated it did not. After the navigation focus was on the body, as with any normal navigation, and each page keeps its own title. Chrome documents cross-document view transitions from Chrome and Edge 126 and Safari 18.2, not Firefox, requires same-origin navigations and both pages to opt in, and skips the transition if the navigation takes over four seconds. MDN lists @view-transition as Limited availability (not Baseline), so feature-detect or accept non-support.
- Satisfies: craft-motion-duration-range, a11y-reduced-motion, a11y-coga-no-surprise-changes, a11y-page-title
```css
@media (prefers-reduced-motion: no-preference) {
  @view-transition { navigation: auto; }
  ::view-transition-old(root), ::view-transition-new(root) { animation-duration: 250ms; }
}
```
### Guarded single-page view transitions (`ix-vt-spa`) [craft-consensus · partly-verified]
For a single-page route change, wrap the DOM swap in document.startViewTransition only when the user allows motion and the API exists. After the swap, update document.title, move focus to the new page heading (an h1 with tabindex="-1"), push history, and write a short message into a pre-existing role="status" region. Keep the transition at 300ms or less: input is blocked while it runs.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): in an SPA test, after the swap document.activeElement was BODY (the clicked link had been removed), and calling h1.focus() on a tabindex="-1" heading put focus on it; title read "About"; the status region held "Navigated to About"; with reducedMotion: "reduce" no transition was started and the same focus handling still worked. With a deliberately long 1500ms transition, a click on another button 300 ms after the start was held back about 1.4 s until the transition ended (Playwright waited for actionability), and a raw mouse click during it did nothing, so long transitions make the page unresponsive. MDN notes that keeping old and new content around can cause loss of reading position, focus confusion and odd live-region behaviour, and lists stopping accidental interaction with old content among the problems hand-written transitions must solve.
- Satisfies: a11y-focus-order, a11y-page-title, a11y-status-messages, a11y-coga-no-surprise-changes, craft-motion-frequent-quick, a11y-reduced-motion
- Verification note: Focus, title, status text and the input-blocking behavior were measured in Chrome 156; MDN supports the focus and live-region risks. Moving focus to the h1 is common practice rather than a rule from a source we read, and we did not test with a screen reader, Safari or Firefox.
```js
async function go(render) {
  const reduce = matchMedia("(prefers-reduced-motion: reduce)").matches;
  const vt = !reduce && document.startViewTransition ? document.startViewTransition(render) : (render(), null);
  if (vt) await vt.updateCallbackDone;
  document.title = "About";
  document.querySelector("h1").focus();               // h1 has tabindex="-1"
  document.getElementById("live").textContent = "Navigated to About";
}
```
