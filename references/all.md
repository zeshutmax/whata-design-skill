# whata.design agent design guide

# whata.design agent design guide: operating protocol

You are a designer-engineer working for an owner who decides. This guide takes a request such as "design and build the homepage for X" from need to launch, producing homepages that are accessible, usable, distinctive and as good as the library's best sites. It is built from a process (39 steps), a Quality Bar of testable rules, recipes that keep stylish looks within those rules, an audited base kit, and a library of reference sites you can query. Everything is local.

## 1. How to use this guide
- Read this file first. Load other files only when a step needs them: `steps/<step>.md` for the step you are on, `rules/*.md` for rules, `recipes/<slug>.md` for a style, `principles.md`, `taxonomy.md`, `trends.md`.
- If the MCP server is connected, prefer its tools (section 7). If not, read the same files from `dist/`.
- Work in the owner's project. Keep all artifacts in a `design/` folder, one file per artifact, named as the step says.

## 2. The process
Seven stages, in order, with loops back when evidence demands it:
**Need > Brief > References > Explore > Decide > Realize > Reflect.**
- Each step has inputs, a procedure, an output file, gates (rules and checks) and a definition of done. Do not start a step whose inputs are missing; produce or ask for them.
- The brief is a versioned hypothesis: when exploring changes how the problem is understood, revise it, record why, and re-check what depends on it. Loops: explore > brief, decide > explore, realize > decide, reflect > need.
- Tracks (pick one with the owner at the start): **sections** (the default since 2026-11-16: need-goal, brief-write, explore-sections, realize-build, realize-qa. The page is assembled from finished, spec-pinned library sections (`list_library_sections`, `get_library_section`) and changed only in their adaptation slots; the rules and audits are checks on the result, not its source. a client pilot: owner 9/10 against 5 to 7.5 for rule-driven rounds), **full** (all steps), **sprint** (five days: Map, Sketch, Decide, Prototype, Test; then realize-build and realize-qa), **lean** (one day: need-goal, need-jobs, brief-write, brief-success, ref-gather, explore-directions, explore-copy, explore-hero, decide-inclusive, decide-choose, decide-tokens, realize-build, realize-qa). When you skip a step, write one line saying what you skipped and the risk.
- **Short tracks fold skipped steps into the artifacts they do produce.** Each affected step file has a `Sections track`, `Lean track` or `Sprint track` section saying what replaces which input (`get_process` lists them as `replaces`; `get_step` with `track` shows only your track). The lean and sprint tracks keep the two taste gates (section 4); the sections track has one, the owner's pick of sections in explore-sections, made from a sheet beside the sources.
- **Sprint days.** The day-to-step table, from `taxonomy/process.json`:

| Day | Name | Steps |
|---|---|---|
| 1 | Map | `need-goal`, `need-audience`, `need-jobs`, `brief-write`, `brief-success`, `brief-review` |
| 2 | Sketch | `ref-gather`, `ref-analyze`, `ref-principles`, `explore-sketch`, `explore-directions` |
| 3 | Decide | `explore-copy`, `explore-hero`, `decide-critique`, `decide-inclusive` |
| 4 | Prototype | `decide-prototype` |
| 5 | Test | `decide-test`, `decide-choose`, `decide-tokens` |
| after day 5 | Build and QA | `realize-build`, `realize-subtract`, `realize-sweep`, `realize-qa` |


  - Day 3 "Decide" holds the critique and the inclusion check; `decide-choose` records the owner's pick. Day 5 with no people to test with: write the script, record `UNTESTED`, and say the decision is untested. realize-build and realize-qa follow Day 5 and are not optional; realize-launch is not part of the sprint.
  - Read a step file when you start that step, never all up front; `rules/blockers.md` once at the start and `rules/build.md` once before building; skip `taxonomy.md` (use `list_tags`) and `all.md`.
- **Start from the base kit.** Every sketch, concept and build starts from the audited base kit (`get_base`, `content/kit/`): header with a real mobile menu, hero skeletons (including a full-bleed backdrop), section types, a form with its states and a footer, all driven by the project's tokens. Add only the lead idea on top. Before the owner sees anything, `pnpm --silent --filter @whata/audit cli widths <file>` says ok at 320, 390, 768, 1440 and 320 at 200% text.
- **Build once.** The prototype is the first draft of the build: make it where the site will live, from the chosen direction's tokens and real copy, and let the later steps refine it; do not rebuild from scratch.

## 3. Honesty rules (non-negotiable)
1. **Evidence labels.** Every recommendation is [Standard] a published requirement, [Evidence] backed by a study, [Craft] widely taught practice, or [Our take] judgement. Keep the label when you repeat it; never present judgement as a requirement.
2. **No invented facts.** Do not make up customers, numbers, testimonials, quotes, awards or results. If it is not given, ask or mark it.
   - **Unconfirmed facts on a page** (a price, an opening hour, an address): never in brackets, never shown as confirmed. Mark each with the visible `.assumed` marker and one legend on the page (the `<Assumed>` pattern in `rules/build.md`, which also covers links and screen readers), and list it in `design/OPEN-QUESTIONS.md`. realize-launch refuses while any remains. Invented customers, numbers, quotes and press are left out, not marked. [Our take]
   - **Named people and credentials** are facts: show a reviewer, author or expert only if the person exists and can be reached; a placeholder id or a dead profile is left out and listed as an open question.
   - **Status taken from history** (a count from git commits or old notes) is an assumption until the owner confirms it: mark it.
   - **Existing content is the owner's.** In a redesign, keep what the scope (need-goal) keeps, flag problems you find in OPEN-QUESTIONS.md, and add no claims of your own.
   - **What the page sends people to:** a homepage inherits the claims of the pages its primary action leads to; check the main three.
3. **Automated is not accessible.** A pass from `review_design` means no automated failure was found. Say what still needs a person.
4. **Never claim user testing you did not run.** Plan the test, ask the owner to run it, record real answers; label any model review as such.
5. **Cite rule ids** when you fix or accept something ("fails `a11y-contrast-text`").
6. **Read the audit before copying a reference.** A reference's accessibility failures are not part of its style.

## 4. Asking the owner
- Ask only when a decision is the owner's (taste, brand, budget, approvals) or a fact is missing and cannot be defaulted. Batch questions in one message. Every question proposes answers as letters, the recommended one first, with your own draft filled in, so the owner can reply "a, a, b"; a bare open question is not allowed.
- Steps that need the owner: need-alignment, brief-review, **ref-gather (gate 1, taste intake)**, **explore-directions (gate 2, directions sheet)**, decide-test, decide-choose, realize-assets (paid images), realize-build (stack), realize-launch.
- **Taste is the owner's, decided from pictures.** Make the choice cheap and well informed, then wait. Two gates, no more: (1) taste intake at the start of ref-gather: style bundles from the library with a quick hero sketch each (`taste_intake`); (2) the directions sheet: safe, stretch and wildcard concepts side by side at both sizes (`propose_directions`, `render_sheet`). Your own scoring is advice, never the decision.
- **Two kinds of taste.** The library is the curator's taste: every site in it is good, the quiet ones too, so it is the quality bar, never rated, and none of it is the "safe default". What you learn is the project owner's (the client's) taste: record what they say with `record_taste` and the project folder, and pass the project to `taste_intake`, `propose_directions` and `recommend` so their profile, or earlier clients in the same niche, picks your recommended answer. It never replaces the question. A client new to choosing from screenshots can start with 8 to 10 A-vs-B pairs (`taste_pairs`).
- **Owner away at a taste gate: stop.** Finish the sheet, make the pick the one blocking question in OPEN-QUESTIONS.md, and build nothing in the site tree (no tokens, no prototype) until `Owner pick:` is recorded. Work that does not depend on the pick may continue. A label such as `ASSUMED` does not make a taste guess safe: in a real run the model picked the safest direction, built it, and the owner's verdict was "really boring".
- **Owner away, any other decision: do not stop.** Write each question with your default, proceed, and mark what depends on it `ASSUMED, not owner-approved`; collect the questions in `design/OPEN-QUESTIONS.md`. Never write "approved", "confirmed" or "tested" for what the owner or a test did not do; results that need people stay `UNTESTED`.

## 5. The Quality Bar
- Severities: **blocker** (never traded for style; zero before anything is done), **major** (fixed, or accepted by the owner in writing), **minor** and **advisory** (triaged).
- **Style does not exempt a design.** Each style has a recipe that keeps its look and passes the rules: call `get_recipe` for any direction using dark, neon, glass, pastel, minimal, 3D, video, ambient loops, marquees, scroll stories, parallax, preloaders, unusual navigation, horizontal scroll, expressive type or theme switching.
- Build with the rules' hints in mind (`rules/build.md`: every blocker and major, the COGA rules and shared patterns) and run `review_design` often.
- **Audience-driven escalation.** If the audience includes people under stress, with low literacy, reading in a second language, with cognitive or learning disabilities, or screen-reader or dyslexia users, the 15 `a11y-coga-*` rules are major for this project and the brief says so. [Our take]
- **High-stakes advice** (legal, medical, financial, safety) needs a qualified reviewer before launch (`copy-expert-review-before-launch`); until then it carries the draft marker. Urgent help: recipe `urgent-help-route`; forms with no backend: `form-no-backend-and-privacy`. [Our take]
- Conflicting rules: the higher severity wins; if equal, ask the owner and record the choice. Known tensions and how to handle them are in `rules/build.md`.

## 6. Distinctiveness and craft
Generic is a design choice made by default. Avoid it deliberately:
- Run the **swap test**: put a competitor's name in; if the headline and layout still fit, rewrite. Every default you keep (a common font, a hue, a card grid) needs a written reason; choose from the brief, not from a list of bans.
- Every direction has a **lead element** the niche's default page lacks (a hero object, layout idea, type move or interaction; `get_moves` lists recurring ones with library examples). It sits above the fold, recurs lower on the page, and the sections below the hero differ in structure. [Our take]
- **The studio method (from the owner's awwwards skill, `get_studio`).** A page earns a point of view: one concept from the subject's own world, tied to an anchor fact, so it could not be moved to another brand. It has one signature moment executed perfectly and everything around it quiet; every static frame reads as a poster; motion runs on one clock in one motion verb, with an idle state and designed reduced-motion and no-JS versions; each section uses a different layout family. Library styles give the art direction for the concept; they are not the concept. The two are not optional halves: the concept without the library's visual language reads as dated (a client pilot: a loved stationery concept in beige paper and centred serif scored 7.5, "feels a bit obsolete ... not inspired by any of the designs in the library"); the library's look without a concept reads as a template. The final check is a fresh critic who sees only screenshots and scores Design, Usability, Creativity and Content 8 or above (`get_critic_brief`), on top of the audits.
- **Presence of style, not only absence of slop.** The library's heroes have strong scale contrast and a lead object that fills most of the first screen. Check concepts with `compare_to_library` against their anchors and side by side with their screenshots before the owner sees them. [Our take]
- **Graphics in the site's own style** (data graphs, diagrams, type as image, SVG motifs and backdrops drawn in code from real content and tokens) need no approval. A product, person, place or scene assembled from shapes is still out (`distinct-real-imagery-and-icons`). `plan_graphics` proposes a kind per section. [Our take]
- **Paid image generation needs the owner's yes per batch**: show prompt, count, placement, model and a marked placeholder first; record tool, prompt, date, the yes and the licence in assets.md.
- Trends (`trends.md`) are tools for a message, with a dated status: one as the lead, not five as decoration.

## 7. Tools (MCP)
- **Process and rules:** `get_process`, `get_step`, `get_guidelines`, `get_recipe` (at most 3 real tag slugs per call), `get_principles`, `get_trends`, `check_contrast` (set `role` per pair: `text` 4.5:1, `large-text` or `ui` 3:1).
- **Library:** `list_tags` first (pass slugs, not sentences), `search_sites` (`{}` returns the library size), `get_site`, `get_design_brief`, `get_sections`, `get_section`, `get_design_system`, `find_similar`, `find_by_color`, `compare`, `recommend`, `get_build_prompt`, `get_craft`, `get_moves`.
- **Studio method:** `get_studio(topic?, section?)` (concepts, art-direction, typography, layout, motion, engine, nextjs, astro, webgl, patterns, content, quality, quality-bar), `get_critic_brief`.
- **Gates and taste:** `taste_intake`, `propose_directions`, `render_sheet`, `record_taste`, `taste_pairs`, `get_taste_profile`.
- **Making and checking:** `get_base`, `get_backdrop`, `plan_graphics`, `review_design`, `compare_to_library`; audit CLI commands `widths`, `types` (one style per role), `shot`, `sheet`, `coverage`.
- No MCP connection: `pnpm --silent --filter @whata/mcp call <tool> '<json args>'` (`--list` shows the names) and `pnpm --silent --filter @whata/audit cli <url|file>`. Use `--silent` so the output pipes cleanly, give local files as absolute paths, and check that the page actually loaded before you trust a report.

## 8. Definition of done (whole project)
- All gates of the executed steps are met; skipped steps are noted.
- Zero blocker failures from `review_design` on the live build, desktop and mobile; manual checks done and recorded.
- A fresh critic, from screenshots of a production build only, scores every category 8 or above (`get_critic_brief`); the scores are recorded as a model's, not the owner's.
- The owner confirmed the brief and picked the direction from the sheet.
- Artifacts are in `design/`; tokens and DESIGN.md match the build.
- The finished site is added to the library (reflect-archive) only after the owner signed it off.
- Without owner sign-off, tests or archive the work is **built, audited, not approved**: list what was not done (approval, user tests, screen-reader pass, real devices, archive, open facts). Never write "approved", "tested" or "launched" for any of these.

## 9. When something goes wrong
- A tool is missing or fails: say so, then use the files in `dist/` or `content/learn/` directly.
- You disagree with a rule: apply it anyway and write the disagreement in the retro notes so the rule can be corrected.
- The owner's request conflicts with a blocker rule: explain, offer the closest compliant option, and record the decision.


---

# Process map
### Need (`need`): What problem are we solving, for whom, under which limits?
- `need-goal`: Define the need and the goal. Needs: nothing. Produces: need-statement.
- `need-audience`: Understand the audience. Needs: need-statement. Produces: audience-profile.
- `need-jobs`: Frame the job to be done. Needs: need-statement, audience-profile. Produces: job-story.
- `need-constraints`: List the constraints. Needs: need-statement. Produces: constraints.
- `need-landscape`: Audit the landscape. Needs: need-statement, audience-profile. Produces: landscape-audit.
- `need-alignment`: Align with stakeholders. Needs: need-statement, audience-profile, constraints, landscape-audit. Produces: kickoff-notes.

### Brief (`brief`): What exactly are we making, and how will we judge it?
- `brief-write`: Write the brief. Needs: need-statement, audience-profile, job-story, constraints, kickoff-notes. Produces: brief-draft.
- `brief-positioning`: Set positioning and tone. Needs: brief-draft, landscape-audit. Produces: positioning.
- `brief-content`: Plan the content and page goal. Needs: brief-draft, positioning. Produces: content-inventory.
- `brief-success`: Define success criteria. Needs: need-statement. Produces: success-criteria.
- `brief-review`: Review and sign off. Needs: brief-draft, positioning, content-inventory, success-criteria. Produces: brief.

### References (`references`): What already exists that points the way?
- `ref-gather`: Gather references. Needs: brief. Produces: reference-board.
- `ref-analyze`: Analyze references. Needs: reference-board. Produces: reference-notes.
- `ref-principles`: Write design principles. Needs: brief, reference-notes. Produces: design-principles.

### Explore (`explore`): What are the genuinely different ways to do this?
- `explore-sections`: Pick library sections. Needs: brief-draft. Produces: section-pick.
- `explore-sketch`: Sketch many ideas. Needs: brief, design-principles, reference-notes. Produces: idea-sketches.
- `explore-directions`: Frame three directions. Needs: brief, design-principles, reference-board, idea-sketches. Produces: direction-matrix.
- `explore-type-color`: Explore type and color. Needs: direction-matrix. Produces: type-color-studies.
- `explore-structure`: Explore structure. Needs: brief, content-inventory, direction-matrix. Produces: structure-wireframes.
- `explore-copy`: Draft headlines and copy. Needs: brief, positioning. Produces: headline-drafts.
- `explore-hero`: Design hero concepts. Needs: direction-matrix, type-color-studies, structure-wireframes, headline-drafts. Produces: hero-concepts.
- `explore-motion`: Explore motion and interaction. Needs: direction-matrix. Produces: motion-notes.

### Decide (`decide`): Which direction, and why?
- `decide-critique`: Critique against the brief. Needs: hero-concepts, design-principles, success-criteria. Produces: critique-notes.
- `decide-inclusive`: Check inclusion and accessibility early. Needs: hero-concepts, type-color-studies, motion-notes. Produces: inclusion-check.
- `decide-prototype`: Prototype the strongest candidates. Needs: hero-concepts, critique-notes, headline-drafts, structure-wireframes. Produces: prototype.
- `decide-test`: Test quickly. Needs: prototype, critique-notes, success-criteria. Produces: test-results.
- `decide-choose`: Choose and document. Needs: critique-notes, inclusion-check, test-results, success-criteria. Produces: direction-decision.
- `decide-tokens`: Define the tokens. Needs: direction-decision, type-color-studies. Produces: design-tokens.

### Realize (`realize`): How do we turn the chosen direction into a real page?
- `realize-design`: Design the homepage in full. Needs: direction-decision, design-tokens, structure-wireframes, content-inventory, headline-drafts. Produces: homepage-design.
- `realize-components`: Build the component set. Needs: design-tokens, homepage-design. Produces: component-set.
- `realize-motion`: Specify motion. Needs: homepage-design, motion-notes. Produces: motion-spec.
- `realize-assets`: Prepare imagery and assets. Needs: homepage-design. Produces: assets.
- `realize-build`: Build it. Needs: homepage-design, component-set, motion-spec, assets, design-tokens. Produces: built-site.
- `realize-subtract`: Remove what the build does not need. Needs: built-site, design-tokens. Produces: subtract-log.
- `realize-sweep`: Look at every state and keep a papercut log. Needs: built-site, subtract-log. Produces: state-sweep, papercut-log.
- `realize-qa`: Check accessibility, performance and SEO. Needs: built-site, success-criteria. Produces: qa-report.
- `realize-launch`: Hand off and launch. Needs: built-site, qa-report. Produces: launched-site.

### Reflect (`reflect`): Did it work, and what do we keep?
- `reflect-measure`: Measure. Needs: launched-site, success-criteria. Produces: metrics-report.
- `reflect-iterate`: Iterate and run a retro. Needs: metrics-report, qa-report, papercut-log. Produces: retro-notes.
- `reflect-archive`: Archive as a case study. Needs: launched-site, direction-decision, retro-notes. Produces: case-study.

## Loops
- explore > brief: Exploring solutions changes how the problem is understood. Treat the brief as a versioned hypothesis, not a contract.
- decide > explore: If no direction passes critique and tests, return to exploration with what you learned.
- realize > decide: Build and QA findings can force changes to the direction or the tokens.
- reflect > need: Results reframe the need. Digital work is never finished.

## Sections track (default): what replaces a skipped input
Steps: need-goal, brief-write, explore-sections, realize-build, realize-qa. Inputs not listed here are produced by an earlier sections step.
- `brief-write`: audience-profile -> need-statement; job-story -> need-statement; constraints -> need-statement; kickoff-notes -> need-statement
- `realize-build`: homepage-design -> section-pick; component-set -> section-pick; motion-spec -> section-pick; assets -> section-pick; design-tokens -> section-pick
- `realize-qa`: success-criteria -> brief-draft

## Lean track: what replaces a skipped input
Steps: need-goal, need-jobs, brief-write, brief-success, ref-gather, explore-directions, explore-copy, explore-hero, decide-inclusive, decide-choose, decide-tokens, realize-build, realize-qa. Inputs not listed here are produced by an earlier lean step.
- `need-jobs`: audience-profile -> need-statement
- `brief-write`: audience-profile -> need-statement; constraints -> need-statement; kickoff-notes -> need-statement
- `ref-gather`: brief -> brief-draft
- `explore-directions`: brief -> brief-draft; design-principles -> brief-draft; idea-sketches -> direction-matrix
- `explore-copy`: brief -> brief-draft; positioning -> brief-draft
- `explore-hero`: type-color-studies -> direction-matrix; structure-wireframes -> direction-matrix
- `decide-inclusive`: type-color-studies -> direction-matrix; motion-notes -> hero-concepts
- `decide-choose`: critique-notes -> hero-concepts; test-results -> dropped
- `decide-tokens`: type-color-studies -> direction-matrix + hero-concepts
- `realize-build`: homepage-design -> direction-decision + headline-drafts + hero-concepts; component-set -> design-tokens; motion-spec -> hero-concepts; assets -> built-site

## Sprint track: what replaces a skipped input
Steps: need-goal, need-audience, need-jobs, brief-write, brief-success, brief-review, ref-gather, ref-analyze, ref-principles, explore-sketch, explore-directions, explore-copy, explore-hero, decide-critique, decide-inclusive, decide-prototype, decide-test, decide-choose, decide-tokens, realize-build, realize-subtract, realize-sweep, realize-qa. Inputs not listed here are produced by an earlier sprint step.
- `brief-write`: constraints -> need-statement; kickoff-notes -> need-statement
- `brief-review`: positioning -> brief-draft; content-inventory -> brief-draft
- `explore-copy`: positioning -> brief-draft
- `explore-hero`: type-color-studies -> direction-matrix; structure-wireframes -> direction-matrix
- `decide-inclusive`: type-color-studies -> direction-matrix; motion-notes -> hero-concepts
- `decide-prototype`: structure-wireframes -> direction-matrix + brief-draft
- `decide-tokens`: type-color-studies -> direction-matrix + hero-concepts
- `realize-build`: homepage-design -> direction-decision + headline-drafts + hero-concepts + prototype; component-set -> design-tokens; motion-spec -> hero-concepts; assets -> built-site

# Files
- `steps/<slug>.md` (40), `rules/{blockers,build,accessibility,usability,craft,copy,components,distinct}.md`, `recipes/<slug>.md` and `recipes/index.md`, `principles.md`, `taxonomy.md`, `trends.md`, `all.md` (everything in one file), `guide.json` (structured data for tools).

# Rule groups
- accessibility: 51 rules
- components: 59 rules
- copy: 36 rules
- craft: 41 rules
- distinct: 25 rules
- usability: 30 rules



# STEPS

# Step: Define the need and the goal (`need-goal`, stage need)
**Goal:** State the business goal, the visitor goal and how success will be recognized.
**Your role:** Pin down what the homepage is for before any design thinking. You are framing a problem, not proposing a solution.
**Inputs:** none  
**Output artifact:** need-statement -> `design/01-need/need-statement.md`
## Procedure
1. Redesigning an existing site? Before you restate anything or ask the owner a question, read what exists (the code, the content, the analytics events) and write down what the site actually does today and which action it really serves. A brief can describe a site that does not exist: a first test found a request for a 'booking site' on a site with no booking at all, whose real action was 'follow'. Where the request and the code disagree, say so and let the code set the primary action unless the owner decides otherwise.
2. Redesigning an existing site? Ask the scope once, first, as the first ask_user question (three multiple-choice lines with the recommended answer first) and write the answer as a `## Scope` block at the top of need-statement.md; every later step reads it. Structure: rebuild from scratch, or keep the current sections. Content: rework key parts (the hero and 2 or 3 key sections; everything else is kept and moved into the new sections), keep verbatim, full rework, or none supplied (you write draft copy marked unconfirmed). SEO: keep URL, title, meta description, canonical, structured data, heading text and internal links, or free to change. For a "make it stylish" job on an existing site the recommended answer is rebuild, rework key parts, keep SEO: the owner's own words were "from scratch ... respect the content, but not the structure ... repurpose the content across the new sections ... keep it for SEO". Owner away: use the recommended answers, mark the block `ASSUMED, not owner-approved`, and list it in OPEN-QUESTIONS.md.
3. Existing content with a scope that keeps any of it: write design/01-need/content-map.md before designing: every text block of the current page (heading, paragraph, list, button, FAQ item) with an id, marked `SEO` when it is the title, meta description, h1 or h2 text, structured data or an internal link; the new section it moves into; and `keep`, `rework` or `drop (owner)`. Nothing is dropped without the owner's word. realize-qa checks the build against it with the audit's `coverage` command.
4. Outside the scope's rework parts the content is the owner's. Content problems you find (unsourced claims, odd copy, missing sections) are findings for the owner, listed in OPEN-QUESTIONS.md and the QA report; do not fix, remove or rewrite them yourself, and do not add claims of your own. In a test the first build rewrote copy outside its scope and dropped sections, and had to be reverted. Also ask whether the done bar may touch shared chrome (header, footer, shared components): it moves the work from one file to many.
5. Open the pages the primary action sends people to (the three main destinations) and check their claims and sources too: a homepage inherits their honesty. In a real run the homepage's own claims were fixable, but 99 of the 124 pages its main action led to might still cite fabricated papers, and the repo's own commit messages said so. Check also the people the content names as authors or reviewers: a name, title or credential is shown only if the person exists and can be reached (protocol 3.2). Read the git log for words such as `fabricated`, `placeholder`, `fake`, `TODO` and `unverified`.
6. Restate the user's request in one sentence without solution words (no 'with a video', 'in dark mode').
7. Write the business goal, the visitor goal and ONE primary action the page asks for (a single verb phrase: buy, book a demo, join the waitlist...). [Craft]
8. Define how success will be recognized: at least one measurable signal (a rate, a count, a task success) and one observable signal (a five-second test result, a stakeholder reaction).
9. No baseline? Do not invent one. Set a relative target (for example `+X% against the first four weeks after launch`, or `more enquiries per 100 visits than the old page`) and name the measure, or write the absolute number and mark it `ASSUMED, no baseline`. Record the missing baseline as an open question: a target with no baseline is a hypothesis, not a result. [Our take]
10. The owner names two actions ('book or buy')? Pick the one with the higher value or the higher frequency as the primary action, name the other as a secondary action, and record the call and the reason as an open question for the owner. Do not write both as primary. If you cannot tell which is more valuable, default to the more frequent one and mark it ASSUMED. [Our take]
11. List what is unknown. Mark every statement that is an assumption, not a fact the user gave you.
12. Stop. Do not start designing. Hand the unknowns to the next steps or ask the user.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- Need-audience, need-constraints and need-alignment are skipped, so this file carries them. Add three short sections to need-statement.md after the assumptions: `## Audience` (who arrives, in what situation, on which device, what could stop them, access needs; each claim tagged evidence or assumption; plus the audience flags and COGA escalation from need-audience), `## Constraints` (brand assets, stack, deadline, content that exists, legal, must-not, accessibility WCAG 2.2 AA and performance defaults, and which shared components render on the page and whether you may change them: header, footer, global styles) and `## Owner's words` (three feeling adjectives, sites liked and disliked; if the owner is unavailable, write your defaults and mark them `ASSUMED, not owner-approved`).
- Keep each section to five lines or fewer. A fact you do not have is an open question in design/OPEN-QUESTIONS.md, not a reason to stop.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- need-constraints and need-alignment are skipped in the sprint, so this file carries them. need-audience is not skipped: the audience keeps its own file. After the assumptions add two short sections to need-statement.md: `## Constraints` (brand assets, stack, deadline, content that exists, legal, must-not, accessibility WCAG 2.2 AA and performance defaults, and which shared components render on the page and whether you may change them: header, footer, global styles) and `## Owner's words` (three feeling adjectives, sites liked and disliked; if the owner is unavailable on Day 1, write your defaults and mark them `ASSUMED, not owner-approved`). brief-write reads them from there.
- Keep each section to five lines or fewer. A fact you do not have is an open question in design/OPEN-QUESTIONS.md, not a reason to stop. Day 1 is the best time to ask the owner: batch the questions in one message with a default for each.
## Ask the owner (only what you cannot default)
- Scope (redesign of an existing site; one letter per line, recommended first). Structure: (a) rebuild from scratch (recommended) (b) keep the current sections and order. Content: (a) rework key parts: hero plus 2 or 3 key sections, the rest kept and moved into the new sections (recommended) (b) keep every text verbatim (c) full rework (d) none supplied: I write draft copy marked unconfirmed. SEO: (a) keep URL, title, meta description, canonical, structured data, heading text and internal links (recommended) (b) free to change.
- What does the company or product do, in one sentence? (a) my draft from the current site: [one sentence] (recommended) (b) your own sentence.
- Who should use the page, and what should they do on it? (a) my reading of the site: [audience] should [primary action] (recommended) (b) a different audience or action: say which.
- How will you know the homepage worked? (a) more [primary action] per 100 visits than the first four weeks after launch (recommended) (b) a number you already track: say which.
## Output template
```markdown
# Need statement
## Scope (asked first; owner's answer or ASSUMED)
- Structure: rebuild | keep
- Content: rework key parts [which] | keep verbatim | full rework | none supplied
- SEO: keep (URL, title, meta description, canonical, structured data, headings, internal links) | free
- Request (no solution words):
- Business goal:
- Visitor goal:
- Primary action (one verb phrase):
- Secondary action (if the owner named two, say which is primary and why; record as open question):
- Success, measurable (relative target if there is no baseline, or ASSUMED):
- Success, observable:
- Out of scope:
## Assumptions (mark each; replace with evidence when you get it)
- [assumption]
```
## Gates
Rules to satisfy: `ux-start-with-needs` (read them with get_guidelines or rules/*.md).
- [ ] The primary action is a single verb phrase.
- [ ] At least one measurable success signal is stated.
- [ ] No sentence in the need statement describes a visual or a feature.
## Done when
- Every field is filled or explicitly marked unknown.
- Assumptions are listed separately from facts.
## Pitfalls
- Writing the solution into the need ('a homepage with a hero video').
- Two or three primary actions: pick one, move the rest to secondary and record the choice as an open question when the owner named both.
- A success target with an invented baseline: use a relative target or mark it ASSUMED.

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

# Step: Frame the job to be done (`need-jobs`, stage need)
**Goal:** Write the job story: the situation, the motivation and the progress the visitor wants to make.
**Your role:** Describe what each visitor is trying to get done, in their words, without naming a product or feature.
**Inputs:** need-statement, audience-profile  
**Output artifact:** job-story -> `design/01-need/job-story.md`
## Procedure
1. For each audience group write one to three job stories: 'When [situation], I want to [motivation], so I can [outcome].' [Craft: the job-story format comes from Intercom's practitioners, not from Christensen, Moesta or Ulwick, whose definitions of a job differ; treat the format as a convenience]
2. A job statement must not contain a solution (no product, page type or feature). Rewrite until it does not.
3. Rank the jobs by how often they occur and how costly failure is. The top job drives the primary action.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- audience-profile is replaced by the Audience section of need-statement.md. Write one to three job stories from it and rank them; the top one must match the primary action.
## Output template
```markdown
# Job stories
1. When [situation], I want to [motivation], so I can [outcome].
   - Group:
   - Frequency / stakes:
```
## Gates
- [ ] No job story names a feature or a page.
- [ ] Top job is consistent with the primary action in the need statement.
## Done when
- Each group has at least one ranked job story.
## Pitfalls
- Smuggling the solution into the job ('I want a dashboard').

# Step: List the constraints (`need-constraints`, stage need)
**Goal:** Capture brand assets, budget, deadline, platform, content, legal and accessibility limits.
**Your role:** Record everything that limits the design so later steps treat limits as inputs, not surprises.
**Inputs:** need-statement  
**Output artifact:** constraints -> `design/01-need/constraints.md`
## Procedure
1. Ask for or find: brand assets (logo, colors, fonts, voice), existing site and its analytics, stack and hosting, CMS, deadline and budget, content that exists, legal needs (cookie consent, claims, regulated language), languages.
2. Set defaults unless the user says otherwise and write them down: accessibility target WCAG 2.2 Level AA [Standard]; Core Web Vitals targets LCP at most 2.5 s, INP at most 200 ms, CLS at most 0.1 at the 75th percentile [Standard]; support the current evergreen browsers and common mobile sizes (320 to 1920 px wide).
3. List explicit 'must not' items (words, colors, competitors' looks, technologies).
4. Shared chrome: list the shared components that render on this page (header, footer, navigation, cookie banner, region or language switcher, global tokens and base styles) and ask whether you may change them. The homepage's done bar (zero blockers) often cannot be met without them: in a real run the failures were a low-contrast button in the footer, 12 to 14 px footer text, an icon-only switcher with no name and a light input border token, all shared. Record the answer as `Shared chrome: may change [list] / must not change [list]`, and in realize-qa report their failures as inherited, not new.
## Ask the owner (only what you cannot default)
- Brand assets I must use? (a) the logo, colours and fonts on the current site (recommended) (b) new or different ones: send them.
- Stack and deadline? (a) the current project's stack, no fixed deadline (recommended) (b) another stack or a date: say which.
- Anything the page must not say or look like? (a) nothing beyond the brief's anti-goals (recommended) (b) yes: list it.
- May I change the shared header, footer and global styles to fix problems on this page? (a) yes, and I audit one inner page too (recommended) (b) no, this page only.
## Output template
```markdown
# Constraints
- Brand assets:
- Stack / platform / hosting:
- Deadline and budget:
- Content available:
- Legal / compliance:
- Languages:
- Accessibility target: WCAG 2.2 AA (default)
- Performance targets: LCP <= 2.5 s, INP <= 200 ms, CLS <= 0.1 (default)
- Must not:
- Shared chrome (header, footer, nav, switchers, global tokens): may change [list] / must not change [list]
```
## Gates
Rules to satisfy: `perf-lcp`, `perf-inp`, `perf-cls` (read them with get_guidelines or rules/*.md).
- [ ] Accessibility and performance targets are written down, even if they are the defaults.
## Done when
- Brand, stack, time, content, legal, accessibility, performance and shared-chrome lines are all present.
## Pitfalls
- Leaving accessibility and performance unstated so they become optional.

# Step: Audit the landscape (`need-landscape`, stage need)
**Goal:** Look at how comparable companies present themselves, and what is overused in the niche.
**Your role:** See how comparable companies present themselves, and what the niche has made generic.
**Inputs:** need-statement, audience-profile  
**Output artifact:** landscape-audit -> `design/01-need/landscape-audit.md`
## Procedure
1. Query the library: search_sites with the industry and site-type tags that fit the need; also one or two adjacent industries.
2. Review at least 6 sites. If the library has fewer than 6 that fit the industry, add sites found on the web (open and view each) and mark them `not in library`. For each note the art style, hero type, page skeleton, how the primary action is presented, and anything the audit says not to copy (get_site returns audit failures).
3. Name the niche's default look in one sentence ('white, blue gradient, three icon cards'). That is what to avoid being indistinguishable from, unless the brief says otherwise. [Our take]
4. Note what nobody does that the audience might want.
## Tools
- `search_sites`: allOf: [industry slug, site-type slug]; status any; limit 20
- `get_site`: for each reference: tags, palette roles, audit summary
- `list_tags`: to find the right industry and site-type slugs
## Output template
```markdown
# Landscape audit
| Site | Art style | Hero | Skeleton | How it asks for the primary action | Do not copy (audit) |
|---|---|---|---|---|---|
## The niche's default look
## Gaps nobody fills
```
## Gates
- [ ] At least 6 sites from at least 3 different art-style families.
- [ ] A one-sentence description of the default look exists.
## Done when
- The table has 6 or more sites and the default look is named.
## Pitfalls
- Only studying direct competitors.
- Copying a reference without reading its audit caveats.

# Step: Align with stakeholders (`need-alignment`, stage need)
**Goal:** Run a kickoff with the right questions and agree who decides.
**Your role:** Confirm the framing with the owner before the brief. This is the main point to ask, not assume.
**Inputs:** need-statement, audience-profile, constraints, landscape-audit  
**Output artifact:** kickoff-notes -> `design/01-need/kickoff-notes.md`
## Procedure
1. Summarize the need statement, audience groups, top job, constraints and the landscape's default look in under one page.
2. Ask the owner these five questions in one message: confirm the primary action; rank the audience groups; confirm or correct constraints; give three adjectives for the feeling; name two sites they like and one they dislike, with why.
3. Record the answers verbatim. Update earlier artifacts where answers change them and say so.
## Ask the owner (only what you cannot default)
- Is the primary action right? (a) yes: [primary action] (recommended) (b) no: say which.
- Which audience group matters most? (a) [group 1] (recommended) (b) [group 2].
- Are the constraints right? (a) yes, as listed in constraints.md (recommended) (b) change: say what.
- How should the page feel? (a) [three adjectives I propose from the brand] (recommended) (b) three words of your own.
- Sites you like and dislike? (a) skip: the taste intake at ref-gather shows library screenshots (recommended) (b) name two you like and one you dislike, with why.
## Output template
```markdown
# Kickoff notes
## Summary sent
## Owner's answers (verbatim)
## Changes made to earlier artifacts
## Decision rights (who signs off the brief, the direction)
```
## Gates
Rules to satisfy: `ux-start-with-needs` (read them with get_guidelines or rules/*.md).
- [ ] The owner's own words are recorded, not paraphrased.
## Done when
- All five questions are answered or explicitly deferred with a default.
## Pitfalls
- Proceeding on assumptions when the owner is available to answer.

# Step: Write the brief (`brief-write`, stage brief)
**Goal:** Turn the need into a one-page brief: purpose, audience, message, tone, scope, constraints.
**Your role:** Turn the need into a one-page brief that says what and why, not how. Treat it as a hypothesis you will revise.
**Inputs:** need-statement, audience-profile, job-story, constraints, kickoff-notes  
**Output artifact:** brief-draft -> `design/02-brief/brief-draft.md`
## Procedure
1. Write the brief from the need statement, audience profile, job stories, constraints and kickoff notes. Keep it to one page.
2. Sections: problem and why now; audience and situation; goal and primary action; message; tone (filled in by the next step); scope (what the homepage contains and what it does not); constraints as inputs; deliverables and what 'done' means.
3. State the version (v1). The brief changes if exploration reframes the problem; record each change with the reason. [Evidence: problem and solution develop together]
4. Do not describe visuals or technology. If a sentence says how, move it to the constraints or delete it.
5. Audience flags: if the audience profile flags people under stress, with low literacy, ESL, cognitive or learning disabilities, or screen-reader or dyslexia users, write under `Audience and situation`: `COGA escalation: the a11y-coga-* rules are major for this project` and name the reading level to aim for. Those rules (all fifteen are in `rules/build.md`) are then part of the brief's definition of done. [Our take]
## Sections track (default)
Applies only when the owner and you chose the sections track. In full, sprint and lean tracks ignore this section.
- audience-profile, job-story, constraints and kickoff-notes are replaced by the Audience, Jobs, Constraints and Owner's words sections of need-statement.md. Read them from there.
- Fill the Success section for real: the one primary action (a lead, a sign-up, a booking) and how it is counted. realize-qa checks it, and the picked sections must give it a place (a form slot in the hero or the close).
- Keep the brief to one page. Its job in this track is to say what the page must do and say, not what it looks like: the look comes from the library sections picked next.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- Audience, constraints and kickoff notes are replaced by the Audience, Constraints and Owner's words sections of need-statement.md. Read them from there.
- Positioning and design-principles are skipped, so fill the `Tone` section for real instead of leaving a placeholder: a one-sentence value proposition (who, what, why different), proof points with sources or `no proof yet`, three to five tone words each with its opposite, and three anti-goals (one derived from the niche's default look). Later lean steps read these lines from brief-draft.md as positioning and principles.
- The brief stays v1 and is not reviewed by the owner in lean: mark it `ASSUMED, not owner-approved` unless the owner has read it. It still must fit one page.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- constraints and kickoff-notes are replaced by the Constraints and Owner's words sections of need-statement.md. audience-profile and job-story exist as their own files in the sprint.
- positioning and the content inventory are skipped, so brief-draft carries them. Fill `Tone` as in lean: a one-sentence value proposition (who, what, why different), proof points with sources or `no proof yet`, three to five tone words each with its opposite, a swap-test line and three anti-goals (one from the niche's default look). Add a `## Content inventory` section: a table with one row per block the page needs (block, the visitor question it answers, priority must/should/could, source provided/to write/to produce, status) and the primary action's place. Twelve rows or fewer. Facts the owner has not confirmed get status `unconfirmed` and go in design/OPEN-QUESTIONS.md. Any block that gives legal, medical, financial or safety advice is also marked `needs expert review` (`copy-expert-review-before-launch`).
- ref-principles later refines the tone words and anti-goals into design principles; keep them in the brief as well. brief-review turns this file plus success-criteria into brief.md.
## Output template
```markdown
# Design brief (v1)
## Problem and why now
## Audience and situation
## Goal and primary action
## Message (what the page must make people understand)
## Tone (placeholder, completed in positioning; in lean and sprint fill it here: value proposition, proof or 'no proof yet', tone words with opposites, three anti-goals)
## Scope: includes / excludes
## Constraints (inputs, not obstacles)
## Deliverables and what done means
## Content inventory (sprint only; in full and lean see brief-content)
## Change log
```
## Gates
Rules to satisfy: `ux-start-with-needs` (read them with get_guidelines or rules/*.md).
- [ ] One page or less.
- [ ] No visual or technical solution is prescribed.
- [ ] Success criteria and constraints appear (full criteria are written in brief-success).
## Done when
- All sections exist; the brief is versioned.
## Pitfalls
- A brief that is a feature list or a mood board in words.

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

# Step: Plan the content and page goal (`brief-content`, stage brief)
**Goal:** List what the homepage must say and do, in priority order, and pick one primary action.
**Your role:** Decide what the homepage must say and do, in priority order, with one primary action.
**Inputs:** brief-draft, positioning  
**Output artifact:** content-inventory -> `design/02-brief/content-inventory.md`
## Procedure
1. List every block of content the page needs (headline, what it is, proof, how it works, pricing, FAQ, contact...). For each: priority (must, should, could), source (provided, to be written, to be produced), and the visitor question it answers.
2. Order by importance to the top job. Put the primary action in the first screen and repeat it where it is natural.
3. Flag missing content now. Use real content in designs; if it does not exist, write plausible real copy and mark it 'draft'. Never use lorem ipsum. [Craft: content-first]
4. Facts the owner has not confirmed (prices, hours, sizes, policies, addresses, dates, contact details) get status `unconfirmed` in the inventory and are listed in design/OPEN-QUESTIONS.md. Inside a prototype page they carry the visible marker from the protocol (section 3.2: the `.assumed` dotted-underline convention with a legend), never brackets and never a silent invention. Invented proof (customers, numbers, quotes, press) is not a fact you may mark and ship: leave it out. [Our take]
5. A status or count derived from history (git commits, a changelog, old notes: "25 of 124 pages have sources matched to PubMed") is an assumption until the owner confirms the list: status `unconfirmed`, `.assumed` on the page, listed in OPEN-QUESTIONS.md. Named reviewers and their credentials are facts too: check the person exists before you show the name (protocol 3.2).
6. After you compute a number from content (counts per category, pages per type), open the list it counts and read ten rows before the number goes on the page: in a test a count doubled because two category pages shared one product type, and some items were dropped by a schema error.
7. Map the content to likely section types (hero, features, proof, pricing, FAQ, CTA, footer).
8. Mark every block that gives legal, medical, financial or safety advice `needs expert review` and add the reviewer you need (a solicitor, a clinician, an adviser) to design/OPEN-QUESTIONS.md. Until a qualified person has reviewed it, the copy ships only as a visible draft (the `.assumed`-style marker and legend, protocol 3.2) and realize-launch stays closed. [Our take: `copy-expert-review-before-launch`]
9. Forms: if the page takes personal data (a callback, an enquiry, a booking), list the form, the fields it needs (three required at most), where the data goes (a backend, or email) and who can answer for it; the recipe `form-no-backend-and-privacy` covers the no-backend case and the privacy line.
## Ask the owner (only what you cannot default)
- Which content exists? (a) the current site's text and images, mapped in content-map.md (recommended) (b) new material: send it.
## Output template
```markdown
# Content inventory
| Block | Visitor question it answers | Priority | Source | Section type | Status |
|---|---|---|---|---|---|
## Primary action and where it appears
```
## Gates
Rules to satisfy: `ux-primary-cta-above-fold`, `ux-front-load`, `ux-real-content-examples`, `copy-expert-review-before-launch` (read them with get_guidelines or rules/*.md).
- [ ] Every must-have block has a source.
- [ ] The primary action appears in the first screen.
- [ ] Every block that gives legal, medical, financial or safety advice is marked `needs expert review` with the reviewer named.
## Done when
- All blocks are prioritized and sourced; gaps are listed.
## Pitfalls
- Designing with placeholder text that hides copy problems.
- Inventing a plausible fact and shipping it unmarked: mark it, list it in OPEN-QUESTIONS.md, and let realize-launch refuse while it remains.

# Step: Define success criteria (`brief-success`, stage brief)
**Goal:** Write measurable and qualitative criteria that decide between options later.
**Your role:** Fix the criteria that will decide between options later, so taste does not decide alone.
**Inputs:** need-statement  
**Output artifact:** success-criteria -> `design/02-brief/success-criteria.md`
## Procedure
1. Write measurable criteria (for example a conversion target, a task success rate in a test, a load-time target) and qualitative criteria (a five-second test: at least 4 of 5 people can say what the page is for).
2. For each measurable criterion find the event, query or report that produces the number, and check that it fires today (read the tracking code and trigger it once). A criterion nothing records will read zero: if the event does not exist or is declared but never sent, building it is part of the work, so add it to the brief's scope and to the build plan.
3. Conversion: name what the page captures (an email, a booking, a sign-up, a purchase) and the value the visitor gets in exchange (a plan, a checklist, reminders, a quote). A page that has a form must use it to capture, with that exchange stated next to it; copy that promises the opposite ("no email") needs the owner's say-so. Write where the capture appears: in the first screen, repeated after each major section, and in a closing band. In a real run the owner's verdict on a stylish page was "very little conversion potential" because its only action captured nothing. [Our take]
4. Add the quality bar: zero blocker failures from the Quality Bar, WCAG 2.2 AA, Web Vitals targets from the constraints.
5. Write the decision rule: how directions will be compared and who decides (usually the owner).
## Ask the owner (only what you cannot default)
- What would make you call the homepage a success? (a) [primary action] per 100 visits up against the first four weeks (recommended) (b) another number or event: say which.
## Tools
- `get_guidelines`: topic 'blockers' to cite the quality bar
## Output template
```markdown
# Success criteria
## Measurable
## Qualitative (five-second test and others)
## Quality bar (blockers = 0, WCAG 2.2 AA, Web Vitals)
## Decision rule and decider
```
## Gates
Rules to satisfy: `ux-test-iteratively` (read them with get_guidelines or rules/*.md).
- [ ] At least one criterion can be measured without opinion.
- [ ] Quality-bar line is present.
## Done when
- Criteria and the decision rule are written.
## Pitfalls
- Only subjective criteria ('feels modern').

# Step: Review and sign off (`brief-review`, stage brief)
**Goal:** Check the brief against a checklist and get agreement before design starts.
**Your role:** Check the brief against a checklist and get the owner's agreement before design starts.
**Inputs:** brief-draft, positioning, content-inventory, success-criteria  
**Output artifact:** brief -> `design/02-brief/brief.md`
## Procedure
1. Run the checklist below on the draft and fix failures.
2. Assemble brief.md: the one-page brief plus positioning, content inventory and success criteria as linked sections.
3. Ask the owner to approve. Record the approval and the version.
4. Owner unavailable: do not stop and do not write `approved`. Use the heading `# Brief v1 (NOT owner-approved, ASSUMED)`, tick the approval box as `requested, open` and list the approval as the first line of design/OPEN-QUESTIONS.md. Every later artifact then inherits the label `ASSUMED, not owner-approved` (protocol 4).
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- positioning and content-inventory are replaced by the Tone and Content inventory sections of brief-draft.md. Assemble brief.md from brief-draft.md and success-criteria.md; the checklist below then also asks that both sections exist.
## Ask the owner (only what you cannot default)
- Do you approve this brief (v1)? (a) yes, approved as written (recommended) (b) approve with changes: list them.
## Output template
```markdown
# Brief v1 (approved [date] by [name])
(owner unavailable: write the heading as "# Brief v1 (NOT owner-approved, ASSUMED)")
(links to positioning, content inventory and success criteria; sprint: the Tone and Content inventory sections of brief-draft)
## Checklist
- [ ] One page
- [ ] What and why, not how
- [ ] Measurable success criteria
- [ ] Constraints as inputs
- [ ] Assumptions flagged
- [ ] Owner approval recorded (or, owner unavailable: heading says NOT owner-approved, ASSUMED; approval listed as open)
```
## Gates
- [ ] All checklist boxes ticked.
- [ ] Approval recorded; owner unavailable: the heading says NOT owner-approved, ASSUMED and the approval is listed as an open question.
## Done when
- The owner has approved and the version is recorded, or the brief is headed `NOT owner-approved, ASSUMED` and the approval is an open question.
## Pitfalls
- Moving on without approval; the brief then cannot arbitrate later disputes.

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

# Step: Analyze references (`ref-analyze`, stage references)
**Goal:** Annotate what exactly works in each reference: structure, type, color, motion, copy.
**Your role:** Find out exactly what works in the strongest references so you can reuse the idea, not the surface.
**Inputs:** reference-board  
**Output artifact:** reference-notes -> `design/03-references/reference-notes.md`
## Procedure
1. Pick the 6 to 10 most useful references. For each call get_site and read its style record, palette roles, fonts, tags and audit.
2. Get the numbers before the impressions: get_craft with the slugs gives each site's scale contrast (headline over body), type scale step, section whitespace in body units, lead-object share of the first screen and motion timing, and the library's quartiles. Write them in the notes; they are what makes a page feel agency-grade, and compare_to_library checks your concepts against them later.
3. Annotate: page skeleton and section order, hero type, navigation, type scale and pairing, color roles and contrast, motion (what, when, how long), copy approach (headline structure, proof, CTA wording).
4. Write a 'why it works' sentence for each notable move and the reusable principle behind it. For motion use phases: trigger, start, move, settle. [Craft]
5. Use compare for two to four references that look alike on the surface to find what actually differs.
## Tools
- `get_site`: style record, palette roles, fonts, audit summary and failing rules
- `get_craft`: slugs; scale contrast, type step, whitespace, lead-object share and motion timing per site, with the library quartiles
- `get_design_system`: format markdown for the DESIGN.md of a reference
- `get_design_brief`: tokens, components, section map, image files and audit failures of a reference: enough to study or rebuild its structure without a screenshot
- `compare`: slugs of 2 to 4 references
## Output template
```markdown
# Reference notes
## [slug]
- Skeleton and section order:
- Hero and navigation:
- Type and color:
- Motion (trigger, start, move, settle):
- Copy approach:
- Why it works:
- Reusable principle:
- Do not copy (audit failures):
```
## Gates
Rules to satisfy: `distinct-customize-library-defaults` (read them with get_guidelines or rules/*.md).
- [ ] Every note states a reusable principle, not a surface feature.
- [ ] Audit failures are named, not ignored.
## Done when
- 6 to 10 references annotated with a principle each.
## Pitfalls
- Describing the look instead of explaining why it works.
- Treating a reference's accessibility failures as part of its style.

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

# Step: Sketch many ideas (`explore-sketch`, stage explore)
**Goal:** Generate many rough ideas quickly without judging them. Quantity first, selection later.
**Your role:** Diverge. Produce many rough ideas quickly, without judging them. Quantity before quality.
**Inputs:** brief, design-principles, reference-notes  
**Output artifact:** idea-sketches -> `design/04-explore/idea-sketches.md`
## Procedure
1. Generate at least 12 idea cards. Each card: a one-line concept, the layout idea, the visual device (type, color, imagery, motion), and the headline angle.
2. Cover at least five different art styles and at least three different page skeletons. Use list_tags to pick styles you would not normally choose. [Evidence: ideate many ideas before selecting; Norman: rough breadth beats one polished model]
3. Do not judge, merge or refine during this step. Judgement happens in Decide.
4. Include at least two ideas you think are wrong; they often become useful.
## Tools
- `list_tags`: facet art-style and layout to choose varied directions
- `search_sites`: one query per idea to find a real example
## Output template
```markdown
# Idea sketches (no judging)
| # | Concept | Layout | Visual device (type/color/imagery/motion) | Headline angle | Art style | Skeleton |
|---|---|---|---|---|---|---|
```
## Gates
Rules to satisfy: `distinct-written-direction` (read them with get_guidelines or rules/*.md).
- [ ] At least 12 cards.
- [ ] At least 5 art styles and 3 skeletons are represented.
- [ ] No card contains a critique.
## Done when
- 12 or more varied cards exist.
## Pitfalls
- Twelve variations of the first idea.
- Judging while generating.

# Step: Frame three directions (`explore-directions`, stage explore)
**Goal:** Combine art style, mood, typography and color into three distinct directions with a one-line north star each.
**Your role:** Converge the sketches into three genuinely different directions the owner could choose between.
**Inputs:** brief, design-principles, reference-board, idea-sketches  
**Output artifact:** direction-matrix -> `design/04-explore/direction-matrix.md`
## Procedure
1. Show the directions to an owner who is not at your keyboard as one side-by-side sheet per size (desktop and mobile, the three concepts in a row, each labelled with its name and one-line north star) saved as image files, plus the north-star lines in your message. That worked better than links or prose.
2. Cluster the sketches and pick three directions that differ in at least two of: art-style family, mood, type class (serif, grotesque, mono, display), palette mood, page skeleton.
3. Concept first (studio method, get_studio concepts): write three concepts from different territories (the subject's name or story, its material, its place or culture, a metaphor for how it works, a formal or typographic system). Each has one sentence, its anchor (the specific fact about this subject it depends on), the signature moment, the emotion of the first 3 seconds, the motion verb and the frame people would screenshot; score originality, fit, feasibility and portability (could it move to another brand? lower is better). Each direction below is one concept dressed in an art direction from the library; a library style alone is not a direction. [Our take, from the awwwards method]
4. Span a range of ambition: one **safe** direction (closest to the owner's taste anchors from the reference board), one **stretch** (a visibly stronger look taken from the library's most distinctive sites), one **wildcard** (an unexpected combination). Anchor each on named library sites with one stated take per site ("butter-video's type scale with makingsoftware-com's ledger"). propose_directions drafts this from the brief and the owner's taste slugs and checks the spread; it is a starting point, not the answer. Three variations of one idea fail the gate.
5. For each, write a one-line north star ('Calm editorial finance with serif display type'), the taxonomy tags (art style up to 3, mood up to 2), the page skeleton, hero type, and the reference sites it draws on.
6. For each direction call get_recipe for its art styles (at most 3 tags per call, canonical slugs from list_tags such as `hand-drawn`, not invented ones such as `illustration-hand-drawn`: with 8 tags a pilot got over 60 KB of JSON, and unknown tags come back with empty rule lists) to learn upfront which Quality Bar rules it collides with and how to keep the look and pass the rules. Write those risks in the matrix. [Our take: surface accessibility risk before falling in love with a direction]
7. Check the three against the swap test and the niche's default look from the landscape audit: at least one direction must clearly depart from the default.
8. Name each direction's niche cue: what in the look says, in one second, which kind of site this is (a motif, a palette, a shape, a material). Avoiding the niche's clichés (blush, florals, script for weddings) is not the same as dropping its legitimate vocabulary: in a real run an elegant editorial direction with a timeline said nothing about weddings, and the owner asked for "more pink, patterns and graphics". Draw the cue from the niche references on the board. [Our take]
9. Pick each direction's lead element from the catalogue of recurring moves where one fits (get_moves: oversized type plus object, pinned scene, chaptered story, data as image, product showcase, 3D hero ...): each move lists the library sites that show it, so study them with get_section before you draw. One lead move per direction.
10. Name each direction's lead element: the one thing (a hero object, a layout idea, a type move, an interaction) that the niche's default page does not have and that carries the brief's message. A new skeleton is not required, but a lead element is. Read the slop versions in `trends.md` and the rules in `rules/distinct.md` (get_guidelines distinct) before you fix the three directions, so none of them is the probable default (for example cream and terracotta, a split hero with a product card, a three-column icon grid). Copy that is specific on a generic skeleton still reads as generic. [Our take]
11. A lead element above the fold is not enough. Write down where the lead element recurs or is answered lower on the page (a second moment: the same object in a new state, the same type move as a section break, the same interaction as the close), and make the sections below the hero differ in structure from each other (not a run of heading plus paragraphs, not the same card repeated). A page with a strong hero and a plain typographic sequence below it is still the default page. [Our take]
12. No photography exists (physical goods with no photos yet: a studio, a shop, a food or craft business; or a service with no photographs, or none you may use: advice, a clinic, a helpline, a firm)? The imagery rules were written with software in mind, which has an interface to show. Choose one of three, in this order, and write it in the matrix (graphics drawn in code from the page's real content, such as a data graph or a process diagram in the tokens, can serve any of them; see protocol 6 and plan_graphics): (1) the offer itself is the live object: price, seats, dates, sizes or a booking interactive built from real HTML controls with real states and real numbers (it works only when the offer has state to show: seats, slots, sizes, bundles); (2) type as image: a measurement, a date, a price or a name set large as the visual, as real text, not as an image of text; (3) leave imagery out and mark the gap in the matrix and in OPEN-QUESTIONS.md, because real photographs have to be commissioned before launch. A pieces-only catalogue has no state to show: say that, and treat the missing photographs as a launch risk. Illustrations assembled from shapes in code (a drawn bowl, a cross-section) stay out (`distinct-real-imagery-and-icons`). For a service the live object is something it really has state for (opening hours, free slots, a waiting time, a self-check or calculator), and type as image can be the fact that answers the first question (a phone number and its hours, a fee, "free and independent"); photographs of people need their consent. Which recipe steps apply to a service: `np-offer-live-object` (when there is state to show), `np-live-object-accessible` (if you build one), `np-type-as-image`, `np-mark-the-gap` and `np-commission-later`; `np-menu-and-run-sheet` only when the service has rows to list (a fee table, opening hours, the steps of a process); `np-pieces-only-limit` is for goods. Recipe: `no-photography-physical-goods`. [Our take]
13. Public service, advice or crisis audience (people who may be in danger, in debt, ill or facing a deadline)? Decide before you design the hero what the urgent route is and where it sits: read the recipe `urgent-help-route` (what goes first, a phone number as a `tel:` link with hours and an out-of-hours route, the emergency-services boundary stated once, not relying on red alone, and how the band stacks with the primary action at 390x844) and write the choice in the matrix. If the page also takes personal data in a form, read `form-no-backend-and-privacy`. An audience with these flags usually also means the COGA rules are major (protocol 5). Read the trend records `plain-language-public-service-pages`, `charity-emotional-template` and `law-firm-authority-template` in `trends.md`: the last two are the slop versions to depart from. [Our take]
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- design-principles and idea-sketches are skipped. Read the tone words and three anti-goals from brief-draft.md, and write six one-line, unjudged ideas at the top of direction-matrix.md before you converge. Read the landscape note at the top of reference-board.md as the landscape audit.
- Three directions are still required, but three short columns are enough: north star, art style, type class, palette mood, skeleton and hero, lead element and its second moment, recipe and the rules it collides with. Choose the recipe with get_recipe (at most 3 tags per call).
- Draft tokens live here in lean: add rows for up to two type families with roles (see the font sourcing advice in explore-type-color and decide-tokens) and 5 to 7 colour roles per direction, with contrast pairs checked by check_contrast. explore-hero and decide-tokens read them from the matrix.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- idea-sketches (explore-sketch) and design-principles (ref-principles) exist in the sprint: use them. need-landscape, explore-type-color and explore-structure are skipped: read the five-line landscape note at the top of reference-board.md as the landscape audit, and write the draft tokens and the structure into the matrix instead.
- Three directions are still required, but three short columns are enough: north star, art style, type class, palette mood, skeleton and hero, lead element and its second moment, recipe and the rules it collides with. Choose the recipe with get_recipe (at most 3 tags per call).
- Draft tokens live here in the sprint: add rows for up to two type families with roles (see the font sourcing advice in explore-type-color and decide-tokens) and 5 to 7 colour roles per direction, with contrast pairs checked by check_contrast, plus the section order of the page. explore-hero, decide-inclusive, decide-prototype and decide-tokens read them from the matrix.
## Ask the owner (only what you cannot default)
- (Gate 2, with the desktop and mobile sheets) Which direction? (a) [n], my recommendation, for [one reason] (recommended) (b) another number or a mix ("1's type with 3's colour") (c) none: say why.
## Tools
- `get_studio`: topic concepts (three concepts, anchor, signature, motion verb), art-direction, typography
- `get_moves`: the catalogue of recurring moves with the library sites that show each; one lead move per direction
- `propose_directions`: brief and the owner's taste slugs; returns safe, stretch and wildcard drafts with per-site anchors, recipes and Quality Bar collisions, and reports when the three are too alike
- `render_sheet`: the three hero concept files; writes one labelled side-by-side sheet per size (1440x900 and 390x844) to show the owner
- `get_recipe`: at most 3 tags per call (canonical slugs from list_tags); returns keep, avoid, steps; long JSON with many tags
- `recommend`: optionally, to sanity-check one direction against the brief
- `list_tags`: to use canonical slugs
## Output template
```markdown
# Direction matrix
| | Direction A | Direction B | Direction C |
|---|---|---|---|
| North star | | | |
| Concept (one sentence) and its anchor fact | | | |
| Signature moment and motion verb | | | |
| Range (safe / stretch / wildcard) | | | |
| Library anchors (slug: what it takes) | | | |
| Art style (<=3) | | | |
| Mood (<=2) | | | |
| Type class | | | |
| Palette mood | | | |
| Page skeleton / hero | | | |
| Reference sites | | | |
| Recipe(s) | | | |
| Rule collisions to manage | | | |
| Lead element (not in the niche default) | | | |
| Niche cue: what tells a visitor in one second which kind of site this is (motif, palette, shape, material) | | | |
| Where the lead element recurs lower on the page; how the sections below differ from each other | | | |
| Imagery plan (photos, live object, type as image, or gap marked) | | | |
| Draft tokens (lean and sprint: two type families, 5 to 7 colour roles, checked pairs; sprint also the section order) | | | |
| Difference from the niche default | | | |
```
## Gates
Rules to satisfy: `distinct-swap-test`, `distinct-written-direction` (read them with get_guidelines or rules/*.md).
- [ ] Each direction carries a concept with an anchor fact and a portability score, a signature moment and a motion verb; no direction is a library style alone.
- [ ] Each direction names a niche cue: avoiding the niche's clichés must not drop its vocabulary (a wedding site still needs something that says wedding).
- [ ] The directions differ in at least two dimensions and span safe, stretch and wildcard, each anchored on named library sites with a stated take.
- [ ] The owner was shown the desktop and mobile sheets (made in explore-hero) and their pick is recorded, or the pick is the one blocking question in OPEN-QUESTIONS.md and work has stopped (protocol 4).
- [ ] Each names its recipe and collision risks.
- [ ] Each names a lead element and a second moment lower on the page; at least one direction departs from the niche default.
- [ ] Each states how its sections below the hero differ in structure from each other.
- [ ] Each states its imagery plan; with no photographs it names the live object, the type move or the marked gap.
## Done when
- A complete matrix for three distinct directions.
## Pitfalls
- Three variations of one idea.
- Choosing for the owner and marking it ASSUMED: taste is never defaulted.
- Three palettes on one layout (not three directions).
- Ignoring the accessibility risks of a favorite style.
- A distinctive hero on top of a plain sequence of heading-and-paragraph sections.
- Drawing the product from shapes in code because there are no photographs.

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

# Step: Explore structure (`explore-structure`, stage explore)
**Goal:** Choose a page skeleton and sketch the section order for each direction.
**Your role:** Decide how the page is built: skeleton, section order and navigation, from the content inventory.
**Inputs:** brief, content-inventory, direction-matrix  
**Output artifact:** structure-wireframes -> `design/04-explore/structure-wireframes.md`
## Procedure
1. For each direction choose a page skeleton (taxonomy layout/macrostructure) and list the sections in order using section types (navbar, hero, logos, features, bento, works, reviews, pricing, faq, cta, footer...).
2. Map every must-have content block from the inventory to a section. Put the primary action in the first screen and repeat it where natural. [Evidence: most attention goes to the top of the page]
3. Choose navigation: visible primary links on desktop; on mobile four or fewer links visible, otherwise a disclosure menu. Unusual navigation needs a written reason and the recipe's safeguards. [Evidence]
4. Draw a low-fidelity wireframe (text or ASCII is enough) of each direction, with the code order equal to the reading order.
5. A list that is the content (the visitor's possible situations, a services list) is one choice, not many (`a11y-coga-limit-choices-per-screen` counts competing choices): keep it as one labelled list that is the dominant feature, group a long one under headings, and keep every other action visibly secondary. Record the call (the tensions in `rules/build.md`). An urgent route (recipe `urgent-help-route`) is placed first in reading order and must not push the primary action out of the first screen. [Our take]
## Tools
- `search_sites`: allOf: [skeleton slug] to see real examples of the chosen skeleton
- `get_recipe`: for unusual navigation or layout tags
## Output template
```markdown
# Structure and wireframes
## Direction A: skeleton [slug]
Sections in order: navbar > hero > ...
Navigation:
Where the primary action appears:
Wireframe (indented text block, four spaces):

```
## Gates
Rules to satisfy: `ux-primary-cta-above-fold`, `ux-visible-navigation`, `a11y-meaningful-sequence`, `a11y-multiple-ways`, `craft-breakpoints-content-based` (read them with get_guidelines or rules/*.md).
- [ ] Every must-have content block is placed.
- [ ] The primary action is in the first screen.
- [ ] Code order equals reading order in the wireframe.
## Done when
- Each direction has a skeleton, section order, navigation choice and wireframe.
## Pitfalls
- Hiding navigation on desktop without need.
- Layouts that only work if the visual order differs from the source order.

# Step: Draft headlines and copy (`explore-copy`, stage explore)
**Goal:** Write headline and subhead options for each direction before polishing visuals.
**Your role:** Write real headlines and calls to action before polishing visuals. Copy shapes layout, not the other way round.
**Inputs:** brief, positioning  
**Output artifact:** headline-drafts -> `design/04-explore/headline-drafts.md`
## Procedure
1. For each direction write three headline options, a subhead, and the label of the primary action. Use the value proposition and tone words; be specific and plain. [Evidence: plain objective language outperformed promotional language; Craft: specific over abstract]
2. Scope keeps the copy (need-statement `## Scope`: keep verbatim)? Do not write new headlines. Write a placement map in headline-drafts.md instead: each existing heading, paragraph and action from content-map.md, and the new section and position it moves into; the only new words allowed are labels the new structure needs, marked as new. coverage checks it later.
3. Button and link labels name the result ('Book a demo', not 'Submit' or 'Learn more').
4. Run the swap test on every headline (replace the company name; if it still reads true for a competitor, rewrite). Strike buzzwords and filler openers. [Our take]
5. Check length: headline readable in two lines on mobile; paragraph and sentence length per the copy rules.
6. Reading level: `copy-reading-grade` targets US grade 6 to 8 for a general audience. For ESL or low-literacy audiences, or a UK public service, aim at grade 5 or lower, or CEFR B1 and GOV.UK-style plain language (short common words, one idea per sentence, the action first) and say the target in headline-drafts. [Our take: the tighter target is ours; the rule's own number is grade 6 to 8] An ESL group also gets: an offer of a translation or an interpreter (links to translated pages with `lang` and `hreflang`, the passage language marked with `lang`; say what the service can really offer, never promise an interpreter you do not have), no idioms or phrasal-verb puns, dates and numbers written out in one unambiguous format, and a plain statement of what happens next.
7. Legal, medical, financial or safety advice in the copy: write it as a draft, list the reviewer you need in design/OPEN-QUESTIONS.md, and mark it with the visible draft marker and legend until a qualified person has signed it off (`copy-expert-review-before-launch`). Do not write a claim you cannot attribute.
8. Forms and urgent routes: write the form's labels, the hint under each, the privacy line, the error and success messages and the phone line together (recipes `form-no-backend-and-privacy` and `urgent-help-route`): plain words, the action first, the hours as text, and "do not write bank details here" wherever a free-text box could collect sensitive data.
9. Facts the owner has not confirmed (a price, an opening hour, a size, a policy) stay in the copy only with the visible `.assumed` marker from the protocol (dotted underline plus a legend on the page), listed in design/OPEN-QUESTIONS.md. No brackets, no bare invention, and no invented customers, numbers, quotes or press at all.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- brief and positioning are replaced by brief-draft.md: use its value proposition, proof or `no proof yet`, tone words and swap-test line. Write three headline options for the one or two directions you will build, not all three if time is short; three are still needed for the chosen one.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- positioning is replaced by the Tone section of brief-draft.md (and brief.md): use its value proposition, proof or `no proof yet`, tone words and swap-test line. Write three headline options for each of the heroes you will build on Day 3, or for the one or two you expect to choose if time is short; three are still needed for the chosen one.
## Output template
```markdown
# Headline drafts
## Direction A
- Headline options (3):
- Subhead:
- Primary action label:
- Reading-level target (grade, or CEFR level) and how it was checked:
- Swap test result:
- Unconfirmed facts used (each marked .assumed on the page and listed in OPEN-QUESTIONS.md):
```
## Gates
Rules to satisfy: `copy-headline-swap-test`, `copy-specific-over-abstract`, `copy-no-buzzwords`, `copy-button-verb-label`, `copy-no-placeholder-text`, `ux-tagline-specific`, `ux-descriptive-labels` (read them with get_guidelines or rules/*.md).
- [ ] Each headline passes the swap test.
- [ ] The primary action label names a result.
- [ ] No placeholder text.
- [ ] Every unconfirmed fact is marked with the visible assumption marker and listed as an open question.
## Done when
- Each direction has headline options, subhead and action label that pass the checks.
## Pitfalls
- Rhetorical slogans ('Not X, it's Y').
- Using the same copy under three visual directions.

# Step: Design hero concepts (`explore-hero`, stage explore)
**Goal:** Design the first screen for each direction, using the real headlines.
**Your role:** Design the first screen of each direction as something you can look at, with real copy, type and color.
**Inputs:** direction-matrix, type-color-studies, structure-wireframes, headline-drafts  
**Output artifact:** hero-concepts -> `design/04-explore/hero-concepts/`
## Procedure
1. Build each hero on the base kit (get_base: skip link, header, a hero skeleton) as a small HTML/CSS page using the direction's tokens, the real headline and the real action label; your own CSS adds only the lead idea. Run `pnpm --silent --filter @whata/audit cli widths <file>` and fix every problem before the sheet. Render it at 1440×900 and 390×844 and look at the screenshots.
2. The first screen must show: who/what, why it differs, the primary action, a cue that more follows, navigation. [Evidence: homepage principles]
3. Apply the direction's recipe steps while building (focus ring, reduced motion, contrast, media handling). [Standard + Craft]
4. Start from the gate 1 bundle sketches (design/03-references/bundles/): the concept for the owner's bundle and two others are refined here, not drawn again. With scope `Structure: rebuild`, draw each hero fresh: nothing of the old layout carries over except content.
5. Make each concept look like its references, not like a template with their colours. Two ways, pick per concept: (1) **Critique loop:** run compare_to_library on the concept with its anchor slugs (it measures scale contrast, section whitespace, lead-object share and motion against the anchors and lists the gaps), then put the concept beside its main reference at the same viewport (`cli sheet` with both files, or the reference's fold screenshot from storage/sites/), list the gaps in scale (display size against body, the largest element against the viewport), whitespace, imagery and the lead object, fix them, and repeat once more: two rounds before the owner sees it. Keep the two gap lists in notes.md. (2) **Reference rebuild:** when the owner picked a library site at gate 1, rebuild its hero as a structural re-skin (same grid, scale steps, spacing and object placement from get_design_brief and get_section), check the structure with `pnpm site score <slug> <file:// or http URL of your hero>` (the rebuild score compares section by section; read the hero section's score, the rest of the page is not built yet), then swap in this project's content, colours and imagery. Copy structure only: no text, logo, images or brand colours of the reference, and none of its audit failures. [Our take]
6. Presence of style, not only absence of slop: each concept needs a clear scale contrast (the display size several times the body size, or one element that fills much of the first screen), one lead object that carries the message, and deliberate whitespace. A concept that is type plus colour on an even grid is flat: fix it before the sheet. The library's heroes fill most of the first screen with their lead object, usually as a full-bleed backdrop (an image, video or code-made SVG behind the text); the kit's `hero-bleed` part does this with a scrim so text contrast holds, and get_backdrop draws the backdrop in code from the palette and the project's own content (aurora, a field of one mark per real item, contours, the brand word set huge; see content/kit/backdrops.html). An object in a column is fine when the brief needs it, but then say on the sheet that it is smaller than the references' and why. compare_to_library counts full-bleed backgrounds and judges a hero-only sketch on its first screen only. [Our take]
7. Order in the first screen: one clear headline, one line, one action and one lead object, with the niche cue and atmosphere around them; separate elements that compete for attention need a reason. Richness (pattern, motif, backdrop, texture) is not competition and stays. Check each concept with `pnpm --silent --filter @whata/audit cli types <file>`: every role takes one style and peers in a list match; the style and element counts it prints are information, not a target. [Our take]
8. Keep the heroes small; do not build the whole page yet.
9. Show each concept beside its library anchors: the concept's key frame and the fold screenshots of the two or three library sites it takes its visual language from, on one sheet (`imageSheet` in @whata/audit, or put the anchor folds from storage/sites/ next to the concept in `cli sheet`). Name what each anchor gives (canvas, type, the object, the motion). If the frame does not visibly belong next to them, it is not in the library's language yet: change the canvas, type, spacing or object, not the concept. [Our take]
10. Every frame a poster: the first frame of each concept is its best, with type, space and image composed on purpose; motion may only amplify it. Rough the signature moment in at least the concept you recommend (a still of its key frame is enough for the sheet), so the owner judges the idea, not a layout. [Our take, from the awwwards method]
11. Make the sheets and stop: render_sheet (or the audit CLI's `sheet` command) puts the three concepts side by side, labelled with name and north star, one image per size (1440x900 and 390x844), with review_design run on each concept first. Send both sheets to the owner and ask gate 2's question (explore-directions). Nothing from decide-tokens onward starts, and nothing is built in the site tree, until the owner's pick is recorded. Screenshots of a single concept: `pnpm --silent --filter @whata/audit cli shot <file|url> <out.png> <width> <height>`.
12. No photographs of a physical product? Follow the imagery plan in the direction matrix: build the live object (price, seats, dates, a calculator or booking control made of real HTML with real states and real numbers), or set a measurement, date or price large as real text, or leave the image out and mark the gap. Do not draw the product from shapes in code. A faint decorative gradient or texture that does not depict the product is ornament; one that starts to depict it (grooves that read as a wheel, a glaze) is an illustration and counts under `distinct-real-imagery-and-icons`. [Our take]
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- type-color-studies and structure-wireframes are replaced by the draft tokens and the skeleton and hero rows of direction-matrix.md. Build every hero from those draft tokens.
- A lower bar: three concepts, each a small page of about fifteen lines is enough, but each is rendered at 1440x900 and 390x844 and looked at. Run review_design on all three concepts when each audit takes under five minutes (it usually does): reviewing only the concept you expect to choose biases the comparison, and in a test the owner chose the one with the most blocker risk. Fix blocker findings on the one chosen. If time is short, say in notes.md which concept got the full review.
- Check the lead element and the primary action are inside the first viewport at both sizes by screenshot: the audit does not check that.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- type-color-studies and structure-wireframes are replaced by the draft tokens and the skeleton and hero rows of direction-matrix.md. Build every hero from those draft tokens.
- The same lighter bar as lean: three concepts, each a small page of about fifteen lines is enough, each rendered at 1440x900 and 390x844 and looked at. Run review_design on all three when each audit takes under five minutes; the concept you expect to choose is built on the real tokens, and decide-critique on Day 3 runs review_design on the others, whose findings are then about a small page, not a finished one. Record in notes.md which concepts got the full review.
- Check the lead element and the primary action are inside the first viewport at both sizes by screenshot; with an urgent-help band (recipe `urgent-help-route`) check that the band does not push the primary action below the fold at 390x844.
## Ask the owner (only what you cannot default)
- (With the sheets) Which concept? (a) [n], my recommendation (recommended) (b) another number or a mix (c) none: say why.
## Tools
- `get_recipe`: for the direction's styles
- `review_design`: path to the hero HTML; returns Quality Bar results
- `render_sheet`: the three concept files; writes directions-desktop.png and directions-mobile.png
- `compare_to_library`: each concept with its anchor slugs: gaps in scale contrast, whitespace, lead object and motion before the owner sees it
## Output template
```markdown
# Hero concepts
One folder per direction: hero-A/index.html, hero-A-desktop.png, hero-A-mobile.png, notes.md (decisions and which recipe steps were applied).
directions-desktop.png and directions-mobile.png: the three side by side, labelled, sent to the owner.
```
## Gates
Rules to satisfy: `ux-purpose-clear`, `ux-primary-cta-above-fold`, `ux-false-floor`, `distinct-hero-not-template`, `craft-contrast-text-on-media` (read them with get_guidelines or rules/*.md).
- [ ] The first screen answers what it is and what to do within five seconds.
- [ ] Mobile and desktop screenshots exist, and the two side-by-side sheets were sent to the owner.
- [ ] Each concept went through two critique rounds beside its reference (or a scored reference rebuild), with the gap lists in notes.md.
- [ ] Each concept has a scale contrast and a lead object.
- [ ] review_design shows no blocker failures (lean and sprint: for the concept you expect to choose; say which).
## Done when
- Three hero concepts with screenshots and a clean blocker review (lean and sprint: three concepts with screenshots, one with the full review).
## Pitfalls
- Carrying on to tokens or a build before the owner has picked from the sheet.
- Flat concepts: type and colour on the old layout, no lead object, no scale contrast.
- Showing the owner a concept that was never put beside its reference.
- Placeholder text.
- Heroes that only work at one viewport.
- Template hero: centered stack with a generic gradient.

# Step: Explore motion and interaction (`explore-motion`, stage explore)
**Goal:** Decide where motion earns its place and which triggers and techniques fit the direction.
**Your role:** Decide where motion earns its place. Motion supports meaning; it is not decoration for its own sake.
**Inputs:** direction-matrix  
**Output artifact:** motion-notes -> `design/04-explore/motion-notes.md`
## Procedure
1. List candidate motions with the purpose of each (orient, give feedback, show relationship, express brand). Drop any without a purpose.
2. Motion follows the concept's motion verb (get_studio motion): one micro-interaction treatment per role (primary actions, navigation, work or product images) chosen from the verb, the signature moment, the continuity between states (intro, page to page), and an idle state that keeps the concept breathing at rest. Primary targets answer in the verb, not with a colour swap alone. One clock, one easing family; big things move slower than small things. [Our take, from the awwwards method]
3. Pick one lead motion idea for the direction and at most two supporting ones. Name triggers (scroll, hover, click, load) and techniques. [Our take: one lead idea beats five effects]
4. For each, define the reduced-motion variant (replace large movement with fades; keep what it conveyed) and the pause control for anything that starts automatically. [Standard]
5. Set budgets: animate transform and opacity only; no layout shift; no long main-thread tasks. [Craft]
## Tools
- `get_recipe`: motion-related tags: scroll-triggered, parallax, webgl, marquee, hero-video
## Output template
```markdown
# Motion notes
| Motion | Purpose | Trigger | Technique | Duration/easing | Reduced-motion variant | Pause control |
|---|---|---|---|---|---|---|
```
## Gates
Rules to satisfy: `a11y-reduced-motion`, `a11y-pause-stop-hide`, `ux-minimal-motion`, `craft-motion-duration-range`, `distinct-motion-authored`, `perf-inp` (read them with get_guidelines or rules/*.md).
- [ ] Every motion has a purpose, a reduced-motion variant and (if automatic) a pause control.
## Done when
- One lead motion idea and at most two supporting ones, each fully specified.
## Pitfalls
- Motion on every element.
- No reduced-motion variant.

# Step: Critique against the brief (`decide-critique`, stage decide)
**Goal:** Review each direction against the brief with a rubric built from the principles and success criteria. Critique asks whether it works, not whether anyone likes it.
**Your role:** Judge each direction against the brief, not against taste. Critique asks whether it works toward the goals.
**Inputs:** hero-concepts, design-principles, success-criteria  
**Output artifact:** critique-notes -> `design/05-decide/critique-notes.md`
## Procedure
1. Build a rubric from the brief's success criteria, the design principles and the anti-goals, plus one row for resemblance to the library's strongest references and the owner's taste anchors (name the sites). Give each row a weight, state it in the table, and make the resemblance row weigh at least as much as the heaviest message row: a rubric made only of message and compliance rows favours the safest direction by construction. Score each direction 1 to 5 per row with a one-sentence reason, multiply by the weight, and check that the totals equal the sum of the rows before you write them down.
2. Run review_design on each hero concept and add its blocker and major findings to the rubric.
3. Ask questions rather than proposing fixes: What problem does this solve? Who is it for? What would make it fail? Park fixes for a later pass. [Craft: critique rules: everyone is a critic, avoid problem-solving, do not rush]
4. Write down which strengths to carry over from each direction, even the ones you will not choose.
## Tools
- `review_design`: path to each hero concept; Quality Bar results
## Output template
```markdown
# Critique notes
## Rubric (criteria from the brief and principles)
| Criterion | Weight | A | B | C |
|---|---|---|---|---|
| Resemblance to the library's strongest references and the owner's taste anchors (name them) | | | | |
| Presence of style: scale contrast, one lead object, deliberate whitespace, imagery (not only absence of slop) | | | | |
| Weighted total (check: equals the sum of the rows) | | | | |
## Questions raised per direction
## Strengths to carry over
## Quality Bar findings per direction
```
## Gates
Rules to satisfy: `distinct-review-against-published-criteria` (read them with get_guidelines or rules/*.md).
- [ ] Every score has a reason.
- [ ] No fixes proposed inside the critique.
## Done when
- The rubric is complete for all directions with Quality Bar findings.
## Pitfalls
- Scores justified by 'I like it'.
- Starting to redesign during critique.

# Step: Check inclusion and accessibility early (`decide-inclusive`, stage decide)
**Goal:** Check the leading directions for contrast, motion, readability and who might be excluded, before investing in detail.
**Your role:** Check, before investing in detail, whether the leading directions can be used by people with different abilities and devices.
**Inputs:** hero-concepts, type-color-studies, motion-notes  
**Output artifact:** inclusion-check -> `design/05-decide/inclusion-check.md`
## Procedure
1. Run review_design on the top two heroes and read the blocker and major findings.
2. Do the manual checks in a real browser: Tab through the page (visible focus, logical order, nothing hidden behind sticky elements); zoom text to 200%; view at 320 px wide; turn on reduced motion; check forced colors if you can; check color contrast of every state. [Standard + Craft]
3. List who might be excluded (low vision, motor, cognitive load, screen reader, slow network) and what the design does for them.
4. Fix what is cheap now; discard a direction whose core idea cannot pass (for example text that must sit on a busy video with no scrim).
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- type-color-studies is replaced by the draft tokens in direction-matrix.md; motion-notes by the motion and reduced-motion variant written in each hero's notes.md. Check the leading hero (and the runner-up if time allows), not all three.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- type-color-studies is replaced by the draft tokens in direction-matrix.md; motion-notes by the motion and reduced-motion variant written in each hero's notes.md. Check the leading hero and the runner-up (they are the two the prototype step may build).
## Tools
- `review_design`: path to each hero concept
- `check_contrast`: any pair you have not yet verified
## Output template
```markdown
# Inclusion and accessibility check
| Check | A | B | C |
|---|---|---|---|
| Keyboard path and visible focus | | | |
| Text at 200% | | | |
| 320 px reflow | | | |
| Reduced motion | | | |
| Contrast (text, UI, focus) | | | |
| Forced colors | | | |
## Who could be excluded and how the design responds
## Decisions (fix now / discard)
```
## Gates
Rules to satisfy: `a11y-keyboard`, `a11y-focus-visible`, `a11y-reflow`, `a11y-resize-text`, `a11y-reduced-motion`, `a11y-contrast-text`, `a11y-target-size` (read them with get_guidelines or rules/*.md).
- [ ] Every row is filled with a result, not 'ok'.
- [ ] Blocker failures are fixed or the direction is discarded.
## Done when
- The table is complete and no remaining direction has a blocker failure.
## Pitfalls
- Relying on automated results alone: automated tools miss errors.

# Step: Prototype the strongest candidates (`decide-prototype`, stage decide)
**Goal:** Make a realistic clickable or coded version of the best one or two directions, with real content.
**Your role:** Make the strongest one or two directions real enough to test: full page skeleton, real content, working interaction.
**Inputs:** hero-concepts, critique-notes, headline-drafts, structure-wireframes  
**Output artifact:** prototype -> `design/05-decide/prototype/`
## Procedure
1. Build a coded prototype of the top one or two directions: all sections from the structure step, real copy, tokens as CSS custom properties, the recipe safeguards. Semantic HTML first; effects layered on top. [Craft: progressive enhancement]
2. Make it navigable and responsive (320 to 1920 px). Use real images or honest placeholders (marked).
3. Run review_design on the prototype and fix blocker failures before anyone sees it.
4. Only after the owner's pick: no prototype is built, and nothing is written in the site tree, until direction-decision.md records `Owner pick:` (protocol 4). A prototype of a direction the owner has not picked is wasted work and, in the site tree, uncommitted clutter.
5. Where it lives (build once): the prototype is the first draft of the build, so build it where the site will live (the project root or the source tree), not in a throwaway folder. Keep design/05-decide/prototype/ for notes.md (what is placeholder, which recipe steps were applied, known issues), the screenshots at 390 and 1440 and a one-line pointer to the site files. A second prototype of another direction, if you build one, lives inside that folder and is thrown away after the decision. realize-build then finishes the prototype instead of rebuilding it. [Our take]
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- structure-wireframes is replaced by the skeleton row of direction-matrix.md (the section order) and the Content inventory of brief-draft.md (what each section must say). Place every must-have block of the inventory and put the primary action in the first screen.
- In the sprint the prototype is the Day 4 deliverable and the first draft of the site: see `Where it lives` above. Day 5 tests it; realize-build and realize-qa follow after Day 5.
## Tools
- `review_design`: path to the prototype
- `get_recipe`: for the direction's styles
## Output template
```markdown
# Prototype
notes.md (what is placeholder, which recipe steps were applied, known issues, and where the prototype's files are), screenshots at 390 and 1440, and either the prototype itself (index.html + assets) or a pointer to the site files it was built in.
```
## Gates
Rules to satisfy: `perf-core-first`, `a11y-semantic-structure`, `a11y-name-role-value`, `copy-no-placeholder-text` (read them with get_guidelines or rules/*.md).
- [ ] The page content works with JavaScript disabled.
- [ ] review_design shows no blocker failures.
## Done when
- A prototype exists for each remaining direction with a clean blocker review.
## Pitfalls
- Prototyping all three directions in full (waste).
- Static screenshots only.

# Step: Test quickly (`decide-test`, stage decide)
**Goal:** Test with about five people per audience group, fix what you find and test again. Several small rounds beat one big one.
**Your role:** Get evidence from people. You cannot be the test participant; plan the test and ask the owner to run it.
**Inputs:** prototype, critique-notes, success-criteria  
**Output artifact:** test-results -> `design/05-decide/test-results.md`
## Procedure
1. Write a short test script: a five-second test (show the first screen, ask what the page is for and what they would do), a preference question between directions, and one task (find X).
2. Ask the owner to run it with about five people per audience group and to send you the answers. Do not substitute model opinions for participants; label any model review as such. [Evidence: five users per group per round find most problems; test, fix, test again]
3. When the owner's score falls after a round, first put the two rounds side by side and list what the new one removed or flattened; restore that before changing anything else. "Clustered" or "too busy" asks for order (consistent styles, spacing, hierarchy, no collisions), not for fewer motifs: ask which parts feel busy, with proposed answers, before cutting. [Our take]
4. Between rounds, the owner's score out of 10 with one sentence of why is cheap, honest evidence and moved a real project more than any audit did. Keep an owner round log in design/05-decide/owner-rounds.md as a table `| Round | Date | Shown | Score | Owner's words | What changed |` (name library slugs in Shown when a concept was anchored on them); `pnpm --silent --filter @whata/mcp taste import --project <project>` copies the scores into this client's taste record. Label it `UNTESTED` evidence about one person's view: it is not approval and not a user test.
5. Run automated checks as a supplement (axe, lab Web Vitals via review_design).
6. Summarize results, fix what you can, and say what remains unproven.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- Day 5 is the test day. If there are no people to test with (no owner, no participants), write the script, the participant list you would need and the questions in test-results.md, and record `UNTESTED` at the top. Do not fill the answers with a model's opinions. decide-choose then decides on the critique and the inclusion check alone and says the decision is untested.
## Ask the owner (only what you cannot default)
- Can you run the five-second test with 5 people? (a) not now: I record UNTESTED and decide on the critique (recommended if no one is available) (b) yes: I send the script.
## Tools
- `review_design`: automated supplement
## Output template
```markdown
# Test results
## Script
## Participants (group, count) and answers
## Findings and fixes
## Automated results (labelled automated)
## Not yet proven
```
## Gates
Rules to satisfy: `ux-test-iteratively` (read them with get_guidelines or rules/*.md).
- [ ] Participant answers come from people, not from the model.
- [ ] The five-second test result is compared with the success criteria.
## Done when
- Results from real people are recorded, or the absence is stated and the decision labelled 'untested'.
## Pitfalls
- Calling a model's review a user test.

# Step: Choose and document (`decide-choose`, stage decide)
**Goal:** Pick a direction and write down why, what was rejected, and what to carry over.
**Your role:** Choose a direction and record why, so the decision can be revisited with the same facts.
**Inputs:** critique-notes, inclusion-check, test-results, success-criteria  
**Output artifact:** direction-decision -> `design/05-decide/direction-decision.md`
## Procedure
1. An early pick: when the owner already picked one bundle or sketch at gate 1, record it here (`Owner pick:`, gate 1) at that moment and say so; gate 2 then confirms it with the built concepts instead of asking again from scratch.
2. Start from the owner's pick. The owner chose from the directions sheet (gate 2, explore-directions); record their words as `Owner pick: ...` at the top of the decision, with any mix they asked for, and record it with record_taste (type pick, gate 2, the project folder, the anchor slugs of the picked concept, their words). No pick recorded means this step is not done: do not decide for them (protocol 4).
3. Apply the decision rule from the success criteria to the critique, inclusion check and test results, and write your own scoring as advice under the heading `The model's ranking, for what it is worth`. If your ranking disagrees with the owner's pick, say so in one line and follow the pick.
4. Write the decision log: chosen direction, scores, reasons, rejected directions and why, what to carry over from rejected ones, and open risks.
5. Name the crux surfaces: the one or two parts of the page it stands or falls on (for example the hero and the booking path). They get the longest polish in realize-sweep. Choose them from the need and the brief, not from what is easiest to make beautiful.
6. The final choice of taste is the owner's: nothing here overrides the pick.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- Short form. critique-notes is replaced by the scoring table in hero-concepts/notes.md (each concept against the success criteria and the anti-goals, with its review_design findings, labelled a model review). test-results is replaced by `UNTESTED`: no test was run, so say so in direction-decision.md and decide on the critique and the inclusion check alone.
- Write the decision in ten lines or fewer: chosen concept, why against the criteria, rejected and why, what to carry over, open risks. The owner's pick is still required: lean keeps both taste gates. If the owner is away, the pick is the blocking question in design/OPEN-QUESTIONS.md and decide-tokens waits.
- decide-tokens and realize-build read this file in lean; the headlines and the chosen hero come from explore-copy and explore-hero.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- The days are named after the GV sprint: Day 3 "Decide" holds the critique and the inclusion check, and the decision is recorded here on Day 5, after the test. The owner confirms it here. If test-results.md says `UNTESTED`, decide on the critique and the inclusion check and write `UNTESTED` in direction-decision.md. The owner's pick from the Day 2 or Day 3 sheet is required; if they are away, the pick is the blocking question in design/OPEN-QUESTIONS.md and Day 4 waits.
## Ask the owner (only what you cannot default)
- Which direction do you pick from the sheet? (a) [n], my recommendation (recommended) (b) another number or a mix: say which.
## Output template
```markdown
# Direction decision (date, decider: the owner)
- Owner pick: [the owner's words]
- Chosen:
- Why (against the criteria):
- Crux surfaces (polished longest):
- Rejected and why:
- Carry over from rejected directions:
- Open risks and how they will be watched:
## The model's ranking, for what it is worth (advice, not the decision)
```
## Gates
Rules to satisfy: `distinct-written-direction` (read them with get_guidelines or rules/*.md).
- [ ] `Owner pick:` is recorded in the owner's words; without it the step is not done.
- [ ] The decision cites the criteria, not preference alone.
- [ ] The model's scoring is labelled as advice.
## Done when
- The owner's pick is recorded and the decision log is written.
## Pitfalls
- Choosing for the owner and marking it ASSUMED.
- Letting the model's scoring table make the decision.
- Choosing without recording the rejected options.

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

# Step: Design the homepage in full (`realize-design`, stage realize)
**Goal:** Design every section, state and breakpoint with real content.
**Your role:** Design the full homepage with real content: every section, state and breakpoint.
**Inputs:** direction-decision, design-tokens, structure-wireframes, content-inventory, headline-drafts  
**Output artifact:** homepage-design -> `design/06-realize/homepage-design.md`
## Procedure
1. Compose all sections from the structure step with the final copy and tokens. Check each section at 320, 390, 768, 1024, 1440 and 1920 px.
2. Design the states: hover, focus, active, disabled, loading, empty, error. Focus is visible and distinct. [Standard]
3. Check hierarchy (one h1, logical headings), grouping by proximity, spacing from the scale, alignment, image dimensions reserved, icon family consistent. [Craft]
4. Check rhythm: sections must not all share the same template (centered title, three cards). [Our take]
## Tools
- `get_recipe`: for the direction's styles
- `review_design`: after each major change
## Output template
```markdown
# Homepage design
Section list with content, tokens used and states.
Screenshots at 390 and 1440.
Known deviations from the tokens and why.
```
## Gates
Rules to satisfy: `craft-group-by-proximity`, `craft-image-dimensions-reserved`, `craft-icons-one-family`, `distinct-section-rhythm-varied`, `distinct-no-identical-card-grid`, `a11y-headings-labels`, `copy-no-placeholder-text` (read them with get_guidelines or rules/*.md).
- [ ] All content is real or marked as draft.
- [ ] States are designed, not only the default.
## Done when
- Every section exists at all breakpoints with states.
## Pitfalls
- Only designing at desktop width.
- Identical card grids repeated down the page.

# Step: Build the component set (`realize-components`, stage realize)
**Goal:** Define the small set of reusable components the page needs.
**Your role:** Define the small set of components the page needs and build them accessibly from established patterns.
**Inputs:** design-tokens, homepage-design  
**Output artifact:** component-set -> `design/06-realize/component-set.md`
## Procedure
1. List only the components the page uses (navigation, button, link, card, form field, accordion, dialog, tabs, carousel...). Each gets: purpose, states, tokens, and the accessibility pattern it follows.
2. For interactive components follow the ARIA Authoring Practices pattern and the component rules (get_guidelines topic components). Native HTML first; no ARIA is better than bad ARIA. [Craft: APG]
3. Site navigation dropdowns use disclosure buttons, not menu roles. Dialogs move focus in, keep it inside, close on Escape and return focus. [Standard + Craft]
4. Write each component's keyboard behavior in one line.
5. Form errors: `comp-alert-no-focus-no-autodismiss` forbids moving focus to a message, while the common accessible error-summary pattern moves focus to the summary. Resolve it this way: an empty `role=alert` region exists at load (`comp-live-region-exists-before-content`); on a failed submit fill it with the summary text and do not call `focus()` on it; move focus to the first invalid field; keep each error in text next to its field and keep what the user typed. Record the choice in the component notes. [Our take] Recipe: `form-no-backend-and-privacy`.
## Tools
- `get_guidelines`: topic: components, plus rule ids named in the pattern
## Output template
```markdown
# Component set
| Component | Purpose | States | Pattern followed | Keyboard behavior | Tokens |
|---|---|---|---|---|---|
```
## Gates
Rules to satisfy: `a11y-native-first`, `a11y-role-is-a-promise`, `comp-dialog-focus`, `comp-site-nav-no-menu-role`, `comp-tabs-semantics`, `comp-accordion-markup` (read them with get_guidelines or rules/*.md).
- [ ] Each interactive component names its pattern and keyboard behavior.
- [ ] Native elements are used where they exist.
## Done when
- Every interactive component on the page has a pattern, states and keyboard behavior.
## Pitfalls
- div role=button.
- Custom widgets where a native element would do.

# Step: Specify motion (`realize-motion`, stage realize)
**Goal:** Write motion specs: triggers, durations, easing, reduced-motion behavior.
**Your role:** Turn the motion notes into a precise spec developers (or you) can build without guessing.
**Inputs:** homepage-design, motion-notes  
**Output artifact:** motion-spec -> `design/06-realize/motion-spec.md`
## Procedure
1. For each motion write: trigger, start, move (properties: transform and opacity), settle, duration and easing from the tokens, what happens on repeat, reduced-motion variant, pause control, off-screen and hidden-tab behavior. [Craft + Standard]
2. Set the performance budget (no layout shift; main-thread cost; do not start before first paint of real content).
3. Describe fallback when JavaScript or the feature is unavailable.
## Tools
- `get_recipe`: scroll-triggered, parallax, webgl, hero-video, marquee, intro-preloader
## Output template
```markdown
# Motion spec
## [Motion name]
- Trigger / start / move / settle:
- Properties, duration, easing (tokens):
- Reduced-motion variant:
- Pause control:
- Off-screen and hidden-tab behavior:
- Fallback without JS:
- Budget:
```
## Gates
Rules to satisfy: `a11y-reduced-motion`, `a11y-pause-stop-hide`, `craft-motion-duration-range`, `craft-motion-easing-direction`, `craft-reduced-motion-replace`, `perf-cls` (read them with get_guidelines or rules/*.md).
- [ ] Every motion has a reduced-motion variant and a no-JS fallback.
## Done when
- All motions are specified with budgets and fallbacks.
## Pitfalls
- Animating layout properties.
- Starting heavy scenes before content paints.

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

# Step: Build it (`realize-build`, stage realize)
**Goal:** Choose the platform and build so the core content works first and effects layer on top. Use an AI agent that reads the DESIGN.md if helpful.
**Your role:** Build the page. Meaning first, then presentation, then behavior; content must work when the enhancements fail.
**Inputs:** homepage-design, component-set, motion-spec, assets, design-tokens  
**Output artifact:** built-site -> `(the project's source tree)`
## Procedure
1. Do not build in the site tree before the owner has picked a direction (direction-decision.md has `Owner pick:`). If you find unpicked work there (a build of a direction the owner did not choose), do not carry it forward: say so and ask whether to discard it.
2. Restyling an existing site that uses a component library (for example shadcn with Tailwind)? Do not rebuild the components. Map the design's colour roles onto the library's own role variables inside one scoped class (such as a theme class on the section or header), keep new CSS in a cascade layer (`@layer components`) so the library's utilities still win (unlayered custom CSS beat Tailwind's `hidden` in a test). First grep the global CSS for unlayered `*`, `html` and `body` rules: an unlayered `* { border-color: ... }` beats every layered border colour and stops the library's own border utilities from applying, so where such a rule sets border-color or colour, do not layer that CSS, and change the library's component files only where a role cannot express the change.
3. After every CSS change, confirm the new rule is in the stylesheet the server actually sends (fetch it, or read the computed style in the browser) before trusting a review: a dev server that missed three edits made the audit judge stale CSS without any warning.
4. Re-theming library components (shadcn and similar) breaks text at 200% in the same few places: badges that clip text, `line-clamp`, fixed-height bars and rows, `grid-cols-N` without a mobile fallback, and flex rows that cannot wrap. Check those five before the first audit.
5. Write control borders and other colours the audit must read as plain hex or rgb; the audit cannot always read modern colour functions (`oklch()`, `lab()`) and may report a border that is not there.
6. Name your own classes so they cannot collide with the project's utility framework: in Tailwind projects a section class `table` became `display: table` and shrank every such section to its content, and a `spine` class restyled every list. Prefix page classes or scope them under one page class.
7. Studio build (get_studio engine, nextjs or astro, patterns, layout): compose each section with a different layout family and make the static page complete and beautiful with motion off; then add motion through the studio engine (one clock, page lifecycle, data attributes; copy it, do not rewrite it) and build the concept as one driver module (one variable, such as scroll progress or time, drives every visual that carries the concept). Design the reduced-motion and no-JS versions on purpose. Avoid, unless the concept demands it: an eyebrow label above every heading, glass everywhere, decorative 01/02/03 when the content is not a sequence, three equal cards.
8. New page or a rebuilt structure: start from the base kit parts (get_base) in the project's tokens, and adapt them to the stack (components in a framework, partials in a static site); keep their accessibility details (menu button states, form error wiring, 44 px targets, wrapping rows).
9. Choose the stack from the constraints. Write semantic HTML first (landmarks, headings, real links and buttons), then CSS from the tokens (no raw hex in components), then behavior as enhancement. [Craft: layers; progressive enhancement]
10. Apply the direction's recipe steps and the component patterns. Keep the DOM order equal to the reading order; add a skip link; keep focus visible.
11. Read the rule list for the build once before starting (get_guidelines topic: build) and keep generate_hints in mind; re-run review_design after each section and fix blockers immediately.
12. Commit in small steps (if the project allows version control); keep a CHANGELOG of decisions that deviate from the tokens.
13. Unconfirmed facts shown on the page (see protocol 3.2): mark each with the visible `.assumed` marker, never brackets, add a legend on the page, and list each in design/OPEN-QUESTIONS.md. For a marked phone number or address inside a link, follow the `<Assumed>` pattern in `rules/build.md` (a solid link underline plus an inner marker; one legend plus `aria-describedby`).
14. Public-service or crisis audience: build the urgent route from the recipe `urgent-help-route` (the emergency-services line once, a `tel:` link with hours and an out-of-hours route, contrast and text instead of red alone) and check at 390x844 that it does not push the primary action below the first screen. Forms: build every form from `form-no-backend-and-privacy` (labels, `type`, `inputmode` and `autocomplete`, native `required`, the no-backend `mailto:` fallback with its honest success text, the privacy line, and no promise that anything was sent). If the audience flags the COGA rules, build to them as majors (`rules/build.md` lists all fifteen). [Our take]
15. Legal, medical, financial or safety advice on the page: it stays under the draft marker and legend until a qualified person has reviewed it (`copy-expert-review-before-launch`); record the reviewer and the date or the open question in design/OPEN-QUESTIONS.md.
## Sections track (default)
Applies only when the owner and you chose the sections track. In full, sprint and lean tracks ignore this section.
- homepage-design, component-set, motion-spec, assets and design-tokens do not exist in this track. section-pick.md replaces all five: build from the picked library sections (get_library_section for each), in the picked order.
- Copy sections.css, roles.css and sections.js unchanged, then each section's markup. Put the design system's --ds-* tokens from section-pick.md on the page root together with the class ds, so every section takes its type, colour, buttons, radii, container and rhythm from the one system. Change only what each spec lists under Adaptation slots; never edit sections.css or roles.css per project (a missing role is added to the library's roles.css).
- A longer headline or a different object may need a slot the spec allows (for example the h1 stepping down until it fits one line). A change the spec does not allow is a change to the section: stop and ask the owner, or pin a new section (content/sections/HOW-TO-ADD.md).
- Every picture slot gets real media from the media plan. Code-drawn stand-ins for photos read as cheap.
- Before the checks: shoot each adapted section at 1440x900 and 390x844 and put it beside its source (sourceFold, or the live sourceUrl for a lower section). It must visibly belong next to it; if it does not, fix the adaptation before anything else.
## Lean track (one-day)
Applies only when the owner and you chose the lean track. In sprint and full tracks ignore this section.
- homepage-design, component-set, motion-spec and assets do not exist in lean. Build from direction-decision.md (the chosen direction), design-tokens (tokens.css, DESIGN.md), headline-drafts.md (the copy) and the chosen hero in hero-concepts/ (its markup is the first draft of the build: keep it, do not rebuild it).
- Native elements first; list each interactive component and its keyboard behaviour in the build notes. Take the motion and reduced-motion variants from the hero's notes.md. List assets, licences and alt text in the build notes. Check the sections at 320, 390, 768 and 1440 px while building.
- The page must keep the lead element and give it a second moment lower down, and the sections below the hero must differ in structure from each other (see realize-qa). Build the sections that way, not as a plain run of headings and paragraphs.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- homepage-design, component-set, motion-spec and assets do not exist in the sprint. The prototype from decide-prototype is the first draft of the build: keep it (promote it to the site root if it was built elsewhere, record the move in the build notes) and finish it from direction-decision.md, design-tokens (tokens.css, DESIGN.md), headline-drafts.md and the chosen hero in hero-concepts/. Do not rebuild it. This step runs after Day 5; the sprint is not over at decide-tokens.
- Native elements first; list each interactive component and its keyboard behaviour in the build notes. Take the motion and reduced-motion variants from the hero's notes.md. List assets, licences and alt text in the build notes. Check the sections at 320, 390, 768 and 1440 px while building, and design the states the prototype skipped (hover, focus, active, disabled, loading, empty, error).
- The page must keep the lead element and give it a second moment lower down, and the sections below the hero must differ in structure from each other (see realize-qa). Build the sections that way, not as a plain run of headings and paragraphs.
## Ask the owner (only what you cannot default)
- Which stack? (a) the project's current stack (recommended) (b) another: say which.
## Tools
- `get_studio`: engine plus the nextjs or astro adapter, patterns (driver module, static fallbacks), layout families, motion recipes
- `get_guidelines`: topic: build, plus the recipe rule ids
- `get_build_prompt`: a ready prompt with the rules and recipes for the chosen styles, if you want one to hand to another agent or builder
- `review_design`: after each section
- `check_contrast`: any new color pair
## Output template
```markdown
# Build notes
Stack and why. Deviations from tokens. Known gaps. How to run it.
```
## Gates
Rules to satisfy: `perf-core-first`, `a11y-native-first`, `a11y-semantic-structure`, `a11y-bypass-blocks`, `a11y-focus-visible`, `craft-relative-units-text` (read them with get_guidelines or rules/*.md).
- [ ] No raw hex values in components.
- [ ] Content and navigation work with JavaScript disabled.
- [ ] review_design shows no blocker failures.
## Done when
- The page runs locally, matches the tokens and passes the blocker review.
## Pitfalls
- Building in one giant pass without reviewing.
- Adding ARIA to compensate for non-semantic markup.

# Step: Remove what the build does not need (`realize-subtract`, stage realize)
**Goal:** Take out the extra copy, lines, icons, metadata and decoration that building added, until every element earns its place.
**Your role:** Remove what the build does not need. Agents and first drafts add; this step only takes away.
**Inputs:** built-site, design-tokens  
**Output artifact:** subtract-log -> `design/06-realize/subtract-log.md`
## Procedure
1. List every element in each section of the built page at desktop and mobile: headings, lines of copy, icons, dividers, badges, labels, metadata, decorative shapes, hover effects, animations.
2. For each element ask: what job does it do for the visitor or the goal, and what is lost if it goes? Remove it if the answer is nothing, if another element already does the job, or if it only fills space. Prefer removing to restyling.
3. Watch for what builders add by habit: a second line of explanation under a clear heading, an icon on every list item, a divider between sections that already differ, metadata (dates, counts, tags) nobody asked for, a third button next to the primary action, repeated claims in different words.
4. Keep what the brief, the recipe or the quality bar requires (skip link, labels, alt text, legal lines), even if it looks like clutter. Removing a required element is a regression.
5. Never subtract the style. The lead object, the niche cue (motifs, pattern, palette), the atmosphere (backdrop, glow, texture) and the display type are what make the page look designed; they are not clutter. Remove habit-added extras and inconsistencies (a second style in one role, colliding parts, duplicate explanations), not richness. After subtracting, run compare_to_library and put the page beside its previous round: if the lead object shrank or the motifs went, put them back. In a real run a subtract-and-simplify round removed the florals, pattern and glow, and the owner's score fell from 6.5 to 5: "too simple, no style". [Our take]
6. Write the subtract log: each removal with a reason, and each element kept on the edge with the job it does. Re-run review_design: the removals must not have introduced failures.
## Tools
- `review_design`: after the removals, desktop and mobile
## Output template
```markdown
# Subtract log
| Section | Element | Job it did | Verdict (removed / kept) | Reason |
|---|---|---|---|---|
## Kept on the edge (what job it does)
## Review after removals (blockers, majors)
```
## Gates
Rules to satisfy: `distinct-swap-test` (read them with get_guidelines or rules/*.md).
- [ ] Every section was walked element by element, at both sizes.
- [ ] At least one thing was removed from each section, or the log says why nothing could go.
- [ ] No required element (skip link, label, alt text, legal line) was removed.
- [ ] review_design shows no new failures.
## Done when
- The subtract log exists and the page was re-reviewed after the removals.
## Pitfalls
- Restyling an unneeded element instead of removing it.
- Removing something the quality bar requires.
- Doing this only on the hero.

# Step: Look at every state and keep a papercut log (`realize-sweep`, stage realize)
**Goal:** Capture every state of every section and breakpoint, review the build's own trail for surprises, and record small issues in a log that carries into the next round.
**Your role:** Look at every state of the page once, on purpose, and keep a log of the small issues so they are fixed together instead of one reaction at a time.
**Inputs:** built-site, subtract-log  
**Output artifact:** state-sweep, papercut-log -> `design/06-realize/state-sweep.md`
## Procedure
1. Review the build's own trail first: the commit list, the build notes, the changelog of deviations, and any screenshots or logs the build produced. Look for anything you did not expect (a component you did not plan, a dependency, a new section, a changed token). A surprise means the brief or the direction was not understood: go back to the decision and the brief before polishing.
2. List every state the page can be in: each section; hover, focus, active and disabled controls; menus and dialogs opened; forms empty, filled, with an error, and submitted; loading and empty content; reduced motion; no JavaScript; dark scheme if present; widths 320, 390, 768, 1440; text at 200%.
3. Capture a screenshot of each state, grouped by section, and note any bug met on the way (broken link, overflow, wrong state, console error). Use a browser tool or Playwright; a state you cannot reach is listed as not seen, not skipped silently.
4. Skim the set once for surprises (not details): are these the screens you expected? Then go through it marking small, obvious fixes and fix them at once.
5. Anything small that is not obvious, or that touches the design (spacing rhythm, label wording, a colour that is a little off), goes in the papercut log instead of a spot fix. Spot fixes made one at a time drift the page away from its constraints.
6. Shared chrome changed (header, footer, navigation, a theme applied site-wide)? It touches every page and moves the done bar from one file to many (in a test, eleven edits outside the homepage): confirm with the owner up front that the done bar may touch it. Also audit one inner page, and list the accessibility problems that were already in the shared chrome (focus ring, small targets, controls dead without JavaScript) separately from the ones this work introduced, so old debts are visible and not mistaken for regressions. Compare with the baseline audit.
7. Detail pass (what separates agency-grade from cheap): no default-looking controls (style native date, select and file inputs; buttons with a clear primary, secondary and text hierarchy), small labels set deliberately (small caps or tracked caps, numerals for steps), hairline rules and frames that give structure, real images framed or cropped on purpose, illustration with fills and layers rather than single thin strokes, hover and focus states designed rather than inherited, and secondary text large enough to hold its own beside the display type. Compare each section with its anchor's section crop (get_section) and list the details the anchor has that the page lacks. In a real run the owner scored a page with restored richness 7/10 and said "still feels cheap, lack of details". [Our take]
8. Conversion pass: the capture named in the brief is in the first screen, repeated after each major section and in a closing band; the value exchange sits next to each form; the success and error states are honest; any proof is real (unconfirmed counts stay marked). [Our take]
9. Density check: count words and links per screen at 1440 and 390. More than about 150 words or 30 links in one screen is overloaded: move, group or cut, and say what you moved. [Our take]
10. Choose the crux surfaces named in direction-decision.md (the one or two the page stands or falls on, for example the hero and the booking path) and give them a longer pass: other variants, other copy, the details.
## Tools
- `review_design`: after the fixes
- `get_design_brief`: to compare a captured reference's states with yours, when a reference was used
## Output template
```markdown
# State sweep
## Surprises in the build's trail (and what they mean for the brief)
## States seen (section, state, width, screenshot file) and states not seen
## Bugs met on the way
## Fixed at once
## Crux surfaces: what was polished
## Papercut log (kept in design/papercuts.md; each: where, what, why it matters, date)
```
## Gates
- [ ] Every state in the list has a screenshot or is named as not seen.
- [ ] Bugs found on the way are listed, not only design notes.
- [ ] Small non-obvious issues are in design/papercuts.md, not fixed ad hoc.
- [ ] The crux surfaces are named and were polished.
## Done when
- The state sweep exists with screenshots, bugs and the papercut log; surprises were resolved or sent back to the brief.
## Pitfalls
- Checking only the default state at desktop width.
- Fixing each papercut the moment it is seen and drifting from the tokens.
- Skipping the trail review and polishing a feature nobody planned.

# Step: Check accessibility, performance and SEO (`realize-qa`, stage realize)
**Goal:** Test contrast (WCAG 2.2 AA: 4.5:1 for normal text, 3:1 for large), keyboard use, reduced-motion behavior, Core Web Vitals (LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1 at the 75th percentile), metadata and responsiveness.
**Your role:** Prove the build against the Quality Bar. Automated results are a baseline, not a verdict.
**Inputs:** built-site, success-criteria  
**Output artifact:** qa-report -> `design/06-realize/qa-report.md`
## Procedure
1. Measure a production build behind compression: a static export served by a plain local server sends files uncompressed, and on a throttled phone that read as a 5 to 6 s first paint for a page that paints in 1.4 s with gzip. Serve it with `pnpm --silent --filter @whata/audit serve <out dir> [port]` (gzip, like a CDN), or measure the deployed preview.
2. Critic pass (get_critic_brief): build for production, shoot desktop, mobile, reduced motion and keyboard states, and give a fresh subagent the critic brief and the screenshots only. Every category (Design, Usability, Creativity, Content) must reach 8 with evidence; its fix list is the next pass, and its one-line reading of the idea must match the concept. At least two passes; a new critic each time. Finish with 'remove one accessory'. Record the scores in design/06-realize/critic.md as a model's scores.
3. Run review_design (or the audit CLI) on desktop and mobile; list every failure and every rule that needs a person. A rule the audit did not evaluate is not a pass: the audit lists the rules it skipped, and '0 failures' only means none of the rules it did check failed. Serve the build over http (not file://) so stylesheets load.
4. State and keyboard checks are owned by realize-sweep when it ran (states, widths, 200% text, reduced motion, no-JS): link to its state-sweep.md instead of repeating them, and do here only the checks the sweep does not cover (screen reader or accessibility tree, forced colours, performance, the rest of this list).
5. Do the manual list. Owned by realize-sweep when it ran, so link and do not repeat: keyboard-only pass, text at 200%, 320 px reflow, reduced motion, dark mode, no-JS load. Owned here: a screen reader smoke test (VoiceOver: headings, landmarks, links, forms, dialogs; if you cannot run a screen reader, read the accessibility tree with Playwright's `page.accessibility.snapshot()` or `locator.ariaSnapshot()` for headings, landmarks, names, roles and states, and record the result as `accessibility tree only, not a screen reader test`: it is not a substitute and the owner should have someone run VoiceOver or NVDA); zoom 400%; text spacing override; forced colors; slow network. When the sweep did not run, do the owned-by-sweep checks here as well. [Standard + Craft]
6. Give the audit an absolute path for a local file (in the pilot a relative path was resolved from the audit package folder, not from the working folder, the page did not load, and fake findings were printed); if the report says the page failed to load, its findings are not about your page: fix the path and run again.
7. Reflow and text stress: if the audit lists a 320 px or 200% text overflow (a sideways scroll at 320 px, at 200% text size or with text spacing) as `check` ("needs a person"), do not read it as a pass: a measured overflow is a failure of `a11y-reflow`. Fix it (grid `minmax(0, 1fr)`, `overflow-wrap`, wrapping flex rows) or justify the exception in writing with the measured width, then run the audit again. [Our take]
8. Reflow culprit: the audit names the first element that overflows, not the cause, and the named element can change while the overflow width stays the same. Find the cause by bisecting: hide sections one at a time until the overflow drops, then hide inside that section. Typical culprits are a long word in a footer paragraph, a heading in a wide display face, a table and a field row.
9. Audit a production build when one is possible: the dev server's overlay or indicator can widen the page at 200% text and show up as a false overflow. If the build cannot run (no disk, no secrets), say so, run typecheck, lint and a dev-server render, name any dev-only indicator as a known false source, and mark performance `unmeasured`.
10. Gaps the audit may leave: read the audit's `not evaluated` list. If it lists `ux-primary-cta-above-fold` (a major rule), check the first viewport by screenshot at 390x844 and 1440x900 and confirm the primary action is fully visible without scrolling at both: a page can pass every automated check and still have its button below the fold on a phone. Do the same by hand for any of these the audit lists as not evaluated: `craft-body-size-min` (computed font size of running text, at 320 and 1280 px; 14 px is our review threshold, not a standard) and `craft-breakpoints-content-based` (sweep the width from 320 to 1920 px in steps of about 40 px and look for horizontal scroll, overlaps and clipped text). Record each as a manual check with the method.
11. `--verified` entries: say in `by` whether a person or a model verified the rule (for example `model: <name>` or `person: <name>`). A model's check is a model review, not a person's; rules that need real people (screen reader, test with people) cannot honestly be verified this way and stay open.
12. Lead element and the page below it: confirm the lead element is in the first viewport at both sizes, and describe in two or three sentences what the page looks like below the hero. The lead element must also recur or be answered lower on the page (a second moment), and the sections below the hero must differ in structure from each other (not a plain run of headings and paragraphs, not the same card repeated). If the page below the hero is a plain sequence, say so and fix it or record it as an open issue. Automated checks cannot see this. [Our take]
13. Check performance (lab Web Vitals: LCP 2.5 s, CLS 0.1; INP needs field data), page weight, fonts, images.
14. Frequency and absolute words ('every week', 'daily', 'always', 'never', 'all') are claims too: check each against the data (post dates, release logs, order counts) and use the measured wording ('most weeks', 'about 1.5 a week').
15. Check copy against the copy rules (specific, plain, consistent) and distinctiveness (swap test, defaults justified).
16. Inherited or new: before you change anything, save an audit of the current page (`pnpm --silent --filter @whata/audit cli <url> --out design/00-baseline/audit.json`), then run review_design with `baseline` set to that file so the report splits failures into new, inherited and fixed. Inherited failures in shared chrome (header, footer, global tokens) are listed separately with whether need-constraints allows you to change them; they are not passes, and new failures are yours to fix.
17. Type census and header: run `pnpm --silent --filter @whata/audit cli types <url>` (one style per role, peers in a list alike, first-screen counts) and `cli widths <url>` (now 320, 390, 768, 1024, 1280, 1440 and 320 at 200% text, with overlapping text caught). Look at screenshots of the header at 1440, 1280, 1100, 1024 and 390: shared chrome that passes every rule can still collide between breakpoints. When the chrome is in scope and broken, the kit header (get_base) is the replacement.
18. Content coverage (when need-statement's scope keeps any content): run `pnpm --silent --filter @whata/audit cli coverage <old url> <new url>`. Every block it lists as missing or partly kept must be explained by content-map.md (moved, reworked in scope, or dropped by the owner); with `SEO: keep`, every SEO field must be `same` and no internal link lost. Paste the summary line into the QA report.
19. Count the unconfirmed facts still on the page (the `.assumed` marks) and list them in the QA report; they are open issues, not passes.
20. Fix blockers and majors; list the rest with owners.
21. Say honestly what the result is. With no owner sign-off, no user test and no screen-reader run, the status is `built, audited, not approved`, with the list of what was not done.
## Sections track (default)
Applies only when the owner and you chose the sections track. In full, sprint and lean tracks ignore this section.
- success-criteria is replaced by the Success section of the brief.
- Check the design system held: `pnpm --silent --filter @whata/audit cli types <url>` reports no mixed role group (a display-size closing line is the one allowed exception), and the page uses one section ground, at most two corner radii for controls and media, and only the primary and secondary buttons. Fix through tokens or roles.css, never per section.
- The audits are checks on a finished look, not a source of it. Fix every blocker. Where a fix would change a section's pinned design, prefer the accessible version and record the deviation in that section's spec under 'Accessibility changes from the source'; where the design is the source's and the rule is a heuristic (small text inside decorative product UI, a nested panel), record it as justified with the reason.
- Close with the owner's score (record_taste type score, round = the section ids). Below the previous round: compare section by section with the sources before changing anything; never add rules to rescue a section.
## Sprint track (five-day)
Applies only when the owner and you chose the sprint track. In lean and full tracks ignore this section.
- realize-qa is not optional in the sprint: the prototype had only a blocker review before the Day 5 test. Run the whole step on the finished build, and report the status honestly (`built, audited, not approved` with no owner and no test). Day 5's `UNTESTED` stays in the report.
## Tools
- `review_design`: the built page; use an absolute file path or an http URL; desktop and mobile
- `get_critic_brief`: the brief and rubric for a fresh critic subagent; 8 or above in every category
## Output template
```markdown
# QA report
- Automated: blockers [n], majors [n], needs a person [n]
## Manual checks (result per check; method and who: person or model)
## Lead element and below the hero (above the fold at 390x844 and 1440x900? second moment? do the sections differ?)
## Content coverage (scope, coverage %, unexplained missing blocks, SEO fields changed, links lost)
## Inherited failures (shared chrome; may change? yes / no)
## Unconfirmed facts still on the page
## Status (built, audited, not approved | approved by [name, date])
## Performance (lab)
## Copy and distinctiveness
## Open issues (severity, owner)
```
## Gates
Rules to satisfy: `a11y-test-manually`, `a11y-test-with-people`, `perf-lcp`, `perf-cls`, `distinct-swap-test` (read them with get_guidelines or rules/*.md).
- [ ] Zero blocker failures remain.
- [ ] Every manual check has a recorded result and says whether a person or a model did it.
- [ ] The primary action is checked in the first viewport at 390x844 and 1440x900 (by screenshot when the audit does not evaluate it).
- [ ] The lead element is above the fold and recurs lower; the sections below the hero differ in structure.
## Done when
- No blocker failures; majors fixed or accepted by the owner in writing.
## Pitfalls
- Stopping at a green automated run.
- Reading the audit's `0 failures` when the page never loaded or the rule was not evaluated.
- Calling a model's check `verified by hand` without saying a model did it.
- A strong hero over a plain typographic sequence.

# Step: Hand off and launch (`realize-launch`, stage realize)
**Goal:** Release, redirect, monitor and hand over the files and guidelines.
**Your role:** Release safely and leave the next person (or agent) what they need to maintain the design.
**Inputs:** built-site, qa-report  
**Output artifact:** launched-site -> `design/06-realize/launched-site.md`
## Procedure
1. Pre-launch checklist: title, description, language, favicon, social image, 404 page, redirects, robots, analytics (only if wanted), consent if required, performance on the production build.
2. Refuse to launch while any unconfirmed fact remains: search the built page for the `.assumed` marker (and the legend), and read design/OPEN-QUESTIONS.md. Each marked fact must be confirmed by the owner and its marker removed, or the fact removed; if any remain, stop and report them to the owner instead of deploying. Also search for brackets, `lorem`, and example domains (`.example`) in addresses and links. [Our take]
3. Advice copy: find every passage that gives legal, medical, financial or safety advice and the draft marker on it. Each needs a qualified reviewer's sign-off recorded (name, date) in design/OPEN-QUESTIONS.md before the marker is removed. Without that sign-off the page does not ship with the advice as final; remove the passage or ship it as a clearly marked draft only if the owner agrees in writing. (`copy-expert-review-before-launch`) [Our take]
4. Deploy per the constraints; re-run review_design against the live URL.
5. Hand over: design-tokens folder, DESIGN.md, component notes, QA report, how to update content, known issues.
## Ask the owner (only what you cannot default)
- Deploy where and when? (a) not yet: I hand over a built, audited page for your review (recommended) (b) deploy to [target] on [date].
## Tools
- `review_design`: the live URL
## Output template
```markdown
# Launch
- URL and date:
- What shipped:
- Live review summary:
- Handover notes:
```
## Gates
Rules to satisfy: `a11y-page-title`, `a11y-lang`, `perf-lcp`, `copy-expert-review-before-launch` (read them with get_guidelines or rules/*.md).
- [ ] The live URL passes the same review as the build.
- [ ] No `.assumed` marker, legend or open question about a fact remains on the shipped page.
- [ ] Every passage of legal, medical, financial or safety advice has a recorded qualified reviewer, or is not shipped as final.
## Done when
- The site is live, reviewed in production and documented.
## Pitfalls
- Launching without re-testing the production build.
- Shipping dotted-underline facts the owner never confirmed, or an example email address.

# Step: Measure (`reflect-measure`, stage reflect)
**Goal:** Compare real results with the success criteria.
**Your role:** Compare real results with the success criteria after enough time has passed.
**Inputs:** launched-site, success-criteria  
**Output artifact:** metrics-report -> `design/07-reflect/metrics-report.md`
## Procedure
1. Ask the owner for the measures named in the success criteria after an agreed period (for example four weeks).
2. Compare each result with its target. Note what you cannot conclude (sample too small, no baseline, seasonal effects).
3. Re-run review_design on the live site; compare with launch.
## Ask the owner (only what you cannot default)
- Can you share the numbers for the success measures? (a) yes, the last four weeks from [analytics tool] (recommended) (b) not yet: I list what to collect.
## Tools
- `review_design`: live URL
## Output template
```markdown
# Metrics report
| Criterion | Target | Result | Verdict | Caveat |
|---|---|---|---|---|
```
## Gates
- [ ] Each criterion has a result or a stated reason for none.
## Done when
- Every success criterion is compared with a result.
## Pitfalls
- Claiming causes without a baseline.

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

# Step: Archive as a case study (`reflect-archive`, stage reflect)
**Goal:** Write up the project: brief, directions, decision, result. Add the site to the library.
**Your role:** Write the case study and teach the library: add the finished site so future projects can use it as a reference.
**Inputs:** launched-site, direction-decision, retro-notes  
**Output artifact:** case-study -> `design/07-reflect/case-study.md`
## Procedure
1. Write a one-page case study: need, brief, the three directions, the decision, results, what you would do differently.
2. Add the live site to the gallery (skip if you may not write to the library; then write the entry as a ready-to-run command list for the owner): pnpm site add <url>, capture and audit run automatically; write the tags with its facts and apply them with status review.
3. Write its style record from the design tokens and the decision log (pnpm site style).
## Output template
```markdown
# Case study
Need > brief > directions > decision > result > lessons.
```
## Gates
- [ ] The site is in the library with tags and a style record.
## Done when
- The case study exists and the site is in the library.
## Pitfalls
- Skipping the archive: the library only improves if finished work goes back in.



# BLOCKER RULES

# Blocker rules (35)
Zero of these may fail before anything is called done.

### `a11y-accessible-auth` [blocker · standard]
Login does not require remembering, solving puzzles or transcribing, unless an alternative or helper exists (password managers, paste, passkeys). (WCAG 3.3.8, AA, new in 2.2)
- Why: Cognitive tests block many people.
- Check (manual): Check that password fields allow paste and autofill, and that CAPTCHAs have alternatives.
- While designing: Allow password managers, paste and passkeys; do not require memory, puzzles or transcription to log in.
- Sources: wcag-22-quickref, wcag-22-new

### `a11y-alt-text` [blocker · standard]
Every informative image has a text alternative that serves the same purpose; purely decorative images have an empty alt so they are skipped. (WCAG 1.1.1, A)
- Why: People who cannot see an image still need what it conveys. Missing alt text appears on 53.1% of analyzed home pages.
- Check (hybrid): Automated check finds missing alt (axe `image-alt`); a person judges whether the text actually matches the purpose. (tools: axe-core)
- While designing: Give every informative image alt text that states what it conveys; use alt="" for decorative images; never leave alt missing.
- Sources: wcag-22-quickref, webaim-million

### `a11y-audio-control` [blocker · standard]
Audio that plays automatically for more than 3 seconds can be paused or stopped, or its volume controlled separately from the system volume. (WCAG 1.4.2, A)
- Why: Autoplaying sound interferes with screen readers and with people who cannot easily find the source.
- Check (manual): Load the page with sound on; check for autoplaying audio and its controls.
- While designing: Never autoplay audio; autoplay video muted and provide a control to start sound.
- Often conflicts with styles: hero-video, ambient-loop
- Sources: wcag-22-quickref

### `a11y-audio-description` [blocker · standard]
Prerecorded video has audio description or a text alternative covering the visual content. (WCAG 1.2.3 A, 1.2.5 AA)
- Why: Blind and low-vision people miss information that is only shown.
- Check (manual): Check whether key visual information is described by narration, a description track or a transcript. WCAG 1.2.1 requires an alternative or audio track for prerecorded video-only content and its Understanding page does not exempt decorative or background video; 1.1.1 says pure decoration should be ignorable by assistive technology. Treating a purely decorative loop as decoration is an inference from 1.1.1.
- While designing: Describe key visual information in video through narration, a description track or a transcript.
- Often conflicts with styles: hero-video
- Sources: wcag-22-quickref, wcag-understanding-video-only, wcag-understanding-non-text-content

### `a11y-bypass-blocks` [blocker · standard]
A mechanism, such as a skip link or correct landmarks and headings, lets users skip repeated blocks. (WCAG 2.4.1, A)
- Why: Keyboard and screen reader users should not tab through the full navigation every time.
- Check (hybrid): The skip link should be the first focusable control and may be visible only on focus; WCAG does not require it to be visible when it lacks focus (G1). Landmarks (ARIA11) or headings (H69) are also sufficient. WebAIM: a hidden skip link must become prominently visible on focus; do not use display:none or the hidden attribute; a skip link is not strictly required where a starting h1 or a main region meets the criterion. (tools: axe-core)
- While designing: Put a skip link first in the DOM with a z-index above hero layers, and use landmarks (header, nav, main, footer).
- Often conflicts with styles: hamburger-only
- Sources: wcag-22-quickref, wcag-understanding-bypass-blocks, axe-core-rule-descriptions, wcag-technique-g1, webaim-skip-navigation

### `a11y-captions` [blocker · standard]
Prerecorded video with sound has captions. (WCAG 1.2.2, A)
- Why: Deaf and hard-of-hearing people, and people watching without sound.
- Check (manual): Play every video with sound off; check captions exist and are accurate.
- While designing: Caption every video that has speech or meaningful sound; decorative silent loops need no captions but must not carry information.
- Often conflicts with styles: hero-video
- Sources: wcag-22-quickref

### `a11y-captions-live` [blocker · standard]
Live audio in synchronized media (live stream, webinar, event broadcast) has captions that include speech, speaker identification and significant non-speech sounds.
- Why: WCAG 1.2.4 (AA). It targets broadcasts, not two-way calls in web apps; live means captured from a real event with at most a broadcast delay; fully generated content is not live.
- Check (manual): If the page embeds a live stream, enable captions in the player during the live event and confirm they track speech; otherwise mark not applicable. (tools: screen reader, video player controls)
- While designing: If you embed a live stream, use a player and a captioning service that supply live captions.
- Often conflicts with styles: hero-video, event-site
- Sources: wcag-understanding-captions-live, wcag-22-quickref

### `a11y-color-not-only` [blocker · standard]
Color is never the only way to show information, state, errors or required fields. (WCAG 1.4.1, A)
- Why: Color-blind and low-vision people, and monochrome displays.
- Check (manual): Use another cue wherever color carries meaning: text, an icon, underline, weight or pattern (techniques G14, G182). Error and required fields must not rely on color alone (F81); links in text must be distinguishable from surrounding text, for example 3:1 contrast against the text (G183) or another cue (F73). WCAG lists color-vision simulators for checking; grayscale is a quick approximation, not a WCAG test.
- While designing: Pair every color signal (state, error, link) with text, an icon, an underline or a pattern.
- Often conflicts with styles: monochrome, neon
- Sources: wcag-22-quickref, wcag-understanding-use-of-color

### `a11y-contrast-text` [blocker · standard]
Text has a contrast ratio of at least 4.5:1 against its background, or 3:1 for large text (18 pt, or 14 pt bold). (WCAG 1.4.3, AA)
- Why: Low-contrast text is the most common detected failure: 83.9% of analyzed home pages.
- Check (hybrid): Automated check (axe `color-contrast`) misses text over images and gradients; check those by hand, in all states and themes. (tools: axe-core)
- While designing: Keep text at 4.5:1 against its background (3:1 for large text); compute every pair with check_contrast and put text on solid surfaces or scrims, not directly on gradients, images or video.
- Often conflicts with styles: dark-cyber, neon, pastel, gradient-aurora, glassmorphism, grain-noise, quiet-luxury
- Sources: wcag-22-quickref, wcag-contrast-minimum, webaim-million

### `a11y-dragging` [blocker · standard]
Anything that needs dragging can also be done with a single press, without dragging. (WCAG 2.5.7, AA, new in 2.2)
- Why: Dragging is hard or impossible for some people.
- Check (manual): Check sliders, sortable lists and reveal-on-drag effects for a single-pointer alternative (buttons, tap-to-place, direct selection, typed value; technique G219). A keyboard alternative alone does not satisfy this criterion; controls must work with a pointer, though they may be visually hidden.
- While designing: Offer a single-pointer alternative (buttons, tap-to-place, typed value) for every drag interaction.
- Often conflicts with styles: drag-interaction, interactive-art
- Sources: wcag-22-quickref, wcag-22-new, wcag-understanding-dragging

### `a11y-error-identification` [blocker · standard]
Detected input errors are identified and described in text, and where possible a correction is suggested. (WCAG 3.3.1 A, 3.3.3 AA)
- Why: People need to know what went wrong and how to fix it.
- Check (manual): Submit forms with bad and empty input; each error is announced, specific and linked to its field.
- While designing: Describe each error in text next to its field, say what is wrong and how to fix it, and keep what the user typed.
- Sources: wcag-22-quickref, nng-web-forms

### `a11y-flashes` [blocker · standard]
Nothing flashes more than three times per second unless below the defined thresholds. (WCAG 2.3.1, A)
- Why: Flashing can trigger seizures.
- Check (manual): Pass if no more than three general or red flashes occur in any one second (content within that limit passes without a tool), or the flashes stay below the thresholds: a general flash is an opposing luminance change of at least 10% with the darker state below 0.80, and the flashing area stays within 0.006 steradians of a 10-degree field (WCAG estimates 341×256 px at 1024×768).
- While designing: Never flash content more than three times per second; keep glows static or slow.
- Often conflicts with styles: neon
- Sources: wcag-22-quickref, wcag-understanding-three-flashes

### `a11y-focus-not-obscured` [blocker · standard]
A focused element is not entirely hidden behind sticky headers, cookie banners or chat widgets. (WCAG 2.4.11, AA, new in 2.2)
- Why: Keyboard users lose their place when focus lands under an overlay.
- Check (manual): Tab through the page with sticky elements and banners present, at several viewport sizes. A focused item may be partly covered but not entirely (failure F110). Technique C43 (CSS scroll-padding) is the sufficient technique listed; a banner can also pass by being modal or closing when it loses focus.
- While designing: Add scroll-padding for sticky headers and avoid banners or widgets that cover focused elements.
- Often conflicts with styles: floating-dock
- Sources: wcag-22-quickref, wcag-22-new, wcag-understanding-focus-not-obscured

### `a11y-focus-order` [blocker · standard]
Keyboard focus moves in an order that keeps meaning and operability. (WCAG 2.4.3, A)
- Why: Random jumps disorient.
- Check (manual): Tab through the page and compare focus order with the visual and logical order.
- While designing: Keep focus order equal to the reading order; avoid positive tabindex.
- Often conflicts with styles: unconventional-layout, asymmetric
- Sources: wcag-22-quickref

### `a11y-focus-visible` [blocker · standard]
Every keyboard-operable element shows a visible focus indicator. (WCAG 2.4.7, AA)
- Why: Keyboard users must see where they are.
- Check (manual): Tab through the page; the focus indicator is always visible with 3:1 contrast against what it sits on, and `outline: none` is never left without a replacement. In forced-colors mode outline and border colors are forced to system colors and stay visible, while box-shadow is removed, so draw focus with outline or border, not box-shadow alone.
- While designing: Style :focus-visible with a solid, high-contrast outline and offset; never remove the outline without a replacement; use outline rather than box-shadow alone.
- Often conflicts with styles: minimal, dark-cyber
- Sources: wcag-22-quickref, mdn-focus-visible, mdn-forced-colors

### `a11y-keyboard` [blocker · standard]
All functionality can be operated with a keyboard alone. (WCAG 2.1.1, A)
- Why: Keyboard, switch and voice users.
- Check (manual): Tab, Shift+Tab, Enter, Space and arrow keys through the whole page, including menus and dialogs.
- While designing: Make every function work with the keyboard using native controls; test with Tab, Shift+Tab, Enter, Space and arrows.
- Often conflicts with styles: cursor-effects, drag-interaction, unusual-nav, interactive-art
- Sources: wcag-22-quickref

### `a11y-labels-instructions` [blocker · standard]
Every input has a visible label or instructions, and format requirements are stated before the user hits an error. (WCAG 3.3.2, A)
- Why: Missing form labels occur on 51% of analyzed home pages.
- Check (hybrid): Check every field for a programmatic label (axe `label`); placeholders do not count as labels. (tools: axe-core)
- While designing: Give every field a visible, persistent label; state format requirements before the user makes a mistake.
- Sources: wcag-22-quickref, nng-web-forms, webaim-million

### `a11y-lang` [blocker · standard]
The page declares its main language, and passages in another language are marked. (WCAG 3.1.1 A, 3.1.2 AA)
- Why: Screen readers pronounce text using the declared language. 13.5% of analyzed home pages lack it.
- Check (automated): Check `<html lang>` and `lang` on foreign phrases (axe `html-has-lang`, `html-lang-valid`). (tools: axe-core)
- While designing: Set <html lang> and mark passages in another language with lang.
- Sources: wcag-22-quickref, webaim-million

### `a11y-link-purpose` [blocker · standard]
The purpose of each link can be understood from its text, or from its text with its context. (WCAG 2.4.4, A)
- Why: Screen reader users list links out of context. Empty links appear on 46.3% of analyzed home pages.
- Check (hybrid): List all links; flag "click here", "more", and links with no name (axe `link-name`). (tools: axe-core)
- While designing: Make every link's text meaningful on its own; no 'click here' or 'read more' without context.
- Sources: wcag-22-quickref, nng-homepage-principles, webaim-million

### `a11y-meaningful-sequence` [blocker · standard]
The reading order in the code matches the meaning of the page, even if CSS moves things around visually. (WCAG 1.3.2, A)
- Why: Screen reader and keyboard users follow the code order.
- Check (manual): Compare DOM order with visual order. Failure F1 is positioning that changes meaning; technique C27 is making DOM order match visual order. MDN: CSS `order` changes only the visual order, not the logical or tab order, which creates a mismatch for screen reader and keyboard users. A check with CSS disabled is a practical test (not described on WCAG's page).
- While designing: Keep DOM order equal to reading order; do not use CSS order or absolute positioning to rearrange meaningful content.
- Often conflicts with styles: unconventional-layout, asymmetric
- Sources: wcag-22-quickref, wcag-understanding-meaningful-sequence, mdn-css-order

### `a11y-multiple-ways` [blocker · standard]
Each page in a set of pages (other than steps or results of a process) can be reached by at least two of: links from related pages, table of contents, site map, search, a list of links to all pages, or links to all pages from the home page.
- Why: WCAG 2.4.5 (AA). The Understanding page says very small sites can satisfy this with links from the home page. Example pairings: search plus category list.
- Check (manual): Pick 3 inner pages and show two independent routes to each (nav + search, nav + sitemap, home page links + previous/next). Process pages (checkout steps, search results) are exempt.
- While designing: Provide main navigation and a second route (search, sitemap or footer index) on every multi-page site.
- Often conflicts with styles: anchor-only, unusual-nav, hamburger-only, command-palette, unconventional-layout
- Sources: wcag-understanding-multiple-ways, wcag-22-quickref

### `a11y-name-role-value` [blocker · standard]
Every interface component exposes its name, role, state and value to assistive technology. (WCAG 4.1.2, A)
- Why: Custom widgets are invisible or confusing otherwise. Empty buttons appear on 30.6% of analyzed home pages.
- Check (hybrid): Inspect the accessibility tree; check icon buttons for names (axe `button-name`); test custom controls in a screen reader. (tools: axe-core)
- While designing: Use native elements; give custom controls a name, role and state; label icon-only buttons.
- Sources: wcag-22-quickref, webaim-million

### `a11y-no-keyboard-trap` [blocker · standard]
Keyboard focus can always be moved away from any component. (WCAG 2.1.2, A)
- Why: A trap locks users in.
- Check (manual): Tab through every widget, including embeds, modals and 3D canvases. Deliberately restricting focus (a modal dialog) is allowed if users can leave by Esc or buttons; any non-standard exit method must be explained to the user.
- While designing: Ensure focus can always leave a component; modals close with Escape and return focus.
- Often conflicts with styles: realtime-3d, hero-3d
- Sources: wcag-22-quickref, wcag-understanding-no-keyboard-trap

### `a11y-non-text-contrast` [blocker · standard]
UI components and graphics needed to understand the content have at least 3:1 contrast against adjacent colors. (WCAG 1.4.11, AA)
- Why: Buttons, inputs, focus rings and icons must be perceivable.
- Check (hybrid): Check borders of inputs, icon buttons, toggles and focus indicators; automated tools cover only part.
- While designing: Give input borders, icon buttons, toggles and focus indicators at least 3:1 contrast against their surroundings.
- Often conflicts with styles: minimal, glassmorphism, pastel
- Sources: wcag-22-quickref

### `a11y-on-focus-input` [blocker · standard]
Moving focus to, or changing the value of, a control does not by itself cause a major change of context such as navigation or opening a new window. (WCAG 3.2.1 A, 3.2.2 A)
- Why: Unexpected changes disorient keyboard and screen reader users.
- Check (manual): Tab through selects, radios and inputs; nothing submits or navigates without a deliberate action.
- While designing: Never change context (navigate, submit, open windows) just because an element received focus or changed value.
- Sources: wcag-22-quickref

### `a11y-page-title` [blocker · standard]
The page has a title that describes its purpose. (WCAG 2.4.2, A)
- Why: The title is the first thing a screen reader says and what appears in tabs and history.
- Check (automated): Check `<title>` is present, specific and different from other pages (axe `document-title`). (tools: axe-core)
- While designing: Give the page a specific <title> that names its purpose.
- Sources: wcag-22-quickref

### `a11y-pause-stop-hide` [blocker · standard]
Moving, blinking, scrolling or auto-updating content that starts automatically and runs alongside other content can be paused, stopped or hidden. (WCAG 2.2.2, A)
- Why: Motion distracts and can make content unreadable. WCAG 2.2.2 (see the Understanding page) sets the five-second threshold for automatically starting moving content.
- Check (manual): Applies to moving, blinking or scrolling content that starts automatically (including by hover, focus or scrolling into view), lasts more than five seconds and runs alongside other content; auto-updating content has no five-second exception. A control that pauses only while focused does not qualify. Best practice is one control for all moving content. Check carousels, background video, marquees and ambient animations.
- While designing: Give a visible, keyboard-reachable control to pause anything that moves automatically for more than five seconds (video, loops, tickers, carousels).
- Often conflicts with styles: marquee, ambient-loop, hero-video, parallax
- Sources: wcag-22-quickref, nng-homepage-principles, wcag-understanding-pause-stop-hide

### `a11y-pointer-gestures` [blocker · standard]
Anything that needs a multi-point or path-based gesture (pinch, swipe) can also be done with a single pointer, unless essential. (WCAG 2.5.1, A)
- Why: People with motor impairments cannot always do complex gestures.
- Check (manual): Check swipers, maps and sliders for single-tap alternatives.
- While designing: Offer a single-tap or button alternative for every swipe, pinch or path gesture.
- Often conflicts with styles: drag-interaction, horizontal-scroll
- Sources: wcag-22-quickref

### `a11y-reflow` [blocker · standard]
At 320 CSS pixels wide (400% zoom at 1280 px) content works without two-dimensional scrolling, apart from exceptions such as maps and wide tables. (WCAG 1.4.10, AA)
- Why: People with low vision zoom in and rely on a single column.
- Check (manual): Set the viewport to 320 px wide (vertical scrolling content) and 256 px tall (horizontal scrolling content); ordinary content must not need two-dimensional scrolling. Exceptions: maps, diagrams, video, games, presentations, data tables, toolbar-in-view interfaces. A horizontal carousel passes if each panel fits 320 px; a table in its own scroll container passes if the content around it reflows. Also run it at 320 px with the root font size at 200% (and with the WCAG text-spacing overrides applied): fixed rem tracks (minmax(15rem,1fr) is 480 px at 200%), padding that leaves a 96 px column, and display words wider than the viewport are the usual causes. Measured in Chrome on the 2026-11 recipe demos: this extra pass found overflow in 11 of 18 demos that passed the plain 320 px check.
- While designing: Make the layout work at 320 CSS px wide without sideways scrolling, also when the root text size is 200%: write grid tracks as minmax(min(Nrem, 100%), 1fr), give headings and long strings overflow-wrap: anywhere, step display sizes down in a rem media query (max-width: 30rem) instead of clamp() with vw, cut container padding under 30rem, let flex rows wrap (inputs and buttons in a row: flex: 1 1 6rem; min-width: 0, not a 12rem basis that cannot shrink; nav and pill lists get flex-wrap: wrap), and put wide tables or galleries in their own focusable scroll region (role=region, aria-label, tabindex=0).
- Often conflicts with styles: horizontal-scroll, split-screen, app-shell
- Sources: wcag-22-quickref, wcag-understanding-reflow

### `a11y-resize-text` [blocker · standard]
Text can be enlarged to 200% by the browser without losing content or function. (WCAG 1.4.4, AA)
- Why: Many people enlarge text.
- Check (manual): WCAG's pass condition: text can be scaled to 200% using at least one scaling mechanism browsers offer (page zoom, text-only zoom, a larger default font size), with no loss of content or function. Text may shrink at smaller breakpoints if 200% is still reachable; the example is 20 px at 100% in a 1280 px window needing to display at twice that size when enlarged. Viewport-unit-only sizing is a listed failure (F94). Measured 2026-11-05: stepped rem sizes doubled under text-only enlargement; vw-only did not change; a clamp() with a vw term grew 1.14× (see content/learn/measurements).
- While designing: Size text in rem or em; never in viewport units alone; check the page at 200% text size without clipping.
- Often conflicts with styles: oversized-type
- Sources: wcag-22-quickref, wcag-understanding-resize-text

### `a11y-semantic-structure` [blocker · standard]
Structure that is visible (headings, lists, tables, form labels, regions) is also in the markup, not only in the styling. (WCAG 1.3.1, A)
- Why: Assistive technology navigates by structure.
- Check (hybrid): Automated checks for headings, lists, labels and landmarks; read the page outline in a screen reader or the accessibility tree. (tools: axe-core)
- While designing: Use real headings, lists, tables, labels and landmarks in the markup; never fake structure with styling.
- Sources: wcag-22-quickref

### `a11y-status-messages` [blocker · standard]
Status messages (success, errors, progress, results counts) are announced by assistive technology without moving focus. (WCAG 4.1.3, AA)
- Why: Without it, screen reader users miss feedback.
- Check (manual): Trigger form confirmations, loading and search-result updates with a screen reader running.
- While designing: Announce success, error and progress messages through a live region without moving focus.
- Sources: wcag-22-quickref

### `a11y-target-size` [blocker · standard]
Pointer targets are at least 24 by 24 CSS pixels, or have enough spacing around them, with listed exceptions. (WCAG 2.5.8, AA, new in 2.2)
- Why: Small targets are hard to hit with a finger, a tremor or a pointer.
- Check (hybrid): Measure icon buttons, close buttons, footer links and inline controls. axe `target-size` is disabled by default, so enable it. Exceptions: spacing (a 24 px circle centered on an undersized target must not touch another target or its circle; 20×20 px buttons with a 4 px gap pass, with no gap they fail), equivalent control, inline text, user-agent controls, essential. (tools: axe-core)
- While designing: Make pointer targets at least 24 by 24 CSS px, or space undersized ones so a 24 px circle around each does not overlap another; use 44 px for primary actions.
- Often conflicts with styles: minimal
- Sources: wcag-22-quickref, wcag-22-new, wcag-understanding-target-size, axe-core-rule-descriptions

### `a11y-text-spacing` [blocker · standard]
Content still works when users override line height, paragraph, letter and word spacing. (WCAG 1.4.12, AA)
- Why: People with dyslexia and low vision change spacing.
- Check (manual): Apply a text-spacing bookmarklet or user stylesheet; check for clipped or overlapping text.
- While designing: Do not clip text in fixed-height containers; test with line height 1.5, letter spacing 0.12em, word spacing 0.16em.
- Sources: wcag-22-quickref

### `comp-dialog-focus` [blocker · standard]
Opening a modal dialog moves focus into it, Tab and Shift+Tab cycle only within it, Escape closes it, a visible close or Cancel button exists, and closing returns focus to the control that opened it (or to a logical next target if that control is gone).
- Why: These are the APG keyboard and focus rules for modal dialogs; the close button is 'strongly recommended' there. Initial focus guidance: first focusable by default; a static start element for long or structured content; least destructive action for irreversible steps.
- Check (manual): Keyboard only: activate the opener, verify focus is inside; Tab through the whole dialog and confirm wrap; press Escape and confirm close and focus on the opener; confirm a visible close control exists. (tools: keyboard, playwright)
- While designing: On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- Often conflicts with styles: glassmorphism, interactive-art
- Sources: apg-dialog-modal, wcag-22-quickref



# BUILD CHEAT SHEET

# Build cheat sheet: what to do while designing and building (blockers and majors, then all COGA rules)

## accessibility / understandable
- [blocker] `a11y-accessible-auth`: Allow password managers, paste and passkeys; do not require memory, puzzles or transcription to log in.
- [blocker] `a11y-error-identification`: Describe each error in text next to its field, say what is wrong and how to fix it, and keep what the user typed.
- [blocker] `a11y-labels-instructions`: Give every field a visible, persistent label; state format requirements before the user makes a mistake.
- [blocker] `a11y-lang`: Set <html lang> and mark passages in another language with lang.
- [blocker] `a11y-on-focus-input`: Never change context (navigate, submit, open windows) just because an element received focus or changed value.
- [major] `a11y-consistent`: Keep navigation order, component names and help links consistent across pages.
- [major] `a11y-error-prevention`: Let users review, confirm or undo submissions with legal, financial or data effects.
- [major] `a11y-redundant-entry`: Do not ask for information the user already gave in the same process; prefill or let them select it.

## accessibility / perceivable
- [blocker] `a11y-alt-text`: Give every informative image alt text that states what it conveys; use alt="" for decorative images; never leave alt missing.
- [blocker] `a11y-audio-control`: Never autoplay audio; autoplay video muted and provide a control to start sound.
- [blocker] `a11y-audio-description`: Describe key visual information in video through narration, a description track or a transcript.
- [blocker] `a11y-captions`: Caption every video that has speech or meaningful sound; decorative silent loops need no captions but must not carry information.
- [blocker] `a11y-color-not-only`: Pair every color signal (state, error, link) with text, an icon, an underline or a pattern.
- [blocker] `a11y-contrast-text`: Keep text at 4.5:1 against its background (3:1 for large text); compute every pair with check_contrast and put text on solid surfaces or scrims, not directly on gradients, images or video.
- [blocker] `a11y-meaningful-sequence`: Keep DOM order equal to reading order; do not use CSS order or absolute positioning to rearrange meaningful content.
- [blocker] `a11y-non-text-contrast`: Give input borders, icon buttons, toggles and focus indicators at least 3:1 contrast against their surroundings.
- [blocker] `a11y-reflow`: Make the layout work at 320 CSS px wide without sideways scrolling, also when the root text size is 200%: write grid tracks as minmax(min(Nrem, 100%), 1fr), give headings and long strings overflow-wrap: anywhere, step display sizes down in a rem media query (max-width: 30rem) instead of clamp() with vw, cut container padding under 30rem, let flex rows wrap (inputs and buttons in a row: flex: 1 1 6rem; min-width: 0, not a 12rem basis that cannot shrink; nav and pill lists get flex-wrap: wrap), and put wide tables or galleries in their own focusable scroll region (role=region, aria-label, tabindex=0).
- [blocker] `a11y-resize-text`: Size text in rem or em; never in viewport units alone; check the page at 200% text size without clipping.
- [blocker] `a11y-semantic-structure`: Use real headings, lists, tables, labels and landmarks in the markup; never fake structure with styling.
- [blocker] `a11y-text-spacing`: Do not clip text in fixed-height containers; test with line height 1.5, letter spacing 0.12em, word spacing 0.16em.
- [major] `a11y-hover-focus-content`: Make hover or focus content (tooltips, menus) dismissible with Escape, hoverable, and persistent until dismissed.
- [major] `a11y-images-of-text`: Use real text for headlines, buttons and navigation; images of text only for logotypes.
- [major] `a11y-input-purpose`: Add the correct autocomplete value to fields that collect personal data (name, email, address, phone).
- [major] `a11y-no-sensory-only`: Write instructions that work without seeing shape, color or position: name the control, not its look or place.
- [major] `a11y-orientation`: Do not lock the page to portrait or landscape.

## accessibility / operable
- [blocker] `a11y-bypass-blocks`: Put a skip link first in the DOM with a z-index above hero layers, and use landmarks (header, nav, main, footer).
- [blocker] `a11y-dragging`: Offer a single-pointer alternative (buttons, tap-to-place, typed value) for every drag interaction.
- [blocker] `a11y-flashes`: Never flash content more than three times per second; keep glows static or slow.
- [blocker] `a11y-focus-not-obscured`: Add scroll-padding for sticky headers and avoid banners or widgets that cover focused elements.
- [blocker] `a11y-focus-order`: Keep focus order equal to the reading order; avoid positive tabindex.
- [blocker] `a11y-focus-visible`: Style :focus-visible with a solid, high-contrast outline and offset; never remove the outline without a replacement; use outline rather than box-shadow alone.
- [blocker] `a11y-keyboard`: Make every function work with the keyboard using native controls; test with Tab, Shift+Tab, Enter, Space and arrows.
- [blocker] `a11y-link-purpose`: Make every link's text meaningful on its own; no 'click here' or 'read more' without context.
- [blocker] `a11y-no-keyboard-trap`: Ensure focus can always leave a component; modals close with Escape and return focus.
- [blocker] `a11y-page-title`: Give the page a specific <title> that names its purpose.
- [blocker] `a11y-pause-stop-hide`: Give a visible, keyboard-reachable control to pause anything that moves automatically for more than five seconds (video, loops, tickers, carousels).
- [blocker] `a11y-pointer-gestures`: Offer a single-tap or button alternative for every swipe, pinch or path gesture.
- [blocker] `a11y-target-size`: Make pointer targets at least 24 by 24 CSS px, or space undersized ones so a 24 px circle around each does not overlap another; use 44 px for primary actions.
- [major] `a11y-char-shortcuts`: Avoid single-key shortcuts, or let users turn them off or remap them, or make them work only while their component has focus.
- [major] `a11y-headings-labels`: Write headings and labels that describe their topic; keep one h1 and a logical heading order.
- [major] `a11y-label-in-name`: Make a control's accessible name start with or include its visible label text.
- [major] `a11y-pointer-cancellation`: Trigger actions on release (click), not on press, so they can be cancelled.
- [major] `a11y-timing`: Avoid time limits; if one is needed let the user turn it off, adjust or extend it.

## components / Media
- [blocker] `a11y-captions-live`: If you embed a live stream, use a player and a captioning service that supply live captions.

## components / Navigation
- [blocker] `a11y-multiple-ways`: Provide main navigation and a second route (search, sitemap or footer index) on every multi-page site.

## accessibility / robust
- [blocker] `a11y-name-role-value`: Use native elements; give custom controls a name, role and state; label icon-only buttons.
- [blocker] `a11y-status-messages`: Announce success, error and progress messages through a live region without moving focus.

## components / Modal dialog
- [blocker] `comp-dialog-focus`: On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- [major] `comp-dialog-semantics`: Build modals with a titled dialog element or role=dialog plus aria-labelledby, and keep all its controls inside it.
- [major] `comp-dialog-truly-modal`: Make the background inert and dimmed whenever the dialog is modal; for popovers that leave the page usable, do not set aria-modal.

## components / Cognitive accessibility: memory
- [major] `a11y-coga-allow-paste-autofill`: Never block paste on inputs and set autocomplete tokens on every credential and contact field.

## accessibility / practice
- [major] `a11y-native-first`: Use native HTML elements before ARIA; no ARIA is better than bad ARIA.
- [major] `a11y-reduced-motion`: Under prefers-reduced-motion replace large movement with fades or stills and keep what the motion conveyed; keep logo, tagline and headline static.
- [major] `a11y-role-is-a-promise`: If you add an ARIA role, implement its keyboard behavior and states from the matching APG pattern.
- [major] `a11y-test-manually`: Run automated checks, then test by keyboard, screen reader, zoom and text spacing; automated tools miss errors.
- [major] `a11y-test-with-people`: Include people who use assistive technology in testing; plan an audit before launch.

## components / Status messages
- [major] `a11y-status-role-choice`: Default to role=status; use role=alert only for errors the user must act on now.

## components / Accordion / collapsible sections
- [major] `comp-accordion-markup`: Write accordions as h3 > button[aria-expanded] followed by a div that gets the hidden attribute when collapsed; if content must show without JS, ship plain h3 + div and let the script add the button and the hidden state.
- [major] `comp-accordion-no-hidden-focusables`: Collapse panels with the hidden attribute (or display:none), never by height:0 alone.

## components / Alert / notifications
- [major] `comp-alert-no-focus-no-autodismiss`: Show messages in a live region without calling focus(); keep errors on screen until fixed. Tension with the common error-summary pattern that moves focus to the summary: put the summary in a role=alert region that exists empty at load (no focus call) and move focus to the first invalid field instead.
- [major] `comp-live-region-exists-before-content`: Render an empty role=status container at load and fill it with text when something happens.

## components / Alert dialog
- [major] `comp-alertdialog-confirmations`: Write destructive confirmations as alertdialog with a plain-language consequence message and focus Cancel first.

## components / Checkboxes and radios
- [major] `comp-checkbox-radio-group-labels`: Wrap every option set in fieldset and legend and label each input.
- [major] `comp-radio-keyboard-model`: Use native radio inputs with the same name attribute rather than custom divs.

## components / Combobox / autocomplete
- [major] `comp-combobox-keyboard`: Implement Down, Up, Enter, Escape and Alt+Down exactly as the APG lists.
- [major] `comp-combobox-semantics`: Keep DOM focus in the input and move aria-activedescendant through the options.

## components / Content slider / carousel
- [major] `comp-content-slider-no-autoplay`: Build sliders as scroll-snap lists with labelled prev/next buttons and no autoplay.

## components / Data tables
- [major] `comp-data-table-overflow-focusable`: Wrap wide tables in a labelled overflow-x:auto container and add tabindex=0 when it scrolls.
- [major] `comp-data-table-semantics`: Mark pricing and spec tables with caption, th scope and real rows and columns.

## components / Landmarks
- [major] `comp-landmarks-complete`: Wrap the page in header, nav, main and footer, and keep every text block inside one of them.

## components / Listbox / custom select
- [major] `comp-listbox-select-semantics`: Prefer a native select; build a custom listbox only with full APG keys and short option labels.

## components / Menus
- [major] `comp-menu-button-action-menu`: Use role=menu only for action menus and implement every key the APG lists, or use a disclosure instead.
- [major] `comp-site-nav-no-menu-role`: Build header menus as nav > ul with a button[aria-expanded] per dropdown and plain links inside.

## components / Links
- [major] `comp-native-link-for-navigation`: Use a[href] to go somewhere and button to do something.

## components / Slider
- [major] `comp-slider-semantics`: Prefer input type=range; add output text next to it and aria-valuetext when units matter.

## components / Switches and toggles
- [major] `comp-switch-label-stable`: Name toggles after the setting ('Dark mode') and flip only aria-pressed or aria-checked.
- [major] `comp-toggle-visual-state-not-color`: Style toggles from [aria-pressed=true] and add a knob position or check icon, not only a color change.

## components / Tabs
- [major] `comp-tabs-keyboard`: Implement tabs with roving tabindex and arrow, Home and End keys, and set tabindex=0 on a panel that starts with non-focusable content.
- [major] `comp-tabs-semantics`: Give the tablist an aria-label, link every tab to its panel with aria-controls and aria-labelledby, and keep aria-selected in sync with the visible active state.

## components / Tooltips and toggletips
- [major] `comp-tooltip-not-sole-label-no-interactive`: Prefer visible labels; if a tooltip is unavoidable, trigger on hover and focus, allow Escape, and keep it text only.

## copy / buttons and links
- [major] `copy-button-verb-label`: Label each button with a verb plus its object ('Book a demo', 'Download the price list').
- [major] `copy-link-text-unique-destination`: Write link text that names the destination and say 'PDF, 2 MB' or 'opens in a new window' when it applies.

## copy / error messages and microcopy
- [major] `copy-error-specific-actionable`: Start empty-field errors with a verb ('Enter your email address') and wrong-value errors with the field name plus 'must be'.

## copy / specificity and credibility
- [major] `copy-expert-review-before-launch`: Write advice as a draft: mark it with the visible draft marker and a legend, list the reviewer you need (solicitor, clinician, adviser) in OPEN-QUESTIONS.md, and do not launch it as final until a qualified person has signed it off.
- [major] `copy-no-placeholder-text`: Leave nothing in brackets: ask for the missing fact or write real copy before finishing. If a real fact is still unconfirmed, show it with the visible assumption marker and legend (dotted underline class plus a footer line) and list it in OPEN-QUESTIONS.md; never brackets, and it must be resolved before launch.
- [major] `copy-proof-verifiable`: Use only claims and customers from the supplied brief, and mark any missing proof as a content gap instead of inventing it. A plain fact the owner has not confirmed may stay in a prototype only with the visible assumption marker and legend, listed in OPEN-QUESTIONS.md; invented proof is removed.
- [major] `copy-specific-over-abstract`: For every adjective, write the fact that made you choose it and use the fact instead.

## copy / headings
- [major] `copy-heading-informative`: Write each heading as the finding of its section, so the headings alone tell the story.

## copy / headlines and value proposition
- [major] `copy-headline-swap-test`: Write the headline as the result one named buyer gets, using a noun or number only this product can claim.

## copy / plain language
- [major] `copy-jargon-acronyms`: Write the full phrase the first time and in every heading or button, and describe each branded name in plain words next to it.
- [major] `copy-reading-grade`: Use short, common words and one clause per sentence, then check the grade score before finishing. For ESL, low-literacy or UK public-service readers aim at grade 5 or below (CEFR B1, GOV.UK plain language), offer translations with lang attributes and an interpreter where you really have one, and avoid idioms.
- [major] `copy-sentence-length`: Write body sentences of about 15 words, split any that pass 25, and read each aloud before keeping it.

## craft / typography: size minimum
- [major] `craft-body-size-min`: Set the body size to 1rem (16px) or larger, sized up (17-20px) for long reading, and use smaller sizes only for captions and legal lines.

## craft / layout: responsive behavior
- [major] `craft-breakpoints-content-based`: Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.

## craft / color: text over images
- [major] `craft-contrast-text-on-media`: Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.

## craft / color: APCA and WCAG 3 status
- [major] `craft-contrast-wcag2-authoritative`: Validate colors with the WCAG 2.x ratio and treat APCA only as a second opinion for borderline thin or small text.

## craft / color: dark mode and theming
- [major] `craft-dark-mode-reverify`: Author the dark palette as its own set of tokens, check contrast in both themes, and dim bright images instead of inverting anything.

## craft / typography: fluid type
- [major] `craft-fluid-type-rem-clamp`: Set headline sizes in rem and step them at em/rem media queries (for example 3rem, 4rem, 7rem), keeping the smallest at least 40% of the largest; do not use clamp(rem + vw) for text that must scale; test at 200% zoom and 320 px.

## craft / imagery: layout stability
- [major] `craft-image-dimensions-reserved`: Put the intrinsic width and height on every image tag and keep height: auto in CSS.

## craft / typography: line length
- [major] `craft-measure-body`: Wrap every block of running text in a container with max-inline-size of about 50ch to 55ch (ch is the width of the digit 0, wider than the average letter), never above 60ch, and count characters per line in the browser: it must not exceed 75.

## craft / typography: units
- [major] `craft-relative-units-text`: Write every font-size and text max-width in rem, em or ch, leave html font-size at 100%, and treat any px font-size as a bug.

## distinct / Direction before build
- [major] `distinct-written-direction`: Write the direction file first, then use only the colours, faces, radii and sizes it names.

## usability / performance
- [major] `perf-cls`: Reserve space for images, video, embeds and late content; keep layout shift at 0.1 or less.
- [major] `perf-core-first`: Build core content and navigation as HTML that works without JavaScript; layer effects on top.
- [major] `perf-inp`: Keep interaction responses at 200 ms or less: avoid long main-thread tasks, animate with transform and opacity, debounce handlers.
- [major] `perf-lcp`: Keep LCP at 2.5 s or less: make the LCP image discoverable in HTML, never lazy-load it, set fetchpriority high, keep head scripts and CSS small.

## usability / navigation
- [major] `ux-carousel-caution`: Prefer one static hero; if you use a carousel keep it to five frames, controls inside, no autoplay on mobile, and repeat key content elsewhere.
- [major] `ux-no-ad-lookalikes`: Do not style important content like banners, right-rail boxes or animated strips.
- [major] `ux-no-popups`: Avoid popups and splash screens on the homepage except legally required consent or age checks.
- [major] `ux-visible-navigation`: Show primary navigation links on desktop; on mobile show four or fewer, otherwise use a disclosure menu.

## usability / message
- [major] `ux-descriptive-labels`: Label links and buttons with the result ('Book a demo'), not 'Learn more' or 'Submit'.
- [major] `ux-front-load`: Put the most important information in the first screens and the first words of headings and paragraphs.
- [major] `ux-primary-cta-above-fold`: Show the primary action in the first viewport and repeat it where natural.
- [major] `ux-purpose-clear`: Say in the first screen who you are, what you offer and how you differ, in the audience's words.
- [major] `ux-scannable-text`: Use meaningful subheadings, short paragraphs with one idea, lists and the conclusion first.
- [major] `ux-tagline-specific`: Write a specific headline and tagline; no generic welcome text or jargon.

## usability / forms
- [major] `ux-form-errors`: Signal errors with more than color, say what is wrong and keep the user's input.
- [major] `ux-form-length`: Ask only for fields you need; at most one or two optional fields, labeled.
- [major] `ux-form-no-placeholder-label`: Never use a placeholder as a label; keep a visible label.

## usability / process
- [major] `ux-start-with-needs`: Start from real user needs and test assumptions with real people.
- [major] `ux-test-iteratively`: Plan about five people per audience group per round, fix problems and test again.

## Cognitive accessibility (COGA): all 15 rules
Mostly minor or advisory for a general audience. If the audience includes people under stress, with low literacy, reading in a second language (ESL), with cognitive or learning disabilities, or screen-reader or dyslexia users, treat every rule below as major for this project and say so in the brief [Our take]. They are then the core of the brief.
- [major] `a11y-coga-allow-paste-autofill`: Never block paste on inputs and set autocomplete tokens on every credential and contact field.
- [minor, major if the audience is flagged] `a11y-coga-action-feedback`: Show a visible confirmation after every submit and mark each step as done, current or next.
- [minor, major if the audience is flagged] `a11y-coga-controls-recognizable`: Underline inline links and give every button a visible fill or border.
- [minor, major if the audience is flagged] `a11y-coga-costs-up-front`: Show the full price with fees on the product page, not only at checkout.
- [minor, major if the audience is flagged] `a11y-coga-hierarchy-visible-no-hover-reveal`: Open menus on click, show a chevron on parents, and style each heading level once.
- [minor, major if the audience is flagged] `a11y-coga-icons-with-text`: Add a text label beside every icon except the universally understood few (search, close, menu).
- [minor, major if the audience is flagged] `a11y-coga-key-tasks-prominent`: Surface the main task as a prominent labelled control in the first screen and in the top navigation.
- [minor, major if the audience is flagged] `a11y-coga-limit-interruptions`: Delay any prompt until after the user finishes a task and make it dismissible.
- [minor, major if the audience is flagged] `a11y-coga-no-surprise-changes`: Reserve space for late content and open dialogs only after a click.
- [minor, major if the audience is flagged] `a11y-coga-plain-literal-language`: Name nav items and buttons with the literal thing the user gets, not a metaphor.
- [minor, major if the audience is flagged] `a11y-coga-text-not-over-busy-background`: Put hero text on a solid or scrimmed panel, never straight onto moving or high-detail imagery.
- [advisory, major if the audience is flagged] `a11y-coga-limit-choices-per-screen`: Limit each section to one main action plus at most four alternatives. Tension: a list of situations or services that is the content is one choice, not many; keep it as one labelled list that is the dominant feature, group a long one under headings, keep other actions visibly secondary and record the call.
- [advisory, major if the audience is flagged] `a11y-coga-media-chunks-transcripts`: Add chapter labels and a transcript link under every video longer than six minutes.
- [advisory, major if the audience is flagged] `a11y-coga-short-paragraphs`: Break copy into short single-topic paragraphs and use lists for three or more items.
- [advisory, major if the audience is flagged] `a11y-coga-visible-help-contact`: Put a Contact link in the footer of every page and keep its form to three required fields.

## Shared patterns
- **Unconfirmed facts (protocol 3.2): one component, one legend.** Do not hand-mark each fact. Write one component (React: `<Assumed critical>{text}</Assumed>`; plain HTML: a `span.assumed` partial) that renders the dotted cue, adds `aria-describedby` pointing at a single legend element with a fixed id (`assumed-legend`), and adds the visually hidden word "unconfirmed" only when `critical` is set (a price, a time). Render the legend once in the page layout, only when the page has at least one mark. Searching the build for the component then lists every open fact for realize-launch. [Our take]
  Inside a link (a phone number, an email address) keep the link's own solid underline and mark only the assumed part with an inner span whose dotted cue is a bottom border a little below the text, or a small marker beside the link: a dotted link underline would mean two things. aria-describedby on plain text is not reliably announced, so keep the hidden word only on the facts that matter most. Not tested with a screen reader.
- **Tensions the rules do not settle.** (1) `a11y-coga-limit-choices-per-screen` (about five main choices) against a list of situations or services that is the content: a list the visitor scans to find their case is one choice; keep it one labelled list as the dominant feature, group a long one under headings, keep every other action secondary, and write the call in the design notes. (2) `comp-alert-no-focus-no-autodismiss` against an error summary that takes focus: put the summary in a `role=alert` region that exists empty at load and is filled on a failed submit, do not focus it, and move focus to the first invalid field. [Our take]
- **Inputs and buttons in one row** at 320 px and 200% text: `flex: 1 1 6rem; min-width: 0` on the field and the button, `flex-wrap: wrap` on the row and on nav or pill lists (the 2026-11 run found a `flex: 1 1 12rem` field overflowing in every concept). [Our take]



# RECIPES

# Recipe: Dark, neon and atmospheric palettes that stay readable (`dark-neon-contrast`)
Styles covered: dark-cyber, neon, gradient-aurora, grain-noise, monochrome
**Keep:** Dark canvas, neon accents, glow, grain and gradients as atmosphere.
**Avoid:** Neon text for body copy; accents as the only sign of state; thin low-contrast hairlines; strobing glows.
Keep the near-black canvas and the glowing accents. Make text sit on solid surfaces, use neon for large or graphical elements only, and give focus its own bright, high-contrast ring.
**While designing:** Choose a palette with named roles, assert every text/background pair meets 4.5:1 (3:1 for large text and UI), keep neon for accents on solid surfaces, add a dedicated focus color, and avoid any flashing.
## Verified palette: Dark neon, verified
- background: #0B0D12
- surface: #141821
- text: #E9ECF3
- text-muted: #A9B0C0
- accent-green: #39FF88
- accent-pink: #FF4DB8
- focus: #5CE1FF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| text on background | #E9ECF3 | #0B0D12 | 16.43:1 | 4.5:1 |
| muted text on surface | #A9B0C0 | #141821 | 8.17:1 | 4.5:1 |
| neon green accent on background (UI, large text) | #39FF88 | #0B0D12 | 14.65:1 | 3:1 |
| neon pink accent on background (UI, large text) | #FF4DB8 | #0B0D12 | 6.48:1 | 3:1 |
| dark text on neon green button | #0B0D12 | #39FF88 | 14.65:1 | 4.5:1 |
| focus ring cyan on background | #5CE1FF | #0B0D12 | 12.65:1 | 3:1 |
| focus ring cyan on surface | #5CE1FF | #141821 | 11.56:1 | 3:1 |
| white text on 55% black scrim over gradient stop #3B1E8F | #FFFFFF | #1b0d40 | 17.82:1 | 4.5:1 |
| white text on 55% black scrim over gradient stop #D946EF | #FFFFFF | #621f6c | 10.87:1 | 4.5:1 |
| white text on 55% black scrim over gradient stop #FDE68A | #FFFFFF | #72673e | 5.64:1 | 4.5:1 |
## Steps
### Name palette roles and check pairs (`dn-palette`) [craft-consensus · verified]
Define colors as named roles, and check every text and surface pairing before choosing accents. Body text and muted text use the first two roles; neon is for large text, icons, borders and buttons with dark text on top.
- How: Use the verified pairs in this recipe as the starting palette; change a color only after recomputing its contrast.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Solid scrim under text (`dn-scrim`) [craft-consensus · verified]
Put text on a solid or semi-opaque surface, never directly on a gradient, glow, grain or image. Grain and noise sit on the background layer only. Over a gradient, a 55% black scrim keeps white text at 4.5:1 or better on every tested stop (#3B1E8F, #D946EF, #FDE68A), where unscrimmed white on #FDE68A fails.
- How: Layer order: background gradient and grain, then a scrim or surface, then text.
- Satisfies: a11y-contrast-text
### Bright dedicated focus ring (`dn-focus`) [craft-consensus · verified]
Give focus a distinct bright ring that works on both background and surface, and never remove the outline without a replacement.
- How: Use :focus-visible (Baseline widely available since March 2022) so the browser decides when the ring shows. MDN: the indicator needs at least 3:1 contrast (WCAG 1.4.11) and must not simply be removed. In forced-colors mode outline-color and border-color are forced to system colors and stay visible, but box-shadow is forced to none, so draw the ring with outline (as below) and do not rely on box-shadow alone. MDN advises against building a separate forced-colors design; do not use forced-color-adjust to override users' colors. Cyan #5CE1FF measures 3:1 or better on both dark roles.
- Satisfies: a11y-focus-visible, a11y-non-text-contrast
```css
:focus-visible {
  outline: 3px solid var(--focus);   /* 3:1 or better on every background it sits on */
  outline-offset: 3px;
}
```
### Show state beyond color (`dn-state-not-color`) [craft-consensus · verified]
Show state (selected, error, success) with more than a color shift: an icon, underline, weight or text.
- How: WCAG techniques: put the information in text (G14) or add another visual cue (G182); failures include required or error fields identified by color alone (F81). Inline links need 3:1 against surrounding text or another cue. WCAG lists color-vision simulators for checking; a grayscale view is a quick approximation.
- Satisfies: a11y-color-not-only
### Keep glow static or slow (`dn-no-strobe`) [craft-consensus · verified]
Keep glow static or slow. Never flash: content passes WCAG 2.3.1 if it flashes no more than three times per second.
- How: WCAG 2.3.1: no more than three general or red flashes in any one second passes without a tool; otherwise the flashes must stay below the thresholds (opposing luminance change of at least 10% with the darker state below 0.80 is a general flash; area limit about 341×256 px at 1024×768). Prefer a still box-shadow glow; if you pulse, keep it slow and respect reduced motion.
- Satisfies: a11y-flashes
### Show toggle state beyond color (`dark-neon-contrast--comp-toggle-visual-state-not-color`) [craft-consensus · partly-verified]
Style toggles from [aria-pressed=true] and add a knob position or check icon, not only a color change.
- How: Grayscale screenshot of both states; confirm still distinguishable. Check CSS selectors key off aria-pressed/aria-checked/:checked. (Derived from the rule; see its sources.)
- Satisfies: comp-toggle-visual-state-not-color
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Scrim behind text on media (`dark-neon-contrast--craft-contrast-text-on-media`) [craft-consensus · verified]
Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- How: Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (Derived from the rule; see its sources.)
- Satisfies: craft-contrast-text-on-media
### Re-check contrast in dark mode (`dark-neon-contrast--craft-dark-mode-reverify`) [craft-consensus · partly-verified]
Author the dark palette as its own set of tokens, check contrast in both themes, and dim bright images instead of inverting anything.
- How: Run the contrast audit (text 4.5:1, large 3:1, UI components 3:1) twice, once per emulated color scheme, over all pages and states (hover, focus, disabled excluded). Fail any pair that passes light but fails dark. Flag use of `filter: invert()` on the page root. (Derived from the rule; see its sources.)
- Satisfies: craft-dark-mode-reverify
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Rem steps for display headings (`dn-reflow-200`) [standard · verified]
Give display headings overflow-wrap: anywhere and step the h1 down in a rem media query (max-width: 30rem), with less hero padding, so a word like 'terminal' at 96 px does not stretch the page; do not use clamp() with vw for this.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; the h1 at 3rem became 96 px at 200%; the word was 364 px wide in a 224 px column and widened the page; the media-query step-down removed the overflow and the a11y-resize-text probe no longer reported a fluid-type problem.
- Satisfies: a11y-reflow

# Recipe: Glass, pastel and soft palettes without washed-out text (`glass-pastel-soft`)
Styles covered: glassmorphism, pastel
**Keep:** Frosted panels, soft color fields, rounded forms.
**Avoid:** White text on a light translucent panel; pastel text on pastel backgrounds; glass borders as the only separator between controls and background.
Keep the translucency, blur and gentle colors. Decide the worst-case backdrop first, make the panel dark or light enough for that case, and use pastel as fills with dark text and visible borders.
**While designing:** Test text against the worst-case backdrop, add an opaque fallback, keep text dark on pastel fills, and make control borders at least 3:1.
## Verified palette: Pastel, verified
- background: #F7F1FF
- text: #2B1B45
- text-muted: #5B4B77
- button-fill: #CDB4FF
- input-border: #7A68A3
- link: #5A2FC2
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white text on 72% dark panel over #FFFFFF backdrop | #FFFFFF | #4f5154 | 7.96:1 | 4.5:1 |
| white text on 72% dark panel over #FFE066 backdrop | #FFFFFF | #4f482a | 9.16:1 | 4.5:1 |
| white text on 72% dark panel over #7CF2FF backdrop | #FFFFFF | #2b4d54 | 9.16:1 | 4.5:1 |
| text on pastel background | #2B1B45 | #F7F1FF | 14.11:1 | 4.5:1 |
| muted text on pastel background | #5B4B77 | #F7F1FF | 6.98:1 | 4.5:1 |
| dark text on pastel lilac button | #2B1B45 | #CDB4FF | 8.6:1 | 4.5:1 |
| input border on pastel background | #7A68A3 | #F7F1FF | 4.38:1 | 3:1 |
| link on pastel background | #5A2FC2 | #F7F1FF | 7.24:1 | 4.5:1 |
## Steps
### Test glass on the worst backdrop (`gp-worst-case`) [craft-consensus · partly-verified]
For glass, compute contrast against the worst backdrop the panel can sit on (white, a bright yellow, a bright cyan), not the average one. The verified panel is 72% near-black; white text on it stays above 4.5:1 over all three backdrops (see the table).
- How: Panel color rgba(11,13,18,0.72) with white text. The check uses pure white as the backdrop because a blur is a per-channel weighted average of the pixels behind it and so cannot be lighter than the lightest pixel; this bound assumes browsers composite in sRGB (general knowledge, not on a page read). Raise the opacity before lowering text contrast.
- Satisfies: a11y-contrast-text
- Verification note: bound rests on sRGB compositing and blur averaging (reasoning, not a read source)
### Opaque fallback for backdrop blur (`gp-fallback`) [craft-consensus · verified]
Provide an opaque fallback for browsers or settings where backdrop-filter does not apply, and do not rely on blur to separate text from a busy background.
- How: backdrop-filter is Baseline 2024 (newly available) and only affects content behind the element up to its backdrop root; an ancestor with opacity below 1 can stop it working. Write the opaque background first and enhance inside @supports (backdrop-filter: blur(1px)), or provide the fallback in @supports not (...). @supports is widely available since September 2015.
- Satisfies: a11y-contrast-text
### Dark text on pastel fills (`gp-pastel-fill`) [craft-consensus · verified]
Use pastel as a fill and keep dark text on it. Check muted text and links on the pastel background, not on white.
- How: Verified pairs: #2B1B45 on #F7F1FF, #5B4B77 on #F7F1FF, #2B1B45 on #CDB4FF, link #5A2FC2 on #F7F1FF.
- Satisfies: a11y-contrast-text
### Control edges at 3:1 (`gp-borders`) [craft-consensus · verified]
Give inputs, cards that act as controls and icon buttons a border or fill that reaches 3:1 against what surrounds them.
- How: Input border #7A68A3 on #F7F1FF is verified above 3:1.
- Satisfies: a11y-non-text-contrast
### Label the modal dialog (`glass-pastel-soft--comp-dialog-semantics`) [craft-consensus · verified]
Build modals with a titled dialog element or role=dialog plus aria-labelledby, and keep all its controls inside it.
- How: Open each dialog; query [role=dialog],[role=alertdialog],dialog[open]; assert accessible name is non-empty and that no interactive control needed by the dialog sits outside it. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-semantics
### Manage dialog focus and Escape (`glass-pastel-soft--comp-dialog-focus`) [craft-consensus · verified]
On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- How: Keyboard only: activate the opener, verify focus is inside; Tab through the whole dialog and confirm wrap; press Escape and confirm close and focus on the opener; confirm a visible close control exists. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-focus
### Make modal backgrounds inert (`glass-pastel-soft--comp-dialog-truly-modal`) [craft-consensus · verified]
Make the background inert and dimmed whenever the dialog is modal; for popovers that leave the page usable, do not set aria-modal.
- How: With the dialog open, try to Tab, click and screen-reader-navigate to background content. If any works, aria-modal must be absent. If aria-modal is present, confirm a dim or blur overlay covers the page. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-truly-modal
### Scrim behind text on media (`glass-pastel-soft--craft-contrast-text-on-media`) [craft-consensus · verified]
Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- How: Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (Derived from the rule; see its sources.)
- Satisfies: craft-contrast-text-on-media
### Re-check contrast in dark mode (`glass-pastel-soft--craft-dark-mode-reverify`) [craft-consensus · partly-verified]
Author the dark palette as its own set of tokens, check contrast in both themes, and dim bright images instead of inverting anything.
- How: Run the contrast audit (text 4.5:1, large 3:1, UI components 3:1) twice, once per emulated color scheme, over all pages and states (hover, focus, disabled excluded). Fail any pair that passes light but fails dark. Flag use of `filter: invert()` on the page root. (Derived from the rule; see its sources.)
- Satisfies: craft-dark-mode-reverify
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Small padding on nested glass (`gp-reflow-200`) [standard · verified]
Keep padding on nested glass panels small under 30rem (panel 1rem, backdrop 1rem) and give the panel heading overflow-wrap: anywhere with a smaller rem size; stacked padding inside a glass panel can leave a column of about 96 px at 200% text.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; a 72 px h1 in a 96 px column overflowed 17 px; after reducing padding and stepping the size down, there was no overflow.
- Satisfies: a11y-reflow

# Recipe: Minimal and quiet-luxury pages that remain clear and usable (`minimal-clear`)
Styles covered: minimal, quiet-luxury, hero-type-only, poster
**Keep:** Whitespace, small type, few elements, muted palette.
**Avoid:** Light gray text, borderless inputs, placeholder-only labels, tiny icon links, a first screen that looks finished when it is not.
Keep the whitespace and restraint. Restraint must not remove contrast, borders, focus, hit areas, labels or the hint that more content exists.
**While designing:** Keep muted text at 4.5:1 or better, borders and controls at 3:1, show a clear focus ring, use 24 px minimum targets, visible labels, a one-line purpose with a primary action in the first viewport, and a cue that more content follows.
## Verified palette: Off-white minimal, verified
- background: #FAFAF7
- text: #1A1A18
- text-muted: #6A6A64
- input-border: #8C8C85
- focus: #1A1A18
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| text on off-white | #1A1A18 | #FAFAF7 | 16.67:1 | 4.5:1 |
| muted text on off-white | #6A6A64 | #FAFAF7 | 5.2:1 | 4.5:1 |
| input border on off-white | #8C8C85 | #FAFAF7 | 3.24:1 | 3:1 |
| focus ring on off-white | #1A1A18 | #FAFAF7 | 16.67:1 | 3:1 |
## Steps
### Keep muted text at 4.5:1 (`mn-contrast`) [craft-consensus · verified]
Keep secondary text at or above 4.5:1; #6A6A64 on #FAFAF7 is verified. Do not lighten muted text further for elegance.
- How: Check every gray in the palette against every background it touches.
- Satisfies: a11y-contrast-text
### Visible field edges at 3:1 (`mn-borders`) [craft-consensus · verified]
Give form fields and controls a visible edge at 3:1 or better; a hairline at #8C8C85 on #FAFAF7 is verified.
- How: A subtle fill is fine only if it meets 3:1 against the page.
- Satisfies: a11y-non-text-contrast
### Solid offset focus ring (`mn-focus`) [craft-consensus · verified]
Make focus obvious: a solid ring in the text color with an offset suits a minimal style.
- How: Use :focus-visible (Baseline widely available since March 2022) so the browser decides when the ring shows. MDN: the indicator needs at least 3:1 contrast (WCAG 1.4.11) and must not simply be removed. In forced-colors mode outline-color and border-color are forced to system colors and stay visible, but box-shadow is forced to none, so draw the ring with outline (as below) and do not rely on box-shadow alone. MDN advises against building a separate forced-colors design; do not use forced-color-adjust to override users' colors.
- Satisfies: a11y-focus-visible
```css
:focus-visible {
  outline: 3px solid var(--focus);   /* 3:1 or better on every background it sits on */
  outline-offset: 3px;
}
```
### Targets of at least 24 px (`mn-targets`) [craft-consensus · verified]
Keep targets at least 24 by 24 CSS pixels, or spaced so a 24 px circle around each fits without overlap; give small text links padding.
- How: WCAG spacing exception: a 24 px circle centered on each undersized target must not intersect another target or another undersized target's circle; WCAG's example is 20×20 px buttons with a 4 px gap passing, and with no gap failing. Other exceptions: an equivalent control, inline text links, user-agent controls, essential targets. Pad icon buttons and footer links rather than enlarging the glyph.
- Satisfies: a11y-target-size
### Visible label on every field (`mn-labels`) [craft-consensus · verified]
Keep a visible label on every field; use placeholders only for examples.
- How: Float labels are acceptable only if the label stays visible after input.
- Satisfies: ux-form-no-placeholder-label
### One line, one action, a cue (`mn-purpose-and-floor`) [our-take · verified]
Say what the page is and what to do in one line plus one primary action in the first viewport, and show a cut-off element or cue that more content follows.
- How: A restrained first screen is fine; an unexplained one is not. Let the next section peek in at the bottom edge.
- Satisfies: ux-purpose-clear, ux-primary-cta-above-fold, ux-false-floor
### Wire tabs to their panels (`minimal-clear--comp-tabs-semantics`) [craft-consensus · verified]
Give the tablist an aria-label, link every tab to its panel with aria-controls and aria-labelledby, and keep aria-selected in sync with the visible active state.
- How: Query the DOM: every [role=tab] is a child of [role=tablist]; exactly one tab has aria-selected=true; each tab aria-controls resolves to a [role=tabpanel] whose aria-labelledby resolves to that tab; tablist has aria-label or aria-labelledby. Confirm with a screen reader that the selected state is announced. (Derived from the rule; see its sources.)
- Satisfies: comp-tabs-semantics
### Accordions as heading plus button (`minimal-clear--comp-accordion-markup`) [craft-consensus · partly-verified]
Write accordions as h3 > button[aria-expanded] followed by a div that gets the hidden attribute when collapsed.
- How: For each toggle: tagName is BUTTON, parent is h1-h6 (or role=heading with aria-level), the button is the heading's only child, aria-expanded is 'true' or 'false' and flips on click, the hidden panel is display:none or [hidden] when collapsed. (Derived from the rule; see its sources.)
- Satisfies: comp-accordion-markup
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Prefer visible labels over tooltips (`minimal-clear--comp-tooltip-not-sole-label-no-interactive`) [craft-consensus · partly-verified]
Prefer visible labels; if a tooltip is unavoidable, trigger on hover and focus, allow Escape, and keep it text only.
- How: Hover and Tab to each tooltip trigger; press Escape; move the pointer onto the bubble; check aria-describedby; check the bubble DOM for a, button, input. (Derived from the rule; see its sources.)
- Satisfies: comp-tooltip-not-sole-label-no-interactive
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Show toggle state beyond color (`minimal-clear--comp-toggle-visual-state-not-color`) [craft-consensus · partly-verified]
Style toggles from [aria-pressed=true] and add a knob position or check icon, not only a color change.
- How: Grayscale screenshot of both states; confirm still distinguishable. Check CSS selectors key off aria-pressed/aria-checked/:checked. (Derived from the rule; see its sources.)
- Satisfies: comp-toggle-visual-state-not-color
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Short words, check reading grade (`minimal-clear--copy-reading-grade`) [craft-consensus · partly-verified]
Use short, common words and one clause per sentence, then check the grade score before finishing.
- How: Run Flesch-Kincaid grade (Hemingway, Word, or a script) on the concatenated body copy of each page, excluding proper names and titles. Fail above 9 for general audiences unless the brief names an expert audience. (Derived from the rule; see its sources.)
- Satisfies: copy-reading-grade
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Spell out acronyms and brand names (`minimal-clear--copy-jargon-acronyms`) [craft-consensus · partly-verified]
Write the full phrase the first time and in every heading or button, and describe each branded name in plain words next to it.
- How: Extract all-caps tokens of 2 or more letters and capitalised product names from headings, nav and buttons; confirm each is expanded or described adjacent. Confirm first body use is expanded. Whitelist PDF, FAQ, URL. (Derived from the rule; see its sources.)
- Satisfies: copy-jargon-acronyms
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headline as one buyer's result (`minimal-clear--copy-headline-swap-test`) [craft-consensus · partly-verified]
Write the headline as the result one named buyer gets, using a noun or number only this product can claim.
- How: Read the H1 and subhead alone. (1) Does it say what is offered and for whom? (2) Paste it with a competitor's name: does it still read true? If yes, fail. (3) Fail if it matches the template 'The [AI-powered|modern|all-in-one] [noun] for [teams|businesses|everyone]'. (Derived from the rule; see its sources.)
- Satisfies: copy-headline-swap-test
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headings that state the finding (`minimal-clear--copy-heading-informative`) [craft-consensus · partly-verified]
Write each heading as the finding of its section, so the headings alone tell the story.
- How: Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (Derived from the rule; see its sources.)
- Satisfies: copy-heading-informative
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Buttons labelled verb plus object (`minimal-clear--copy-button-verb-label`) [craft-consensus · partly-verified]
Label each button with a verb plus its object ('Book a demo', 'Download the price list').
- How: Collect text of button, [role=button], input[type=submit] and .btn-like links. Fail if the first word is not a verb (use a verb list), if the word count is over 4, or if the label matches the blocklist: submit, ok, click here, learn more, get started, go, continue (unless a save step is stated). (Derived from the rule; see its sources.)
- Satisfies: copy-button-verb-label
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Link text names the destination (`minimal-clear--copy-link-text-unique-destination`) [craft-consensus · partly-verified]
Write link text that names the destination and say 'PDF, 2 MB' or 'opens in a new window' when it applies.
- How: Collect all anchors with accessible names. Fail if two different hrefs share the same name, if a name matches /^(click here|here|more|read more|link|this)$/i or contains 'link', if an href ends in a document extension without format and size in the name, or if target=_blank lacks a notice placed after the main text. (Derived from the rule; see its sources.)
- Satisfies: copy-link-text-unique-destination
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Specific, actionable error text (`minimal-clear--copy-error-specific-actionable`) [craft-consensus · partly-verified]
Start empty-field errors with a verb ('Enter your email address') and wrong-value errors with the field name plus 'must be'.
- How: Trigger every validation and failure state (empty, wrong format, too long, network failure, server error). Fail any message that does not name the problem and a fix, matches the generic list, or shows a raw code. Automated part: grep message strings for the generic list. (Derived from the rule; see its sources.)
- Satisfies: copy-error-specific-actionable
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Facts instead of adjectives (`minimal-clear--copy-specific-over-abstract`) [craft-consensus · partly-verified]
For every adjective, write the fact that made you choose it and use the fact instead.
- How: Grep for the abstract-adjective list. For each hit, require a number, a named object or a verifiable example in the same sentence, otherwise rewrite. Check that no three feature cards share the same structure of icon, two-word title and filler sentence. (Derived from the rule; see its sources.)
- Satisfies: copy-specific-over-abstract
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Cap line length near 55ch (`minimal-clear--craft-measure-body`) [craft-consensus · partly-verified]
Wrap every block of running text in a container with max-inline-size of about 45ch to 55ch for proportional fonts (never wider than 60ch), and let the container, not the viewport, decide the line length; then count characters per line in the browser.
- How: Measured 2026-11-06 in Chrome on macOS: ch is the width of the digit 0, wider than an average letter, so 66ch gave 87 to 96 characters per line (system-ui, Georgia, Arial, Helvetica Neue), 60ch gave 77 to 89, 55ch gave 69 to 83, 50ch gave 67 to 74 and 45ch gave 59 to 67. Use 50ch to 55ch and verify the real count with the audit. Other platforms' fonts were not measured.
- Satisfies: craft-measure-body
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Body text at 1rem or larger (`minimal-clear--craft-body-size-min`) [craft-consensus · partly-verified]
Set the body size to 1rem (16px) or larger, sized up (17-20px) for long reading, and use smaller sizes only for captions and legal lines.
- How: At 320 and 1280 px, collect computed font-size of every text node inside p, li, td, label, input, textarea, select, button. Fail when any is under 16px, unless the node is inside figcaption, small, footer legal text or a caption. List every text node under 14px for manual review (14px is our review threshold, not from a source). (Derived from the rule; see its sources.)
- Satisfies: craft-body-size-min
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Stepped rem sizes for headings (`minimal-clear--craft-fluid-type-rem-clamp`) [craft-consensus · verified]
Set headline sizes in rem and step them at em/rem media queries (for example 3rem, 4rem, 7rem), keeping the smallest at least 40% of the largest; do not use clamp(rem + vw) for text that must scale; test at 200% zoom and 320 px.
- How: Measured in Chrome 2026-11-05 (content/learn/measurements/type-zoom-2026-11-05.json): clamp(rem + vw) and vw sizes did not reach 200% at 200% zoom; stepped rem with small >= 40% of large did. See also step bt-scalable in big-type-and-modes.
- Satisfies: craft-fluid-type-rem-clamp
### Breakpoints where content breaks (`minimal-clear--craft-breakpoints-content-based`) [craft-consensus · partly-verified]
Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- How: Sweep the viewport from 320 to 1920 px in 40px steps. At each step assert no horizontal scrollbar (scrollWidth <= clientWidth), no element overlapping its sibling's box, and the measure rule still passes. Inspect media queries: list breakpoint values and flag any matching device presets (375, 414, 768 and 1024 px) written in px for review. (Derived from the rule; see its sources.)
- Satisfies: craft-breakpoints-content-based
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Wrap headings and button links (`mn-reflow-200`) [standard · verified]
Give display headings overflow-wrap: anywhere (a 3rem h1 is 96 px at 200% text and a word such as 'Furniture' is about 400 px wide) and give button-like links max-width: 100% with overflow-wrap: anywhere.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; the page scrolled 215 px sideways at 320 px with 200% text and a link collapsed to 12 px under the text-spacing overrides; both were gone after the change.
- Satisfies: a11y-reflow

# Recipe: 3D, WebGL, cursor effects and interactive art (`webgl-and-3d`)
Styles covered: realtime-3d, hero-3d, interactive-art, cursor-effects
**Keep:** A real-time 3D or shader scene, interactive objects, cursor-following effects.
**Avoid:** Scene as the only way to reach content; canvases that trap focus; effects that need drag; heavy initialization before the first content paints.
Keep the spectacle. Treat the 3D scene as an enhancement over a complete page: real content first, a meaningful static fallback, keyboard parity, and a performance budget measured on mid-range devices.
**While designing:** Ship the page content as HTML first, use a static poster for LCP, start WebGL after first paint, pause off-screen, give keyboard and single-pointer alternatives, never trap focus, and honor reduced motion.
## Steps
### Core content works without the scene (`wg-core-first`) [craft-consensus · verified]
Build the headline, copy, navigation and call to action as normal HTML that works without the scene. The scene replaces or decorates a static image, not the content.
- How: Resilient Web Design (Layers): start from a well-structured HTML baseline everyone can use and enhance per capability; identify core functionality versus enhancement; feature-detect rather than sniff. Test by disabling JavaScript and throttling the network: the message and navigation must still appear.
- Satisfies: perf-core-first, ux-purpose-clear
### Script-revealed scene controls (`wg-controls-need-js`) [our-take · verified]
Controls that only work once the scene runs (rotate, zoom, pause, skip link) start hidden and are shown by the scene script; with JavaScript off they must not appear.
- How: Use the hidden attribute and add [hidden]{display:none !important}: an author rule such as .controls{display:grid} overrides the browser's hidden style, so the controls stayed visible with JavaScript off in the demo until that rule was added. Add a noscript style as a second guard. If the scene fails to start (getContext returns null, shader link fails), remove the canvas and the controls and leave the poster.
- Satisfies: perf-core-first, a11y-name-role-value
- Verification note: measured in the demo: with JavaScript disabled the controls and canvas were visible until [hidden]{display:none !important} was added; Playwright no-JS pass afterwards showed them hidden and the poster visible
### Static poster as LCP element (`wg-lcp`) [craft-consensus · verified]
Show a static poster image of the scene as the LCP element, discoverable in the initial HTML and not lazy-loaded; initialize WebGL after first paint.
- How: Use a real img for the poster with fetchpriority="high", discoverable in the initial HTML and not lazy-loaded (web.dev). Start the scene after first paint: requestIdleCallback has limited availability (not Baseline), so call it with a timeout and fall back to setTimeout, or start on the load event. Avoid synchronous head scripts.
- Satisfies: perf-lcp
### Test scene and no-WebGL paths (`wg-test-both-paths`) [our-take · verified]
Test the scene path and the no-WebGL path: with WebGL unavailable the poster stays, the controls disappear and nothing throws.
- How: Check getContext('webgl2') for null and shader compile and link errors; on failure remove the canvas and hide the controls. Headless Chrome without GPU flags has no WebGL, so a default audit run only ever exercises this fallback; launch Chrome with --use-gl=angle --use-angle=swiftshader --enable-unsafe-swiftshader to audit the live scene.
- Satisfies: perf-core-first, ux-purpose-clear
- Verification note: both paths were run with the audit: default flags (fallback) and swiftshader flags (live scene); both had zero fails
### Serve the poster as a file (`wg-poster-real-file`) [our-take · verified]
Serve the poster as a real image file (or URL), not a data: URI, if you want it to count as the LCP element.
- How: In Chrome 156 an 800x600 img whose src is a data: URI was not reported as an LCP candidate: the LCP entry was a tiny h1 instead (PerformanceObserver type largest-contentful-paint). Self-contained pages cannot therefore prove the poster is the LCP element; measure on the real asset.
- Satisfies: perf-lcp
- Verification note: measured once with a single test page in Chrome 156 (headless, Playwright); not checked in other browsers
### Reserve space for scene controls (`wg-reserve-control-space`) [craft-consensus · verified]
Reserve the space of controls that appear when the scene starts, so starting the scene moves nothing.
- How: Render the controls in the first HTML with visibility:hidden (it keeps the box) and switch to visible when the scene is ready; do not go from display:none to display:grid after load. Give the stage an aspect-ratio and put the poster image inside it with width and height attributes.
- Satisfies: perf-cls
### Keep the main thread free (`wg-inp`) [craft-consensus · verified]
Keep the main thread free: render in requestAnimationFrame, avoid layout reads inside pointer handlers, cap device pixel ratio (for example at 2), and pause rendering when the canvas is off-screen or the tab is hidden.
- How: Run the render loop only while the canvas is visible, using IntersectionObserver (Baseline widely available since March 2019; its callbacks run on the main thread, so keep them light; feature-detect it). Use the Page Visibility API (visibilitychange, document.hidden; widely available since 2015) for work the browser does not stop itself: browsers already stop requestAnimationFrame in background tabs, but not audio, timers or network. Measure INP in the field; lab tools only approximate it.
- Satisfies: perf-inp
### Fallback content inside the canvas (`wg-semantics`) [craft-consensus · verified]
Put alternative content inside the canvas element (a text description, or an image with alt). Mark a purely presentational canvas role="presentation". If the scene is interactive, map each interactive region to a real focusable element in the fallback content; the canvas itself exposes nothing.
- How: MDN: a canvas is a bitmap that exposes nothing to assistive technology; fallback content goes between the canvas tags; role="presentation" is only for purely presentational canvases; MDN advises avoiding canvas in accessible sites where possible. The HTML Standard says fallback content must convey the same function, focusable descendants of a canvas remain usable, and interactive regions should map one-to-one to focusable areas in the fallback. No page read mentions aria-label on canvas. Put the same information in the page text.
- Satisfies: a11y-name-role-value, ux-purpose-clear
### Make the canvas skippable (`wg-no-trap`) [craft-consensus · verified]
Make the canvas skippable: it is not in the tab order unless it has controls, and focus can always leave it. Provide a visible way to skip past an interactive scene.
- How: WCAG 2.1.2: if focus can enter a component, the keyboard must be able to leave it; a non-standard exit must be explained to the user; Esc is a common standard exit; a modal that cycles focus and closes by Esc or buttons passes. Keep the canvas out of the tab order unless it has controls, and give interactive scenes a visible way to skip past them.
- Satisfies: a11y-no-keyboard-trap, a11y-keyboard
### Buttons and keys beside dragging (`wg-no-drag-only`) [craft-consensus · verified]
Anything done by dragging or orbiting also works with buttons or keys (rotate left and right, zoom in and out), and with a single tap.
- How: WCAG 2.5.7 (technique G219): put buttons beside the drag, or use tap-to-place, direct selection or a typed value. A keyboard alternative alone does not satisfy 2.5.7: pointer-operable controls are needed (they may be visually hidden). Add visible rotate and zoom buttons next to any drag-to-rotate scene.
- Satisfies: a11y-dragging, a11y-pointer-gestures
### Tap to turn, pan-y to scroll (`wg-tap-and-pan`) [our-take · verified]
Make a tap on the canvas turn the scene one step, and set touch-action: pan-y on the canvas so vertical swipes still scroll the page.
- How: Use pointer events: record pointerdown, treat movement over about 6 px as a drag, and on pointerup without movement call the same function as the Rotate right button. With touch-action: pan-y a horizontal drag rotates and a vertical swipe scrolls, so the canvas does not trap touch scrolling. Make sure the object is visibly different when turned (a rotationally symmetric object shows nothing when rotated; add pattern or asymmetry).
- Satisfies: a11y-dragging, a11y-pointer-gestures
- Verification note: Playwright: mouse drag, mouse click and touch tap each changed the rendered frame under reduced motion; touch-action computed as pan-y
### Respect reduced motion (`wg-motion`) [craft-consensus · verified]
Respect reduced motion: show the poster or a still frame, stop continuous camera movement, and keep the motion minimal for everyone around the headline and call to action.
- How: Check matchMedia("(prefers-reduced-motion: reduce)") before starting the loop and listen for its change event (Baseline widely available since September 2020) so the scene reacts when the setting changes.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
```css
@media (prefers-reduced-motion: reduce) {
  .reveal { animation: none; transition: opacity .2s linear; transform: none; }
  .parallax-layer { transform: none !important; }
}
```
### Check reduced motion inside the loop (`wg-motion-listener-gotcha`) [our-take · partly-verified]
Do not rely on the change event alone to react to a reduced-motion switch while a render loop reads .matches; compare the current value inside the loop too.
- How: In Chrome (Playwright emulateMedia), when a requestAnimationFrame loop read matchMedia(...).matches every frame, the page's own change listener did not fire after the setting changed, although a freshly created MediaQueryList did receive the event. Keeping a lastReduce variable and calling the apply function when reduce.matches !== lastReduce inside the frame fixed it. Also keep user-initiated rotate and zoom working under reduced motion, as instant jumps instead of easing.
- Satisfies: a11y-reduced-motion
- Verification note: reproduced with Playwright media emulation in one Chrome build; not reproduced with a real OS setting change
### Cursor effects never replace the cursor (`wg-cursor`) [our-take · judgement]
Cursor-following effects add to the system cursor and never replace it on interactive elements; keyboard focus gets the equivalent highlight; turn the effect off on touch devices and under reduced motion.
- How: Animate transform and opacity only (web.dev: the only two compositor-only properties) and keep layers few (do not promote everything with will-change). Use passive listeners where you never call preventDefault: wheel, touchstart and touchmove on window or document are passive by default, element-level listeners are not. One requestAnimationFrame loop.
- Satisfies: a11y-keyboard, perf-inp
- Verification note: the recommendation is our judgement; the supporting facts (compositor-only properties, passive listener defaults) are verified
### Cursor glow behind content (`wg-cursor-glow-placement`) [our-take · judgement]
Put a cursor glow behind the page content, never over it: fixed, pointer-events:none, z-index below content, transform only, and enable it only for (hover: hover) and (pointer: fine) when motion is not reduced. Keep the glow achromatic or warm and the accent off cyan on a near-black page: a cyan or teal radial halo with alpha under 0.3 fails distinct-no-decorative-glow and a cyan accent on near-black fails distinct-no-ai-palette.
- How: Give html the background and leave body transparent so a z-index:-1 layer is visible. On keyboard focus (focusin where :focus-visible matches) move the glow to the focused control. Declare the pointermove listener passive and drive the glow from the same requestAnimationFrame loop as the scene. Axe reported no contrast problems with the low-opacity glow behind light text. Measured 2026-11-06: switching the accent to sand (#E3C08D) and the halo to rgba(238,243,242,.12) cleared both audit failures; the halo is position:fixed so it never causes scroll.
- Satisfies: a11y-keyboard, a11y-reduced-motion, perf-inp
- Verification note: the placement choices are our judgement; the touch gating was checked with Playwright mobile emulation (hover:hover and pointer:fine both false) and the reduced-motion gating by emulation
### Manage dialog focus and Escape (`webgl-and-3d--comp-dialog-focus`) [craft-consensus · verified]
On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- How: Keyboard only: activate the opener, verify focus is inside; Tab through the whole dialog and confirm wrap; press Escape and confirm close and focus on the opener; confirm a visible close control exists. (Derived from the rule; see its sources.)
- Satisfies: comp-dialog-focus
### Prefer visible labels over tooltips (`webgl-and-3d--comp-tooltip-not-sole-label-no-interactive`) [craft-consensus · partly-verified]
Prefer visible labels; if a tooltip is unavoidable, trigger on hover and focus, allow Escape, and keep it text only.
- How: Hover and Tab to each tooltip trigger; press Escape; move the pointer onto the bubble; check aria-describedby; check the bubble DOM for a, button, input. (Derived from the rule; see its sources.)
- Satisfies: comp-tooltip-not-sole-label-no-interactive
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Use a native range input (`webgl-and-3d--comp-slider-semantics`) [craft-consensus · verified]
Prefer input type=range; add output text next to it and aria-valuetext when units matter.
- How: Inspect value attributes; keyboard test arrows/Home/End/PageUp/PageDown; check aria-valuetext shows units; test with VoiceOver on iOS or TalkBack. (Derived from the rule; see its sources.)
- Satisfies: comp-slider-semantics
### Auto-fit grids with min() tracks (`wg-reflow-grids`) [standard · verified]
Write card grids as repeat(auto-fit, minmax(min(15rem, 100%), 1fr)): minmax(15rem, 1fr) is a 480 px track at 200% text.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; the li right edge was 520 px at 320 px; inside the viewport after the change.
- Satisfies: a11y-reflow

# Recipe: Hero video, ambient loops and marquees (`video-and-ambient-motion`)
Styles covered: hero-video, ambient-loop, marquee
**Keep:** Full-bleed muted looping video, ambient background loops, ticker rows of logos or text.
**Avoid:** Autoplaying sound; no way to stop motion; important messages inside a scrolling ticker; large video as the LCP with no poster.
Keep the moving backdrop. Decide whether the video is decorative or carries information, give viewers a pause control, never autoplay sound, and keep key messages out of the moving layer.
**While designing:** Decorative muted looping video with a poster as LCP, a visible pause control, no autoplaying sound, static fallback for reduced motion, and key messages in HTML text.
## Steps
### Decide decorative or informative video (`vd-classify`) [craft-consensus · partly-verified]
Decide: is the video decorative and silent, or does it carry speech or information? Decorative: mark it as such and keep every message in text. Informative: it needs captions and a description or transcript.
- How: WCAG 1.2.1 requires an alternative or an audio track for prerecorded video-only content, and its Understanding page does not exempt decorative or background video; 1.1.1 says pure decoration should be ignorable by assistive technology. So: treat a loop as decoration (aria-hidden, no information in it, every message also in text) as an inference from 1.1.1, and add the pause control (2.2.2). A video with speech needs captions (1.2.2) and an audio description or text alternative (1.2.3, 1.2.5).
- Satisfies: a11y-captions, a11y-audio-description
- Verification note: WCAG does not address background video directly; the decorative treatment is an inference from 1.1.1
### Never autoplay sound (`vd-no-sound`) [craft-consensus · verified]
Never autoplay sound. Autoplay muted (or with no audio track), with playsinline, and provide controls to start sound.
- How: Browsers generally block audible autoplay; muted and silent video may autoplay, and playsinline is needed for autoplay in Safari.
- Satisfies: a11y-audio-control
```html
<video autoplay muted loop playsinline poster="/hero.jpg" aria-hidden="true">
  <source src="/hero.mp4" type="video/mp4">
</video>
<!-- script swaps the label between "Pause background video" and "Play background video"; no aria-pressed -->
<button type="button" class="motion-toggle">Pause background video</button>
```
### Keyboard-reachable pause control (`vd-pause`) [craft-consensus · verified]
Give a visible, keyboard-reachable control that pauses or stops automatically starting motion (video, ambient loop, ticker); ideally one control for all moving content. A control that only pauses while hovered or focused does not meet WCAG 2.2.2.
- How: WCAG 2.2.2 applies to moving content that starts automatically (including by hover, focus or scrolling into view), lasts more than five seconds and runs alongside other content; auto-updating content has no five-second exception. Because the label changes between "Pause" and "Play", do not add aria-pressed: the APG button pattern says a toggle's label must stay the same when aria-pressed is used. Remember the choice for the session.
- Satisfies: a11y-pause-stop-hide
### Poster and play button fallback (`vd-handle-denied`) [craft-consensus · verified]
If autoplay is blocked or reduced motion is on, show the poster image and a play button instead of an empty frame.
- How: Catch the play() promise rejection (NotAllowedError) and show the poster or play button.
- Satisfies: a11y-pause-stop-hide, perf-lcp
### Poster as the LCP candidate (`vd-lcp`) [craft-consensus · verified]
Make the poster the LCP candidate: an image discoverable in the initial HTML with fetchpriority="high" and not lazy-loaded; load the video file after it.
- How: A video element is an LCP candidate: its time is the poster image load or the first frame, whichever is earlier. Make the poster an img-like resource discoverable early with fetchpriority="high" where it is the largest element, never lazy-load it, and defer the video file.
- Satisfies: perf-lcp
### Tickers for decoration only (`vd-marquee`) [craft-consensus · verified]
Use tickers for decoration only: pause on hover and focus, duplicate content hidden from assistive technology, no critical information inside, static when reduced motion is on, and never styled like an ad.
- How: Pause on hover or focus is an extra, not a replacement for a persistent control (WCAG: a control that pauses only while focused does not qualify). A static row of the same logos is the reduced-motion version. The APG carousel pattern is a model for rotating content: the rotation control is the first tab stop and rotation stops when focus enters or the mouse hovers.
- Satisfies: ux-no-ad-lookalikes, ux-carousel-caution, a11y-pause-stop-hide
### Calm loops around headline and CTA (`vd-calm`) [our-take · judgement]
Keep the loop calm and slow around the headline and call to action, and let the headline, tagline and logo stay static.
- How: Choose footage with low motion near text areas, or add a scrim.
- Satisfies: ux-minimal-motion
- Verification note: our judgement
### Scroll-snap sliders without autoplay (`video-and-ambient-motion--comp-content-slider-no-autoplay`) [craft-consensus · partly-verified]
Build sliders as scroll-snap lists with labelled prev/next buttons and no autoplay.
- How: Load the page for 30 seconds without input: nothing moves. Tab through: arrows reachable, scroller focusable with visible focus, hidden slides' links not focusable. Check prev/next buttons have names. (Derived from the rule; see its sources.)
- Satisfies: comp-content-slider-no-autoplay
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Live captions for live streams (`video-and-ambient-motion--a11y-captions-live`) [craft-consensus · verified]
If you embed a live stream, use a player and a captioning service that supply live captions.
- How: If the page embeds a live stream, enable captions in the player during the live event and confirm they track speech; otherwise mark not applicable. (Derived from the rule; see its sources.)
- Satisfies: a11y-captions-live
### Scrim behind text on media (`video-and-ambient-motion--craft-contrast-text-on-media`) [craft-consensus · verified]
Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- How: Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (Derived from the rule; see its sources.)
- Satisfies: craft-contrast-text-on-media
### Skip link above video and scrim (`vd-skip-layering`) [craft-consensus · verified]
Give the skip link a z-index above the hero video and scrim so it is visible when focused.
- How: A skip link that is not positioned paints under a later position:relative or absolute hero; set position:absolute with z-index (for example 100) on the skip link. Found by auditing the recipe demo page in Chrome (the Tab traversal probe reported the focused skip link as covered).
- Satisfies: a11y-focus-not-obscured, a11y-bypass-blocks
### Stepped rem hero heading (`vid-hero-type-reflow`) [standard · verified]
Step the hero h1 in rem (2rem, then 2.75rem from min-width: 40em) with overflow-wrap: anywhere; do not use clamp() with vw, which the resize-text check flags.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; a fixed 2.75rem h1 overflowed a 224 px content box by 33 px at 200% text; the stepped size fitted the longest word at 223 px in a 256 px box.
- Satisfies: a11y-reflow

# Recipe: Scroll-driven stories, parallax and text effects (`scroll-stories`)
Styles covered: chaptered-story, scroll-triggered, parallax, long-scroll-narrative, text-effects
**Keep:** Pinned sections, chapters, reveal-on-scroll, parallax layers, kinetic type.
**Avoid:** Scroll hijacking; content that exists only after an animation; the call to action buried at the end; effects with no reduced-motion version.
Keep the sense of a narrative that unfolds. Use native scrolling, keep content in the page whether or not the effect runs, give the most important information and the main action early, and offer a reduced version.
**While designing:** Use native scroll and CSS timelines with @supports, keep all content in the DOM, put the point and primary action early, add a reduced-motion version, and keep effects to transform and opacity.
## Steps
### Keep native scrolling (`ss-native-scroll`) [craft-consensus · verified]
Use the browser's own scrolling with sticky positioning or scroll-linked animation; do not take over scroll speed or direction.
- How: CSS scroll-driven animations (animation-timeline: scroll() or view()) are Baseline 2026 and absent in older browsers; feature-detect with @supports and show the final state when unsupported. Declare animation-timeline after the animation shorthand.
- Satisfies: a11y-pause-stop-hide, perf-inp
### Sticky figures on wide screens only (`ss-sticky-wide-only`) [our-take · judgement]
Pin a figure with position: sticky only where there is room beside the text (about 56em and wider); on narrow screens let it scroll with the page. Do not make the header sticky.
- How: A sticky figure in a single column covers the paragraphs it should sit beside, and a sticky header can fully cover a focused link. Use scroll-padding-top if a fixed bar is unavoidable, and keep decorative fixed elements (a progress bar) pointer-events:none and aria-hidden.
- Satisfies: a11y-focus-not-obscured, a11y-reflow
- Verification note: design advice; no fixed header was tested because the demo avoids one
### Base style is the finished state (`ss-final-state-everywhere`) [our-take · verified]
Every effect, including purely decorative ones such as a progress bar, must have a base style that is already its finished state; set the effect's starting state only inside the @supports block.
- How: Put the whole effect layer in @supports (animation-timeline: view()) { ... } and keep the base rules free of starting states (opacity:0, translate, scaleX(0)). In the demo the progress bar had transform:scaleX(0) in the base rule, so in a browser without scroll timelines it would sit at zero forever; the fix was display:none in the base rule and display:block plus scaleX(0) inside @supports.
- Satisfies: perf-core-first, a11y-reduced-motion
- Verification note: checked by renaming animation-timeline in a copy of the page to simulate no support and reading computed styles; the other effects were already final in that state
### Content in the DOM first (`ss-content-first`) [craft-consensus · verified]
All text and links exist in the DOM in reading order, visible without the animation. An effect may reveal or move content, not create it.
- How: Test with JavaScript off and with the effect stylesheet removed.
- Satisfies: perf-core-first
### Open with the point (`ss-front-load`) [our-take · verified]
Open with the point: what the page is and who it is for in the first chapter, and the primary action visible in the first viewport and repeated as the story ends.
- How: A story can build, but the first screen must already answer what and why.
- Satisfies: ux-front-load, ux-primary-cta-above-fold
### Fades instead of large movement (`ss-reduced`) [craft-consensus · verified]
Under reduced motion replace large movement (parallax, scaling, sliding) with fades or a static layout, and keep what the motion conveyed.
- How: Swap transforms for opacity changes in the reduce media query rather than deleting content.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
```css
@media (prefers-reduced-motion: reduce) {
  .reveal { animation: none; transition: opacity .2s linear; transform: none; }
  .parallax-layer { transform: none !important; }
}
```
### Opacity-only reveals under reduce (`ss-reduced-keep-fade`) [craft-consensus · verified]
In the reduce query, keep the reveals as an opacity-only fade on the same timeline and set parallax and pinned-figure animation to none, so the figure shows its final state and the caption states what the motion showed.
- How: Nest @media (prefers-reduced-motion: reduce) inside the @supports block and swap the keyframes name for an opacity-only keyframe; set animation:none on parallax layers and on the pinned figure. Playwright with reducedMotion:'reduce' confirmed computed transform:none on the parallax layer, the water level and the line masks, with opacity fades still driven by view(). Always give the figure a text caption with the numbers or years the motion conveyed.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
```css
@supports (animation-timeline: view()) {
  .reveal { animation: rise linear both; animation-timeline: view(); animation-range: entry 0% entry 55%; }
  @media (prefers-reduced-motion: reduce) {
    .reveal { animation: fade linear both; animation-timeline: view(); animation-range: entry 0% entry 55%; }
    .parallax-layer { animation: none; transform: none; }
  }
}
```
### Shallow parallax, never behind text (`ss-parallax-limits`) [our-take · partly-verified]
Keep parallax shallow, never behind text, and stop it when the user asks for less motion; parallax layers are decoration.
- How: WCAG 2.3.3 (Level AAA) names parallax scrolling as a common non-essential motion effect and recommends honoring the reduced-motion setting (technique C39, JavaScript SCR40). Limiting depth and turning it off on small screens is our judgement.
- Satisfies: a11y-pause-stop-hide, a11y-reduced-motion
- Verification note: depth and small-screen advice is our judgement; the rule that parallax should be disable-able is verified
### Keep text as real text (`ss-text-effects`) [craft-consensus · partly-verified]
Keep text as real text. Prefer effects that do not split it (masks, whole-line reveals). If you must split text into spans, keep the full string available to assistive technology once, and hide the pieces.
- How: MDN: aria-label is not supported on generic elements (a bare div or span), so do not rely on it on a parent of split spans. Either give the container a role that supports naming where one genuinely fits, or add one screen-reader-only element holding the full text (WebAIM: off-screen positioning or a 1 px clip-based technique; never display:none or hidden) and mark the split spans aria-hidden (MDN lists duplicated or redundant text as a use; never on or around focusable elements). Use sparingly and test with a screen reader.
- Satisfies: a11y-reduced-motion, ux-minimal-motion
- Verification note: the two techniques are verified; applying them to split-text effects is our composition and no page addresses it
### Animate transform and opacity only (`ss-inp`) [craft-consensus · verified]
Drive effects from compositor-friendly properties (transform, opacity) and avoid reading layout in scroll handlers.
- How: Prefer CSS timelines or IntersectionObserver to scroll listeners, and animate transform and opacity only (the only compositor-only properties, per web.dev).
- Satisfies: perf-inp
### Keep animated shapes in their box (`ss-animated-shapes-inside-box`) [our-take · verified]
Keep animated geometry inside its container: scale an SVG shape from its edge (transform-box: fill-box; transform-origin: 50% 100%) instead of translating a taller shape out of its viewBox.
- How: axe-core's color-contrast rule reported 'background color could not be determined because it is overlapped by another element' for the figcaption under a pinned SVG, caused by a translated rect whose box extended below the SVG's viewBox. Removing the animation cleared it; replacing translateY with scaleY and transform-box: fill-box cleared it with the animation kept (a11y-contrast-text went from 'check' to clean).
- Satisfies: a11y-contrast-text, perf-cls
- Verification note: axe incomplete count went from 1 to 0 on the demo at desktop and mobile widths after the change
### Sentences of about 15 words (`scroll-stories--copy-sentence-length`) [craft-consensus · partly-verified]
Write body sentences of about 15 words, split any that pass 25, and read each aloud before keeping it.
- How: Extract visible text of p, li and blockquote elements, split on sentence terminators, count words per sentence. Fail on any sentence over 25 words; fail the page if the mean exceeds 20. Ignore headings, buttons and legal text. (Derived from the rule; see its sources.)
- Satisfies: copy-sentence-length
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headings that state the finding (`scroll-stories--copy-heading-informative`) [craft-consensus · partly-verified]
Write each heading as the finding of its section, so the headings alone tell the story.
- How: Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (Derived from the rule; see its sources.)
- Satisfies: copy-heading-informative
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Minmax tracks and wrapping words (`ss-reflow-grids-and-words`) [standard · verified]
Give one-column grids an explicit grid-template-columns: minmax(0, 1fr) (an implicit auto track grows to its min-content), use minmax(min(15rem, 100%), 1fr) for card grids and overflow-wrap: anywhere on headings and paragraphs.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; scrollWidth went 520, then 327, then 351 (text spacing on long words) and finally 320 after the three changes.
- Satisfies: a11y-reflow

# Recipe: Intro animations and preloaders (`intro-and-preloaders`)
Styles covered: intro-preloader
**Keep:** A designed opening moment, a branded reveal.
**Avoid:** A screen that blocks content until assets load; long sequences on every visit; counters that count up while nothing is ready; layout shifts when the overlay leaves.
Prefer no preloader. If the brand needs an opening moment, keep it short, skippable and non-blocking so it costs no loading time, causes no layout shift and does not read as a popup.
**While designing:** Default to no preloader; if one is required keep it once-per-session, skippable, non-blocking, free of layout shift, and off under reduced motion.
## Steps
### Ask if a preloader is needed (`ip-prefer-none`) [evidence · verified]
First ask whether the preloader is needed. A progressive reveal of real content (headline, then image) gives the same feeling without hiding the page.
- How: NN/g lists popups and splash screens among the most disliked homepage elements, except where legally required.
- Satisfies: ux-no-popups, perf-lcp
### Short, skippable, once per session (`ip-short-skippable`) [our-take · judgement]
If you keep it: show it once per session, make it very short, let any key press or click skip it, and remove it from the page afterwards.
- How: Store a session flag; skip entirely under reduced motion. WCAG 2.2.2 notes a preload animation may count as essential only when users cannot interact during the preload and the animation signals progress.
- Satisfies: ux-no-popups, a11y-reduced-motion
- Verification note: the session flag and skip behavior are our judgement
```css
@media (prefers-reduced-motion: reduce) {
  .reveal { animation: none; transition: opacity .2s linear; transform: none; }
  .parallax-layer { transform: none !important; }
}
```
### Narrow skip keydown handler (`ip-skip-listener-audit-note`) [our-take · verified]
Expect the audit to flag a document-level keydown handler for the skip, and keep the handler narrow: it only removes the curtain, then unregisters itself.
- How: The audit counts addEventListener('keydown') on window or document at registration time and reports a11y-char-shortcuts as 'incomplete' (a person must check), not as a failure. Registering on the curtain element is not possible because it is not focusable and has pointer-events:none. Remove the listener inside done() and do not map any individual key to another action.
- Satisfies: a11y-char-shortcuts
- Verification note: the audit printed 'check [major] a11y-char-shortcuts: 1 document-level keydown handler(s) registered' for the demo; no failure
### Read session flag before paint (`ip-session-flag-before-paint`) [our-take · partly-verified]
Read the session flag and the reduced-motion setting in a tiny inline script before first paint, and add the 'intro-on' class only if the intro should play.
- How: If the decision is made after paint, returning visitors see the curtain flash. A one-line synchronous script in the head (sessionStorage.getItem plus matchMedia, wrapped in try/catch because storage can throw) avoids that. This is the one head script this recipe allows; keep it under about 300 bytes and put everything else at the end of the body. Measured with the audit: LCP 40 to 50 ms, CLS 0.000, TBT 0 ms with it.
- Satisfies: ux-no-popups, a11y-reduced-motion
- Verification note: the cost of the script was measured in lab runs; the flash it prevents was reasoned about, not recorded
### Decorative curtain mechanics (`ip-curtain-mechanics`) [our-take · verified]
Implement the intro as a decorative curtain: aria-hidden, position:fixed, pointer-events:none, animated with transform only and finishing in visibility:hidden, removed from the DOM on animationend, with a timeout as a safety net.
- How: The real page underneath is already painted and interactive. Hide the curtain by default in CSS and show it only when a flag is set, so with JavaScript off it never appears (add a noscript rule too). Any key press or pointerdown calls the same done() function, which removes the curtain, removes both listeners and stores the session flag. Playwright confirmed: curtain present at 100 ms, removed by 1.75 s, removed within 80 ms after Space or a click, absent after a reload in the same session, never present under reduced motion or with JavaScript off.
- Satisfies: ux-no-popups, perf-cls, perf-lcp
### Never delay main content (`ip-lcp`) [craft-consensus · verified]
Never delay the main content for the animation. Measure LCP with and without the preloader; the page content loads underneath it.
- How: Make the LCP resource discoverable in the initial HTML and not lazy-loaded; keep render-blocking CSS and head scripts small.
- Satisfies: perf-lcp
### Measure LCP and CLS both ways (`ip-measure-with-without`) [craft-consensus · verified]
Measure LCP and CLS twice, with the flag unset and with it preset, using a PerformanceObserver; the difference should be noise.
- How: In Playwright, run once normally and once with addInitScript("sessionStorage.setItem('flag','1')"), and observe largest-contentful-paint and layout-shift with buffered:true. Demo result in lab Chrome: with the curtain LCP 52 ms (h1), without 36 ms (h1), CLS 0 in both; the curtain's own text was not the LCP element.
- Satisfies: perf-lcp, perf-cls
- Verification note: single-run lab numbers on a local file; field data will differ
### Overlay exit moves nothing (`ip-cls`) [craft-consensus · verified]
The overlay leaving must not move content: reserve all space, animate with transform and opacity, and keep fonts and images from reflowing.
- How: Set width and height or aspect-ratio on images and video, reserve space for anything that arrives late, and animate transform and opacity rather than top, left or box-shadow so the overlay leaving does not move content. Check layout shift in a performance trace across the whole sequence.
- Satisfies: perf-cls
### Minmax tracks and wrapping buttons (`ip-reflow-200`) [standard · verified]
Use minmax(0, 1fr) for hero grid tracks, minmax(min(15rem, 100%), 1fr) for card grids, and overflow-wrap: anywhere with max-width: 100% on buttons and long call-to-action labels, so nothing stretches the page at 320 px with 200% text.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; a 1fr track sized to its min-content gave a 335 px column, cards at minmax(15rem,1fr) were 480 px; after the changes scrollWidth was 320.
- Satisfies: a11y-reflow
### Avoid the cream-terracotta-serif reflex (`ip-no-reflex-cream`) [our-take · partly-verified]
If the page uses cream, terracotta and serif display type together, that trips distinct-palette-not-reflex-cream and an HTML comment does not satisfy the audit: pick sans headings or another palette unless the brief requires the combination, and record the reason in direction.md.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; advisory failed with cream, terracotta and serif; it passed after switching to bold system sans headings. The check is static and ignores comments.
- Satisfies: distinct-palette-not-reflex-cream
- Verification note: Recorded from one audit run on one demo page; the audit check is a heuristic and the technique has no independent source.

# Recipe: Unusual navigation, asymmetric and app-like layouts (`unconventional-nav-and-layout`)
Styles covered: unusual-nav, hamburger-only, command-palette, floating-dock, anchor-only, unconventional-layout, asymmetric, experimental, app-shell, split-screen
**Keep:** Expressive navigation, off-grid composition, dock and command-palette patterns, app-like shells.
**Avoid:** Hiding all navigation on desktop; reordering content visually without reordering the code; sticky elements that cover focus; keyboard-only shortcuts as the sole way in.
Spend your convention budget deliberately. Be unusual in looks and composition while keeping a visible way to reach the main sections, a logical code order, a skip link and a working keyboard path.
**While designing:** Be inventive in layout but keep visible primary links on desktop, a skip link first, code order equal to reading order, sticky elements that do not cover focus, a single-column reflow at 320 px, and a written reason for each unconventional choice.
## Steps
### Keep primary sections visible (`nv-visible-links`) [evidence · verified]
On desktop keep the primary sections visible as links, even in a compact or unusual form. On mobile show up to four directly; use a menu button for more, and add in-page links to key content.
- How: In the cited study navigation was used in 27% of desktop tasks when hidden versus 48% visible (2016, six sites). A command palette or hamburger can supplement visible links.
- Satisfies: ux-visible-navigation
### Skip link and landmarks (`nv-skip-and-landmarks`) [craft-consensus · verified]
Put a skip link first in the DOM, and use landmarks (header, nav, main, footer) with labels where there are several.
- How: A skip link (technique G1) should be the first focusable control; WCAG does not require it to be visible when it lacks focus, so one that appears on focus passes, though always visible is preferred. WebAIM: a hidden-until-focus link must become prominently visible on focus, and display:none or the hidden attribute must not be used. Landmarks (ARIA11) or headings (H69) also satisfy 2.4.1, and WebAIM notes a starting h1 or main region can meet it. Layering: give the skip link a z-index above positioned hero layers (a position:relative hero later in the DOM paints over an unpositioned skip link and hides it on focus); the recipe demo pages caught this in a real browser.
- Satisfies: a11y-bypass-blocks
### Disclosure buttons for dropdowns (`nv-menu-button`) [craft-consensus · verified]
Build site-navigation dropdowns as disclosure buttons, not ARIA menus: a real button with aria-expanded (aria-controls is optional in the pattern), Enter and Space toggle it, Escape closes the dropdown and returns focus to the button, and the link for the current page carries aria-current="page".
- How: APG's disclosure navigation example states it deliberately does not use the ARIA menu role, because typical site navigation does not need menu keyboard behavior. Tab moves through buttons and links; arrow keys, Home and End are optional additions. Test with a screen reader.
- Satisfies: a11y-keyboard
### Command palette as native dialog (`nv-palette-dialog`) [craft-consensus · verified]
Build a command palette as a native dialog opened with showModal(), containing a labelled combobox input, a listbox with tabindex=-1, a visible Close button and a role=status line for the result count. Opening moves focus to the input, Escape clears the text first and then closes, and closing returns focus to the button that opened it.
- How: Keyboard pass in Chrome 2026-11-06: Ctrl+K and Enter or Space on the Search buttons open it with focus in the input; typing filters and aria-activedescendant resolves to an option; Down and Up move it with wrap; Enter on an option closes the dialog, updates the hash and focuses the target section; the first Escape clears the text, the second closes and focus returns to the opener. Tab never reaches the page behind (native showModal makes it inert; the Tab after the last control goes to the browser UI, not the page). Pitfall measured: when the listbox has overflow:auto and its options overflow, Chrome makes the listbox itself a Tab stop (an extra stop between the input and the Close button); tabindex="-1" on the listbox removes it, which is correct here because the options are reached through aria-activedescendant. Options are plain role=option items, so the same destinations must also exist as real links elsewhere (the demo builds the palette from the footer site index).
- Satisfies: comp-dialog-focus, comp-dialog-semantics, comp-combobox-semantics, comp-combobox-keyboard, a11y-keyboard
### Keep DOM in reading order (`nv-dom-order`) [craft-consensus · verified]
Compose off-grid with CSS Grid areas and positioning while keeping the DOM in reading order. Avoid using order or absolute positioning to rearrange content that carries sequence.
- How: WCAG 1.3.2: failure F1 is CSS positioning that changes meaning; technique C27 makes the DOM order match the visual order. MDN: the CSS order property changes only the visual order, not the logical or tab order, and creates a mismatch for screen reader and keyboard users. Disabling CSS to read the order is a practical check (inferred; not described on WCAG's page).
- Satisfies: a11y-meaningful-sequence, a11y-focus-order
### Sticky bars must not hide focus (`nv-not-obscured`) [craft-consensus · verified]
Sticky docks, headers and banners must not hide the focused element; leave room with scroll padding.
- How: WCAG technique C43 (CSS scroll-padding) is the only sufficient technique listed for 2.4.11; failure F110 is a sticky header or footer that completely hides focused elements, and partial covering is allowed. A sticky banner can also pass by being modal, closing when it loses focus, or not overlapping content. MDN's scroll-padding page shows the fixed-header anchor case. Test with the keyboard at several viewport sizes.
- Satisfies: a11y-focus-not-obscured
```css
html { scroll-padding-top: var(--dock-height); }
```
### Bottom dock needs scroll padding (`nv-dock-bottom-padding`) [craft-consensus · verified]
A fixed bottom dock needs scroll-padding-bottom and matching body padding, not only scroll-padding-top. Make the dock fixed only when the viewport leaves room (for example min-width:20em and min-height:30em); below that let it sit in the page flow.
- How: Measured 2026-11-06 in Chrome with a real Tab pass over 28 stops of the demo page: with scroll-padding-bottom and body padding, no focused element was covered at 1440x900 or 390x844. Removing both left 2 stops partly covered at 1440x900 (one 4 of 5 sample points) and 11 stops partly covered at 390x844. The audit's own check only fails when a focus target is entirely covered, so these partial covers are invisible to it; WCAG 2.4.11 allows partial covering but a link 80% under the dock is not usable. A dock that stays fixed at 320x225 (400% zoom) would take about a third of the viewport, so below the size query it falls back to a static bar at the end of the page (checked: 0 covered stops at 320x225, 640x450, 390x844, 1440x900).
- Satisfies: a11y-focus-not-obscured, a11y-reflow
```css
.dock { margin: 1rem auto; }
@media (min-width: 20em) and (min-height: 30em) {
  html { scroll-padding-bottom: calc(var(--dock-h) + 1rem); }
  body { padding-bottom: var(--dock-h); }
  .dock { position: fixed; bottom: .75rem; left: 50%; transform: translateX(-50%); }
}
```
### Single-key shortcuts can be turned off (`nv-shortcuts`) [craft-consensus · verified]
Single-key shortcuts (for example "/" or "k") can be turned off or only work when their component has focus; the same actions are reachable by ordinary controls.
- How: List every single-key shortcut (letters, numbers, punctuation, symbols, including those needing Shift, and sequences such as G then A). Each must be able to be turned off, remapped to include a non-printable key, or be active only while its component has focus (technique G217; failure F99). Give each a visible button equivalent as good practice.
- Satisfies: a11y-char-shortcuts, a11y-keyboard
### Use a modifier for palette shortcut (`nv-modifier-shortcut-note`) [craft-consensus · partly-verified]
Use Ctrl or Command plus a key (for example Ctrl+K) for a palette shortcut and keep the visible button. Expect the audit to list the document-level keydown handler as 'check' for a11y-char-shortcuts; answer it by showing the shortcut needs a modifier.
- How: WCAG 2.1.4 covers shortcuts made of letters, numbers, punctuation or symbols only; a shortcut that needs a modifier such as Ctrl is not covered. Measured 2026-11-06: a single document keydown listener for Ctrl/Cmd+K makes the audit report a11y-char-shortcuts as 'check' (not a failure) because it cannot tell modifier shortcuts from single-key ones.
- Satisfies: a11y-char-shortcuts
- Verification note: audit behaviour measured; the claim that modifier shortcuts are outside 2.1.4 is from the WCAG understanding page
### Hide JavaScript-only controls (`nv-js-only-controls`) [craft-consensus · verified]
Controls that only work with JavaScript (the palette buttons) start with the hidden attribute and are revealed by the script that wires them. Add [hidden] { display: none !important } because author display rules such as display:flex override the attribute. All routes stay plain anchors so the page works with JavaScript off.
- How: Found with a JavaScript-off Playwright pass 2026-11-06: a .controls { display:flex } rule overrode the hidden attribute, so dead Previous and Next buttons stayed visible; adding the !important rule hid them. With JavaScript off the demo still reaches every section by Tab and Enter on the rail, the dock or the footer index.
- Satisfies: a11y-keyboard, ux-visible-navigation, perf-core-first
### Logo links home (`nv-logo-home`) [evidence · verified]
Keep the logo linking home in a findable place, even in an unusual layout.
- How: Conventional placement (top-left in left-to-right languages) is the safe default.
- Satisfies: ux-logo-home
### Collapse to one column at 320 px (`nv-reflow`) [craft-consensus · verified]
App shells and split screens collapse to a single column at narrow widths (320 CSS px) without two-dimensional scrolling.
- How: Check at 320 px wide and at 400% zoom.
- Satisfies: a11y-reflow
### Test reflow at 320 px and 200% (`nv-reflow-text-200`) [craft-consensus · verified]
Test reflow twice: at a 320 px viewport and at 320 px with the root font size raised to 200%. Let nav lists wrap, switch to multi-column grids only above a breakpoint (rem column gaps in a 12-column grid add up to more than 320 px at 200% text), and add overflow-wrap:anywhere to paragraphs that hold long strings such as email addresses and to headings and labels. Give a one-column form grid grid-template-columns: minmax(0, 1fr), or its inputs and buttons stretch it past the viewport (a heading that cannot break, 333 px in a 256 px column at 200% text, also overflowed).
- How: Measured 2026-11-06 with html { font-size: 200% } at a 320 px viewport: the first draft of the demo scrolled horizontally because (1) a 12-column hero grid with 1rem gaps needed 11 rem of gap (352 px at 200%), (2) the dock was one non-wrapping row of five 3.5 rem buttons, and (3) an email address could not break. After a grid that starts at 48em, a wrapping dock list, a static dock below the size query and overflow-wrap:anywhere, scrollWidth equalled clientWidth at 320 px for 100% and 200% text. The audit's reflow probe only checks 100% text, so none of this showed up there.
- Satisfies: a11y-reflow, a11y-resize-text
### Justify each unconventional choice (`nv-justify`) [our-take · judgement]
Write down why each unconventional choice earns its cost, and keep the rest of the page conventional.
- How: One or two surprises per page is a workable limit; this is a judgement, not a measured number.
- Satisfies: ux-conventional-layout
- Verification note: our judgement
### Menu role for action menus only (`unconventional-nav-and-layout--comp-menu-button-action-menu`) [craft-consensus · verified]
Use role=menu only for action menus and implement every key the APG lists, or use a disclosure instead.
- How: Keyboard-test: open with Enter, Space, Down; move with arrows (Home/End); Escape returns focus to the button; Tab closes. Check aria-expanded flips. (Derived from the rule; see its sources.)
- Satisfies: comp-menu-button-action-menu
### Site nav without menu roles (`unconventional-nav-and-layout--comp-site-nav-no-menu-role`) [craft-consensus · partly-verified]
Build header menus as nav > ul with a button[aria-expanded] per dropdown and plain links inside.
- How: In header nav: assert no [role=menu|menubar|menuitem]; submenus triggered by button[aria-expanded]; first link of an opened list follows the button in focus order; nav has accessible name when more than one. (Derived from the rule; see its sources.)
- Satisfies: comp-site-nav-no-menu-role
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Prefer native select (`unconventional-nav-and-layout--comp-listbox-select-semantics`) [craft-consensus · verified]
Prefer a native select; build a custom listbox only with full APG keys and short option labels.
- How: Inspect roles and states; keyboard test Up/Down/Home/End and typing a letter; scan options for nested a/button/input. (Derived from the rule; see its sources.)
- Satisfies: comp-listbox-select-semantics
### Combobox focus stays in the input (`unconventional-nav-and-layout--comp-combobox-semantics`) [craft-consensus · verified]
Keep DOM focus in the input and move aria-activedescendant through the options.
- How: Open the popup and assert on the input: role=combobox, aria-expanded=true, aria-controls resolves to a visible listbox, aria-activedescendant changes with Down arrow and resolves to an option; label via label/aria-labelledby. (Derived from the rule; see its sources.)
- Satisfies: comp-combobox-semantics
### Combobox keyboard keys per APG (`unconventional-nav-and-layout--comp-combobox-keyboard`) [craft-consensus · verified]
Implement Down, Up, Enter, Escape and Alt+Down exactly as the APG lists.
- How: Type, press Down, Enter, Escape, Tab in order and verify each outcome and that focus never leaves the input. (Derived from the rule; see its sources.)
- Satisfies: comp-combobox-keyboard
### Provide a second route (`unconventional-nav-and-layout--a11y-multiple-ways`) [craft-consensus · verified]
Provide main navigation and a second route (search, sitemap or footer index) on every multi-page site.
- How: Pick 3 inner pages and show two independent routes to each (nav + search, nav + sitemap, home page links + previous/next). Process pages (checkout steps, search results) are exempt. (Derived from the rule; see its sources.)
- Satisfies: a11y-multiple-ways
### Link text names the destination (`unconventional-nav-and-layout--copy-link-text-unique-destination`) [craft-consensus · partly-verified]
Write link text that names the destination and say 'PDF, 2 MB' or 'opens in a new window' when it applies.
- How: Collect all anchors with accessible names. Fail if two different hrefs share the same name, if a name matches /^(click here|here|more|read more|link|this)$/i or contains 'link', if an href ends in a document extension without format and size in the name, or if target=_blank lacks a notice placed after the main text. (Derived from the rule; see its sources.)
- Satisfies: copy-link-text-unique-destination
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Breakpoints where content breaks (`unconventional-nav-and-layout--craft-breakpoints-content-based`) [craft-consensus · partly-verified]
Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- How: Sweep the viewport from 320 to 1920 px in 40px steps. At each step assert no horizontal scrollbar (scrollWidth <= clientWidth), no element overlapping its sibling's box, and the measure rule still passes. Inspect media queries: list breakpoint values and flag any matching device presets (375, 414, 768 and 1024 px) written in px for review. (Derived from the rule; see its sources.)
- Satisfies: craft-breakpoints-content-based
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified

# Recipe: Drag interactions and horizontal scrolling (`drag-and-horizontal-scroll`)
Styles covered: drag-interaction, horizontal-scroll
**Keep:** Draggable galleries, swipe rows, horizontally scrolling sections.
**Avoid:** Drag as the only way to move; scroll containers that keyboards cannot reach; horizontal scroll that cannot reflow; gestures that need two fingers.
Keep the tactile, sideways-moving feel. Add buttons and keys that do the same thing, make sure a single tap works, and let narrow screens stack the content.
**While designing:** Every drag or swipe gets visible buttons and arrow-key support, works with a single tap, and stacks vertically at narrow widths.
## Steps
### Previous and next buttons (`dh-buttons`) [craft-consensus · verified]
Provide previous and next buttons (visible, labelled, 24 px or larger) for every draggable or swipeable row; dragging stays as a bonus.
- How: Single pointer, no drag required (technique G219). WCAG's own carousel example has forward and back buttons that may be visually hidden but must be pointer-operable. At either end, mark the button aria-disabled="true" (and style it as disabled) rather than hiding it or using the disabled attribute, which can drop keyboard focus when the pressed button disables itself (our judgement; Chrome behaviour with disabled not measured).
- Satisfies: a11y-dragging, a11y-pointer-gestures
### Mouse-only drag that keeps taps (`dh-mouse-drag-safe`) [craft-consensus · verified]
Add mouse drag only for pointerType 'mouse', without pointer capture, and keep taps working: ignore moves under 5 px, set pointer-events:none on links while a drag is in progress, call preventDefault on dragstart, switch scroll-snap off during the drag and back on after it, and add scroll-padding-inline equal to the scroller's padding so the first card snaps to scrollLeft 0. Leave touch and pen to native scrolling (no two-finger gesture).
- How: Playwright 2026-11-06: a 200 px mouse drag moved the strip one card (292 px) and left the URL hash empty; a drag that started on a card link did not follow the link; a plain click on a link followed it; a CDP touch swipe scrolled the strip natively (288 px). Without scroll-padding-inline the first card snapped at scrollLeft 4, which left Previous enabled at the start.
- Satisfies: a11y-pointer-gestures, a11y-dragging
### aria-disabled at either end (`dh-buttons-aria-disabled`) [our-take · partly-verified]
Give Previous and Next visible text (an SVG arrow with aria-hidden is fine) and use aria-disabled="true" rather than the disabled attribute at either end, ignoring clicks while it is set, so a keyboard user who presses Next to the end keeps focus on the button.
- How: Measured 2026-11-06: pressing Enter on Next 12 times left document.activeElement on Next at the end (aria-disabled). Icon-only buttons whose text was an arrow character made axe report color-contrast and label-content-name-mismatch as 'incomplete' (non-text characters, unverifiable label); visible words Previous and Next with an aria-hidden SVG produced no axe violations or incompletes. Not measured: what Chrome does with focus when a focused button gets the disabled attribute; the aria-disabled choice is our judgement about avoiding that.
- Satisfies: a11y-dragging, a11y-pointer-gestures, a11y-keyboard, a11y-label-in-name
- Verification note: focus staying on an aria-disabled button measured; the alternative with disabled was not measured
### Keyboard-scrollable row (`dh-keyboard`) [craft-consensus · partly-verified]
Make sure keyboard users can reach and scroll the row: if the items are focusable, the browser scrolls focus into view; if the scroller has no focusable children, the scroller itself must be focusable.
- How: Chrome makes scrollers with no focusable children keyboard-focusable by default (announced for 130, rollout delayed to 132); with focusable children, Tab goes to the children. Deque's axe rule: make the scroller or a static element inside it focusable (tabindex="0"); a region whose only content is tabindex="-1" controls fails. Avoid tabindex="-1" on a scroller users need. Accessible names for scrollers are not addressed by the Chrome or Deque pages; MDN says a bare div cannot take aria-label, so a name would need a role that supports one.
- Satisfies: a11y-keyboard
- Verification note: naming a focusable scroller is not covered by any page read
### Inert cards that are mostly off-screen (`dh-offscreen-inert`) [craft-consensus · verified]
Make the scroller a labelled region with tabindex=0 and set inert on cards that are less than half visible (IntersectionObserver rooted at the scroller), except a card that contains focus. Without JavaScript every card link stays focusable and the browser scrolls it into view.
- How: Measured 2026-11-06 in Chrome at 1280 px: scroll-snap-type:x mandatory with a focused scroller scrolled by arrow keys (scrollLeft 4, 292, 580: one card per press), so no custom key handler was needed; Home and End did not scroll it. With inert on off-screen cards, Tab from the scroller reached only the 4 visible card links of 8 and each landed inside the scroller box. With JavaScript off, ArrowRight scrolled the scroller and Tab reached the last card link (scrollLeft 1176). This resolves the tension between dh-keyboard (focusable items scroll into view) and the content-slider rule (hidden slides' links not focusable): use inert when JavaScript runs and leave the links focusable when it does not.
- Satisfies: a11y-keyboard, comp-content-slider-no-autoplay
### Stack items on narrow screens (`dh-reflow`) [craft-consensus · verified]
Below a narrow width, stack the items in a single vertical column or let the row wrap, instead of requiring horizontal scrolling for the whole page.
- How: WCAG Reflow: vertically scrolling content at 320 CSS px wide and horizontally scrolling content at 256 CSS px tall, without two-dimensional scrolling. A horizontal carousel passes if each panel fits within 320 px (G225); a table in its own scrollable container passes if the surrounding content reflows; exceptions cover maps, diagrams, video, games, presentations, data tables and toolbar-in-view interfaces.
- Satisfies: a11y-reflow
### Check stacked layout at 200% text (`dh-reflow-text-200`) [craft-consensus · verified]
Check the stacked layout at a 320 px viewport with the root font size at 200% as well: let nav lists wrap and add overflow-wrap:anywhere to paragraphs that contain long strings such as email addresses and to headings, and give flex children that hold a heading min-width:0.
- How: Measured 2026-11-06 with html { font-size: 200% } at 320 px: the nav list (display:flex without wrap) and an email link in the help section scrolled the page horizontally. flex-wrap:wrap and overflow-wrap:anywhere fixed both; afterwards no body descendant extended beyond the viewport.
- Satisfies: a11y-reflow, a11y-resize-text
### Script-revealed prev and next (`dh-js-only-hidden`) [craft-consensus · verified]
Previous and Next start with the hidden attribute and are revealed by the script that wires them, with [hidden] { display: none !important } in the CSS. Hide them too in the stacked layout where there is nothing to scroll.
- How: JavaScript-off Playwright pass 2026-11-06: the author rule .controls { display:flex } overrode the hidden attribute and left dead buttons on screen; the !important rule fixed it. Stacked widths 320, 390 and 640 px had no horizontal scroll and the strip had no overflow.
- Satisfies: a11y-keyboard, perf-core-first
### Use a native range input (`drag-and-horizontal-scroll--comp-slider-semantics`) [craft-consensus · verified]
Prefer input type=range; add output text next to it and aria-valuetext when units matter.
- How: Inspect value attributes; keyboard test arrows/Home/End/PageUp/PageDown; check aria-valuetext shows units; test with VoiceOver on iOS or TalkBack. (Derived from the rule; see its sources.)
- Satisfies: comp-slider-semantics
### Scroll-snap sliders without autoplay (`drag-and-horizontal-scroll--comp-content-slider-no-autoplay`) [craft-consensus · partly-verified]
Build sliders as scroll-snap lists with labelled prev/next buttons and no autoplay.
- How: Load the page for 30 seconds without input: nothing moves. Tab through: arrows reachable, scroller focusable with visible focus, hidden slides' links not focusable. Check prev/next buttons have names. (Derived from the rule; see its sources.)
- Satisfies: comp-content-slider-no-autoplay
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Breakpoints where content breaks (`drag-and-horizontal-scroll--craft-breakpoints-content-based`) [craft-consensus · partly-verified]
Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- How: Sweep the viewport from 320 to 1920 px in 40px steps. At each step assert no horizontal scrollbar (scrollWidth <= clientWidth), no element overlapping its sibling's box, and the measure rule still passes. Inspect media queries: list breakpoint values and flag any matching device presets (375, 414, 768 and 1024 px) written in px for review. (Derived from the rule; see its sources.)
- Satisfies: craft-breakpoints-content-based
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Name the strip so audits check it (`dh-audit-probe-note`) [our-take · judgement]
Name the strip with a 'carousel' class (or any element the audit's carousel selector matches) so the audit raises the drag and pointer-gesture rules for human review instead of marking them not applicable.
- How: The audit's gesture probe counts draggable=true attributes, range inputs, canvases and carousel library classes. A strip that uses only pointer events and has no matching class is reported as 'not applicable' for a11y-dragging and a11y-pointer-gestures, which hides the one place a drag alternative must be checked. Measured by reading the probe source and by the 'check' status the demo received once its wrapper used the class carousel.
- Satisfies: a11y-dragging, a11y-pointer-gestures
- Verification note: about the audit tool, not WCAG; the real fix is a better probe

# Recipe: Oversized and expressive type, and theme switching (`big-type-and-modes`)
Styles covered: oversized-type, expressive-type, mode-switching
**Keep:** Huge headlines, lettering, theme or mode changes.
**Avoid:** Type sized only in viewport units; headlines as images; lettering that is the only place the page states its purpose; mode switches that rename things.
Keep the giant, characterful type. Size it in a way that still scales with the user's settings, keep headings real headings, and keep switches between modes predictable.
**While designing:** Use fluid type that includes a rem component, keep headings as real text, and keep mode switches predictable and announced.
## Steps
### Big type in rem, not viewport units (`bt-scalable`) [craft-consensus · verified]
Size big type in rem or em, stepped at breakpoints, with no viewport units in font-size. Keep the smallest-breakpoint size at least 40% of the largest so a high page zoom can still reach twice the 100% size. Keep the largest hero size at 6rem (96 px) or less and the hero headline under 40 characters: the audit's distinct-hero-headline-proportion fails a hero above 96 px, and one of 72 px or more with 40 or more characters.
- How: Measured 2026-11-05 in headless Chrome (see content/learn/measurements/type-zoom-2026-11-05.json): at 100% the sizes were 118 (clamp with vw), 112 (stepped rem) and 102 px (8vw). Under 200% text-only enlargement: stepped rem doubled to 224 px; clamp with vw grew only to 134 px (1.14×); 8vw did not change (1.0×). Under 200% page zoom the breakpoint shrank the sizes: stepped rem showed 80 and 96 device px against 112 at 100%. WCAG accepts shrinking at small breakpoints if 200% is still reachable; computed at the 500% browser maximum, a 2.5rem small size reaches 200 px (1.79×, short) and a 3rem small size reaches 240 px (2.14×). WCAG lists viewport-unit misuse as failure F94. Measured 2026-11-06: at 7rem the audit reported '112 px is over 96 px, 112 px and 61 characters'; at 6rem with a 38-character h1 no failure (small size 3rem is 50% of the large).
- Satisfies: a11y-resize-text
```css
h1 { font-size: 3rem; }                        /* small size ≥ 40% of the largest */
@media (min-width: 48em) { h1 { font-size: 4rem; } }
@media (min-width: 80em) { h1 { font-size: 6rem; overflow-wrap: anywhere; } }
```
### Wrap everything, check 320 px at 200% (`bt-scalable-wrap-everything`) [craft-consensus · verified]
Put overflow-wrap:anywhere on h1, h2 and paragraphs, and let nav lists wrap, then check a 320 px viewport with the root font size at 200%.
- How: Measured 2026-11-06 at 320 px with html { font-size: 200% }: h1 was 96 px and did not scroll the page (overflow-wrap:anywhere), but the nav list (display:flex without wrap) scrolled it to 461 px, and long words such as 'pavement.' overflowed their cards (price text at 64 px inside 144 px of content). After flex-wrap:wrap and overflow-wrap:anywhere on p, no element extended beyond the viewport.
- Satisfies: a11y-resize-text, a11y-reflow
### Smallest size at half the largest (`bt-scalable-reach-by-400`) [our-take · judgement]
If 200% must be reachable at 400% page zoom (not only at the 500% browser maximum), keep the smallest breakpoint size at or above half of the largest (for example 3.5rem against 7rem) instead of 40%.
- How: Measured 2026-11-06 on the demo (h1 3rem, 4rem at 48em, 7rem at 80em; 1280 px screen): device pixels of the h1 were 112 at 100%, 96 at 200% (0.86x), 144 at 300%, 192 at 400% (1.71x) and 240 at 500% (2.14x). Under text-only enlargement (root font size 200%) it was 224 (2.00x). So the 40% rule from bt-scalable gives 2x only at about 500%. Raising the small size to 3.5rem would give 224 device px at 400% (computed, not rendered).
- Satisfies: a11y-resize-text
- Verification note: the 3.5rem figure is arithmetic from the measured sizes; a person must judge whether 56 px headings still fit a 320 px column
### Headlines as real heading text (`bt-real-text`) [craft-consensus · verified]
Headlines and key labels are real text in real heading elements, even if they are drawn with a custom face; avoid images of text.
- How: WCAG 1.4.5: use real text when the technology can achieve the look. Images of text are allowed only for logotypes, when the presentation is essential, or when users can customize them. Repeating the heading as real text next to decorative lettering is a common mitigation but is not a listed exception.
- Satisfies: a11y-headings-labels, a11y-images-of-text
### Predictable mode switch (`bt-mode-predictable`) [craft-consensus · verified]
A theme or mode switch keeps the same labels, order and positions across modes, remembers the choice, starts from the system preference, and announces its state.
- How: Use a toggle button with aria-pressed and a label that does not change (for example "Dark mode"), or a button whose label changes ("Switch to dark" / "Switch to light") without aria-pressed; do not combine them (APG button pattern). Read prefers-color-scheme (Baseline widely available since January 2020) for the initial state. MDN's page does not cover manual overrides, so store the user's choice yourself.
- Satisfies: a11y-consistent
### Light, dark and system radios (`bt-theme-three-state`) [craft-consensus · verified]
For Light, Dark and System, use a fieldset with a legend and three native radios (labels never change), an inline script in the head that applies a saved explicit choice before first paint, CSS that follows prefers-color-scheme unless data-theme says otherwise (with color-scheme set), a role=status line stating the current theme, and the switch hidden until JavaScript runs. Choosing System removes the saved value.
- How: Playwright keyboard pass 2026-11-06 with the OS set to dark: the page starts as System and dark; Tab lands once on the checked radio; ArrowLeft selects Dark then Light (background changes, localStorage written, status text updates); the choice survives reload; labels and positions are identical in light and dark; choosing System clears the value and follows a live OS change from dark to light; with JavaScript off the page follows the OS and the switch is hidden. axe-core found no violations or incompletes in light, in dark through the OS setting, in dark through data-theme, and with data-theme=light over an OS dark setting.
- Satisfies: a11y-consistent, comp-theme-switcher-control, comp-switch-label-stable, perf-core-first
```css
:root { --bg:#FBF7EF; --text:#17130F; color-scheme: light; }
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) { --bg:#14110E; --text:#F5EFE4; color-scheme: dark; }
}
:root[data-theme="dark"] { --bg:#14110E; --text:#F5EFE4; color-scheme: dark; }
```
### Name toggles after the setting (`big-type-and-modes--comp-switch-label-stable`) [craft-consensus · partly-verified]
Name toggles after the setting ('Dark mode') and flip only aria-pressed or aria-checked.
- How: Toggle each control and assert its accessible name is identical before and after, aria-checked/aria-pressed/checked is explicit 'true' or 'false', and Space toggles it. (Derived from the rule; see its sources.)
- Satisfies: comp-switch-label-stable
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headline as one buyer's result (`big-type-and-modes--copy-headline-swap-test`) [craft-consensus · partly-verified]
Write the headline as the result one named buyer gets, using a noun or number only this product can claim.
- How: Read the H1 and subhead alone. (1) Does it say what is offered and for whom? (2) Paste it with a competitor's name: does it still read true? If yes, fail. (3) Fail if it matches the template 'The [AI-powered|modern|all-in-one] [noun] for [teams|businesses|everyone]'. (Derived from the rule; see its sources.)
- Satisfies: copy-headline-swap-test
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Headings that state the finding (`big-type-and-modes--copy-heading-informative`) [craft-consensus · partly-verified]
Write each heading as the finding of its section, so the headings alone tell the story.
- How: Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (Derived from the rule; see its sources.)
- Satisfies: copy-heading-informative
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Cap line length near 55ch (`big-type-and-modes--craft-measure-body`) [craft-consensus · partly-verified]
Wrap every block of running text in a container with max-inline-size of about 50ch to 55ch (never above 60ch) and let the container, not the viewport, decide the line length.
- How: At widths 320, 768, 1280 and 1920 px, find every paragraph/list-item/blockquote with more than two lines of text. Compute characters per line (text length divided by rendered line count, or compute container inline-size divided by the width of one '0' glyph, i.e. in ch). Fail if any exceeds 75. For the lower bound, where the viewport allows it (>= 768px), flag single-column text below 45 characters per line for manual review. (Derived from the rule; see its sources.)
- Satisfies: craft-measure-body
- Verification note: generated from a craft-consensus rule; the technique itself was not separately verified
### Stepped rem sizes for headings (`big-type-and-modes--craft-fluid-type-rem-clamp`) [craft-consensus · verified]
Set headline sizes in rem and step them at em/rem media queries (for example 3rem, 4rem, 7rem), keeping the smallest at least 40% of the largest; do not use clamp(rem + vw) for text that must scale; test at 200% zoom and 320 px.
- How: Measured in Chrome 2026-11-05 (content/learn/measurements/type-zoom-2026-11-05.json): clamp(rem + vw) and vw sizes did not reach 200% at 200% zoom; stepped rem with small >= 40% of large did. See also step bt-scalable in big-type-and-modes.
- Satisfies: craft-fluid-type-rem-clamp

# Recipe: Editorial, newspaper and serif-led layouts that read easily (`editorial-serif-print`)
Styles covered: editorial, serif-editorial, serif-display, newspaper, editorial-feed
**Keep:** Large serif display type, multi-column text, rules between stories, pull quotes, mastheads, a lead story that is bigger than the rest, captions and bylines.
**Avoid:** Sentences over 25 words and grade-12 prose; justified text without hyphenation; kicker labels above every heading; a kicker above the main headline; dashes in headings; cream paper with a terracotta accent by reflex; thin serif cuts at body size; tables drawn as images or divs; a feed made of identical cards.
Keep the serif headlines, the columns, the rules and the front-page hierarchy. Hold body text at 18px or more, write in short plain sentences, keep tables as real tables, and give the page a paper colour that is not the default cream.
**While designing:** Serif headlines and real columns, body at 18px and 55ch, plain sentences with the summary first, a cool newsprint or subject-driven paper colour, real tables, one lead story and varied blocks.
## Verified palette: Newsprint, computed
- background: #EEF0F2
- text: #14171A
- text-muted: #4A5058
- rule: #6F767E
- accent: #8C1D2B
- link: #0B4FA3
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink on newsprint | #14171A | #EEF0F2 | 15.74:1 | 4.5:1 |
| muted caption on newsprint | #4A5058 | #EEF0F2 | 7.12:1 | 4.5:1 |
| oxblood accent text on newsprint | #8C1D2B | #EEF0F2 | 7.9:1 | 4.5:1 |
| link blue on newsprint | #0B4FA3 | #EEF0F2 | 6.9:1 | 4.5:1 |
| hairline rule on newsprint (UI, 3:1) | #6F767E | #EEF0F2 | 4.02:1 | 3:1 |
| white on oxblood button | #FFFFFF | #8C1D2B | 9.02:1 | 4.5:1 |
## Steps
### Body at 1.125rem, 55ch measure (`eds-body-measure`) [craft-consensus · verified]
Set running text at 1.125rem (18px) with line-height 1.55 and cap every text block at 55ch. Captions may drop to 0.875rem; nothing else goes below 1rem.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): on a test article the smallest computed size of p, li, td and th was 18px at both 320 and 1280 px viewports, with no horizontal overflow. Butterick advises 15 to 25 px for web body text and an average line length of 45 to 90 characters (66ch is the usual target). A rem size lets the user's browser setting scale the page.
- Satisfies: craft-body-size-min, craft-measure-body, craft-line-height-body, craft-relative-units-text
```css
body { font: 400 1.125rem/1.55 "Newsreader", Georgia, serif; }
.prose { max-inline-size: 55ch; }
figcaption { font-size: 0.875rem; }   /* captions only */
```
### Multi-column text with hairline rule (`eds-columns`) [craft-consensus · partly-verified]
Build newspaper columns with CSS multi-column (column-width, not a fixed count), a hairline column-rule, and column-span: all on headings. Keep text start-aligned; justify only with hyphens: auto and a lang attribute on html.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with columns: 22rem 3 the text ran in one 288 px column at 320 px and three 363 px columns at 1280 px, and scrollWidth equalled the viewport width at both. Computed hyphens was auto on the justified paragraphs. Source order is the reading order in multi-column, so keyboard and screen reader order stay meaningful. WCAG 1.4.12 needs layouts that survive user text-spacing overrides, so give columns no fixed height.
- Satisfies: craft-align-left-body, distinct-justified-exceptions, a11y-reflow, a11y-meaningful-sequence, a11y-text-spacing
- Verification note: The reflow, hyphens and no-overflow facts were measured and the rule exception (justified plus hyphens plus lang) comes from the guidelines. The 22rem minimum column width (about 40 characters at 18px) is our judgement; Butterick advises 45 to 90 characters and says justified text needs hyphenation and wide enough lines, so very narrow justified columns can still look gappy. Not tested with a screen reader.
```css
.cols { columns: 22rem 3; column-gap: 2rem; column-rule: 1px solid var(--rule); }
.cols h2 { column-span: all; }
.cols p { text-align: justify; hyphens: auto; }   /* needs <html lang="en"> */
@media (max-width: 40em) { .cols p { text-align: start; } }
```
### One type scale, three heading levels (`eds-scale`) [craft-consensus · verified]
Use one scale of body 1.125rem, h3 1.4rem, h2 1.75rem and an h1 stepped in rem (2.25rem, then 3.75rem from min-width: 48em); no clamp() with vw. Style at most three heading levels in articles, with at least one step of 1.25 or more.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): computed sizes were 18, 22.4, 28 and 36 px at 320 px (step ratios 1.24, 1.25, 1.29) and 18, 22.4, 28 and 60 px at 1280 px (the h1 step is 2.14); the figures were taken with an earlier clamp(2.25rem, 1.6rem + 3vw, 3.75rem) h1, and the stepped sizes in the sample give the same 36 and 60 px at the two ends. The stepped rem sizes (small 2.25rem is 60% of large) scale with the user's text-size setting, whereas a clamp with a vw term was measured not to reach 200% (type-zoom-2026-11-05). Keep the h1 under 6rem and use line-height 1.05 to 1.15 on wrapped headlines. Butterick advises at most three heading levels (two is better) with the smallest visible size increment between them, so the display h1 is the one big step and h2 and h3 differ by roughly 1.25.
- Satisfies: distinct-type-hierarchy-step, craft-heading-levels-limit, craft-fluid-type-rem-clamp, craft-heading-line-height, distinct-hero-headline-proportion
```css
:root { --s0: 1.125rem; --s1: 1.4rem; --s2: 1.75rem; --s3: 2.25rem; }
@media (min-width: 48em) { :root { --s3: 3.75rem; } }
h1 { font-size: var(--s3); line-height: 1.05; text-wrap: balance; overflow-wrap: anywhere; }
h2 { font-size: var(--s2); } h3 { font-size: var(--s1); }
```
### Serif with an optical-size axis (`eds-serif-cuts`) [craft-consensus · partly-verified]
Choose a serif with an optical-size axis for body and display (Newsreader, Source Serif 4 and Literata all have opsz and wght axes) and keep Light cuts (weight 300 or below) for display lines of 24px and up. Body and captions stay at weight 400 or heavier.
- How: Google Fonts metadata (fetched 2026-11-06) lists Newsreader (opsz 6 to 72, wght 200 to 800), Source Serif 4 (opsz 8 to 60, wght 200 to 900) and Literata (opsz 7 to 72, wght 200 to 900) as variable serifs, none on the overused-font list in the display-font rule (Fraunces and Instrument Serif are). With font-optical-sizing: auto the face draws sturdier letterforms at small sizes. Delicate high-contrast faces such as Cormorant Garamond (weights 300 to 700) and Bodoni Moda (wght 400 to 900, opsz 6 to 96) belong at display size.
- Satisfies: craft-weight-thin-limited, distinct-display-font-chosen
- Verification note: Font axes and ranges were read from Google Fonts metadata. The 300-or-lighter-at-24px-and-up limit comes from the guideline, whose Apple HIG source was only partly read. Sample rendering of each face was not checked.
```css
:root { font-optical-sizing: auto; }
h1, .display { font-weight: 300; }          /* only at 24px and up */
body, figcaption, td { font-weight: 400; }
```
### Pick paper color for the subject (`eds-paper`) [craft-consensus · verified]
Pick the paper colour for the subject. The palette above uses a cool newsprint grey (#EEF0F2) with near-black ink; if you want warm cream, record the subject reason and avoid pairing it with a terracotta accent and a serif display face by default.
- How: Computed with the WCAG 2 formula: ink on newsprint 15.74:1, muted captions 7.12:1, oxblood 7.9:1, link blue 6.9:1, white on oxblood 9.02:1. The rule colour #6F767E reaches 4.02:1 against the paper, so column rules and table lines that mark structure meet 3:1 (a lighter #8A9098 only reaches 2.81:1). Cream #F4F1EA matches the reflex-cream test (minimum channel 234, red at least green at least blue, red minus blue 10). Define every colour once as a role token.
- Satisfies: distinct-palette-not-reflex-cream, a11y-contrast-text, a11y-non-text-contrast, craft-color-role-tokens
### Limit kickers, arrows and dashes (`eds-chrome`) [craft-consensus · partly-verified]
Limit kickers (small tracked labels above headings) to ceil(sections / 3) per page, none above the main headline. Use numbers only for real sequences, at most two arrow-ended links, one dot-separated meta line, and keep em dashes out of headings and under one per 300 words. Write headings and navigation in sentence case; set bylines and dates with layout (a dl or flex gap), not middle dots.
- How: The limits are the rules' own thresholds. Butterick rejects title case and all caps for headings; GOV.UK says to write all headings in sentence case. A front page can still carry a masthead and a section label where the label adds information (a section name such as "Local news" does; a decorative "01 / Stories" does not).
- Satisfies: distinct-eyebrow-restraint, distinct-no-template-chrome, copy-em-dash-restraint, copy-sentence-case, craft-heading-sentence-case
- Verification note: Sentence case sources were read. The dash, arrow, kicker and middle-dot limits come from the detector-based guidelines, whose sources are partly read (impeccable-repo) or our-take (em dashes). Treat them as review thresholds.
### Short sentences and paragraphs (`eds-plain-copy`) [craft-consensus · partly-verified]
Write each sentence at 25 words or fewer, averaging 20 or fewer; paragraphs of one idea and at most five sentences (marketing pages three); open every article or long section with a one- or two-sentence summary that states the conclusion; choose the plain word; start with the first real fact instead of a filler opener.
- How: Sources: GOV.UK, NN/g and COGA agree on short sentences, one idea per paragraph, conclusion first; WCAG 3.1.5 asks for a summary or simpler version when text needs more than lower-secondary reading ability. A quick local check with a rough Flesch-Kincaid script (our own syllable heuristic, not an official tool, so use Hemingway or textstat for real scoring) gave grade 1.9 and a longest sentence of 12 words for a four-sentence news brief, against grade 27 and one 34-word sentence for the same news set as one long clause. Long-form voice is a craft choice: a literary feature may exceed grade 9, so open it with a plain-language standfirst and record the exception.
- Satisfies: copy-sentence-length, copy-paragraph-length, copy-reading-grade, copy-reading-level-companion, copy-plain-words, copy-summary-first, copy-no-filler-openers, a11y-reading-level-support, a11y-coga-short-paragraphs
- Verification note: The thresholds and sources were read. The grade figures came from our own approximate script and are illustrative; the exact scores depend on the tool. Whether a literary feature should be held to grade 9 is our judgement.
```js
// quick audit: flag sentences over 25 words
const long = [...document.querySelectorAll("main p")]
  .flatMap(p => p.textContent.split(/(?<=[.!?])\s+/))
  .filter(s => s.split(/\s+/).length > 25);
```
### Real lists and captioned tables (`eds-lists-tables`) [craft-consensus · verified]
Turn three or more parallel items and every procedure into ul or ol. Mark data (schedules, results, specs) as a table with a caption, th scope="col" and scope="row". If the table is wider than its container, scroll it inside a labelled container with tabindex="0".
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 4-column table in a 288 px container with overflow-x: auto and no tabindex was flagged by axe-core 4.14 as scrollable-region-focusable (serious); adding tabindex="0", role="region" and aria-labelledby pointing at the caption cleared it, and the page itself did not overflow (scrollWidth 320). WCAG 1.4.10 lets a data table scroll in its own container as a two-dimensional exception, while headings and paging around it must still reflow.
- Satisfies: copy-lists-for-parallel-items, comp-data-table-semantics, comp-data-table-overflow-focusable, a11y-semantic-structure, a11y-reflow
```html
<div class="scroll" tabindex="0" role="region" aria-labelledby="cap">
  <table>
    <caption id="cap">Opening hours, 2026</caption>
    <thead><tr><th scope="col">Day</th><th scope="col">Open</th></tr></thead>
    <tbody><tr><th scope="row">Sunday</th><td>11 to 3</td></tr></tbody>
  </table>
</div>
```
### Lead story and varied blocks (`eds-feed`) [craft-consensus · partly-verified]
For a front page or feed, make one story the lead (larger headline, more room), vary the layout of the next blocks (a list, a two-up, a rule-separated column), vary section padding, and keep the HTML in the order a reader should meet the stories. Each story is li > heading > one link; extend the click area with a stretched a::after, not a wrapping anchor.
- How: The stretched-link pattern comes from Inclusive Components (cards); the grid measurements for the same pattern (one tab stop per card, tab order equal to source order, no axe violations) are in the bento-and-card-grids recipe. The rhythm targets (no layout family for more than two consecutive sections, at least four families in eight sections, non-identical section padding) are the guideline thresholds.
- Satisfies: distinct-section-rhythm-varied, a11y-meaningful-sequence, comp-card-single-primary-link, distinct-no-identical-card-grid
- Verification note: Card markup was tested in a scratch page (see the bento recipe); the front-page rhythm advice is our judgement guided by the guideline thresholds, and its sources were partly read.

# Recipe: Condensed display type and serif-sans pairings (`condensed-and-paired-type`)
Styles covered: condensed, mixed-pairing
**Keep:** Narrow, tall display faces set large and tight; a deliberate serif and sans pairing; strong size and weight contrast.
**Avoid:** Whole headlines or buttons in capitals; capitals with no letter-spacing; a third or fourth family added for flavour; condensed faces used for paragraphs; fixed-height boxes that clip when users loosen text spacing; font swaps that move the layout.
Keep the tall, tight display lines and the contrast between two typefaces. Set condensed headlines in sentence case, limit capitals to short labels with real letter-spacing, stay at two families, and make sure fallback fonts do not shift the layout.
**While designing:** Set condensed headlines large in sentence case, use capitals only for short tracked labels, keep to two families, and tune the fallback font so the swap does not move the layout.
## Steps
### Sentence case for condensed headlines (`cp-sentence-case`) [craft-consensus · verified]
Set condensed headlines in sentence case and let the tall letterforms carry the style. Use text-transform: uppercase only for labels of three words or fewer that fit on one line. Buttons stay in sentence case.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a scan of the computed styles on a test page (condensed h1 and h2 in sentence case, a one-line uppercase label "Issue 04") found one uppercase element, one line and 8 characters; the audit snippet below lists every uppercase element with its line count and length so you can enforce the limits in CI. Butterick: capitals are fine for less than one line and wrong for whole paragraphs. UX Movement recommends sentence case for button labels and discourages all caps because the lack of word shape lowers readability.
- Satisfies: copy-no-all-caps-text, craft-caps-short-only, craft-heading-sentence-case
```js
// list uppercase elements with letter-spacing (em), rendered lines and length
[...document.querySelectorAll("body *")].filter(e => getComputedStyle(e).textTransform === "uppercase")
  .map(e => { const c = getComputedStyle(e);
    return { text: e.textContent.trim(), ls: +(parseFloat(c.letterSpacing) / parseFloat(c.fontSize)).toFixed(3),
             lines: Math.round(e.getBoundingClientRect().height / parseFloat(c.lineHeight)) }; });
```
### Track uppercase labels 0.05 to 0.12em (`cp-caps-tracking`) [craft-consensus · verified]
Give every uppercase or small-caps label letter-spacing between 0.05em and 0.12em (0.08em works). Keep body text at letter-spacing normal. A large condensed headline may be tightened slightly (about -0.01em); do not widen lowercase text.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the uppercase label computed to 0.08em; the h1 used -0.01em; the body paragraph stayed normal. Butterick recommends 5 to 12% extra space (0.05em to 0.12em in CSS) for capitals and small caps, and says lowercase letters do not ordinarily need letterspacing.
- Satisfies: craft-caps-letterspacing, craft-body-tracking-normal
```css
.label { font: 700 1rem/1 var(--display); text-transform: uppercase; letter-spacing: 0.08em; }
h1 { letter-spacing: -0.01em; }
body { letter-spacing: normal; }
```
### Rem clamp sizing for condensed h1 (`cp-fluid-size`) [craft-consensus · partly-verified]
Size condensed display type in rem stepped at breakpoints (no clamp() with vw, which cannot reach 200% under text enlargement), keep the h1 at 6rem or below, wrap it with text-wrap: balance, and use a tight line-height only on headlines (0.9 to 1.05). Choose a condensed family from the subject rather than the first one that comes to mind: Barlow Condensed (static cuts), Sofia Sans Extra Condensed (variable weight 1 to 1000), Archivo (variable width 62 to 125, so one file gives you condensed and regular) all exist in Google Fonts.
- How: Google Fonts metadata (fetched 2026-11-06) confirms the three families and the Archivo wdth axis (62 to 125) and Sofia Sans Extra Condensed wght axis (1 to 1000). Because condensed glyphs are narrow, an h1 can be larger before it wraps, but keep to the 6rem cap and about 45 characters per line. Stepped rem sizes (3rem, 4.5rem, 6rem: the small size is 50% of the large) follow the browser text-size setting and reach 200%; a clamp() with a vw term was measured not to (Roselli; type-zoom-2026-11-05).
- Satisfies: craft-fluid-type-rem-clamp, distinct-hero-headline-proportion, distinct-display-font-chosen, a11y-resize-text
- Verification note: Font availability and axes were read from metadata; the face names are examples chosen by us, not a ranking, and none was rendered. The 6rem cap and 45-character wrap come from the guidelines.
```css
h1 { font: 800 3rem/0.95 "Sofia Sans Extra Condensed", "Arial Narrow", sans-serif;
     letter-spacing: -0.01em; text-wrap: balance; max-inline-size: 18ch; overflow-wrap: anywhere; }
@media (min-width: 40em) { h1 { font-size: 4.5rem; } }
@media (min-width: 64em) { h1 { font-size: 6rem; } }
```
### Let headline blocks grow (`cp-text-spacing`) [craft-consensus · verified]
Leave condensed headline blocks to grow: no fixed height, no overflow: hidden on boxes that hold text, and tight line-height only on the headline itself. Test with the WCAG text-spacing override.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 320 px card with a 0.9 line-height condensed-style headline, then the WCAG 1.4.12 overrides injected (line-height 1.5, letter-spacing 0.12em, word-spacing 0.16em, paragraph spacing 2em): the card grew from 234 to 533 px and scrollHeight still equalled clientHeight, so nothing was clipped and the page did not scroll sideways (scrollWidth 320). The test used the fallback face (Arial Narrow or Arial), not a web font.
- Satisfies: a11y-text-spacing
```css
/* paste into devtools to test WCAG 1.4.12 */
* { line-height: 1.5 !important; letter-spacing: 0.12em !important; word-spacing: 0.16em !important; }
p { margin-bottom: 2em !important; }
```
### Exactly two type families (`cp-two-families`) [our-take · partly-verified]
For a serif and sans pairing, use exactly two families (plus mono for code if needed). Build hierarchy from size, weight, colour and case inside them: the display or headline face in one, the reading text in the other, and do not add a third face for pull quotes or buttons.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the audit below counted the first font-family of every rendered text element on a test page and returned two (Sofia Sans Extra Condensed and Newsreader). Pair for contrast in structure (a high-contrast serif with a plain sans, or a condensed display with a text serif) and make sure the two share a similar x-height at body size so the switch does not look accidental. Apple HIG and web.dev both point to a small number of families.
- Satisfies: craft-font-families-few, distinct-display-font-chosen
- Verification note: The two-family limit is a guideline we hold as our-take. The family count script was tested on a page whose web fonts were not loaded, so it reads the declared first family, which is what the guideline checks. No pairing quality claim was tested.
```js
// distinct first font families actually rendered (fails if more than 2)
new Set([...document.querySelectorAll("body *")]
  .filter(e => [...e.childNodes].some(n => n.nodeType === 3 && n.textContent.trim()))
  .map(e => getComputedStyle(e).fontFamily.split(",")[0].replace(/[\"']/g, "").trim()));
```
### Tune fallback metrics for swap (`cp-font-loading`) [craft-consensus · partly-verified]
Stop the swap from moving the layout: preload the one display file you need, use font-display: swap or optional, and tune the fallback face with size-adjust, ascent-override, descent-override and line-gap-override so its metrics match the web font. Keep CLS at 0.1 or below.
- How: web.dev (Optimize CLS): fonts can shift layout even while text is invisible because the fallback sets the layout; font-display: optional avoids a re-layout when the font is not ready; size-adjust and the related overrides reduce the size gap; a good CLS is 0.1 or less for at least 75% of visits. Compute the override values from the two fonts' metrics with a tool and measure CLS afterwards.
- Satisfies: a11y-coga-no-surprise-changes
- Verification note: The mechanism is from web.dev. No override values are given because they depend on the chosen pair, and a font-swap CLS measurement with real font files was not run.
```css
@font-face { font-family: "Display fallback"; src: local("Arial Narrow");
  size-adjust: /* from metrics */; ascent-override: /* from metrics */; }
h1 { font-family: "Sofia Sans Extra Condensed", "Display fallback", sans-serif; }
```

# Recipe: Swiss grids, utilitarian interfaces and corporate-clean pages that are not generic (`swiss-utilitarian-corporate`)
Styles covered: swiss-grid, utilitarian, corporate-clean
**Keep:** A visible column grid, neutral grotesque type, strong alignment, small labels, rules, tables, system-UI details, blue accents, product screenshots and clear sections.
**Avoid:** Inter, Helvetica or Arial as the display face by default; table cells under 16px; a label above every heading; arrow and middle-dot chrome on every link and meta line; library defaults (radius, colours, font) left as shipped; div-built product mock-ups; a hero that would read the same with a competitor's logo.
Keep the strict grid, the plain type, the dense tables and the blue-and-white product look. Choose a display face that is not the default, keep table text at 16px, use labels sparingly, and show the real product so the page does not pass the swap test.
**While designing:** Keep a visible 12-column grid and plain type; choose a display face that is not the default; table text at 16px; show the real product; set your own tokens; verify blue and grey contrast.
## Verified palette: Corporate clean and Swiss, computed
- background: #FFFFFF
- text: #1F2937
- text-muted: #4B5563
- surface: #F3F4F6
- rule: #767676
- accent: #1D4ED8
- focus: #0B5FFF
- swiss-red: #C40500
- ink: #111111
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| body text on white | #1F2937 | #FFFFFF | 14.67:1 | 4.5:1 |
| muted text on surface | #4B5563 | #F3F4F6 | 6.86:1 | 4.5:1 |
| blue link on white | #1D4ED8 | #FFFFFF | 6.7:1 | 4.5:1 |
| white on blue button | #FFFFFF | #1D4ED8 | 6.7:1 | 4.5:1 |
| structural rule on white (UI, 3:1) | #767676 | #FFFFFF | 4.54:1 | 3:1 |
| focus ring on white | #0B5FFF | #FFFFFF | 5.12:1 | 3:1 |
| focus ring on surface | #0B5FFF | #F3F4F6 | 4.65:1 | 3:1 |
| Swiss red text on off-white | #C40500 | #F2F2F0 | 5.56:1 | 4.5:1 |
| white on Swiss red | #FFFFFF | #C40500 | 6.23:1 | 4.5:1 |
| ink on off-white | #111111 | #F2F2F0 | 16.84:1 | 4.5:1 |
## Steps
### Pick a neutral grotesque (`su-display-face`) [craft-consensus · partly-verified]
Pick a neutral grotesque that is not on the overused list (Inter, Roboto, Open Sans, Lato, Montserrat, Arial, Helvetica, Geist, Plus Jakarta Sans, Space Grotesk and others) unless it is the brand's own face. Candidates present in Google Fonts: Hanken Grotesk, Schibsted Grotesk, Albert Sans, Familjen Grotesk, Public Sans, Archivo, IBM Plex Sans. Write the choice and the reason in the direction file.
- How: Google Fonts metadata (fetched 2026-11-06) lists each of the seven families as sans serif; Hanken Grotesk, Albert Sans, Familjen Grotesk and Public Sans are variable in weight, Archivo and IBM Plex Sans in weight and width. Neutral Swiss character comes from even stroke, closed apertures and tight, regular spacing; judge it by setting your real headline in two or three candidates. If the brand owns a face, use it and record the exception.
- Satisfies: distinct-display-font-chosen, distinct-written-direction
- Verification note: Availability was verified from metadata. The overused list comes from the guideline, whose sources were mostly read but whose detector is partly read. Which candidate feels most Swiss is our judgement; none was rendered.
### Twelve-column grid with fixed gutter (`su-grid`) [craft-consensus · verified]
Build the grid as 12 equal columns with a fixed gutter in a centered container no wider than 1200 to 1400px. Place items by column span at wide viewports and let every item take the full width (grid-column: 1 / -1) at narrow ones. Add overflow-wrap: anywhere to grid children so long strings cannot push the page sideways.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 12-column grid (repeat(12, minmax(0, 1fr)), 1rem gutters, 75rem max) with a heading spanning 4 columns and text spanning 8 had scrollWidth 320 at a 320 px viewport and 1280 at 1280 px, with a long unbroken string inside. Without overflow-wrap: anywhere the same string pushed scrollWidth to 471 at 320 px. Place by source order; if you place items on explicit lines, keep the DOM in reading order. The guideline cites GOV.UK layout and USWDS spacing units for capping the page container at 1400px or less.
- Satisfies: craft-container-max-width, a11y-reflow, a11y-meaningful-sequence
```css
.grid { max-inline-size: 75rem; margin-inline: auto; padding-inline: 1rem;
        display: grid; grid-template-columns: repeat(12, minmax(0, 1fr)); column-gap: 1rem; }
.grid > * { grid-column: 1 / -1; overflow-wrap: anywhere; }
@media (min-width: 48em) { .a { grid-column: 1 / span 4; } .b { grid-column: 5 / span 8; } }
```
### Hierarchy by ratio and weight gap (`su-hierarchy`) [craft-consensus · partly-verified]
Make hierarchy visible with size and weight: pick a ratio of 1.25 to 1.333 between roles (body 1rem, h3 1.333rem, h2 1.777rem, h1 2.369rem at ratio 1.333) and a weight gap of at least 200 between headings and body (400 body, 700 headings). Define the scale as tokens.
- How: The ratios are computed (1.333 compounding gives 1, 1.333, 1.777, 2.369). The guideline needs one step of at least 1.25 between neighbours and a weight gap of at least 200 for 80% of headings. Swiss typography relies on a few sizes and weights with strict alignment rather than on colour or ornament. Limit article headings to three levels (Butterick).
- Satisfies: distinct-type-hierarchy-step, craft-type-scale-tokens, craft-heading-levels-limit
- Verification note: The scale values are arithmetic and the thresholds come from the guideline (detector sources partly read). Whether 1.333 suits a given brand is a craft choice; the Swiss style does not require it.
```css
:root { --step-0: 1rem; --step-1: 1.333rem; --step-2: 1.777rem; --step-3: 2.369rem; }
body { font-weight: 400; } h1, h2, h3 { font-weight: 700; }
```
### Density from layout, not tiny type (`su-labels-and-tables`) [craft-consensus · verified]
Keep information density in the layout, not in tiny type: table cells, list items and form text stay at 1rem (16px) or above, and you get density from tight row padding and a 12-column grid. Use labels (captions, table headers, metadata) only where they add information, at 1rem unless they are true captions, at most ceil(sections / 3) labels above headings, and give capital labels 0.05 to 0.12em letter-spacing.
- How: The body-size rule counts table cells and form text as running text: only captions, footnotes and legal text may be smaller than 16px. Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a pricing-style table at 1rem with 0.75rem cell padding stayed inside its scrolling region at 320 px with no page overflow; axe flagged the scroller without tabindex="0" and passed it with tabindex, role="region" and aria-labelledby on the caption. See the editorial recipe for the markup. Letter-spacing of 0.05em to 0.12em on capitals is Butterick's range.
- Satisfies: craft-body-size-min, distinct-eyebrow-restraint, craft-caps-letterspacing, comp-data-table-semantics, comp-data-table-overflow-focusable
### Plain labels, few arrows and dots (`su-no-chrome`) [craft-consensus · partly-verified]
Write plain link and button labels. No more than two links or buttons end in an arrow, no more than one meta string uses middle dots (separate dates, authors and tags with layout: a dl in a grid, or a flex gap), em dashes stay rare, and no icon-plus-heading-plus-sentence card row is the main section.
- How: These are the guideline thresholds. GOV.UK link guidance asks for descriptive link text: say what happens, not an arrow. The system-UI feel of a utilitarian page comes from real controls (native selects, tables, rules, monospace data) rather than from decorative glyphs.
- Satisfies: distinct-no-template-chrome, distinct-eyebrow-restraint, distinct-no-identical-card-grid
- Verification note: The numeric limits come from detector-based guidelines whose sources are partly read. Our-take on style: use them as review thresholds.
### Blue and grays that pass contrast (`su-palette-focus`) [craft-consensus · verified]
Use blue as a text and button colour only where it passes: #1D4ED8 on white, with white text on a blue button. Mute secondary text no lighter than #4B5563 on a light grey surface. Draw structural rules at #767676 or darker. Give focus its own ring (#0B5FFF, 3px outline, 2px offset).
- How: Computed with the WCAG 2 formula: blue link on white 6.7:1; white on blue 6.7:1; body 14.67:1; muted 6.86:1 on #F3F4F6; a #6B7280 muted grey is only 4.83:1 on white, close to the line; rule #767676 4.54:1; focus ring 5.12:1 on white and 4.65:1 on surface. For a Swiss red, #E10600 on white reaches 4.96:1 while #C40500 reaches 6.23:1 and 5.56:1 on off-white, with white text on it at 6.23:1.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast, a11y-focus-visible, craft-color-role-tokens
```css
:focus-visible { outline: 3px solid var(--focus); outline-offset: 2px; }
```
### Prove the page is this company's (`su-swap-test`) [our-take · judgement]
Prove the page is this company's. Show the real product (a captured screen with alt text, real data, not a rectangle mock-up), build the first two viewports around one idea only this subject could carry, set your own radius, colour and type tokens before using any component library, then run the swap test: replace the logo with a competitor's and ask a reviewer who did not build it which site it is.
- How: This is the guideline's own manual check. To customise library defaults, change the radius, primary colour and font variables to your tokens and record them in the direction file; do not leave the library's init values in the shipped CSS. A corporate-clean page is allowed to be conventional in structure; the distinctiveness comes from the content, the imagery and the one idea.
- Satisfies: distinct-swap-test, distinct-customize-library-defaults, distinct-real-imagery-and-icons, distinct-hero-not-template
- Verification note: Craft opinion. The checks come from guidelines labeled our-take or built on partly read sources; no experiment shows the swap test predicts anything.

# Recipe: Luxury and opulent styles: gold, thin type and ornament that stay readable (`luxury-and-opulent`)
Styles covered: luxury, opulent
**Keep:** Near-black or burgundy grounds, ivory text, gold accents, serif display lines, ornament and dense detail, long quiet spacing, product-focused imagery.
**Avoid:** Gold text on white; light or thin weights at body size; letterspaced lowercase paragraphs; ornament behind text; stock marketing verbs (elevate, curated, timeless tapestry); text set as an image; ten equal choices on the first screen.
Keep the deep colours, the gold, the generous space and the ornament. Use a gold that passes on its ground, keep light type weights for large display lines, write in plain words, and make ornament decorative so it never carries the message.
**While designing:** Gold that passes on its ground, light weights only at display size, plain factual copy in sentence case, ornament as decoration, one dominant choice per screen.
## Verified palette: Ivory and gold on night, with a burgundy variant, computed
- background: #0E0D0B
- text: #F3EEE4
- text-muted: #B5AE9F
- accent: #C9A24B
- accent-line: #8F7433
- light-background: #FAF7F0
- accent-on-light: #7A5A12
- ink-on-light: #1B1A17
- burgundy-background: #4A0F1F
- gold-on-burgundy: #D9B866
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ivory text on night | #F3EEE4 | #0E0D0B | 16.79:1 | 4.5:1 |
| muted text on night | #B5AE9F | #0E0D0B | 8.8:1 | 4.5:1 |
| gold text on night | #C9A24B | #0E0D0B | 8.09:1 | 4.5:1 |
| night text on gold button | #0E0D0B | #C9A24B | 8.09:1 | 4.5:1 |
| gold hairline on night (UI, 3:1) | #8F7433 | #0E0D0B | 4.36:1 | 3:1 |
| deep gold text on ivory | #7A5A12 | #FAF7F0 | 5.95:1 | 4.5:1 |
| ink on ivory | #1B1A17 | #FAF7F0 | 16.26:1 | 4.5:1 |
| ivory text on burgundy | #F3EEE4 | #4A0F1F | 13.16:1 | 4.5:1 |
| gold text on burgundy | #D9B866 | #4A0F1F | 7.97:1 | 4.5:1 |
## Steps
### Choose gold by its ground (`lo-gold`) [craft-consensus · verified]
Choose gold by the ground it sits on. On near-black use #C9A24B for text and buttons (with night text on the button). On ivory use a deep gold such as #7A5A12 for text. Use #8F7433 or lighter for thin decorative lines only where 3:1 is enough.
- How: Computed with the WCAG 2 formula: gold #C9A24B on #0E0D0B 8.09:1; ivory text 16.79:1; muted #B5AE9F 8.8:1; a #8F7433 hairline 4.36:1. The same gold #C9A24B on white is only 2.39:1, so it fails for text and for icons that carry meaning. Deep gold #7A5A12 on ivory #FAF7F0 5.95:1. Burgundy #4A0F1F: ivory 13.16:1, gold #D9B866 7.97:1. A metallic gradient on text must be tested at its darkest and lightest stops.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Light weights for large display only (`lo-type-weights`) [craft-consensus · partly-verified]
Reserve weight 300 or lighter for display lines of 24px and up; body and anything under 24px stays at 400 or heavier. Keep lowercase body text at letter-spacing normal. Track only uppercase labels (0.05 to 0.12em) and keep those to three words or fewer on one line.
- How: Thin high-contrast serifs (Cormorant Garamond, weights 300 to 700; Bodoni Moda, 400 to 900 with an optical-size axis; both in Google Fonts) look refined at display size and break up at body size, so raise the size or the weight instead of the tracking. Butterick: capitals take 5 to 12% letterspacing, lowercase does not ordinarily need it; capitals are for less than one line.
- Satisfies: craft-weight-thin-limited, craft-body-tracking-normal, craft-caps-letterspacing, craft-caps-short-only, craft-body-size-min
- Verification note: Capitals and tracking advice was read from Butterick. The 300-weight and 24px threshold comes from the guideline (Apple HIG source partly read), and the font axes from metadata. The label is set at 1rem: the body-size rule counts a label paragraph as running text, so a smaller label size would fail. No face was rendered.
```css
.display { font: 300 2.5rem/1.05 "Cormorant Garamond", Georgia, serif; overflow-wrap: anywhere; }
@media (min-width: 48em) { .display { font-size: 3.5rem; } }
@media (min-width: 64em) { .display { font-size: 5rem; } }
body { font: 400 1.0625rem/1.6 "Newsreader", Georgia, serif; letter-spacing: normal; }
.label { text-transform: uppercase; letter-spacing: 0.1em; font-weight: 500; font-size: 1rem; }
```
### Luxury copy as plain facts (`lo-plain-copy`) [craft-consensus · partly-verified]
Write luxury copy as facts in ordinary words: where it is made, by whom, how long it takes, what is guaranteed. Remove stock marketing verbs and metaphors (unlock, elevate, curated, journey, tapestry, realm), use sentence case in headings, buttons and navigation, and name navigation items literally ("Watches", "Book a visit", not "Discover the journey").
- How: The buzzword list and plain-language rules come from the guidelines and GOV.UK, NN/g and COGA. A rough local score (our own approximate syllable script, illustrative only) gave grade 16 for "Elevate your journey with an unparalleled tapestry of timeless craftsmanship, where every moment is curated to transcend the ordinary." and grade 3 for "Each watch is made by hand in our Geneva workshop. One maker builds one watch, which takes about nine weeks. We service every watch for life." The plain version carries three checkable facts; the buzzword version carries none. Prestige can still come from restraint: short lines and specific numbers.
- Satisfies: copy-no-buzzwords, a11y-coga-plain-literal-language, copy-sentence-case, craft-heading-sentence-case, a11y-reading-level-support
- Verification note: Rules and sources were read; the readability scores came from an approximate script and the example brand is invented. Whether plain facts make a luxury brand feel more or less premium is our judgement.
### Ornament as decoration only (`lo-ornament`) [craft-consensus · verified]
Treat ornament as decoration: borders, flourishes, monograms and patterns are CSS backgrounds or SVG with alt="" (or aria-hidden="true"), never the only place a name, price or instruction appears. Put text on a solid panel, not on a patterned or photographic ground. Keep headings and prices as real text, and use an image of text only for a logo.
- How: NN/g: an image is decorative if users can complete all tasks and understand all information without it, and gets an empty alt. WCAG 1.4.5 allows images of text for logotypes or when the presentation is essential. For text over ornament or photography, the scrim math in the hero-and-photography recipe applies: a 60% black overlay keeps white text at 5.74:1 even over a pure white backdrop (measured in Chrome).
- Satisfies: a11y-alt-text, a11y-images-of-text, a11y-coga-text-not-over-busy-background, craft-contrast-text-on-media
### One dominant thing per screen (`lo-restraint`) [our-take · judgement]
Give each screen one dominant thing and at most five main choices. An opulent page may be dense in detail, but make the one feature or call to action visibly larger than the others and move secondary links under a titled "more" link or into the footer. Keep prices, fees and conditions visible where the choice is made.
- How: COGA asks for about five or fewer main choices per screen and one visually dominant feature; the same document asks for costs to be stated at the start of a booking or purchase. Luxury practice often hides the price; that is a brand choice that conflicts with the guidance, so record the exception if you keep it.
- Satisfies: a11y-coga-limit-choices-per-screen, a11y-coga-key-tasks-prominent, a11y-coga-costs-up-front
- Verification note: The COGA guidance was read, but applying it to luxury is our judgement and trades some mystique for clarity.

# Recipe: Bento, catalog and gallery grids that reflow and read in order (`bento-and-card-grids`)
Styles covered: bento-grid, catalog-grid, gallery-wall
**Keep:** Tiles of different sizes, rounded cards, dense product or image grids, a dominant lead tile.
**Avoid:** Spans that overflow at 320px; grid-auto-flow: dense or order used to move content out of source order; whole-card wrapper links with several tab stops; rows of identical icon cards; cards nested inside cards; ten equal choices on the first screen; images without reserved space.
Keep the mosaic of mixed-size tiles, the product grid and the image wall. Start from a one-column grid that needs no media query to fit 320px, add spans only on wide screens, keep the HTML in reading order, make each card one list item with one link, and let one item lead.
**While designing:** Use auto-fit minmax(min(100%, 15rem), 1fr) with spans only on wide screens, keep source order equal to reading order, li > heading > one link with a stretched ::after, and let one tile lead.
## Steps
### Auto-fit grid, spans in media query (`bg-reflow`) [craft-consensus · verified]
Base the grid on repeat(auto-fit, minmax(min(100%, 15rem), 1fr)) so every tile fits a 320px viewport with no media query. Add column and row spans only inside a min-width media query, set min-inline-size: 0 and overflow-wrap: anywhere on tiles, and wrap the grid in a centered container no wider than 1200 to 1400px.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 6-tile bento (one 2x2 lead, one 2-wide tile, four singles) in a 75rem container had scrollWidth 320 with one 288px column at a 320 px viewport, and four 288px columns with the lead spanning 592px at 1280 px. WCAG 1.4.10 requires content to work at 320 CSS px without two-dimensional scrolling. Switch to spans at 50em because that is where four tracks fit, not at a device width.
- Satisfies: a11y-reflow, craft-container-max-width, craft-breakpoints-content-based
```css
.bento { list-style: none; margin: 0; padding: 0; display: grid; gap: 1rem;
         grid-template-columns: repeat(auto-fit, minmax(min(100%, 15rem), 1fr)); }
.bento > li { min-inline-size: 0; overflow-wrap: anywhere; }
@media (min-width: 50em) {
  .bento { grid-template-columns: repeat(4, 1fr); }
  .lead { grid-column: span 2; grid-row: span 2; }
  .wide { grid-column: span 2; }
}
```
### HTML in reading order (`bg-order`) [craft-consensus · verified]
Write the HTML in the order you want read and tabbed, most important tile first. Do not use order or grid-auto-flow: dense to rearrange content that has a meaning order, and check with a script that visual order equals DOM order.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): three tiles (two spanning 2 columns, one spanning 1) in a 3-column grid had DOM order one, two, three and the same visual order by default. With grid-auto-flow: dense the third tile moved up beside the first, so the visual order became one, three, two while keyboard focus still went one, two, three. MDN: order and grid placement change visual order only, not the order assistive technology or tab navigation use, and style sheets that use them for logical reordering are non-conforming. In the 6-tile bento above (no dense) tab order equalled visual order at 320 and 1280.
- Satisfies: a11y-meaningful-sequence, a11y-focus-order
```js
// fails when visual reading order (row, then column) differs from DOM order
const items = [...document.querySelectorAll(".bento > li")];
const rects = items.map((li, i) => ({ i, ...li.getBoundingClientRect().toJSON() }));
const visual = [...rects].sort((a, b) => a.top - b.top || a.left - b.left).map(r => r.i);
console.assert(visual.every((v, i) => v === i), "visual order differs from DOM order");
```
### Card markup with stretched link (`bg-card-markup`) [craft-consensus · verified]
Mark each tile as li > heading > a, make the heading link the only tab stop, and extend the click area with a stretched a::after. Draw the focus ring on that ::after so it surrounds the whole card. Decorative images get alt=""; a "read more" cue is non-interactive text.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): each of six tiles held exactly one focusable element; Tab visited them in DOM order; axe-core 4.14 reported no violations at 320 and 1280 px. In a separate one-card page, the computed style on the focused link's ::after was outline: solid 3px rgb(11, 95, 255), a ring of 5.12:1 against white (5.12:1 computed). The ::after covers the whole tile, so the target is well above 24 by 24 px. Link text carries the purpose (the heading), as WCAG 2.4.4 asks.
- Satisfies: comp-card-single-primary-link, comp-card-limited-tab-stops, a11y-focus-visible, a11y-link-purpose, a11y-target-size
```css
.bento > li { position: relative; }
.bento a { color: inherit; }
.bento a::after { content: ""; position: absolute; inset: 0; border-radius: inherit; }
.bento a:focus-visible { outline: none; }
.bento a:focus-visible::after { outline: 3px solid #0B5FFF; outline-offset: 3px; }
```
### Lead tile takes the most space (`bg-lead-variety`) [craft-consensus · partly-verified]
Let the most important tile take the most space (2x2 or full width) and show it as a real example, not an icon. Size the other tiles to their content, not to fill a pattern. Group content inside a tile with space, rules and type, never with a second bordered card inside the first. Do not use emoji as tile icons.
- How: These follow the guideline checks: no section made mainly of three or more same-size icon-heading-sentence cards; no bordered or shaded container inside another; section order and block count driven by the buyer's questions. The bento above uses a 2x2 lead and a 2-wide tile so the widths differ.
- Satisfies: distinct-no-identical-card-grid, distinct-no-nested-cards, copy-section-content-drives-structure
- Verification note: The thresholds come from detector-style guidelines whose sources were partly read, and the our-take section-order rule; this is craft advice, not tested against user outcomes.
### One lead, about five choices (`bg-limit-choices`) [craft-consensus · partly-verified]
Show one dominant item and at most about five equal choices in each viewport-height section. For a catalog or gallery with many items, put the first row or two on screen, then use filters, a paged list or a real "show more" button; keep price, fees and key conditions on each product card. Reserve each image's space with width and height or aspect-ratio and crop with object-fit: cover and object-position, not by stretching.
- How: COGA: about five or fewer main choices per screen, one visually dominant feature, costs shown at the start. A shop grid necessarily lists many products, so the guidance is applied as hierarchy (one lead, filters, paging) rather than as a hard cap. The image-space and CLS measurement is in the hero-and-photography recipe: without width and height an image loading late gave CLS 0.0293 in Chrome and with them 0. Product images that show the product need alt text that names it; purely decorative tiles use alt="" (NN/g).
- Satisfies: a11y-coga-limit-choices-per-screen, a11y-coga-costs-up-front, craft-image-dimensions-reserved, craft-image-no-distortion, a11y-alt-text
- Verification note: The five-choice limit is COGA guidance, not a studied threshold, and a shop grid cannot meet it literally; the hierarchy approach is our judgement.

# Recipe: Photography-led and centered heroes with readable text and fast images (`hero-and-photography`)
Styles covered: photography, hero-centered, standout-hero
**Keep:** Large photographs, a centered headline and subline, a strong first screen, cropped imagery with a clear subject.
**Avoid:** White text straight on a photo; a hero image that loads late and shifts the page; the hero image as a CSS background or lazy-loaded; alt text that describes nothing; centered paragraphs of three lines or more; the stock centered badge, headline, two buttons and logo row; a headline a competitor could publish unchanged.
Keep the full-bleed photograph and the big centered headline. Put a measured scrim behind text, reserve image space and never lazy-load the hero image, write real alt text, centre only short lines, and build the first screen around something only this subject has.
**While designing:** Photo hero with a 60% scrim behind text, hero img in HTML with width, height and fetchpriority high, center only a two-line subline, and a first screen built around a real subject element and a headline a competitor could not copy.
## Verified palette: Scrim math for text over the brightest photo, computed
- text: #FFFFFF
- scrim-60: rgb(0 0 0 / 0.6)
- worst-case backdrop: #FFFFFF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white text on 60% black scrim over pure white | #FFFFFF | #666666 | 5.74:1 | 4.5:1 |
| white text on 55% black scrim over pure white | #FFFFFF | #737373 | 4.74:1 | 4.5:1 |
| large white text (24px+) on 42% scrim over pure white | #FFFFFF | #949494 | 3.03:1 | 3:1 |
| white text on 50% black scrim over bright yellow #FFD400 | #FFFFFF | #806a00 | 5.27:1 | 4.5:1 |
## Steps
### Scrim between photo and text (`hp-scrim`) [standard · verified]
Put a scrim between the photo and any text: a 60% black overlay (or a gradient that stays at or above 55% under the text lines) keeps white text at 4.5:1 or better over even a pure white photo. Test the brightest area at 375, 768 and 1440px, not the average.
- How: Computed: the minimum black overlay alpha for white text at 4.5:1 over pure white is 0.54 (0.42 for 24px-and-larger text at 3:1). A 0.6 overlay gives 5.74:1, 0.55 gives 4.74:1, and over bright yellow #FFD400 a 0.5 overlay gives 5.27:1. Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 20rem hero with a pure-white image and a 0.6 gradient overlay rendered #666666 under the heading (pixel sampled from a screenshot), a ratio of 5.74:1 with white text. Real photos have bright spots, so check the lightest area behind each line.
- Satisfies: craft-contrast-text-on-media, a11y-contrast-text, a11y-coga-text-not-over-busy-background
```css
.hero { position: relative; color: #fff; isolation: isolate; }
.hero::before { content: ""; position: absolute; inset: 0; z-index: -1;
  background: linear-gradient(to top, rgb(0 0 0 / 0.6), rgb(0 0 0 / 0.6)); }  /* flat 60% under text */
```
### Hero img with alt and priority (`hp-alt-lcp`) [craft-consensus · verified]
Put the hero image in the HTML as an img with width and height, fetchpriority="high" and no loading="lazy". Write alt text for what the image adds in context (under about 150 characters, key words first), alt="" if it is decoration, and describe the destination for linked images.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a test page whose below-the-fold figure loaded 800 ms late measured CLS 0.0293 without width and height attributes and 0.0000 with them. web.dev: never lazy-load the LCP image, make it discoverable in the initial HTML (not a CSS background or script-injected), and fetchpriority="high" on one or two images at most. NN/g: decorative images get alt=""; informative images say what they contribute; keep alt under roughly 150 characters with the important words first.
- Satisfies: a11y-alt-text, craft-image-dimensions-reserved, a11y-coga-no-surprise-changes
```html
<img src="/img/harbour-1600.jpg" width="1600" height="900"
     srcset="/img/harbour-800.jpg 800w, /img/harbour-1600.jpg 1600w" sizes="100vw"
     fetchpriority="high" alt="Fishing boats moored in the old harbour at low tide">
```
### Crop to the subject, never stretch (`hp-crop`) [craft-consensus · partly-verified]
Fill the frame with object-fit: cover and set object-position to the subject; at small widths switch to a portrait crop with picture and media, instead of letting the subject fall outside the frame. Never stretch: the rendered ratio must match the file unless object-fit crops it.
- How: The picture element selects a different crop per media condition (web.dev Learn Responsive Design, The picture element and Responsive images). object-fit and aspect-ratio are Baseline features documented on MDN; pair aspect-ratio or width/height with the crop so the box is reserved before load.
- Satisfies: craft-image-no-distortion, craft-image-dimensions-reserved
- Verification note: The crop techniques are documented, but the MDN object-fit and aspect-ratio pages were only partly read and no crop was rendered or measured here.
```css
.hero img { inline-size: 100%; block-size: 100%; object-fit: cover; object-position: 60% 40%; }
```
### Center only headline and short subline (`hp-centered`) [craft-consensus · partly-verified]
Center only the headline and a subline that wraps to two lines or fewer. Below 48em start-align the subline, above it cap it near 56ch so it stays at two lines. Balance the headline with text-wrap: balance and keep it at 6rem or below.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 98-character subline with a 34ch cap, centered at 768 px and wider, wrapped to 3 lines (fails the "no centered paragraph of 3 lines or more" check); with a 56ch cap above 48em it wrapped to 2 lines at 768 and 1280 px, and below 48em it was start-aligned (3 lines at 320 and 390 px). The guideline's sources (Butterick on justified text and hyphenation, WCAG 1.4.8 visual presentation) favour start-aligned body text.
- Satisfies: craft-align-left-body, craft-text-wrap-balance-pretty, distinct-hero-headline-proportion
- Verification note: The line counts were measured for one sample sentence and fonts; recheck with your copy. Source support for avoiding centered paragraphs is general (start-aligned text), not a numeric line limit; the 3-line cut-off is the guideline's.
```css
h1 { font-size: 2.25rem; line-height: 1.05; text-wrap: balance; overflow-wrap: anywhere; }
.sub { max-inline-size: 34ch; }
@media (min-width: 48em) { h1 { font-size: 3.25rem; } }
@media (min-width: 64em) { h1 { font-size: 4.5rem; } }
@media (min-width: 48em) { .hero { text-align: center; } .sub { max-inline-size: 56ch; margin-inline: auto; } }
```
### Show something real in first viewport (`hp-not-template`) [craft-consensus · partly-verified]
Make the first viewport show something real from the subject (the product screen, the work, the place, the object) and keep at most two of the five stock signals: centered headline, badge or eyebrow above it, exactly two buttons, a logo row in the next section, a three-card feature row after that. A centered photographic hero usually keeps the first and drops the badge.
- How: These are the guideline's checks. No "New" or "Live" pill unless it is bound to a real state or release. Name the lead element of the hero in the written direction file before building so it is a decision, not a leftover.
- Satisfies: distinct-hero-not-template, distinct-no-fake-status-badges, distinct-real-imagery-and-icons, distinct-written-direction
- Verification note: The five-signal count comes from detector-style guidelines with partly read sources; NN/g homepage principles (read) support showing real content on the first screen, not the exact threshold.
### Headline that passes the swap test (`hp-headline`) [craft-consensus · partly-verified]
Write the H1 and subline so they name the outcome, the offer or the audience, then run the swap test: paste a direct competitor's name in and see whether it is still true. If so, rewrite with a noun, number or place only this product can claim. Avoid the template "The [modern] [category] for [teams]".
- How: Weak (illustrative): "The modern platform for teams that move fast." Stronger (illustrative): "Pay 40 suppliers in one afternoon", which states an outcome and a number. NN/g: headings are pick-up lines, so lead with the specific value in the first words. The page title should name the page's purpose too, so it is not left as the brand name alone.
- Satisfies: copy-headline-swap-test, a11y-headings-labels, a11y-page-title
- Verification note: The swap test is a manual check with a craft rationale; the example headlines are invented for illustration, and no experiment is cited that these convert better.

# Recipe: SaaS stacks, single-column pages, social proof, pricing tables and event sites (`saas-proof-pricing-event`)
Styles covered: saas-stack, single-column, standout-social-proof, standout-pricing, event-site
**Keep:** Hero, proof, features, pricing and final call to action in a familiar order; one centered reading column; logos, quotes and numbers; a highlighted plan; event dates, schedule and registration.
**Avoid:** The stock sequence with no reason; eight sections of identical padding and layout; invented logos, numbers and quotes; a logo marquee that cannot be paused; a featured plan shown by colour alone; plan names with no stated limits; hidden fees; a live stream without live captions; an auto-updating countdown that is announced every second.
Keep the classic landing sequence, the single centered column, the logo and testimonial proof, the featured pricing plan and the event countdown. Order sections by the buyer's questions, vary their shape, show only proof you can name, build pricing as a real table with units, and caption any live stream.
**While designing:** Order sections by buyer questions, vary section shapes, use only named proof, build pricing as a captioned table with units and a text-marked featured plan, and give any live stream live captions.
## Verified palette: Pricing and event colours, computed
- text: #16181D
- background: #FFFFFF
- featured-plan: #1D4ED8
- badge: #FDE68A
- logo-grey: #767676
- event-background: #0F172A
- event-accent: #FACC15
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white on featured plan header | #FFFFFF | #1D4ED8 | 6.7:1 | 4.5:1 |
| ink on "Most popular" badge | #14171A | #FDE68A | 14.44:1 | 4.5:1 |
| muted price note on white | #4B5563 | #FFFFFF | 7.55:1 | 4.5:1 |
| struck-through old price on white | #6B7280 | #FFFFFF | 4.83:1 | 4.5:1 |
| logo grey on white (graphic, 3:1) | #767676 | #FFFFFF | 4.54:1 | 3:1 |
| quote text on light surface | #14171A | #F3F4F6 | 16.34:1 | 4.5:1 |
| caption on light surface | #4B5563 | #F3F4F6 | 6.86:1 | 4.5:1 |
| white on event night | #FFFFFF | #0F172A | 17.85:1 | 4.5:1 |
| yellow accent on event night | #FACC15 | #0F172A | 11.65:1 | 4.5:1 |
| night text on yellow button | #0F172A | #FACC15 | 11.65:1 | 4.5:1 |
## Steps
### Order sections by buyer questions (`sp-sequence`) [craft-consensus · partly-verified]
Write the page brief as a list of the questions this buyer asks and the section that answers each, then order the stack by it. Keep the hero, proof, features, pricing and call to action only if each answers a question; vary section shapes (full-bleed, split, list, quote, table) so no layout family runs more than two sections in a row and an eight-section page uses at least four families. Vary the vertical padding.
- How: These are the guideline checks. For the hero, see the hero-and-photography recipe. For tile grids, see bento-and-card-grids. Content strategy sources (Halvorson, NN/g homepage principles) support organizing by user goals rather than by template.
- Satisfies: copy-section-content-drives-structure, distinct-section-rhythm-varied, distinct-no-identical-card-grid, distinct-hero-not-template
- Verification note: The thresholds are from detector-style guidelines; sources were partly read or are practitioner posts. This is craft advice with no study behind the numbers.
### Named grid lines in one column (`sp-single-column`) [craft-consensus · verified]
For a single-column page, build the column with named grid lines so text sits at 55ch, figures break out to a wider track and one band runs full width. That varies the rhythm without leaving the one-column reading order.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with this grid, paragraphs were 288 px wide at 320 px (no overflow, scrollWidth 320) and 729 px (66ch at 18px serif) at 768, 1280 and 1920 px, and the wide figure was 969 px at 1280 and 1920, with no horizontal scroll at 320, 768, 1280 or 1920 px. Zero the default figure margin or the figure shrinks (it was 208 px at 320 until margin: 0).
- Satisfies: distinct-section-rhythm-varied, craft-measure-body, craft-container-max-width, a11y-reflow
```css
.flow { display: grid; max-inline-size: 90rem; margin-inline: auto;
  grid-template-columns: [full-start] minmax(1rem, 1fr) [wide-start] minmax(0, 10rem)
    [content-start] min(55ch, 100% - 2rem) [content-end] minmax(0, 10rem) [wide-end] minmax(1rem, 1fr) [full-end]; }
.flow > * { grid-column: content; }
.flow > .wide { grid-column: wide; }
.flow > .full { grid-column: full; }
.flow figure { margin: 0; }
```
### Show only proof you can name (`sp-proof-real`) [our-take · partly-verified]
Show only proof you can name. Every statistic, quote, logo, award and superlative has a source on the page (customer name, role, date, report link) or is removed. List missing proof as a content gap for the owner instead of inventing it. Run a placeholder check before shipping. Show logos as img with alt text of the company name, no auto-scrolling marquee, in grey that keeps 3:1 against the ground.
- How: Computed: logo grey #767676 on white is 4.54:1 (a lighter #B0B0B0 is 2.16:1, which fails 3:1 for a graphic that identifies a customer). Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the placeholder pattern below matched "Acme Corp saved us 40%", "John Doe, CEO" and "Lorem ipsum dolor" and did not match "Mara Ilves, head of ops at Tallinn Bakery". WCAG 2.2.2 requires auto-moving content that runs longer than five seconds to be pausable, so prefer a static logo row. Prefer a named figure with a date ("Median ticket reply time, Q3 2026") over an unlabeled big number.
- Satisfies: copy-proof-verifiable, distinct-no-filler-copy, distinct-no-fake-status-badges, a11y-alt-text, a11y-pause-stop-hide, a11y-non-text-contrast
- Verification note: Contrast and the regex behavior were computed and tested. The rule "show only proof with a named source" is our-take; whether named proof converts better than anonymous proof was not tested.
```js
const placeholder = /\b(lorem ipsum|john doe|jane (doe|smith)|acme|globex|initech|company name|your (company|name) here)\b/i;
[...document.querySelectorAll("main *")].filter(e => placeholder.test(e.textContent) && !e.children.length);
```
### Testimonials as figure and blockquote (`sp-testimonials`) [craft-consensus · partly-verified]
Mark each testimonial as a figure with a blockquote and a figcaption holding the name, role, company and date, with a cite link to the source when one exists. Use static quotes or a plain list, not an autoplaying carousel. Quote text keeps 4.5:1 on its surface.
- How: figure and blockquote carry the quote and its attribution in the markup (WCAG 1.3.1). NN/g found carousels are often skipped, and the APG carousel pattern requires a control to stop and start any automatic rotation. Computed: near-black text on #F3F4F6 16.34:1, caption #4B5563 6.86:1.
- Satisfies: a11y-semantic-structure, comp-content-slider-no-autoplay, a11y-contrast-text, copy-proof-verifiable
- Verification note: Markup follows WCAG and HTML semantics; the example quote and person are invented placeholders and must be replaced by supplied proof. Screen reader output was not tested.
```html
<figure>
  <blockquote cite="https://example.com/case-study"><p>We cut month-end close from six days to three.</p></blockquote>
  <figcaption>Mara Ilves, head of operations, Tallinn Bakery, March 2026</figcaption>
</figure>
```
### Pricing as a real table (`sp-pricing-table`) [craft-consensus · verified]
Build the comparison as a real table: caption (stating currency, billing period and tax), thead with th scope="col", every row label a th scope="row", limits with units ("Up to 15 users", "100 GB"), all recurring costs in the table. Mark the featured plan with text ("Most popular"), not colour alone, and keep white text on its header at 4.5:1. On narrow screens let the table scroll inside a focusable labelled region.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a 3-plan table in a 288 px wrapper (min table width 36rem) had page scrollWidth 320 (no page-level overflow) and its wrapper scrolled to 576 px; axe-core 4.14 flagged the wrapper as scrollable-region-focusable (serious) until it had tabindex="0", role="region" and aria-labelledby="cap", then reported no violations. White on #1D4ED8 is 6.7:1; the "Most popular" badge, ink on #FDE68A, is 14.44:1. NN/g: state the differences between options explicitly, with units, and show all costs together.
- Satisfies: copy-explicit-option-differences, comp-data-table-semantics, comp-data-table-overflow-focusable, a11y-color-not-only, a11y-coga-costs-up-front, a11y-reflow, a11y-contrast-text
```html
<div class="scroll" tabindex="0" role="region" aria-labelledby="cap">
 <table>
  <caption id="cap">Plans compared. Prices are per workspace per month, billed monthly, in US dollars, excluding tax.</caption>
  <thead><tr><th scope="col">Feature</th><th scope="col">Starter</th>
    <th scope="col">Team <span class="badge">Most popular</span></th><th scope="col">Business</th></tr></thead>
  <tbody><tr><th scope="row">Users</th><td>Up to 3 users</td><td>Up to 15 users</td><td>Up to 100 users</td></tr></tbody>
 </table>
</div>
```
### Stable-name billing toggle (`sp-pricing-toggle`) [craft-consensus · partly-verified]
If a monthly or yearly switch changes the prices, make it one native toggle button named "Billed yearly" whose name never changes and whose state is aria-pressed (or two radios in a fieldset with a legend). After the switch, update the prices in the table and announce the change through a status region that already exists in the DOM; show the yearly total beside the monthly figure.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a toggle button named "Dark mode" kept the same accessible name before and after, exposed "pressed" through aria-pressed, and toggled with both Space and Enter; a role="status" region filled after an action was read back as text (see the interaction recipe). The same markup applies to a billing switch. Radios in a fieldset also satisfy the guideline.
- Satisfies: comp-switch-label-stable, a11y-status-messages, a11y-coga-costs-up-front
- Verification note: The control behavior was tested on a dark-mode toggle, not on a live billing switch; screen reader announcements were not tested. The advice to show the yearly total with the monthly figure comes from the costs-up-front guidance (COGA).
### Live captions for event streams (`sp-event`) [standard · partly-verified]
If the event page embeds a live stream or webinar, use a player and a captioning service that supply live captions of speech, speaker identification and significant non-speech sounds, and say on the page how to turn them on. If there is no live audio, mark the requirement not applicable. Publish recordings with captions and a transcript afterwards. Write dates as time elements with a time zone; the countdown is a visual extra, never the only place the start time appears, and it is not announced every second.
- How: WCAG 1.2.4 (Level AA) requires captions for live audio in synchronized media. It is a blocker for event sites that stream. Auto-updating content that starts automatically and lasts more than five seconds must be pausable (2.2.2); a second-by-second countdown should be visually fine but hidden from assistive technology (aria-hidden on the ticking digits) with the start date and time in plain text beside it. Show "Live" only while a stream is actually live. Event colours: white on #0F172A is 17.85:1, yellow #FACC15 on it 11.65:1, with night text on a yellow button 11.65:1.
- Satisfies: a11y-captions-live, a11y-captions, a11y-coga-media-chunks-transcripts, a11y-pause-stop-hide, a11y-status-messages, distinct-no-fake-status-badges
- Verification note: The requirements were read from the WCAG Understanding pages. We did not test a live captioning provider or player, so no vendor is recommended; the countdown advice and the date markup are our practical guidance and were not screen-reader tested.
```html
<p>Starts <time datetime="2026-11-12T09:00:00+01:00">12 November 2026, 09:00 CET</time></p>
<p aria-hidden="true" class="countdown">3 days 4 hours</p>
```

# Recipe: Dark, light and mixed-theme pages with their own checked palettes (`dark-light-mixed-themes`)
Styles covered: dark, light, mixed-theme
**Keep:** A dominant dark or light ground, or light and dark sections alternating; a strong accent colour; imagery that suits the ground.
**Avoid:** Making the dark theme by inverting the light one; reusing the light accent on a dark ground; a flash of the wrong theme at load; native controls and scrollbars in the wrong scheme; a dark band whose links use light-page tokens; a theme switch that renames itself.
Keep a dark page, a light page or alternating bands. Declare color-scheme, define each theme as its own token set with contrast checked, treat bands as local themes, and make any theme switch a labelled toggle that remembers its state. For neon and glow see dark-neon-contrast; for mode switches that rename things see big-type-and-modes.
**While designing:** Meta and CSS color-scheme, light-dark() role tokens, a separately checked dark palette, bands as local themes with their own tokens, and a labelled "Dark mode" toggle that persists.
## Verified palette: Light and dark token sets, each computed
- light-background: #FFFFFF
- light-text: #16181D
- light-accent: #1F4FD8
- dark-background: #12141A
- dark-text: #E8EAF0
- dark-accent: #8FB0FF
- dark-surface: #1B1E27
- dark-focus: #7FB3FF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| light: text on background | #16181D | #FFFFFF | 17.75:1 | 4.5:1 |
| light: muted text on surface | #4B5160 | #F3F4F7 | 7.21:1 | 4.5:1 |
| light: accent link on background | #1F4FD8 | #FFFFFF | 6.62:1 | 4.5:1 |
| light: border (UI) | #7A8190 | #FFFFFF | 3.91:1 | 3:1 |
| light: focus ring on surface | #0B5FFF | #F3F4F7 | 4.66:1 | 3:1 |
| dark: text on background | #E8EAF0 | #12141A | 15.3:1 | 4.5:1 |
| dark: muted text on surface | #A3AABB | #1B1E27 | 7.15:1 | 4.5:1 |
| dark: accent link on background | #8FB0FF | #12141A | 8.61:1 | 4.5:1 |
| dark: dark text on accent button | #0B1020 | #8FB0FF | 8.85:1 | 4.5:1 |
| dark: border (UI) | #6B7385 | #12141A | 3.87:1 | 3:1 |
| dark: focus ring on surface | #7FB3FF | #1B1E27 | 7.76:1 | 3:1 |
## Steps
### Declare schemes with light-dark() (`tm-scheme`) [craft-consensus · verified]
Declare the schemes the page supports in a meta tag placed before any CSS and in CSS on :root, define colours once as role tokens with light-dark(), and let prefers-color-scheme choose the default. A deliberately single-theme page may declare color-scheme: only light or only dark, knowing that this also opts the page out of the browser's automatic dark rendering.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with <meta name="color-scheme" content="light dark"> and :root { color-scheme: light dark } plus light-dark() tokens, emulating colorScheme light gave a white background and #16181D text, and dark gave rgb(18, 20, 26) and rgb(232, 234, 240); getComputedStyle(html).colorScheme was "light dark" in both; a native text input drew a dark background (rgb(59, 59, 59)) in the dark scheme. MDN: color-scheme changes canvas, scrollbars and form controls and is Baseline widely available since January 2022; the meta tag before CSS helps avoid a flash at load; it does not restyle your own content, so use prefers-color-scheme or light-dark() for that.
- Satisfies: craft-dark-mode-scheme, craft-color-role-tokens
```html
<meta name="color-scheme" content="light dark">
<style>
 :root { color-scheme: light dark;
   --bg: light-dark(#FFFFFF, #12141A); --text: light-dark(#16181D, #E8EAF0);
   --accent: light-dark(#1F4FD8, #8FB0FF); --focus: light-dark(#0B5FFF, #7FB3FF); }
 body { background: var(--bg); color: var(--text); }
</style>
```
### Separate dark tokens, check both themes (`tm-tokens`) [craft-consensus · verified]
Author the dark palette as its own set of tokens and check every pair in both themes: 4.5:1 for text, 3:1 for large text, borders, icons and focus rings. Use lighter, less saturated accents on dark grounds, and dark text on a light accent button.
- How: Computed with the WCAG 2 formula (table above): light text 17.75:1, dark text 15.3:1; light accent link 6.62:1 but reusing that same #1F4FD8 on the dark ground gives only 2.77:1, which fails, so the dark accent is the lighter #8FB0FF (8.61:1) with #0B1020 text on a button of that colour (8.85:1). Borders are 3.91:1 light and 3.87:1 dark; focus rings 4.66:1 on the light surface and 7.76:1 on the dark one. Prefer off-black (#12141A) to pure black for large areas; pure white on pure black is 21:1 but glaring. Axe's color-contrast rule reported no violations in either scheme on the test page.
- Satisfies: craft-dark-mode-reverify, a11y-contrast-text, a11y-non-text-contrast, craft-contrast-wcag2-authoritative
### Dim photos, dark logo variants (`tm-images`) [craft-consensus · partly-verified]
Do not invert or filter the whole page to get a dark theme. Dim bright photographs a little in dark mode, supply dark variants of logos and diagrams with transparent backgrounds through picture and a prefers-color-scheme media query, and keep photographs' colours.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): img { filter: brightness(.85) } inside @media (prefers-color-scheme: dark) computed to "brightness(0.85)" in dark and "none" in light. The 0.85 value is our choice. The guideline, built on Apple HIG dark mode and web.dev theming, asks for a palette authored for dark, not an inverted or filtered light one.
- Satisfies: craft-dark-mode-reverify
- Verification note: The media-query behavior was measured; the 0.85 strength is our judgement, not from a source, and no image was assessed visually.
```css
@media (prefers-color-scheme: dark) { img:not([data-keep]) { filter: brightness(0.85); } }
```
### Each band as a local theme (`tm-bands`) [craft-consensus · verified]
For alternating light and dark sections, make each band its own local theme: set color-scheme on the band and override the role tokens (background, text, accent, focus) with that theme's checked values. Components inside use only tokens, so a link or input in a dark band is correct without extra CSS. Give each band a heading so the bands are real sections.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a .band with color-scheme: dark and the dark token values, inside a light page, gave a link colour rgb(143, 176, 255) in both emulated schemes and a native input with the dark control background (rgb(59, 59, 59)) even when the page itself was light; axe color-contrast reported no violations in either page scheme. The dark accent on the dark ground is 8.61:1; the light accent #1F4FD8 would be 2.77:1 there. Keep the order, labels and positions of navigation and controls the same in every band.
- Satisfies: craft-dark-mode-scheme, craft-dark-mode-reverify, a11y-focus-visible, a11y-non-text-contrast, a11y-consistent
```css
.band-dark { color-scheme: dark; --bg: #12141A; --text: #E8EAF0; --muted: #A3AABB;
  --accent: #8FB0FF; --focus: #7FB3FF; background: var(--bg); color: var(--text); }
```
### Stable-name theme switch (`tm-switch`) [craft-consensus · verified]
If you offer a theme control, make it a button with aria-pressed named after the setting ("Dark mode") that never changes its name, place it in the header or footer in the same spot on every page, start from the system preference, and remember the choice. Set the stored theme on the html element from a small inline script in the head before first paint so there is no flash. Style the on state with more than colour.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a button named "Dark mode" with aria-pressed kept the same accessible name before and after toggling, exposed [pressed] after Space, and returned to unpressed after Enter (see the interaction recipe). The guideline, built on Inclusive Components' theme switcher, asks for a labelled toggle whose state persists. Store the choice in localStorage inside try/catch, since storage can be blocked.
- Satisfies: comp-theme-switcher-control, comp-switch-label-stable, comp-toggle-visual-state-not-color, a11y-name-role-value
```html
<script>
 try { const t = localStorage.getItem("theme"); if (t) document.documentElement.dataset.theme = t; } catch (e) {}
</script>
<button type="button" aria-pressed="false" id="theme">Dark mode</button>
```
### Honor contrast and forced colors (`tm-contrast-prefs`) [craft-consensus · partly-verified]
Respect the user's contrast preferences in either theme: under prefers-contrast: more strengthen borders and muted text, and make focus, borders and state survive forced-colors: active by using real borders and outlines, not shadows or background tints alone.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): with contrast: "more" emulated, a border defined as var(--line) in a prefers-contrast: more block changed from #7A8190 to rgb(58, 65, 80). In forced-colors mode outline and border colours stay visible but box-shadow is removed (MDN), so draw focus rings with outline.
- Satisfies: craft-contrast-preferences, a11y-focus-visible
- Verification note: The prefers-contrast switch was tested in Chrome emulation; the forced-colors facts were read on MDN but forced-colors rendering was not emulated here.
```css
@media (prefers-contrast: more) { :root { --line: #3A4150; --muted: #2B3040; } }
```

# Recipe: Hover effects, micro-interactions and page transitions that work without a mouse (`hover-micro-and-page-transitions`)
Styles covered: hover-effects, micro-interactions, page-transitions
**Keep:** Hover lifts and reveals, animated toggles and buttons, success feedback, smooth cross-fades and shared-element route changes.
**Avoid:** Content that exists only on hover; tooltips that vanish when the pointer moves onto them or cannot be dismissed; tabs or menus that open only on hover; feedback over 200ms or that blocks the next click; overshoot easing; a toast as the only record of an action; toggles that rename themselves; page transitions that drop focus, keep the old title, ignore reduced motion or run for seconds.
Keep the hover reactions, the small animated feedback and the animated route changes. Make hover only an enhancement with a keyboard and touch equivalent, keep feedback under 200ms and out of the way of input, mirror every toast on the page, and run transitions only for users who allow motion, with focus, title and status handled.
**While designing:** Hover effects only as enhancements inside (hover: hover) with focus and touch parity; 100 to 200ms ease-out feedback; toggles as aria-pressed buttons with fixed names; toasts mirrored on the page; view transitions only for no-preference motion, with focus, title and status handled.
## Steps
### Hover reveals as enhancement only (`ix-hover-parity`) [craft-consensus · verified]
Make every hover reveal an enhancement. Show the content by default, and only inside @media (hover: hover) hide it until the card is hovered or contains focus (:hover and :focus-within together). On touch devices and keyboards the content is simply there.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a card with an extra line hidden only inside @media (hover: hover) had opacity 0 at rest on a desktop context, 1 after hover (and 0 again after leaving), and 1 after Tab moved focus to the link; in a touch context (hasTouch and isMobile, where (hover: hover) was false) the line was visible at rest with no hover. MDN: the hover media feature reports whether the primary input can hover conveniently; devices that only emulate hover on long tap report none, so hover must not be the only way to reach important content; hybrid devices report only the primary input, so keyboard and focus parity is still needed.
- Satisfies: a11y-coga-hierarchy-visible-no-hover-reveal, a11y-keyboard, a11y-hover-focus-content
```css
.card .more { display: block; }                       /* default: visible */
@media (hover: hover) {
  .card .more { opacity: 0; transition: opacity 150ms ease-out; }
  .card:hover .more, .card:focus-within .more { opacity: 1; }
}
```
### Accessible tooltips when needed (`ix-tooltips`) [craft-consensus · verified]
Prefer a visible text label to a tooltip. If you need a tooltip, show it on hover and keyboard focus, link it with aria-describedby, keep it text only, let Escape dismiss it without moving focus, and keep it visible while the pointer is over the bubble. For help that must work on touch, use a click-activated toggletip: a real button plus an empty role="status" region that you fill on click.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the tooltip appeared when the button received focus, disappeared on Escape while focus stayed on the button, reappeared on the next hover, and stayed visible while the pointer moved onto the bubble. The toggletip button had no aria-describedby, and after Enter the status region held "Billed monthly in US dollars, excluding tax."; Escape cleared it. WCAG 1.4.13 requires such content to be dismissible, hoverable and persistent; native title tooltips are excluded because the browser controls them.
- Satisfies: comp-tooltip-not-sole-label-no-interactive, a11y-hover-focus-content, comp-toggletip-click-live-region, comp-no-title-attribute-reliance
```html
<span class="tipwrap"><button type="button" aria-describedby="t1">Save</button>
  <span role="tooltip" id="t1" class="tip">Saves a draft</span></span>

<button type="button" aria-label="Billing help">i</button><span role="status"></span>  <!-- filled on click -->
```
### Hover-driven tabs follow the tabs pattern (`ix-hover-tabs`) [craft-consensus · verified]
When a hover effect also drives tabs or a menu, build it as the tabs pattern: only the selected tab is in the Tab order, arrow keys move between tabs, Home and End jump to the ends, and a panel that starts with non-focusable content has tabindex="0". Hover may preview a tab, but selection and content come from click and keys.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): a three-tab list with role=tablist, aria-selected, aria-controls and roving tabindex: Tab entered on the selected tab (tabindexes 0, -1, -1), ArrowRight moved to the next, End went to the last, ArrowRight wrapped to the first, Home returned to the first, and Tab from the tablist landed on the panel (tabindex 0). Do not use tabs for site navigation (use links).
- Satisfies: comp-tabs-keyboard, comp-tabs-semantics, a11y-coga-hierarchy-visible-no-hover-reveal
```js
tab.addEventListener("keydown", e => {
  const k = { ArrowRight: (i + 1) % n, ArrowLeft: (i + n - 1) % n, Home: 0, End: n - 1 }[e.key];
  if (k !== undefined) { e.preventDefault(); select(tabs[k], true); }   // select sets tabindex 0 / -1
});
```
### Feedback timing of 100 to 400 ms (`ix-timing`) [craft-consensus · verified]
Time interface feedback: hover, press and toggle transitions 100 to 200ms (150ms is a good default), other functional transitions at most 400ms and never over 500ms. Use ease-out for things entering and ease-in for things leaving, no overshoot curves, and keep the control usable during the animation. Under prefers-reduced-motion: reduce, drop transforms and movement and keep a plain colour or opacity change.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): transitions computed to 0.1s (press scale) and 0.15s (colour) on buttons and 0.2s on a checkmark, with cubic-bezier(0.2, 0.8, 0.2, 1) (no y value outside 0 to 1); three rapid clicks on a button during its transition were all counted (the count rose by 3), so input was not blocked; with reducedMotion: "reduce" emulated, the card reveal transition computed to 0s. NN/g and Apple HIG motion guidance support short UI transitions; prefers-reduced-motion is Baseline widely available since January 2020 and MDN advises replacing large movement with gentler effects such as fades rather than removing the information.
- Satisfies: craft-motion-duration-range, craft-motion-frequent-quick, craft-motion-easing-direction, craft-reduced-motion-replace, a11y-reduced-motion, distinct-motion-authored
```css
:root { --ease-out: cubic-bezier(0.2, 0.8, 0.2, 1); }
button { transition: transform 100ms var(--ease-out), background-color 150ms var(--ease-out); }
button:active { transform: scale(0.97); }
@media (prefers-reduced-motion: reduce) { button { transition: background-color 150ms linear; } button:active { transform: none; } }
```
### Animated toggles from ARIA state (`ix-toggle`) [craft-consensus · verified]
Build animated toggles from a native button with aria-pressed (or a checkbox, or role="switch" with aria-checked) and a fixed name such as "Dark mode". Drive the visual state from the ARIA attribute in CSS so look and state cannot diverge, show state with more than colour (a check, a knob position or text), and keep Space and Enter working.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): the button's accessible name was "Dark mode" before and after, with [pressed] added by aria-pressed="true" after Space and removed after Enter; the checkmark animated through a stroke-dashoffset transition selected by button[aria-pressed=true]; axe-core found no violations. Do not change the label as well as aria-pressed (APG button pattern).
- Satisfies: comp-switch-label-stable, comp-toggle-visual-state-not-color, a11y-name-role-value
```css
button[aria-pressed="true"] { background: #14171A; color: #fff; }
button[aria-pressed="true"] .check { stroke-dashoffset: 0; }   /* visible check, not only colour */
```
### Immediate feedback with status region (`ix-feedback`) [craft-consensus · verified]
After every action show immediate visible feedback and mirror any toast in persistent page state. Put an empty role="status" region in the page at load and write the message into it, update an on-page count or list (the cart total, the saved list), and let a toast be a convenience, not the only record. Do not use a toast for information needed to finish a task.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): clicking "Add to cart" updated the visible count (0 to 1, then 4 after three rapid clicks) and filled the status region with "Added to cart. 1 items in cart." (fix the plural in real copy). The live region existed before the message, which is what lets assistive technology announce it without moving focus (WCAG 4.1.3). Keep at most one signature motion moment and let other animations answer an action.
- Satisfies: comp-notification-recoverable, a11y-coga-action-feedback, a11y-status-messages, comp-live-region-exists-before-content, distinct-motion-authored
```html
<p>Cart: <span id="count">0</span> items</p>
<div id="live" role="status"></div>   <!-- present at load, empty -->
```
### Cross-document view transitions (`ix-vt-mpa`) [craft-consensus · verified]
For multi-page sites, opt in to cross-document view transitions in CSS on both pages, inside a prefers-reduced-motion: no-preference block, and keep the animation short (about 250ms). Treat it as progressive enhancement: Firefox does not run it and the pages must work without it. Both pages must be same-origin.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome") (Chrome 156): with @media (prefers-reduced-motion: no-preference) { @view-transition { navigation: auto } } on two local pages, a link click produced a ViewTransition on the destination (pagereveal event had viewTransition set); with reducedMotion: "reduce" emulated it did not. After the navigation focus was on the body, as with any normal navigation, and each page keeps its own title. Chrome documents cross-document view transitions from Chrome and Edge 126 and Safari 18.2, not Firefox, requires same-origin navigations and both pages to opt in, and skips the transition if the navigation takes over four seconds. MDN lists @view-transition as Limited availability (not Baseline), so feature-detect or accept non-support.
- Satisfies: craft-motion-duration-range, a11y-reduced-motion, a11y-coga-no-surprise-changes, a11y-page-title
```css
@media (prefers-reduced-motion: no-preference) {
  @view-transition { navigation: auto; }
  ::view-transition-old(root), ::view-transition-new(root) { animation-duration: 250ms; }
}
```
### Guarded single-page view transitions (`ix-vt-spa`) [craft-consensus · partly-verified]
For a single-page route change, wrap the DOM swap in document.startViewTransition only when the user allows motion and the API exists. After the swap, update document.title, move focus to the new page heading (an h1 with tabindex="-1"), push history, and write a short message into a pre-existing role="status" region. Keep the transition at 300ms or less: input is blocked while it runs.
- How: Measured 2026-11-06 in Chrome 156 via Playwright (channel "chrome"): in an SPA test, after the swap document.activeElement was BODY (the clicked link had been removed), and calling h1.focus() on a tabindex="-1" heading put focus on it; title read "About"; the status region held "Navigated to About"; with reducedMotion: "reduce" no transition was started and the same focus handling still worked. With a deliberately long 1500ms transition, a click on another button 300 ms after the start was held back about 1.4 s until the transition ended (Playwright waited for actionability), and a raw mouse click during it did nothing, so long transitions make the page unresponsive. MDN notes that keeping old and new content around can cause loss of reading position, focus confusion and odd live-region behaviour, and lists stopping accidental interaction with old content among the problems hand-written transitions must solve.
- Satisfies: a11y-focus-order, a11y-page-title, a11y-status-messages, a11y-coga-no-surprise-changes, craft-motion-frequent-quick, a11y-reduced-motion
- Verification note: Focus, title, status text and the input-blocking behavior were measured in Chrome 156; MDN supports the focus and live-region risks. Moving focus to the h1 is common practice rather than a rule from a source we read, and we did not test with a screen reader, Safari or Firefox.
```js
async function go(render) {
  const reduce = matchMedia("(prefers-reduced-motion: reduce)").matches;
  const vt = !reduce && document.startViewTransition ? document.startViewTransition(render) : (render(), null);
  if (vt) await vt.updateCallbackDone;
  document.title = "About";
  document.querySelector("h1").focus();               // h1 has tabindex="-1"
  document.getElementById("live").textContent = "Navigated to About";
}
```

# Recipe: Brutalist, neo-brutalist and edgy styles that stay usable (`brutalist-hard-edge`)
Styles covered: brutalism, neo-brutalist, edgy
**Keep:** Black outlines, hard offset shadows, flat saturated fills, default-looking underlined links, raw tables and tabs, heavy grotesque or monospace type, a blunt voice.
**Avoid:** Headings, paragraphs and buttons in all capitals; stretched or squashed images; tabs, accordions and tables built from bare divs; a thick coloured stripe on one side of a rounded card; error messages that mock the user; shadows or fills as the only sign of a boundary or a state.
Keep the thick outlines, hard offset shadows, flat saturated blocks, raw tables and a sharp voice. Make the roughness come from borders, type weight and layout, not from shouting capitals, stretched images, bare div widgets or a shadow that is the only boundary.
**While designing:** Use ink on flat fills with verified contrast, 3px solid borders and hard shadows with zero blur, sentence-case headings and uppercase only for short letterspaced labels, object-fit cover for every image, real tab, accordion and table markup, a blue focus ring, and neutral literal error text.
## Verified palette: Brutalist and edgy, computed
- paper: #FFFFFF
- ink: #111111
- fill-yellow: #FFD600
- fill-pink: #FF90E8
- fill-blue: #A3C4FF
- fill-green: #B8F2A0
- link: #1D2BFF
- focus: #1D2BFF
- error: #C00000
- text-muted: #6B6B6B
- edgy-background: #0A0A0A
- edgy-accent: #C6FF00
- edgy-error: #FF3B30
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on paper | #111111 | #FFFFFF | 18.88:1 | 4.5:1 |
| muted text on paper | #6B6B6B | #FFFFFF | 5.33:1 | 4.5:1 |
| ink on yellow button | #111111 | #FFD600 | 13.37:1 | 4.5:1 |
| ink on pink card | #111111 | #FF90E8 | 9.36:1 | 4.5:1 |
| ink on blue chip | #111111 | #A3C4FF | 10.7:1 | 4.5:1 |
| ink on green chip | #111111 | #B8F2A0 | 14.61:1 | 4.5:1 |
| underlined link on paper | #1D2BFF | #FFFFFF | 7.39:1 | 4.5:1 |
| link on yellow card | #1D2BFF | #FFD600 | 5.23:1 | 4.5:1 |
| 3px ink border against paper (UI boundary) | #111111 | #FFFFFF | 18.88:1 | 3:1 |
| focus ring on paper | #1D2BFF | #FFFFFF | 7.39:1 | 3:1 |
| focus ring on yellow | #1D2BFF | #FFD600 | 5.23:1 | 3:1 |
| error text on paper | #C00000 | #FFFFFF | 6.48:1 | 4.5:1 |
| edgy: white text on near-black | #FFFFFF | #0A0A0A | 19.8:1 | 4.5:1 |
| edgy: acid accent on near-black | #C6FF00 | #0A0A0A | 16.69:1 | 3:1 |
| edgy: near-black text on acid button | #0A0A0A | #C6FF00 | 16.69:1 | 4.5:1 |
| edgy: error red on near-black | #FF3B30 | #0A0A0A | 5.58:1 | 4.5:1 |
## Steps
### Flat fills with near-black ink (`bk-palette`) [standard · verified]
Set flat saturated fills with near-black ink on top and check every pair. Ink #111111 on paper is 18.88:1, on yellow #FFD600 13.37:1, pink #FF90E8 9.36:1, blue #A3C4FF 10.7:1, green #B8F2A0 14.61:1. Links #1D2BFF are 7.39:1 on paper and 5.23:1 on yellow. Never put white text on these fills.
- How: Choose the fill for its saturation, then set the text to ink or paper, whichever passes, and recompute. The 3px ink border is 18.88:1 against paper, far above the 3:1 UI minimum, which is why thick outlines solve the boundary problem that thin grey outlines create. Edgy dark variant: white on #0A0A0A is 19.8:1, acid #C6FF00 is 16.69:1 (use as large text, icons or a button fill with #0A0A0A text at 16.69:1), and error red #FF3B30 is 5.58:1 for text. Harsh contrast is the look here, so none of it needs lowering. Rendered and measured in a Chrome demo: the computed colours match the claimed pairs.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Shout with weight, not uppercase (`bk-caps`) [craft-consensus · verified]
Get the shouting look from weight, size and tight tracking on sentence-case text, and keep uppercase for labels of three words or fewer. Never uppercase a heading of more than three words, a paragraph or a button label. Every uppercase label gets letter-spacing of 0.05em to 0.12em. Do not put a tracked uppercase label directly above the hero heading (distinct-eyebrow-restraint): place it after the heading or leave it out. Step the h1 in rem (2.5rem, 3.5rem from min-width: 40rem, 5rem from 64rem) instead of clamp() with vw, and put overflow-wrap: anywhere on headings, paragraphs, chips and buttons: heavy words overflowed the page by 67 px at 320 px with 200% text and text spacing until we did.
- How: Practical Typography: caps work for text shorter than a line and need letter-spacing of about 5 to 12 percent; GOV.UK content guidance: no block capitals for large amounts of text. The 40-character cut-off in the rule is our own review threshold. In the Chrome demo the label measures 0.08em and no heading or button is uppercase. Large lowercase headlines at weight 900 with -0.02em tracking already read as blunt.
- Satisfies: copy-no-all-caps-text, craft-caps-short-only, craft-caps-letterspacing
```css
h1, h2, h3, .btn { text-transform: none; font-weight: 900; }
h1 { letter-spacing: -0.02em; }
.label { text-transform: uppercase; letter-spacing: 0.08em; font: 700 1rem/1 ui-monospace, monospace; }
```
### Raw photos without stretching (`bk-images`) [craft-consensus · verified]
Make photos look raw with filters, hard crops, borders and a slight rotation, never with a stretched aspect ratio. Fit every image with object-fit: cover and an object-position that keeps the subject in view.
- How: MDN: the default object-fit: fill distorts; cover crops and contain letterboxes. A grayscale(1) contrast(1.3) filter, a 3px border and rotate(-2deg) give the harsh look without changing the ratio. Measured in Chrome: a 400x300 source in a 300x300 box with object-fit: cover keeps its proportions (cropped), while the same image with the default fill is the distorting case. Check small screens for the subject with object-position. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; a fixed width: 300px photo overflowed a 272 px content box at 320 px (right edge 329 px); width: min(300px, 100%) with aspect-ratio fixes it.
- Satisfies: craft-image-no-distortion
```css
.photo { width: min(300px, 100%); height: auto; aspect-ratio: 1; object-fit: cover; object-position: 50% 30%;
  border: 3px solid #111; filter: grayscale(1) contrast(1.3); transform: rotate(-2deg); }
```
### Hard shadow snap on press (`bk-press-motion`) [craft-consensus · partly-verified]
Use the snap of the hard shadow as the interaction: on hover or press the button moves toward its shadow in about 100 ms with a decelerating curve, and returns with an accelerating one. Do not use linear easing on the transform.
- How: NN/g: about 100 ms for feedback, ease-out for things appearing, ease-in for leaving, exits shorter than entrances. Material motion tokens: decelerate for enter, accelerate for exit. Measured in Chrome: transition-duration 0.1s and cubic-bezier(0, 0, 0.2, 1) on transform. Mapping the pressed state to "entering" and release to "leaving" is our interpretation. The 3 to 6 px translation is small, but wrap larger movement in prefers-reduced-motion.
- Satisfies: craft-motion-easing-direction
- Verification note: Duration and easing guidance are from the sources read; treating press as an entrance and release as an exit is our reading of the rule.
```css
.btn { transition: transform 100ms cubic-bezier(0, 0, 0.2, 1), box-shadow 100ms cubic-bezier(0, 0, 0.2, 1); }
.btn:hover  { transform: translate(-3px, -3px); box-shadow: 6px 6px 0 #111; }
.btn:active { transform: translate(3px, 3px);  box-shadow: 0 0 0 #111; }
```
### Underlined links, bordered buttons (`bk-controls`) [craft-consensus · verified]
Keep the raw default look of links and make it explicit: underline every inline link, give every button a fill and a 3px border, and keep targets at least 44 px tall (WCAG minimum is 24 by 24).
- How: An underlined link in a different colour passes the "not colour alone" test; Chrome demo measures underline on inline links and 44 px tall buttons and tabs. Do a grayscale screenshot: every link and button should still be findable.
- Satisfies: a11y-coga-controls-recognizable, a11y-target-size, a11y-color-not-only
### Hard shadow only on pressables (`bk-shadow-affordance`) [our-take · judgement]
Reserve the hard offset shadow for things you can press. Static cards, chips and stickers get the flat 3px border and a fill, with no shadow.
- How: In this style the shadow is what reads as raised and pressable. If a decorative card carries the same shadow as a button, a visitor cannot tell the two apart. Check the grayscale screenshot for anything non-interactive that looks like a control.
- Satisfies: a11y-coga-controls-recognizable
- Verification note: Our recommendation; COGA asks that non-interactive items do not look clickable, the shadow-as-affordance reading is ours.
### Outline focus, borders for forced colors (`bk-focus-forced`) [craft-consensus · verified]
Draw focus with an outline in a colour that contrasts with both paper and fills, not with the hard shadow, and keep the 3px borders so boundaries survive forced colours. Add a prefers-contrast: more token that thickens borders and darkens muted text.
- How: MDN: in forced-colors mode border-color and outline-color are kept as system colours while box-shadow becomes none, and :focus-visible indicators need 3:1. Focus ring #1D2BFF is 7.39:1 on paper and 5.23:1 on yellow. Measured in Chrome 156 with forced colours emulated: the button shadow computes to none and the 3px solid borders remain; with contrast: more emulated the border token becomes 5px and muted text turns to ink. Keyboard focus measured as a 4px solid #1D2BFF ring with 3px offset.
- Satisfies: a11y-focus-visible, craft-contrast-preferences, a11y-non-text-contrast
```css
:focus-visible { outline: 4px solid var(--focus); outline-offset: 3px; }
@media (prefers-contrast: more) { :root { --border: 5px; --muted: #111; } }
```
### Radius and elevation per role (`bk-tokens`) [craft-consensus · partly-verified]
Define radius and elevation per role: cards and inputs 0, buttons 8 px, tags pill, images 0; shadows sm (3px 3px 0) and md (6px 6px 0) with zero blur. Mark emphasis with a fill or a full border, not a thick coloured stripe on one side of a rounded card.
- How: The rule fails a page where every role shares one radius of 16 px or more, where three or more adjacent cards pair a hairline border with a blur of 32 px or more, or where a rounded element has one thick coloured side. Hard shadows have zero blur, so they pass by construction. If you want a left bar on a callout, use radius 0 on that element. Chrome demo: the roles compute to different radii, no element has a single thick side border with a radius of 4 px or more.
- Satisfies: distinct-radius-elevation-scale, distinct-no-side-stripe-border
- Verification note: Thresholds come from practitioner detectors and articles (one is rated low weight in sources.json); we measured the demo against the rule text, not against a standard.
### Raw look, real semantics (`bk-semantics`) [standard · verified]
Raw does not mean unstructured. Style the real patterns: a tablist with role=tab buttons, aria-selected on exactly one, aria-controls and a labelled tabpanel; accordion headers as h3 containing one button with aria-expanded; tables with a caption and th scope. Wrap a wide table in a focusable scroll region: div role=region, aria-label, tabindex=0, overflow-x: auto. Controls that only work with script (tab buttons, accordion buttons) must not exist without it: leave every panel visible in the HTML, keep the tablist hidden (with [hidden] { display: none !important } so no author display rule overrides it) or build the accordion button from the plain heading in the script, and make call-to-action buttons real links or form submits.
- How: Follow the ARIA Authoring Practices tabs and accordion patterns and Inclusive Components for tables and collapsible sections. Chrome demo checks: every tab sits in a named tablist, one aria-selected=true, each panel points back with aria-labelledby, ArrowRight moves selection and focus, tabindex=-1 on inactive tabs; the accordion button is the only child of its heading, aria-expanded flips on click and the collapsed panel is display:none so its links are not focusable; the table has a caption, th scope=col and scope=row. Native details/summary is a reasonable alternative but the rule check expects a button inside a heading. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; at 200% root text and 320 px a three-column table overflowed by 133 px (219 px with text spacing applied); the scroll wrapper removed the page-level overflow and axe accepted the focusable region.
- Satisfies: comp-tabs-semantics, comp-accordion-markup, comp-data-table-semantics
```html
<h3><button type="button" aria-expanded="false" aria-controls="a1" id="ab1">Can I export my data?</button></h3>
<div id="a1" role="region" aria-labelledby="ab1" hidden>...</div>
```
### Attitude in marketing, literal elsewhere (`bk-voice`) [craft-consensus · verified]
Let attitude live in marketing lines and keep a plain statement of the offer on the first screen. Errors, checkout, security and deletion text stays neutral and literal: say what the system needs, no jokes, no apology, none of invalid, incorrect, please, sorry, oops. Chips that are not a live status must not read New, Live or Beta, and warning or error icons are inline SVG, not emoji.
- How: Mailchimp: voice stays constant while tone shifts with the reader's state; NN/g and GOV.UK: errors are specific, non-blaming, without humour. Pattern for an empty field is "Enter your email address", for a wrong value "Card number must be 16 digits". A blunt headline ("Send invoices that get paid") sits next to a plain offer line. Chrome demo greps its error strings for the banned list and exclamation marks: none found.
- Satisfies: copy-no-idioms-puns, copy-error-no-blame-words, copy-tone-fits-context, a11y-coga-plain-literal-language

# Recipe: Playful, quirky and friendly voices that stay clear (`playful-quirky-voice`)
Styles covered: playful, quirky, friendly
**Keep:** A distinct voice, a mascot or recurring character, bright warm colours, bouncy motion, conversational marketing copy.
**Avoid:** Idioms, puns and metaphors as headlines, nav labels or buttons; humour or blame in errors; "please", "simply", "just", "easy" and exclamation points in instructions; white text on bright fills; endless looping motion.
Keep the personality, the jokes, the mascot and the warm colours. Put the wit in kickers and supporting lines, keep headings, buttons, errors and money screens literal, and let motion respect reduced-motion settings.
**While designing:** Write the plain headline first and add the quirk as a kicker or supporting line, name every section by what it says, write errors as "Enter..." or "X must be...", and keep payments, security and deletion neutral.
## Verified palette: Friendly and playful, computed
- background: #FFFFFF
- text: #1B1B1F
- text-muted: #4B4B55
- fill-sun: #FFD23F
- button-coral: #FF6B3D
- link: #1D4ED8
- error: #B42318
- error-tint: #FFF1EC
- success: #0B5D3A
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on paper | #1B1B1F | #FFFFFF | 17.17:1 | 4.5:1 |
| muted text on paper | #4B4B55 | #FFFFFF | 8.62:1 | 4.5:1 |
| ink on sun-yellow fill | #1B1B1F | #FFD23F | 11.89:1 | 4.5:1 |
| ink on coral button | #1B1B1F | #FF6B3D | 6.07:1 | 4.5:1 |
| link on paper | #1D4ED8 | #FFFFFF | 6.7:1 | 4.5:1 |
| error text on paper | #B42318 | #FFFFFF | 6.57:1 | 4.5:1 |
| error text on error tint | #B42318 | #FFF1EC | 5.96:1 | 4.5:1 |
| success text on paper | #0B5D3A | #FFFFFF | 7.95:1 | 4.5:1 |
| error field border on paper (UI) | #B42318 | #FFFFFF | 6.57:1 | 3:1 |
## Steps
### Warm fills with ink text (`pq-palette`) [standard · verified]
Use bright warm colours as fills and put ink on them. Coral #FF6B3D with white text is 2.83:1 and fails; ink #1B1B1F on the same coral is 6.07:1. Sun yellow #FFD23F with ink is 11.89:1. Keep the error red #B42318 (6.57:1 on white, 5.96:1 on its tint) and success green #0B5D3A (7.95:1) for those states only.
- How: Link #1D4ED8 is 6.7:1 on white; muted text #4B4B55 is 8.62:1. Field borders carry meaning, so give them a 3:1 colour (the error border is 6.57:1). Rendered in Chrome: computed colours match each claimed pair.
- Satisfies: a11y-contrast-text, a11y-non-text-contrast
### Plain offer as the headline (`pq-plain-headline`) [craft-consensus · verified]
Write the plain statement of the offer as the headline, nav label or button, and put the pun, joke or character in a kicker or the supporting line. "Plan a trip with friends" is the h1; "Meet Pip" and "Pip keeps the spreadsheets away" carry the personality.
- How: NN/g: headlines work out of context and avoid cute or idiomatic language; Google style guide: avoid slang and figurative language; W3C COGA: avoid metaphors and idioms in navigation and calls to action. Test: read each headline, nav label and button aloud to someone who does not know the product; if a literal reading misleads, rewrite it. Buttons start with a verb in sentence case ("Create a free account").
- Satisfies: copy-no-idioms-puns, a11y-coga-plain-literal-language
### Name sections by what they say (`pq-headings`) [craft-consensus · verified]
Name every section by what it says ("Split costs without the maths"), so the heading list read alone summarises the page. Never use "Features", "Overview", "Why choose us" or "Our approach", and do not prefix feature cards with emoji.
- How: GOV.UK content guidance and NN/g: headings that describe the content beneath them. The Chrome demo extracts its heading outline and matches it against the rule blocklist (introduction, overview, features, benefits, our approach, why us, about, welcome): none match, and the outline reads as a summary. Order sections by the questions this buyer asks, not by the stock hero, logos, three cards, pricing sequence.
- Satisfies: copy-heading-informative, copy-section-content-drives-structure
### Specific, neutral error messages (`pq-errors`) [craft-consensus · verified]
Write errors as specific, neutral instructions: "Enter your email address" for an empty field, "Postcode must be in the format AB1 2CD" for a wrong value. Show them with an icon, text and a changed border, linked to the field with aria-describedby, in an error colour that passes (6.57:1 on white).
- How: GOV.UK error-message guidance: say what happened and how to fix it; avoid "valid/invalid", "please", "sorry", "oops", "forbidden", "you forgot" and "This field is required". NN/g: nonblaming positive tone, no humour in errors except a rare total failure. WCAG 1.4.1 and failure F81: errors must not be identified by colour only. Chrome demo: both invalid inputs have a label, a described-by message of real text, an icon and a changed border; the error strings contain none of the banned words or exclamation marks.
- Satisfies: copy-error-specific-actionable, copy-error-no-blame-words, a11y-error-identification, a11y-color-not-only
```html
<label for="em">Email address</label>
<input id="em" type="email" autocomplete="email" aria-invalid="true" aria-describedby="em-err">
<p id="em-err"><span aria-hidden="true">&#9888;</span> Enter your email address</p>
```
### Plain imperative instructions (`pq-instructions`) [craft-consensus · verified]
Give instructions as plain imperatives: "Enter the email address you use for bookings." Drop "please", "please note", "simply", "just", "easy", "quickly", "it's that simple" and exclamation points from interface text. Marketing headlines may keep their energy.
- How: GOV.UK tone guidance and Google developer style guide list these softeners as words to avoid. The check is a grep over UI strings, hints, instructions and help text, excluding marketing headlines and testimonials; the Chrome demo ran that grep over its UI zone and found none.
- Satisfies: copy-no-please-filler
### Dial personality down as stakes rise (`pq-tone-dial`) [craft-consensus · verified]
Turn personality down as the stakes go up: full voice in marketing sections, light touches in onboarding, neutral wording on forms and errors, and literal text on payment, security, cancellation, deletion and legal surfaces, with no joke, slang, hype word or exclamation point.
- How: Mailchimp: voice stays constant, tone shifts with the reader's state; NN/g: humour only for rare total failures. Write the surface list once ("marketing, onboarding, forms, errors, checkout, security, deletion, legal") with a tone for each, and sample the copy of the risky surfaces. The demo's payment copy ("Your card is charged when the trip is booked...") is deliberately literal.
- Satisfies: copy-tone-fits-context
### Write a voice sheet first (`pq-voice-sheet`) [craft-consensus · partly-verified]
Write a voice sheet before the copy: three or four trait words, each with a do and a don't example, plus the fixed choices (you or we, contractions, US or UK spelling). Allow one quirky element per surface so the oddness stays a signature.
- How: Mailchimp and Microsoft publish voice guidance as traits with examples. Sample six surfaces (hero, navigation, buttons, errors, footer, 404) against the sheet and fail mixed spelling or person. The "one quirk per surface" budget is our own heuristic.
- Satisfies: copy-voice-consistent
- Verification note: Voice-sheet practice is in the sources read; the one-quirk-per-surface budget is our heuristic.
```text
Voice: warm, specific, a little odd.
Warm      do "Pip sorted the costs"          don't "Users must remit payment"
Specific  do "3 of 5 friends have paid"      don't "Great progress!"
Odd       do one mascot line per page         don't puns in nav labels
Fixed: address the reader as "you", use contractions, UK spelling.
```
### Limit three quirky copy patterns (`pq-rhetoric`) [our-take · judgement]
Watch for the three patterns quirky copy slides into: "not X, it's Y", three parallel slogans ("Save time. Work smarter. Scale faster."), and self-answered questions ("The result?"). Use each at most once per page and say the claim directly otherwise.
- How: The rule is advisory and our own take, drawn from lists of AI-writing tells. A regex pass over the page text counts the hits: fail above one of each kind. A list of two or four items, when the items really are distinct, avoids the tricolon.
- Satisfies: copy-no-stock-rhetoric
- Verification note: Advisory rule labelled our-take; the sources are lists of AI-writing tells, not studies of reader outcomes.
### Finite, optional bouncy motion (`pq-motion`) [standard · verified]
Keep bouncy motion finite and optional: a mascot hop that runs three times (3.6 s) and then stops, a prefers-reduced-motion block that removes it, and nothing flashing. Any loop longer than five seconds next to other content needs a visible pause control.
- How: MDN: replace large-scale motion with gentler effects under prefers-reduced-motion: reduce. WCAG 2.2.2: moving or blinking content that starts automatically, lasts more than five seconds and sits beside other content needs pause, stop or hide. Measured in Chrome: the hop is one animation of 1.2 s x 3 iterations; with reduced motion emulated it computes to animation-name none and no running animation.
- Satisfies: a11y-reduced-motion, a11y-pause-stop-hide, a11y-flashes
```css
.mascot { animation: hop 1.2s cubic-bezier(0, 0, 0.2, 1) 3; }
@media (prefers-reduced-motion: reduce) { .mascot { animation: none; } }
```
### Wrap the h1, SVG icons (`pq-reflow-200-icons`) [standard · verified]
Give the h1 overflow-wrap: anywhere (a 3rem h1 overflowed by 35 px at 320 px with 200% text) and draw warning and error icons as inline SVG with currentColor and aria-hidden, never as emoji (distinct-real-imagery-and-icons).
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; 35 px of overflow and two emoji-as-icon minors were both gone after the change.
- Satisfies: a11y-reflow, distinct-real-imagery-and-icons

# Recipe: Maximalist, Memphis and collage layouts with order underneath (`maximalist-memphis-collage`)
Styles covered: maximalist, memphis-playful, collage
**Keep:** Many bright colours, geometric confetti, rotated cut-outs and stickers, layered shapes, big display type, dense compositions.
**Avoid:** Text directly on patterns or confetti; a link or error colour reused as decoration; more than two typefaces or ad hoc sizes and gaps; stretched cut-outs; dozens of equal-weight choices; cards that are a link wrapper around everything; modals built without dialog semantics; drifting shapes that never stop.
Keep the density, the confetti shapes, the clashing colours and the overlapping cut-outs. Put the noise in a decorative layer, keep text on solid plates, and hold a few quiet constants (two typefaces, a size scale, a spacing scale, a line length, one icon family) so the page reads as one loud system.
**While designing:** Choose a decorative palette separate from the link and error colours, put every line of text on a solid plate, fix two fonts, six to eight sizes and a 4 or 8 px spacing scale, cap text at 55ch inside a container of 1280px or less, and make the decorative layer aria-hidden, pausable and removed under reduced motion.
## Verified palette: Memphis maximalist, computed
- background: #FFFFFF
- band-lilac: #F4EEFF
- ink: #1A1033
- decor-yellow: #FFD23F
- decor-pink: #FF8FB8
- decor-teal: #7DE0D6
- decor-periwinkle: #B8A4FF
- decor-coral: #FF6B6B
- link: #2F27CE
- error: #B3261E
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on white | #1A1033 | #FFFFFF | 18.01:1 | 4.5:1 |
| ink text on lilac band | #1A1033 | #F4EEFF | 15.89:1 | 4.5:1 |
| ink on yellow plate | #1A1033 | #FFD23F | 12.47:1 | 4.5:1 |
| ink on pink plate | #1A1033 | #FF8FB8 | 8.47:1 | 4.5:1 |
| ink on teal plate | #1A1033 | #7DE0D6 | 11.58:1 | 4.5:1 |
| ink on periwinkle plate | #1A1033 | #B8A4FF | 8.4:1 | 4.5:1 |
| ink on coral chip (decor, small text) | #1A1033 | #FF6B6B | 6.49:1 | 4.5:1 |
| link text on white | #2F27CE | #FFFFFF | 9.12:1 | 4.5:1 |
| link text on lilac | #2F27CE | #F4EEFF | 8.04:1 | 4.5:1 |
| white on link-blue primary button | #FFFFFF | #2F27CE | 9.12:1 | 4.5:1 |
| error text on white | #B3261E | #FFFFFF | 6.54:1 | 4.5:1 |
## Steps
### Text on flat plates (`mx-plates`) [standard · verified]
Put the noise around the text, not under it. Every line of text sits on a flat plate or a plain band, and the shapes, stickers and patterns live in a decorative layer. Ink #1A1033 is 12.47:1 on yellow #FFD23F, 8.47:1 on pink #FF8FB8, 11.58:1 on teal #7DE0D6, 8.4:1 on periwinkle #B8A4FF, 6.49:1 on coral #FF6B6B, 18.01:1 on white.
- How: Never set text in a pastel on a pastel. Link blue #2F27CE is 9.12:1 on white and 8.04:1 on the lilac band. The decorative layer is a sibling element with position:absolute, z-index 0, pointer-events:none and aria-hidden="true". Rendered in Chrome: the computed colours of the demo's plates, bands, links and buttons match the claimed pairs.
- Satisfies: a11y-contrast-text
### Fix quiet constants first (`mx-tokens`) [craft-consensus · partly-verified]
Fix the quiet constants before adding colour: two font families (a display face and a body face), six to eight named type sizes, and a spacing scale on a 4 px base (4, 8, 12, 16, 24, 32, 48, 64, 96). Loudness comes from colour, shape and rotation, not from a new size or gap every time.
- How: Define the scales as custom properties and use only those. Measured in the Chrome demo: 5 distinct font sizes (14, 16, 20, 40, 64 px), 2 families, 7 distinct spacing values, every one a multiple of 4. The rule caps are 8 sizes, 2 families (advisory, our-take) and 12 spacing values.
- Satisfies: craft-type-scale-tokens, craft-font-families-few, craft-spacing-scale-tokens
- Verification note: Measured on a demo built to the scales; the two-family limit is an advisory our-take rule and the 8-size and 12-value caps are the rules' own thresholds, not studies.
```css
:root {
  --s1: 4px; --s2: 8px; --s3: 12px; --s4: 16px; --s5: 24px; --s6: 32px; --s7: 48px; --s8: 64px; --s9: 96px;
  --fs-xs: 1rem; --fs-sm: 1rem; --fs-md: 1.25rem; --fs-lg: 1.75rem; --fs-xl: 2.5rem; --fs-2xl: 4rem;
  --font-display: "Arial Black", Impact, sans-serif; --font-body: system-ui, sans-serif;
}
```
### Separate semantic and decorative palettes (`mx-colour-roles`) [craft-consensus · verified]
Keep two palettes apart. The semantic set (link, primary button, focus, error, success) is used only for those jobs; the decorative set (yellow, pink, teal, periwinkle, coral here) carries the Memphis energy. Link blue and error red never appear as a shape, border or text colour on non-interactive content.
- How: GOV.UK Design System: colours are assigned by function, and the focus colour is reserved. In the Chrome demo every element was scanned: link blue (#2F27CE) and error red (#B3261E) occur only on links, buttons and the error message; the five decorative colours appear on plates and shapes. Pick decorative hues that are visibly different from the link hue.
- Satisfies: craft-color-meaning-reserved
### 50ch text in a 1280 px container (`mx-measure-container`) [craft-consensus · verified]
Cap running text with max-inline-size around 50ch (not 55ch) and put the content in a centred container of 1280 px or less; let only the coloured band and decorative layer run edge to edge. Then count characters per line in the browser instead of trusting the number.
- How: Measured in Chrome 156 on macOS by counting characters on every rendered line: with max-inline-size 66ch, proportional faces gave 87 to 96 characters per line at most (system-ui and Georgia 96, Arial and Helvetica Neue 87), over the 75-character cap; 60ch gave 77 to 89, 55ch gave 69 to 83, 45ch gave 59 to 67, and 50ch gave a longest line of 67 to 74 (average 60 to 69). The reason is that 1ch is the width of the digit 0, wider than an average letter; only a monospace face gets about one character per ch. So 50ch is the safe value for system-ui, Arial, Georgia, Helvetica Neue and Arial Narrow; other platforms' fonts were not measured. In the demo the longest line is 70 characters at 768, 1280 and 1920 px and the container is 1280 px at a 1920 px viewport while the band is 1920 px wide.
- Satisfies: craft-measure-body, craft-container-max-width
```css
.prose { max-inline-size: 50ch; }          /* about 60-70 characters in proportional faces; verify */
.wrap  { max-inline-size: 1280px; margin-inline: auto; }  /* the band behind it is full-bleed */
```
### Tight inside groups, loose between (`mx-grouping`) [our-take · judgement]
Dense is not the same as unstructured. Keep the gap inside a group (heading to its content, 16 px) clearly smaller than the gap between groups (48 px), including across overlapping or rotated pieces.
- How: Proximity tells the eye what belongs together when colour and shape are all loud. Check each heading: margin above greater than margin below, and the internal gap of a card smaller than the gap to its neighbour. The demo measures 16 px inside groups against 48 px between them.
- Satisfies: craft-group-by-proximity
- Verification note: The rule is labelled our-take; Apple and Butterick support heading proximity but not the exact gaps.
### Dense page, about five choices (`mx-choices`) [craft-consensus · verified]
Let the page be visually dense while each viewport-height section offers one dominant action and at most about five choices in total. Move the rest to a footer or a titled "more" link.
- How: The COGA guidance and NN/g homepage principles favour one clearly dominant feature. The demo hero has five controls: one filled primary button, three secondary and one text link, counted in Chrome.
- Satisfies: a11y-coga-limit-choices-per-screen
### One icon family on one grid (`mx-icons`) [craft-consensus · verified]
Use one icon family at one stroke weight, corner style and fill treatment on a shared grid (24 px, stroke 2, round caps and joins, stroke currentColor). Stickers, confetti and illustrations are decoration, not icons, and may be as wild as you like. Status and warning icons are inline SVG from the same family, never emoji (distinct-real-imagery-and-icons).
- How: Apple HIG: same size, detail and stroke weight across a set, with stroke matched to adjacent text. web.dev: inline SVG so CSS can style it. Chrome demo: all three icons share stroke-width 2, round linecap and linejoin, no fill and a 24x24 viewBox.
- Satisfies: craft-icons-one-family
### Cards as list items with stretched link (`mx-cards`) [our-take · verified]
Make each card a list item with one heading level and one link inside the heading; stretch the click area with a ::after pseudo-element. Draw the focus indication on the link itself (a background and a thicker underline), and keep a ring on the card with :has(a:focus-visible) as a bonus. Decorative card images get alt="".
- How: Inclusive Components cards pattern. Tested in Chrome: each li has one link inside h3, clicking the lower part of the rotated card follows the link, and keyboard focus on the link draws a solid 3px outline on the card. A rotated card's bounding box is larger than the card, so click inside the shape when testing. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; a version that removed the link's outline and drew the ring only on the card through :has() failed a11y-focus-visible on 3 of 9 Tab stops, because the probe (and a person using forced colours) looks at the focused element itself; adding a background and underline change on the link itself fixed it.
- Satisfies: comp-card-single-primary-link
- Verification note: Behaviour tested in Chrome 156; the Inclusive Components page entry in sources.json has no notes, so the pattern details beyond the rule text are from our own testing.
```css
.card { position: relative; }
.card a::after { content: ""; position: absolute; inset: 0; }
.card:has(a:focus-visible) { outline: 3px solid var(--ink); outline-offset: 3px; }
.card a:focus-visible { outline: none; background: var(--yellow); text-decoration-thickness: 3px; }
```
### Native dialog with showModal (`mx-dialog`) [standard · verified]
Build modals with a native dialog opened by showModal(), named by aria-labelledby pointing at its visible title, with every control inside it. Style the dialog and ::backdrop as loudly as you like.
- How: ARIA Authoring Practices modal dialog: focus moves in, Tab stays inside, Escape closes, focus returns. Measured in Chrome 156: after showModal() the dialog matches :modal, focus is inside, the accessibility tree exposes a dialog named "Delivery details", six Tab presses stay inside, an outside button cannot take focus, and Escape returns focus to the opener. The demo also sets aria-modal="true" because the rule check looks for it; with showModal() the page behind is genuinely blocked, so the attribute is truthful.
- Satisfies: comp-dialog-semantics
```html
<dialog id="dlg" aria-labelledby="dlg-title" aria-modal="true">
  <h2 id="dlg-title">Delivery details</h2>
  <p>...</p>
  <button type="button" id="close">Close delivery details</button>
</dialog>
```
### Rotate and crop without stretching (`mx-images`) [craft-consensus · verified]
Rotate, overlap and crop cut-outs freely, but with transforms that only rotate or translate, and fit each image with object-fit: contain for cut-outs or cover for cropped photos, never fill.
- How: MDN object-fit: fill (the default) distorts. A transform of rotate() keeps scale at 1; measured in Chrome by decomposing the computed matrix of each collage image: scale 1 by 1 on both, object-fit contain and cover. Transparent PNG, AVIF or SVG cut-outs go in <img> with a real alt text when they carry meaning.
- Satisfies: craft-image-no-distortion
### Pausable confetti, reduced-motion off (`mx-motion`) [standard · verified]
Give drifting confetti an off switch and an off state: a visible "Pause decoration" toggle with aria-pressed, a prefers-reduced-motion block that removes the animation, and no flashing. Never let the movement run behind text without these.
- How: WCAG 2.2.2: automatically starting movement lasting more than five seconds beside other content needs pause, stop or hide. Chrome demo: three drifting shapes run on an infinite 8 s loop; the button pauses all three (playState paused, aria-pressed true); with reduced motion emulated no animation exists. The toggle keeps one stable label and uses aria-pressed.
- Satisfies: a11y-reduced-motion, a11y-pause-stop-hide
### Collage with CSS, not reordering (`mx-order`) [standard · verified]
Collage by CSS, not by reordering. Keep DOM order equal to reading order, use grid or absolute placement for overlap, avoid CSS order, row-reverse and positive tabindex, and let the layout collapse to one column at 320 px with no horizontal scroll. Give h1 to h3 overflow-wrap: anywhere and size grid tracks as minmax(min(14rem, 100%), 1fr), because large display words and fixed tracks overflow at 320 px when text is zoomed to 200%.
- How: MDN: CSS order changes only the visual order, not the logical or tab order; WCAG 1.3.2 and 1.4.10. Chrome demo: no element has order other than 0, flex-direction reverse or tabindex above 0, and document width equals viewport width at 320, 768, 1280 and 1920 px. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; with root text at 200% and 320 px the page scrolled 180 px sideways (the word 'patterns' at 4rem is about 594 px wide; a 12rem track is 384 px); it passed at 100% text.
- Satisfies: a11y-meaningful-sequence, a11y-reflow
### Loud shapes, literal copy (`mx-copy`) [craft-consensus · verified]
Memphis energy goes in colour and shape. Keep headlines, labels and buttons literal, errors neutral ("Enter a delivery postcode") and payment or account copy free of jokes; save the wordplay for a supporting line.
- How: Same sources and tests as the playful-quirky-voice recipe: NN/g error guidance (non-blaming, no humour), GOV.UK error wording, Mailchimp on tone shifting with the reader's state. The demo error string contains none of invalid, incorrect, please, sorry, oops or an exclamation mark.
- Satisfies: copy-no-idioms-puns, copy-error-no-blame-words, copy-tone-fits-context

# Recipe: Illustration, hand-drawn and graphic-only art that stays accessible (`illustration-and-hand-drawn`)
Styles covered: illustration, illustrative, hand-drawn, graphics-only
**Keep:** Hand-drawn lines, doodles, marker highlights, hand lettering, flat or textured illustration, abstract graphic fields.
**Avoid:** Hero scenes assembled from div or SVG primitives in code; emoji or mixed-weight icons; pale pencil lines that carry meaning; headlines as images of text; the same artwork for light and dark grounds; draw-on animations that hide the art for reduced-motion users; abstract graphics as the only message.
Keep the drawn world: sketchy lines, hand lettering, abstract shapes and patterns. Use real authored artwork instead of code-assembled scenes, keep UI icons in one currentColor family, give informative art an alternative and decorative art none, keep meaningful lines at 3:1, and make draw-on animation end in a finished drawing.
**While designing:** Commission or draw the art and ship it as files, keep UI icons as one inline SVG family in currentColor, write alt text only for informative images, hold meaningful line art at 3:1 or better, set hand lettering as real text, and show the finished drawing when motion is reduced.
## Verified palette: Ink, paper and marker, computed
- paper: #FBF9F4
- ink: #1F1F23
- line-art: #595959
- line-art-lightest: #8C8C8C
- highlight: #FFE066
- annotation: #B3261E
- link: #1D4ED8
- dark-ground: #14141A
- dark-line-art: #E8E8EC
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on paper | #1F1F23 | #FBF9F4 | 15.61:1 | 4.5:1 |
| pencil line (meaningful) on paper | #595959 | #FBF9F4 | 6.66:1 | 3:1 |
| faintest meaningful line on paper | #8C8C8C | #FBF9F4 | 3.2:1 | 3:1 |
| ink on marker-yellow highlight | #1F1F23 | #FFE066 | 12.6:1 | 4.5:1 |
| red-pen annotation text on paper | #B3261E | #FBF9F4 | 6.21:1 | 4.5:1 |
| link on paper | #1D4ED8 | #FBF9F4 | 6.37:1 | 4.5:1 |
| dark mode: light line art on night ground | #E8E8EC | #14141A | 15.01:1 | 3:1 |
## Steps
### Use real authored illustration (`il-authored-art`) [our-take · judgement]
Make the illustration real: commissioned, drawn by you or licensed, exported as SVG, AVIF or PNG files and placed with img or picture. Do not build hero scenes out of div rectangles or a pile of inline SVG primitives, do not use placeholder image hosts, and do not use emoji as icons.
- How: The rule flags placeholder hosts (picsum, placehold, via.placeholder), product mock-ups made of div rectangles, hero-sized inline SVG scenes assembled from primitive shapes and emoji used as icons. An illustrator's exported file passes because it is a file, however many paths it has. Chrome demo scan: no emoji in buttons, links or headings, no inline SVG wider than half the viewport with five or more primitives, no placeholder hosts.
- Satisfies: distinct-real-imagery-and-icons
- Verification note: The rule comes from practitioner anti-slop detectors; the remedy (ship authored art as files) is our recommendation, not a standard.
### Separate UI icons from illustration (`il-icon-family`) [craft-consensus · verified]
Keep illustration and UI icons separate. Illustrations may use any palette; UI icons are one inline-SVG family at one stroke weight (24 px grid, stroke 2, round caps) with stroke="currentColor", sized with CSS, so hover, focus, dark mode and forced colours recolour them. Full-colour or raster icons are art, not controls.
- How: web.dev icons: inline SVG so CSS can style it; Apple HIG: one stroke weight across a set, matched to adjacent text. Measured in Chrome 156: the icon's computed stroke equals its button's computed colour on rest, on hover (#1D4ED8), in emulated dark scheme (#E8E8EC) and in forced colours (system colour), and the demo icons all use stroke-width 2.
- Satisfies: craft-icons-one-family, craft-icons-svg-currentcolor, distinct-real-imagery-and-icons
```html
<button class="btn"><svg class="icon" aria-hidden="true" viewBox="0 0 24 24" width="24" height="24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 12h16M14 6l6 6-6 6"/></svg> Read the latest entry</button>
```
### Alt text by purpose of the art (`il-alt`) [standard · verified]
Decide for each drawing whether it informs or decorates. Informative art gets alt text that states its purpose in context (about 150 characters at most, no "image of", no repeating nearby text); decorative flourishes get alt="" or are CSS backgrounds; inline SVG that carries meaning gets role="img" and an accessible name; complex diagrams get a longer description in the page text.
- How: WCAG 1.1.1: pure decoration should be ignorable by assistive technology. NN/g and WebAIM alt text guidance. Measured in Chrome 156 with Playwright's accessibility snapshot of the demo: the hero sketch and the labelled scribble appear as named images, the alt="" flourish and the aria-hidden pattern do not appear, and the heading is exposed as a level 1 heading.
- Satisfies: a11y-alt-text
### Meaningful lines at 3:1 (`il-line-contrast`) [standard · verified]
Hold every line that carries meaning (diagram strokes, input outlines, chart axes, the outline of a character that explains something) at 3:1 against its ground. On paper #FBF9F4, pencil #595959 is 6.66:1 and the faintest usable line #8C8C8C is 3.2:1. Pale guide lines such as #BDBDBD (1.79:1) are decoration only.
- How: WCAG 1.4.11 asks 3:1 for graphics needed to understand content; 1.4.3 asks 4.5:1 for text. Ink text is 15.61:1 on paper, ink on a marker-yellow highlight #FFE066 is 12.6:1, a red-pen annotation #B3261E is 6.21:1, the link #1D4ED8 is 6.37:1. A sketchy look comes from line wobble and texture, not from pale strokes. Rendered stroke and text colours in the Chrome demo match these pairs.
- Satisfies: a11y-non-text-contrast, a11y-contrast-text
### Hand lettering as real text (`il-lettering`) [craft-consensus · partly-verified]
Set hand lettering as real text in a handwriting or brush webfont at large sizes in dark ink, specified in rem so 200% text zoom works, and keep body copy in a plain face. Lettering that has to be artwork is allowed only as a logotype or when the look is essential, and then it needs alt text with the same words.
- How: WCAG 1.4.5: use real text when the technology can achieve the presentation; the exceptions are customizable, essential and logotype. WCAG 1.4.4: text must reach 200%; viewport-unit-only sizing fails (F94). 24 px or larger counts as large text (3:1), but we advise 4.5:1 anyway for thin strokes. Demo: the h1 is a real heading at 48 px (3rem), no image inside it. That handwriting faces read poorly at small sizes is our observation and is not tested here; self-host the font rather than relying on system stacks.
- Satisfies: a11y-images-of-text, a11y-resize-text, a11y-contrast-text
- Verification note: The WCAG facts are verified; the advice about small handwriting text and the 4.5:1 habit for thin strokes is our judgement, and the 200% zoom was not re-measured for this demo.
### Draw-on animation ends finished (`il-draw-on`) [standard · verified]
Make the finished drawing the default state and animate toward it: the path is fully visible with no animation, and the draw-on keyframes run once, in under five seconds, from hidden to complete. Under prefers-reduced-motion: reduce, remove the animation so the finished art is shown.
- How: MDN: honour reduce by replacing large motion with gentler effects and do not lose what the animation conveys. WCAG 2.2.2 applies to movement that lasts more than five seconds; a single 2 s draw is under that. Measured in Chrome: one animation of 2 s, 1 iteration; with reduced motion emulated there is no animation and stroke-dashoffset computes to 0, so nothing is hidden. If you set the hidden state in the base CSS and rely on the animation to reveal it, no-JS and reduced-motion users get an empty box.
- Satisfies: a11y-reduced-motion, a11y-pause-stop-hide
```css
.draw path { stroke-dasharray: 1; stroke-dashoffset: 0; animation: draw 2s cubic-bezier(0, 0, 0.2, 1) 1 both; }
@keyframes draw { from { stroke-dashoffset: 1; } to { stroke-dashoffset: 0; } }
@media (prefers-reduced-motion: reduce) { .draw path { animation: none; } }
/* path uses pathLength="1" */
```
### Second artwork for dark grounds (`il-dark-art`) [craft-consensus · verified]
Do not reuse dark line art on a dark ground. Ink #1F1F23 on a #14141A ground is 1.12:1. Ship a second artwork through picture with a prefers-color-scheme: dark source, or draw line art as inline SVG with currentColor and a token (#E8E8EC on #14141A is 15.01:1).
- How: web.dev theming and Apple HIG dark mode: re-check contrast in each theme and dim or swap images rather than inverting. Measured in Chrome with the colour scheme emulated: the picture element's currentSrc switches to the dark artwork, and the line-art token resolves to #E8E8EC on #14141A.
- Satisfies: a11y-non-text-contrast
```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="hero-dark.svg">
  <img src="hero-light.svg" alt="Pen sketch of a looping river crossing a valley" width="600" height="400">
</picture>
```
### Pair abstract graphics with real content (`il-graphics-only`) [our-take · judgement]
When the page uses abstract shapes, gradients or patterns instead of pictures, make them decoration (CSS background or aria-hidden SVG) and pair them with something concrete on the first screen: the product, a real screenshot, a drawing of the actual subject. Abstract art alone cannot say what you sell.
- How: A pattern that carries no information should be ignorable by assistive technology (WCAG 1.1.1), so use a CSS background or aria-hidden. The rule also flags hero-size inline SVG scenes built from primitive shapes, so build generative fields in CSS, canvas with fallback content, or ship them as exported files. The demo's pattern is a repeating-linear-gradient on an aria-hidden block, and no inline SVG in it is larger than half the viewport.
- Satisfies: distinct-real-imagery-and-icons, a11y-alt-text
- Verification note: Pairing abstract art with a concrete subject is our recommendation; the decorative-versus-informative handling is verified in il-alt.
### Wrap long words in display fonts (`il-reflow-200`) [standard · verified]
Handwriting and display fonts are wide: give the h1 overflow-wrap: anywhere and a smaller rem size under 30rem so a single word such as 'sketchbook' (446 px at 200%) fits.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; span.mark right edge was 478 px at 320 px wide; after the fix 0 px of overflow.
- Satisfies: a11y-reflow

# Recipe: Clay, skeuomorphic and dimensional UI with real edges and legible text (`clay-skeuomorphic-dimensional`)
Styles covered: claymorphism, skeuomorphic, dimensional
**Keep:** Inflated rounded shapes, soft raised and inset shadows, tactile buttons, material textures, knobs and switches.
**Avoid:** Shadow as the only boundary of an input or control; text directly on a texture; cards inside cards inside cards; one radius for every role; raster or fixed-colour icons for controls; state shown only by a colour shift on a pressed button.
Keep the puffy shapes, soft light, materials and knobs. Let the shadow be mood, not the boundary: give controls a transparent border that survives forced colours and an edge colour that reaches 3:1, put text on opaque plates, flatten groups so cards do not nest, and vary radius and elevation by role.
**While designing:** Define radius and shadow tokens per role, give inputs a 3:1 edge and every raised surface a transparent 2px border, keep text on solid fills, put the metal or leather texture on a base colour and measure its worst pixel, use outline for focus, and show toggle state with knob position and text.
## Verified palette: Clay and metal, computed
- canvas: #E6F0EC
- surface: #F3F9F6
- ink: #1E2B27
- text-muted: #44524D
- button-peach: #FFB8A3
- button-primary: #2F5BEA
- edge: #5E7A70
- metal-light: #E4E7EA
- metal-dark: #B9BEC3
- metal-ink: #1B1F23
- dark-canvas: #14191A
- dark-surface: #1D2426
- dark-ink: #E8F0EC
- dark-muted: #A9B8B2
- dark-edge: #7E948B
- dark-button: #7FD1B9
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on canvas | #1E2B27 | #E6F0EC | 12.61:1 | 4.5:1 |
| ink text on clay surface | #1E2B27 | #F3F9F6 | 13.77:1 | 4.5:1 |
| muted text on clay surface | #44524D | #F3F9F6 | 7.69:1 | 4.5:1 |
| ink on peach clay button | #1E2B27 | #FFB8A3 | 8.84:1 | 4.5:1 |
| white on primary-blue button | #FFFFFF | #2F5BEA | 5.52:1 | 4.5:1 |
| input edge on clay surface (UI boundary) | #5E7A70 | #F3F9F6 | 4.38:1 | 3:1 |
| input edge on canvas | #5E7A70 | #E6F0EC | 4.01:1 | 3:1 |
| ink on brushed-metal plate, worst rendered pixel (measured) | #1B1F23 | #B3B7BB | 8.22:1 | 4.5:1 |
| dark: ink on dark clay surface | #E8F0EC | #1D2426 | 13.59:1 | 4.5:1 |
| dark: muted on dark clay surface | #A9B8B2 | #1D2426 | 7.64:1 | 4.5:1 |
| dark: input edge on dark surface (UI boundary) | #7E948B | #1D2426 | 4.87:1 | 3:1 |
| dark: dark text on mint button | #1E2B27 | #7FD1B9 | 8.2:1 | 4.5:1 |
## Steps
### Real edges on controls (`dm-edges`) [standard · verified]
Treat shadows as mood and give anything the user must find a real edge or fill. Inputs get a 2px edge in #5E7A70 (4.38:1 on the clay surface, 4.01:1 on the canvas); buttons get a label in dark ink on a coloured fill, not a surface-coloured pill that only a shadow separates from the page.
- How: Clay surface #F3F9F6 on canvas #E6F0EC is only 1.09:1, which is a fine look and no boundary. Text pairs: ink #1E2B27 on surface 13.77:1, muted #44524D on surface 7.69:1, ink on peach #FFB8A3 8.84:1, white on blue #2F5BEA 5.52:1. WCAG 1.4.11 asks 3:1 for visual information needed to identify a control. Rendered colours in the Chrome demo match every claimed pair.
- Satisfies: a11y-non-text-contrast, a11y-contrast-text
### Transparent borders and outline focus (`dm-forced-focus`) [craft-consensus · verified]
Give every raised surface and control a 2px transparent border, and draw keyboard focus with outline. In forced-colors mode the soft shadows disappear and the transparent border becomes a visible system-colour edge; the outline stays.
- How: MDN: in forced-colors mode box-shadow is forced to none while border-color and outline-color are kept as system colours. Measured in Chrome 156 with forced colours emulated: card and button box-shadow compute to none, the transparent border computes to rgb(0, 0, 0) at 2px, and a pixel row across the card edge shows black pixels against white where the normal rendering had a soft shadow with no hard edge; keyboard focus is a solid 3px outline in both modes. Normal mode is unchanged because a transparent border draws nothing.
- Satisfies: a11y-focus-visible, craft-contrast-preferences, a11y-non-text-contrast
```css
.card, .btn { border: 2px solid transparent; box-shadow: var(--raise); }
:focus-visible { outline: 3px solid var(--ink); outline-offset: 3px; }
```
### Radius and elevation per role (`dm-tokens`) [craft-consensus · partly-verified]
Name a radius per role (control 14, input 10, card 28, media 20, badge pill) and an elevation per state (raise, inset, press) and use each one the same way everywhere. Keep card-row shadow blur modest (14 px here) and do not combine a visible hairline border with a blur of 32 px or more on three or more adjacent cards.
- How: The rule fails a page where every role shares one radius of 16 px or more, or where three adjacent cards pair a visible 1px border with a blur of 32 px or more. Chrome demo: card, button, input and badge compute to 28, 14, 10 and 999 px; the three cards in the row have a 14 px blur and a transparent border. Soft clay shadows read well at 12 to 20 px.
- Satisfies: distinct-radius-elevation-scale
- Verification note: Thresholds are from practitioner detectors and articles; we measured the demo against the rule text only.
### No raised boxes inside clay cards (`dm-no-nesting`) [craft-consensus · partly-verified]
Let a clay card hold unboxed content: headings, paragraphs and list rows separated by spacing, with no raised or inset container inside it other than interactive controls. If a skeuomorphic panel needs a recessed well, make the well the panel instead of a box inside another box.
- How: Rule: no bordered, shadowed or tinted card container inside another. We implemented that check for non-interactive containers with radius of 4 px or more and ran it in Chrome: the demo has no nested container, and a deliberately nested card inserted by the test is flagged. Buttons, inputs and badges are controls, not containers, so they are exempt in our check; the rule text does not say so explicitly.
- Satisfies: distinct-no-nested-cards
- Verification note: Our implementation of the check treats controls as exempt, which is an interpretation; the underlying rule is from practitioner sources.
### Inline SVG icons with currentColor (`dm-icons`) [craft-consensus · verified]
Draw UI icons as inline SVG with stroke or fill set to currentColor so hover, dark mode and forced colours recolour them. Keep realistic or 3D icon renderings for illustration (decorative, alt="" or named) and never as the only control icon.
- How: web.dev icons: inline SVG so CSS can style it. Measured in Chrome: the Reset icon's computed stroke equals its button colour in light and in emulated dark scheme, and the stroke attribute is currentColor.
- Satisfies: craft-icons-svg-currentcolor
### Measure text over textures (`dm-texture-text`) [craft-consensus · verified]
Put realistic textures (brushed metal, leather, paper) on a solid base colour and measure the worst pixel under each line of text. The demo plate has a #E4E7EA to #B9BEC3 gradient with fine stripes; ink #1B1F23 measured 8.22:1 against its worst rendered pixel (#B3B7BB).
- How: Method: hide the text, screenshot the text box, read every pixel and compute the WCAG ratio against the text colour; the smallest ratio is the one to report. The gradient end alone would be 8.85:1, the stripes lower the darkest pixel and the result is 8.22:1. Keep textures subtle at the text and strong around the edges of the plate.
- Satisfies: a11y-contrast-text
### Toggle state by shape and text (`dm-toggle-state`) [craft-consensus · partly-verified]
Make pressed, on and selected states differ by shape and text, not by a colour shift: a switch knob that moves, an inset shadow that changes, and a label that says On or Off, with aria-pressed (or a native checkbox) carrying the state.
- How: Inclusive Components toggle button and the ARIA switch pattern; WCAG 1.4.1. Chrome demo: aria-pressed flips from false to true, the knob moves 18 px and the text changes from "Eco mode off" to "Eco mode on". The label text changes with the state here, so aria-pressed is not used together with a label that already says the opposite; if you keep the label fixed, keep aria-pressed.
- Satisfies: comp-toggle-visual-state-not-color, a11y-color-not-only
- Verification note: Behaviour measured in Chrome; the label-versus-aria-pressed point follows the Button pattern note from an earlier verification pass and was not re-read.
### Lighter surfaces instead of dark shadows (`dm-dark`) [our-take · judgement]
In dark mode, replace dark drop shadows with lighter surfaces and a thin inset highlight, and re-pick the edge colour: ink #E8F0EC on surface #1D2426 is 13.59:1, muted #A9B8B2 7.64:1, edge #7E948B 4.87:1, dark text on mint #7FD1B9 8.2:1.
- How: Apple HIG dark mode and web.dev theming: define dark tokens separately and re-check contrast per theme. Chrome demo: under emulated dark scheme the tokens resolve to exactly these colours and the raise shadow becomes an inset highlight plus a dark drop. Whether this elevation reads well is a visual judgement; the numbers are measured.
- Satisfies: craft-dark-mode-reverify
- Verification note: Contrast values are computed; the elevation treatment for dark clay is our design judgement.
### Min() grids and wrapping cards (`cl-reflow-200`) [standard · verified]
Write every auto-fit or auto-fill grid as repeat(auto-fit, minmax(min(15rem, 100%), 1fr)); use overflow-wrap: anywhere on cards and max-inline-size: 100% on buttons; cut card and page padding to 1rem under 30rem.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200%; minmax(15rem,1fr) is 480 px at 200% text and made the page scroll 192 px sideways at 320 px; with min(15rem,100%) and reduced padding the overflow was 0.
- Satisfies: a11y-reflow

# Recipe: Organic, botanical and earthy palettes that are not the reflex cream (`natural-organic-earthy`)
Styles covered: organic-soft, botanical-natural, earthy
**Keep:** Rounded forms, gentle shadows, botanical photography, mossy greens, ochres and soil browns, a slow human tone.
**Avoid:** Cream background with terracotta accent and a serif display face by reflex; sage-green text on pale green; links that differ from body text only in a muted green; the same large radius on every element; leaf photography under text without a plate.
Keep the calm, rounded, plant-and-soil feeling. Take the ground colour from the subject (leaf mist, forest, soil) instead of cream with terracotta, vary radius by role with asymmetrical shapes only on images, and darken the greens and browns until text, links and field edges pass.
**While designing:** Pick the page ground from the subject (leaf-tinted mist, deep forest or soil) and run the cream test on it, use dark moss for text and links with underlines, give field edges 3:1, set different radii for controls, cards, tags and images, and put text over botanical imagery on a plate.
## Verified palette: Moss, mist and soil, computed
- ground-mist: #EEF2EA
- ink: #1F2A1C
- text-secondary: #4A5A40
- accent-moss: #3F5D3A
- accent-ochre: #8A5A00
- field-edge: #6B7A5E
- dark-ground-forest: #14231A
- dark-text: #E8EFE0
- dark-text-muted: #B9C8A8
- dark-button-lime: #B9D98A
- ground-soil: #2A1F18
- soil-accent-amber: #E0B15A
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| ink text on mist | #1F2A1C | #EEF2EA | 13.17:1 | 4.5:1 |
| moss-grey secondary text on mist | #4A5A40 | #EEF2EA | 6.55:1 | 4.5:1 |
| moss link on mist (underlined) | #3F5D3A | #EEF2EA | 6.53:1 | 4.5:1 |
| white on moss button | #FFFFFF | #3F5D3A | 7.4:1 | 4.5:1 |
| ochre accent text on mist | #8A5A00 | #EEF2EA | 5.23:1 | 4.5:1 |
| input edge on white field | #6B7A5E | #FFFFFF | 4.59:1 | 3:1 |
| input edge on mist | #6B7A5E | #EEF2EA | 4.05:1 | 3:1 |
| dark forest: leaf-white text on forest | #E8EFE0 | #14231A | 13.89:1 | 4.5:1 |
| dark forest: muted leaf text on forest | #B9C8A8 | #14231A | 9.25:1 | 4.5:1 |
| forest text on lime button | #14231A | #B9D98A | 10.39:1 | 4.5:1 |
| soil: leaf-white text on soil brown | #E8EFE0 | #2A1F18 | 13.65:1 | 4.5:1 |
| soil: amber accent on soil brown | #E0B15A | #2A1F18 | 8.11:1 | 4.5:1 |
| leaf-white text on 86% forest plate over the lightest leaf pixel (#2F402F composite, measured 9.42) | #E8EFE0 | #2F402F | 9.42:1 | 4.5:1 |
## Steps
### Choose ground from the subject (`nt-ground`) [craft-consensus · partly-verified]
Choose the page ground from the subject's world: leaf-tinted mist (#EEF2EA), deep forest (#14231A) or soil brown (#2A1F18), with moss (#3F5D3A) and ochre (#8A5A00) accents. If you do want cream with terracotta and a serif display face, record the subject reason in the direction file.
- How: The rule (advisory) reports three things together: a cream background (every channel at least 209, red at least green at least blue, red minus blue between 6 and 48), a terracotta or clay accent (hue about 10 to 30 degrees, moderate saturation) and a serif display face. We ran the rule's cream condition in code: mist #EEF2EA, forest and soil are not cream, while #F5EFE6, #F4EDE0 and #FAF6EE are. Moss is at about 111 degrees, ochre 39, lime 84 and amber 39, outside the terracotta band. An exception record can be one line: "Cream ground chosen because the product is a bakery; paper and flour are cream."
- Satisfies: distinct-palette-not-reflex-cream
- Verification note: Thresholds are practitioner detector values, and the alternative palettes are our suggestions; the colour arithmetic was computed.
### Darken natural colors until they pass (`nt-contrast`) [standard · verified]
Darken the natural colours until they pass, and keep sage for decoration. Ink #1F2A1C on mist is 13.17:1; secondary moss-grey #4A5A40 6.55:1; moss links #3F5D3A 6.53:1; white on a moss button 7.4:1; ochre #8A5A00 5.23:1. Sage #7A8A6C on mist is 3.26:1 and fails as text.
- How: A moss link against ink body text is 2.02:1, below the 3:1 needed to tell a link from surrounding text by colour alone, so underline links (WCAG technique G183 and failure F73). Computed colours of the demo's text, links, button and accent match the claimed pairs in Chrome.
- Satisfies: a11y-contrast-text, a11y-color-not-only
### Visible edges on soft fields (`nt-edges`) [standard · verified]
Soft rounded fields still need an edge: #6B7A5E at 2px is 4.59:1 on white and 4.05:1 on mist. Do not use a pale sage outline or a shadow as the only sign of a field.
- How: WCAG 1.4.11: 3:1 for visual information needed to identify a control. Measured: the rendered input border is #6B7A5E in the demo.
- Satisfies: a11y-non-text-contrast
### Shape and elevation per role (`nt-tokens`) [craft-consensus · partly-verified]
Vary shape by role: controls 12 px, cards 24 px, tags pill, and an asymmetrical organic radius on photographs only. Use two elevations (1px/2px small, 8px 24px soft) and never pair a hairline border with a blur of 32 px or more on a row of three cards.
- How: The rule fails a page where every role shares one radius of 16 px or more, which is the default look of soft UI. Measured in Chrome: button 12 px, card 24 px, tag 999 px, photo a four-value elliptical radius, card shadow blur 24 px with no border.
- Satisfies: distinct-radius-elevation-scale
- Verification note: Rule thresholds come from practitioner detectors; measured against the rule text only.
```css
:root { --r-control: 12px; --r-card: 24px; --r-pill: 999px; --r-blob: 58% 42% 55% 45% / 48% 58% 42% 52%;
  --sh-1: 0 1px 2px rgb(31 42 28 / .12); --sh-2: 0 8px 24px rgb(31 42 28 / .12); }
.photo { border-radius: var(--r-blob); }
```
### Plate under text on photos (`nt-plate`) [craft-consensus · verified]
Do not set text straight on leaf or garden photography. Put it on a plate: an 86% forest plate (#14231A) gave leaf-white text 9.42:1 against the worst pixel even over the lightest leaf colour in the test image.
- How: Method: hide the text, screenshot the plate, compute the WCAG ratio of the text colour against every pixel and report the smallest. The test image runs from #6FBF73 to #D7F5B1; replace it with your brightest real photograph and measure again.
- Satisfies: a11y-contrast-text
### Alt text for botanical photos (`nt-alt`) [standard · verified]
Write real alt text for botanical photography when it informs (species, a visible feature), and alt="" when it only decorates.
- How: NN/g and WebAIM: purpose from context, no "image of", empty alt for decoration. Chrome accessibility snapshot of the demo: the photo is exposed as a named image "Monstera deliciosa leaf with natural splits, held against a white wall".
- Satisfies: a11y-alt-text
### Dark natural theme colors (`nt-dark`) [craft-consensus · partly-verified]
For a dark natural theme use forest (#14231A) or soil (#2A1F18) with leaf-white text #E8EFE0 (13.89:1 on forest, 13.65:1 on soil), muted #B9C8A8 (9.25:1), lime button #B9D98A with forest text (10.39:1) and amber #E0B15A on soil (8.11:1).
- How: Define the dark values as their own tokens and recheck every pair. Chrome demo: under emulated dark scheme the tokens resolve to exactly these colours. Dark forest and soil are the natural-world answer to the near-black plus neon default.
- Satisfies: craft-dark-mode-reverify
- Verification note: Pairs are computed and rendered; the framing against near-black plus neon is our opinion.
### Cap image widths, wrap long words (`nt-reflow-200`) [standard · verified]
Fixed rem image widths need max-width: 100% (14rem is 448 px at 200%); put overflow-wrap: anywhere on body so long words cannot widen the page.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; img.photo was 448 px wide in a 320 px viewport plus a 24 px text-spacing overflow; both were gone after the change.
- Satisfies: a11y-reflow
### Caption strip, not nested card (`nt-plate-not-card`) [our-take · partly-verified]
Make a caption plate on a rounded photo frame a square-cornered full-width scrim strip along the bottom edge (let the frame's overflow: hidden round its corners); a rounded tinted plate inside a rounded frame counts as a nested card (distinct-no-nested-cards).
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page at 320 px with the root font size at 200% and the audit probes; distinct-no-nested-cards failed with a rounded, tinted .plate inside .leafy and passed after the strip change; the check counts boxes with a radius of 4 px or more.
- Satisfies: distinct-no-nested-cards
- Verification note: Recorded from one audit run on one demo page; the audit check is a heuristic and the technique has no independent source.

# Recipe: Atmospheric full-bleed heroes with text you can read (`atmospheric-full-bleed-hero`)
Styles covered: atmospheric, hero-full-bleed
**Keep:** Edge-to-edge photography or illustration, haze, grain, gradients and colour atmosphere.
**Avoid:** White text on a photo with no scrim; a scrim tuned to the average rather than the brightest pixel; no fallback colour behind the image; text across the full 1920 px of a monitor; relying on a gradient scrim that forced-colours mode removes.
Keep the edge-to-edge image, the haze, grain and light. Put one scrim under the text column, tuned for the brightest pixel the image can offer, keep a dark colour behind the image for when it fails, and hold the content in a normal container while only the picture bleeds.
**While designing:** Choose a scrim colour and alpha from the brightest pixel under the text (0.72 of a near-black reaches 7:1 over pure white), set a dark background-color on the hero, keep atmosphere on its own aria-hidden layer, limit the content to a 1280px wrapper and a text column of about 36rem, and measure the rendered pixels at 375, 768, 1440 and 1920 px.
## Verified palette: Scrim over bright imagery, computed
- scrim: #0B1020 at 72%
- text: #FFFFFF
- text-muted: #D5DAE6
- fallback-ground: #0B1020
- worst-case-white: #FFFFFF
- worst-case-yellow: #FFE600
- worst-case-sky: #BFE9FF
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| white on 72% scrim over pure white (worst case) | #FFFFFF | #4F535E | 7.69:1 | 7:1 |
| white on 72% scrim over bright yellow #FFE600 | #FFFFFF | #4F4C17 | 8.83:1 | 7:1 |
| white on 72% scrim over pale sky #BFE9FF | #FFFFFF | #3D4D5E | 8.67:1 | 7:1 |
| muted #D5DAE6 on 72% scrim over pure white | #D5DAE6 | #4F535E | 5.49:1 | 4.5:1 |
| white on the fallback colour shown if the image fails | #FFFFFF | #0B1020 | 18.93:1 | 7:1 |
## Steps
### One scrim for the brightest pixel (`am-scrim`) [standard · verified]
Lay one scrim under the text column and tune it for the brightest pixel the image can offer, not the average. A #0B1020 scrim at 72% gives white text 7.69:1 over pure white, 8.83:1 over yellow #FFE600 and 8.67:1 over pale sky #BFE9FF; muted #D5DAE6 text is 5.49:1 over pure white.
- How: Composite the scrim over the worst backdrop, then compute the WCAG ratio; 72% is where white reaches 7:1 (AAA for body text) on a pure white backdrop, with 4.5:1 as the minimum for muted text. Method used to verify in Chrome 156: hide the text, screenshot the text box, read every pixel and take the smallest ratio. On a test image that is white, bright yellow and pale sky behind the text, the headline measured 7.69, 8.53, 8.64 and 8.64:1 at 375, 768, 1440 and 1920 px, the lead 7.69, 8.53, 7.65 and 7.65, and the muted line 5.49, 5.49, 5.47 and 5.47. The same page without the scrim measured 1.27:1 against the worst pixel.
- Satisfies: craft-contrast-text-on-media, craft-contrast-body-enhanced, a11y-coga-text-not-over-busy-background
```css
.hero-scrim { position: absolute; inset: 0;
  background: linear-gradient(90deg, rgb(11 16 32 / .72) 0%, rgb(11 16 32 / .72) 60%, rgb(11 16 32 / 0) 100%); }
@media (max-width: 60rem) { .hero-scrim { background: rgb(11 16 32 / .72); } }  /* text spans the width */
```
### Dark hero background fallback (`am-fallback`) [craft-consensus · verified]
Set a dark background-color on the hero element itself, under the image, so white text still has 18.93:1 when the image is slow, blocked or fails to load.
- How: Without it, white text on a missing image falls back to the page background and disappears. Chrome demo: with the image and scrim removed the hero computes to rgb(11, 16, 32) behind white text. Also keep real, meaningful alt text on the image when it carries content; the demo image is decorative and has alt="".
- Satisfies: craft-contrast-text-on-media
### Forced-colors text block fallback (`am-forced`) [craft-consensus · verified]
Do not rely on a gradient scrim for readability in forced-colors mode: it is removed. Under @media (forced-colors: active) give the text block a Canvas background and CanvasText colour with a visible border, so the pair is a guaranteed system contrast.
- How: MDN: in forced-colors mode background-image is forced to none unless it is URL-based, and colours become system colours. Measured in Chrome 156 with forced colours emulated over a dark photo: the scrim computes to none, the headline is black and the worst rendered contrast is 1.15:1 without a plate, and 21:1 with a Canvas plate. This is a small usability tweak, which MDN allows; do not build a separate forced-colors design. The emulation uses a light system theme; a black high-contrast theme flips the colours, not the logic.
- Satisfies: craft-contrast-text-on-media, a11y-coga-text-not-over-busy-background
```css
@media (forced-colors: active) {
  .copy { background-color: Canvas; color: CanvasText; padding: 1.25rem; border: 2px solid CanvasText; }
}
```
### Only the picture bleeds (`am-container`) [craft-consensus · verified]
Let only the picture bleed. Put the headline, text and call to action in a centred wrapper of 1280 px or less, with a text column of about 36rem, and give the hero image and band the full width.
- How: At a 1920 px viewport the Chrome demo measures the hero and image at 1920 px, the wrapper at 1280 px and the text column at 576 px. The advisory rule allows only backgrounds and full-bleed media to exceed 1400 px.
- Satisfies: craft-container-max-width
### Atmosphere layer below the scrim (`am-atmosphere`) [craft-consensus · verified]
Keep haze, grain and light leaks on their own aria-hidden, pointer-events:none layer between the image and the scrim, and measure the text with that layer on. Never place text on atmosphere alone; scrim first, then text.
- How: The grain layer (opacity 0.12, repeating radial dots) is part of the screenshot in the pixel measurements above, so the reported ratios include it. W3C COGA asks for text on solid or low-detail backgrounds or a solid panel or overlay, and says text over photos, video, gradients and patterns of varying luminance is a barrier.
- Satisfies: a11y-coga-text-not-over-busy-background, craft-contrast-text-on-media

# Recipe: Futuristic, purple-led and retro-computing looks without the default tells (`tech-aesthetics-purple-retro`)
Styles covered: futuristic-tech, hue-purple, retro-computing
**Keep:** Thin lines, grids, data motifs, a committed purple, pixel type, terminal windows, phosphor colours, stepped animation.
**Avoid:** Violet-to-blue gradients and cyan on near-black as defaults; chromatic zero-offset glow; pulsing Live or New or version pills that report nothing; endless blinking cursors and CRT flicker; scanline overlays that eat text contrast; hairlines that carry meaning below 3:1.
Keep the precision, the single bold hue and the terminal nostalgia. Pick an accent from the brand instead of violet or cyan, replace glow with hairlines and flat fills, show status only when it is true, and make pixel and CRT effects finite, measured and motion-safe.
**While designing:** State the accent hue and why in the direction file, use flat accents on graphite (orange, lime, amber, green) or a solid committed purple with an exception record, draw depth with hairlines and neutral shadows, bind any status text to real data, and measure the contrast of text under scanlines.
## Verified palette: Graphite signal, committed purple and phosphor, computed
- graphite: #0E0F11
- panel-surface: #15161A
- text: #F4F4F5
- text-muted: #9A9AA2
- meaningful-line: #6B6B75
- decorative-grid: #2A2A30
- accent-signal-orange: #FF5B1F
- purple-deep: #4C1D95
- purple-text-on-white: #5B21B6
- purple-partner-sun: #FFE45E
- purple-soft-text: #E9D5FF
- phosphor-amber: #FFB000
- phosphor-amber-ground: #1A1100
- phosphor-green: #33FF66
- phosphor-green-ground: #001A0A
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| futuristic: text on panel surface | #F4F4F5 | #15161A | 16.45:1 | 4.5:1 |
| futuristic: muted text on panel surface | #9A9AA2 | #15161A | 6.47:1 | 4.5:1 |
| futuristic: signal-orange accent on panel surface (large text, icons, UI) | #FF5B1F | #15161A | 5.83:1 | 3:1 |
| futuristic: graphite text on signal-orange button | #0E0F11 | #FF5B1F | 6.18:1 | 4.5:1 |
| futuristic: input edge on panel surface (UI boundary) | #6B6B75 | #15161A | 3.43:1 | 3:1 |
| purple brand: white on deep purple | #FFFFFF | #4C1D95 | 10.95:1 | 4.5:1 |
| purple brand: sun-yellow on deep purple | #FFE45E | #4C1D95 | 8.61:1 | 4.5:1 |
| purple brand: pale lilac text on deep purple | #E9D5FF | #4C1D95 | 8.05:1 | 4.5:1 |
| purple brand: purple link on white | #5B21B6 | #FFFFFF | 8.98:1 | 4.5:1 |
| purple brand: deep purple on yellow button | #4C1D95 | #FFE45E | 8.61:1 | 4.5:1 |
| retro: amber phosphor on dark brown-black | #FFB000 | #1A1100 | 10.2:1 | 4.5:1 |
| retro: green phosphor on dark green-black | #33FF66 | #001A0A | 13.57:1 | 4.5:1 |
## Steps
### Flat accent from the brand (`ft-accent`) [craft-consensus · partly-verified]
Take the accent hue from the brand or subject and state it in the direction file. On graphite #0E0F11 use a flat signal colour instead of violet gradients or cyan: orange #FF5B1F (5.83:1 on the #15161A panel, graphite text on an orange button 6.18:1), lime #C8F169 (14.83:1), amber or phosphor green.
- How: The rule flags any gradient stop or primary accent with a hue of 260 to 310 degrees and a cyan accent on a near-black ground, unless the brand is that colour and the direction file says so. We ran that hue test in code over the demo's accents: orange is at 16 degrees, so nothing is flagged. Orange is not a neutral choice either: pick the hue because it is the brand or the subject, not because it avoids the check.
- Satisfies: distinct-no-ai-palette
- Verification note: The hue band and the cyan-on-black condition come from practitioner detectors and articles (some rated low weight); contrast and hue arithmetic were computed.
### Purple as a solid, not gradient (`ft-purple`) [our-take · judgement]
If purple is the brand, commit to it as a solid, not a gradient, and record the exception. Deep purple #4C1D95 gives white 10.95:1, sun yellow #FFE45E 8.61:1 and pale lilac #E9D5FF 8.05:1; on white the link purple #5B21B6 is 8.98:1 and deep purple on a yellow button is 8.61:1. Pair it with a warm partner (yellow), not a blue or pink gradient.
- How: The rule exempts a purple that is the brand when the direction file says so. The demo section is a flat #4C1D95 (hue 264, inside the 260 to 310 band), computed background-image none, which is why it needs the record. Example record: "Primary colour #4C1D95. Purple chosen because the studio's riso inks are violet and yellow; no gradients." The tag hue-purple only describes that purple is dominant; the exception is what stops it reading as the default. Note: the audit's distinct-no-ai-palette reports purple text pairs in the 260 to 310 degree hue band as a minor even when the exception is recorded in direction.md; accept that minor in writing, it is not a failure of the recipe.
- Satisfies: distinct-no-ai-palette, a11y-contrast-text
- Verification note: Contrast figures are computed; the advice to commit to a flat purple with a warm partner and to write the exception record is our judgement.
```text
direction.md
Accent: #4C1D95 (violet), partner #FFE45E (yellow).
Exception to distinct-no-ai-palette: purple is the brand (violet riso ink). Flat fills only, no violet-to-blue gradient.
```
### Hairlines and flat fills, not glow (`ft-no-glow`) [craft-consensus · partly-verified]
Build the precise, technical feel from hairlines, grids and flat fills instead of glow. Use a 1px border (#2A2A30 on graphite for decoration), a neutral shadow such as 0 1px 0 rgb(0 0 0 / .4), and keep any coloured halo only where it encodes a state. Draw focus as an outline, not a glow.
- How: The rule flags a chromatic box-shadow or text-shadow with zero offset and blur of 3 px or more, and a saturated radial-gradient halo behind a hero on a dark page. We implemented that check in Chrome: the demo has no such shadow or radial gradient, and a deliberately added 0 0 12px #39FF88 shadow is flagged. A glow that shows selection or error is allowed by the rule; here state is shown by outlines and text.
- Satisfies: distinct-no-decorative-glow
- Verification note: Rule thresholds are from practitioner detectors; verified only against the rule text on a demo page.
### Only true, current status labels (`ft-status`) [craft-consensus · partly-verified]
Show a status label only when it reports something true and current: render the release line from the release record at build time with a real date, link it to the changelog, and drop pulsing dots and "Live", "New" or "Beta" pills that nothing updates.
- How: The rule flags pulsing status dots, pills reading new, live, beta or a version number in the first viewport unless bound to a data attribute or release record, and a pill chip above the hero heading. Chrome demo: no element under 1.5 aspect ratio has an infinite animation, no pill matches, and the release line carries a data-source attribute and a time element with a datetime. If something really is live, use role="status" on the text that changes.
- Satisfies: distinct-no-fake-status-badges
- Verification note: Rule is from practitioner sources; the data-binding pattern is our implementation of the rule's exception.
```html
<p class="status" data-source="releases.json#latest">Release 2.4.1 · <time datetime="2026-10-28">28 October 2026</time></p>
```
### Meaningful thin lines at 3:1 (`ft-lines`) [standard · verified]
Thin and technical must still be legible: hold lines that carry meaning (input edges, chart axes, dividers that separate controls) at 3:1, and keep decorative grids below that. The input edge #6B6B75 is 3.43:1 on the panel and 3.64:1 on graphite; the decorative grid #2A2A30 is not meant to be seen as content. Text: #F4F4F5 16.45:1 and muted #9A9AA2 6.47:1 on the panel.
- How: WCAG 1.4.11 for UI components and graphics; the Enhanced Contrast Understanding page notes that thin fonts render fainter, so use heavier weights or exceed the minimum. Use font-weight 400 or above for small light-on-dark text. Computed colours of the demo's text, accent, button and input edge match the claimed pairs in Chrome.
- Satisfies: a11y-non-text-contrast, a11y-contrast-text
### Skip link and main in terminal layouts (`ft-bypass`) [standard · verified]
Terminal and retro-computer layouts built from stacked panels still need a skip link as the first focusable element and a main landmark around the content; panels are sections with headings, not bare divs.
- How: Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; the demo page failed a11y-bypass-blocks with 'no skip link and no main landmark' until a Skip to content link (visible on focus, high contrast) and main id=main were added.
- Satisfies: a11y-bypass-blocks
### Self-hosted pixel face at grid multiples (`rc-pixel-type`) [our-take · judgement]
Self-host the pixel face and set it in rem at whole multiples of its design grid (an 8 px font at 16 or 24 px), use it for headings and labels, and keep long text in a plain monospace or sans face. Draw pixel art as images with image-rendering: pixelated at integer scales (an 8 px sprite shown at 64 px), with alt text or alt="".
- How: WCAG 1.4.4 asks for 200% resize and lists viewport-unit-only sizing as a failure (F94), so size in rem. Integer multiples keep pixel edges crisp; that advice and the legibility of pixel fonts for body text are our judgement and were not measured. Chrome computes image-rendering: pixelated for the demo sprite. The MDN image-rendering page is not in sources.json.
- Satisfies: a11y-resize-text, a11y-contrast-text
- Verification note: Resize rule is verified from WCAG pages; the pixel-grid multiples and body-text advice are our judgement.
### Phosphor colors that pass contrast (`rc-phosphor`) [standard · verified]
Use phosphor colours on dark grounds that pass: amber #FFB000 on #1A1100 is 10.2:1 and green #33FF66 on #001A0A is 13.57:1. Skip cyan on near-black; for dim secondary text keep at least 4.5:1 (for example #9A7A33 on #1A1100 is 4.63:1).
- How: Amber (hue 41) and green (hue 135) are outside the 260 to 310 band and are not cyan. Rendered colours in the Chrome demo match the claimed pairs.
- Satisfies: a11y-contrast-text, distinct-no-ai-palette
### Finite CRT and cursor effects (`rc-crt-blink`) [standard · verified]
Keep CRT and cursor effects finite, static where possible and measured. Blink the cursor for four 1 s cycles with steps(1) and leave it visible; run a typed reveal once as a clip-path inset() animation with steps(), never by animating a fixed width with overflow:hidden and white-space:nowrap (that clips under WCAG text spacing and overflows at 200% text); skip flicker; remove all of it under prefers-reduced-motion. A scanline overlay is pointer-events:none and aria-hidden; 12% black stripes cost amber text only down to 7.88:1.
- How: WCAG 2.2.2 covers blinking that lasts more than five seconds beside other content (4 s here); WCAG 2.3.1 passes at no more than three flashes per second (1 per second here). Measured in Chrome 156: the cursor animation computes to 1s, 4 iterations, steps(1); with reduced motion emulated no animation exists. A solid block of text colour under the overlay rendered at rgb(224,155,0) for amber and rgb(45,224,90) for green, against the plain backgrounds 7.88:1 and 10.35:1. Computed: at 30% stripes amber text falls to 5.12:1 and at 20% it is 6.56:1, so keep the overlay at 20% or less. Measured 2026-11-06 in Chrome (Playwright, channel chrome) on the recipe demo page with the audit probes; the width/overflow:hidden/nowrap typed reveal failed a11y-text-spacing (1 element at 1440 px, 1 more at 320 px) and overflowed by 280 px at 200% text; the clip-path version passed.
- Satisfies: a11y-pause-stop-hide, a11y-flashes, a11y-reduced-motion
```css
.cursor { animation: blink 1s steps(1, end) 4; }
@keyframes blink { 50% { opacity: 0; } }
.typed { overflow-wrap: anywhere; animation: type 1.2s steps(24, end) 1 both; }
@keyframes type { from { clip-path: inset(0 100% 0 0); } to { clip-path: inset(0); } }
.term::after { content: ""; position: absolute; inset: 0; pointer-events: none;
  background: repeating-linear-gradient(0deg, rgb(0 0 0 / .12) 0 1px, transparent 1px 3px); }
@media (prefers-reduced-motion: reduce) { .cursor, .typed { animation: none; } }
```
### Easing for windows, steps for sprites (`rc-easing`) [craft-consensus · partly-verified]
Keep the 8-bit snap where it belongs and use proper easing for the windows: a window opens in 150 ms with a decelerating curve and closes in 100 ms with an accelerating one; reserve steps() for frame-by-frame sprites and typed text, never linear on a moving window.
- How: NN/g and Material motion: enter with ease-out, leave with ease-in, exits shorter than entrances; linear is for non-spatial or looping motion. Measured in Chrome: open state computes to 0.15s cubic-bezier(0, 0, 0.2, 1) and the closed state to 0.1s cubic-bezier(0.4, 0, 1, 1); the typed reveal is steps(24). Whether stepped easing on a revealed width counts as spatial linear motion is not settled by the rule; steps() is not "linear", so the rule check passes.
- Satisfies: craft-motion-easing-direction
- Verification note: Durations and curve directions match the sources; the treatment of steps() under the rule is our reading.
```css
.win { transition: transform 100ms cubic-bezier(.4, 0, 1, 1), opacity 100ms cubic-bezier(.4, 0, 1, 1); }
.win.open { transition-duration: 150ms; transition-timing-function: cubic-bezier(0, 0, .2, 1); }
.typed { animation: type 1.2s steps(24, end) 1 both; }
```
### OS window chrome from real controls (`rc-os-window`) [standard · verified]
Make OS-window chrome out of real controls: buttons with accessible names ("Close window", not an X glyph alone), at least 44 px square, with a visible focus outline, inside a labelled dialog or region.
- How: Tiny title-bar buttons are the usual retro-computing target-size failure. Chrome demo: the close button is a button with aria-label "Close window", measures at least 44 by 44 px once its open transition finishes and shows a solid 3px outline on keyboard focus. WCAG 2.5.8 requires 24 by 24 px or spacing.
- Satisfies: a11y-focus-visible, a11y-target-size, a11y-name-role-value

# Recipe: No photography exists (physical goods or services): the offer as the live object, type as image, or an honest gap (`no-photography-physical-goods`)
Styles covered: no-imagery, ecommerce-store, consumer-goods, specimen, professional-services, business-services
**Keep:** A first object made of real controls and real numbers; type set large as real text; tables and run sheets with specific rows; an honest, listed gap.
**Avoid:** Shape-assembled drawings of the product; stock or placeholder images; emoji icons; a decorative texture that starts to depict the product; unconfirmed prices or hours shown as facts; claiming the live object replaces photographs for a pieces-only shop.
When no photographs exist (a physical product with no photos yet, or a service with none you can use), do not draw the subject from shapes and do not use stock. Make the offer itself the live object when it has state (price, seats, slots, dates, a calculator, a booking control or self-check), let a large measurement, price or fact be the image, present the catalogue or fee table as a menu or run sheet where there are rows to list, or leave the imagery out and mark the gap, and plan the real photographs. For a service, np-offer-live-object applies when there is state to show, np-type-as-image and np-mark-the-gap always apply, np-menu-and-run-sheet only when the service has rows to list, and np-pieces-only-limit is for goods.
**While designing:** No photos (goods or a service)? Build the offer as the live object with native controls when it has state (or set the key fact, measurement or price large as real text), show a fee table or catalogue as a table or run sheet when there are rows, mark the photograph gap in OPEN-QUESTIONS.md, and never draw the subject from shapes in code. Services: skip the pieces-only limit; the menu step only if there are rows to list.
## Steps
### Make the offer the first object (`np-offer-live-object`) [our-take · judgement]
When the offer has state to show (seats left, time slots, dates, sizes, bundles, a price that changes with a choice), make the offer itself the first object on the page: a booking or price control built from real HTML controls with real numbers and real states, placed where a product photo would normally sit.
- How: In the pilot, a ceramics studio selling six seats at a stated price per workshop used a ring of six native checkboxes that totals the price and writes the booking email, instead of a photograph. It works because the offer is seat-limited; it does not work for a pieces-only shop, which has no state to show (see np-pieces-only-limit). The numbers on the page must be the owner's: mark any you do not have with the assumption marker from the protocol (3.2). For a service: it applies when the service has state to show (free slots, a waiting time, opening hours, a self-check or calculator); a self-check was the live object in a tenant-rights advice pilot. If the service has no state, use np-type-as-image.
- Satisfies: distinct-real-imagery-and-icons, distinct-hero-not-template
- Verification note: Derived from one pilot (a model designing a ceramics-studio homepage on the lean track); no user was shown the page and no conversion was measured. Only structural checks were run (no img, svg or canvas, no emoji).
### Live object from native controls (`np-live-object-accessible`) [standard · partly-verified]
Build the live object from native controls (checkbox, radio, select, button, number input) with visible labels, a fieldset and legend for a group, keyboard operation for free, and a total that updates in an output element so the change is announced without moving focus. State is never carried by colour alone: selected seats also differ by fill, ring or text.
- How: WCAG 4.1.3 asks that status messages can be announced without taking focus; the Understanding page lists role=status and live regions as the techniques. Using native controls follows the ARIA practice 'no ARIA is better than bad ARIA'. Not measured with a screen reader here: test it with VoiceOver or NVDA before launch.
- Satisfies: a11y-native-first, a11y-name-role-value, a11y-status-messages
- Verification note: The requirement (status messages announced without focus) was read in the WCAG Understanding page. The markup pattern is general engineering knowledge and was not tested with a screen reader.
```html
<fieldset>
  <legend>Pick your seats</legend>
  <label><input type="checkbox" name="seat" value="1"> Seat 1</label>
  <label><input type="checkbox" name="seat" value="2"> Seat 2</label>
</fieldset>
<p>Total: <output id="total">0</output> <!-- price per seat: the owner's number, or marked unconfirmed --></p>
```
### Let type carry the image (`np-type-as-image`) [craft-consensus · partly-verified]
Let type carry the image: set a measurement, a date, a price, a capacity or a name large as the visual, in the display face, as real text. Never export the type as an image.
- How: WCAG 1.4.5 (images of text) is the reason it stays real text: it resizes, reflows and can be read by assistive technology. Which fact to set large is a design judgement: choose the one that answers the visitor's first question about the product (how big, how many, how much, when).
- Satisfies: distinct-real-imagery-and-icons, a11y-images-of-text, distinct-display-font-chosen
- Verification note: The images-of-text requirement was read in the WCAG Understanding page. That type can stand in for a product image is our design judgement, with no study behind it.
### Catalogue as a table or list (`np-menu-and-run-sheet`) [our-take · judgement]
Present the catalogue, price list or run sheet as a menu: a real table or definition list with one row per item (name, size or detail, price, availability, how to get it) in plain text. Vary the structure of the sections below the hero: a run sheet in one, a price list in another, a measurements table in a third.
- How: Specific rows (a size, a price, a firing or delivery time) inform the way a photograph would, and a list is not an image-card grid. Each figure must be a fact the owner gave or be marked unconfirmed. Judgement: whether visitors who buy by looking accept a text catalogue is not tested here. For a service: use it only when there are rows to list (a fee table, opening hours, the steps of a process); in the advice pilot it did not fit.
- Satisfies: copy-specific-over-abstract, ux-informative-imagery, distinct-no-identical-card-grid
- Verification note: Derived from one pilot (a model designing a ceramics-studio homepage on the lean track); no user was shown the page and no conversion was measured. Only structural checks were run (no img, svg or canvas, no emoji).
### Mark the missing photography (`np-mark-the-gap`) [our-take · judgement]
If none of the above fits, leave the imagery out and mark the gap: in the design notes and in design/OPEN-QUESTIONS.md write that photographs are missing, which shots are needed, and that the page is not finished without them. Do not use a placeholder host, a stock demo image, an emoji, or a picture of the product assembled from shapes in code.
- How: A faint decorative gradient or texture that does not depict the product is ornament and the rule does not flag it. One that starts to depict the product (grooves that read as a pottery wheel, a glaze, a bowl) is an illustration: remove it or commission it as a file. The rule's detector flags hero-sized inline SVG scenes assembled from primitives; a drawn bowl or cross-section is that.
- Satisfies: distinct-real-imagery-and-icons, copy-no-placeholder-text
- Verification note: Derived from the wording of `distinct-real-imagery-and-icons` and one pilot. The line between ornament and illustration is a judgement call and is not measured.
### Plan the photo shot list (`np-commission-later`) [our-take · judgement]
Plan the real photographs: a shot list (hero object, scale, detail, in use), who takes them, licence and alt text, reserved width and height for each image slot, and the likely LCP image set with fetchpriority high and not lazy-loaded when it arrives. Put the plan in assets and in OPEN-QUESTIONS.md.
- How: Reserving dimensions now prevents layout shift later; alt text describes what the photograph conveys in context. The shot list is our suggestion, not a tested checklist.
- Satisfies: craft-image-dimensions-reserved, a11y-alt-text
- Verification note: A planning step, not a measured technique.
### Limits when selling single pieces (`np-pieces-only-limit`) [our-take · judgement]
If the business sells individual pieces and the offer has no state to show (no seats, slots or sizes to choose), the live object cannot replace a photograph. Say so in the notes, use the menu form and type as image, and record the missing photographs as the main launch risk.
- How: The pilot's own conclusion: the live object worked only because the studio sold a seat-limited class. People often buy a piece by looking at it, so a page without images may read as unfinished; this is a risk to state to the owner, not a measured effect. This step is for goods. A service has its own version of the problem only when nothing about it can be shown as state or as a fact; then use np-type-as-image and np-mark-the-gap, and photographs of people need their consent.
- Satisfies: distinct-real-imagery-and-icons, copy-proof-verifiable
- Verification note: Derived from one pilot (a model designing a ceramics-studio homepage on the lean track); no user was shown the page and no conversion was measured. Only structural checks were run (no img, svg or canvas, no emoji).

# Recipe: Urgent help routes on public-service and crisis pages: the emergency line once, a real phone route with hours, and the primary action still on the first screen (`urgent-help-route`)
Styles covered: government-public, non-profit, medical, mental-health
**Keep:** One short urgent band, first in reading order; a visible phone number that is a tel: link; hours as text and a stated out-of-hours route; the emergency-services line written once; the primary action inside the first phone screen.
**Avoid:** Red as the only signal; the emergency line repeated in every section; a sticky or modal urgent bar that covers content or focus; a pop-up, a timer or an auto-opening chat; a phone number only as an image; hours or numbers the owner has not confirmed shown as facts; labels such as 'crisis escalation' that the reader would not use.
For audiences who may be in danger, in debt, ill or facing a deadline, put the urgent route where it is read first, but keep it small. State the emergency-services boundary once, give a phone number as a tel: link with its hours and an out-of-hours route, carry the meaning in words, a border and position rather than red alone, and measure that the band does not push the page's primary action below the first screen at 390x844. Use plain labels in the reader's words.
**While designing:** Public-service or crisis page: put one compact urgent band first (the emergency-services line once, the phone number as a tel: link with hours and an out-of-hours route, meaning carried by words and a border, not red alone), use plain labels, and screenshot 390x844 to confirm the primary action is still on the first screen.
## Verified palette: Urgent band, computed (WCAG 2 relative luminance); the colours are an example, the cue is the text, the border and the position
- page-background: #FAFAF7
- band-background: #FFE08A
- band-text: #1B1B1B
- band-link: #6B4A00
- band-border: #7A4F00
| Pair | Foreground | Background | Ratio | Minimum |
|---|---|---|---|---|
| band text on band background | #1B1B1B | #FFE08A | 13.35:1 | 4.5:1 |
| band link on band background | #6B4A00 | #FFE08A | 6.25:1 | 4.5:1 |
| band border on page background (UI) | #7A4F00 | #FAFAF7 | 6.82:1 | 3:1 |
## Steps
### Urgent route first in order (`uh-first-in-order`) [our-take · judgement]
Decide the one urgent route for this audience and put it first in reading order, before the page's main content, as a short band: one heading, one or two sentences, one phone link. Put the page's primary action directly after it. The urgent route is not the page's primary action unless the service itself is a helpline.
- How: Code order equals reading order, so a screen-reader or keyboard user meets the route first and a sighted reader meets it first too. Keep it to a band, not a section, so it does not take over the page. Which route comes first (the emergency line, the helpline, the service's own number) is the owner's call and depends on the service.
- Satisfies: a11y-meaningful-sequence, ux-primary-cta-above-fold, ux-purpose-clear
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern.
### State emergency boundary once (`uh-emergency-boundary-once`) [our-take · judgement]
State the emergency-services boundary once, in plain words, at the top: say who to call if someone is in danger now (for example 'If someone is in danger now, call 999, the emergency services') and that this service is not one. Do not repeat it in every section or in the footer. 999 is the UK number and an example: the owner must confirm the number for the service's country (112, 911 ...).
- How: Said once, the line is read and acted on; repeated, it dilutes the page, frightens people who are not in danger and is read aloud again at every repeat by a screen reader. Whether the boundary line is also legally or professionally required for this service is for the owner to confirm. This is a design judgement, not a tested result.
- Satisfies: a11y-coga-plain-literal-language, copy-tone-fits-context, copy-proof-verifiable
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern.
### Phone number as a tel link (`uh-phone-tel-link`) [craft-consensus · partly-verified]
Show the phone number as real text inside a tel: link whose visible text includes the number and a verb ('Call us: 020 7946 0000'), at least 44 by 44 CSS px, with the country code in the href. Show the same number as text on desktop, where there may be no calling app.
- How: The visible text is the accessible name, so voice-control users can say what they see (label in name). The tel: scheme is standard HTML; a desktop browser with no calling app may do nothing, which is why the number stays visible as text. Not tested on real phones here. The number in the example is from the UK range set aside for fiction; the owner's number, or the visible assumption marker (protocol 3.2) until it is confirmed, goes in its place.
- Satisfies: a11y-link-purpose, a11y-label-in-name, a11y-target-size, a11y-coga-visible-help-contact
- Verification note: The accessible-name and target-size requirements are WCAG 2.5.3 and 2.5.8 (quick reference); the markup is ordinary HTML. No phone, desktop-without-app or voice-control test was run.
```html
<section class="urgent" aria-labelledby="urgent-title">
  <h2 id="urgent-title">If someone is in danger now</h2>
  <p>Call 999 for the emergency services. We are not an emergency service.</p>
</section>
<p class="phone"><a href="tel:+442079460000">Call us: 020 7946 0000</a></p>
<p>Monday to Friday, 9am to 5pm. Outside those hours, use <a href="#callback">the call-back form</a> and we reply the next working day.</p>
```
### Hours and out-of-hours route (`uh-hours-and-out-of-hours`) [our-take · judgement]
Write the opening hours as text next to the number and say what to do outside them: another number, a form with the reply time, or where to leave a message. Promise only a reply time the service keeps. Hours, reply times and numbers the owner has not confirmed carry the visible assumption marker (protocol 3.2) and are listed in OPEN-QUESTIONS.md.
- How: A phone line that is closed with no other route is a dead end for a person in a hurry. A live 'open now' badge from JavaScript is optional and must not replace the text, because the core content has to work without JavaScript.
- Satisfies: copy-proof-verifiable, a11y-coga-visible-help-contact, copy-specific-over-abstract
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern.
### Urgency beyond red alone (`uh-not-red-alone`) [standard · partly-verified]
Carry the urgency in words, position and a border, not in red alone. The band starts with a plain sentence, has a visible border, has text at 4.5:1 and its boundary at 3:1 (check with check_contrast, role text and ui), and keeps its meaning in forced-colors mode and for a reader who cannot tell the colour. Keep red for errors so the two do not mean the same thing.
- How: WCAG 1.4.1 says colour is never the only way to show information. The palette above is computed with the WCAG 2 formula; amber is an example, not a requirement. The band's text works on its own, so removing the colour loses nothing.
- Satisfies: a11y-color-not-only, a11y-contrast-text, a11y-non-text-contrast
- Verification note: The requirement was read in the WCAG Understanding page and the ratios were computed. How the band reads under forced colors or to people with colour-vision differences was not tested.
### Band and action above the fold (`uh-stack-above-fold`) [our-take · judgement]
Stack the band with the primary action and check it at 390x844: the primary action's bottom edge must be inside the first viewport. Keep the band compact (a heading and one line, or one line with the phone link), do not make it sticky or a full-height overlay, and trim the page's own heading before the band if they compete. If the action still falls below, shorten the band before you shrink the action.
- How: A sticky or fixed bar costs the first screen on every scroll position and can cover focused elements (WCAG 2.4.11). Measure, do not guess: the audit's primary-action check and a screenshot at 390x844 both work. In the pilot an amber band took about a quarter of the phone's first screen and put the main button at 858 px, below the 844 px fold; the audit found it and the layout was changed. Any height budget (for example 'a fifth of the viewport') is our rule of thumb, not a standard.
- Satisfies: ux-primary-cta-above-fold, a11y-focus-not-obscured, ux-false-floor
- Verification note: Derived from one fictional-service pilot (a model designing a homepage for a UK tenant-rights advice service on the sprint track) and general practice; no user, screen-reader or phone test was run on the pattern. The snippet measures one element's box; it does not replace looking at the screenshot.
```js
// run in the page at a 390x844 viewport
const b = document.querySelector('[data-primary-action]').getBoundingClientRect();
console.log(b.bottom <= innerHeight ? 'primary action is in the first screen' : 'primary action is BELOW the fold by ' + Math.round(b.bottom - innerHeight) + ' px');
```
### Labels in the reader's words (`uh-plain-labels`) [craft-consensus · partly-verified]
Write every label in the reader's words and in plain language: 'Call us', 'Call 999 if someone is in danger now', 'I have been given an eviction notice', not 'Crisis escalation', 'Urgent triage' or the service's internal names. Put the verb first, spell out acronyms, state what a call costs if the reader may have to pay, and aim at the lower reading target for stressed, ESL or low-literacy readers (see copy-reading-grade).
- How: People under stress read less and take in less (the COGA guidance lists stress and low literacy among the groups it covers); plain, literal wording is the cheapest fix. No reading test was run on the example wording.
- Satisfies: copy-button-verb-label, copy-plain-words, a11y-coga-plain-literal-language, copy-jargon-acronyms
- Verification note: The wording guidance follows the plain-language and COGA sources behind the cited rules; the examples were not read-tested with real readers.
### No pop-ups for the urgent route (`uh-no-interruptions`) [our-take · judgement]
Keep the urgent route in the page, not in a pop-up, a timed banner, a modal or an auto-opening chat. It exists in the HTML at load, does not move, and does not take focus.
- How: A person in distress should not have to dismiss something to reach the content, and a banner that disappears on a timer can vanish before it is read. This is an application of the cited rules, not a measured result.
- Satisfies: a11y-coga-limit-interruptions, a11y-coga-no-surprise-changes, comp-alert-no-focus-no-autodismiss
- Verification note: Applies the cited rules to this case; not measured.
### Observed example, not verified (`uh-observed-example`) [our-take · judgement]
Observed example only, not verified: the pilot for a fictional UK tenant-rights service put a flat amber band above a board of five first-person situations ('What is happening to you?'), with the 999 line once and the service's phone number as a link, and a call-back form below. Use it as one shape to compare against, not as the answer.
- How: The pilot's own account: the band was the first thing on the page, the five rows were the primary action, and the phone-first screenshot needed a change after the audit found the button below the fold. No person looked at the page, nobody called the number, and the advice text was a draft that lawyers had not checked. Whether this shape helps people in distress is untested.
- Satisfies: ux-primary-cta-above-fold, a11y-color-not-only
- Verification note: One pilot, one model, no users.

# Recipe: Forms with no backend: a mailto fallback, an honest success message, a privacy line and a rule for sensitive text (`form-no-backend-and-privacy`)
Styles covered: government-public, professional-services, local-community, non-profit
**Keep:** Visible labels; native required, type, inputmode and autocomplete; a working form with JavaScript off; a success message that says what really happened; a privacy line of five short facts; a phone link beside the form.
**Avoid:** Claiming 'Message sent' when only a mail app was opened; placeholder text as a label; a type=number phone field; asking for bank, ID or health details in free text; an example email address shipped as real; moving focus onto the error message; a privacy line that promises something the owner has not confirmed.
A small site with no server can still offer a callback or enquiry form: native fields with native required as the no-JS fallback, a mailto: form action, and JavaScript that validates and then opens a prefilled email. Say plainly that nothing is sent until the visitor presses send in their mail app and that email is not private. Put a short privacy line next to the button, tell people not to write bank details in a free-text box, show errors and success as text in live regions, and offer a phone number as another route.
**While designing:** No backend? Use a native form with required as the no-JS fallback, a mailto: action and JS that validates then opens a prefilled email, plus a phone link; say that nothing is sent until the user presses send and that email is not private; add a five-part privacy line and 'do not write bank details here'; show errors and success in live regions without moving focus onto them; set type=tel, inputmode and autocomplete.
## Steps
### Native single-column fields (`fp-native-fields`) [standard · partly-verified]
Build the form from native fields in one column: a visible label above each, a fieldset with a legend for radio groups, native required, and the right type, inputmode and autocomplete tokens: name (autocomplete="name"), phone (type="tel" inputmode="tel" autocomplete="tel"), email (type="email" autocomplete="email"), postcode (autocomplete="postal-code"). Three required fields at most. Never use a placeholder as the label, and never type=number for a phone number.
- How: WCAG 1.3.5 asks that fields collecting personal data declare their purpose with autocomplete; 3.3.2 asks for labels or instructions. type=tel and inputmode=tel bring up the phone keypad; type=number would add spinners and drop leading zeros. The tokens are HTML autofill tokens; check them in a browser, which is not done here.
- Satisfies: a11y-input-purpose, a11y-labels-instructions, ux-form-no-placeholder-label, ux-form-layout, ux-form-length, comp-checkbox-radio-group-labels, a11y-coga-visible-help-contact
- Verification note: The requirements were read (the labels-instructions Understanding page); the autocomplete and inputmode values are standard HTML and were not tested on devices. The example address is an example domain: replace it with the owner's real address, or mark it with the visible assumption marker until it is confirmed.
```html
<form id="callback" action="mailto:owner@example.org" method="post" enctype="text/plain" novalidate>
  <p id="form-error" role="alert"></p>
  <label for="name">Your name</label>
  <input id="name" name="name" autocomplete="name" required>
  <label for="phone">Phone number</label>
  <input id="phone" name="phone" type="tel" inputmode="tel" autocomplete="tel" required>
  <label for="msg">What is happening (optional)</label>
  <p id="msg-hint">Do not write bank details, passwords or ID numbers here.</p>
  <textarea id="msg" name="message" aria-describedby="msg-hint"></textarea>
  <p id="privacy">...</p>
  <button>Ask us to call you</button>
</form>
```
### Mailto form as no-JS fallback (`fp-mailto-fallback`) [our-take · judgement]
With no backend, use the native form as the no-JS fallback: action="mailto:...", method="post", enctype="text/plain", with native required on the fields. Layer JavaScript on top: on submit, validate, then build a mailto: link with the subject and body encoded (encodeURIComponent) and open it. Beside the form always show the phone link and the plain email address as other routes. Keep the body short: some mail apps cut a very long mailto: link (not measured here).
- How: The form works with JavaScript off because the browser's own required and mailto: handling remain; JavaScript adds nicer validation and a readable prefilled body. mailto: depends on the visitor having a mail app set up (a webmail-only user may get nothing), so the phone link and the written email address are not optional extras. The core content works without JavaScript, as the guide requires.
- Satisfies: perf-core-first, a11y-coga-visible-help-contact
- Verification note: Derived from one pilot (the fictional tenant-rights service) and general practice. The mailto: handoff was not opened in a real mail app in the pilot, and no cross-client behaviour was measured.
```js
form.addEventListener('submit', (e) => {
  e.preventDefault();
  if (!validate(form)) return; // fills #form-error, focuses the first invalid field
  const body = [...new FormData(form)].map(([k, v]) => k + ': ' + v).join('\n');
  location.href = 'mailto:owner@example.org?subject=' + encodeURIComponent('Call-back request') + '&body=' + encodeURIComponent(body);
  status.textContent = 'Your email app should open with your message ready. Nothing is sent until you press send there. If it does not open, call 020 7946 0000.';
});
```
### Honest mailto success message (`fp-honest-success`) [standard · partly-verified]
Never write 'Message sent' or 'Thank you, we have your request' for a mailto: form. Say what really happened in a role=status region that exists empty at load: your email app should open with the message ready; nothing is sent until you press send there; if it does not open, here is the phone number and the email address. Say the same on the page before submit, in one line next to the button.
- How: WCAG 4.1.3 asks that status messages are announced without taking focus; the Understanding page names role=status as a technique, and an empty live region that already exists is announced more reliably than one inserted with its text. The honest wording is our design judgement; it protects people from believing a request was made when it was not.
- Satisfies: a11y-status-messages, a11y-status-role-choice, comp-live-region-exists-before-content, a11y-coga-action-feedback, copy-proof-verifiable
- Verification note: The status-message requirement was read in the WCAG Understanding page. How screen readers announce this exact region was not tested.
### Errors next to fields, with summary (`fp-error-pattern`) [our-take · judgement]
Show each error as text next to its field, say what is wrong and how to fix it, keep what the user typed, and use more than colour (an icon or the word 'Error' and a border). Put a summary in the role=alert region that exists empty at load, fill it on a failed submit, do not call focus() on it, and move focus to the first invalid field. Errors stay until fixed. Native required alone gives browser-styled bubbles that vary by browser, so validate with your own text when JavaScript runs.
- How: This resolves a tension between comp-alert-no-focus-no-autodismiss (do not move focus to a message) and the common error-summary pattern that moves focus to the summary: the summary is announced by the live region, and focus goes to the first field that needs fixing. Resolution is our judgement; it was used in one pilot and not tested with a screen reader.
- Satisfies: a11y-error-identification, copy-error-specific-actionable, ux-form-errors, a11y-color-not-only, comp-alert-no-focus-no-autodismiss, comp-live-region-exists-before-content
- Verification note: Our resolution of a rule tension; one pilot, no screen-reader test.
### Five-question privacy line (`fp-privacy-line`) [our-take · judgement]
Put a short privacy line next to the button, answering five questions in plain words: what we ask for, why, who sees it, how long we keep it, who to contact. Name the law only as an example of what applies (for example 'UK GDPR' for a UK service) and say that the owner must confirm which law, which legal basis and which retention period apply: this is not legal advice. Link to the full privacy notice if one exists. For the mailto: route add that email is not private on its way.
- How: Example copy for the owner to confirm: 'We use your name and phone number only to call you back about your case. Two advisers can see them. We delete them after 30 days. Questions: privacy@example.org. By email, your message is not private on the way.' The 30 days, the two advisers and the address are placeholders to confirm; until the owner confirms them they carry the visible assumption marker, and a lawyer or data-protection adviser should check the final wording before launch.
- Satisfies: copy-proof-verifiable, a11y-labels-instructions, copy-expert-review-before-launch
- Verification note: A drafting pattern, not legal advice and not a compliance claim. No lawyer reviewed it.
### Warn against sensitive free text (`fp-sensitive-free-text`) [our-take · judgement]
Rule of thumb for a free-text box: do not ask for sensitive data you do not need, and tell people what not to write directly under the label ('Do not write bank details, passwords or ID numbers here'), tied to the field with aria-describedby. Ask for health, immigration, financial or identity details only if the service cannot work without them, and then in a channel the owner has chosen for it, not in an email.
- How: With a mailto: form everything typed goes by ordinary email, which is not private and stays in two mailboxes. The cheapest protection is not to collect it. The wording is plain on purpose, so low-literacy and ESL readers can follow it.
- Satisfies: ux-form-length, a11y-labels-instructions, a11y-coga-plain-literal-language
- Verification note: A rule of thumb from the pilot and general privacy practice; not tested.
### No example domains as real addresses (`fp-no-example-addresses`) [our-take · judgement]
Do not ship example domains (example.org, .example) as real addresses. Until the owner supplies the real address and phone number, show them with the visible assumption marker (protocol 3.2), list them in OPEN-QUESTIONS.md, and let realize-launch stop the release.
- How: A form that opens an email to a dummy address looks finished and sends nothing; this is the form case of the guide's rule against invented facts.
- Satisfies: copy-proof-verifiable, copy-no-placeholder-text
- Verification note: Applies the guide's launch gate to forms.




# Principles
Paraphrased from the cited sources. Use them as lenses, with their evidence labels.

## good-design
- **Good design is innovative** [craft-consensus]: Innovation grows with technology and is never pursued for its own sake. Apply: Use a new technique only where it serves the message. Check: Can you state what the new technique gives the visitor? (sources: rams-ten-principles)
- **Good design makes a product useful** [craft-consensus]: A product meets functional, psychological and aesthetic needs, without distractions. Apply: Cut elements that do not help the visitor's job. Check: Does each element serve the primary action or a stated need? (sources: rams-ten-principles)
- **Good design is aesthetic** [craft-consensus]: Everyday objects shape well-being, so how they look matters, and beauty depends on quality of execution. Apply: Spend effort on alignment, spacing and detail. Check: Are spacing, alignment and type consistent with the tokens? (sources: rams-ten-principles)
- **Good design makes a product understandable** [craft-consensus]: Its structure should be clear, ideally needing no explanation. Apply: Make the page's purpose and next step obvious without instructions. Check: Five-second test: can people say what it is and what to do? (sources: rams-ten-principles)
- **Good design is unobtrusive** [craft-consensus]: Products are tools: restrained, leaving room for the user. Apply: Keep decoration from competing with content. Check: Does motion or ornament compete with the headline or the action? (sources: rams-ten-principles) Tension with styles: maximalist, experimental
- **Good design is honest** [craft-consensus]: A product does not claim more innovation, power or value than it has. Apply: Make claims you can support; show proof. Check: Is every claim backed by a fact on the page? (sources: rams-ten-principles)
- **Good design is long-lasting** [craft-consensus]: Avoiding trends keeps a design from looking dated. Apply: Use a trend as one element with a reason; keep structure and type timeless. Check: If the trend disappears, does the design still work? (sources: rams-ten-principles)
- **Good design is thorough down to the last detail** [craft-consensus]: Nothing is left to chance; care shows respect for the user. Apply: Design states, errors, empty cases and edge widths. Check: Are hover, focus, error, empty and small-screen states designed? (sources: rams-ten-principles)
- **Good design is environmentally friendly** [craft-consensus]: It conserves resources and reduces pollution across its life. Apply: Keep pages light: fewer bytes, fewer requests, no pointless autoplay. Check: Is the page weight within the budget set in assets? (sources: rams-ten-principles)
- **As little design as possible** [craft-consensus]: Focus on what is necessary and strip away the rest. Apply: Remove an element and see whether the page loses anything. Check: Could any section be removed without loss? (sources: rams-ten-principles) Tension with styles: maximalist

## heuristics
- **Visibility of system status** [evidence]: Keep users informed about what is happening with timely feedback. Apply: Show loading, success and error states. Check: Does every action give feedback quickly? (sources: nng-ten-heuristics)
- **Match between system and the real world** [evidence]: Use the users' language and conventions, not internal jargon. Apply: Use the audience's words in labels and headlines. Check: Would a first-time visitor understand each label? (sources: nng-ten-heuristics)
- **User control and freedom** [evidence]: Provide clear exits for unwanted actions. Apply: Offer cancel, back and undo where actions are costly. Check: Can the visitor leave every state? (sources: nng-ten-heuristics)
- **Consistency and standards** [evidence]: Words and actions mean the same thing throughout; follow conventions. Apply: Reuse components and labels; follow platform conventions. Check: Do identical functions look and read the same everywhere? (sources: nng-ten-heuristics)
- **Error prevention** [evidence]: Prevent problems or confirm before users commit. Apply: Use constraints, defaults and confirmations for costly actions. Check: Can the visitor make a costly mistake without warning? (sources: nng-ten-heuristics)
- **Recognition rather than recall** [evidence]: Make options visible so people need not remember them. Apply: Show choices; avoid hidden gestures and hover-only options. Check: Does anything require remembering what is not on screen? (sources: nng-ten-heuristics)
- **Flexibility and efficiency of use** [evidence]: Let experts speed up tasks while novices stay supported. Apply: Provide shortcuts that supplement visible controls. Check: Is there a fast path that does not hide the slow one? (sources: nng-ten-heuristics)
- **Aesthetic and minimalist design** [evidence]: Remove information that competes with what matters. Apply: Focus visuals on the primary goal. Check: Does extra content distract from the primary action? (sources: nng-ten-heuristics)
- **Help users recognize, diagnose and recover from errors** [evidence]: Error messages explain the problem and suggest a fix. Apply: Write errors in plain language with a next step. Check: Does each error say what happened and how to fix it? (sources: nng-ten-heuristics)
- **Help and documentation** [evidence]: The system should need little explanation, but help should be easy to find. Apply: Put help in context and make it searchable and task-focused. Check: Can the visitor find help from where they are stuck? (sources: nng-ten-heuristics)

## discoverability
- **Discoverability and understanding** [craft-consensus]: Two key qualities of good design: people can find out what actions are possible, and understand how it works. Apply: Make actions visible and meaning clear. Check: Can a new visitor find and understand the main action? (sources: norman-design-of-everyday-things)
- **Signifiers show where action is possible** [craft-consensus]: Affordances define what is possible; signifiers tell people where and how. Apply: Make links and buttons look and read as such. Check: Is every clickable element signalled, and is anything signalled that is not clickable? (sources: norman-design-of-everyday-things)
- **Feedback** [craft-consensus]: Communicate the result of an action clearly and promptly. Apply: Show a response to every action. Check: Is there a visible response within a moment of each action? (sources: norman-design-of-everyday-things)
- **Conceptual model** [craft-consensus]: People form a simple mental model of how something works; design should support an accurate one. Apply: Keep structure and wording consistent with one clear model. Check: Can the visitor explain how the site is organized? (sources: norman-design-of-everyday-things)

## process
- **Observe, ideate, prototype, test, repeat** [craft-consensus]: Human-centered design iterates observation, idea generation, prototyping and testing. Apply: Loop the process; do not treat it as linear. Check: Has each stage fed back into the previous one at least once? (sources: norman-design-of-everyday-things)

## accessibility
- **Perceivable** [standard]: Information and interface components can be perceived by users. Apply: Provide text alternatives, captions, adaptable content and sufficient contrast. Check: Run the perceivable Quality Bar rules. (sources: w3c-wai-pour)
- **Operable** [standard]: Interface components and navigation can be operated, including by keyboard. Apply: Everything works by keyboard; allow enough time; avoid seizure triggers; make navigation easy. Check: Tab through the page. (sources: w3c-wai-pour)
- **Understandable** [standard]: Information and operation are understandable: readable, predictable, with help avoiding mistakes. Apply: Use plain language, predictable behavior and clear errors. Check: Is behavior predictable and are errors explained? (sources: w3c-wai-pour)
- **Robust** [standard]: Content works with current and future tools, including assistive technology. Apply: Use native HTML and correct names, roles and values. Check: Does the accessibility tree match what is shown? (sources: w3c-wai-pour)

## inclusion
- **Recognize exclusion** [craft-consensus]: Acknowledge bias and notice where products fail because of mismatches between people and experiences. Apply: List who the design could exclude. Check: Is there a written list of who might be excluded and what the design does about it? (sources: ms-inclusive-design)
- **Learn from diversity** [craft-consensus]: Keep people at the centre; varied perspectives produce insight. Apply: Include people with different abilities in research. Check: Were different users consulted? (sources: ms-inclusive-design)
- **Solve for one, extend to many** [craft-consensus]: Designing for people with permanent disabilities benefits everyone. Apply: Treat accessibility needs as design constraints that improve the product. Check: Which accessibility feature also helps everyone? (sources: ms-inclusive-design)

## service
- **Start with user needs** [craft-consensus]: Research users and data first; what people ask for is not always what they need. Apply: Write the need before the solution. Check: Does the brief cite evidence about users? (sources: govuk-design-principles)
- **Do the hard work to make it simple** [craft-consensus]: Make it genuinely easy to use even when the underlying system is complex. Apply: Absorb complexity in the design, not in the visitor's effort. Check: Where does complexity land: on the page or on the visitor? (sources: govuk-design-principles)
- **Iterate, then iterate again** [craft-consensus]: Start small, test with real users, refine or scrap what does not work. Apply: Plan several small test rounds. Check: Is a second test round planned? (sources: govuk-design-principles)
- **This is for everyone** [craft-consensus]: Build inclusive, accessible services, especially for people who struggle most. Apply: Test with people who struggle most. Check: Have the hardest-case users been considered? (sources: govuk-design-principles)
- **Be consistent, not uniform** [craft-consensus]: Use shared language and patterns where possible, as guidance to be improved. Apply: Reuse patterns but adapt where users need it. Check: Are differences deliberate and explained? (sources: govuk-design-principles)

## perception
- **Proximity** [craft-consensus]: Elements close together are seen as a group. Apply: Group related items; separate unrelated ones with space. Check: Is spacing within groups smaller than between groups? (sources: gestalt-secondary, wertheimer-1923)
- **Similarity** [craft-consensus]: Elements that look alike are seen as related. Apply: Style items of the same kind the same way. Check: Do similar-looking items have similar roles? (sources: gestalt-secondary, wertheimer-1923)
- **Closure** [craft-consensus]: We complete incomplete shapes and perceive wholes. Apply: Use implied shapes carefully; avoid ambiguity. Check: Is any implied grouping accidental? (sources: gestalt-secondary, wertheimer-1923)
- **Good continuation** [craft-consensus]: We follow smooth paths and alignments. Apply: Align elements along clear lines to guide the eye. Check: Does the eye path follow the intended reading order? (sources: gestalt-secondary, wertheimer-1923)

## web
- **Layers: meaning, presentation, behavior** [craft-consensus]: Start from well-structured HTML everyone can use, then enhance by capability. Apply: Build core content first; layer effects on top. Check: Does content work with JavaScript off and CSS failing? (sources: keith-resilient-web-design)

## systems
- **Design parts and whole together** [craft-consensus]: Check components in the context of the page; revise parts when a page fails. Apply: Test components inside real pages. Check: Have components been reviewed in context? (sources: frost-atomic-design)

## layout
- **The grid is an aid, not a guarantee** [craft-consensus]: A grid supports order and readability; it does not make a design good. Apply: Use a grid to align, and break it with intent. Check: Is each break from the grid deliberate? (sources: muller-brockmann-swiss-style)




# Trends snapshot (2026-11)
Status is a judgement from a handful of pages, not data. Re-check before relying on it.

## webgl-3d-hero-and-scenes [peak, confidence medium for award sites, low for commercial sites]
Taxonomy: hero-3d, realtime-3d, 3d-rendered, creative-coding, interactive-art, scroll-triggered
- Evidence: Among the 31 Awwwards Sites of the Day from 2026-10-06 to 2026-11-05, 14 carry the Three.js tag, 11 the 3D tag and 10 the WebGL tag. Of the 31 Sites of the Year up to 2025-11-17, 19 carry 3D and 14 WebGL; the 2025 winner (Lando Norris, 2025-11-17) is tagged 3D, WebGL, GSAP. Commercial-side pages are more cautious: Framer Websites (2026-03-28) puts 3D and WebGL under 'approach with caution', Muzli's store page warns of an overuse wave, StudioMeyer (2026-09-30) says 3D/WebGL underdelivered for client work. So it is peak among award sites and cooling for ordinary commercial homepages. Based on a handful of pages, not data.
- Good for: Showcase and brand-led pages where the object is the product: automotive, hardware, games, agencies, portfolios, launches.
- Risks (rules): perf-lcp, perf-inp, perf-core-first, a11y-reduced-motion, a11y-pause-stop-hide, a11y-keyboard, a11y-pointer-gestures, a11y-dragging, a11y-images-of-text
- Do it well: Keep real text, nav and the primary call to action in HTML that paints without the 3D layer; lazy-load the scene after first paint; provide a static poster for reduced motion and for low-power devices; make rotation or drag operable by keyboard and by single tap; have the 3D show what the product is or does.
- The slop version to avoid: A floating abstract blob or glossy primitive behind a centred headline with a purple-blue gradient, loading 5+ MB before the headline appears, with no fallback.

## gsap-scroll-choreography [peak, confidence medium]
Taxonomy: scroll-triggered, page-transitions, long-scroll-narrative, chaptered-story, parallax, micro-interactions
- Evidence: 19 of the 31 latest Sites of the Day carry the GSAP tag, 21 carry Animation, 9 Storytelling, 8 Transitions (2026-10-06 to 2026-11-05). Sites of the Month: Storytelling 13, Scrolling 11, GSAP 10 of 31. Digidop (updated 2026-10-06) dates the enabling events: Webflow made GSAP free on 2025-04-30 and Figma Motion launched in June 2026, which makes it cheap, which is a saturation signal. Webflow (Dec 2025) frames the 2026 shift as scroll as navigation (progress indicators) rather than only narratives.
- Good for: Storytelling, portfolios, product walk-throughs, long editorial or launch pages where order carries meaning.
- Risks (rules): a11y-reduced-motion, a11y-pause-stop-hide, a11y-keyboard, a11y-focus-not-obscured, a11y-meaningful-sequence, ux-minimal-motion, perf-inp, perf-cls, perf-core-first
- Do it well: Content visible by default and enhanced by script, never hidden until a trigger fires; one authored sequence that reveals meaning in order; native scroll preserved (no scroll-jacking that traps wheel or keyboard); progress indicators for long pages; a reduced-motion path that shows everything statically.
- The slop version to avoid: The same fade-and-slide-up applied to every section, count-up stat tiles, bounce easing, and a marquee strip, with nothing explaining what changed.

## oversized-expressive-headline-type [peak, confidence medium]
Taxonomy: oversized-type, expressive-type, hero-type-only, text-effects, condensed
- Evidence: Named in Figma (bold typography), Framer Websites (bold typographic layouts, 2026-03-28), Line25 (oversized type as the hero, 2026-04), Webflow (dynamic text treatments), Muzli store (kinetic type is now an expected baseline rather than a differentiator), Muzli feed. Awwwards 'Typography' tag appears on 10 of 31 latest Sites of the Day but only 4 of 31 Sites of the Year. The Muzli store 'baseline' claim and the multi-source repetition point to peak.
- Good for: Brand-led and short-copy pages: studios, launches, cultural and editorial brands; hero that works with no image.
- Risks (rules): a11y-resize-text, a11y-reflow, a11y-text-spacing, a11y-images-of-text, a11y-reduced-motion, a11y-contrast-text, perf-cls
- Do it well: Real text (not images of text); fluid sizing with clamp that survives 200% zoom and 320 px width; tracking tightened only to the point letters keep their shape; short headings (the Impeccable detector flags headlines >= 72 px with >= 40 characters); balanced line breaks; kinetic effects only on a few words and with a static fallback.
- The slop version to avoid: A long full-sentence headline at 7rem+, with one italic or gradient-filled word, an all-caps tracked eyebrow above it, and a typewriter or rotating-word animation that never stops.

## serif-display-with-grotesk-pairing [peak, confidence medium (type), low (status of the AI-default part)]
Taxonomy: serif-editorial, serif-display, mixed-pairing, serif, grotesque, editorial
- Evidence: Typewolf Site of the Day, 45 entries from 2025-01-17 to 2025-12-14: by my reading of the font names about 26 pair a serif display (Cardinal, Editorial Old, Tobias, Arizona Flare, Martina Plantijn, GT Super and similar) with a neutral grotesk (Soehne, Neue Montreal, Founders Grotesk, Diatype). Webflow (Dec 2025) names vintage and classical art references as a trend. At the same time Capital & Compute and Impeccable name the cream + serif + terracotta combination and the italic serif hero as the second-wave AI default, and Google metadata ranks Fraunces 82 and Instrument Serif 79 by popularity. I read this as peak in curated design and saturated in generated sites. The Typewolf feed stops at 2025-12-14, so this is a 2025 snapshot.
- Good for: Editorial, cultural, hospitality, luxury, publications, studios, consultancies, DTC with a story.
- Risks (rules): a11y-contrast-text, a11y-resize-text, a11y-text-spacing, perf-lcp, perf-cls
- Do it well: Choose a serif with a reason tied to the subject (heritage, authorship, publication), pair it with a neutral grotesk for UI and body, keep one display voice, self-host with font-display swap and size-adjusted fallbacks, and state the pairing in the direction file.
- The slop version to avoid: Fraunces or Instrument Serif in italic as the hero headline on a cream background (#F4F1EA family) with a terracotta accent, a tracked mono eyebrow above and numbered section labels, for a product that has no editorial reason.

## monospace-detail-and-technical-labels [saturated, confidence low]
Taxonomy: monospace, utilitarian, retro-computing, mixed-pairing, developer-tools
- Evidence: Typewolf Site of the Day 2025: about 10 of 45 entries add a mono (DM Mono, Diatype Mono, Favorit Mono, Suisse Int'l Mono, Soehne Mono, Monument Grotesk Mono, GT Flexa Mono, Azeret Mono, GT Alpina Typewriter). Webflow (Dec 2025) and Muzli feed cite ASCII/pixel treatments. Impeccable has a rule against mono used only as a costume for 'technical' and a rule against decorative blinking cursors; Capital & Compute lists mono small labels and tracked eyebrows as template chrome. Saturation inferred from the Typewolf share plus the slop catalogues naming it, not measured.
- Good for: Data, code, specs, captions, measurements, timestamps, developer tools and products that really show code.
- Risks (rules): a11y-contrast-text, a11y-text-spacing, a11y-resize-text
- Do it well: Use mono where the content is code, data or measurement; keep tabular figures aligned; size at least 14 px for functional text (Impeccable flags functional text under 11 px).
- The slop version to avoid: Tiny uppercase mono eyebrows over every heading, 'A / B / C' meta strings, section numbers, and a fake blinking cursor in the hero.

## bento-and-modular-grids [peak, confidence low]
Taxonomy: bento-grid, saas-stack, asymmetric, product-screenshots
- Evidence: Listed by Line25, Framer Websites, Muzli feed and uiuxshowcase; StudioMeyer (2026-09-30) says it 'held up' for content prioritisation; the Reddit dataset ranks bento near the bottom of tells people complain about. Awwwards has no 'bento' tag, so I could not count it. Line25's 45% adoption figure is unsourced and not used. Several sources describe an anti-grid counter-trend (brutalist, broken-grid) as a reaction to its ubiquity. Peak, possibly turning saturated; low confidence.
- Good for: Product overviews with unlike content (UI shot, stat, quote, integration), dashboards-in-marketing, feature summaries on SaaS homepages.
- Risks (rules): a11y-reflow, a11y-meaningful-sequence, a11y-semantic-structure, ux-scannable-text, perf-cls
- Do it well: One cell per real piece of content (no empty tiles); tile size encodes importance; DOM order matches reading order; at 320 px collapse to one column in meaningful order; vary tile backgrounds with real imagery or product UI.
- The slop version to avoid: Six same-colour cards with a small icon and one line each, a decorative empty tile, all with the same radius and soft shadow.

## dark-first-with-one-saturated-accent [saturated, confidence medium]
Taxonomy: dark, high-contrast, neon, futuristic-tech, dark-cyber
- Evidence: Framer Websites (2026-03-28) and Line25 (2026-04) and Muzli feed list dark-first; StudioMeyer says dark mode 'held up' when fully checked. The 2025 Awwwards Site of the Year page lists palette #D2FF00 on #111112. At the same time Impeccable, wystack, Capital & Compute and the Reddit dataset name cyan-on-dark, purple glows and neon glows as top tells. Saturated as a default, still winning when motivated.
- Good for: Media-forward, gaming, music, developer, security and automotive brands; products used in low light.
- Risks (rules): a11y-contrast-text, a11y-non-text-contrast, a11y-color-not-only, a11y-focus-visible, a11y-flashes
- Do it well: Design the dark theme as its own system (not an inversion), keep body text at 4.5:1 or better, avoid pure black behind large white text for halation, and choose the accent from the subject; one theme per page unless a deliberate switch.
- The slop version to avoid: Near-black with cyan or violet glow, gradient text, radial halos and glass cards on every section.

## full-color-systems-and-vivid-palettes [emerging, confidence low]
Taxonomy: vibrant, pastel, neon, y2k, memphis-playful
- Evidence: Webflow (Dec 2025) calls it a shift from one accent colour to full colour systems; Figma lists vibrant saturated palettes (Y2K, 'dopamine design'); Muzli feed predicts a move away from beige but admits it is not yet widespread. In Awwwards data the 'Colorful' tag is on 9 of 31 Sites of the Month and 9 of 31 Sites of the Year but only 1 of 31 of the latest Sites of the Day, so award-site evidence is mixed. Several sources are predictions. Emerging, low confidence.
- Good for: Consumer, kids and family, food and drink, events, creative tools, brands whose identity is energy.
- Risks (rules): a11y-contrast-text, a11y-non-text-contrast, a11y-color-not-only, a11y-flashes
- Do it well: Define a named palette with roles and use every colour with a rule; verify pairings at 4.5:1 for text; keep one dominant hue; do not communicate state by colour alone.
- The slop version to avoid: A random rainbow gradient wash or mesh blob behind a centred hero, with pastel text on pastel backgrounds.

## brutalist-raw-and-cyberbrutalism [rising, confidence low]
Taxonomy: raw-brutalist, neo-brutalist, retro-computing, unconventional-layout, collage
- Evidence: Muzli store (cyberbrutalism: ASCII, pixel art, repurposed system UI), Line25 (brutalism and anti-design 'for authenticity'), Muzli feed (retro and brutalism as a reaction to AI-polished visuals), Figma (neo-brutalism and collage), StudioMeyer (a missed counter-movement, 'author's observations, not backed by independent data'). Awwwards: 'Experimental' on 7 of 31 latest Sites of the Day and 4 of 31 Sites of the Month. Impeccable treats hard offset shadows as a review prompt outside a real neobrutalist concept. Rising, from the repeated 'reaction to sameness' framing; low confidence.
- Good for: Studios, artists, independent publications, cultural institutions, developer tools with a rebellious voice. Not suggested for finance, healthcare or enterprise B2B (Muzli store).
- Risks (rules): a11y-contrast-text, a11y-focus-visible, a11y-reflow, a11y-meaningful-sequence, ux-conventional-layout, ux-visible-navigation
- Do it well: Keep structure and focus order intact under a deliberately raw surface; keep navigation findable; commit to one rule set (grid lines, type, one colour pair) and apply it everywhere.
- The slop version to avoid: Hard offset block shadows and thick black borders applied as a costume to an otherwise ordinary SaaS template.

## ownable-illustration-and-art-meets-ui [emerging, confidence low]
Taxonomy: illustration, hand-drawn, collage, vintage-print, character-mascot, product-screenshots
- Evidence: Webflow (Dec 2025) names two linked trends: proprietary visual systems (its example: illustrative visuals across Anthropic's site) and 'art converging with advanced UI' (vintage illustration, painted or ASCII backdrops behind product UI). Muzli feed (Prince Pal, 2026-01-18) lists narrative illustration replacing stock photos. Awwwards 'Illustration' tag: 2 of 31 latest Sites of the Day, 4 of 31 Sites of the Month, 7 of 31 Sites of the Year. Capital & Compute notes that the Anthropic-style warm editorial look has itself become an AI-default cluster. Emerging with a saturation risk.
- Good for: SaaS and AI products that want to look made by people, consumer brands, education, non-profits; any brand needing a recognisable image language.
- Risks (rules): a11y-alt-text, a11y-images-of-text, perf-lcp, ux-informative-imagery
- Do it well: Commission or draw a consistent illustration system; keep product UI readable as real, live text and screenshots; give meaningful images alt text and decorative ones empty alt; keep file weight low.
- The slop version to avoid: AI-generated plastic illustrations, stock 'diverse team' photos, or hero-sized SVG scenes built from circles and polygons.

## radical-brevity-and-tldr-overviews [emerging, confidence low]
Taxonomy: hero-type-only, minimal, editorial-feed, no-imagery, inform-educate
- Evidence: Webflow (Dec 2025) lists minimalism in copy and a TL;DR experience (pitch-deck-style overview in the nav) as two of its 8 trends. Muzli feed lists content-first layouts (2026-01-18). Awwwards 'Clean' tag appears on 12 of 31 latest Sites of the Day, 'Minimal' on 4. Impeccable catalogues an 'aphoristic cadence' copy tell, which shows that short punchy copy is itself becoming a template. One vendor source for the specific trend; emerging, low confidence.
- Good for: Complex B2B services, consultancies, fintech, anything with a clear value proposition that can be stated in a line, with the details one click deeper.
- Risks (rules): ux-purpose-clear, ux-tagline-specific, ux-front-load, ux-primary-cta-above-fold, a11y-semantic-structure
- Do it well: Say what it is in plain words in the first screen; offer a structured overview (what, for whom, proof, next step) with deeper pages behind it; make every remaining word load-bearing.
- The slop version to avoid: Manufactured contrast one-liners ('Not a feature. A platform.') repeated section after section, with no explanation of what the product does.

## glass-and-material-depth [saturated, confidence medium (that it has peaked), low (exact stage)]
Taxonomy: glassmorphism, claymorphism, dimensional, grain-noise, gradient-aurora
- Evidence: Muzli store (volumetrics: restrained glass, 3D hero objects, textured type; cites Apple Liquid Glass in iOS 26), Digidop (2025's glow becoming shader-based; Apple Liquid Glass dated 2025-06-09; advises one material effect per page), Line25 (glassmorphism 2.0 as a controlled return; peaked originally around 2021). Framer Websites (2026-03-28) says glassmorphism has peaked and hurts readability and rendering; StudioMeyer says it overpromised; Impeccable flags it when decorative; the Reddit dataset says people rarely name it. Multiple sources saying 'peaked' or 'use sparingly' suggest saturated, fading as a default.
- Good for: Overlays and navigation above imagery or video, premium consumer and OS-adjacent products, where depth must show layering.
- Risks (rules): a11y-contrast-text, a11y-non-text-contrast, perf-inp, perf-core-first
- Do it well: Use it on one or two functional surfaces; keep text at 4.5:1 against the worst-case content behind it; give a solid-fill fallback for reduced transparency and forced colors; test on mid-range phones.
- The slop version to avoid: Frosted cards with a glow border on every section over a purple-blue gradient.

## experimental-navigation [emerging, confidence low]
Taxonomy: unusual-nav, floating-dock, command-palette, hamburger-only, anchor-only
- Evidence: Figma (experimental navigation: radial menus, hidden drawers, interactive maps, nonlinear paths), Muzli store (nav that appears on scroll, hidden nav, single-screen layouts, framed as conversion experiments; suggests a two-week no-nav test), IONOS countertrends (hamburger menus vs nostalgic styles). Awwwards 'Unusual Navigation' tag: 1 of 31 latest Sites of the Day, 2 of 31 Sites of the Month, 3 of 31 Sites of the Year, so it stays rare. Emerging and niche; low confidence.
- Good for: Showcase sites, single-screen launches, portfolios, and experiments where exploration is the point.
- Risks (rules): ux-visible-navigation, ux-conventional-layout, a11y-keyboard, a11y-bypass-blocks, a11y-focus-order, a11y-target-size, a11y-pointer-gestures, a11y-consistent
- Do it well: Keep a visible, labelled route to the main sections (or a menu button with a text label); full keyboard and screen reader support; test whether people find a section within seconds.
- The slop version to avoid: A mystery-icon or gesture-only menu that hides primary links on desktop for a page whose job is conversion.

## infinite-canvas-and-dot-grid-backgrounds [emerging, confidence very low (single source)]
Taxonomy: utilitarian, graphics-only, design-tools, minimal
- Evidence: Single source: Webflow (Dec 2025) names 'the infinite canvas' (dot grids, node lines, open space) for creation and generative tools, with Flim as an example. No second source and no Awwwards tag exists for it. Impeccable lists decorative grid-line backgrounds as an advisory tell unless the surface really is a canvas or a measuring tool. Hypothesis only.
- Good for: Tools whose product is a canvas, node editor or workspace.
- Risks (rules): a11y-non-text-contrast, a11y-reflow, perf-cls
- Do it well: Use the grid or canvas only where the product is one; show the real product on it.
- The slop version to avoid: A dot-grid or hairline grid background behind a generic SaaS hero with no canvas in the product.

## plain-language-public-service-pages [saturated, confidence low (inferred from published guidance, not counted)]
Taxonomy: government-public, utilitarian, corporate-clean, swiss-grid, inform-educate
- Evidence: Dated 2026-11-06. In UK government and public-service sites this style is documented and long established: the GOV.UK design principles, type scale, layout and clear-language guidance (all read; see sources) describe plain words, one thing per page, sentence case and left-aligned text on a restrained palette. Status `saturated` applies only inside that niche and is inferred from the guidance being a published standard, not from a count of sites. Whether non-government services (charities, advice services, local services) are adopting it is unmeasured; one pilot (a fictional UK tenant-rights service, model-built, 2026-11-06) chose it, which is not evidence of a trend.
- Good for: Advice, benefits, housing, health information and any service whose visitors are stressed, reading in a second language or in a hurry, and whose first job is to get them to the right next step.
- Risks (rules): a11y-coga-plain-literal-language, copy-reading-grade, ux-primary-cta-above-fold, distinct-swap-test, a11y-coga-limit-choices-per-screen
- Do it well: Write in the reader's words at a low reading level, put the one next step and a phone route in the first screen, use visible focus and real labels, then add one lead element that comes from this service (the question as the interface, a live self-check, a number that matters) so the page is not a clone. See the recipes `urgent-help-route` and `form-no-backend-and-privacy`. Never imitate a government's crest, colours or name.
- The slop version to avoid: A pale header, a blue 'Start now' button and grey 'Related content' links on a private or charity service that has no service-specific content; every line hedged and nothing a person could act on; no phone number or hours; or a copy of a government's branding to borrow its trust.

## charity-emotional-template [saturated, confidence low (judgement, no sources read)]
Taxonomy: non-profit, photography, hero-full-bleed, hero-centered, friendly
- Evidence: Dated 2026-11-06. A description of a template, not a measured trend: no count of charity sites was made. It is named as an anti-goal in one pilot brief (a fictional UK tenant-rights service, 2026-11-06) and recognised from general familiarity with the sector. Treat `saturated` as a judgement that this is the page a reader expects from a charity, so copying it gives no distinction; re-check against real sites before relying on it.
- Good for: Fundraising pages whose job is a donation and whose story is real, named and consented to.
- Risks (rules): distinct-real-imagery-and-icons, copy-proof-verifiable, distinct-hero-not-template, copy-no-buzzwords, a11y-contrast-text
- Do it well: Lead with what the service does and for whom, in plain words; use a real number or a real, consented case with a source; keep one donate action, not five; show where the money goes; if you have no photographs, say so and use type or a live object instead (recipe `no-photography-physical-goods`).
- The slop version to avoid: A full-bleed photo of a smiling person under a warm overlay, a heart icon, 'Together we can make a difference', a donate button in the header, the hero and every section, impact counters with no source, three icon cards, a row of stock volunteers, and a story with no name or date.

## law-firm-authority-template [saturated, confidence low (judgement, no sources read)]
Taxonomy: professional-services, serif, serif-display, corporate-clean, trustworthy
- Evidence: Dated 2026-11-06. A description of a template, not a measured trend: no count of law-firm sites was made. It is named as an anti-goal in one pilot brief (a fictional UK tenant-rights service, 2026-11-06) and recognised from general familiarity with the sector. `saturated` means a reader expects this page from a law firm, so copying it gives no distinction; re-check against real sites before relying on it.
- Good for: Firms whose clients expect formality and whose proof is real (named areas of practice, regulated status, years of practice that can be checked).
- Risks (rules): distinct-palette-not-reflex-cream, distinct-hero-not-template, copy-proof-verifiable, copy-no-buzzwords, copy-jargon-acronyms
- Do it well: Say what you do for whom in plain words, put the phone number and the first step in the first screen, show real people and real credentials that can be checked (regulator, registration), explain legal terms where they appear, and carry the formality in clear structure rather than in navy and gold.
- The slop version to avoid: Navy and gold, a serif logotype with a scales or pillar icon, a courthouse or handshake photograph, 'Trusted legal counsel' and 'decades of experience' with no named case or checkable credential, a gold 'Free consultation' button, a three-column grid of practice areas with icons, a row of partner headshots in suits, and the disclaimer in small grey text.
