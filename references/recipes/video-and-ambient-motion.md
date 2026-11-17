# Recipe: Hero video, ambient loops and marquees (`video-and-ambient-motion`)
Styles covered: hero-video, ambient-loop, marquee
**Keep:** Full-bleed muted looping video, ambient background loops, ticker rows of logos or text.
**Avoid:** Autoplaying sound; no way to stop motion; important messages inside a scrolling ticker; large video as the LCP with no poster.
Keep the moving backdrop. Decide whether the video is decorative or carries information, give viewers a pause control, never autoplay sound, and keep key messages out of the moving layer.
**While designing:** Decorative muted looping video with a poster as LCP, a visible pause control, no autoplaying sound, static fallback for reduced motion, and key messages in HTML text.
## Steps
### Decide decorative or informative video (`vd-classify`) [craft-consensus · partly-verified]
Decide: is the video decorative and silent, or does it carry speech or information? Decorative: mark it as such and keep every message in text. Informative: it needs captions and a description or transcript.
- How: WCAG 1.2.1 requires an alternative or an audio track for prerecorded video-only content, and its Understanding page does not exempt decorative or background video; 1.1.1 says pure decoration should be ignorable by assistive technology. So: treat a loop as decoration (aria-hidden, no information in it, every message also in text) as an inference from 1.1.1, and add the pause control (2.2.2). A video with speech needs captions (1.2.2) and an audio description or text alternative (1.2.3, 1.2.5).
- Satisfies: a11y-captions, a11y-audio-description
- Verification note: WCAG does not address background video directly; the decorative treatment is an inference from 1.1.1
### Never autoplay sound (`vd-no-sound`) [craft-consensus · verified]
Never autoplay sound. Autoplay muted (or with no audio track), with playsinline, and provide controls to start sound.
- How: Browsers generally block audible autoplay; muted and silent video may autoplay, and playsinline is needed for autoplay in Safari.
- Satisfies: a11y-audio-control
```html
<video autoplay muted loop playsinline poster="/hero.jpg" aria-hidden="true">
  <source src="/hero.mp4" type="video/mp4">
</video>
<!-- script swaps the label between "Pause background video" and "Play background video"; no aria-pressed -->
<button type="button" class="motion-toggle">Pause background video</button>
```
### Keyboard-reachable pause control (`vd-pause`) [craft-consensus · verified]
Give a visible, keyboard-reachable control that pauses or stops automatically starting motion (video, ambient loop, ticker); ideally one control for all moving content. A control that only pauses while hovered or focused does not meet WCAG 2.2.2.
- How: WCAG 2.2.2 applies to moving content that starts automatically (including by hover, focus or scrolling into view), lasts more than five seconds and runs alongside other content; auto-updating content has no five-second exception. Because the label changes between "Pause" and "Play", do not add aria-pressed: the APG button pattern says a toggle's label must stay the same when aria-pressed is used. Remember the choice for the session.
- Satisfies: a11y-pause-stop-hide
### Poster and play button fallback (`vd-handle-denied`) [craft-consensus · verified]
If autoplay is blocked or reduced motion is on, show the poster image and a play button instead of an empty frame.
- How: Catch the play() promise rejection (NotAllowedError) and show the poster or play button.
- Satisfies: a11y-pause-stop-hide, perf-lcp
### Poster as the LCP candidate (`vd-lcp`) [craft-consensus · verified]
Make the poster the LCP candidate: an image discoverable in the initial HTML with fetchpriority="high" and not lazy-loaded; load the video file after it.
- How: A video element is an LCP candidate: its time is the poster image load or the first frame, whichever is earlier. Make the poster an img-like resource discoverable early with fetchpriority="high" where it is the largest element, never lazy-load it, and defer the video file.
- Satisfies: perf-lcp
### Tickers for decoration only (`vd-marquee`) [craft-consensus · verified]
Use tickers for decoration only: pause on hover and focus, duplicate content hidden from assistive technology, no critical information inside, static when reduced motion is on, and never styled like an ad.
- How: Pause on hover or focus is an extra, not a replacement for a persistent control (WCAG: a control that pauses only while focused does not qualify). A static row of the same logos is the reduced-motion version. The APG carousel pattern is a model for rotating content: the rotation control is the first tab stop and rotation stops when focus enters or the mouse hovers.
- Satisfies: ux-no-ad-lookalikes, ux-carousel-caution, a11y-pause-stop-hide
### Calm loops around headline and CTA (`vd-calm`) [our-take · judgement]
Keep the loop calm and slow around the headline and call to action, and let the headline, tagline and logo stay static.
- How: Choose footage with low motion near text areas, or add a scrim.
- Satisfies: ux-minimal-motion
- Verification note: our judgement
### Scroll-snap sliders without autoplay (`video-and-ambient-motion--comp-content-slider-no-autoplay`) [craft-consensus · partly-verified]
Build sliders as scroll-snap lists with labelled prev/next buttons and no autoplay.
- How: Load the page for 30 seconds without input: nothing moves. Tab through: arrows reachable, scroller focusable with visible focus, hidden slides' links not focusable. Check prev/next buttons have names. (Derived from the rule; see its sources.)
- Satisfies: comp-content-slider-no-autoplay
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Live captions for live streams (`video-and-ambient-motion--a11y-captions-live`) [craft-consensus · verified]
If you embed a live stream, use a player and a captioning service that supply live captions.
- How: If the page embeds a live stream, enable captions in the player during the live event and confirm they track speech; otherwise mark not applicable. (Derived from the rule; see its sources.)
- Satisfies: a11y-captions-live
### Scrim behind text on media (`video-and-ambient-motion--craft-contrast-text-on-media`) [craft-consensus · verified]
Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- How: Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (Derived from the rule; see its sources.)
- Satisfies: craft-contrast-text-on-media
### Skip link above video and scrim (`vd-skip-layering`) [craft-consensus · verified]
Give the skip link a z-index above the hero video and scrim so it is visible when focused.
- How: A skip link that is not positioned paints under a later position:relative or absolute hero; set position:absolute with z-index (for example 100) on the skip link. Found by auditing the recipe demo page in Chrome (the Tab traversal probe reported the focused skip link as covered).
- Satisfies: a11y-focus-not-obscured, a11y-bypass-blocks
### Stepped rem hero heading (`vid-hero-type-reflow`) [standard · verified]
Step the hero h1 in rem (2rem, then 2.75rem from min-width: 40em) with overflow-wrap: anywhere; do not use clamp() with vw, which the resize-text check flags.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; a fixed 2.75rem h1 overflowed a 224 px content box by 33 px at 200% text; the stepped size fitted the longest word at 223 px in a 256 px box.
- Satisfies: a11y-reflow
