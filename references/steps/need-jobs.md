# Step: Frame the job to be done (`need-jobs`, stage need)
**Goal:** Write the job story: the situation, the motivation and the progress the visitor wants to make.
**Your role:** Describe what each visitor is trying to get done, in their words, without naming a product or feature.
**Inputs:** need-statement, audience-profile  
**Output artifact:** job-story -> `design/01-need/job-story.md`
## Procedure
1. For each audience group write one to three job stories: 'When [situation], I want to [motivation], so I can [outcome].' [Craft: the job-story format comes from Intercom's practitioners, not from Christensen, Moesta or Ulwick, whose definitions of a job differ; treat the format as a convenience]
2. A job statement must not contain a solution (no product, page type or feature). Rewrite until it does not.
3. Rank the jobs by how often they occur and how costly failure is. The top job drives the primary action.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- audience-profile is replaced by the Audience section of need-statement.md. Write one to three job stories from it and rank them; the top one must match the primary action.
## Output template
```markdown
# Job stories
1. When [situation], I want to [motivation], so I can [outcome].
   - Group:
   - Frequency / stakes:
```
## Gates
- [ ] No job story names a feature or a page.
- [ ] Top job is consistent with the primary action in the need statement.
## Done when
- Each group has at least one ranked job story.
## Pitfalls
- Smuggling the solution into the job ('I want a dashboard').
