# Step: Write design principles (`ref-principles`, stage references)
**Goal:** Distill 3–5 principles and 3 anti-goals that guide every later decision.
**Your role:** Distill the project's own design principles, short and testable, so later choices have a rule to be judged against.
**Inputs:** brief, reference-notes  
**Output artifact:** design-principles -> `design/03-references/design-principles.md`
## Procedure
1. From the brief and reference notes write 3 to 5 principles. Each one must be a positive, testable sentence that can decide between two options ('Evidence before ornament', 'One idea per screen').
2. Add 3 anti-goals: things the design must not be. Include one derived from the niche's default look.
3. Trace each principle back to a brief line or a reference note. Use established principle sets (Rams, Nielsen, Norman, POUR) as a lens to check for gaps; do not copy them in. [Craft]
4. Write one tension the design will have to manage (for example calm versus bold) and which side wins when they conflict.
## Ask the owner (only what you cannot default)
- Do these principles fit the project? (a) yes, as written (recommended) (b) change: say which.
## Tools
- `get_principles`: the library of named principles with how to apply and check them
## Output template
```markdown
# Design principles
## Principles (each can decide between two options)
1. [principle] : traces to [brief line / reference]
## Anti-goals
## The main tension and which side wins
```
## Gates
Rules to satisfy: `distinct-written-direction` (read them with get_guidelines or rules/*.md).
- [ ] Each principle can be used to reject an option.
- [ ] No principle is a platitude ('be user-friendly').
## Done when
- 3 to 5 principles, 3 anti-goals and one stated tension.
## Pitfalls
- Vague principles that never reject anything.
