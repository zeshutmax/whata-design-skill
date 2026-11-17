# Step: Gather references (`ref-gather`, stage references)
**Goal:** Collect 15–30 references by niche, style and mood, not only from direct competitors.
**Your role:** Collect references that point the way. References are evidence for decisions, not things to copy.
**Inputs:** brief  
**Output artifact:** reference-board -> `design/03-references/reference-board.md`
## Procedure
1. Gate 1, taste intake, before any search: call taste_intake (brief text, tag slugs; lean and sprint ask for 3 bundles, full 4). It returns style bundles: each named after two library sites, with three feeling words, why it could fit and what it takes from each site. Rewrite each `why` in one line for this project. Make one cheap hero sketch per bundle on the base kit (get_base: header plus one hero skeleton, with the bundle's tokens): the real headline and primary action in the bundle's type, colour and lead object, about fifteen lines of your own on top of the kit, the widths check passed, drawn fresh (when the scope says rebuild, never on the old layout), with the graphic from the asset plan below. Put them on one labelled sheet (`pnpm --silent --filter @whata/audit cli sheet design/03-references/bundles <sketch>="Bundle name|three feeling words" ...`) and send it with the bundle sites' screenshots. Ask the ref-gather question (proposed answers as letters, your recommended bundle first). These sketches become the explore-hero concepts: refine them there, do not start over.
2. Asset and motion plan at gate 1: for each bundle say what the hero's visual is and its one lead motion (from the bundle sites' motion, get_craft gives their timing), made in code first (a data graph or diagram from the real content, type as image, an SVG motif in the bundle's colours; plan_graphics proposes one per section). A paid generated image appears only as a marked placeholder with its proposed prompt; it is generated later and only after the owner's yes (protocol 6).
3. The library is the owner's taste profile: every site in it is liked, the plain ones included, so include the most visually ambitious sites (art-style, standout and motion tags) alongside the quiet ones and do not pre-filter to what looks safe for the niche. Record the answer as the first line of the board: `Owner taste: bundle [n] ([slugs]), not for this project [slugs], why: ...`; library rows the owner picked are `taste anchor` rows. Record the answer with record_taste (type pick, gate 1, the project folder, picked and notFor slugs, their words, the project's industry slugs). Pass the project (and industry) to taste_intake so the client's earlier answers, or earlier clients in the same niche, pick your recommended bundle. A client new to this can do the faster intake first: 8 to 10 A-vs-B pairs (taste_pairs with the project), answered as letters and recorded as type ab. Owner away: send the question, draft the board meanwhile, and write `Owner taste: waiting for the owner`; explore-directions cannot finish without it (protocol 4).
4. Look at the pictures, not only the text: every library site has fold screenshots and section crops under `storage/sites/<slug>/` (get_site and get_design_brief give the paths; get_sections and get_section give per-section crops). Open the images for every library row you keep; a text brief alone does not tell you whether a site is visually ambitious.
5. Call list_tags first (facets art-style, mood, industry, site-type) and pass tag slugs (recommend takes them in `tags`, search_sites in `allOf`/`anyOf`), not sentences: a natural-language brief often matches no tag and returns only a fallback. Then call recommend with the brief plus those slugs, and the owner's liked slugs from the taste intake as `taste` (they come first and sites that look like them rank higher), and search_sites across at least three art-style families that fit the tone words. recommend can return references from an unrelated niche because it matches on style tags (a playful ceramics brief can return a software product): read why each one was returned before you keep it.
6. See how big the library is before you search for niche matches: search_sites with `{}` returns the library total. An empty result for a niche (for example `text: "ceramics"`) usually means the library has nothing there, not that your query is wrong; go to the thin-library step below instead of retrying variants.
7. Gather 15 to 30 references: about a third from the same niche, a third from adjacent niches, a third chosen purely for style, type or motion. [Our take: diverse references prevent copying the niche's default]
8. Use find_similar from your strongest reference.
9. Include the library's strongest visual sites even when their niche is unrelated, and say for each what it would give this project (a type move, a hero object, a palette mood, a motion idea). With a thin library the shortfall is easily filled with utilitarian sites from the niche (evidence hubs, clinics, directories); they show the niche default, which is useful as a landscape note but not as a direction. [Our take]
10. Niche the library does not cover (fewer than three library sites with the project's industry tag): web references are required, not optional. See at least three sites from the niche in a browser and write the visual vocabulary they share (motifs, palette, shapes, materials, type): it is where the niche cue in explore-directions comes from. Skipping them to save time left a wedding page with nothing that said wedding.
11. Thin library: if the library holds fewer than 15 sites that fit (recommend and search_sites will tell you), fill the shortfall with web research (awards listings, competitor sites, the owner's likes) and mark those rows `not in library`. Open each one in a browser and look; do not list a site you did not view. Say in the file how many came from the library and how many from outside.
12. A text-only fetch (WebFetch, a page-to-text tool) is not looking: it returns a model's text summary of the page, not the design. Open the site in a browser or take a screenshot. A site you could only read as text may stay on the board only if its row says `read as text, not seen`, and it is not used for any visual decision (type, colour, layout, motion) and not counted as seen. Say in the file how many rows were seen and how many were read as text. [Our take]
13. For each reference record why it is here (one specific thing), what to take, what not to take. Read each site's audit failures before deciding what to take (get_site): do not copy what fails a blocker rule.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- brief is replaced by brief-draft.md (v1); an unreviewed brief is fine in lean.
- Lower the minimum to about 8 references (library plus web) from at least three art-style families, with some from adjacent niches. First-screen notes are enough: open each site, say what the first screen does, what to take, what not to take. Do not list a site you did not open; if a site fails to load or hides behind a cookie wall, say so and drop it.
- Audit column: write the get_site audit failures for library rows; write `UNKNOWN` for every `not in library` row and do not spend audits on them in lean. Do not copy anything from an UNKNOWN row that touches accessibility.
- Landscape: need-landscape is skipped, so put a five-line landscape note at the top of reference-board.md: (1) the niche's default look in one sentence, (2) the default hero, (3) the default skeleton, (4) what nobody does that this audience might want, (5) how many sites you looked at, from the library and from outside. explore-directions reads it as the landscape audit.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- brief is the reviewed brief.md here (brief-review runs on Day 1), so no replacement is needed for it.
- Thin-library minimum: when the library holds fewer than 15 sites that fit, about 8 references (library plus web) from at least three art-style families are enough, with some from adjacent niches, exactly as in lean. First-screen notes are enough: what the first screen does, what to take, what not to take. Audit column: the get_site failures for library rows, `UNKNOWN` for every `not in library` row; copy nothing from an UNKNOWN row that touches accessibility. ref-analyze then annotates the six or so you looked at most closely (get_site only works for library rows; for the rest annotate from your own first-screen notes).
- need-landscape is skipped, so put a five-line landscape note at the top of reference-board.md: (1) the niche's default look in one sentence, (2) the default hero, (3) the default skeleton, (4) what nobody does that this audience might want, (5) how many sites you saw, read as text, and took from the library. explore-directions reads it as the landscape audit.
## Ask the owner (only what you cannot default)
- (Taste intake, with the bundle sheet) Which style bundle fits this project? (a) bundle [n], my pick from the brief (recommended) (b) another bundle number, or a mix ("1's type with 3's colour") (c) none: say why.
- Any other sites to include or exclude? (a) no, the library is enough (recommended) (b) yes: name them.
## Tools
- `taste_intake`: gate 1: style bundles (`bundles`, 3 to 5) named after library sites, with feeling words, why and takes, plus the sites' screenshot paths, the question and the sketch plan
- `list_tags`: first: the canonical slugs for art-style, mood, industry and site-type
- `recommend`: brief text plus tag slugs, and `taste` (the owner's liked slugs); returns art direction and references; may include an unrelated niche, so check each
- `search_sites`: allOf by art-style/mood/type; passesBlockers true when you only want safe-to-copy references; call with {} to see the library size
- `find_similar`: slug of the strongest reference
## Output template
```markdown
# Reference board
Owner taste: bundle [n] ([slugs]), not for this project [slugs], why: [owner's words] (or: waiting for the owner)
Bundle sheet: design/03-references/bundles/directions-desktop.png, directions-mobile.png
(lean and sprint: five-line landscape note first: default look, default hero, default skeleton, gap nobody fills, counts of seen / read as text / from the library)
| Slug | Why it is here (one specific thing) | Take | Do not take (audit / taste) | Art style | Niche |
|---|---|---|---|---|---|
```
## Gates
Rules to satisfy: `distinct-swap-test` (read them with get_guidelines or rules/*.md).
- [ ] The board opens with an `Owner taste` line recorded from the owner's answer to the screenshots (or `waiting for the owner`, which blocks explore-directions).
- [ ] The library's most visually ambitious sites were looked at (images, not only briefs) and the board says what each would give this project.
- [ ] 15 or more references (library plus web research; lean and sprint with a thin library: about 8), at least three art-style families; the file states how many are from the library and how many were seen rather than read as text.
- [ ] Each reference has a specific reason, not 'looks good'.
- [ ] No reference with a known blocker failure is listed as something to copy in that respect.
## Done when
- The board has 15 or more references (lean, or sprint with a thin library: about 8) with take and do-not-take columns filled.
## Pitfalls
- Skipping the taste intake because the owner is away: ask anyway and wait at the directions sheet.
- Filling a thin library with the niche's plainest sites and calling it a reference set.
- Reading the text briefs of library sites without opening their screenshots.
- Only collecting direct competitors.
- Recording 'nice' instead of a reason.
- Retrying a niche query that returned nothing instead of checking the library size.
- Passing a whole brief sentence to search_sites or recommend and treating the fallback as a real match.
- Writing an audit result for a site you never audited: use UNKNOWN.
- Counting sites a text-only fetch summarised as if you had seen them.
