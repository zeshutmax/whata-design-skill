# Step: Critique against the brief (`decide-critique`, stage decide)
**Goal:** Review each direction against the brief with a rubric built from the principles and success criteria. Critique asks whether it works, not whether anyone likes it.
**Your role:** Judge each direction against the brief, not against taste. Critique asks whether it works toward the goals.
**Inputs:** hero-concepts, design-principles, success-criteria  
**Output artifact:** critique-notes -> `design/05-decide/critique-notes.md`
## Procedure
1. Build a rubric from the brief's success criteria, the design principles and the anti-goals, plus one row for resemblance to the library's strongest references and the owner's taste anchors (name the sites). Give each row a weight, state it in the table, and make the resemblance row weigh at least as much as the heaviest message row: a rubric made only of message and compliance rows favours the safest direction by construction. Score each direction 1 to 5 per row with a one-sentence reason, multiply by the weight, and check that the totals equal the sum of the rows before you write them down.
2. Run review_design on each hero concept and add its blocker and major findings to the rubric.
3. Ask questions rather than proposing fixes: What problem does this solve? Who is it for? What would make it fail? Park fixes for a later pass. [Craft: critique rules: everyone is a critic, avoid problem-solving, do not rush]
4. Write down which strengths to carry over from each direction, even the ones you will not choose.
## Tools
- `review_design`: path to each hero concept; Quality Bar results
## Output template
```markdown
# Critique notes
## Rubric (criteria from the brief and principles)
| Criterion | Weight | A | B | C |
|---|---|---|---|---|
| Resemblance to the library's strongest references and the owner's taste anchors (name them) | | | | |
| Presence of style: scale contrast, one lead object, deliberate whitespace, imagery (not only absence of slop) | | | | |
| Weighted total (check: equals the sum of the rows) | | | | |
## Questions raised per direction
## Strengths to carry over
## Quality Bar findings per direction
```
## Gates
Rules to satisfy: `distinct-review-against-published-criteria` (read them with get_guidelines or rules/*.md).
- [ ] Every score has a reason.
- [ ] No fixes proposed inside the critique.
## Done when
- The rubric is complete for all directions with Quality Bar findings.
## Pitfalls
- Scores justified by 'I like it'.
- Starting to redesign during critique.
