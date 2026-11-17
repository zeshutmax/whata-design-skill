# Step: Prepare imagery and assets (`realize-assets`, stage realize)
**Goal:** Produce or source images, icons, video and fonts with licenses and performance in mind.
**Your role:** Prepare images, video and fonts so they look right and load fast, with licenses and alt text sorted.
**Inputs:** homepage-design  
**Output artifact:** assets -> `design/06-realize/assets.md`
## Procedure
1. List each asset: purpose, source, license, format, size, responsive variants. Prefer modern formats; set width and height; never lazy-load the likely LCP image; give it fetchpriority high. [Standard + Craft]
2. A creator's own videos and photos often contain other people (photos pinned on a board, a friend in frame, a screenshot of a follower). Rules about consent for photographs of people cover strangers; here, choose frames or crops that show only the person who owns the page, by eye, because automated frame selection does not see the others. Note each exception in the asset list.
3. Graphics made in code: for each section, decide the graphic with plan_graphics (pass the sections and tokens.css). Draw data graphs and diagrams as SVG or HTML from the real content in the project's tokens (colour roles, type scale, one stroke width), give each a text equivalent (the numbers as text or a table, the steps as a list) and check every stroke and label with check_contrast (ui 3:1, text 4.5:1). A number still marked `.assumed` stays marked inside the graph. A graph or diagram encodes content and is allowed; a scene, product, person or place drawn from shapes is not (`distinct-real-imagery-and-icons`). If the audit's detector flags a data graph as a shape-built scene, record it as a false positive with the data source. No approval needed. [Our take]
4. Paid image generation (Gemini or any paid model): only after the owner's explicit yes for the batch. Ask with the prompt, the number of images, the placement of each and the model, with a marked placeholder already in the page; record tool, model, prompt, date, the owner's yes and the licence terms in assets.md. No yes, no call; owner away, the placeholder stays and the request goes into OPEN-QUESTIONS.md.
5. Write alt text for each informative image (what it conveys, not 'image of'); mark decorative images with empty alt. Provide posters for videos.
6. Fonts: self-host or a documented provider, subset, WOFF2, font-display chosen deliberately; check the license. Concept pages (explore-hero) may link a font from a provider to look right; the build must not: self-host it (build-time self-hosting such as `next/font/google` counts) and remove the provider link.
7. Set the page weight budget and record it.
## Ask the owner (only what you cannot default)
- Who supplies photographs? (a) graphics made in code now, real photographs marked as a gap for later (recommended) (b) you send photographs or licences.
- (Only when proposing paid generation) May I generate [n] images with [model]? (a) no, keep the placeholders and code-made graphics (recommended unless the page needs a picture) (b) yes, this batch: prompt, placement and placeholder attached.
## Tools
- `plan_graphics`: sections and tokens; proposes a graphic kind per section (data graph, diagram, type as image, code SVG motif, live object, photograph) and drafts the approval request for paid generation
- `check_contrast`: strokes and labels of every graphic
## Output template
```markdown
# Assets
| Asset | Purpose | Source and license | Format and size | Alt text | LCP candidate |
|---|---|---|---|---|---|
## Graphics made in code (section, kind, data source, text equivalent, contrast checked)
## Generated images (tool, model, prompt, date, owner's yes, licence)
## Fonts (family, license, subset, font-display)
## Page weight budget
```
## Gates
Rules to satisfy: `a11y-alt-text`, `craft-image-dimensions-reserved`, `craft-image-no-distortion`, `copy-alt-text-writing`, `distinct-real-imagery-and-icons`, `perf-lcp`, `perf-cls` (read them with get_guidelines or rules/*.md).
- [ ] Every image has alt text or is marked decorative.
- [ ] The LCP image is identified and not lazy-loaded.
## Done when
- All assets are listed with license, format and alt text.
## Pitfalls
- Unlicensed images.
- Lazy-loading the hero image.
