# Recipe: SaaS stacks, single-column pages, social proof, pricing tables and event sites (`saas-proof-pricing-event`)
Styles covered: saas-stack, single-column, standout-social-proof, standout-pricing, event-site
**Keep:** Hero, proof, features, pricing and final call to action in a familiar order; one centered reading column; logos, quotes and numbers; a highlighted plan; event dates, schedule and registration.
**Avoid:** The stock sequence with no reason; eight sections of identical padding and layout; invented logos, numbers and quotes; a logo marquee that cannot be paused; a featured plan shown by colour alone; plan names with no stated limits; hidden fees; a live stream without live captions; an auto-updating countdown that is announced every second.
Keep the classic landing sequence, the single centered column, the logo and testimonial proof, the featured pricing plan and the event countdown. Order sections by the buyer's questions, vary their shape, show only proof you can name, build pricing as a real table with units, and caption any live stream.
**While designing:** Order sections by buyer questions, vary section shapes, use only named proof, build pricing as a captioned table with units and a text-marked featured plan, and give any live stream live captions.
## Verified palette: Pricing and event colours, computed
- text: #16181D
- background: #FFFFFF
- featured-plan: #1D4ED8
- badge: #FDE68A
- logo-grey: #767676
- event-background: #0F172A
- event-accent: #FACC15
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white on featured plan header | #FFFFFF | #1D4ED8 | 6.7:1 | 4.5:1 |
| ink on "Most popular" badge | #14171A | #FDE68A | 14.44:1 | 4.5:1 |
| muted price note on white | #4B5563 | #FFFFFF | 7.55:1 | 4.5:1 |
| struck-through old price on white | #6B7280 | #FFFFFF | 4.83:1 | 4.5:1 |
| logo grey on white (graphic, 3:1) | #767676 | #FFFFFF | 4.54:1 | 3:1 |
| quote text on light surface | #14171A | #F3F4F6 | 16.34:1 | 4.5:1 |
| caption on light surface | #4B5563 | #F3F4F6 | 6.86:1 | 4.5:1 |
| white on event night | #FFFFFF | #0F172A | 17.85:1 | 4.5:1 |
| yellow accent on event night | #FACC15 | #0F172A | 11.65:1 | 4.5:1 |
| night text on yellow button | #0F172A | #FACC15 | 11.65:1 | 4.5:1 |
## Steps
### Order sections by buyer questions (`sp-sequence`) [craft-consensus · partly-verified]
Write the page brief as a list of the questions this buyer asks and the section that answers each, then order the stack by it. Keep the hero, proof, features, pricing and call to action only if each answers a question; vary section shapes (full-bleed, split, list, quote, table) so no layout family runs more than two sections in a row and an eight-section page uses at least four families. Vary the vertical padding.
- How: These are the guideline checks. For the hero, see the hero-and-photography recipe. For tile grids, see bento-and-card-grids. Content strategy sources (Halvorson, NN/g homepage principles) support organizing by user goals rather than by template.
- Satisfies: copy-section-content-drives-structure, distinct-section-rhythm-varied, distinct-no-identical-card-grid, distinct-hero-not-template
- Verification note: The thresholds are from detector-style guidelines; sources were partly read or are practitioner posts. This is craft advice with no study behind the numbers.
### Named grid lines in one column (`sp-single-column`) [craft-consensus · verified]
For a single-column page, build the column with named grid lines so text sits at 55ch, figures break out to a wider track and one band runs full width. That varies the rhythm without leaving the one-column reading order.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with this grid, paragraphs were 288 px wide at 320 px (no overflow, scrollWidth 320) and 729 px (66ch at 18px serif) at 768, 1280 and 1920 px, and the wide figure was 969 px at 1280 and 1920, with no horizontal scroll at 320, 768, 1280 or 1920 px. Zero the default figure margin or the figure shrinks (it was 208 px at 320 until margin: 0).
- Satisfies: distinct-section-rhythm-varied, craft-measure-body, craft-container-max-width, a11y-reflow
```css
.flow { display: grid; max-inline-size: 90rem; margin-inline: auto;
  grid-template-columns: [full-start] minmax(1rem, 1fr) [wide-start] minmax(0, 10rem)
    [content-start] min(55ch, 100% - 2rem) [content-end] minmax(0, 10rem) [wide-end] minmax(1rem, 1fr) [full-end]; }
.flow > * { grid-column: content; }
.flow > .wide { grid-column: wide; }
.flow > .full { grid-column: full; }
.flow figure { margin: 0; }
```
### Show only proof you can name (`sp-proof-real`) [our-take · partly-verified]
Show only proof you can name. Every statistic, quote, logo, award and superlative has a source on the page (customer name, role, date, report link) or is removed. List missing proof as a content gap for the owner instead of inventing it. Run a placeholder check before shipping. Show logos as img with alt text of the company name, no auto-scrolling marquee, in grey that keeps 3:1 against the ground.
- How: Computed: logo grey #767676 on white is 4.54:1 (a lighter #B0B0B0 is 2.16:1, which fails 3:1 for a graphic that identifies a customer). Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the placeholder pattern below matched "Acme Corp saved us 40%", "John Doe, CEO" and "Lorem ipsum dolor" and did not match "Mara Ilves, head of ops at Tallinn Bakery". WCAG 2.2.2 requires auto-moving content that runs longer than five seconds to be pausable, so prefer a static logo row. Prefer a named figure with a date ("Median ticket reply time, Q3 2026") over an unlabeled big number.
- Satisfies: copy-proof-verifiable, distinct-no-filler-copy, distinct-no-fake-status-badges, a11y-alt-text, a11y-pause-stop-hide, a11y-non-text-contrast
- Verification note: Contrast and the regex behavior were computed and tested. The rule "show only proof with a named source" is our-take; whether named proof converts better than anonymous proof was not tested.
```js
const placeholder = /\b(lorem ipsum|john doe|jane (doe|smith)|acme|globex|initech|company name|your (company|name) here)\b/i;
[...document.querySelectorAll("main *")].filter(e => placeholder.test(e.textContent) && !e.children.length);
```
### Testimonials as figure and blockquote (`sp-testimonials`) [craft-consensus · partly-verified]
Mark each testimonial as a figure with a blockquote and a figcaption holding the name, role, company and date, with a cite link to the source when one exists. Use static quotes or a plain list, not an autoplaying carousel. Quote text keeps 4.5:1 on its surface.
- How: figure and blockquote carry the quote and its attribution in the markup (WCAG 1.3.1). NN/g found carousels are often skipped, and the APG carousel pattern requires a control to stop and start any automatic rotation. Computed: near-black text on #F3F4F6 16.34:1, caption #4B5563 6.86:1.
- Satisfies: a11y-semantic-structure, comp-content-slider-no-autoplay, a11y-contrast-text, copy-proof-verifiable
- Verification note: Markup follows WCAG and HTML semantics; the example quote and person are invented placeholders and must be replaced by supplied proof. Screen reader output was not tested.
```html
<figure>
  <blockquote cite="https://example.com/case-study"><p>We cut month-end close from six days to three.</p></blockquote>
  <figcaption>Mara Ilves, head of operations, Tallinn Bakery, March 2026</figcaption>
</figure>
```
### Pricing as a real table (`sp-pricing-table`) [craft-consensus · verified]
Build the comparison as a real table: caption (stating currency, billing period and tax), thead with th scope="col", every row label a th scope="row", limits with units ("Up to 15 users", "100 GB"), all recurring costs in the table. Mark the featured plan with text ("Most popular"), not colour alone, and keep white text on its header at 4.5:1. On narrow screens let the table scroll inside a focusable labelled region.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 3-plan table in a 288 px wrapper (min table width 36rem) had page scrollWidth 320 (no page-level overflow) and its wrapper scrolled to 576 px; axe-core 4.14 flagged the wrapper as scrollable-region-focusable (serious) until it had tabindex="0", role="region" and aria-labelledby="cap", then reported no violations. White on #1D4ED8 is 6.7:1; the "Most popular" badge, ink on #FDE68A, is 14.44:1. NN/g: state the differences between options explicitly, with units, and show all costs together.
- Satisfies: copy-explicit-option-differences, comp-data-table-semantics, comp-data-table-overflow-focusable, a11y-color-not-only, a11y-coga-costs-up-front, a11y-reflow, a11y-contrast-text
```html
<div class="scroll" tabindex="0" role="region" aria-labelledby="cap">
 <table>
  <caption id="cap">Plans compared. Prices are per workspace per month, billed monthly, in US dollars, excluding tax.</caption>
  <thead><tr><th scope="col">Feature</th><th scope="col">Starter</th>
    <th scope="col">Team <span class="badge">Most popular</span></th><th scope="col">Business</th></tr></thead>
  <tbody><tr><th scope="row">Users</th><td>Up to 3 users</td><td>Up to 15 users</td><td>Up to 100 users</td></tr></tbody>
 </table>
</div>
```
### Stable-name billing toggle (`sp-pricing-toggle`) [craft-consensus · partly-verified]
If a monthly or yearly switch changes the prices, make it one native toggle button named "Billed yearly" whose name never changes and whose state is aria-pressed (or two radios in a fieldset with a legend). After the switch, update the prices in the table and announce the change through a status region that already exists in the DOM; show the yearly total beside the monthly figure.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a toggle button named "Dark mode" kept the same accessible name before and after, exposed "pressed" through aria-pressed, and toggled with both Space and Enter; a role="status" region filled after an action was read back as text (see the interaction recipe). The same markup applies to a billing switch. Radios in a fieldset also satisfy the guideline.
- Satisfies: comp-switch-label-stable, a11y-status-messages, a11y-coga-costs-up-front
- Verification note: The control behavior was tested on a dark-mode toggle, not on a live billing switch; screen reader announcements were not tested. The advice to show the yearly total with the monthly figure comes from the costs-up-front guidance (COGA).
### Live captions for event streams (`sp-event`) [standard · partly-verified]
If the event page embeds a live stream or webinar, use a player and a captioning service that supply live captions of speech, speaker identification and significant non-speech sounds, and say on the page how to turn them on. If there is no live audio, mark the requirement not applicable. Publish recordings with captions and a transcript afterwards. Write dates as time elements with a time zone; the countdown is a visual extra, never the only place the start time appears, and it is not announced every second.
- How: WCAG 1.2.4 (Level AA) requires captions for live audio in synchronized media. It is a blocker for event sites that stream. Auto-updating content that starts automatically and lasts more than five seconds must be pausable (2.2.2); a second-by-second countdown should be visually fine but hidden from assistive technology (aria-hidden on the ticking digits) with the start date and time in plain text beside it. Show "Live" only while a stream is actually live. Event colours: white on #0F172A is 17.85:1, yellow #FACC15 on it 11.65:1, with night text on a yellow button 11.65:1.
- Satisfies: a11y-captions-live, a11y-captions, a11y-coga-media-chunks-transcripts, a11y-pause-stop-hide, a11y-status-messages, distinct-no-fake-status-badges
- Verification note: The requirements were read from the WCAG Understanding pages. We did not test a live captioning provider or player, so no vendor is recommended; the countdown advice and the date markup are our practical guidance and were not screen-reader tested.
```html
<p>Starts <time datetime="2026-11-12T09:00:00+01:00">12 November 2026, 09:00 CET</time></p>
<p aria-hidden="true" class="countdown">3 days 4 hours</p>
```
