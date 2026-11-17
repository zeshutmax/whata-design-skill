# Step: Write the brief (`brief-write`, stage brief)
**Goal:** Turn the need into a one-page brief: purpose, audience, message, tone, scope, constraints.
**Your role:** Turn the need into a one-page brief that says what and why, not how. Treat it as a hypothesis you will revise.
**Inputs:** need-statement, audience-profile, job-story, constraints, kickoff-notes  
**Output artifact:** brief-draft -> `design/02-brief/brief-draft.md`
## Procedure
1. Write the brief from the need statement, audience profile, job stories, constraints and kickoff notes. Keep it to one page.
2. Sections: problem and why now; audience and situation; goal and primary action; message; tone (filled in by the next step); scope (what the homepage contains and what it does not); constraints as inputs; deliverables and what 'done' means.
3. State the version (v1). The brief changes if exploration reframes the problem; record each change with the reason. [Evidence: problem and solution develop together]
4. Do not describe visuals or technology. If a sentence says how, move it to the constraints or delete it.
5. Audience flags: if the audience profile flags people under stress, with low literacy, ESL, cognitive or learning disabilities, or screen-reader or dyslexia users, write under `Audience and situation`: `COGA escalation: the a11y-coga-* rules are major for this project` and name the reading level to aim for. Those rules (all fifteen are in `rules/build.md`) are then part of the brief's definition of done. [Our take]
## Sections track (default)
Applies only when the owner and you chose the sections track. In full, sprint and lean tracks ignore this section.
- audience-profile, job-story, constraints and kickoff-notes are replaced by the Audience, Jobs, Constraints and Owner's words sections of need-statement.md. Read them from there.
- Fill the Success section for real: the one primary action (a lead, a sign-up, a booking) and how it is counted. realize-qa checks it, and the picked sections must give it a place (a form slot in the hero or the close).
- Keep the brief to one page. Its job in this track is to say what the page must do and say, not what it looks like: the look comes from the library sections picked next.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- Audience, constraints and kickoff notes are replaced by the Audience, Constraints and Owner's words sections of need-statement.md. Read them from there.
- Positioning and design-principles are skipped, so fill the `Tone` section for real instead of leaving a placeholder: a one-sentence value proposition (who, what, why different), proof points with sources or `no proof yet`, three to five tone words each with its opposite, and three anti-goals (one derived from the niche's default look). Later lean steps read these lines from brief-draft.md as positioning and principles.
- The brief stays v1 and is not reviewed by the owner in lean: mark it `ASSUMED, not owner-approved` unless the owner has read it. It still must fit one page.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- constraints and kickoff-notes are replaced by the Constraints and Owner's words sections of need-statement.md. audience-profile and job-story exist as their own files in the sprint.
- positioning and the content inventory are skipped, so brief-draft carries them. Fill `Tone` as in lean: a one-sentence value proposition (who, what, why different), proof points with sources or `no proof yet`, three to five tone words each with its opposite, a swap-test line and three anti-goals (one from the niche's default look). Add a `## Content inventory` section: a table with one row per block the page needs (block, the visitor question it answers, priority must/should/could, source provided/to write/to produce, status) and the primary action's place. Twelve rows or fewer. Facts the owner has not confirmed get status `unconfirmed` and go in design/OPEN-QUESTIONS.md. Any block that gives legal, medical, financial or safety advice is also marked `needs expert review` (`copy-expert-review-before-launch`).
- ref-principles later refines the tone words and anti-goals into design principles; keep them in the brief as well. brief-review turns this file plus success-criteria into brief.md.
## Output template
```markdown
# Design brief (v1)
## Problem and why now
## Audience and situation
## Goal and primary action
## Message (what the page must make people understand)
## Tone (placeholder, completed in positioning; in lean and sprint fill it here: value proposition, proof or 'no proof yet', tone words with opposites, three anti-goals)
## Scope: includes / excludes
## Constraints (inputs, not obstacles)
## Deliverables and what done means
## Content inventory (sprint only; in full and lean see brief-content)
## Change log
```
## Gates
Rules to satisfy: `ux-start-with-needs` (read them with get_guidelines or rules/*.md).
- [ ] One page or less.
- [ ] No visual or technical solution is prescribed.
- [ ] Success criteria and constraints appear (full criteria are written in brief-success).
## Done when
- All sections exist; the brief is versioned.
## Pitfalls
- A brief that is a feature list or a mood board in words.
