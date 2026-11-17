# Step: Draft headlines and copy (`explore-copy`, stage explore)
**Goal:** Write headline and subhead options for each direction before polishing visuals.
**Your role:** Write real headlines and calls to action before polishing visuals. Copy shapes layout, not the other way round.
**Inputs:** brief, positioning  
**Output artifact:** headline-drafts -> `design/04-explore/headline-drafts.md`
## Procedure
1. For each direction write three headline options, a subhead, and the label of the primary action. Use the value proposition and tone words; be specific and plain. [Evidence: plain objective language outperformed promotional language; Craft: specific over abstract]
2. Scope keeps the copy (need-statement `## Scope`: keep verbatim)? Do not write new headlines. Write a placement map in headline-drafts.md instead: each existing heading, paragraph and action from content-map.md, and the new section and position it moves into; the only new words allowed are labels the new structure needs, marked as new. coverage checks it later.
3. Button and link labels name the result ('Book a demo', not 'Submit' or 'Learn more').
4. Run the swap test on every headline (replace the company name; if it still reads true for a competitor, rewrite). Strike buzzwords and filler openers. [Our take]
5. Check length: headline readable in two lines on mobile; paragraph and sentence length per the copy rules.
6. Reading level: `copy-reading-grade` targets US grade 6 to 8 for a general audience. For ESL or low-literacy audiences, or a UK public service, aim at grade 5 or lower, or CEFR B1 and GOV.UK-style plain language (short common words, one idea per sentence, the action first) and say the target in headline-drafts. [Our take: the tighter target is ours; the rule's own number is grade 6 to 8] An ESL group also gets: an offer of a translation or an interpreter (links to translated pages with `lang` and `hreflang`, the passage language marked with `lang`; say what the service can really offer, never promise an interpreter you do not have), no idioms or phrasal-verb puns, dates and numbers written out in one unambiguous format, and a plain statement of what happens next.
7. Legal, medical, financial or safety advice in the copy: write it as a draft, list the reviewer you need in design/OPEN-QUESTIONS.md, and mark it with the visible draft marker and legend until a qualified person has signed it off (`copy-expert-review-before-launch`). Do not write a claim you cannot attribute.
8. Forms and urgent routes: write the form's labels, the hint under each, the privacy line, the error and success messages and the phone line together (recipes `form-no-backend-and-privacy` and `urgent-help-route`): plain words, the action first, the hours as text, and "do not write bank details here" wherever a free-text box could collect sensitive data.
9. Facts the owner has not confirmed (a price, an opening hour, a size, a policy) stay in the copy only with the visible `.assumed` marker from the protocol (dotted underline plus a legend on the page), listed in design/OPEN-QUESTIONS.md. No brackets, no bare invention, and no invented customers, numbers, quotes or press at all.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- brief and positioning are replaced by brief-draft.md: use its value proposition, proof or `no proof yet`, tone words and swap-test line. Write three headline options for the one or two directions you will build, not all three if time is short; three are still needed for the chosen one.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- positioning is replaced by the Tone section of brief-draft.md (and brief.md): use its value proposition, proof or `no proof yet`, tone words and swap-test line. Write three headline options for each of the heroes you will build on Day 3, or for the one or two you expect to choose if time is short; three are still needed for the chosen one.
## Output template
```markdown
# Headline drafts
## Direction A
- Headline options (3):
- Subhead:
- Primary action label:
- Reading-level target (grade, or CEFR level) and how it was checked:
- Swap test result:
- Unconfirmed facts used (each marked .assumed on the page and listed in OPEN-QUESTIONS.md):
```
## Gates
Rules to satisfy: `copy-headline-swap-test`, `copy-specific-over-abstract`, `copy-no-buzzwords`, `copy-button-verb-label`, `copy-no-placeholder-text`, `ux-tagline-specific`, `ux-descriptive-labels` (read them with get_guidelines or rules/*.md).
- [ ] Each headline passes the swap test.
- [ ] The primary action label names a result.
- [ ] No placeholder text.
- [ ] Every unconfirmed fact is marked with the visible assumption marker and listed as an open question.
## Done when
- Each direction has headline options, subhead and action label that pass the checks.
## Pitfalls
- Rhetorical slogans ('Not X, it's Y').
- Using the same copy under three visual directions.
