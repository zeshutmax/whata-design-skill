# Recipe: Photography-led and centered heroes with readable text and fast images (`hero-and-photography`)
Styles covered: photography, hero-centered, standout-hero
**Keep:** Large photographs, a centered headline and subline, a strong first screen, cropped imagery with a clear subject.
**Avoid:** White text straight on a photo; a hero image that loads late and shifts the page; the hero image as a CSS background or lazy-loaded; alt text that describes nothing; centered paragraphs of three lines or more; the stock centered badge, headline, two buttons and logo row; a headline a competitor could publish unchanged.
Keep the full-bleed photograph and the big centered headline. Put a measured scrim behind text, reserve image space and never lazy-load the hero image, write real alt text, centre only short lines, and build the first screen around something only this subject has.
**While designing:** Photo hero with a 60% scrim behind text, hero img in HTML with width, height and fetchpriority high, center only a two-line subline, and a first screen built around a real subject element and a headline a competitor could not copy.
## Verified palette: Scrim math for text over the brightest photo, computed
- text: #FFFFFF
- scrim-60: rgb(0 0 0 / 0.6)
- worst-case backdrop: #FFFFFF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white text on 60% black scrim over pure white | #FFFFFF | #666666 | 5.74:1 | 4.5:1 |
| white text on 55% black scrim over pure white | #FFFFFF | #737373 | 4.74:1 | 4.5:1 |
| large white text (24px+) on 42% scrim over pure white | #FFFFFF | #949494 | 3.03:1 | 3:1 |
| white text on 50% black scrim over bright yellow #FFD400 | #FFFFFF | #806a00 | 5.27:1 | 4.5:1 |
## Steps
### Scrim between photo and text (`hp-scrim`) [standard · verified]
Put a scrim between the photo and any text: a 60% black overlay (or a gradient that stays at or above 55% under the text lines) keeps white text at 4.5:1 or better over even a pure white photo. Test the brightest area at 375, 768 and 1440px, not the average.
- How: Computed: the minimum black overlay alpha for white text at 4.5:1 over pure white is 0.54 (0.42 for 24px-and-larger text at 3:1). A 0.6 overlay gives 5.74:1, 0.55 gives 4.74:1, and over bright yellow #FFD400 a 0.5 overlay gives 5.27:1. Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 20rem hero with a pure-white image and a 0.6 gradient overlay rendered #666666 under the heading (pixel sampled from a screenshot), a ratio of 5.74:1 with white text. Real photos have bright spots, so check the lightest area behind each line.
- Satisfies: craft-contrast-text-on-media, a11y-contrast-text, a11y-coga-text-not-over-busy-background
```css
.hero { position: relative; color: #fff; isolation: isolate; }
.hero::before { content: ""; position: absolute; inset: 0; z-index: -1;
  background: linear-gradient(to top, rgb(0 0 0 / 0.6), rgb(0 0 0 / 0.6)); }  /* flat 60% under text */
```
### Hero img with alt and priority (`hp-alt-lcp`) [craft-consensus · verified]
Put the hero image in the HTML as an img with width and height, fetchpriority="high" and no loading="lazy". Write alt text for what the image adds in context (under about 150 characters, key words first), alt="" if it is decoration, and describe the destination for linked images.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a test page whose below-the-fold figure loaded 800 ms late measured CLS 0.0293 without width and height attributes and 0.0000 with them. web.dev: never lazy-load the LCP image, make it discoverable in the initial HTML (not a CSS background or script-injected), and fetchpriority="high" on one or two images at most. NN/g: decorative images get alt=""; informative images say what they contribute; keep alt under roughly 150 characters with the important words first.
- Satisfies: a11y-alt-text, craft-image-dimensions-reserved, a11y-coga-no-surprise-changes
```html
<img src="/img/harbour-1600.jpg" width="1600" height="900"
     srcset="/img/harbour-800.jpg 800w, /img/harbour-1600.jpg 1600w" sizes="100vw"
     fetchpriority="high" alt="Fishing boats moored in the old harbour at low tide">
```
### Crop to the subject, never stretch (`hp-crop`) [craft-consensus · partly-verified]
Fill the frame with object-fit: cover and set object-position to the subject; at small widths switch to a portrait crop with picture and media, instead of letting the subject fall outside the frame. Never stretch: the rendered ratio must match the file unless object-fit crops it.
- How: The picture element selects a different crop per media condition (web.dev Learn Responsive Design, The picture element and Responsive images). object-fit and aspect-ratio are Baseline features documented on MDN; pair aspect-ratio or width/height with the crop so the box is reserved before load.
- Satisfies: craft-image-no-distortion, craft-image-dimensions-reserved
- Verification note: The crop techniques are documented, but the MDN object-fit and aspect-ratio pages were only partly read and no crop was rendered or measured here.
```css
.hero img { inline-size: 100%; block-size: 100%; object-fit: cover; object-position: 60% 40%; }
```
### Center only headline and short subline (`hp-centered`) [craft-consensus · partly-verified]
Center only the headline and a subline that wraps to two lines or fewer. Below 48em start-align the subline, above it cap it near 56ch so it stays at two lines. Balance the headline with text-wrap: balance and keep it at 6rem or below.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 98-character subline with a 34ch cap, centered at 768 px and wider, wrapped to 3 lines (fails the "no centered paragraph of 3 lines or more" check); with a 56ch cap above 48em it wrapped to 2 lines at 768 and 1280 px, and below 48em it was start-aligned (3 lines at 320 and 390 px). The guideline's sources (Butterick on justified text and hyphenation, WCAG 1.4.8 visual presentation) favour start-aligned body text.
- Satisfies: craft-align-left-body, craft-text-wrap-balance-pretty, distinct-hero-headline-proportion
- Verification note: The line counts were measured for one sample sentence and fonts; recheck with your copy. Source support for avoiding centered paragraphs is general (start-aligned text), not a numeric line limit; the 3-line cut-off is the guideline's.
```css
h1 { font-size: 2.25rem; line-height: 1.05; text-wrap: balance; overflow-wrap: anywhere; }
.sub { max-inline-size: 34ch; }
@media (min-width: 48em) { h1 { font-size: 3.25rem; } }
@media (min-width: 64em) { h1 { font-size: 4.5rem; } }
@media (min-width: 48em) { .hero { text-align: center; } .sub { max-inline-size: 56ch; margin-inline: auto; } }
```
### Show something real in first viewport (`hp-not-template`) [craft-consensus · partly-verified]
Make the first viewport show something real from the subject (the product screen, the work, the place, the object) and keep at most two of the five stock signals: centered headline, badge or eyebrow above it, exactly two buttons, a logo row in the next section, a three-card feature row after that. A centered photographic hero usually keeps the first and drops the badge.
- How: These are the guideline's checks. No "New" or "Live" pill unless it is bound to a real state or release. Name the lead element of the hero in the written direction file before building so it is a decision, not a leftover.
- Satisfies: distinct-hero-not-template, distinct-no-fake-status-badges, distinct-real-imagery-and-icons, distinct-written-direction
- Verification note: The five-signal count comes from detector-style guidelines with partly read sources; NN/g homepage principles (read) support showing real content on the first screen, not the exact threshold.
### Headline that passes the swap test (`hp-headline`) [craft-consensus · partly-verified]
Write the H1 and subline so they name the outcome, the offer or the audience, then run the swap test: paste a direct competitor's name in and see whether it is still true. If so, rewrite with a noun, number or place only this product can claim. Avoid the template "The [modern] [category] for [teams]".
- How: Weak (illustrative): "The modern platform for teams that move fast." Stronger (illustrative): "Pay 40 suppliers in one afternoon", which states an outcome and a number. NN/g: headings are pick-up lines, so lead with the specific value in the first words. The page title should name the page's purpose too, so it is not left as the brand name alone.
- Satisfies: copy-headline-swap-test, a11y-headings-labels, a11y-page-title
- Verification note: The swap test is a manual check with a craft rationale; the example headlines are invented for illustration, and no experiment is cited that these convert better.
