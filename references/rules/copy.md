# Quality Bar: Content and copy
Severity: blocker (never traded for style), major, minor, advisory. Labels: standard, evidence, craft-consensus, our-take.

### `copy-button-verb-label` [major · craft-consensus]
Every button and primary call to action label starts with a verb, names the outcome in 1 to 4 words, uses sentence case, and is never 'Submit', 'OK', 'Click here', 'Learn more' or 'Get started' on its own.
- Why: GOV.UK says button text describes the action and gives examples such as 'Start now' and 'Save and continue'; Mailchimp requires a verb in every button; NN/g (2026) says avoid 'Learn More'. Practitioners (Sacks 2024, UX Movement 2019) say 'Get started' hides the next step and suggest 2 to 3 words. The 1 to 4 word range is our synthesis; no source sets a hard limit (GOV.UK: none). Overlaps ux-descriptive-labels, which names only 'click here' and 'learn more'.
- Check (automated): Collect text of button, [role=button], input[type=submit] and .btn-like links. Fail if the first word is not a verb (use a verb list), if the word count is over 4, or if the label matches the blocklist: submit, ok, click here, learn more, get started, go, continue (unless a save step is stated). (tools: custom script)
- While designing: Label each button with a verb plus its object ('Book a demo', 'Download the price list').
- Often conflicts with styles: minimal, hero-type-only, quiet-luxury
- Sources: govuk-ds-button, mailchimp-web-elements, nng-ux-writing-faqs, nng-homepage-principles, sacks-get-started, uxmovement-button-labels

### `copy-error-specific-actionable` [major · craft-consensus]
Every error message names the field or problem and tells the user how to fix it in plain words; generic messages such as 'An error occurred', 'This field is required', 'Something went wrong' and raw error codes are not used without a cause and next step.
- Why: GOV.UK says to say what happened and how to fix it, with the pattern 'Enter your first name' for empty fields and 'Name must be 35 characters or less' for wrong values, and lists 'This field is required' as a generic message to avoid. NN/g (2023) says be specific, offer remedies and hide error codes. Overlaps ux-form-errors and a11y-error-identification, which require specificity but give no wording patterns.
- Check (hybrid): Trigger every validation and failure state (empty, wrong format, too long, network failure, server error). Fail any message that does not name the problem and a fix, matches the generic list, or shows a raw code. Automated part: grep message strings for the generic list. (tools: custom script, manual form testing)
- While designing: Start empty-field errors with a verb ('Enter your email address') and wrong-value errors with the field name plus 'must be'.
- Often conflicts with styles: minimal, quirky, playful
- Sources: govuk-ds-error-message, nng-error-message-guidelines, govuk-ds-validation

### `copy-expert-review-before-launch` [major · our-take]
Copy that gives legal, medical, financial or safety advice (anything where a wrong or out-of-date sentence could harm the reader) is reviewed by a qualified person before launch; until then each such passage carries a visible draft marker with a legend on the page, and the page does not ship it as final.
- Why: This is our judgement, often called 'your money or your life' (YMYL) content in search-quality writing; no source was read for this rule. NN/g (2026) says a human must check that AI-written claims are correct, which supports the principle for generated copy but is not specific to advice. A model cannot hold the licence, the jurisdiction or the current law that the advice depends on, so a draft written by a model is a draft. The marker is the same visible, non-bracket convention as for unconfirmed facts (guide protocol 3.2), so the draft is never presented as checked. Severity is major, not blocker, because an our-take rule cannot be a blocker; realize-launch applies it as a launch gate.
- Check (manual): List every passage that advises on law, health, money or safety (rights, deadlines, dosages, eligibility, 'you should', 'you must'). For each, confirm that a named qualified reviewer and a date are recorded (design/OPEN-QUESTIONS.md or the QA report), or that the passage carries the visible draft marker and its legend and the launch gate is still closed. Search the built page for the marker before launch.
- While designing: Write advice as a draft: mark it with the visible draft marker and a legend, list the reviewer you need (solicitor, clinician, adviser) in OPEN-QUESTIONS.md, and do not launch it as final until a qualified person has signed it off.
- Sources: nng-ai-editorial-process

### `copy-heading-informative` [major · craft-consensus]
Each H2 and H3 describes the content beneath it in literal terms, with generic headings ('Introduction', 'Overview', 'Features', 'Our approach', 'Why choose us') replaced by topic-specific ones, and the list of headings read alone summarises the page.
- Why: NN/g (FAQ 2026) recommends literal, informative headings that summarise what follows; GOV.UK adds that headings must be descriptive, front-loaded and removable without breaking sense, and says not to use questions as headings. Overlaps a11y-headings-labels and ux-scannable-text; this rule adds the generic-heading blocklist and the 'read headings alone' test.
- Check (hybrid): Extract the heading outline. Fail any heading matching the blocklist (case-insensitive: introduction, overview, features, benefits, our approach, why us, about, welcome). Then read the outline alone: a reader should be able to say what the page offers. (tools: custom script)
- While designing: Write each heading as the finding of its section, so the headings alone tell the story.
- Often conflicts with styles: expressive-type, poster, chaptered-story, quirky
- Sources: nng-ux-writing-faqs, govuk-writing-structure, mailchimp-web-elements, digital-gov-plain-language

### `copy-headline-swap-test` [major · craft-consensus]
The H1 and hero subhead name a concrete outcome, offer or audience, and fail a swap test: a direct competitor could not publish the same text unchanged without lying; template headlines of the form 'The [adjective] [category] for modern [audience]' are not used.
- Why: NN/g says to explain what the organisation does and why to choose it, and to replace generic welcome lines with specific taglines (2024). NN/g's headline guidance replaces 'Make better, faster decisions' with a named benefit (2015). Two practitioner write-ups (Superdesign 2026, Landing Doctor) independently flag the mad-lib hero and 'platform for teams' headlines as generic. Overlaps existing ux-tagline-specific, which does not give the swap test or the template pattern.
- Check (manual): Read the H1 and subhead alone. (1) Does it say what is offered and for whom? (2) Paste it with a competitor's name: does it still read true? If yes, fail. (3) Fail if it matches the template 'The [AI-powered|modern|all-in-one] [noun] for [teams|businesses|everyone]'.
- While designing: Write the headline as the result one named buyer gets, using a noun or number only this product can claim.
- Often conflicts with styles: hero-type-only, poster, quiet-luxury, expressive-type, standout-hero
- Sources: nng-homepage-principles, nng-headings-pickup-lines, superdesign-generic-landing, landingdoctors-ai-landing

### `copy-jargon-acronyms` [major · craft-consensus]
Every acronym and specialist term that is not universally known is expanded or explained where it appears in headings, navigation and buttons, and at first use in body copy; branded feature names are always accompanied by a plain description.
- Why: NN/g says to spell out acronyms on every use because readers scan and miss first-use definitions, and to treat branded labels as jargon; GOV.UK says explain at first use and write unfamiliar abbreviations out in titles. The sources differ on 'every use' versus 'first use'; the rule takes the stricter reading only for the places people scan.
- Check (hybrid): Extract all-caps tokens of 2 or more letters and capitalised product names from headings, nav and buttons; confirm each is expanded or described adjacent. Confirm first body use is expanded. Whitelist PDF, FAQ, URL. (tools: custom script)
- While designing: Write the full phrase the first time and in every heading or button, and describe each branded name in plain words next to it.
- Often conflicts with styles: minimal, quiet-luxury
- Sources: nng-ux-writing-faqs, govuk-writing-clear-language, govuk-writing-titles, nng-plain-language-experts, nng-homepage-principles

### `copy-link-text-unique-destination` [major · craft-consensus]
Link text makes sense out of context and is brief; identical link text always goes to the same destination, different destinations never share the same text; the word 'link' and 'click here' are not in link text; external, new-window and file links say so, with file format and size for downloads.
- Why: GOV.UK: do not reuse the same text for different pages, state when a link leaves the site, give file type and size (its example is 'PDF, 19.5KB'). WebAIM: omit 'link', keep it brief, make it understandable out of context, put 'opens in a new window' after the main text. Overlaps a11y-link-purpose (WCAG 2.4.4) and ux-descriptive-labels; this adds the duplicate-text, destination-notice and file-notice checks.
- Check (automated): Collect all anchors with accessible names. Fail if two different hrefs share the same name, if a name matches /^(click here|here|more|read more|link|this)$/i or contains 'link', if an href ends in a document extension without format and size in the name, or if target=_blank lacks a notice placed after the main text. (tools: axe-core, custom script)
- While designing: Write link text that names the destination and say 'PDF, 2 MB' or 'opens in a new window' when it applies.
- Often conflicts with styles: minimal, unusual-nav
- Sources: govuk-writing-links, webaim-hypertext, mailchimp-web-elements

### `copy-no-placeholder-text` [major · our-take]
Shipped pages contain no lorem ipsum, bracketed placeholders ('[Company]', 'Your tagline here'), default template text, or chatbot residue such as 'Certainly!', 'I hope this helps', 'Would you like me to', or 'As an AI'.
- Why: Wikipedia's guide lists chatbot leftovers ('Certainly!', 'I hope this helps') as a sign of pasted output. Landing Doctor lists placeholder logos as a tell. A published placeholder is a functional content failure. No source measures how often this happens. Not a placeholder: a real fact the owner has not confirmed yet, shown in a prototype with the visible, non-bracket assumption marker and legend from the guide protocol (3.2), listed in OPEN-QUESTIONS.md; it is a draft state, not a ship state, and the launch step refuses while any remain.
- Check (automated): Grep rendered text and alt attributes for: lorem ipsum, \[.*\], 'your (company|tagline|text) here', 'certainly!', 'I hope this helps', 'as an AI', 'let me know if', 'sample text', 'placeholder'. (tools: grep, custom script)
- While designing: Leave nothing in brackets: ask for the missing fact or write real copy before finishing. If a real fact is still unconfirmed, show it with the visible assumption marker and legend (dotted underline class plus a footer line) and list it in OPEN-QUESTIONS.md; never brackets, and it must be resolved before launch.
- Sources: wikipedia-signs-ai-writing, landingdoctors-ai-landing

### `copy-proof-verifiable` [major · our-take]
Statistics, testimonials, client logos, awards and superlatives ('#1', 'trusted by 10,000 teams', 'increase conversions 300%') are either backed by a named, checkable source on the page or removed; nothing is invented to fill a layout.
- Why: Landing Doctor lists fabricated or unsourced proof (invented testimonials, placeholder logos, precise unsourced stats) as a tell of generated pages; Wikipedia's guide lists vague attribution ('experts argue') as a pattern; NN/g (2026) says AI never certifies that a claim is correct, so a human must check. Mailchimp says to keep claims grounded. Overlaps ux-objective-language; this adds the verification step and the ban on invented proof. Plain facts that are given or agreed (a price, an hour) but not yet confirmed are not proof claims: show them in a prototype with the visible assumption marker and legend (guide protocol 3.2) and list them as open questions; this rule still bans invented customers, numbers, quotes and press, which are removed, not marked.
- Check (manual): List every number, quote, logo and superlative on the page. For each, record the source and confirm the customer or study exists and consented. Remove any with no source. Also grep for placeholder names (John Doe, Acme, Company Name).
- While designing: Use only claims and customers from the supplied brief, and mark any missing proof as a content gap instead of inventing it. A plain fact the owner has not confirmed may stay in a prototype only with the visible assumption marker and legend, listed in OPEN-QUESTIONS.md; invented proof is removed.
- Often conflicts with styles: standout-social-proof
- Sources: landingdoctors-ai-landing, wikipedia-signs-ai-writing, nng-ai-editorial-process, mailchimp-writing-principles

### `copy-reading-grade` [major · craft-consensus]
Body copy for a general audience scores at or below US grade 9 on a readability formula (target grade 6 to 8); specialist audiences may go to grade 10 to 12 only when the audience is documented. For ESL, low-literacy or UK public-service audiences the target is lower: grade 5 or below, or CEFR B1 and GOV.UK-style plain language (our take).
- Why: NN/g says aim for grades 6 to 8 for general audiences and 10 to 12 for experts, and that plain language helps experts too (2017 article; 2026 FAQ). WCAG 3.1.5 uses more than 9 years of school as the trigger for needing a summary. digital.gov says to write for the 8th grade only if the readers are 8th graders, so the target depends on audience. The lower target for ESL, low-literacy and UK public-service readers (grade 5 or below, CEFR B1, GOV.UK plain language) is our take: grades are a US schooling measure and a poor fit for a UK service, so the brief should name the audience's target and how it was checked. ESL group note: offer a translation or an interpreter where the service really can (translated pages linked with lang and hreflang, passages in another language marked with lang), avoid idioms and phrasal-verb puns, write dates and numbers in one unambiguous form, and put the action first.
- Check (hybrid): Automated (apps/audit): Flesch-Kincaid grade, with an English-only syllable heuristic, on the page's visible p, li, blockquote and dd text (headings, navigation, forms, headers, footers and buttons left out). It needs 80 words and <html lang> starting with en, otherwise the result is manual. Generic thresholds only: fail above grade 10, needs a person from 8 to 10, pass below 8. A pass never shows that a plain-language target (grade 5 or lower, CEFR B1, ESL or low-literacy readers) is met, and proper names and technical terms inflate the score. A person confirms the audience and the target the brief names, and scores the page by hand where the scorer did not run. (tools: Hemingway, textstat)
- While designing: Use short, common words and one clause per sentence, then check the grade score before finishing. For ESL, low-literacy or UK public-service readers aim at grade 5 or below (CEFR B1, GOV.UK plain language), offer translations with lang attributes and an interpreter where you really have one, and avoid idioms.
- Often conflicts with styles: editorial, serif-editorial, quiet-luxury
- Sources: nng-ux-writing-faqs, nng-plain-language-experts, nng-genai-write-for-web, wcag-understanding-reading-level, digital-gov-plain-language

### `copy-sentence-length` [major · craft-consensus]
No sentence in body copy is longer than 25 words, and the average sentence length across a page's body copy is 20 words or fewer.
- Why: GOV.UK says to split any sentence over 25 words; NN/g (Loranger, 2017) suggests 15 to 20 words at most. The two sources differ slightly, so the rule uses 25 as the hard cap and 20 as the average. NN/g also reports that users read only about 20 to 28% of the text on a page.
- Check (hybrid): Automated (apps/audit): extract the visible text of p, li, blockquote and dd elements (headings, navigation, forms, headers, footers and buttons left out), split on sentence terminators and line ends, count words per sentence. Needs 80 words and <html lang> starting with en, otherwise the result is manual. Fail when the mean exceeds 20 words or more than 25% of sentences are over 25 words; needs a person when only some sentences are over 25 (the splitter can join sentences around abbreviations); pass when none is. A person checks the long sentences it lists and any legal text. (tools: custom script, Hemingway-style readability checker)
- While designing: Write body sentences of about 15 words, split any that pass 25, and read each aloud before keeping it.
- Often conflicts with styles: editorial, serif-editorial, long-scroll-narrative
- Sources: govuk-writing-clear-language, nng-plain-language-experts, ms-brand-voice

### `copy-specific-over-abstract` [major · craft-consensus]
Feature and benefit copy replaces abstract adjectives (powerful, seamless, robust, intuitive, innovative, cutting-edge, next-generation, world-class) with a measurable change, a named workflow or a concrete example, and each feature block opens with a concrete detail rather than an icon plus a two-word title.
- Why: NN/g (2015) turns 'Make better, faster decisions' into a named benefit and warns against hype; NN/g (2024) says avoid feature-driven wording and jargon and prefer concrete examples over umbrella terms. Landing Doctor, Superdesign and Microcopy Secrets independently recommend replacing vague adjectives and 'fits any product' benefit lines with specifics. Overlaps ux-real-content-examples and ux-objective-language.
- Check (hybrid): Grep for the abstract-adjective list. For each hit, require a number, a named object or a verifiable example in the same sentence, otherwise rewrite. Check that no three feature cards share the same structure of icon, two-word title and filler sentence. (tools: custom script)
- While designing: For every adjective, write the fact that made you choose it and use the fact instead.
- Often conflicts with styles: quiet-luxury, minimal, hero-type-only
- Sources: nng-headings-pickup-lines, nng-homepage-principles, landingdoctors-ai-landing, superdesign-generic-landing, microcopy-secrets-landing-words

### `copy-active-voice` [minor · craft-consensus]
Headings, buttons, error messages and calls to action are written in the active voice, and body sentences use the passive only where the actor is unknown or unimportant.
- Why: GOV.UK and digital.gov both prefer active voice; digital.gov says passive hides who does what and calls it one of the biggest problems in government writing; Mailchimp and Microsoft also say active. Neither GOV.UK nor digital.gov gives a percentage limit.
- Check (hybrid): Run a passive-voice detector (be-verb plus past participle) over all copy. Any hit in a heading, button, error or CTA fails; review body hits for a named actor. (tools: custom script, write-good)
- While designing: Name the actor first: write 'We send your invoice', not 'Your invoice will be sent'.
- Sources: govuk-writing-clear-language, digital-gov-plain-language, mailchimp-voice-tone

### `copy-alt-text-writing` [minor · craft-consensus]
Alt text states the image's purpose in context in about 150 characters or fewer, starts with the key words, does not begin with 'image of' or 'photo of', does not repeat adjacent text, does not contain keyword lists, and is empty for decorative images.
- Why: NN/g (2024) gives about 150 characters, purpose from context, no leading 'image', empty alt for decorative images and says AI is unreliable at writing alt text from scratch; WebAIM (2021) says brief, no 'image of', no keyword stuffing, no repeat of nearby text, and gives no numeric limit. Overlaps a11y-alt-text; this adds length and wording checks.
- Check (automated): For every img with non-empty alt: fail if length exceeds about 150 characters, starts with /^(image|photo|picture|graphic) of/i, equals the text of a nearby caption or heading, or contains 3 or more comma-separated keywords. Review decorative images for alt="". (tools: axe-core, custom script)
- While designing: Write alt text that says what the image adds here in one short sentence, or leave it empty if it adds nothing.
- Sources: nng-write-alt-text, webaim-alttext

### `copy-cta-next-step` [minor · our-take]
Each primary call to action is followed within the same viewport by a short line saying what happens next or what it costs (for example 'No card needed' or 'Takes 2 minutes'), and a repeated generic CTA is not used as filler.
- Why: NN/g (2025) says CTAs should reduce uncertainty and give an easy next step. Landing Doctor lists the repeated decorative 'Get started' with no stated next step as a tell of generic page copy and recommends reassurance under the button. The second source is a vendor and gives no data, so treat the exact pattern as practice, not proof.
- Check (manual): For each primary CTA, check the adjacent text states the next step, cost or commitment truthfully. Fail if the same unexplained CTA label repeats in 3 or more sections.
- While designing: Put one factual reassurance line under each primary button naming what happens after the click.
- Often conflicts with styles: minimal, quiet-luxury, hero-type-only
- Sources: nng-3is-microcopy, landingdoctors-ai-landing, sacks-get-started

### `copy-error-no-blame-words` [minor · craft-consensus]
Error and warning text contains none of: invalid, illegal, incorrect, forbidden, prohibited, 'you forgot', 'please', 'sorry', 'oops', and uses no jokes; humour is allowed only for a rare complete system failure.
- Why: GOV.UK lists these as words to avoid (it says 'please' implies a choice and 'sorry' does not help fix the problem); NN/g avoids 'invalid, illegal, incorrect', says humour wears thin on repeated errors, and allows novelty only for rare total failures. Mailchimp's guide also says forced humour can be worse than none. Sources agree.
- Check (automated): Grep all validation, toast and error-page strings for the banned list (case-insensitive) and for exclamation marks. Manually confirm that any jokes appear only on a whole-site failure page. (tools: custom script)
- While designing: Describe what the system needs from the user in neutral words, with no apology and no joke.
- Often conflicts with styles: quirky, playful, memphis-playful, edgy
- Sources: govuk-ds-error-message, nng-error-message-guidelines, mailchimp-voice-tone

### `copy-explicit-option-differences` [minor · our-take]
Where a page offers plans, tiers or products, the differences between them are stated explicitly with units and precise labels (for example 'Up to 5 users' not 'Small team'), and all costs are shown in one place.
- Why: NN/g (2024) says implicit differences lead to wrong choices, recommends explicit units and precise labels, and says to show all costs together. Only one source (NN/g, updating a 2013 Nielsen article), so this is not marked craft-consensus.
- Check (manual): For each comparison, confirm each plan label states what differs, numbers have units, and the total price including recurring fees can be read without leaving the page.
- While designing: Name what differs between options in the label and give every number its unit.
- Often conflicts with styles: minimal, quiet-luxury, standout-pricing
- Sources: nng-explicit-differences

### `copy-heading-front-load` [minor · craft-consensus]
Headlines and headings make sense out of context (in a search result, a link list or a feed), put the key term in the first few words, and drop nonessential words.
- Why: NN/g (Loranger, 2015) says headlines often appear alone, that readers focus on the first words, and that long headlines get truncated on small screens; GOV.UK says front-load headings. The article gives no study numbers. Overlaps ux-front-load, which covers the idea generally.
- Check (manual): For each H1 and H2, read it with no surrounding text. Fail if the topic cannot be named, if the key term is not within the first 3 words, or if removing a word changes nothing.
- While designing: Lead each heading with its subject noun and delete any word that does not change its meaning.
- Often conflicts with styles: expressive-type, poster, chaptered-story
- Sources: nng-headings-pickup-lines, govuk-writing-structure, govuk-writing-titles

### `copy-lists-for-parallel-items` [minor · craft-consensus]
Sequential steps are a numbered list and 3 or more parallel items are a bulleted list, not a comma-run sentence or a long paragraph.
- Why: GOV.UK and digital.gov say to use bullets and numbered steps to reduce duplication and aid scanning; NN/g (2017) lists bullets and tables for scanning; NN/g (2025) found AI output often presented lists as plain paragraphs. The '3 or more' threshold is our choice. Overlaps ux-scannable-text.
- Check (hybrid): Flag paragraphs containing 3 or more comma-separated parallel items or the words 'first, second, third', and steps written in prose. Confirm real ul or ol elements are used. (tools: custom script)
- While designing: Turn any list of three or more items or any procedure into a proper list element.
- Often conflicts with styles: editorial, serif-editorial
- Sources: govuk-writing-structure, digital-gov-plain-language, nng-plain-language-experts, nng-genai-write-for-web

### `copy-no-all-caps-text` [minor · craft-consensus]
Sentences, paragraphs, headings of more than 3 words and button labels are not set in all capitals, either in the source text or with text-transform: uppercase; short eyebrow labels of 3 words or fewer are the only exception.
- Why: GOV.UK says no block capitals for large amounts of text because they are hard to read and can read as shouting; digital.gov says the same; UX Movement says all caps is loud and harder to read. The 3-word allowance is our threshold; the sources only say 'large amounts of text'.
- Check (automated): Flag text nodes in source with 4+ words entirely uppercase, and elements with computed text-transform: uppercase whose text has more than 3 words, or that are buttons. (tools: custom script, Playwright)
- While designing: Keep headings and buttons in sentence case and use uppercase only for one- to three-word labels.
- Often conflicts with styles: brutalism, neo-brutalist, edgy, condensed, oversized-type, poster, expressive-type
- Sources: govuk-writing-tone, digital-gov-plain-language, uxmovement-button-labels

### `copy-no-buzzwords` [minor · craft-consensus]
Headlines, buttons and subheads contain none of the stock marketing verbs and metaphors (unlock, unleash, empower, supercharge, elevate, revolutionize, transform, harness, leverage, streamline, game-changer, journey, tapestry, landscape, realm, delve), and body copy has no more than 2 distinct ones per page.
- Why: GOV.UK, Google and Microsoft separately tell writers to avoid buzzwords, jargon and figurative language; Microcopy Secrets (2024) and ContentBeta (2026) list unlock, unleash, empower, supercharge, game-changer as empty; Wisp (2024) and Wikipedia list tapestry, delve, realm, crucial, pivotal as overused. The thresholds (zero in headlines, 2 in body) are ours. Word lists drift by model era (Wikipedia) and single words are weak evidence (Wikipedia, TechCrunch), so this rule is about empty wording, not about detecting AI.
- Check (automated): Grep headings, buttons, hero text and meta descriptions for the list (case-insensitive, word-boundary); fail on any hit. Count distinct hits in body copy; fail above 2 per page. (tools: custom script)
- While designing: State the plain action in ordinary words ('save', 'connect', 'fix') and drop the stock marketing verb.
- Often conflicts with styles: luxury, opulent, quiet-luxury
- Sources: govuk-writing-clear-language, google-dev-tone, ms-brand-voice, microcopy-secrets-landing-words, contentbeta-ai-words, wisp-ai-phrases, wikipedia-signs-ai-writing

### `copy-no-filler-openers` [minor · our-take]
Copy does not open or close with filler framing such as 'In today's fast-paced world', 'In the realm of', 'It is important to note', 'Whether you're a X or a Y', 'In conclusion', 'stands as a testament to', or an inspirational closing line.
- Why: Wisp (2024) lists 'In the realm of' and 'It is important to understand'; ContentBeta (2026) lists 'in today's world' and 'digital age'; Wikipedia lists 'stands as a testament', 'pivotal', canned 'It's important to note' (2023 to 2024) and 'In conclusion' summaries (about 2023, since less frequent); RAXXO lists inspirational closings. Google says to cut filler like 'please note'. Corroborated by at least three, but the exact phrases date quickly.
- Check (automated): Grep for the phrase list at the start and end of paragraphs and sections; fail on any hit. Manually review any section whose final sentence only restates the heading. (tools: custom script)
- While designing: Start each section with its first real fact and stop when the point is made.
- Often conflicts with styles: editorial, chaptered-story
- Sources: wisp-ai-phrases, contentbeta-ai-words, wikipedia-signs-ai-writing, raxxo-ai-tells, google-dev-tone

### `copy-no-idioms-puns` [minor · craft-consensus]
Headlines, navigation labels and calls to action contain no idioms, puns, slang, pop-culture references or metaphors that need decoding; any playful line sits next to a plain one that states the offer.
- Why: NN/g (2015) says cute, faddish or idiomatic headlines sound inauthentic and confuse non-native speakers; Google's style guide says to avoid slang, figurative language and pop-culture references; Mailchimp says avoid slang. NN/g's 2026 microcopy article ranks 'character' last, after clarity and concision, so humour is allowed only after clarity.
- Check (manual): Read each headline, nav label and button aloud to someone who does not know the product. Fail where a literal reading misleads or the meaning needs a cultural reference. Confirm one plain statement of the offer is within the first screen.
- While designing: Say the plain thing in the headline and put any wit in a supporting line.
- Often conflicts with styles: quirky, playful, memphis-playful, edgy, neo-brutalist, brutalism
- Sources: nng-headings-pickup-lines, google-dev-tone, mailchimp-voice-tone, nng-3cs-microcopy

### `copy-no-please-filler` [minor · craft-consensus]
Instructions and interface text do not use 'please', 'please note', 'simply', 'just', 'easy', 'quickly', 'it's that simple', or exclamation points.
- Why: GOV.UK: no 'please' or 'please note'. Google: no 'please', no 'simply/easy/quickly/it's that simple', avoid exclamation points, cut filler such as 'please note' and 'at this time'. Two independent guides agree. Marketing headlines are out of scope; this is for instructions and UI text.
- Check (automated): Grep UI strings, form hints, instructions and help text for the banned list; exclude marketing headlines and testimonials. (tools: custom script)
- While designing: Give instructions as plain imperatives ('Enter your postcode') with no softeners and no exclamation marks.
- Often conflicts with styles: friendly, playful, quirky
- Sources: govuk-writing-tone, google-dev-tone, govuk-ds-error-message

### `copy-page-title-length` [minor · craft-consensus]
Each page's title element is unique, 65 characters or fewer, names what the page offers with the key term first, and meta descriptions are about 160 characters.
- Why: GOV.UK sets 65 characters including spaces and says titles must be unique and use search terms; NN/g (2026) says page titles over 60 characters tend to be truncated and descriptions should be about 160 characters. The sources differ by 5 characters. Existing a11y-page-title only requires that a title exist and describe purpose.
- Check (automated): Crawl every page; assert title length is 65 or less, titles are unique across the site, and description length is 150 to 160. (tools: Lighthouse, custom crawler)
- While designing: Write a unique title under 60 characters that starts with the page's main subject.
- Sources: govuk-writing-titles, nng-3cs-microcopy

### `copy-paragraph-length` [minor · craft-consensus]
Each body paragraph has one idea and at most 5 sentences; marketing and product pages aim for 3 sentences or fewer.
- Why: GOV.UK sets 5 sentences as the maximum; NN/g (Loranger, 2017) says one idea per paragraph. The 3-sentence marketing target is our choice, not stated by either source.
- Check (automated): Count sentences in each p element. Fail above 5; warn above 3 on landing and product pages. Manual spot check that each paragraph carries one idea. (tools: custom script)
- While designing: Start a new paragraph whenever the idea changes and stop at five sentences.
- Often conflicts with styles: editorial, serif-editorial, long-scroll-narrative
- Sources: govuk-writing-clear-language, nng-plain-language-experts

### `copy-plain-words` [minor · craft-consensus]
Copy uses short everyday words (for example 'buy', 'help', 'about') instead of 'purchase', 'assist', 'approximately', and avoids stacking nominalizations (-tion, -ment, -ance nouns) where a verb works.
- Why: GOV.UK lists those exact swaps and notes that -ion and -ment words lengthen sentences; digital.gov calls hidden verbs a weakness and prefers the strongest verb form; Microsoft says to use short everyday words and prune every excess word.
- Check (hybrid): Grep body copy for a banned-word list (utilize, leverage, purchase, assist, approximately, commence, facilitate, in order to, prior to, subsequent to, endeavour, numerous) and flag sentences whose main verb is 'make/take/give/have/achieve + -tion noun'. Review flags manually. (tools: custom script)
- While designing: Pick the shorter word and the plain verb ('use', not 'utilize'; 'decide', not 'make a decision').
- Often conflicts with styles: quiet-luxury, serif-editorial
- Sources: govuk-writing-clear-language, digital-gov-plain-language, ms-brand-voice, google-dev-tone

### `copy-section-content-drives-structure` [minor · our-take]
The section order and number of feature blocks on a page follow the audience's decisions and objections (documented in the brief), not the default sequence hero, logo bar, three feature cards, testimonial, pricing, FAQ, CTA, and feature cards do not carry emoji as icons.
- Why: Superdesign (2026) and Landing Doctor independently name the stock section order and three identical feature cards as tells; Superdesign also names emoji or thin-line icons on cards, and Wikipedia lists emoji at the start of headings or list entries as a possible sign. Landing Doctor recommends answering the buyer's top reasons not to convert near each CTA. No data is given by either vendor.
- Check (manual): Write the page's section order and the question each section answers. Fail if the order matches the stock sequence with no documented reason, if three or more cards share identical structure, or if emoji are used as feature icons or heading prefixes.
- While designing: Order sections by the questions this buyer asks, and vary block sizes to fit the content.
- Often conflicts with styles: saas-stack, bento-grid, playful
- Sources: superdesign-generic-landing, landingdoctors-ai-landing, wikipedia-signs-ai-writing

### `copy-summary-first` [minor · craft-consensus]
Every article, guide or long section (more than roughly 300 words) opens with a one- or two-sentence summary that states the conclusion, and each section's first sentence carries its main point.
- Why: GOV.UK says write a summary at the top and put the most important information first; digital.gov says summarize lengthy documents at the start; NN/g (2025, 2026) recommends the inverted pyramid and found AI answers often buried the overview in the conclusion. The 300-word threshold is our choice. Overlaps ux-front-load.
- Check (manual): For each long page or section, read only the first sentence: does it state the main point? Fail if the summary appears last or is missing.
- While designing: State the conclusion first and add detail after it.
- Often conflicts with styles: chaptered-story, long-scroll-narrative, editorial
- Sources: govuk-writing-structure, digital-gov-plain-language, nng-ux-writing-faqs, nng-genai-write-for-web, nng-plain-language-experts

### `copy-tone-fits-context` [minor · craft-consensus]
Tone is adjusted to the reader's situation: payments, errors, legal, security and account-deletion text is neutral and literal, with no jokes, slang or hype.
- Why: Mailchimp says tone should follow the reader's emotional state and not to force humour; NN/g (2023) says avoid humour in errors; Microsoft says adapt tone from serious to lighthearted to fit context; NN/g (2026) warns AI can approximate tone but cannot predict how it lands.
- Check (manual): List the copy on checkout, error, security, deletion, cancellation and legal surfaces; fail any joke, exclamation point or hype word.
- While designing: Keep personality in marketing sections and switch to plain neutral wording wherever money, errors or risk appear.
- Often conflicts with styles: quirky, playful, edgy, memphis-playful
- Sources: mailchimp-voice-tone, nng-error-message-guidelines, ms-brand-voice, nng-ux-writing-faqs

### `copy-voice-consistent` [minor · craft-consensus]
The site has a written voice sheet (3 to 4 trait words, each with a do and a don't example), and copy sampled from hero, navigation, buttons, errors, footer and 404 page is consistent on person (you/we), contractions, spelling variant and formality.
- Why: NN/g (2026), Mailchimp and Microsoft all say keep voice constant while tone varies; GOV.UK says address the reader as 'you'. Inconsistent copy is also a sign of copy pasted from different sources, which is a common failure of generated pages (hypothesis; no source measures it).
- Check (hybrid): Automated: count 'we/our' versus third-person ('users', 'customers') per page, contraction use, and US versus UK spelling pairs (color/colour); fail on mixed spelling. Manual: sample 6 surfaces and compare against the voice sheet. (tools: custom script)
- While designing: Fix the voice in four words with examples before writing, then speak to the reader as 'you' throughout.
- Often conflicts with styles: experimental, quirky
- Sources: nng-ux-writing-faqs, mailchimp-voice-tone, ms-brand-voice, govuk-writing-tone

### `copy-em-dash-restraint` [advisory · our-take]
Em dashes are absent from headings, buttons and labels and appear no more than about once per 300 words of body copy.
- Why: Three sources report em-dash overuse in AI drafts: Wikipedia's guide (heavy use in place of commas, parentheses or colons, formulaic punch-up), Bullock (her own count: about 1 per 130 words in 24 AI-first drafts against about 1 per 850 words in 15 human pieces), and Monteiro (asserted, no data). All are anecdotal or small, Wikipedia says the sign works only with others, and Wikipedia also notes newer models reportedly avoid em dashes. The 300-word threshold is ours.
- Check (automated): Count U+2014 in visible text; fail any in headings, buttons, nav or labels; fail if body density exceeds 1 per 300 words. (tools: custom script)
- While designing: Use periods, commas or colons instead of em dashes, and keep them out of headings entirely.
- Often conflicts with styles: editorial, serif-editorial, newspaper
- Sources: wikipedia-signs-ai-writing, bullock-ai-dashes, monteiro-em-dash

### `copy-microcopy-length` [advisory · craft-consensus]
Interface microcopy (button and link labels, form hints, tooltips, error messages, empty states) is under 3 sentences, with the key information in the first words.
- Why: NN/g defines microcopy as under 3 sentences and ranks clarity first, then concision, then character (2025 and 2026 articles); it warns that key details get truncated when copy is too long. Microsoft says to prune every excess word.
- Check (automated): Collect microcopy elements (labels, hints, tooltips, alerts, empty states) and count sentences; fail at 3 or more. (tools: custom script)
- While designing: Cut hint and error text to one or two sentences and move longer explanations to a linked page.
- Sources: nng-ux-copy-sizes, nng-3cs-microcopy, ms-brand-voice

### `copy-no-stock-rhetoric` [advisory · our-take]
A page uses at most one negative-parallelism construction ('not X, it's Y', 'not only... but also', 'No X. No Y. Just Z.'), at most one slogan of three parallel short items ('Save time. Work smarter. Scale faster.'), and no self-answered rhetorical question openers ('The result?').
- Why: Corroborated by two independent sources: Wikipedia's guide lists negative parallelism and the rule of three; ContentBeta (2026) lists 'It's not about X, it's about Y', 'No X. No Y. Just Z.' and 'The result?'. RAXXO and Superdesign add the triad ('works with any product'). Wikipedia warns that humans also write these, so frequency, not presence, is the signal. The 'one per page' limit is ours.
- Check (hybrid): Regex for /not (just|only|about)? .{3,40}[,;] (it's|but|it is)/i, /\bno \w+\. no \w+\. just/i, sentences of the form 'X. Y. Z.' with each under 4 words, and short-question-then-answer lines (looked for only in headings, paragraphs, list items and quotes, not in form labels, legends or buttons, where a question with a hint such as '(optional)' is not rhetoric). Count hits per page; fail above 1 of each kind. (tools: custom script)
- While designing: Say the claim once and directly, and use a list of two or four only when the items really are distinct. A self-answered label such as 'What is happening? (optional)' can be a false positive of the detector (a question with a hint is not rhetoric), but rewrite it anyway as a plain statement label ('What is happening (optional)').
- Often conflicts with styles: poster, hero-type-only, expressive-type, quirky
- Sources: wikipedia-signs-ai-writing, contentbeta-ai-words, raxxo-ai-tells, superdesign-generic-landing

### `copy-reading-level-companion` [advisory · standard]
Any text that needs more than lower secondary education (more than 9 years of school) to read has a plain-language summary or an easier version on the same page, or the page records the conscious exception.
- Why: WCAG 2.2 SC 3.1.5 (AAA) requires a companion for text above lower secondary level; proper names and titles are excluded, and each language that is at least 5% of the content is assessed separately. AAA is not required for conformance, hence advisory.
- Check (hybrid): Compute grade per page as in copy-reading-grade. For any section above grade 9, confirm a summary at grade 9 or lower exists (technique G86) or an illustration or easier version (G103, G153). (tools: Hemingway, textstat)
- While designing: Open any complex section with a two-sentence summary written at a plain reading level.
- Often conflicts with styles: editorial, serif-editorial
- Sources: wcag-understanding-reading-level

### `copy-sentence-case` [advisory · craft-consensus]
Buttons, headings and navigation labels use sentence case consistently across the site.
- Why: Mailchimp, GOV.UK (buttons), Microsoft and UX Movement all prescribe sentence case; Google says to match the page's existing capitalization. Mailchimp itself uses title case for form titles, so sources are not perfectly aligned. Wikipedia's AI-writing guide lists title-case section headings as a possible tell, but that is a single source about encyclopedia articles.
- Check (automated): For headings, buttons and nav items, flag strings where 3 or more words after the first start with a capital letter (excluding proper nouns); confirm the style is the same across all pages. (tools: custom script)
- While designing: Capitalise only the first word and proper nouns in every heading, button and nav label.
- Often conflicts with styles: newspaper, serif-editorial, luxury
- Sources: mailchimp-web-elements, govuk-ds-button, ms-brand-voice, uxmovement-button-labels, google-dev-ui-elements
