# Recipe: Scroll-driven stories, parallax and text effects (`scroll-stories`)
Styles covered: chaptered-story, scroll-triggered, parallax, long-scroll-narrative, text-effects
**Keep:** Pinned sections, chapters, reveal-on-scroll, parallax layers, kinetic type.
**Avoid:** Scroll hijacking; content that exists only after an animation; the call to action buried at the end; effects with no reduced-motion version.
Keep the sense of a narrative that unfolds. Use native scrolling, keep content in the page whether or not the effect runs, give the most important information and the main action early, and offer a reduced version.
**While designing:** Use native scroll and CSS timelines with @supports, keep all content in the DOM, put the point and primary action early, add a reduced-motion version, and keep effects to transform and opacity.
## Steps
### Keep native scrolling (`ss-native-scroll`) [craft-consensus · verified]
Use the browser's own scrolling with sticky positioning or scroll-linked animation; do not take over scroll speed or direction.
- How: CSS scroll-driven animations (animation-timeline: scroll() or view()) are Baseline 2026 and absent in older browsers; feature-detect with @supports and show the final state when unsupported. Declare animation-timeline after the animation shorthand.
- Satisfies: a11y-pause-stop-hide, perf-inp
### Sticky figures on wide screens only (`ss-sticky-wide-only`) [our-take · judgement]
Pin a figure with position: sticky only where there is room beside the text (about 56em and wider); on narrow screens let it scroll with the page. Do not make the header sticky.
- How: A sticky figure in a single column covers the paragraphs it should sit beside, and a sticky header can fully cover a focused link. Use scroll-padding-top if a fixed bar is unavoidable, and keep decorative fixed elements (a progress bar) pointer-events:none and aria-hidden.
- Satisfies: a11y-focus-not-obscured, a11y-reflow
- Verification note: design advice; no fixed header was tested because the demo avoids one
### Base style is the finished state (`ss-final-state-everywhere`) [our-take · verified]
Every effect, including purely decorative ones such as a progress bar, must have a base style that is already its finished state; set the effect's starting state only inside the @supports block.
- How: Put the whole effect layer in @supports (animation-timeline: view()) { ... } and keep the base rules free of starting states (opacity:0, translate, scaleX(0)). In the demo the progress bar had transform:scaleX(0) in the base rule, so in a browser without scroll timelines it would sit at zero forever; the fix was display:none in the base rule and display:block plus scaleX(0) inside @supports.
- Satisfies: perf-core-first, a11y-reduced-motion
- Verification note: checked by renaming animation-timeline in a copy of the page to simulate no support and reading computed styles; the other effects were already final in that state
### Content in the DOM first (`ss-content-first`) [craft-consensus · verified]
All text and links exist in the DOM in reading order, visible without the animation. An effect may reveal or move content, not create it.
- How: Test with JavaScript off and with the effect stylesheet removed.
- Satisfies: perf-core-first
### Open with the point (`ss-front-load`) [our-take · verified]
Open with the point: what the page is and who it is for in the first chapter, and the primary action visible in the first viewport and repeated as the story ends.
- How: A story can build, but the first screen must already answer what and why.
- Satisfies: ux-front-load, ux-primary-cta-above-fold
### Fades instead of large movement (`ss-reduced`) [craft-consensus · verified]
Under reduced motion replace large movement (parallax, scaling, sliding) with fades or a static layout, and keep what the motion conveyed.
- How: Swap transforms for opacity changes in the reduce media query rather than deleting content.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
```css
@media (prefers-reduced-motion: reduce) {
  .reveal { animation: none; transition: opacity .2s linear; transform: none; }
  .parallax-layer { transform: none !important; }
}
```
### Opacity-only reveals under reduce (`ss-reduced-keep-fade`) [craft-consensus · verified]
In the reduce query, keep the reveals as an opacity-only fade on the same timeline and set parallax and pinned-figure animation to none, so the figure shows its final state and the caption states what the motion showed.
- How: Nest @media (prefers-reduced-motion: reduce) inside the @supports block and swap the keyframes name for an opacity-only keyframe; set animation:none on parallax layers and on the pinned figure. Playwright with reducedMotion:'reduce' confirmed computed transform:none on the parallax layer, the water level and the line masks, with opacity fades still driven by view(). Always give the figure a text caption with the numbers or years the motion conveyed.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
```css
@supports (animation-timeline: view()) {
  .reveal { animation: rise linear both; animation-timeline: view(); animation-range: entry 0% entry 55%; }
  @media (prefers-reduced-motion: reduce) {
    .reveal { animation: fade linear both; animation-timeline: view(); animation-range: entry 0% entry 55%; }
    .parallax-layer { animation: none; transform: none; }
  }
}
```
### Shallow parallax, never behind text (`ss-parallax-limits`) [our-take · partly-verified]
Keep parallax shallow, never behind text, and stop it when the user asks for less motion; parallax layers are decoration.
- How: WCAG 2.3.3 (Level AAA) names parallax scrolling as a common non-essential motion effect and recommends honoring the reduced-motion setting (technique C39, JavaScript SCR40). Limiting depth and turning it off on small screens is our judgement.
- Satisfies: a11y-pause-stop-hide, a11y-reduced-motion
- Verification note: depth and small-screen advice is our judgement; the rule that parallax should be disable-able is verified
### Keep text as real text (`ss-text-effects`) [craft-consensus · partly-verified]
Keep text as real text. Prefer effects that do not split it (masks, whole-line reveals). If you must split text into spans, keep the full string available to assistive technology once, and hide the pieces.
- How: MDN: aria-label is not supported on generic elements (a bare div or span), so do not rely on it on a parent of split spans. Either give the container a role that supports naming where one genuinely fits, or add one screen-reader-only element holding the full text (WebAIM: off-screen positioning or a 1 px clip-based technique; never display:none or hidden) and mark the split spans aria-hidden (MDN lists duplicated or redundant text as a use; never on or around focusable elements). Use sparingly and test with a screen reader.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
- Verification note: the two techniques are verified; applying them to split-text effects is our composition and no page addresses it
### Animate transform and opacity only (`ss-inp`) [craft-consensus · verified]
Drive effects from compositor-friendly properties (transform, opacity) and avoid reading layout in scroll handlers.
- How: Prefer CSS timelines or IntersectionObserver to scroll listeners, and animate transform and opacity only (the only compositor-only properties, per web.dev).
- Satisfies: perf-inp
### Keep animated shapes in their box (`ss-animated-shapes-inside-box`) [our-take · verified]
Keep animated geometry inside its container: scale an SVG shape from its edge (transform-box: fill-box; transform-origin: 50% 100%) instead of translating a taller shape out of its viewBox.
- How: axe-core's color-contrast rule reported 'background color could not be determined because it is overlapped by another element' for the figcaption under a pinned SVG, caused by a translated rect whose box extended below the SVG's viewBox. Removing the animation cleared it; replacing translateY with scaleY and transform-box: fill-box cleared it with the animation kept (a11y-contrast-text went from 'check' to clean).
- Satisfies: a11y-contrast-text, perf-cls
- Verification note: axe incomplete count went from 1 to 0 on the demo at desktop and mobile widths after the change
### Sentences of about 15 words (`scroll-stories--copy-sentence-length`) [craft-consensus · partly-verified]
Write body sentences of about 15 words, split any that pass 25, and read each aloud before keeping it.
- How: Extract visible text of p, li and blockquote elements, split on sentence terminators, count words per sentence. Fail on any sentence over 25 words; fail the page if the mean exceeds 20. Ignore headings, buttons and legal text. (Derived from the rule; see its sources.)
- Satisfies: copy-sentence-length
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headings that state the finding (`scroll-stories--copy-heading-informative`) [craft-consensus · partly-verified]
Write each heading as the finding of its section, so the headings alone tell the story.
- How: Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (Derived from the rule; see its sources.)
- Satisfies: copy-heading-informative
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Minmax tracks and wrapping words (`ss-reflow-grids-and-words`) [standard · verified]
Give one-column grids an explicit grid-template-columns: minmax(0, 1fr) (an implicit auto track grows to its min-content), use minmax(min(15rem, 100%), 1fr) for card grids and overflow-wrap: anywhere on headings and paragraphs.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; scrollWidth went 520, then 327, then 351 (text spacing on long words) and finally 320 after the three changes.
- Satisfies: a11y-reflow
