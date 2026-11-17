# Step: Understand the audience (`need-audience`, stage need)
**Goal:** Talk to and observe real people. Describe who visits the homepage, what they came for, how aware they are and on which devices.
**Your role:** Describe the real people the page serves, from evidence where it exists. Do not invent personas.
**Inputs:** need-statement  
**Output artifact:** audience-profile -> `design/01-need/audience-profile.md`
## Procedure
1. List up to three audience groups. For each write: the situation they arrive in, what they already know about the company, the decision they must make, the device and setting, and what could stop them (doubt, risk, time).
2. Use only evidence the user has given you (interviews, analytics, support questions, sales notes). Mark everything else 'assumption'. [Evidence: start from user data, not assumptions]
3. If there is no evidence, say so in the file and recommend the owner run 3 to 5 short conversations before launch; continue with clearly marked assumptions.
4. Add access needs for each group: screen reader or keyboard use, low vision or zoom, motor limits, cognitive load, slow networks, small screens, one-handed use. [Craft: designing for the margins improves the page for everyone]
5. Flag the groups that need cognitive accessibility first: people under stress (a crisis, a deadline, a frightening letter), with low literacy, reading in a second language (ESL), with cognitive or learning disabilities, or who use a screen reader or have dyslexia. If any group has a flag, write `COGA escalation: yes` in the file: the 15 `a11y-coga-*` rules are then treated as major for this project, and brief-write says so. Also note the reading level to aim for (see `copy-reading-grade`: a lower target for ESL, low-literacy and UK public-service audiences) and whether a translation or interpreter offer is needed. [Our take]
## Ask the owner (only what you cannot default)
- Do you have real customer evidence? (a) no: I mark audience claims as assumptions (recommended if none exists) (b) yes: send interviews, analytics or sales notes.
- Which groups matter most? (a) my proposal: [group 1], [group 2] (recommended) (b) a different order or group: say which.
## Output template
```markdown
# Audience profile
## Group 1: [name]
- Situation on arrival:
- What they know already:
- Decision they must make:
- Device and setting:
- What could stop them:
- Access needs:
- Audience flags (stress | low literacy | ESL | cognitive or learning disability | screen-reader or dyslexia users | none):
- COGA escalation (yes: treat the a11y-coga-* rules as major | no):
- Evidence: [source | assumption]
```
## Gates
Rules to satisfy: `ux-start-with-needs`, `a11y-test-with-people` (read them with get_guidelines or rules/*.md).
- [ ] Every group states a situation, not only a demographic.
- [ ] Each claim is tagged evidence or assumption.
## Done when
- Two or three groups, each with situation, decision, device, access needs and an evidence tag.
## Pitfalls
- Demographic personas ('Sarah, 34, loves coffee').
- Omitting assistive technology and small-screen use.
- Leaving a stressed, low-literacy or ESL audience unflagged, so the COGA rules stay minor and get missed.
