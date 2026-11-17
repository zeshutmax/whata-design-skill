# Step: Review and sign off (`brief-review`, stage brief)
**Goal:** Check the brief against a checklist and get agreement before design starts.
**Your role:** Check the brief against a checklist and get the owner's agreement before design starts.
**Inputs:** brief-draft, positioning, content-inventory, success-criteria  
**Output artifact:** brief -> `design/02-brief/brief.md`
## Procedure
1. Run the checklist below on the draft and fix failures.
2. Assemble brief.md: the one-page brief plus positioning, content inventory and success criteria as linked sections.
3. Ask the owner to approve. Record the approval and the version.
4. Owner unavailable: do not stop and do not write `approved`. Use the heading `# Brief v1 (NOT owner-approved, ASSUMED)`, tick the approval box as `requested, open` and list the approval as the first line of design/OPEN-QUESTIONS.md. Every later artifact then inherits the label `ASSUMED, not owner-approved` (protocol 4).
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- positioning and content-inventory are replaced by the Tone and Content inventory sections of brief-draft.md. Assemble brief.md from brief-draft.md and success-criteria.md; the checklist below then also asks that both sections exist.
## Ask the owner (only what you cannot default)
- Do you approve this brief (v1)? (a) yes, approved as written (recommended) (b) approve with changes: list them.
## Output template
```markdown
# Brief v1 (approved [date] by [name])
(owner unavailable: write the heading as "# Brief v1 (NOT owner-approved, ASSUMED)")
(links to positioning, content inventory and success criteria; sprint: the Tone and Content inventory sections of brief-draft)
## Checklist
- [ ] One page
- [ ] What and why, not how
- [ ] Measurable success criteria
- [ ] Constraints as inputs
- [ ] Assumptions flagged
- [ ] Owner approval recorded (or, owner unavailable: heading says NOT owner-approved, ASSUMED; approval listed as open)
```
## Gates
- [ ] All checklist boxes ticked.
- [ ] Approval recorded; owner unavailable: the heading says NOT owner-approved, ASSUMED and the approval is listed as an open question.
## Done when
- The owner has approved and the version is recorded, or the brief is headed `NOT owner-approved, ASSUMED` and the approval is an open question.
## Pitfalls
- Moving on without approval; the brief then cannot arbitrate later disputes.
