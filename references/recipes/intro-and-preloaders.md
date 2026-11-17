# Recipe: Intro animations and preloaders (`intro-and-preloaders`)
Styles covered: intro-preloader
**Keep:** A designed opening moment, a branded reveal.
**Avoid:** A screen that blocks content until assets load; long sequences on every visit; counters that count up while nothing is ready; layout shifts when the overlay leaves.
Prefer no preloader. If the brand needs an opening moment, keep it short, skippable and non-blocking so it costs no loading time, causes no layout shift and does not read as a popup.
**While designing:** Default to no preloader; if one is required keep it once-per-session, skippable, non-blocking, free of layout shift, and off under reduced motion.
## Steps
### Ask if a preloader is needed (`ip-prefer-none`) [evidence · verified]
First ask whether the preloader is needed. A progressive reveal of real content (headline, then image) gives the same feeling without hiding the page.
- How: NN/g lists popups and splash screens among the most disliked homepage elements, except where legally required.
- Satisfies: ux-no-popups, perf-lcp
### Short, skippable, once per session (`ip-short-skippable`) [our-take · judgement]
If you keep it: show it once per session, make it very short, let any key press or click skip it, and remove it from the page afterwards.
- How: Store a session flag; skip entirely under reduced motion. WCAG 2.2.2 notes a preload animation may count as essential only when users cannot interact during the preload and the animation signals progress.
- Satisfies: ux-no-popups, a11y-reduced-motion
- Verification note: the session flag and skip behavior are our judgement
```css
@media (prefers-reduced-motion: reduce) {
  .reveal { animation: none; transition: opacity .2s linear; transform: none; }
  .parallax-layer { transform: none !important; }
}
```
### Narrow skip keydown handler (`ip-skip-listener-audit-note`) [our-take · verified]
Expect the audit to flag a document-level keydown handler for the skip, and keep the handler narrow: it only removes the curtain, then unregisters itself.
- How: The audit counts addEventListener('keydown') on window or document at registration time and reports a11y-char-shortcuts as 'incomplete' (a person must check), not as a failure. Registering on the curtain element is not possible because it is not focusable and has pointer-events:none. Remove the listener inside done() and do not map any individual key to another action.
- Satisfies: a11y-char-shortcuts
- Verification note: the audit printed 'check [major] a11y-char-shortcuts: 1 document-level keydown handler(s) registered' for the demo; no failure
### Read session flag before paint (`ip-session-flag-before-paint`) [our-take · partly-verified]
Read the session flag and the reduced-motion setting in a tiny inline script before first paint, and add the 'intro-on' class only if the intro should play.
- How: If the decision is made after paint, returning visitors see the curtain flash. A one-line synchronous script in the head (sessionStorage.getItem plus matchMedia, wrapped in try/catch because storage can throw) avoids that. This is the one head script this recipe allows; keep it under about 300 bytes and put everything else at the end of the body. Measured with the audit: LCP 40 to 50 ms, CLS 0.000, TBT 0 ms with it.
- Satisfies: ux-no-popups, a11y-reduced-motion
- Verification note: the cost of the script was measured in lab runs; the flash it prevents was reasoned about, not recorded
### Decorative curtain mechanics (`ip-curtain-mechanics`) [our-take · verified]
Implement the intro as a decorative curtain: aria-hidden, position:fixed, pointer-events:none, animated with transform only and finishing in visibility:hidden, removed from the DOM on animationend, with a timeout as a safety net.
- How: The real page underneath is already painted and interactive. Hide the curtain by default in CSS and show it only when a flag is set, so with JavaScript off it never appears (add a noscript rule too). Any key press or pointerdown calls the same done() function, which removes the curtain, removes both listeners and stores the session flag. Playwright confirmed: curtain present at 100 ms, removed by 1.75 s, removed within 80 ms after Space or a click, absent after a reload in the same session, never present under reduced motion or with JavaScript off.
- Satisfies: ux-no-popups, perf-cls, perf-lcp
### Never delay main content (`ip-lcp`) [craft-consensus · verified]
Never delay the main content for the animation. Measure LCP with and without the preloader; the page content loads underneath it.
- How: Make the LCP resource discoverable in the initial HTML and not lazy-loaded; keep render-blocking CSS and head scripts small.
- Satisfies: perf-lcp
### Measure LCP and CLS both ways (`ip-measure-with-without`) [craft-consensus · verified]
Measure LCP and CLS twice, with the flag unset and with it preset, using a PerformanceObserver; the difference should be noise.
- How: In Playwright, run once normally and once with addInitScript("sessionStorage.setItem('flag','1')"), and observe largest-contentful-paint and layout-shift with buffered:true. Demo result in lab Chrome: with the curtain LCP 52 ms (h1), without 36 ms (h1), CLS 0 in both; the curtain's own text was not the LCP element.
- Satisfies: perf-lcp, perf-cls
- Verification note: single-run lab numbers on a local file; field data will differ
### Overlay exit moves nothing (`ip-cls`) [craft-consensus · verified]
The overlay leaving must not move content: reserve all space, animate with transform and opacity, and keep fonts and images from reflowing.
- How: Set width and height or aspect-ratio on images and video, reserve space for anything that arrives late, and animate transform and opacity rather than top, left or box-shadow so the overlay leaving does not move content. Check layout shift in a performance trace across the whole sequence.
- Satisfies: perf-cls
### Minmax tracks and wrapping buttons (`ip-reflow-200`) [standard · verified]
Use minmax(0, 1fr) for hero grid tracks, minmax(min(15rem, 100%), 1fr) for card grids, and overflow-wrap: anywhere with max-width: 100% on buttons and long call-to-action labels, so nothing stretches the page at 320 px with 200% text.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; a 1fr track sized to its min-content gave a 335 px column, cards at minmax(15rem,1fr) were 480 px; after the changes scrollWidth was 320.
- Satisfies: a11y-reflow
### Avoid the cream-terracotta-serif reflex (`ip-no-reflex-cream`) [our-take · partly-verified]
If the page uses cream, terracotta and serif display type together, that trips distinct-palette-not-reflex-cream and an HTML comment does not satisfy the audit: pick sans headings or another palette unless the brief requires the combination, and record the reason in direction.md.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; advisory failed with cream, terracotta and serif; it passed after switching to bold system sans headings. The check is static and ignores comments.
- Satisfies: distinct-palette-not-reflex-cream
- Verification note: Recorded from one audit run on one demo page; the audit check is a heuristic and the technique has no independent source.
