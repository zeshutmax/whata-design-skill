# Step: Define the tokens (`decide-tokens`, stage decide)
**Goal:** Fix color roles, type scale, spacing, radius and elevation; write them as a DESIGN.md.
**Your role:** Freeze the design decisions as tokens so building is mechanical and consistent.
**Inputs:** direction-decision, type-color-studies  
**Output artifact:** design-tokens -> `design/05-decide/design-tokens/`
## Procedure
1. Write the tokens: color roles with a verified contrast table, type scale (rem), spacing scale, radii, borders, elevation, motion durations and easing, container widths, breakpoints. [Craft]
2. Write a role table in DESIGN.md: every text role on the page (h1, section heading, card or item title, lead, body, label, numeral or stat, button, nav, caption, small print) gets exactly one token (family, size step, weight, case). Every element of a role uses that token; peers in one list or row (all values of a readout, all phase names) are one role, and an override for one member is a defect. Keep the hero to about four styles and the page to about eight. In a real run the owner's first complaint was "too many font variations, same-level things don't have the same font". `pnpm --silent --filter @whata/audit cli types <file>` checks it. [Our take]
3. Produce three files: DESIGN.md (the agent-readable summary with dos and don'ts), tokens.json in the W3C design-tokens format, tokens.css (CSS custom properties).
4. Verify every contrast pair again with check_contrast and put the ratios in DESIGN.md. Include the recipe steps that apply to this direction.
5. State the anti-slop decisions: which defaults you chose deliberately and why.
6. Fonts: use the family shown on the sheet the owner picked from. Build-time self-hosting of an open-licence family (`next/font/google` or `next/font/local` in Next.js, a Fontsource package) is self-hosting and needs no separate download approval. A system stack remains allowed but only as a choice the owner saw on the sheet, never as a silent default; name it and warn that it renders as a different face per operating system (Charter on Apple devices, Cambria on Windows, another face on Android or Linux), and keep the same stack in tokens.json, tokens.css and DESIGN.md. For a web font, open-licence places to look are Fontsource, Google Fonts (download and self-host, never link) and Open Foundry, as names only: read the licence file that comes with the font and record it in assets. Details: explore-type-color. [Craft]
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- type-color-studies is replaced by the draft tokens in direction-matrix.md and the chosen hero: start from them, then verify every pair again and freeze. direction-decision.md comes from the short decide-choose.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- type-color-studies is replaced by the draft tokens in direction-matrix.md and the chosen hero: start from them, then verify every pair again and freeze. direction-decision.md comes from decide-choose earlier on Day 5. Font sourcing and the per-OS warning above apply, because the sprint has no explore-type-color step.
## Tools
- `check_contrast`: all pairs; pass role text (default, 4.5:1), large-text (3:1) or ui (3:1) for each pair
- `get_design_system`: for the format of reference DESIGN.md files
## Output template
```markdown
# Design tokens
DESIGN.md: north star, principles, color roles with contrast table, type scale, spacing, radii, elevation, motion, components list, dos and don'ts, recipe steps that apply.
tokens.json: DTCG format ($type, $value).
tokens.css: :root { --color-bg: ...; --space-1: ...; }
```
## Gates
Rules to satisfy: `craft-color-role-tokens`, `craft-type-scale-tokens`, `craft-spacing-scale-tokens`, `distinct-radius-elevation-scale`, `a11y-contrast-text` (read them with get_guidelines or rules/*.md).
- [ ] Every token has a purpose.
- [ ] Every contrast pair has a computed ratio.
- [ ] No raw hex values are expected in components later: only tokens.
## Done when
- DESIGN.md, tokens.json and tokens.css exist and agree.
## Pitfalls
- Tokens that only name values (blue-500) instead of roles.
- Skipping the dos and don'ts.
- A font stack in the tokens that is not the stack the build uses.
- Checking a border or focus ring as body text (or the other way round): set role per pair.
