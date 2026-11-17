# Step: Iterate and run a retro (`reflect-iterate`, stage reflect)
**Goal:** Decide what to change next and what the process taught.
**Your role:** Decide what to change next and what the project taught about the process.
**Inputs:** metrics-report, qa-report, papercut-log  
**Output artifact:** retro-notes -> `design/07-reflect/retro-notes.md`
## Procedure
1. Copy the owner's round scores into this client's taste record: `pnpm --silent --filter @whata/mcp taste import --project <project dir>` (reads design/05-decide/owner-rounds.md), then `taste profile --project <project dir>`: it also adds the project's line to the shared clients record, so the next client in the same niche starts from a better recommended answer.
2. Turn findings (metrics, QA leftovers, owner feedback, and the papercut log from realize-sweep, handled together as one design pass, not one by one) into a prioritized list of changes with expected impact and effort.
3. Run a short retrospective: what helped, what wasted time, which assumptions were wrong, which rules or recipes needed correcting.
4. If exploration changed the problem, update the brief version and note why (the brief is a hypothesis). [Evidence]
## Output template
```markdown
# Retro and next changes
## Prioritized changes
## What helped / what wasted time
## Assumptions proven wrong
## Corrections needed in the guide (rules, recipes, steps)
```
## Gates
- [ ] Corrections to the guide are listed, not forgotten.
## Done when
- A prioritized list and retro notes exist.
## Pitfalls
- Treating launch as the end.
