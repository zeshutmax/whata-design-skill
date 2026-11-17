# Step: Define success criteria (`brief-success`, stage brief)
**Goal:** Write measurable and qualitative criteria that decide between options later.
**Your role:** Fix the criteria that will decide between options later, so taste does not decide alone.
**Inputs:** need-statement  
**Output artifact:** success-criteria -> `design/02-brief/success-criteria.md`
## Procedure
1. Write measurable criteria (for example a conversion target, a task success rate in a test, a load-time target) and qualitative criteria (a five-second test: at least 4 of 5 people can say what the page is for).
2. For each measurable criterion find the event, query or report that produces the number, and check that it fires today (read the tracking code and trigger it once). A criterion nothing records will read zero: if the event does not exist or is declared but never sent, building it is part of the work, so add it to the brief's scope and to the build plan.
3. Conversion: name what the page captures (an email, a booking, a sign-up, a purchase) and the value the visitor gets in exchange (a plan, a checklist, reminders, a quote). A page that has a form must use it to capture, with that exchange stated next to it; copy that promises the opposite ("no email") needs the owner's say-so. Write where the capture appears: in the first screen, repeated after each major section, and in a closing band. In a real run the owner's verdict on a stylish page was "very little conversion potential" because its only action captured nothing. [Our take]
4. Add the quality bar: zero blocker failures from the Quality Bar, WCAG 2.2 AA, Web Vitals targets from the constraints.
5. Write the decision rule: how directions will be compared and who decides (usually the owner).
## Ask the owner (only what you cannot default)
- What would make you call the homepage a success? (a) [primary action] per 100 visits up against the first four weeks (recommended) (b) another number or event: say which.
## Tools
- `get_guidelines`: topic 'blockers' to cite the quality bar
## Output template
```markdown
# Success criteria
## Measurable
## Qualitative (five-second test and others)
## Quality bar (blockers = 0, WCAG 2.2 AA, Web Vitals)
## Decision rule and decider
```
## Gates
Rules to satisfy: `ux-test-iteratively` (read them with get_guidelines or rules/*.md).
- [ ] At least one criterion can be measured without opinion.
- [ ] Quality-bar line is present.
## Done when
- Criteria and the decision rule are written.
## Pitfalls
- Only subjective criteria ('feels modern').
