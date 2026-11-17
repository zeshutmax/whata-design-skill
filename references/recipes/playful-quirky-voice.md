# Recipe: Playful, quirky and friendly voices that stay clear (`playful-quirky-voice`)
Styles covered: playful, quirky, friendly
**Keep:** A distinct voice, a mascot or recurring character, bright warm colours, bouncy motion, conversational marketing copy.
**Avoid:** Idioms, puns and metaphors as headlines, nav labels or buttons; humour or blame in errors; "please", "simply", "just", "easy" and exclamation points in instructions; white text on bright fills; endless looping motion.
Keep the personality, the jokes, the mascot and the warm colours. Put the wit in kickers and supporting lines, keep headings, buttons, errors and money screens literal, and let motion respect reduced-motion settings.
**While designing:** Write the plain headline first and add the quirk as a kicker or supporting line, name every section by what it says, write errors as "Enter..." or "X must be...", and keep payments, security and deletion neutral.
## Verified palette: Friendly and playful, computed
- background: #FFFFFF
- text: #1B1B1F
- text-muted: #4B4B55
- fill-sun: #FFD23F
- button-coral: #FF6B3D
- link: #1D4ED8
- error: #B42318
- error-tint: #FFF1EC
- success: #0B5D3A
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on paper | #1B1B1F | #FFFFFF | 17.17:1 | 4.5:1 |
| muted text on paper | #4B4B55 | #FFFFFF | 8.62:1 | 4.5:1 |
| ink on sun-yellow fill | #1B1B1F | #FFD23F | 11.89:1 | 4.5:1 |
| ink on coral button | #1B1B1F | #FF6B3D | 6.07:1 | 4.5:1 |
| link on paper | #1D4ED8 | #FFFFFF | 6.7:1 | 4.5:1 |
| error text on paper | #B42318 | #FFFFFF | 6.57:1 | 4.5:1 |
| error text on error tint | #B42318 | #FFF1EC | 5.96:1 | 4.5:1 |
| success text on paper | #0B5D3A | #FFFFFF | 7.95:1 | 4.5:1 |
| error field border on paper (UI) | #B42318 | #FFFFFF | 6.57:1 | 3:1 |
## Steps
### Warm fills with ink text (`pq-palette`) [standard · verified]
Use bright warm colours as fills and put ink on them. Coral #FF6B3D with white text is 2.83:1 and fails; ink #1B1B1F on the same coral is 6.07:1. Sun yellow #FFD23F with ink is 11.89:1. Keep the error red #B42318 (6.57:1 on white, 5.96:1 on its tint) and success green #0B5D3A (7.95:1) for those states only.
- How: Link #1D4ED8 is 6.7:1 on white; muted text #4B4B55 is 8.62:1. Field borders carry meaning, so give them a 3:1 colour (the error border is 6.57:1). Rendered in Chrome: computed colours match each claimed pair.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Plain offer as the headline (`pq-plain-headline`) [craft-consensus · verified]
Write the plain statement of the offer as the headline, nav label or button, and put the pun, joke or character in a kicker or the supporting line. "Plan a trip with friends" is the h1; "Meet Pip" and "Pip keeps the spreadsheets away" carry the personality.
- How: NN/g: headlines work out of context and avoid cute or idiomatic language; Google style guide: avoid slang and figurative language; W3C COGA: avoid metaphors and idioms in navigation and calls to action. Test: read each headline, nav label and button aloud to someone who does not know the product; if a literal reading misleads, rewrite it. Buttons start with a verb in sentence case ("Create a free account").
- Satisfies: copy-no-idioms-puns, a11y-coga-plain-literal-language
### Name sections by what they say (`pq-headings`) [craft-consensus · verified]
Name every section by what it says ("Split costs without the maths"), so the heading list read alone summarises the page. Never use "Features", "Overview", "Why choose us" or "Our approach", and do not prefix feature cards with emoji.
- How: GOV.UK content guidance and NN/g: headings that describe the content beneath them. The Chrome demo extracts its heading outline and matches it against the rule blocklist (introduction, overview, features, benefits, our approach, why us, about, welcome): none match, and the outline reads as a summary. Order sections by the questions this buyer asks, not by the stock hero, logos, three cards, pricing sequence.
- Satisfies: copy-heading-informative, copy-section-content-drives-structure
### Specific, neutral error messages (`pq-errors`) [craft-consensus · verified]
Write errors as specific, neutral instructions: "Enter your email address" for an empty field, "Postcode must be in the format AB1 2CD" for a wrong value. Show them with an icon, text and a changed border, linked to the field with aria-describedby, in an error colour that passes (6.57:1 on white).
- How: GOV.UK error-message guidance: say what happened and how to fix it; avoid "valid/invalid", "please", "sorry", "oops", "forbidden", "you forgot" and "This field is required". NN/g: nonblaming positive tone, no humour in errors except a rare total failure. WCAG 1.4.1 and failure F81: errors must not be identified by colour only. Chrome demo: both invalid inputs have a label, a described-by message of real text, an icon and a changed border; the error strings contain none of the banned words or exclamation marks.
- Satisfies: copy-error-specific-actionable, copy-error-no-blame-words, a11y-error-identification, a11y-color-not-only
```html
<label for="em">Email address</label>
<input id="em" type="email" autocomplete="email" aria-invalid="true" aria-describedby="em-err">
<p id="em-err"><span aria-hidden="true">&#9888;</span> Enter your email address</p>
```
### Plain imperative instructions (`pq-instructions`) [craft-consensus · verified]
Give instructions as plain imperatives: "Enter the email address you use for bookings." Drop "please", "please note", "simply", "just", "easy", "quickly", "it's that simple" and exclamation points from interface text. Marketing headlines may keep their energy.
- How: GOV.UK tone guidance and Google developer style guide list these softeners as words to avoid. The check is a grep over UI strings, hints, instructions and help text, excluding marketing headlines and testimonials; the Chrome demo ran that grep over its UI zone and found none.
- Satisfies: copy-no-please-filler
### Dial personality down as stakes rise (`pq-tone-dial`) [craft-consensus · verified]
Turn personality down as the stakes go up: full voice in marketing sections, light touches in onboarding, neutral wording on forms and errors, and literal text on payment, security, cancellation, deletion and legal surfaces, with no joke, slang, hype word or exclamation point.
- How: Mailchimp: voice stays constant, tone shifts with the reader's state; NN/g: humour only for rare total failures. Write the surface list once ("marketing, onboarding, forms, errors, checkout, security, deletion, legal") with a tone for each, and sample the copy of the risky surfaces. The demo's payment copy ("Your card is charged when the trip is booked...") is deliberately literal.
- Satisfies: copy-tone-fits-context
### Write a voice sheet first (`pq-voice-sheet`) [craft-consensus · partly-verified]
Write a voice sheet before the copy: three or four trait words, each with a do and a don't example, plus the fixed choices (you or we, contractions, US or UK spelling). Allow one quirky element per surface so the oddness stays a signature.
- How: Mailchimp and Microsoft publish voice guidance as traits with examples. Sample six surfaces (hero, navigation, buttons, errors, footer, 404) against the sheet and fail mixed spelling or person. The "one quirk per surface" budget is our own heuristic.
- Satisfies: copy-voice-consistent
- Verification note: Voice-sheet practice is in the sources read; the one-quirk-per-surface budget is our heuristic.
```text
Voice: warm, specific, a little odd.
Warm      do "Pip sorted the costs"          don't "Users must remit payment"
Specific  do "3 of 5 friends have paid"      don't "Great progress!"
Odd       do one mascot line per page         don't puns in nav labels
Fixed: address the reader as "you", use contractions, UK spelling.
```
### Limit three quirky copy patterns (`pq-rhetoric`) [our-take · judgement]
Watch for the three patterns quirky copy slides into: "not X, it's Y", three parallel slogans ("Save time. Work smarter. Scale faster."), and self-answered questions ("The result?"). Use each at most once per page and say the claim directly otherwise.
- How: The rule is advisory and our own take, drawn from lists of AI-writing tells. A regex pass over the page text counts the hits: fail above one of each kind. A list of two or four items, when the items really are distinct, avoids the tricolon.
- Satisfies: copy-no-stock-rhetoric
- Verification note: Advisory rule labelled our-take; the sources are lists of AI-writing tells, not studies of reader outcomes.
### Finite, optional bouncy motion (`pq-motion`) [standard · verified]
Keep bouncy motion finite and optional: a mascot hop that runs three times (3.6 s) and then stops, a prefers-reduced-motion block that removes it, and nothing flashing. Any loop longer than five seconds next to other content needs a visible pause control.
- How: MDN: replace large-scale motion with gentler effects under prefers-reduced-motion: reduce. WCAG 2.2.2: moving or blinking content that starts automatically, lasts more than five seconds and sits beside other content needs pause, stop or hide. Measured in Chrome: the hop is one animation of 1.2 s x 3 iterations; with reduced motion emulated it computes to animation-name none and no running animation.
- Satisfies: a11y-reduced-motion, a11y-pause-stop-hide, a11y-flashes
```css
.mascot { animation: hop 1.2s cubic-bezier(0, 0, 0.2, 1) 3; }
@media (prefers-reduced-motion: reduce) { .mascot { animation: none; } }
```
### Wrap the h1, SVG icons (`pq-reflow-200-icons`) [standard · verified]
Give the h1 overflow-wrap: anywhere (a 3rem h1 overflowed by 35 px at 320 px with 200% text) and draw warning and error icons as inline SVG with currentColor and aria-hidden, never as emoji (distinct-real-imagery-and-icons).
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; 35 px of overflow and two emoji-as-icon minors were both gone after the change.
- Satisfies: a11y-reflow, distinct-real-imagery-and-icons
