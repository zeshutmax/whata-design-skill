# Step: Explore type and color (`explore-type-color`, stage explore)
**Goal:** Try type pairings and palettes with defined roles for each direction, and check text contrast against WCAG AA from the start.
**Your role:** Make type and color concrete for each direction, with roles and proven contrast.
**Inputs:** direction-matrix  
**Output artifact:** type-color-studies -> `design/04-explore/type-color-studies.md`
## Procedure
1. For each direction choose at most two type families with roles (display, body), a scale with named steps, and a measure for body text. Follow the craft rules for size, line length and line height. [Craft]
2. Define the palette as named roles (background, surface, text, text-muted, accent, border, focus, and state colors). Compute contrast for every text/background pair and every UI/background pair with check_contrast; fix pairs that fail: normal text 4.5:1, large text and UI parts 3:1. [Standard]
3. State what the accent is for (one job) and keep the palette small. Reserve semantic colors for meaning. [Craft]
4. Fonts: use only fonts you can ship. If the owner gave brand fonts, use them. Otherwise choose one of two, and write which and why. (a) A deliberate system stack is an allowed default (for example a native transitional serif, humanist or grotesque stack): name the stack and the reason, and warn that it renders differently per operating system (a stack that begins with Charter shows Charter on Apple devices, Cambria on Windows and something else on Android or Linux): check size, line length and line breaks with the fallback face too, and state which systems you did not see. (b) An open-licence web font, saved locally and self-hosted: look in places such as Fontsource, Google Fonts (download and self-host, do not link), or Open Foundry; these are names to look in, not endorsements, and licences differ per family, so read the licence file that comes with the font and record it in assets.md before relying on it. Check that the font file is present before you rely on it. Build-time self-hosting counts as self-hosting and needs no separate download approval: in a Next.js project `next/font/google` (or `next/font/local`) downloads an open-licence family at build and serves it from the site, with no runtime link; the same goes for a Fontsource package. A system stack is a last resort, not the owner-away default: in a real run the safe reading (dropping a web serif for Charter and Georgia) made the page look generic. Show the font on the directions sheet so the owner picks it with the look. Never link a font from a CDN you cannot reach offline, and never design with a font that will silently fall back to a different one. Check the fallback in the browser at the chosen sizes. [Craft]
5. Do not use a reflex palette or font without a stated reason (see the distinctiveness rules). If you choose a common font or hue, write why.
## Ask the owner (only what you cannot default)
- Brand fonts or colours that fix some choices? (a) keep the current logo colour and fonts where the direction allows (recommended) (b) free to change everything.
## Tools
- `check_contrast`: pairs [{fg, bg, role}] with role text (4.5:1, the default if you leave it out), large-text (3:1) or ui (3:1, borders, focus rings, icons); returns ratio and pass/fail
- `find_by_color`: to find references near a brand color
- `get_design_system`: a reference's tokens as a starting point
## Output template
```markdown
# Type and color studies
## Direction A
- Type: [families and roles], scale [steps], measure [ch]
- Palette roles and verified contrast table:
| Role | Hex | Used on | Ratio | Passes |
|---|---|---|---|---|
- Why these choices (not defaults):
```
## Gates
Rules to satisfy: `a11y-contrast-text`, `a11y-non-text-contrast`, `craft-color-role-tokens`, `craft-type-scale-tokens`, `craft-measure-body`, `craft-line-height-body`, `craft-body-size-min`, `distinct-no-ai-palette`, `distinct-display-font-chosen` (read them with get_guidelines or rules/*.md).
- [ ] Every text/background pair is in the contrast table with a computed ratio.
- [ ] Every default font or hue has a written reason.
## Done when
- Each direction has type, scale, palette roles and a passing contrast table.
## Pitfalls
- Eyeballing contrast.
- Neon or pastel text on a matching background.
- More than two families.
- Leaving out role for a border or focus ring: every pair is then judged as body text at 4.5:1.
- A system stack presented as one face: it is a different face on each operating system.
- Falling back to a system stack to stay safe: it is a font choice too and must be shown on the sheet.
