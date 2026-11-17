# Recipe: Urgent help routes on public-service and crisis pages: the emergency line once, a real phone route with hours, and the primary action still on the first screen (`urgent-help-route`)
Styles covered: government-public, non-profit, medical, mental-health
**Keep:** One short urgent band, first in reading order; a visible phone number that is a tel: link; hours as text and a stated out-of-hours route; the emergency-services line written once; the primary action inside the first phone screen.
**Avoid:** Red as the only signal; the emergency line repeated in every section; a sticky or modal urgent bar that covers content or focus; a pop-up, a timer or an auto-opening chat; a phone number only as an image; hours or numbers the owner has not confirmed shown as facts; labels such as 'crisis escalation' that the reader would not use.
For audiences who may be in danger, in debt, ill or facing a deadline, put the urgent route where it is read first, but keep it small. State the emergency-services boundary once, give a phone number as a tel: link with its hours and an out-of-hours route, carry the meaning in words, a border and position rather than red alone, and measure that the band does not push the page's primary action below the first screen at 390x844. Use plain labels in the reader's words.
**While designing:** Public-service or crisis page: put one compact urgent band first (the emergency-services line once, the phone number as a tel: link with hours and an out-of-hours route, meaning carried by words and a border, not red alone), use plain labels, and screenshot 390x844 to confirm the primary action is still on the first screen.
## Verified palette: Urgent band, computed (WCAG 2 relative luminance); the colours are an example, the cue is the text, the border and the position
- page-background: #FAFAF7
- band-background: #FFE08A
- band-text: #1B1B1B
- band-link: #6B4A00
- band-border: #7A4F00
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| band text on band background | #1B1B1B | #FFE08A | 13.35:1 | 4.5:1 |
| band link on band background | #6B4A00 | #FFE08A | 6.25:1 | 4.5:1 |
| band border on page background (UI) | #7A4F00 | #FAFAF7 | 6.82:1 | 3:1 |
## Steps
### Urgent route first in order (`uh-first-in-order`) [our-take · judgement]
Decide the one urgent route for this audience and put it first in reading order, before the page's main content, as a short band: one heading, one or two sentences, one phone link. Put the page's primary action directly after it. The urgent route is not the page's primary action unless the service itself is a helpline.
- How: Code order equals reading order, so a screen-reader or keyboard user meets the route first and a sighted reader meets it first too. Keep it to a band, not a section, so it does not take over the page. Which route comes first (the emergency line, the helpline, the service's own number) is the owner's call and depends on the service.
- Satisfies: a11y-meaningful-sequence, ux-primary-cta-above-fold, ux-purpose-clear
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern.
### State emergency boundary once (`uh-emergency-boundary-once`) [our-take · judgement]
State the emergency-services boundary once, in plain words, at the top: say who to call if someone is in danger now (for example 'If someone is in danger now, call 999, the emergency services') and that this service is not one. Do not repeat it in every section or in the footer. 999 is the UK number and an example: the owner must confirm the number for the service's country (112, 911 ...).
- How: Said once, the line is read and acted on; repeated, it dilutes the page, frightens people who are not in danger and is read aloud again at every repeat by a screen reader. Whether the boundary line is also legally or professionally required for this service is for the owner to confirm. This is a design judgement, not a tested result.
- Satisfies: a11y-coga-plain-literal-language, copy-tone-fits-context, copy-proof-verifiable
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern.
### Phone number as a tel link (`uh-phone-tel-link`) [craft-consensus · partly-verified]
Show the phone number as real text inside a tel: link whose visible text includes the number and a verb ('Call us: 020 7946 0000'), at least 44 by 44 CSS px, with the country code in the href. Show the same number as text on desktop, where there may be no calling app.
- How: The visible text is the accessible name, so voice-control users can say what they see (label in name). The tel: scheme is standard HTML; a desktop browser with no calling app may do nothing, which is why the number stays visible as text. Not tested on real phones here. The number in the example is from the UK range set aside for fiction; the owner's number, or the visible assumption marker (protocol 3.2) until it is confirmed, goes in its place.
- Satisfies: a11y-link-purpose, a11y-label-in-name, a11y-target-size, a11y-coga-visible-help-contact
- Verification note: The accessible-name and target-size requirements are WCAG 2.5.3 and 2.5.8 (quick reference); the markup is ordinary HTML. No phone, desktop-without-app or voice-control test was run.
```html
<section class="urgent" aria-labelledby="urgent-title">
  <h2 id="urgent-title">If someone is in danger now</h2>
  <p>Call 999 for the emergency services. We are not an emergency service.</p>
</section>
<p class="phone"><a href="tel:+442079460000">Call us: 020 7946 0000</a></p>
<p>Monday to Friday, 9am to 5pm. Outside those hours, use <a href="#callback">the call-back form</a> and we reply the next working day.</p>
```
### Hours and out-of-hours route (`uh-hours-and-out-of-hours`) [our-take · judgement]
Write the opening hours as text next to the number and say what to do outside them: another number, a form with the reply time, or where to leave a message. Promise only a reply time the service keeps. Hours, reply times and numbers the owner has not confirmed carry the visible assumption marker (protocol 3.2) and are listed in OPEN-QUESTIONS.md.
- How: A phone line that is closed with no other route is a dead end for a person in a hurry. A live 'open now' badge from JavaScript is optional and must not replace the text, because the core content has to work without JavaScript.
- Satisfies: copy-proof-verifiable, a11y-coga-visible-help-contact, copy-specific-over-abstract
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern.
### Urgency beyond red alone (`uh-not-red-alone`) [standard · partly-verified]
Carry the urgency in words, position and a border, not in red alone. The band starts with a plain sentence, has a visible border, has text at 4.5:1 and its boundary at 3:1 (check with check_contrast, role text and ui), and keeps its meaning in forced-colors mode and for a reader who cannot tell the colour. Keep red for errors so the two do not mean the same thing.
- How: WCAG 1.4.1 says colour is never the only way to show information. The palette above is computed with the WCAG 2 formula; amber is an example, not a requirement. The band's text works on its own, so removing the colour loses nothing.
- Satisfies: a11y-color-not-only, a11y-contrast-text, a11y-non-text-contrast
- Verification note: The requirement was read in the WCAG Understanding page and the ratios were computed. How the band reads under forced colors or to people with colour-vision differences was not tested.
### Band and action above the fold (`uh-stack-above-fold`) [our-take · judgement]
Stack the band with the primary action and check it at 390x844: the primary action's bottom edge must be inside the first viewport. Keep the band compact (a heading and one line, or one line with the phone link), do not make it sticky or a full-height overlay, and trim the page's own heading before the band if they compete. If the action still falls below, shorten the band before you shrink the action.
- How: A sticky or fixed bar costs the first screen on every scroll position and can cover focused elements (WCAG 2.4.11). Measure, do not guess: the audit's primary-action check and a screenshot at 390x844 both work. In the pilot an amber band took about a quarter of the phone's first screen and put the main button at 858 px, below the 844 px fold; the audit found it and the layout was changed. Any height budget (for example 'a fifth of the viewport') is our rule of thumb, not a standard.
- Satisfies: ux-primary-cta-above-fold, a11y-focus-not-obscured, ux-false-floor
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern. The snippet measures one element's box; it does not replace looking at the screenshot.
```js
// run in the page at a 390x844 viewport
const b = document.querySelector('[data-primary-action]').getBoundingClientRect();
console.log(b.bottom <= innerHeight ? 'primary action is in the first screen' : 'primary action is BELOW the fold by ' + Math.round(b.bottom - innerHeight) + ' px');
```
### Labels in the reader's words (`uh-plain-labels`) [craft-consensus · partly-verified]
Write every label in the reader's words and in plain language: 'Call us', 'Call 999 if someone is in danger now', 'I have been given an eviction notice', not 'Crisis escalation', 'Urgent triage' or the service's internal names. Put the verb first, spell out acronyms, state what a call costs if the reader may have to pay, and aim at the lower reading target for stressed, ESL or low-literacy readers (see copy-reading-grade).
- How: People under stress read less and take in less (the COGA guidance lists stress and low literacy among the groups it covers); plain, literal wording is the cheapest fix. No reading test was run on the example wording.
- Satisfies: copy-button-verb-label, copy-plain-words, a11y-coga-plain-literal-language, copy-jargon-acronyms
- Verification note: The wording guidance follows the plain-language and COGA sources behind the cited rules; the examples were not read-tested with real readers.
### No pop-ups for the urgent route (`uh-no-interruptions`) [our-take · judgement]
Keep the urgent route in the page, not in a pop-up, a timed banner, a modal or an auto-opening chat. It exists in the HTML at load, does not move, and does not take focus.
- How: A person in distress should not have to dismiss something to reach the content, and a banner that disappears on a timer can vanish before it is read. This is an application of the cited rules, not a measured result.
- Satisfies: a11y-coga-limit-interruptions, a11y-coga-no-surprise-changes, comp-alert-no-focus-no-autodismiss
- Verification note: Applies the cited rules to this case; not measured.
### Observed example, not verified (`uh-observed-example`) [our-take · judgement]
Observed example only, not verified: the pilot for a fictional UK tenant-rights service put a flat amber band above a board of five first-person situations ('What is happening to you?'), with the 999 line once and the service's phone number as a link, and a call-back form below. Use it as one shape to compare against, not as the answer.
- How: The pilot's own account: the band was the first thing on the page, the five rows were the primary action, and the phone-first screenshot needed a change after the audit found the button below the fold. No person looked at the page, nobody called the number, and the advice text was a draft that lawyers had not checked. Whether this shape helps people in distress is untested.
- Satisfies: ux-primary-cta-above-fold, a11y-color-not-only
- Verification note: One pilot, one model, no users.
