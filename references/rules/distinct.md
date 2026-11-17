# Quality Bar: Distinctiveness
Severity: blocker (never traded for style), major, minor, advisory. Labels: standard, evidence, craft-consensus, our-take.

### `distinct-reference-not-brand` [major · our-take]
A page rebuilt after a reference site ("make it like X") takes the reference's structure, proportions, sizes and motion, and none of its brand: not its name, copy, logo, illustrations or signature object, not a paid font it licenses, and not screenshots or pictures of its own product. Its signature object is replaced by one made from the subject's own world, and its picture slots hold the subject's own or properly credited material.
- Why: Structure and rhythm are craft anyone may learn from; the name, words, art and licensed fonts are the reference's property, and a picture of the reference's own product on another site reads as an advertisement for it (the owner caught exactly that on the whata.design home, 2026-11-17). Replacing the reference's object with one from the subject's world (a keychain of interface parts on a site about interface design) is what made the rebuild read as the subject's own.
- Check (manual): Put the rebuilt page beside the reference. List every name, sentence, logo, illustration, font family and picture on the rebuilt page that also appears on the reference, or that shows the reference's own product; each one is a finding. Then ask what the hero object is made of: if it is the reference's object recoloured, it is a finding. (tools: get_sections, get_section, render_sheet)
- While designing: Measure the reference into the library first (get_sections, get_section) and copy its numbers, order and motion beats; draw the hero object from the subject's own parts; fill pictures from the subject or the library with credit; use a free or owned font with the same role.
- Sources: whata-owner-review-2026-11-17

### `distinct-written-direction` [major · craft-consensus]
Before building, a written direction file exists that names 4 to 6 colours with roles, the display, body and (if used) mono font roles, a radius scale, and the subject-derived lead element of the hero, and every colour, font family and border-radius value in the shipped CSS appears in that file.
- Why: Four independent practitioner sources recommend fixing tokens up front (a 4 to 6 colour plan; exact tokens instead of adjectives like 'modern and clean'), and Impeccable ships rules that flag a font, colour, radius or font size outside a DESIGN.md. Vague adjective prompts are said to return the statistical average.
- Check (hybrid): Read the direction file. Extract distinct computed colours, font-family primaries, border-radius values and font sizes from the built page's CSS. Fail any value that is absent from the file (allow neutrals derived from the stated ramp). Confirm the file names the hero's lead element and why it fits the subject. (tools: headless browser, getComputedStyle, impeccable detect (design-system-* rules))
- While designing: Write the direction file first, then use only the colours, faces, radii and sizes it names.
- Sources: capitalandcompute-fix-ai-slop, anthropic-frontend-design-skill, noqta-ai-slop-patterns, prg-purple-gradient, impeccable-repo, local-design-taste-frontend

### `distinct-display-font-chosen` [minor · craft-consensus]
The primary font-family of the display headings (h1 to h3) is not on the overused list (inter, roboto, open sans, lato, montserrat, arial, helvetica, fraunces, instrument sans, instrument serif, geist, geist sans, geist mono, mona sans, plus jakarta sans, space grotesk, recoleta) unless it is the brand's own face or the direction file justifies it; the body face may be a neutral sans.
- Why: Six independent groups of sources name default faces as the top typographic tell; Impeccable's list was current as of 2026-11-05. The list is contested (one local skill recommends Geist; Google ranks Inter 5th in popularity), so the stable rule is a chosen and recorded face, not membership of a list.
- Check (automated): In a headless browser, read getComputedStyle(fontFamily) for h1, h2, h3 and body; take the first non-generic family, lowercase it, ignore spaces, hyphens and underscores, and compare with the list. Flag a match on display headings that is not recorded as an exception. (tools: headless browser, impeccable detect (overused-font))
- While designing: Pick the display face from the subject and brand, say why, and avoid the face most generated pages use.
- Often conflicts with styles: swiss-grid, utilitarian, corporate-clean, minimal
- Sources: impeccable-repo, wystack-anti-patterns, capitalandcompute-fix-ai-slop, prg-purple-gradient, noqta-ai-slop-patterns, laith-ux-skill-wiki, jc-aiwiki-unslop-ui, local-design-taste-frontend

### `distinct-eyebrow-restraint` [minor · craft-consensus]
Small labels used as ornament stay rare: tracked uppercase or small-caps labels directly above headings plus small (14 px or less) uppercase, small-caps or monospace labels anywhere in the first viewport that are not links, buttons, navigation, form, table or code text (corner labels such as "SHEET 01" or "MEASURED ON RENDER") number at most ceil(sections / 3) on the page and at most one in the first viewport; none sits above the hero headline unless recorded as an exception; and numbered markers (01, 02, 03) appear only where the content is a real sequence.
- Why: Impeccable bans a kicker above a heading outright and flags the hero chip; Anthropic's skill and Capital & Compute list tracked all-caps eyebrows and numbered markers; Noqta flags excess tracking on uppercase eyebrows; the local skill sets 'at most one per three sections'. The strict source and the lenient source disagree; this rule checks the lenient threshold. Corner and caption labels in the first viewport were added on 2026-11-17: the owner named decorative all-caps mono labels as a tell in our own mock-ups, and the local skill bans the mono-caps decoration strip at the hero bottom. The one-per-first-viewport limit is our own threshold.
- Check (automated): Find elements with text-transform uppercase (or small-caps), positive letter-spacing and length of 40 characters or fewer that are the previous sibling of a heading (eyebrows). Separately, in the first viewport, find elements whose own text is 2 to 40 characters at 14 px or less, set uppercase, small-caps, literal capitals (two or more words, or six or more letters) or a monospace family, outside a, button, nav, label, form fields, footer, code, pre, table and headings (ornament labels). Fail if eyebrows plus ornament labels exceed ceil(section count / 3), if eyebrows in the first viewport plus ornament labels exceed 1, or if an eyebrow sits above the h1. Flag numeric prefixes in eyebrows where the section list is not an ordered process. (tools: headless browser, impeccable detect (kicker-above-heading, hero-eyebrow-chip, numbered-section-labels))
- While designing: Let each heading stand alone, and drop corner labels, sheet numbers and mono captions that only decorate; keep a label only when it tells the reader something.
- Often conflicts with styles: editorial, swiss-grid, utilitarian, newspaper
- Sources: impeccable-repo, capitalandcompute-fix-ai-slop, anthropic-frontend-design-skill, noqta-ai-slop-patterns, local-design-taste-frontend

### `distinct-hero-headline-proportion` [minor · craft-consensus]
The hero h1 is no larger than 6rem (96 px), is not both 72 px or larger and 40 characters or longer, uses letter-spacing no tighter than -0.04em, and wraps within about 45 characters per line.
- Why: Impeccable's detector flags h1 at 72 px or more with 40 or more characters and its craft floor caps display type at 6rem with a tracking floor of -0.04em; Laith's wiki gives 30 to 45 characters per line and about -0.03em at 48 px or more. These thresholds conflict with very large, short headlines only when the headline is long.
- Check (automated): At 1440 px and 390 px viewports, read the hero h1 computed font-size, letter-spacing (in em), text length, and the longest rendered line length in characters. Fail any threshold above; review one-to-three-word headlines as allowed. (tools: headless browser, impeccable detect (oversized-h1, extreme-negative-tracking))
- While designing: Keep the headline short enough that its type size stays under 6rem and the line stays near 45 characters.
- Often conflicts with styles: oversized-type, expressive-type, hero-type-only
- Sources: impeccable-repo, laith-ux-skill-wiki, local-design-taste-frontend

### `distinct-hero-not-template` [minor · craft-consensus]
The first viewport shows a real, subject-specific element (the product UI, work, place or object) and does not match the stock skeleton: at most two of these six signals appear together (centred headline, badge or eyebrow above it, exactly two buttons, a logo row within the next section, a three-card feature row as the following section, a stats strip of three or more big numbers in one row below the headline or as the following section).
- Why: Five independent groups describe the same skeleton; Capital & Compute lists it as 'stock page order'. A centred hero alone is common and conventional, so this rule scores the whole skeleton plus whether real subject content leads. The stats strip was added as the sixth signal on 2026-11-17: the owner named the centred stack of eyebrow, headline, sub, pill button and stats row as the shape of our own AI-looking mock-ups.
- Check (hybrid): At 1440 px, score the six signals from the DOM and computed styles. A big number is an element whose own text is a number of 10 characters or fewer (with an optional unit, %, x, + or currency) at max(28 px, 1.6 x body size); three or more with tops within 16 px and different left edges, below the h1 in the hero's section or anywhere in the next section, form a stats strip. Fail at three or more signals. A reviewer confirms the hero's dominant visual is real subject content (not a gradient blob or a div mock-up). (tools: headless browser, screenshots)
- While designing: Open with the most characteristic real element of the subject and compose the hero around it.
- Often conflicts with styles: hero-centered, saas-stack, hero-type-only
- Sources: capitalandcompute-fix-ai-slop, prg-purple-gradient, jc-aiwiki-unslop-ui, laith-ux-skill-wiki, impeccable-repo, local-design-taste-frontend, nng-homepage-principles

### `distinct-justified-exceptions` [minor · craft-consensus]
Every use of a flagged default in this family (overused font, purple/cyan palette, gradient text, glow, glass, cream+terracotta, identical card grid, eyebrow labels, marquee) is listed in the direction file with a subject-specific reason.
- Why: The tells are defaults, not banned techniques; Capital & Compute and Laith's tool both provide an explicit way to mark an intentional use, and Impeccable offers inline ignores. An unrecorded use is indistinguishable from a reflex.
- Check (manual): Run the automated checks of the other distinct- rules. For each finding, confirm the direction file records the reason. Findings without a recorded reason fail.
- While designing: When you choose a common default on purpose, write down why it fits this subject.
- Sources: capitalandcompute-fix-ai-slop, laith-ux-skill-wiki, impeccable-repo, local-design-taste-frontend

### `distinct-motion-authored` [minor · craft-consensus]
Motion is one authored sequence plus responses to user action: the same entrance animation is not applied to every section, no easing overshoots (cubic-bezier with y outside 0 to 1, or elastic/bounce), no infinite animation exists that does not encode a state, and at most one auto-scrolling marquee exists.
- Why: Five independent groups describe motion on everything and bounce easing; Impeccable treats bounce as advisory and any auto-scrolling marquee as a tell, while the local skill allows one marquee per page. Awwwards Sites of the Day are heavily animated (GSAP on 19 of 31), so the tell is sameness and lack of purpose, not motion itself. See also a11y-reduced-motion, a11y-pause-stop-hide and ux-minimal-motion.
- Check (hybrid): Collect CSS animations and transitions: flag identical keyframe names applied to 4 or more sibling sections; flag cubic-bezier with a coordinate outside 0 to 1 on y; count animation-iteration-count infinite and marquee patterns. A reviewer records the purpose of each remaining animation (hierarchy, story, feedback, state). (tools: headless browser, impeccable detect (bounce-easing, marquee, pulsing-dot))
- While designing: Design one signature motion moment and make every other animation answer a user action.
- Often conflicts with styles: ambient-loop, marquee, scroll-triggered, micro-interactions
- Sources: impeccable-repo, wystack-anti-patterns, prg-purple-gradient, noqta-ai-slop-patterns, laith-ux-skill-wiki, capitalandcompute-fix-ai-slop, local-design-taste-frontend, mdn-prefers-reduced-motion

### `distinct-no-accent-word-headline` [minor · our-take]
No h1 or h2 sets one word or a short run (up to three words and under half of the heading's characters, not a link or code) apart from the rest of the heading by italic, a different colour, a different font family or a weight 200 or more units away (for example "Taste your AI can <em>read.</em>" with the accent colour on "read."). One such heading per page is allowed only as a recorded exception with a subject reason.
- Why: The single italic or accent-coloured word in a serif display headline is a stock move of generated hero sections: the owner named it on 2026-11-17 as one of the tells that made our own mock-ups read as AI-made, and the local design-taste skill bans the line-broken italic headline as a default move and mixed-family emphasis. Emphasis that the sentence needs can come from wording and order; the three-word and half-heading limits are our own thresholds.
- Check (automated): For every visible h1 and h2 with two or more words, compare each descendant element (skipping links, code, sup, sub, images and runs of 1 px or less) whose text is three words or fewer and under half the heading's characters with the heading's computed style: font-style italic or oblique versus normal, colour (summed RGB channel difference over 48, a hue shift over 30 degrees between chromatic colours, or chromatic versus neutral), primary font family, and font-weight 200 or more apart. Report one finding per heading; any finding fails unless it is recorded as an exception. (tools: headless browser, getComputedStyle)
- While designing: Write a headline that carries its own emphasis; if one word must stand out, change the sentence, not the word's colour or slant.
- Often conflicts with styles: serif-editorial, expressive-type, editorial
- Sources: local-design-taste-frontend

### `distinct-no-ai-palette` [minor · craft-consensus]
No gradient stop or primary accent has a hue between 260 and 310 degrees (purple, violet, indigo), and no cyan accent sits on a near-black ground, unless the brand is that colour and the direction file says so.
- Why: Six independent source groups name purple-to-blue gradients as the most recognised tell. Impeccable tests purple text at hue 260 to 310 (and treats a declared colour as purple within 250 to 320). The Reddit-mining dataset (3,214,533 posts scanned, 3,033 comments) ranks the 'AI purple' gradient among its top tells; that measures what people complain about, not cause.
- Check (automated): Parse all gradients and accent colours in computed styles; convert stops to HSL or OKLCH hue; flag any in 260-310 degrees with meaningful saturation, plus Tailwind classes from/to purple, violet, indigo. Flag cyan accent text or fills on a background with very low luminance. (tools: headless browser, impeccable detect (ai-color-palette))
- While designing: Derive the accent hue from the brand or subject and avoid default violet-to-blue gradients.
- Often conflicts with styles: gradient-aurora, futuristic-tech, dark-cyber, hue-purple, neon
- Sources: impeccable-repo, wystack-anti-patterns, prg-purple-gradient, noqta-ai-slop-patterns, jc-aiwiki-unslop-ui, vibecoded-design-tells-repo, laith-ux-skill-wiki, local-design-taste-frontend

### `distinct-no-decorative-glow` [minor · craft-consensus]
No element has a chromatic box-shadow or text-shadow with zero offset and blur of 3 px or more; no chromatic radial-gradient halo (a saturated stop fading to transparent, on an element or its ::before/::after) sits behind the hero or a section, on a dark page at any size or on a light page at 160 x 160 px or larger; and no blurred colour blob (a textless element of 120 px or more with a chromatic fill and filter: blur of 20 px or more) is used, unless the glow or halo encodes a state (focus, selection, live status).
- Why: Five independent source groups call glows and halos a default AI look. Impeccable's detector uses a minimum glow strength of 3 px and, for radial halos, a minimum effective alpha of 0.14 and contrast of 1.30 on the surface. One lineage's numbers; treat as indicative. The light-page halo (a soft peach or pink radial glow behind a centred hero) was added on 2026-11-17 after the owner named it as one of the tells that made our own hero mock-ups read as AI-made; the 160 px floor is our own threshold so a small button sheen does not count.
- Check (automated): Parse computed box-shadow and text-shadow lists: flag entries with 0 horizontal and vertical offset, blur at or above 3 px and a saturated colour. Flag background-image radial-gradient (on the element or its ::before/::after) with a saturated stop and a stop under 0.3 alpha: on a dark page at any size, on a light page when the box is 160 px or more both ways. Flag textless elements of 120 px or more with a chromatic background and filter blur of 20 px or more. A halo that encodes a state is recorded as an exception. (tools: headless browser, impeccable detect (dark-glow, radial-halo, radial-spotlight-glow))
- While designing: Use neutral elevation shadows and a flat or subtly shifted background instead of coloured glow.
- Often conflicts with styles: dark-cyber, futuristic-tech, neon, gradient-aurora
- Sources: impeccable-repo, jc-aiwiki-unslop-ui, noqta-ai-slop-patterns, laith-ux-skill-wiki, local-design-taste-frontend

### `distinct-no-fake-status-badges` [minor · craft-consensus]
No pulsing status dot and no 'Live', 'New', 'Beta' or version pill appears unless it is bound to real changing state or a real release, and no pill chip sits above the hero heading.
- Why: Noqta, Impeccable (pulsing-dot, hero-eyebrow-chip), the redesign skill and the design-taste skill all flag decorative liveness badges. Reserving pulse for live data is the stated fix.
- Check (automated): Find small elements (aspect ratio 1.5 or less) with an infinite pulse animation; find pill-shaped elements (radius at or above half the height) whose text is new, live, beta, alpha, or matches a version pattern, within the first viewport; flag unless linked to data attributes or a release record. (tools: headless browser, impeccable detect (pulsing-dot, hero-eyebrow-chip))
- While designing: Show a status label only when it reports something true and current.
- Often conflicts with styles: dark-cyber, futuristic-tech
- Sources: noqta-ai-slop-patterns, impeccable-repo, local-redesign-existing-projects, local-design-taste-frontend

### `distinct-no-filler-copy` [minor · craft-consensus]
Shipped copy contains no lorem ipsum, no placeholder people or brands (John Doe, Jane Smith, Acme, Globex, Initech), none of the filler words streamline, empower, supercharge, unlock, elevate, seamless, unleash, world-class, enterprise-grade, next-generation, cutting-edge, game-changer, and every statistic is traceable to a source or removed.
- Why: Five independent groups list invented round numbers, placeholder names and filler verbs; Impeccable has a buzzword rule and Laith names the stat pattern (for example 10x, 99.9%, 10,000+). The existing guideline set already covers plain tagline and objective language (ux-tagline-specific, ux-objective-language, ux-descriptive-labels); this rule adds the mechanical list check.
- Check (automated): Extract visible text and alt text. Regex for the list above (case-insensitive), lorem ipsum, and standalone round statistics (10x, 99.9%, \d{1,3},000+). For every statistic, require a data-source or footnote in the content brief; flag otherwise. (tools: headless browser, impeccable detect (marketing-buzzword))
- While designing: Write what the product literally does with real numbers, and delete any figure you cannot source.
- Sources: impeccable-repo, capitalandcompute-fix-ai-slop, noqta-ai-slop-patterns, laith-ux-skill-wiki, local-design-taste-frontend, local-redesign-existing-projects

### `distinct-no-gradient-text` [minor · craft-consensus]
No text (headings, metrics, body) is filled with a gradient: no element combines background-clip: text with a gradient background-image.
- Why: Gradient text appears in the Impeccable detector as its own rule, in wystack and the Reddit dataset, in Laith's list and in the local skills; emphasis can come from weight or size instead.
- Check (automated): Query all elements; flag those whose computed -webkit-background-clip or background-clip is text and whose background-image contains a gradient function. (tools: headless browser, impeccable detect (gradient-text))
- While designing: Set emphasis with weight, size or a solid colour, not a gradient fill.
- Often conflicts with styles: gradient-aurora, expressive-type
- Sources: impeccable-repo, wystack-anti-patterns, jc-aiwiki-unslop-ui, laith-ux-skill-wiki, local-design-taste-frontend

### `distinct-no-identical-card-grid` [minor · craft-consensus]
No section is built mainly from three or more same-size sibling cards that each hold an icon (or rounded icon tile), a heading and a short paragraph; the most important item gets more space than the others.
- Why: Five independent source groups name the three-column icon-card feature row and the icon tile above a heading; Impeccable lists both as rules. Laith's tool lets you waive it when the product truly has three equal pillars.
- Check (hybrid): In the DOM find sibling groups of 3 or more elements with widths within 5% of each other that each contain an svg/img icon, a heading and a paragraph. Report groups; a reviewer accepts a group only when the content is genuinely parallel and recorded as an exception. (tools: headless browser, impeccable detect (identical-card-grids, icon-tile-stack))
- While designing: Give the lead feature more room or show it as a real example instead of a row of identical cards.
- Often conflicts with styles: bento-grid, saas-stack, catalog-grid
- Sources: impeccable-repo, wystack-anti-patterns, prg-purple-gradient, jc-aiwiki-unslop-ui, laith-ux-skill-wiki, local-design-taste-frontend

### `distinct-no-nested-cards` [minor · craft-consensus]
No bordered, shadowed or tinted card container sits inside another such container.
- Why: Impeccable has a nested-cards rule and wystack lists cards inside cards; Laith flags stacking shadow, border and tint on one card; the local skill allows cards only where elevation signals hierarchy. Flattening with spacing and dividers is the common fix.
- Check (automated): For each element with a visible border, box-shadow, or non-transparent background different from its parent plus radius at or above 4 px, check whether an ancestor within the same section also qualifies. Report depth 2 or more. (tools: headless browser, impeccable detect (nested-cards))
- While designing: Use spacing, rules and type to group content instead of boxes inside boxes.
- Often conflicts with styles: bento-grid, claymorphism, skeuomorphic
- Sources: impeccable-repo, wystack-anti-patterns, laith-ux-skill-wiki, local-design-taste-frontend

### `distinct-no-side-stripe-border` [minor · craft-consensus]
No rounded element (radius 4 px or more) has a chromatic border on a single side wider than 1 px.
- Why: Impeccable calls the thick coloured one-sided border on a card the most recognisable tell and sets 4 px radius as the point where it reads as a rounded card; Noqta makes the same claim. Square callouts with a severity rule are an older convention and are not flagged.
- Check (automated): For each element, compare computed border widths per side. Flag where exactly one side is above 1 px, its colour is chromatic, and the two corners away from that side have radius at or above 4 px. (tools: headless browser, impeccable detect (side-tab, border-accent-on-rounded))
- While designing: Mark emphasis with a background tint or an icon, not a thick coloured edge on a rounded card.
- Often conflicts with styles: neo-brutalist
- Sources: impeccable-repo, wystack-anti-patterns, noqta-ai-slop-patterns

### `distinct-radius-elevation-scale` [minor · craft-consensus]
The CSS defines a named radius scale and a named elevation scale, each element role (button, input, card, badge, image) maps to a documented value, a single radius of 16 px or more is not applied to all roles, and no row of three or more cards pairs a hairline border with a shadow blur of 32 px or more.
- Why: Noqta recommends a named scale (24 px everywhere versus a 6 px card example), Laith flags 16 to 24 px on everything and stacked border-shadow-tint, Impeccable flags rows of cards with a hairline border and a shadow of at least 32 px blur. The local design-taste skill asks for one consistent scale, so the compromise is a documented role map.
- Check (automated): Collect computed border-radius for buttons, inputs, cards, badges and images; fail when all share one value at or above 16 px. Collect box-shadow blur on card rows: fail when 3 or more adjacent cards have a visible 1 px border and blur at or above 32 px. Confirm radius/shadow tokens exist in the direction file. (tools: headless browser, impeccable detect (gpt-thin-border-wide-shadow))
- While designing: Define radius and shadow tokens per element role and use each token the same way everywhere.
- Often conflicts with styles: claymorphism, organic-soft, neo-brutalist
- Sources: noqta-ai-slop-patterns, laith-ux-skill-wiki, impeccable-repo, prg-purple-gradient, local-redesign-existing-projects, local-design-taste-frontend

### `distinct-real-imagery-and-icons` [minor · craft-consensus]
No img uses a placeholder or stock-demo host, the product is not shown as a mock-up built from empty div rectangles (live interface built from real text, controls and states is fine), no hero-sized inline SVG scene is assembled from primitive shapes, no emoji or Unicode pictograph stands in for an icon, and icons come from one family at one stroke weight.
- Why: Five independent groups flag stock or machine-made imagery, emoji icons or default icon sets; Impeccable has a shape-assembled-illustration rule (advisory) and bans glyph icons in its craft floor; the local skill suggests picsum placeholders only while developing, so they must be replaced before shipping. Existing rule ux-informative-imagery already asks for imagery that informs. When no real screenshots or photos exist yet, show the product as live HTML/CSS with real text and states (not empty boxes), or leave the imagery out and mark the gap; never ship a placeholder host or stock demo image. For physical goods there is no interface to show, so the offer itself (price, seats, dates, a calculator or booking control built from real HTML), type set large as the image, or an omitted and marked gap are the honest options; real photographs have to be commissioned.
- Check (hybrid): List img and background-image sources and flag placeholder hosts (picsum, placehold, via.placeholder, unsplash source URLs used as demo); regex visible text and button labels for pictographic emoji used as icons; flag svg elements above half the viewport width built from at least a handful of primitive shapes; compare icon svg stroke widths. A reviewer confirms the hero image is real. (tools: headless browser, impeccable detect (shape-assembled-illustration, broken-image))
- While designing: Use real photos or screenshots and one consistent icon set, never emoji or placeholder images; with no screenshots yet, build the product view as live HTML with real text and states, or omit it. For a physical product with no photographs, the offer itself can be the live object (price, seats, dates, a calculator, a booking control), or a measurement or price can be set large as real text, or leave the imagery out and mark the gap; do not draw the product from shapes in code (recipe no-photography-physical-goods).
- Often conflicts with styles: illustration, hand-drawn, graphics-only
- Sources: noqta-ai-slop-patterns, impeccable-repo, jc-aiwiki-unslop-ui, laith-ux-skill-wiki, local-design-taste-frontend, local-redesign-existing-projects

### `distinct-type-hierarchy-step` [minor · craft-consensus]
The rendered type roles (body, h3, h2, h1) contain at least one step of 1.25x or more between neighbours, and headings are visibly separated from body by size or by weight (at least 200 weight units heavier for at least 80% of headings).
- Why: Impeccable flags a flat hierarchy when heading and body roles differ by less than 1.25x at every step (it needs at least 3 roles) and weight does not separate them. Other sources push stronger contrast (prg.sh suggests size jumps of 3x or more and extreme weights); those numbers come from one blog.
- Check (automated): For h1 to h3 and p, li, td, blockquote read computed font-size and font-weight. Compute the largest ratio between neighbouring size roles and the share of headings at least 200 weight units heavier than the body weight. Fail if every step is below 1.25 and fewer than 80% of headings clear the weight gap. (tools: headless browser, impeccable detect (flat-type-hierarchy))
- While designing: Make at least one type step visibly larger than the 1.25x floor and give headings real weight contrast.
- Often conflicts with styles: minimal, swiss-grid
- Sources: impeccable-repo, prg-purple-gradient, wystack-anti-patterns, laith-ux-skill-wiki, webdev-typography

### `distinct-customize-library-defaults` [advisory · craft-consensus]
Component-library defaults (for example shadcn/ui tokens or Tailwind palette values) are customised: the shipped radius, colour and font variables differ from the library's init output.
- Why: The Reddit dataset ranks the default shadcn/Tailwind look as its top specific tell; the local design-taste skill says never ship default state. Two groups, one of them an informal proxy of opinion.
- Check (automated): Generate the library's default theme in a scratch project; diff its CSS variables for radius, background, foreground, primary and font against the shipped CSS; flag when radius, primary and font all equal the defaults. (tools: diff)
- While designing: Set your own radius, colour and type tokens before using any library component.
- Often conflicts with styles: corporate-clean, utilitarian
- Sources: jc-aiwiki-unslop-ui, vibecoded-design-tells-repo, local-design-taste-frontend

### `distinct-glass-with-purpose` [advisory · our-take]
Every element using backdrop-filter blur is listed in the direction file with its function (for example nav over media, overlay separation), has a solid-colour fallback, and glass is not the default style of cards.
- Why: Impeccable and Capital & Compute flag decorative glass; the Reddit dataset indicates users rarely complain about glassmorphism, and trend articles disagree on whether it has peaked. No source gives a numeric limit, so this is a judgement call.
- Check (hybrid): Count elements with computed backdrop-filter containing blur. For each, confirm a recorded function and that text on it passes contrast against the worst-case content behind it (see a11y-contrast-text). Check a @supports fallback exists. (tools: headless browser)
- While designing: Use blur only where it separates a layer from content that changes behind it, with a solid fallback.
- Often conflicts with styles: glassmorphism
- Sources: impeccable-repo, capitalandcompute-fix-ai-slop, vibecoded-design-tells-repo, mdn-backdrop-filter, framerwebsites-trends-2026

### `distinct-no-template-chrome` [advisory · craft-consensus]
No more than two links or buttons end in an arrow glyph, no more than one meta string uses middle-dot separators, and em-dashes stay below saturation (fewer than 8 in total, or less than one per 500 characters of body text).
- Why: Anthropic's skill and Laith list arrows on links and buttons; the Anthropic skill and the local skill ration middle-dot strings; Impeccable's em-dash rule is advisory and only fires at 8 or more em-dashes near one per 500 characters. The 'two' and 'one' limits are our own working thresholds. The local skill's total em-dash ban is not shared by any other source.
- Check (automated): Count link and button labels ending in an arrow character (arrow, chevron); count text nodes with 2 or more middle-dot separators; count em-dashes and body-text length. (tools: headless browser, impeccable detect (em-dash-overuse, aphoristic-cadence))
- While designing: Write plain button and link labels and separate metadata with layout instead of dots and arrows.
- Often conflicts with styles: editorial, newspaper, utilitarian
- Sources: anthropic-frontend-design-skill, laith-ux-skill-wiki, capitalandcompute-fix-ai-slop, impeccable-repo, local-design-taste-frontend

### `distinct-palette-not-reflex-cream` [advisory · craft-consensus]
A warm cream or beige page background (minimum channel 209 or higher, red at least green at least blue, red minus blue between 6 and 48) combined with a terracotta or clay accent and a serif display face is used only when the direction file gives a subject reason.
- Why: Impeccable has a rule for the cream surface; Anthropic's skill names cream with a terracotta accent near #D97757 as a default to avoid; Capital & Compute reports it as the second-wave cluster that appears after purple is banned; the local design-taste skill bans a family of cream, brass and espresso hexes for premium-consumer briefs. These are all one lineage plus one local skill, so the evidence is thin.
- Check (automated): Read body and main-section background colours; test the cream condition above; if true, also check for a terracotta/clay accent (hue roughly 10-30 degrees, moderate saturation) and a serif display face. Report all three together as one finding and require an exception record. (tools: headless browser, impeccable detect (cream-palette))
- While designing: Choose the page background from the subject's world, not from the safe warm off-white.
- Often conflicts with styles: serif-editorial, quiet-luxury, organic-soft, botanical-natural, earthy
- Sources: impeccable-repo, anthropic-frontend-design-skill, capitalandcompute-fix-ai-slop, local-design-taste-frontend

### `distinct-review-against-published-criteria` [advisory · our-take]
Before shipping, the page is reviewed against the four published Awwwards criteria (Design 40%, Usability 30%, Creativity 20%, Content 10%) with one piece of evidence recorded per criterion, and any criterion without evidence is treated as failing.
- Why: Awwwards publishes these weights and states that at least 18 jurors score each nominee; Webby lists seven criteria (including accessibility and speed under Visual Design and Functionality) without weights; CSS Design Awards gives only thresholds. Using a public rubric makes the review explicit; the evidence requirement is our own.
- Check (manual): Score Design, Usability, Creativity and Content on 1 to 10 with a cited screenshot or report per score; compute 0.4*Design + 0.3*Usability + 0.2*Creativity + 0.1*Content; optionally also check the Webby list (content with a point of view, structure and navigation, visual design, functionality, interactivity, innovation, overall experience). (tools: screenshots)
- While designing: Keep a one-line piece of evidence for design, usability, creativity and content before calling the page done.
- Sources: awwwards-evaluation, webby-judging-criteria, cssda-about, awwwards-site-lando-norris

### `distinct-section-rhythm-varied` [advisory · craft-consensus]
Section paddings or heights are not all identical, no layout family is used for more than two consecutive sections, and a page of 8 sections uses at least 4 different layout families.
- Why: Four independent groups flag uniform spacing and repeated section shapes (Impeccable's monotonous-spacing rule; Laith's uniform section rhythm). The numbers 4 of 8 and 2 in a row come from one local skill only.
- Check (automated): Measure each top-level section's computed padding-block and height; flag a coefficient of variation near zero. Classify each section's skeleton (full-bleed, split, grid of N, list, quote) and count runs and distinct families. (tools: headless browser, impeccable detect (monotonous-spacing))
- While designing: Vary section structure and spacing on purpose, with one anchor section per screen of content.
- Often conflicts with styles: saas-stack, single-column, editorial-feed
- Sources: impeccable-repo, wystack-anti-patterns, laith-ux-skill-wiki, noqta-ai-slop-patterns, local-design-taste-frontend

### `distinct-swap-test` [advisory · our-take]
With the logo and name replaced by a competitor's, a reviewer can still tell which site is which from the hero, type, colour and imagery alone.
- Why: Only Noqta states this test; Prg.sh's call for personality and a clear point of view is related. Treat as a judgement heuristic.
- Check (manual): Screenshot the first two viewports, swap the logo and brand name with a competitor's, and ask a reviewer who did not build it to identify the site and say what the design idea is. If they cannot, record a finding.
- While designing: Anchor the design in one idea that only this subject could carry.
- Often conflicts with styles: corporate-clean, minimal
- Sources: noqta-ai-slop-patterns, prg-purple-gradient
