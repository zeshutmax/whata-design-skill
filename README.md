# whata.design skill

A web design skill for Claude Code (and any agent that reads Markdown): a designer's process from need to launch,
a Quality Bar of testable rules, recipes that keep bold styles accessible, and named design principles.

- What it is and how it works: https://whata.design/skill/
- The library it is built on: https://whata.design/library/
- Version: 2026-11-17 (96e1ad0)

## Install

Claude Code, for all your projects:

```bash
git clone https://github.com/zeshutmax/whata-design-skill ~/.claude/skills/whata-design
```

Or for one project, from its root:

```bash
git clone https://github.com/zeshutmax/whata-design-skill .claude/skills/whata-design
```

Then ask Claude to design or review a homepage; the skill loads when the task matches. Update with `git pull` in that folder.

Other agents: point them at `SKILL.md` and let them read `references/` as the steps ask.

## What is inside

- `SKILL.md`: the operating protocol (process, honesty rules, how to ask the owner, the Quality Bar).
- `references/steps/`: one file per step.
- `references/rules/`: the testable rules, by group.
- `references/recipes/`: stylish looks that pass the rules.
- `references/principles.md`, `taxonomy.md`, `trends.md`, `GUIDE.md` and `guide.json` (everything in one file, for tools).

The MCP server (live library search, measured sections and a browser reviewer) is not public yet: https://whata.design/mcp/

## Licence

Creative Commons Attribution-NonCommercial 4.0 (CC BY-NC 4.0). Use it in your own and your clients' projects; do not resell
the guide itself. See LICENSE.
