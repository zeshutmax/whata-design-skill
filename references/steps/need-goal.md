# Step: Define the need and the goal (`need-goal`, stage need)
**Goal:** State the business goal, the visitor goal and how success will be recognized.
**Your role:** Pin down what the homepage is for before any design thinking. You are framing a problem, not proposing a solution.
**Inputs:** none  
**Output artifact:** need-statement -> `design/01-need/need-statement.md`
## Procedure
1. Redesigning an existing site? Before you restate anything or ask the owner a question, read what exists (the code, the content, the analytics events) and write down what the site actually does today and which action it really serves. A brief can describe a site that does not exist: a first test found a request for a 'booking site' on a site with no booking at all, whose real action was 'follow'. Where the request and the code disagree, say so and let the code set the primary action unless the owner decides otherwise.
2. Redesigning an existing site? Ask the scope once, first, as the first ask_user question (three multiple-choice lines with the recommended answer first) and write the answer as a `## Scope` block at the top of need-statement.md; every later step reads it. Structure: rebuild from scratch, or keep the current sections. Content: rework key parts (the hero and 2 or 3 key sections; everything else is kept and moved into the new sections), keep verbatim, full rework, or none supplied (you write draft copy marked unconfirmed). SEO: keep URL, title, meta description, canonical, structured data, heading text and internal links, or free to change. For a "make it stylish" job on an existing site the recommended answer is rebuild, rework key parts, keep SEO: the owner's own words were "from scratch ... respect the content, but not the structure ... repurpose the content across the new sections ... keep it for SEO". Owner away: use the recommended answers, mark the block `ASSUMED, not owner-approved`, and list it in OPEN-QUESTIONS.md.
3. Existing content with a scope that keeps any of it: write design/01-need/content-map.md before designing: every text block of the current page (heading, paragraph, list, button, FAQ item) with an id, marked `SEO` when it is the title, meta description, h1 or h2 text, structured data or an internal link; the new section it moves into; and `keep`, `rework` or `drop (owner)`. Nothing is dropped without the owner's word. realize-qa checks the build against it with the audit's `coverage` command.
4. Outside the scope's rework parts the content is the owner's. Content problems you find (unsourced claims, odd copy, missing sections) are findings for the owner, listed in OPEN-QUESTIONS.md and the QA report; do not fix, remove or rewrite them yourself, and do not add claims of your own. In a test the first build rewrote copy outside its scope and dropped sections, and had to be reverted. Also ask whether the done bar may touch shared chrome (header, footer, shared components): it moves the work from one file to many.
5. Open the pages the primary action sends people to (the three main destinations) and check their claims and sources too: a homepage inherits their honesty. In a real run the homepage's own claims were fixable, but 99 of the 124 pages its main action led to might still cite fabricated papers, and the repo's own commit messages said so. Check also the people the content names as authors or reviewers: a name, title or credential is shown only if the person exists and can be reached (protocol 3.2). Read the git log for words such as `fabricated`, `placeholder`, `fake`, `TODO` and `unverified`.
6. Restate the user's request in one sentence without solution words (no 'with a video', 'in dark mode').
7. Write the business goal, the visitor goal and ONE primary action the page asks for (a single verb phrase: buy, book a demo, join the waitlist...). [Craft]
8. Define how success will be recognized: at least one measurable signal (a rate, a count, a task success) and one observable signal (a five-second test result, a stakeholder reaction).
9. No baseline? Do not invent one. Set a relative target (for example `+X% against the first four weeks after launch`, or `more enquiries per 100 visits than the old page`) and name the measure, or write the absolute number and mark it `ASSUMED, no baseline`. Record the missing baseline as an open question: a target with no baseline is a hypothesis, not a result. [Our take]
10. The owner names two actions ('book or buy')? Pick the one with the higher value or the higher frequency as the primary action, name the other as a secondary action, and record the call and the reason as an open question for the owner. Do not write both as primary. If you cannot tell which is more valuable, default to the more frequent one and mark it ASSUMED. [Our take]
11. List what is unknown. Mark every statement that is an assumption, not a fact the user gave you.
12. Stop. Do not start designing. Hand the unknowns to the next steps or ask the user.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- Need-audience, need-constraints and need-alignment are skipped, so this file carries them. Add three short sections to need-statement.md after the assumptions: `## Audience` (who arrives, in what situation, on which device, what could stop them, access needs; each claim tagged evidence or assumption; plus the audience flags and COGA escalation from need-audience), `## Constraints` (brand assets, stack, deadline, content that exists, legal, must-not, accessibility WCAG 2.2 AA and performance defaults, and which shared components render on the page and whether you may change them: header, footer, global styles) and `## Owner's words` (three feeling adjectives, sites liked and disliked; if the owner is unavailable, write your defaults and mark them `ASSUMED, not owner-approved`).
- Keep each section to five lines or fewer. A fact you do not have is an open question in design/OPEN-QUESTIONS.md, not a reason to stop.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- need-constraints and need-alignment are skipped in the sprint, so this file carries them. need-audience is not skipped: the audience keeps its own file. After the assumptions add two short sections to need-statement.md: `## Constraints` (brand assets, stack, deadline, content that exists, legal, must-not, accessibility WCAG 2.2 AA and performance defaults, and which shared components render on the page and whether you may change them: header, footer, global styles) and `## Owner's words` (three feeling adjectives, sites liked and disliked; if the owner is unavailable on Day 1, write your defaults and mark them `ASSUMED, not owner-approved`). brief-write reads them from there.
- Keep each section to five lines or fewer. A fact you do not have is an open question in design/OPEN-QUESTIONS.md, not a reason to stop. Day 1 is the best time to ask the owner: batch the questions in one message with a default for each.
## Ask the owner (only what you cannot default)
- Scope (redesign of an existing site; one letter per line, recommended first). Structure: (a) rebuild from scratch (recommended) (b) keep the current sections and order. Content: (a) rework key parts: hero plus 2 or 3 key sections, the rest kept and moved into the new sections (recommended) (b) keep every text verbatim (c) full rework (d) none supplied: I write draft copy marked unconfirmed. SEO: (a) keep URL, title, meta description, canonical, structured data, heading text and internal links (recommended) (b) free to change.
- What does the company or product do, in one sentence? (a) my draft from the current site: [one sentence] (recommended) (b) your own sentence.
- Who should use the page, and what should they do on it? (a) my reading of the site: [audience] should [primary action] (recommended) (b) a different audience or action: say which.
- How will you know the homepage worked? (a) more [primary action] per 100 visits than the first four weeks after launch (recommended) (b) a number you already track: say which.
## Output template
```markdown
# Need statement
## Scope (asked first; owner's answer or ASSUMED)
- Structure: rebuild | keep
- Content: rework key parts [which] | keep verbatim | full rework | none supplied
- SEO: keep (URL, title, meta description, canonical, structured data, headings, internal links) | free
- Request (no solution words):
- Business goal:
- Visitor goal:
- Primary action (one verb phrase):
- Secondary action (if the owner named two, say which is primary and why; record as open question):
- Success, measurable (relative target if there is no baseline, or ASSUMED):
- Success, observable:
- Out of scope:
## Assumptions (mark each; replace with evidence when you get it)
- [assumption]
```
## Gates
Rules to satisfy: `ux-start-with-needs` (read them with get_guidelines or rules/*.md).
- [ ] The primary action is a single verb phrase.
- [ ] At least one measurable success signal is stated.
- [ ] No sentence in the need statement describes a visual or a feature.
## Done when
- Every field is filled or explicitly marked unknown.
- Assumptions are listed separately from facts.
## Pitfalls
- Writing the solution into the need ('a homepage with a hero video').
- Two or three primary actions: pick one, move the rest to secondary and record the choice as an open question when the owner named both.
- A success target with an invented baseline: use a relative target or mark it ASSUMED.
