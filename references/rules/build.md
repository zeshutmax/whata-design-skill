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
