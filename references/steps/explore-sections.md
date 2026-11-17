# Step: Pick library sections (`explore-sections`, stage explore)
**Goal:** Choose, with the owner, the 2 to 4 finished library sections the page is built from, and say for each what changes in its adaptation slots.
**Your role:** Choose the page's sections from the library: finished, spec-pinned sections from sites the owner curated. The look comes from them; this step decides which ones, in what order, and what goes in their slots.
**Inputs:** brief-draft  
**Output artifact:** section-pick -> `design/04-explore/section-pick.md`
## Procedure
1. Call list_library_sections. Match sections to the brief's jobs: a hero that carries the primary action, then the sections that answer the visitor's top questions, then a close that captures (the Success section of the brief).
2. Propose 2 to 4 sections, plus one alternative for the hero. For each: why it fits this brief, which slots change and with what (words, pictures, the client's product UI, the canvas within the spec's range, one niche accent), and which of its bans matter here.
3. Show the owner one sheet: per section a row with the source (get_library_section's sourceFold, or the live sourceUrl for a lower section) and the rebuild, labelled with the section id. An owner who is not at your keyboard needs the sheet as image files, not links.
4. Write the media plan: for every picture slot, the real photo, video or product UI it will hold and where it comes from. No code-drawn stand-ins for photographs.
5. Write the design system before any section is adapted (content/sections/TOKENS.md): every --ds-* token, one ground, one ink, two greys, one accent, two families plus mono, one h2 size, one h3 style, two buttons, two radii, one container and gutter, one section rhythm. Sections keep their source geometry and motion; their paint and type come from these tokens through content/sections/roles.css (class ds on the page root). Skipping this ships a page where every section brings its source's fonts and colours (a client pilot, 2026-11-16: 41 type styles, 13 text colours, 8 radii, 8 button styles).
6. No section fits a need the brief has: pin a new one from a library site first (content/sections/HOW-TO-ADD.md), or ask the owner for a site to take it from. Do not design that part from scratch.
## Ask the owner (only what you cannot default)
- Which sections should the page be built from? (a) recommended: the proposed set in the order shown (b) the proposed set with the alternative hero (c) other sections or another library site; name them
## Tools
- `list_library_sections`: the sections, their sources and adaptation slots
- `get_library_section`: spec, markup and source screenshot for each candidate
- `record_taste`: record the owner's pick (type pick, gate sections) and words
## Output template
```markdown
# Section pick
Owner pick: (the owner's words, or ASSUMED)

| # | Section id | Source | Why it fits the brief | Slots and their new content | Bans that matter here |
|---|---|---|---|---|---|

## Media plan
| Slot | Real media | Source and licence |
|---|---|---|

## Design system (every --ds-* token; content/sections/TOKENS.md)
| Group | Values |
|---|---|
| Families | |
| Type scale (display, statement, h2, h3, lead, body, small, label) | |
| Ink, muted, subtle, accent (with contrast) | |
| Ground, surface, surface-dim, dark, lines | |
| Container, gutter, section rhythm | |
| Radii, control height, buttons | |

## Gaps
(needs no section covers, and the site a new section will be pinned from)
```
## Gates
- [ ] The design system table is complete: every --ds-* token has a value, contrast noted.
- [ ] 2 to 4 sections, each with its slots filled in.
- [ ] The primary action from the brief has a place in a picked section.
- [ ] Every picture slot has real media in the media plan.
- [ ] The owner picked from a sheet beside the sources, or the pick is marked ASSUMED.
## Done when
- section-pick.md lists the sections in order with their slot content, the media plan and the owner's pick.
## Pitfalls
- Changing a section beyond its slots and calling it an adaptation.
- Picking by description without looking at the sources.
- Filling picture slots with code-drawn placeholders.
