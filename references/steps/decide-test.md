# Step: Test quickly (`decide-test`, stage decide)
**Goal:** Test with about five people per audience group, fix what you find and test again. Several small rounds beat one big one.
**Your role:** Get evidence from people. You cannot be the test participant; plan the test and ask the owner to run it.
**Inputs:** prototype, critique-notes, success-criteria  
**Output artifact:** test-results -> `design/05-decide/test-results.md`
## Procedure
1. Write a short test script: a five-second test (show the first screen, ask what the page is for and what they would do), a preference question between directions, and one task (find X).
2. Ask the owner to run it with about five people per audience group and to send you the answers. Do not substitute model opinions for participants; label any model review as such. [Evidence: five users per group per round find most problems; test, fix, test again]
3. When the owner's score falls after a round, first put the two rounds side by side and list what the new one removed or flattened; restore that before changing anything else. "Clustered" or "too busy" asks for order (consistent styles, spacing, hierarchy, no collisions), not for fewer motifs: ask which parts feel busy, with proposed answers, before cutting. [Our take]
4. Between rounds, the owner's score out of 10 with one sentence of why is cheap, honest evidence and moved a real project more than any audit did. Keep an owner round log in design/05-decide/owner-rounds.md as a table `| Round | Date | Shown | Score | Owner's words | What changed |` (name library slugs in Shown when a concept was anchored on them); `pnpm --silent --filter @whata/mcp taste import --project <project>` copies the scores into this client's taste record. Label it `UNTESTED` evidence about one person's view: it is not approval and not a user test.
5. Run automated checks as a supplement (axe, lab Web Vitals via review_design).
6. Summarize results, fix what you can, and say what remains unproven.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- Day 5 is the test day. If there are no people to test with (no owner, no participants), write the script, the participant list you would need and the questions in test-results.md, and record `UNTESTED` at the top. Do not fill the answers with a model's opinions. decide-choose then decides on the critique and the inclusion check alone and says the decision is untested.
## Ask the owner (only what you cannot default)
- Can you run the five-second test with 5 people? (a) not now: I record UNTESTED and decide on the critique (recommended if no one is available) (b) yes: I send the script.
## Tools
- `review_design`: automated supplement
## Output template
```markdown
# Test results
## Script
## Participants (group, count) and answers
## Findings and fixes
## Automated results (labelled automated)
## Not yet proven
```
## Gates
Rules to satisfy: `ux-test-iteratively` (read them with get_guidelines or rules/*.md).
- [ ] Participant answers come from people, not from the model.
- [ ] The five-second test result is compared with the success criteria.
## Done when
- Results from real people are recorded, or the absence is stated and the decision labelled 'untested'.
## Pitfalls
- Calling a model's review a user test.
