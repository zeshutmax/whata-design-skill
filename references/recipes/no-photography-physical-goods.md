# Recipe: No photography exists (physical goods or services): the offer as the live object, type as image, or an honest gap (`no-photography-physical-goods`)
Styles covered: no-imagery, ecommerce-store, consumer-goods, specimen, professional-services, business-services
**Keep:** A first object made of real controls and real numbers; type set large as real text; tables and run sheets with specific rows; an honest, listed gap.
**Avoid:** Shape-assembled drawings of the product; stock or placeholder images; emoji icons; a decorative texture that starts to depict the product; unconfirmed prices or hours shown as facts; claiming the live object replaces photographs for a pieces-only shop.
When no photographs exist (a physical product with no photos yet, or a service with none you can use), do not draw the subject from shapes and do not use stock. Make the offer itself the live object when it has state (price, seats, slots, dates, a calculator, a booking control or self-check), let a large measurement, price or fact be the image, present the catalogue or fee table as a menu or run sheet where there are rows to list, or leave the imagery out and mark the gap, and plan the real photographs. For a service, np-offer-live-object applies when there is state to show, np-type-as-image and np-mark-the-gap always apply, np-menu-and-run-sheet only when the service has rows to list, and np-pieces-only-limit is for goods.
**While designing:** No photos (goods or a service)? Build the offer as the live object with native controls when it has state (or set the key fact, measurement or price large as real text), show a fee table or catalogue as a table or run sheet when there are rows, mark the photograph gap in OPEN-QUESTIONS.md, and never draw the subject from shapes in code. Services: skip the pieces-only limit; the menu step only if there are rows to list.
## Steps
### Make the offer the first object (`np-offer-live-object`) [our-take · judgement]
When the offer has state to show (seats left, time slots, dates, sizes, bundles, a price that changes with a choice), make the offer itself the first object on the page: a booking or price control built from real HTML controls with real numbers and real states, placed where a product photo would normally sit.
- How: In the pilot, a ceramics studio selling six seats at a stated price per workshop used a ring of six native checkboxes that totals the price and writes the booking email, instead of a photograph. It works because the offer is seat-limited; it does not work for a pieces-only shop, which has no state to show (see np-pieces-only-limit). The numbers on the page must be the owner's: mark any you do not have with the assumption marker from the protocol (3.2). For a service: it applies when the service has state to show (free slots, a waiting time, opening hours, a self-check or calculator); a self-check was the live object in a tenant-rights advice pilot. If the service has no state, use np-type-as-image.
- Satisfies: distinct-real-imagery-and-icons, distinct-hero-not-template
- Verification note: Derived from one pilot (a model designing a ceramics-studio homepage on the lean track); no user was shown the page and no conversion was measured. Only structural checks were run (no img, svg or canvas, no emoji).
### Live object from native controls (`np-live-object-accessible`) [standard · partly-verified]
Build the live object from native controls (checkbox, radio, select, button, number input) with visible labels, a fieldset and legend for a group, keyboard operation for free, and a total that updates in an output element so the change is announced without moving focus. State is never carried by colour alone: selected seats also differ by fill, ring or text.
- How: WCAG 4.1.3 asks that status messages can be announced without taking focus; the Understanding page lists role=status and live regions as the techniques. Using native controls follows the ARIA practice 'no ARIA is better than bad ARIA'. Not measured with a screen reader here: test it with VoiceOver or NVDA before launch.
- Satisfies: a11y-native-first, a11y-name-role-value, a11y-status-messages
- Verification note: The requirement (status messages announced without focus) was read in the WCAG Understanding page. The markup pattern is general engineering knowledge and was not tested with a screen reader.
```html
<fieldset>
  <legend>Pick your seats</legend>
  <label><input type="checkbox" name="seat" value="1"> Seat 1</label>
  <label><input type="checkbox" name="seat" value="2"> Seat 2</label>
</fieldset>
<p>Total: <output id="total">0</output> <!-- price per seat: the owner's number, or marked unconfirmed --></p>
```
### Let type carry the image (`np-type-as-image`) [craft-consensus · partly-verified]
Let type carry the image: set a measurement, a date, a price, a capacity or a name large as the visual, in the display face, as real text. Never export the type as an image.
- How: WCAG 1.4.5 (images of text) is the reason it stays real text: it resizes, reflows and can be read by assistive technology. Which fact to set large is a design judgement: choose the one that answers the visitor's first question about the product (how big, how many, how much, when).
- Satisfies: distinct-real-imagery-and-icons, a11y-images-of-text, distinct-display-font-chosen
- Verification note: The images-of-text requirement was read in the WCAG Understanding page. That type can stand in for a product image is our design judgement, with no study behind it.
### Catalogue as a table or list (`np-menu-and-run-sheet`) [our-take · judgement]
Present the catalogue, price list or run sheet as a menu: a real table or definition list with one row per item (name, size or detail, price, availability, how to get it) in plain text. Vary the structure of the sections below the hero: a run sheet in one, a price list in another, a measurements table in a third.
- How: Specific rows (a size, a price, a firing or delivery time) inform the way a photograph would, and a list is not an image-card grid. Each figure must be a fact the owner gave or be marked unconfirmed. Judgement: whether visitors who buy by looking accept a text catalogue is not tested here. For a service: use it only when there are rows to list (a fee table, opening hours, the steps of a process); in the advice pilot it did not fit.
- Satisfies: copy-specific-over-abstract, ux-informative-imagery, distinct-no-identical-card-grid
- Verification note: Derived from one pilot (a model designing a ceramics-studio homepage on the lean track); no user was shown the page and no conversion was measured. Only structural checks were run (no img, svg or canvas, no emoji).
### Mark the missing photography (`np-mark-the-gap`) [our-take · judgement]
If none of the above fits, leave the imagery out and mark the gap: in the design notes and in design/OPEN-QUESTIONS.md write that photographs are missing, which shots are needed, and that the page is not finished without them. Do not use a placeholder host, a stock demo image, an emoji, or a picture of the product assembled from shapes in code.
- How: A faint decorative gradient or texture that does not depict the product is ornament and the rule does not flag it. One that starts to depict the product (grooves that read as a pottery wheel, a glaze, a bowl) is an illustration: remove it or commission it as a file. The rule's detector flags hero-sized inline SVG scenes assembled from primitives; a drawn bowl or cross-section is that.
- Satisfies: distinct-real-imagery-and-icons, copy-no-placeholder-text
- Verification note: Derived from the wording of `distinct-real-imagery-and-icons` and one pilot. The line between ornament and illustration is a judgement call and is not measured.
### Plan the photo shot list (`np-commission-later`) [our-take · judgement]
Plan the real photographs: a shot list (hero object, scale, detail, in use), who takes them, licence and alt text, reserved width and height for each image slot, and the likely LCP image set with fetchpriority high and not lazy-loaded when it arrives. Put the plan in assets and in OPEN-QUESTIONS.md.
- How: Reserving dimensions now prevents layout shift later; alt text describes what the photograph conveys in context. The shot list is our suggestion, not a tested checklist.
- Satisfies: craft-image-dimensions-reserved, a11y-alt-text
- Verification note: A planning step, not a measured technique.
### Limits when selling single pieces (`np-pieces-only-limit`) [our-take · judgement]
If the business sells individual pieces and the offer has no state to show (no seats, slots or sizes to choose), the live object cannot replace a photograph. Say so in the notes, use the menu form and type as image, and record the missing photographs as the main launch risk.
- How: The pilot's own conclusion: the live object worked only because the studio sold a seat-limited class. People often buy a piece by looking at it, so a page without images may read as unfinished; this is a risk to state to the owner, not a measured effect. This step is for goods. A service has its own version of the problem only when nothing about it can be shown as state or as a fact; then use np-type-as-image and np-mark-the-gap, and photographs of people need their consent.
- Satisfies: distinct-real-imagery-and-icons, copy-proof-verifiable
- Verification note: Derived from one pilot (a model designing a ceramics-studio homepage on the lean track); no user was shown the page and no conversion was measured. Only structural checks were run (no img, svg or canvas, no emoji).
