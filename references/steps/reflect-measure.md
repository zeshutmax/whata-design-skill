# Step: Measure (`reflect-measure`, stage reflect)
**Goal:** Compare real results with the success criteria.
**Your role:** Compare real results with the success criteria after enough time has passed.
**Inputs:** launched-site, success-criteria  
**Output artifact:** metrics-report -> `design/07-reflect/metrics-report.md`
## Procedure
1. Ask the owner for the measures named in the success criteria after an agreed period (for example four weeks).
2. Compare each result with its target. Note what you cannot conclude (sample too small, no baseline, seasonal effects).
3. Re-run review_design on the live site; compare with launch.
## Ask the owner (only what you cannot default)
- Can you share the numbers for the success measures? (a) yes, the last four weeks from [analytics tool] (recommended) (b) not yet: I list what to collect.
## Tools
- `review_design`: live URL
## Output template
```markdown
# Metrics report
| Criterion | Target | Result | Verdict | Caveat |
|---|---|---|---|---|
```
## Gates
- [ ] Each criterion has a result or a stated reason for none.
## Done when
- Every success criterion is compared with a result.
## Pitfalls
- Claiming causes without a baseline.
