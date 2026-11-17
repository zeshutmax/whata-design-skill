# Step: Plan the content and page goal (`brief-content`, stage brief)
**Goal:** List what the homepage must say and do, in priority order, and pick one primary action.
**Your role:** Decide what the homepage must say and do, in priority order, with one primary action.
**Inputs:** brief-draft, positioning  
**Output artifact:** content-inventory -> `design/02-brief/content-inventory.md`
## Procedure
1. List every block of content the page needs (headline, what it is, proof, how it works, pricing, FAQ, contact...). For each: priority (must, should, could), source (provided, to be written, to be produced), and the visitor question it answers.
2. Order by importance to the top job. Put the primary action in the first screen and repeat it where it is natural.
3. Flag missing content now. Use real content in designs; if it does not exist, write plausible real copy and mark it 'draft'. Never use lorem ipsum. [Craft: content-first]
4. Facts the owner has not confirmed (prices, hours, sizes, policies, addresses, dates, contact details) get status `unconfirmed` in the inventory and are listed in design/OPEN-QUESTIONS.md. Inside a prototype page they carry the visible marker from the protocol (section 3.2: the `.assumed` dotted-underline convention with a legend), never brackets and never a silent invention. Invented proof (customers, numbers, quotes, press) is not a fact you may mark and ship: leave it out. [Our take]
5. A status or count derived from history (git commits, a changelog, old notes: "25 of 124 pages have sources matched to PubMed") is an assumption until the owner confirms the list: status `unconfirmed`, `.assumed` on the page, listed in OPEN-QUESTIONS.md. Named reviewers and their credentials are facts too: check the person exists before you show the name (protocol 3.2).
6. After you compute a number from content (counts per category, pages per type), open the list it counts and read ten rows before the number goes on the page: in a test a count doubled because two category pages shared one product type, and some items were dropped by a schema error.
7. Map the content to likely section types (hero, features, proof, pricing, FAQ, CTA, footer).
8. Mark every block that gives legal, medical, financial or safety advice `needs expert review` and add the reviewer you need (a solicitor, a clinician, an adviser) to design/OPEN-QUESTIONS.md. Until a qualified person has reviewed it, the copy ships only as a visible draft (the `.assumed`-style marker and legend, protocol 3.2) and realize-launch stays closed. [Our take: `copy-expert-review-before-launch`]
9. Forms: if the page takes personal data (a callback, an enquiry, a booking), list the form, the fields it needs (three required at most), where the data goes (a backend, or email) and who can answer for it; the recipe `form-no-backend-and-privacy` covers the no-backend case and the privacy line.
## Ask the owner (only what you cannot default)
- Which content exists? (a) the current site's text and images, mapped in content-map.md (recommended) (b) new material: send it.
## Output template
```markdown
# Content inventory
| Block | Visitor question it answers | Priority | Source | Section type | Status |
|---|---|---|---|---|---|
## Primary action and where it appears
```
## Gates
Rules to satisfy: `ux-primary-cta-above-fold`, `ux-front-load`, `ux-real-content-examples`, `copy-expert-review-before-launch` (read them with get_guidelines or rules/*.md).
- [ ] Every must-have block has a source.
- [ ] The primary action appears in the first screen.
- [ ] Every block that gives legal, medical, financial or safety advice is marked `needs expert review` with the reviewer named.
## Done when
- All blocks are prioritized and sourced; gaps are listed.
## Pitfalls
- Designing with placeholder text that hides copy problems.
- Inventing a plausible fact and shipping it unmarked: mark it, list it in OPEN-QUESTIONS.md, and let realize-launch refuse while it remains.
