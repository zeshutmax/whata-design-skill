# Quality Bar: Usability, content and performance
Severity: blocker (never traded for style), major, minor, advisory. Labels: standard, evidence, craft-consensus, our-take.

### `perf-cls` [major · standard]
Cumulative Layout Shift is 0.1 or less at the 75th percentile.
- Why: Reflects whether the page feels stable.
- Check (automated): Check field and lab data. Common fixes: width and height or aspect-ratio on images and video, reserved space for late content, font-display: optional with a close fallback, animate transform instead of top, left or box-shadow. (tools: lighthouse)
- While designing: Reserve space for images, video, embeds and late content; keep layout shift at 0.1 or less.
- Often conflicts with styles: intro-preloader
- Sources: webdev-core-web-vitals, webdev-optimize-cls

### `perf-core-first` [major · craft-consensus]
Core content loads immediately and does not depend on a heavy effect layer; build effects on top of working content.
- Why: Progressive enhancement keeps the page usable when effects fail or are slow.
- Check (manual): Disable JavaScript and throttle the network; the message and navigation should still appear.
- While designing: Build core content and navigation as HTML that works without JavaScript; layer effects on top.
- Often conflicts with styles: realtime-3d, chaptered-story, hero-3d
- Sources: nng-homepage-principles, keith-resilient-web-design

### `perf-inp` [major · standard]
Interaction to Next Paint is 200 ms or less at the 75th percentile.
- Why: Reflects whether the page feels responsive.
- Check (automated): Check field data; lab tools only approximate it. (tools: lighthouse)
- While designing: Keep interaction responses at 200 ms or less: avoid long main-thread tasks, animate with transform and opacity, debounce handlers.
- Often conflicts with styles: realtime-3d, scroll-triggered, cursor-effects
- Sources: webdev-core-web-vitals

### `perf-lcp` [major · standard]
Largest Contentful Paint is 2.5 seconds or less at the 75th percentile of page loads, for mobile and desktop separately.
- Why: Reflects whether the page feels like it is loading. NN/g cites a Google finding that bounce likelihood rises 32% as load time goes from 1 to 3 seconds; the method is not given, so treat it as secondary evidence.
- Check (automated): Check field data (CrUX) and lab data (Lighthouse). LCP candidates are img, image in svg, video (poster load or first frame, whichever is earlier), url() background images (not gradients) and block-level text. (tools: lighthouse)
- While designing: Keep LCP at 2.5 s or less: make the LCP image discoverable in HTML, never lazy-load it, set fetchpriority high, keep head scripts and CSS small.
- Often conflicts with styles: realtime-3d, hero-video, hero-3d, intro-preloader
- Sources: webdev-core-web-vitals, nng-homepage-principles, webdev-lcp

### `ux-carousel-caution` [major · evidence]
Prefer a single static hero to a rotating carousel. If you use a carousel: five frames or fewer, controls inside it with a clear current state, no auto-advance on mobile, timing based on reading speed (about 3 words per second), and the important content repeated elsewhere.
- Why: Users often scroll past carousels and miss frames after the first. This is a 2013 article (reviewed 2026) with no stated sample size, so the guidance is guideline-level, not study-level.
- Check (manual): Check frame count, controls, auto-rotation and whether any critical message exists only inside the carousel. APG carousel pattern: an auto-rotating carousel has a stop/start button as its first tab stop (its label changes, so no aria-pressed), rotation stops when focus enters or the mouse hovers, and previous and next buttons are required.
- While designing: Prefer one static hero; if you use a carousel keep it to five frames, controls inside, no autoplay on mobile, and repeat key content elsewhere.
- Often conflicts with styles: marquee
- Sources: nng-carousels, wcag-22-quickref, aria-apg-carousel

### `ux-descriptive-labels` [major · evidence]
Links and buttons have specific descriptive labels, not "Click here" or "Learn more".
- Why: Users scan, and screen reader users hear links out of context.
- Check (hybrid): List every link and button label out of context.
- While designing: Label links and buttons with the result ('Book a demo'), not 'Learn more' or 'Submit'.
- Sources: nng-homepage-principles, nng-how-users-read

### `ux-form-errors` [major · evidence]
Signal errors with several cues, not color alone; explain the problem specifically; keep what the user typed.
- Why: Users must understand and fix errors without redoing work.
- Check (manual): Submit invalid data and read the messages.
- While designing: Signal errors with more than color, say what is wrong and keep the user's input.
- Sources: nng-web-forms, wcag-22-quickref

### `ux-form-length` [major · evidence]
Keep forms as short as possible: remove fields that can be derived, collected later or dropped; limit optional fields to one or two and label them.
- Why: Fewer fields mean higher completion.
- Check (manual): List every field and justify it.
- While designing: Ask only for fields you need; at most one or two optional fields, labeled.
- Sources: nng-web-forms

### `ux-form-no-placeholder-label` [major · evidence]
Do not use placeholder text as the label or as the only instruction.
- Why: NN/g reports usability problems with placeholders; the text disappears on input.
- Check (hybrid): Check every field has a visible, persistent label.
- While designing: Never use a placeholder as a label; keep a visible label.
- Often conflicts with styles: minimal
- Sources: nng-web-forms, wcag-22-quickref

### `ux-front-load` [major · evidence]
Put the most important information in the first screens and the first two paragraphs; begin headings, bullets and paragraphs with meaningful words.
- Why: Eyetracking of 232 users found a rough F-shaped pattern (Nielsen, 16 Apr 2006; a later study 11 years on reportedly confirmed it); it is a shape, not a law. In a 2018 study (Fessenden, 15 Apr 2018; 120 participants, over 130,000 fixations) 57% of viewing time was above the fold and 74% in the first two screenfuls.
- Check (manual): List the top three things a visitor must learn and check they appear in the first two screens.
- While designing: Put the most important information in the first screens and the first words of headings and paragraphs.
- Often conflicts with styles: chaptered-story, long-scroll-narrative
- Sources: nng-f-pattern, nng-scrolling-attention

### `ux-no-ad-lookalikes` [major · evidence]
Do not style important content like an ad (banner shapes, right-rail boxes, animated strips).
- Why: Users ignore elements they perceive as ads, including content nearby and large distinct images (NN/g, 22 Apr 2018, 26 participants in the latest eyetracking study). One participant's gaze on one page gave the right rail 33 times fewer fixations than its size suggested (1 of 132 content-area fixations); that is an illustration, not a statistic.
- Check (manual): Check that key messages are not in banner-like containers.
- While designing: Do not style important content like banners, right-rail boxes or animated strips.
- Often conflicts with styles: marquee
- Sources: nng-banner-blindness

### `ux-no-popups` [major · evidence]
Avoid popups and splash screens on the homepage, except where legally required (cookie consent, age checks).
- Why: They are among the most disliked web design elements, per NN/g.
- Check (manual): Load the page fresh; note anything that interrupts the first view.
- While designing: Avoid popups and splash screens on the homepage except legally required consent or age checks.
- Often conflicts with styles: intro-preloader
- Sources: nng-homepage-principles

### `ux-primary-cta-above-fold` [major · evidence]
The primary call to action is visible without scrolling, with visual hierarchy built around the top task.
- Why: Attention drops sharply after the fold: 57% of viewing time was above the fold in 2018 versus 80% in 2010; 74% fell in the first two screenfuls (NN/g, 15 Apr 2018, 120 participants).
- Check (hybrid): Automated: find the primary call to action (the first visible link or button in the hero, else in main, that starts with an action verb or is drawn as a button; else the first button-like element on the page) and fail when its bounding box is not fully inside the first viewport at 1440x900 and 390x844. The evidence names the element it took and why (for example 'first filled button in the hero'). When the page's main action is something else (a board of rows, a form, a single link), mark that element with a data-primary-cta attribute: it overrides the heuristic and its bounding box is measured instead. A person confirms the element found is the page's top task and that the visual hierarchy is built around it.
- While designing: Show the primary action in the first viewport and repeat it where natural.
- Often conflicts with styles: poster, chaptered-story
- Sources: nng-scrolling-attention, nng-homepage-principles

### `ux-purpose-clear` [major · evidence]
The homepage says who you are, what you offer and how you differ, quickly, in the audience's own words.
- Why: When the purpose is not visible at a glance, potential customers leave.
- Check (manual): Five-second test: show the first screen and ask what the site is for; compare answers with the brief.
- While designing: Say in the first screen who you are, what you offer and how you differ, in the audience's words.
- Often conflicts with styles: poster, hero-type-only, interactive-art
- Sources: nng-homepage-principles

### `ux-scannable-text` [major · evidence]
Make text scannable: meaningful subheadings, short paragraphs with one idea each, lists, and the conclusion first.
- Why: In NN/g's study (Nielsen, 30 Sep 1997; sample size not stated) 79% of users always scanned and 16% read word by word. Concise text scored +58%, scannable layout +47% and the combined version +124% on usability, relative to a promotional-writing control.
- Check (manual): Read only headings, first sentences and bold text; the page should still make sense.
- While designing: Use meaningful subheadings, short paragraphs with one idea, lists and the conclusion first.
- Sources: nng-how-users-read, nng-f-pattern

### `ux-start-with-needs` [major · craft-consensus]
Start from real user needs and test assumptions with real people from the beginning.
- Why: GOV.UK and the U.S. Web Design System both list it as their first principle.
- Check (manual): Check the brief cites research, not only internal opinion.
- While designing: Start from real user needs and test assumptions with real people.
- Sources: govuk-design-principles, uswds-design-principles

### `ux-tagline-specific` [major · evidence]
Use a plain, specific tagline and headline instead of generic welcome messages or jargon.
- Why: Users scan and spend most of their time at the top; vague text wastes it.
- Check (manual): Read the headline without the logo: could any competitor say the same?
- While designing: Write a specific headline and tagline; no generic welcome text or jargon.
- Sources: nng-homepage-principles

### `ux-test-iteratively` [major · evidence]
Test usability with about five people per audience group per round, fix problems, and test again; several small rounds beat one large one.
- Why: Nielsen (18 Mar 2000): the first user finds about a third of problems (31% averaged over projects studied), five users find about 85%, and three rounds of five beat one round of fifteen; test 3 to 4 users per group for two groups and at least 3 per group for three or more. Norman (2013, ch. 6) also advises five and iterating.
- Check (manual): Run the planned rounds; record problems and fixes.
- While designing: Plan about five people per audience group per round, fix problems and test again.
- Sources: nng-five-users

### `ux-visible-navigation` [major · evidence]
Show primary navigation on desktop; on mobile show four or fewer top-level links, and use a menu only for more.
- Why: In a study with 179 participants on 6 live sites (Pernice and Budiu, 26 Jun 2016), navigation was used in 27% of desktop tasks when hidden versus 48% visible and 50% combined; hidden navigation cut content discoverability by more than 20%. On mobile the article suggests showing four or fewer top-level links, otherwise hiding some.
- Check (manual): Check whether the main sections are visible without opening a menu.
- While designing: Show primary navigation links on desktop; on mobile show four or fewer, otherwise use a disclosure menu.
- Often conflicts with styles: hamburger-only, unusual-nav, command-palette, floating-dock, anchor-only
- Sources: nng-hidden-navigation, nng-homepage-principles

### `ux-consistency` [minor · craft-consensus]
Keep labels, components and behavior consistent within the site and with common conventions.
- Why: Heuristic 4 (consistency and standards); GOV.UK says "consistent, not uniform".
- Check (manual): Audit repeated components and labels across pages.
- While designing: Reuse the same labels, components and behavior for the same function.
- Sources: nng-ten-heuristics, govuk-design-principles

### `ux-false-floor` [minor · evidence]
Avoid false floors: signal that there is more below, for example with cut-off content.
- Why: Minimalist layouts can look finished before they are.
- Check (manual): Look at the first screen: does anything suggest more content below?
- While designing: Let the next section peek in at the bottom edge so the first screen does not look finished.
- Often conflicts with styles: minimal, hero-type-only
- Sources: nng-scrolling-attention

### `ux-form-controls` [minor · evidence]
Use radio buttons instead of dropdowns for two or three options; size inputs to the expected value; state format rules up front; avoid Reset and Clear buttons.
- Why: Reduces hidden options and accidental data loss.
- Check (manual): Review each control type.
- While designing: Use radio buttons instead of dropdowns for two or three options; state formats up front; avoid Reset buttons.
- Sources: nng-web-forms

### `ux-form-layout` [minor · evidence]
Use a single column with labels close to their fields (above on mobile); only short related fields share a row.
- Why: A single column keeps people moving down the form.
- Check (manual): Check layout at desktop and mobile widths.
- While designing: Use one column with labels close to their fields (above on mobile).
- Sources: nng-web-forms

### `ux-informative-imagery` [minor · evidence]
Images carry information about the offer or brand rather than serving as decorative stock.
- Why: Decorative imagery adds weight without meaning.
- Check (manual): For each major image ask what it communicates that the text does not.
- While designing: Use images that carry information about the offer, not decorative stock.
- Sources: nng-homepage-principles

### `ux-logo-home` [minor · evidence]
The logo links to the homepage and sits where people expect it (top-left in left-to-right languages); the homepage looks distinct from interior pages.
- Why: Easy access to the starting point is a basic orientation need.
- Check (manual): Click the logo from several pages.
- While designing: Link the logo to the homepage in a findable place, top-left in left-to-right layouts.
- Often conflicts with styles: unusual-nav
- Sources: nng-homepage-principles

### `ux-mega-menu` [minor · craft-consensus]
If you use a mega menu: group options with short front-loaded labels, show each option once, keep the search visible, make it work with a keyboard and screen reader, and use hover intent (pointer still for about 0.5 s before opening).
- Why: Prevents flicker and lost context.
- Check (manual): Test with mouse, keyboard and screen reader.
- While designing: For mega menus group options with short labels, use hover intent, keep search visible and support keyboard and screen readers.
- Sources: nng-mega-menus

### `ux-minimal-motion` [minor · evidence]
Keep motion minimal on the homepage; moving elements are often mistaken for ads, and the logo, tagline and headline should stay static.
- Why: Motion draws attention away from the message and can look like advertising.
- Check (manual): Watch the first 10 seconds with and without motion.
- While designing: Keep motion minimal near the headline and primary action; keep logo, tagline and headline static.
- Often conflicts with styles: parallax, scroll-triggered, ambient-loop, text-effects, realtime-3d
- Sources: nng-homepage-principles, nng-banner-blindness

### `ux-objective-language` [minor · evidence]
Prefer plain factual statements to boastful marketing language.
- Why: Objective language scored +27% on usability relative to a promotional control (Nielsen, 30 Sep 1997; sample size not stated); users spend effort filtering out hype.
- Check (manual): Highlight superlatives and claims; each should be backed by a fact or removed.
- While designing: Prefer plain facts to boastful marketing language; back claims with proof.
- Sources: nng-how-users-read

### `ux-real-content-examples` [minor · evidence]
Show specific samples of real content (products, articles, projects) instead of only generic category links.
- Why: Concrete examples reveal what the site offers.
- Check (manual): Check that the first two screens show actual items, not only labels.
- While designing: Show real samples of products, work or articles, not only category links.
- Sources: nng-homepage-principles

### `ux-conventional-layout` [advisory · evidence]
Use conventional layouts and patterns where the user's goal is practical, so existing mental models apply; depart from convention deliberately.
- Why: Users bring expectations from other sites. NN/g recommends standard layouts for homepages.
- Check (manual): Ask whether each unconventional choice is worth its cost, and write the reason down.
- While designing: Use conventional patterns for practical goals and break convention deliberately, with a written reason.
- Often conflicts with styles: experimental, unconventional-layout, app-shell
- Sources: nng-homepage-principles, nng-ten-heuristics
