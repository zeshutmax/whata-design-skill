# Step: Choose and document (`decide-choose`, stage decide)
**Goal:** Pick a direction and write down why, what was rejected, and what to carry over.
**Your role:** Choose a direction and record why, so the decision can be revisited with the same facts.
**Inputs:** critique-notes, inclusion-check, test-results, success-criteria  
**Output artifact:** direction-decision -> `design/05-decide/direction-decision.md`
## Procedure
1. An early pick: when the owner already picked one bundle or sketch at gate 1, record it here (`Owner pick:`, gate 1) at that moment and say so; gate 2 then confirms it with the built concepts instead of asking again from scratch.
2. Start from the owner's pick. The owner chose from the directions sheet (gate 2, explore-directions); record their words as `Owner pick: ...` at the top of the decision, with any mix they asked for, and record it with record_taste (type pick, gate 2, the project folder, the anchor slugs of the picked concept, their words). No pick recorded means this step is not done: do not decide for them (protocol 4).
3. Apply the decision rule from the success criteria to the critique, inclusion check and test results, and write your own scoring as advice under the heading `The model's ranking, for what it is worth`. If your ranking disagrees with the owner's pick, say so in one line and follow the pick.
4. Write the decision log: chosen direction, scores, reasons, rejected directions and why, what to carry over from rejected ones, and open risks.
5. Name the crux surfaces: the one or two parts of the page it stands or falls on (for example the hero and the booking path). They get the longest polish in realize-sweep. Choose them from the need and the brief, not from what is easiest to make beautiful.
6. The final choice of taste is the owner's: nothing here overrides the pick.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- Short form. critique-notes is replaced by the scoring table in hero-concepts/notes.md (each concept against the success criteria and the anti-goals, with its review_design findings, labelled a model review). test-results is replaced by `UNTESTED`: no test was run, so say so in direction-decision.md and decide on the critique and the inclusion check alone.
- Write the decision in ten lines or fewer: chosen concept, why against the criteria, rejected and why, what to carry over, open risks. The owner's pick is still required: lean keeps both taste gates. If the owner is away, the pick is the blocking question in design/OPEN-QUESTIONS.md and decide-tokens waits.
- decide-tokens and realize-build read this file in lean; the headlines and the chosen hero come from explore-copy and explore-hero.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- The days are named after the GV sprint: Day 3 "Decide" holds the critique and the inclusion check, and the decision is recorded here on Day 5, after the test. The owner confirms it here. If test-results.md says `UNTESTED`, decide on the critique and the inclusion check and write `UNTESTED` in direction-decision.md. The owner's pick from the Day 2 or Day 3 sheet is required; if they are away, the pick is the blocking question in design/OPEN-QUESTIONS.md and Day 4 waits.
## Ask the owner (only what you cannot default)
- Which direction do you pick from the sheet? (a) [n], my recommendation (recommended) (b) another number or a mix: say which.
## Output template
```markdown
# Direction decision (date, decider: the owner)
- Owner pick: [the owner's words]
- Chosen:
- Why (against the criteria):
- Crux surfaces (polished longest):
- Rejected and why:
- Carry over from rejected directions:
- Open risks and how they will be watched:
## The model's ranking, for what it is worth (advice, not the decision)
```
## Gates
Rules to satisfy: `distinct-written-direction` (read them with get_guidelines or rules/*.md).
- [ ] `Owner pick:` is recorded in the owner's words; without it the step is not done.
- [ ] The decision cites the criteria, not preference alone.
- [ ] The model's scoring is labelled as advice.
## Done when
- The owner's pick is recorded and the decision log is written.
## Pitfalls
- Choosing for the owner and marking it ASSUMED.
- Letting the model's scoring table make the decision.
- Choosing without recording the rejected options.
