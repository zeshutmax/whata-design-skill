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
