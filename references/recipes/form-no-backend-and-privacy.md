# Recipe: Forms with no backend: a mailto fallback, an honest success message, a privacy line and a rule for sensitive text (`form-no-backend-and-privacy`)
Styles covered: government-public, professional-services, local-community, non-profit
**Keep:** Visible labels; native required, type, inputmode and autocomplete; a working form with JavaScript off; a success message that says what really happened; a privacy line of five short facts; a phone link beside the form.
**Avoid:** Claiming 'Message sent' when only a mail app was opened; placeholder text as a label; a type=number phone field; asking for bank, ID or health details in free text; an example email address shipped as real; moving focus onto the error message; a privacy line that promises something the owner has not confirmed.
A small site with no server can still offer a callback or enquiry form: native fields with native required as the no-JS fallback, a mailto: form action, and JavaScript that validates and then opens a prefilled email. Say plainly that nothing is sent until the visitor presses send in their mail app and that email is not private. Put a short privacy line next to the button, tell people not to write bank details in a free-text box, show errors and success as text in live regions, and offer a phone number as another route.
**While designing:** No backend? Use a native form with required as the no-JS fallback, a mailto: action and JS that validates then opens a prefilled email, plus a phone link; say that nothing is sent until the user presses send and that email is not private; add a five-part privacy line and 'do not write bank details here'; show errors and success in live regions without moving focus onto them; set type=tel, inputmode and autocomplete.
## Steps
### Native single-column fields (`fp-native-fields`) [standard · partly-verified]
Build the form from native fields in one column: a visible label above each, a fieldset with a legend for radio groups, native required, and the right type, inputmode and autocomplete tokens: name (autocomplete="name"), phone (type="tel" inputmode="tel" autocomplete="tel"), email (type="email" autocomplete="email"), postcode (autocomplete="postal-code"). Three required fields at most. Never use a placeholder as the label, and never type=number for a phone number.
- How: WCAG 1.3.5 asks that fields collecting personal data declare their purpose with autocomplete; 3.3.2 asks for labels or instructions. type=tel and inputmode=tel bring up the phone keypad; type=number would add spinners and drop leading zeros. The tokens are HTML autofill tokens; check them in a browser, which is not done here.
- Satisfies: a11y-input-purpose, a11y-labels-instructions, ux-form-no-placeholder-label, ux-form-layout, ux-form-length, comp-checkbox-radio-group-labels, a11y-coga-visible-help-contact
- Verification note: The requirements were read (the labels-instructions Understanding page); the autocomplete and inputmode values are standard HTML and were not tested on devices. The example address is an example domain: replace it with the owner's real address, or mark it with the visible assumption marker until it is confirmed.
```html
<form id="callback" action="mailto:owner@example.org" method="post" enctype="text/plain" novalidate>
  <p id="form-error" role="alert"></p>
  <label for="name">Your name</label>
  <input id="name" name="name" autocomplete="name" required>
  <label for="phone">Phone number</label>
  <input id="phone" name="phone" type="tel" inputmode="tel" autocomplete="tel" required>
  <label for="msg">What is happening (optional)</label>
  <p id="msg-hint">Do not write bank details, passwords or ID numbers here.</p>
  <textarea id="msg" name="message" aria-describedby="msg-hint"></textarea>
  <p id="privacy">...</p>
  <button>Ask us to call you</button>
</form>
```
### Mailto form as no-JS fallback (`fp-mailto-fallback`) [our-take · judgement]
With no backend, use the native form as the no-JS fallback: action="mailto:...", method="post", enctype="text/plain", with native required on the fields. Layer JavaScript on top: on submit, validate, then build a mailto: link with the subject and body encoded (encodeURIComponent) and open it. Beside the form always show the phone link and the plain email address as other routes. Keep the body short: some mail apps cut a very long mailto: link (not measured here).
- How: The form works with JavaScript off because the browser's own required and mailto: handling remain; JavaScript adds nicer validation and a readable prefilled body. mailto: depends on the visitor having a mail app set up (a webmail-only user may get nothing), so the phone link and the written email address are not optional extras. The core content works without JavaScript, as the guide requires.
- Satisfies: perf-core-first, a11y-coga-visible-help-contact
- Verification note: Derived from one pilot (the fictional tenant-rights service) and general practice. The mailto: handoff was not opened in a real mail app in the pilot, and no cross-client behaviour was measured.
```js
form.addEventListener('submit', (e) => {
  e.preventDefault();
  if (!validate(form)) return; // fills #form-error, focuses the first invalid field
  const body = [...new FormData(form)].map(([k, v]) => k + ': ' + v).join('\n');
  location.href = 'mailto:owner@example.org?subject=' + encodeURIComponent('Call-back request') + '&body=' + encodeURIComponent(body);
  status.textContent = 'Your email app should open with your message ready. Nothing is sent until you press send there. If it does not open, call 020 7946 0000.';
});
```
### Honest mailto success message (`fp-honest-success`) [standard · partly-verified]
Never write 'Message sent' or 'Thank you, we have your request' for a mailto: form. Say what really happened in a role=status region that exists empty at load: your email app should open with the message ready; nothing is sent until you press send there; if it does not open, here is the phone number and the email address. Say the same on the page before submit, in one line next to the button.
- How: WCAG 4.1.3 asks that status messages are announced without taking focus; the Understanding page names role=status as a technique, and an empty live region that already exists is announced more reliably than one inserted with its text. The honest wording is our design judgement; it protects people from believing a request was made when it was not.
- Satisfies: a11y-status-messages, a11y-status-role-choice, comp-live-region-exists-before-content, a11y-coga-action-feedback, copy-proof-verifiable
- Verification note: The status-message requirement was read in the WCAG Understanding page. How screen readers announce this exact region was not tested.
### Errors next to fields, with summary (`fp-error-pattern`) [our-take · judgement]
Show each error as text next to its field, say what is wrong and how to fix it, keep what the user typed, and use more than colour (an icon or the word 'Error' and a border). Put a summary in the role=alert region that exists empty at load, fill it on a failed submit, do not call focus() on it, and move focus to the first invalid field. Errors stay until fixed. Native required alone gives browser-styled bubbles that vary by browser, so validate with your own text when JavaScript runs.
- How: This resolves a tension between comp-alert-no-focus-no-autodismiss (do not move focus to a message) and the common error-summary pattern that moves focus to the summary: the summary is announced by the live region, and focus goes to the first field that needs fixing. Resolution is our judgement; it was used in one pilot and not tested with a screen reader.
- Satisfies: a11y-error-identification, copy-error-specific-actionable, ux-form-errors, a11y-color-not-only, comp-alert-no-focus-no-autodismiss, comp-live-region-exists-before-content
- Verification note: Our resolution of a rule tension; one pilot, no screen-reader test.
### Five-question privacy line (`fp-privacy-line`) [our-take · judgement]
Put a short privacy line next to the button, answering five questions in plain words: what we ask for, why, who sees it, how long we keep it, who to contact. Name the law only as an example of what applies (for example 'UK GDPR' for a UK service) and say that the owner must confirm which law, which legal basis and which retention period apply: this is not legal advice. Link to the full privacy notice if one exists. For the mailto: route add that email is not private on its way.
- How: Example copy for the owner to confirm: 'We use your name and phone number only to call you back about your case. Two advisers can see them. We delete them after 30 days. Questions: privacy@example.org. By email, your message is not private on the way.' The 30 days, the two advisers and the address are placeholders to confirm; until the owner confirms them they carry the visible assumption marker, and a lawyer or data-protection adviser should check the final wording before launch.
- Satisfies: copy-proof-verifiable, a11y-labels-instructions, copy-expert-review-before-launch
- Verification note: A drafting pattern, not legal advice and not a compliance claim. No lawyer reviewed it.
### Warn against sensitive free text (`fp-sensitive-free-text`) [our-take · judgement]
Rule of thumb for a free-text box: do not ask for sensitive data you do not need, and tell people what not to write directly under the label ('Do not write bank details, passwords or ID numbers here'), tied to the field with aria-describedby. Ask for health, immigration, financial or identity details only if the service cannot work without them, and then in a channel the owner has chosen for it, not in an email.
- How: With a mailto: form everything typed goes by ordinary email, which is not private and stays in two mailboxes. The cheapest protection is not to collect it. The wording is plain on purpose, so low-literacy and ESL readers can follow it.
- Satisfies: ux-form-length, a11y-labels-instructions, a11y-coga-plain-literal-language
- Verification note: A rule of thumb from the pilot and general privacy practice; not tested.
### No example domains as real addresses (`fp-no-example-addresses`) [our-take · judgement]
Do not ship example domains (example.org, .example) as real addresses. Until the owner supplies the real address and phone number, show them with the visible assumption marker (protocol 3.2), list them in OPEN-QUESTIONS.md, and let realize-launch stop the release.
- How: A form that opens an email to a dummy address looks finished and sends nothing; this is the form case of the guide's rule against invented facts.
- Satisfies: copy-proof-verifiable, copy-no-placeholder-text
- Verification note: Applies the guide's launch gate to forms.
