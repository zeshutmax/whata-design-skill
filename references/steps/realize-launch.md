# Step: Hand off and launch (`realize-launch`, stage realize)
**Goal:** Release, redirect, monitor and hand over the files and guidelines.
**Your role:** Release safely and leave the next person (or agent) what they need to maintain the design.
**Inputs:** built-site, qa-report  
**Output artifact:** launched-site -> `design/06-realize/launched-site.md`
## Procedure
1. Pre-launch checklist: title, description, language, favicon, social image, 404 page, redirects, robots, analytics (only if wanted), consent if required, performance on the production build.
2. Refuse to launch while any unconfirmed fact remains: search the built page for the `.assumed` marker (and the legend), and read design/OPEN-QUESTIONS.md. Each marked fact must be confirmed by the owner and its marker removed, or the fact removed; if any remain, stop and report them to the owner instead of deploying. Also search for brackets, `lorem`, and example domains (`.example`) in addresses and links. [Our take]
3. Advice copy: find every passage that gives legal, medical, financial or safety advice and the draft marker on it. Each needs a qualified reviewer's sign-off recorded (name, date) in design/OPEN-QUESTIONS.md before the marker is removed. Without that sign-off the page does not ship with the advice as final; remove the passage or ship it as a clearly marked draft only if the owner agrees in writing. (`copy-expert-review-before-launch`) [Our take]
4. Deploy per the constraints; re-run review_design against the live URL.
5. Hand over: design-tokens folder, DESIGN.md, component notes, QA report, how to update content, known issues.
## Ask the owner (only what you cannot default)
- Deploy where and when? (a) not yet: I hand over a built, audited page for your review (recommended) (b) deploy to [target] on [date].
## Tools
- `review_design`: the live URL
## Output template
```markdown
# Launch
- URL and date:
- What shipped:
- Live review summary:
- Handover notes:
```
## Gates
Rules to satisfy: `a11y-page-title`, `a11y-lang`, `perf-lcp`, `copy-expert-review-before-launch` (read them with get_guidelines or rules/*.md).
- [ ] The live URL passes the same review as the build.
- [ ] No `.assumed` marker, legend or open question about a fact remains on the shipped page.
- [ ] Every passage of legal, medical, financial or safety advice has a recorded qualified reviewer, or is not shipped as final.
## Done when
- The site is live, reviewed in production and documented.
## Pitfalls
- Launching without re-testing the production build.
- Shipping dotted-underline facts the owner never confirmed, or an example email address.
