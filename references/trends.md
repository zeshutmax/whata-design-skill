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
