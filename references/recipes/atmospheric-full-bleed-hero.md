# Recipe: Atmospheric full-bleed heroes with text you can read (`atmospheric-full-bleed-hero`)
Styles covered: atmospheric, hero-full-bleed
**Keep:** Edge-to-edge photography or illustration, haze, grain, gradients and colour atmosphere.
**Avoid:** White text on a photo with no scrim; a scrim tuned to the average rather than the brightest pixel; no fallback colour behind the image; text across the full 1920 px of a monitor; relying on a gradient scrim that forced-colours mode removes.
Keep the edge-to-edge image, the haze, grain and light. Put one scrim under the text column, tuned for the brightest pixel the image can offer, keep a dark colour behind the image for when it fails, and hold the content in a normal container while only the picture bleeds.
**While designing:** Choose a scrim colour and alpha from the brightest pixel under the text (0.72 of a near-black reaches 7:1 over pure white), set a dark background-color on the hero, keep atmosphere on its own aria-hidden layer, limit the content to a 1280px wrapper and a text column of about 36rem, and measure the rendered pixels at 375, 768, 1440 and 1920 px.
## Verified palette: Scrim over bright imagery, computed
- scrim: #0B1020 at 72%
- text: #FFFFFF
- text-muted: #D5DAE6
- fallback-ground: #0B1020
- worst-case-white: #FFFFFF
- worst-case-yellow: #FFE600
- worst-case-sky: #BFE9FF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white on 72% scrim over pure white (worst case) | #FFFFFF | #4F535E | 7.69:1 | 7:1 |
| white on 72% scrim over bright yellow #FFE600 | #FFFFFF | #4F4C17 | 8.83:1 | 7:1 |
| white on 72% scrim over pale sky #BFE9FF | #FFFFFF | #3D4D5E | 8.67:1 | 7:1 |
| muted #D5DAE6 on 72% scrim over pure white | #D5DAE6 | #4F535E | 5.49:1 | 4.5:1 |
| white on the fallback colour shown if the image fails | #FFFFFF | #0B1020 | 18.93:1 | 7:1 |
## Steps
### One scrim for the brightest pixel (`am-scrim`) [standard · verified]
Lay one scrim under the text column and tune it for the brightest pixel the image can offer, not the average. A #0B1020 scrim at 72% gives white text 7.69:1 over pure white, 8.83:1 over yellow #FFE600 and 8.67:1 over pale sky #BFE9FF; muted #D5DAE6 text is 5.49:1 over pure white.
- How: Composite the scrim over the worst backdrop, then compute the WCAG ratio; 72% is where white reaches 7:1 (AAA for body text) on a pure white backdrop, with 4.5:1 as the minimum for muted text. Method used to verify in Chrome 156: hide the text, screenshot the text box, read every pixel and take the smallest ratio. On a test image that is white, bright yellow and pale sky behind the text, the headline measured 7.69, 8.53, 8.64 and 8.64:1 at 375, 768, 1440 and 1920 px, the lead 7.69, 8.53, 7.65 and 7.65, and the muted line 5.49, 5.49, 5.47 and 5.47. The same page without the scrim measured 1.27:1 against the worst pixel.
- Satisfies: craft-contrast-text-on-media, craft-contrast-body-enhanced, a11y-coga-text-not-over-busy-background
```css
.hero-scrim { position: absolute; inset: 0;
  background: linear-gradient(90deg, rgb(11 16 32 / .72) 0%, rgb(11 16 32 / .72) 60%, rgb(11 16 32 / 0) 100%); }
@media (max-width: 60rem) { .hero-scrim { background: rgb(11 16 32 / .72); } }  /* text spans the width */
```
### Dark hero background fallback (`am-fallback`) [craft-consensus · verified]
Set a dark background-color on the hero element itself, under the image, so white text still has 18.93:1 when the image is slow, blocked or fails to load.
- How: Without it, white text on a missing image falls back to the page background and disappears. Chrome demo: with the image and scrim removed the hero computes to rgb(11, 16, 32) behind white text. Also keep real, meaningful alt text on the image when it carries content; the demo image is decorative and has alt="".
- Satisfies: craft-contrast-text-on-media
### Forced-colors text block fallback (`am-forced`) [craft-consensus · verified]
Do not rely on a gradient scrim for readability in forced-colors mode: it is removed. Under @media (forced-colors: active) give the text block a Canvas background and CanvasText colour with a visible border, so the pair is a guaranteed system contrast.
- How: MDN: in forced-colors mode background-image is forced to none unless it is URL-based, and colours become system colours. Measured in Chrome 156 with forced colours emulated over a dark photo: the scrim computes to none, the headline is black and the worst rendered contrast is 1.15:1 without a plate, and 21:1 with a Canvas plate. This is a small usability tweak, which MDN allows; do not build a separate forced-colors design. The emulation uses a light system theme; a black high-contrast theme flips the colours, not the logic.
- Satisfies: craft-contrast-text-on-media, a11y-coga-text-not-over-busy-background
```css
@media (forced-colors: active) {
  .copy { background-color: Canvas; color: CanvasText; padding: 1.25rem; border: 2px solid CanvasText; }
}
```
### Only the picture bleeds (`am-container`) [craft-consensus · verified]
Let only the picture bleed. Put the headline, text and call to action in a centred wrapper of 1280 px or less, with a text column of about 36rem, and give the hero image and band the full width.
- How: At a 1920 px viewport the Chrome demo measures the hero and image at 1920 px, the wrapper at 1280 px and the text column at 576 px. The advisory rule allows only backgrounds and full-bleed media to exceed 1400 px.
- Satisfies: craft-container-max-width
### Atmosphere layer below the scrim (`am-atmosphere`) [craft-consensus · verified]
Keep haze, grain and light leaks on their own aria-hidden, pointer-events:none layer between the image and the scrim, and measure the text with that layer on. Never place text on atmosphere alone; scrim first, then text.
- How: The grain layer (opacity 0.12, repeating radial dots) is part of the screenshot in the pixel measurements above, so the reported ratios include it. W3C COGA asks for text on solid or low-detail backgrounds or a solid panel or overlay, and says text over photos, video, gradients and patterns of varying luminance is a barrier.
- Satisfies: a11y-coga-text-not-over-busy-background, craft-contrast-text-on-media
