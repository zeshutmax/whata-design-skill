# Recipe: Luxury and opulent styles: gold, thin type and ornament that stay readable (`luxury-and-opulent`)
Styles covered: luxury, opulent
**Keep:** Near-black or burgundy grounds, ivory text, gold accents, serif display lines, ornament and dense detail, long quiet spacing, product-focused imagery.
**Avoid:** Gold text on white; light or thin weights at body size; letterspaced lowercase paragraphs; ornament behind text; stock marketing verbs (elevate, curated, timeless tapestry); text set as an image; ten equal choices on the first screen.
Keep the deep colours, the gold, the generous space and the ornament. Use a gold that passes on its ground, keep light type weights for large display lines, write in plain words, and make ornament decorative so it never carries the message.
**While designing:** Gold that passes on its ground, light weights only at display size, plain factual copy in sentence case, ornament as decoration, one dominant choice per screen.
## Verified palette: Ivory and gold on night, with a burgundy variant, computed
- background: #0E0D0B
- text: #F3EEE4
- text-muted: #B5AE9F
- accent: #C9A24B
- accent-line: #8F7433
- light-background: #FAF7F0
- accent-on-light: #7A5A12
- ink-on-light: #1B1A17
- burgundy-background: #4A0F1F
- gold-on-burgundy: #D9B866
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ivory text on night | #F3EEE4 | #0E0D0B | 16.79:1 | 4.5:1 |
| muted text on night | #B5AE9F | #0E0D0B | 8.8:1 | 4.5:1 |
| gold text on night | #C9A24B | #0E0D0B | 8.09:1 | 4.5:1 |
| night text on gold button | #0E0D0B | #C9A24B | 8.09:1 | 4.5:1 |
| gold hairline on night (UI, 3:1) | #8F7433 | #0E0D0B | 4.36:1 | 3:1 |
| deep gold text on ivory | #7A5A12 | #FAF7F0 | 5.95:1 | 4.5:1 |
| ink on ivory | #1B1A17 | #FAF7F0 | 16.26:1 | 4.5:1 |
| ivory text on burgundy | #F3EEE4 | #4A0F1F | 13.16:1 | 4.5:1 |
| gold text on burgundy | #D9B866 | #4A0F1F | 7.97:1 | 4.5:1 |
## Steps
### Choose gold by its ground (`lo-gold`) [craft-consensus · verified]
Choose gold by the ground it sits on. On near-black use #C9A24B for text and buttons (with night text on the button). On ivory use a deep gold such as #7A5A12 for text. Use #8F7433 or lighter for thin decorative lines only where 3:1 is enough.
- How: Computed with the WCAG 2 formula: gold #C9A24B on #0E0D0B 8.09:1; ivory text 16.79:1; muted #B5AE9F 8.8:1; a #8F7433 hairline 4.36:1. The same gold #C9A24B on white is only 2.39:1, so it fails for text and for icons that carry meaning. Deep gold #7A5A12 on ivory #FAF7F0 5.95:1. Burgundy #4A0F1F: ivory 13.16:1, gold #D9B866 7.97:1. A metallic gradient on text must be tested at its darkest and lightest stops.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Light weights for large display only (`lo-type-weights`) [craft-consensus · partly-verified]
Reserve weight 300 or lighter for display lines of 24px and up; body and anything under 24px stays at 400 or heavier. Keep lowercase body text at letter-spacing normal. Track only uppercase labels (0.05 to 0.12em) and keep those to three words or fewer on one line.
- How: Thin high-contrast serifs (Cormorant Garamond, weights 300 to 700; Bodoni Moda, 400 to 900 with an optical-size axis; both in Google Fonts) look refined at display size and break up at body size, so raise the size or the weight instead of the tracking. Butterick: capitals take 5 to 12% letterspacing, lowercase does not ordinarily need it; capitals are for less than one line.
- Satisfies: craft-weight-thin-limited, craft-body-tracking-normal, craft-caps-letterspacing, craft-caps-short-only, craft-body-size-min
- Verification note: Capitals and tracking advice was read from Butterick. The 300-weight and 24px threshold comes from the guideline (Apple HIG source partly read), and the font axes from metadata. The label is set at 1rem: the body-size rule counts a label paragraph as running text, so a smaller label size would fail. No face was rendered.
```css
.display { font: 300 2.5rem/1.05 "Cormorant Garamond", Georgia, serif; overflow-wrap: anywhere; }
@media (min-width: 48em) { .display { font-size: 3.5rem; } }
@media (min-width: 64em) { .display { font-size: 5rem; } }
body { font: 400 1.0625rem/1.6 "Newsreader", Georgia, serif; letter-spacing: normal; }
.label { text-transform: uppercase; letter-spacing: 0.1em; font-weight: 500; font-size: 1rem; }
```
### Luxury copy as plain facts (`lo-plain-copy`) [craft-consensus · partly-verified]
Write luxury copy as facts in ordinary words: where it is made, by whom, how long it takes, what is guaranteed. Remove stock marketing verbs and metaphors (unlock, elevate, curated, journey, tapestry, realm), use sentence case in headings, buttons and navigation, and name navigation items literally ("Watches", "Book a visit", not "Discover the journey").
- How: The buzzword list and plain-language rules come from the guidelines and GOV.UK, NN/g and COGA. A rough local score (our own approximate syllable script, illustrative only) gave grade 16 for "Elevate your journey with an unparalleled tapestry of timeless craftsmanship, where every moment is curated to transcend the ordinary." and grade 3 for "Each watch is made by hand in our Geneva workshop. One maker builds one watch, which takes about nine weeks. We service every watch for life." The plain version carries three checkable facts; the buzzword version carries none. Prestige can still come from restraint: short lines and specific numbers.
- Satisfies: copy-no-buzzwords, a11y-coga-plain-literal-language, copy-sentence-case, craft-heading-sentence-case, a11y-reading-level-support
- Verification note: Rules and sources were read; the readability scores came from an approximate script and the example brand is invented. Whether plain facts make a luxury brand feel more or less premium is our judgement.
### Ornament as decoration only (`lo-ornament`) [craft-consensus · verified]
Treat ornament as decoration: borders, flourishes, monograms and patterns are CSS backgrounds or SVG with alt="" (or aria-hidden="true"), never the only place a name, price or instruction appears. Put text on a solid panel, not on a patterned or photographic ground. Keep headings and prices as real text, and use an image of text only for a logo.
- How: NN/g: an image is decorative if users can complete all tasks and understand all information without it, and gets an empty alt. WCAG 1.4.5 allows images of text for logotypes or when the presentation is essential. For text over ornament or photography, the scrim math in the hero-and-photography recipe applies: a 60% black overlay keeps white text at 5.74:1 even over a pure white backdrop (measured in Chrome).
- Satisfies: a11y-alt-text, a11y-images-of-text, a11y-coga-text-not-over-busy-background, craft-contrast-text-on-media
### One dominant thing per screen (`lo-restraint`) [our-take · judgement]
Give each screen one dominant thing and at most five main choices. An opulent page may be dense in detail, but make the one feature or call to action visibly larger than the others and move secondary links under a titled "more" link or into the footer. Keep prices, fees and conditions visible where the choice is made.
- How: COGA asks for about five or fewer main choices per screen and one visually dominant feature; the same document asks for costs to be stated at the start of a booking or purchase. Luxury practice often hides the price; that is a brand choice that conflicts with the guidance, so record the exception if you keep it.
- Satisfies: a11y-coga-limit-choices-per-screen, a11y-coga-key-tasks-prominent, a11y-coga-costs-up-front
- Verification note: The COGA guidance was read, but applying it to luxury is our judgement and trades some mystique for clarity.
