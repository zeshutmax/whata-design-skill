# Step: Set positioning and tone (`brief-positioning`, stage brief)
**Goal:** Choose the value proposition and 3–5 tone words with their opposites.
**Your role:** Decide what the page claims and in what voice, specifically enough that a competitor could not say it.
**Inputs:** brief-draft, landscape-audit  
**Output artifact:** positioning -> `design/02-brief/positioning.md`
## Procedure
1. Write a value proposition in one sentence: who it is for, what it does, why it is different. Use the audience's words, not internal jargon. [Evidence: say who you are, what you offer and how you differ]
2. List three to five proof points that are facts (numbers, names, results), each with its source. If there is no proof yet (new product, no customers), write `no proof yet`, lead with what the product does and how it works instead, and never fill the gap with invented numbers, logos or quotes; list what proof the owner should collect first.
3. Choose three to five tone words, each with its opposite ('direct, not curt'). Add words and phrases to avoid.
4. Run the swap test: replace the company name with a competitor's. If the claim still reads true, rewrite it. [Our take]
## Ask the owner (only what you cannot default)
- What can you prove with a number, a name or a result? (a) only what is already public on the site: [list] (recommended) (b) more: send it with its source.
## Tools
- `search_sites`: optional: read competitor headlines in the landscape audit to check the swap test
## Output template
```markdown
# Positioning
- Value proposition (one sentence):
- Differentiator:
- Proof points (with source):
- Tone words (and their opposites):
- Words and phrases to avoid:
- Swap test result:
```
## Gates
Rules to satisfy: `ux-purpose-clear`, `ux-tagline-specific`, `ux-objective-language` (read them with get_guidelines or rules/*.md).
- [ ] The value proposition passes the swap test only if it is specific: with a competitor's name swapped in it becomes false or absurd.
- [ ] Each proof point has a source.
## Done when
- Value proposition, proof, tone words and swap test result are written.
## Pitfalls
- Superlatives with no evidence.
- Generic claims ('seamless', 'powerful', 'next-generation') that any company could write.
