# Recipe: 3D, WebGL, cursor effects and interactive art (`webgl-and-3d`)
Styles covered: realtime-3d, hero-3d, interactive-art, cursor-effects
**Keep:** A real-time 3D or shader scene, interactive objects, cursor-following effects.
**Avoid:** Scene as the only way to reach content; canvases that trap focus; effects that need drag; heavy initialization before the first content paints.
Keep the spectacle. Treat the 3D scene as an enhancement over a complete page: real content first, a meaningful static fallback, keyboard parity, and a performance budget measured on mid-range devices.
**While designing:** Ship the page content as HTML first, use a static poster for LCP, start WebGL after first paint, pause off-screen, give keyboard and single-pointer alternatives, never trap focus, and honor reduced motion.
## Steps
### Core content works without the scene (`wg-core-first`) [craft-consensus · verified]
Build the headline, copy, navigation and call to action as normal HTML that works without the scene. The scene replaces or decorates a static image, not the content.
- How: Resilient Web Design (Layers): start from a well-structured HTML baseline everyone can use and enhance per capability; identify core functionality versus enhancement; feature-detect rather than sniff. Test by disabling JavaScript and throttling the network: the message and navigation must still appear.
- Satisfies: perf-core-first, ux-purpose-clear
### Script-revealed scene controls (`wg-controls-need-js`) [our-take · verified]
Controls that only work once the scene runs (rotate, zoom, pause, skip link) start hidden and are shown by the scene script; with JavaScript off they must not appear.
- How: Use the hidden attribute and add [hidden]{display:none !important}: an author rule such as .controls{display:grid} overrides the browser's hidden style, so the controls stayed visible with JavaScript off in the demo until that rule was added. Add a noscript style as a second guard. If the scene fails to start (getContext returns null, shader link fails), remove the canvas and the controls and leave the poster.
- Satisfies: perf-core-first, a11y-name-role-value
- Verification note: measured in the demo: with JavaScript disabled the controls and canvas were visible until [hidden]{display:none !important} was added; Playwright no-JS pass afterwards showed them hidden and the poster visible
### Static poster as LCP element (`wg-lcp`) [craft-consensus · verified]
Show a static poster image of the scene as the LCP element, discoverable in the initial HTML and not lazy-loaded; initialize WebGL after first paint.
- How: Use a real img for the poster with fetchpriority="high", discoverable in the initial HTML and not lazy-loaded (web.dev). Start the scene after first paint: requestIdleCallback has limited availability (not Baseline), so call it with a timeout and fall back to setTimeout, or start on the load event. Avoid synchronous head scripts.
- Satisfies: perf-lcp
### Test scene and no-WebGL paths (`wg-test-both-paths`) [our-take · verified]
Test the scene path and the no-WebGL path: with WebGL unavailable the poster stays, the controls disappear and nothing throws.
- How: Check getContext('webgl2') for null and shader compile and link errors; on failure remove the canvas and hide the controls. Headless Chrome without GPU flags has no WebGL, so a default audit run only ever exercises this fallback; launch Chrome with --use-gl=angle --use-angle=swiftshader --enable-unsafe-swiftshader to audit the live scene.
- Satisfies: perf-core-first, ux-purpose-clear
- Verification note: both paths were run with the audit: default flags (fallback) and swiftshader flags (live scene); both had zero fails
### Serve the poster as a file (`wg-poster-real-file`) [our-take · verified]
Serve the poster as a real image file (or URL), not a data: URI, if you want it to count as the LCP element.
- How: In Chrome 156 an 800x600 img whose src is a data: URI was not reported as an LCP candidate: the LCP entry was a tiny h1 instead (PerformanceObserver type largest-contentful-paint). Self-contained pages cannot therefore prove the poster is the LCP element; measure on the real asset.
- Satisfies: perf-lcp
- Verification note: measured once with a single test page in Chrome 156 (headless, Playwright); not checked in other browsers
### Reserve space for scene controls (`wg-reserve-control-space`) [craft-consensus · verified]
Reserve the space of controls that appear when the scene starts, so starting the scene moves nothing.
- How: Render the controls in the first HTML with visibility:hidden (it keeps the box) and switch to visible when the scene is ready; do not go from display:none to display:grid after load. Give the stage an aspect-ratio and put the poster image inside it with width and height attributes.
- Satisfies: perf-cls
### Keep the main thread free (`wg-inp`) [craft-consensus · verified]
Keep the main thread free: render in requestAnimationFrame, avoid layout reads inside pointer handlers, cap device pixel ratio (for example at 2), and pause rendering when the canvas is off-screen or the tab is hidden.
- How: Run the render loop only while the canvas is visible, using IntersectionObserver (Baseline widely available since March 2019; its callbacks run on the main thread, so keep them light; feature-detect it). Use the Page Visibility API (visibilitychange, document.hidden; widely available since 2015) for work the browser does not stop itself: browsers already stop requestAnimationFrame in background tabs, but not audio, timers or network. Measure INP in the field; lab tools only approximate it.
- Satisfies: perf-inp
### Fallback content inside the canvas (`wg-semantics`) [craft-consensus · verified]
Put alternative content inside the canvas element (a text description, or an image with alt). Mark a purely presentational canvas role="presentation". If the scene is interactive, map each interactive region to a real focusable element in the fallback content; the canvas itself exposes nothing.
- How: MDN: a canvas is a bitmap that exposes nothing to assistive technology; fallback content goes between the canvas tags; role="presentation" is only for purely presentational canvases; MDN advises avoiding canvas in accessible sites where possible. The HTML Standard says fallback content must convey the same function, focusable descendants of a canvas remain usable, and interactive regions should map one-to-one to focusable areas in the fallback. No page read mentions aria-label on canvas. Put the same information in the page text.
- Satisfies: a11y-name-role-value, ux-purpose-clear
### Make the canvas skippable (`wg-no-trap`) [craft-consensus · verified]
Make the canvas skippable: it is not in the tab order unless it has controls, and focus can always leave it. Provide a visible way to skip past an interactive scene.
- How: WCAG 2.1.2: if focus can enter a component, the keyboard must be able to leave it; a non-standard exit must be explained to the user; Esc is a common standard exit; a modal that cycles focus and closes by Esc or buttons passes. Keep the canvas out of the tab order unless it has controls, and give interactive scenes a visible way to skip past them.
- Satisfies: a11y-no-keyboard-trap, a11y-keyboard
### Buttons and keys beside dragging (`wg-no-drag-only`) [craft-consensus · verified]
Anything done by dragging or orbiting also works with buttons or keys (rotate left and right, zoom in and out), and with a single tap.
- How: WCAG 2.5.7 (technique G219): put buttons beside the drag, or use tap-to-place, direct selection or a typed value. A keyboard alternative alone does not satisfy 2.5.7: pointer-operable controls are needed (they may be visually hidden). Add visible rotate and zoom buttons next to any drag-to-rotate scene.
- Satisfies: a11y-dragging, a11y-pointer-gestures
### Tap to turn, pan-y to scroll (`wg-tap-and-pan`) [our-take · verified]
Make a tap on the canvas turn the scene one step, and set touch-action: pan-y on the canvas so vertical swipes still scroll the page.
- How: Use pointer events: record pointerdown, treat movement over about 6 px as a drag, and on pointerup without movement call the same function as the Rotate right button. With touch-action: pan-y a horizontal drag rotates and a vertical swipe scrolls, so the canvas does not trap touch scrolling. Make sure the object is visibly different when turned (a rotationally symmetric object shows nothing when rotated; add pattern or asymmetry).
- Satisfies: a11y-dragging, a11y-pointer-gestures
- Verification note: Playwright: mouse drag, mouse click and touch tap each changed the rendered frame under reduced motion; touch-action computed as pan-y
### Respect reduced motion (`wg-motion`) [craft-consensus · verified]
Respect reduced motion: show the poster or a still frame, stop continuous camera movement, and keep the motion minimal for everyone around the headline and call to action.
- How: Check matchMedia("(prefers-reduced-motion: reduce)") before starting the loop and listen for its change event (Baseline widely available since September 2020) so the scene reacts when the setting changes.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
```css
@media (prefers-reduced-motion: reduce) {
  .reveal { animation: none; transition: opacity .2s linear; transform: none; }
  .parallax-layer { transform: none !important; }
}
```
### Check reduced motion inside the loop (`wg-motion-listener-gotcha`) [our-take · partly-verified]
Do not rely on the change event alone to react to a reduced-motion switch while a render loop reads .matches; compare the current value inside the loop too.
- How: In Chrome (Playwright emulateMedia), when a requestAnimationFrame loop read matchMedia(...).matches every frame, the page's own change listener did not fire after the setting changed, although a freshly created MediaQueryList did receive the event. Keeping a lastReduce variable and calling the apply function when reduce.matches !== lastReduce inside the frame fixed it. Also keep user-initiated rotate and zoom working under reduced motion, as instant jumps instead of easing.
- Satisfies: a11y-reduced-motion
- Verification note: reproduced with Playwright media emulation in one Chrome build; not reproduced with a real OS setting change
### Cursor effects never replace the cursor (`wg-cursor`) [our-take · judgement]
Cursor-following effects add to the system cursor and never replace it on interactive elements; keyboard focus gets the equivalent highlight; turn the effect off on touch devices and under reduced motion.
- How: Animate transform and opacity only (web.dev: the only two compositor-only properties) and keep layers few (do not promote everything with will-change). Use passive listeners where you never call preventDefault: wheel, touchstart and touchmove on window or document are passive by default, element-level listeners are not. One requestAnimationFrame loop.
- Satisfies: a11y-keyboard, perf-inp
- Verification note: the recommendation is our judgement; the supporting facts (compositor-only properties, passive listener defaults) are verified
### Cursor glow behind content (`wg-cursor-glow-placement`) [our-take · judgement]
Put a cursor glow behind the page content, never over it: fixed, pointer-events:none, z-index below content, transform only, and enable it only for (hover: hover) and (pointer: fine) when motion is not reduced. Keep the glow achromatic or warm and the accent off cyan on a near-black page: a cyan or teal radial halo with alpha under 0.3 fails distinct-no-decorative-glow and a cyan accent on near-black fails distinct-no-ai-palette.
- How: Give html the background and leave body transparent so a z-index:-1 layer is visible. On keyboard focus (focusin where :focus-visible matches) move the glow to the focused control. Declare the pointermove listener passive and drive the glow from the same requestAnimationFrame loop as the scene. Axe reported no contrast problems with the low-opacity glow behind light text. Measured 2026-11-06: switching the accent to sand (#E3C08D) and the halo to rgba(238,243,242,.12) cleared both audit failures; the halo is position:fixed so it never causes scroll.
- Satisfies: a11y-keyboard, a11y-reduced-motion, perf-inp
- Verification note: the placement choices are our judgement; the touch gating was checked with Playwright mobile emulation (hover:hover and pointer:fine both false) and the reduced-motion gating by emulation
### Manage dialog focus and Escape (`webgl-and-3d--comp-dialog-focus`) [craft-consensus · verified]
On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- How: Keyboard only: activate the opener, verify focus is inside; Tab through the whole dialog and confirm wrap; press Escape and confirm close and focus on the opener; confirm a visible close control exists. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-focus
### Prefer visible labels over tooltips (`webgl-and-3d--comp-tooltip-not-sole-label-no-interactive`) [craft-consensus · partly-verified]
Prefer visible labels; if a tooltip is unavoidable, trigger on hover and focus, allow Escape, and keep it text only.
- How: Hover and Tab to each tooltip trigger; press Escape; move the pointer onto the bubble; check aria-describedby; check the bubble DOM for a, button, input. (Derived from the rule; see its sources.)
- Satisfies: comp-tooltip-not-sole-label-no-interactive
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Use a native range input (`webgl-and-3d--comp-slider-semantics`) [craft-consensus · verified]
Prefer input type=range; add output text next to it and aria-valuetext when units matter.
- How: Inspect value attributes; keyboard test arrows/Home/End/PageUp/PageDown; check aria-valuetext shows units; test with VoiceOver on iOS or TalkBack. (Derived from the rule; see its sources.)
- Satisfies: comp-slider-semantics
### Auto-fit grids with min() tracks (`wg-reflow-grids`) [standard · verified]
Write card grids as repeat(auto-fit, minmax(min(15rem, 100%), 1fr)): minmax(15rem, 1fr) is a 480 px track at 200% text.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; the li right edge was 520 px at 320 px; inside the viewport after the change.
- Satisfies: a11y-reflow
