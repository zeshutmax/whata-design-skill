# Quality Bar: Accessible components and cognitive accessibility
Severity: blocker (never traded for style), major, minor, advisory. Labels: standard, evidence, craft-consensus, our-take.

### `a11y-captions-live` [blocker · standard]
Live audio in synchronized media (live stream, webinar, event broadcast) has captions that include speech, speaker identification and significant non-speech sounds.
- Why: WCAG 1.2.4 (AA). It targets broadcasts, not two-way calls in web apps; live means captured from a real event with at most a broadcast delay; fully generated content is not live.
- Check (manual): If the page embeds a live stream, enable captions in the player during the live event and confirm they track speech; otherwise mark not applicable. (tools: screen reader, video player controls)
- While designing: If you embed a live stream, use a player and a captioning service that supply live captions.
- Often conflicts with styles: hero-video, event-site
- Sources: wcag-understanding-captions-live, wcag-22-quickref

### `a11y-multiple-ways` [blocker · standard]
Each page in a set of pages (other than steps or results of a process) can be reached by at least two of: links from related pages, table of contents, site map, search, a list of links to all pages, or links to all pages from the home page.
- Why: WCAG 2.4.5 (AA). The Understanding page says very small sites can satisfy this with links from the home page. Example pairings: search plus category list.
- Check (manual): Pick 3 inner pages and show two independent routes to each (nav + search, nav + sitemap, home page links + previous/next). Process pages (checkout steps, search results) are exempt.
- While designing: Provide main navigation and a second route (search, sitemap or footer index) on every multi-page site.
- Often conflicts with styles: anchor-only, unusual-nav, hamburger-only, command-palette, unconventional-layout
- Sources: wcag-understanding-multiple-ways, wcag-22-quickref

### `comp-dialog-focus` [blocker · standard]
Opening a modal dialog moves focus into it, Tab and Shift+Tab cycle only within it, Escape closes it, a visible close or Cancel button exists, and closing returns focus to the control that opened it (or to a logical next target if that control is gone).
- Why: These are the APG keyboard and focus rules for modal dialogs; the close button is 'strongly recommended' there. Initial focus guidance: first focusable by default; a static start element for long or structured content; least destructive action for irreversible steps.
- Check (manual): Keyboard only: activate the opener, verify focus is inside; Tab through the whole dialog and confirm wrap; press Escape and confirm close and focus on the opener; confirm a visible close control exists. (tools: keyboard, playwright)
- While designing: On open focus the first control (or the start of long content), trap Tab, wire Escape and a visible Close button, and restore focus to the opener on close.
- Often conflicts with styles: glassmorphism, interactive-art
- Sources: apg-dialog-modal, wcag-22-quickref

### `a11y-coga-allow-paste-autofill` [major · craft-consensus]
Password and code fields allow pasting and password-manager autofill; fields use correct autocomplete attributes; the site does not block browser extensions or assistive add-ons.
- Why: COGA 4.7.1 says password fields allow pasting; 4.9.2 says make sure password managers and spell checkers work and do not block extensions; 4.9.4 asks for HTML autocomplete on common fields. Overlaps a11y-accessible-auth and a11y-input-purpose.
- Check (automated): In login/signup: paste into password and confirm it is accepted; check autocomplete tokens (username, current-password, new-password, email, one-time-code); search for onpaste preventDefault handlers. (tools: playwright)
- While designing: Never block paste on inputs and set autocomplete tokens on every credential and contact field.
- Sources: coga-usable, wcag-22-quickref

### `a11y-status-role-choice` [major · standard]
Non-blocking status messages (results count, success, progress, cart updated) use role=status or an equivalent polite live region; role=alert or aria-live=assertive is reserved for important, time-sensitive messages such as errors; none of them take focus.
- Why: Understanding 4.1.3 maps success/results to role=status (ARIA22) and errors to role=alert (ARIA19), and lists assertive use on unimportant content as a failure. It adds that over-announcing makes apps chatty.
- Check (hybrid): List every dynamic message on the page. Assert each has a live-region role or property; assert role=alert / assertive appears only on errors or urgent warnings; test with a screen reader that it is announced once. (tools: axe-core, screen reader)
- While designing: Default to role=status; use role=alert only for errors the user must act on now.
- Sources: wcag-understanding-status-messages, wcag-22-quickref, apg-alert

### `comp-accordion-markup` [major · craft-consensus]
Each accordion header is a native button that is the only child of a heading element, with aria-expanded reflecting the panel state, and the button's accessible name is the visible title.
- Why: APG accordion and Inclusive Components agree: put the button inside the heading so the heading keeps its structure role; do not give the heading role=button. Progressive enhancement: when content must also work without JavaScript (perf-core-first, a11y-native-first), write plain heading + div markup (the content is visible) and let the script insert the button inside the heading and set the hidden state; this is the pattern the 2026-11 pilot used. Native details/summary is an acceptable no-JS alternative where the design allows it.
- Check (automated): For each toggle: tagName is BUTTON, parent is h1-h6 (or role=heading with aria-level), the button is the heading's only child, aria-expanded is 'true' or 'false' and flips on click, the hidden panel is display:none or [hidden] when collapsed. (tools: axe-core, playwright)
- While designing: Write accordions as h3 > button[aria-expanded] followed by a div that gets the hidden attribute when collapsed; if content must show without JS, ship plain h3 + div and let the script add the button and the hidden state.
- Often conflicts with styles: minimal, brutalism
- Sources: apg-accordion, ic-collapsible-sections, aria-apg-disclosure

### `comp-accordion-no-hidden-focusables` [major · craft-consensus]
Content inside a collapsed accordion panel cannot receive keyboard focus (hidden attribute or display:none, not just zero height or opacity).
- Why: Inclusive Components notes collapsed content is removed from the tab order when hidden; focus on invisible controls fails WCAG focus visibility and confuses keyboard users.
- Check (automated): With all panels collapsed, tab through the page and assert no focus lands on an element inside a collapsed panel; or query focusable elements inside collapsed panels and assert none are rendered. (tools: playwright)
- While designing: Collapse panels with the hidden attribute (or display:none), never by height:0 alone.
- Sources: ic-collapsible-sections, apg-accordion, wcag-22-quickref

### `comp-alert-no-focus-no-autodismiss` [major · standard]
Alerts and notifications do not move keyboard focus, are not removed by a timer shorter than the user needs to read them, and error or action-required messages stay until the user resolves or dismisses them.
- Why: The APG alert page says alerts must not take focus and should not vanish automatically (it ties this to time-limit criteria). WCAG 2.2.1 already requires adjustable timing.
- Check (manual): Trigger each alert; confirm document.activeElement does not change. Time how long it stays; any auto-dismiss under about 10 seconds or on an error is a finding unless the user can extend or recover the message elsewhere. (tools: devtools)
- While designing: Show messages in a live region without calling focus(); keep errors on screen until fixed. Tension with the common error-summary pattern that moves focus to the summary: put the summary in a role=alert region that exists empty at load (no focus call) and move focus to the first invalid field instead.
- Sources: apg-alert, ic-notifications, wcag-22-quickref

### `comp-alertdialog-confirmations` [major · standard]
Confirmations of destructive or irreversible actions use role=alertdialog with aria-describedby pointing at the message, and initial focus goes to the least destructive control (Cancel) when undoing is hard.
- Why: APG alertdialog is for interrupting the workflow to get a response and requires aria-describedby on the message; the modal-dialog page advises focusing the least destructive action for irreversible steps. COGA 4.8.3 asks that consequences of actions are stated.
- Check (manual): Trigger each delete/purchase/discard confirmation: verify the role, aria-describedby target text, and that focus starts on Cancel (not the destructive button). (tools: keyboard, devtools accessibility tree)
- While designing: Write destructive confirmations as alertdialog with a plain-language consequence message and focus Cancel first.
- Sources: apg-alertdialog, apg-dialog-modal, coga-usable

### `comp-checkbox-radio-group-labels` [major · standard]
Related checkboxes or radios are wrapped in a fieldset with a legend (or role=group / radiogroup with aria-labelledby) that names the group, each input has its own label, and a mixed-state parent checkbox uses aria-checked=mixed.
- Why: APG checkbox, radio and switch pages require a group label for visible group labels; the radiogroup must be labeled; mixed is the third state for tri-state checkboxes.
- Check (automated): For each set of inputs sharing a name or visual group, assert a fieldset>legend or [role=group|radiogroup][aria-labelledby|aria-label]; every input has a label. (tools: axe-core)
- While designing: Wrap every option set in fieldset and legend and label each input.
- Sources: apg-checkbox, apg-radio, apg-switch, wcag-22-quickref

### `comp-combobox-keyboard` [major · standard]
In a combobox, Down Arrow opens the popup and moves into it, Enter accepts the highlighted option, Escape closes the popup (restoring the typed value), typing keeps editing the input, and Tab moves on without stopping inside the popup.
- Why: APG lists these keys; Escape restoring the previous value is named as a distinction from listbox and menu button.
- Check (manual): Type, press Down, Enter, Escape, Tab in order and verify each outcome and that focus never leaves the input. (tools: keyboard)
- While designing: Implement Down, Up, Enter, Escape and Alt+Down exactly as the APG lists.
- Often conflicts with styles: command-palette
- Sources: apg-combobox, wcag-22-quickref

### `comp-combobox-semantics` [major · standard]
An autocomplete input has role=combobox on the input with aria-expanded, aria-controls pointing at the popup, aria-autocomplete matching its behavior, aria-activedescendant naming the highlighted option, and a real label.
- Why: APG combobox requires these relationships; DOM focus stays on the input while virtual focus moves in the popup (except for dialog popups).
- Check (automated): Open the popup and assert on the input: role=combobox, aria-expanded=true, aria-controls resolves to a visible listbox, aria-activedescendant changes with Down arrow and resolves to an option; label via label/aria-labelledby. (tools: axe-core, playwright)
- While designing: Keep DOM focus in the input and move aria-activedescendant through the options.
- Often conflicts with styles: command-palette
- Sources: apg-combobox, wcag-22-quickref

### `comp-content-slider-no-autoplay` [major · craft-consensus]
A horizontal slider uses native scrolling with a focusable (tabindex=0) labelled region, list markup for slides, labelled previous/next buttons, does not autoplay or move without user action, and slides that are out of view have their links removed from the tab order.
- Why: Inclusive Components says a slider should never move without the user's say-so and that WCAG 2.2.2 is a minimum; it also recommends native overflow scrolling, a region with aria-label and tabindex=-1 on links in hidden slides. APG carousel (existing source) covers rotating carousels.
- Check (hybrid): Load the page for 30 seconds without input: nothing moves. Tab through: arrows reachable, scroller focusable with visible focus, hidden slides' links not focusable. Check prev/next buttons have names. (tools: playwright, keyboard)
- While designing: Build sliders as scroll-snap lists with labelled prev/next buttons and no autoplay.
- Often conflicts with styles: horizontal-scroll, marquee, ambient-loop
- Sources: ic-content-slider, aria-apg-carousel, wcag-22-quickref, nng-carousels

### `comp-data-table-overflow-focusable` [major · craft-consensus]
A table wider than its container scrolls inside a labelled container (aria-labelledby the caption) that is keyboard focusable (tabindex=0) only when it actually overflows; table display properties are not changed to reflow it.
- Why: Inclusive Components: keyboard users cannot scroll unfocusable scrollers; tabindex=0 only on overflow avoids useless tab stops; changing display breaks table semantics. Inclusive Components uses role=group for the container.
- Check (automated): At 320 px and 1280 px: for each table container with scrollWidth > clientWidth assert tabindex=0 and an accessible name; for non-overflowing containers assert no tabindex. (tools: playwright, axe-core (scrollable-region-focusable))
- While designing: Wrap wide tables in a labelled overflow-x:auto container and add tabindex=0 when it scrolls.
- Sources: ic-data-tables, chrome-keyboard-focusable-scrollers, deque-scrollable-region-focusable, wcag-22-quickref

### `comp-data-table-semantics` [major · craft-consensus]
Tabular data uses table with a caption (or a figure and figcaption), th with scope=col / scope=row, and no layout tables; the grid role is used only for interactive cell-by-cell widgets.
- Why: Inclusive Components lists these basics; WCAG 1.3.1 requires the structure to be in the markup, which the existing a11y-semantic-structure rule covers.
- Check (automated): Each table has caption or figcaption/heading, header cells are th with scope, no table used purely for layout (role=presentation only as legacy fallback). (tools: axe-core)
- While designing: Mark pricing and spec tables with caption, th scope and real rows and columns.
- Often conflicts with styles: editorial, brutalism
- Sources: ic-data-tables, wcag-22-quickref

### `comp-dialog-semantics` [major · standard]
A modal dialog has role=dialog (or alertdialog), aria-modal=true, and an accessible name from aria-labelledby pointing at its visible title (or aria-label), and every control needed to operate it is inside the dialog element.
- Why: The APG makes the label required and the modal flag part of the pattern. Prefer the native dialog element with showModal(), which supplies modality; the APG page itself does not discuss inert or the native element.
- Check (automated): Open each dialog; query [role=dialog],[role=alertdialog],dialog[open]; assert accessible name is non-empty and that no interactive control needed by the dialog sits outside it. (tools: axe-core, playwright)
- While designing: Build modals with a titled dialog element or role=dialog plus aria-labelledby, and keep all its controls inside it.
- Often conflicts with styles: glassmorphism, maximalist
- Sources: apg-dialog-modal, apg-alertdialog, wcag-22-quickref

### `comp-dialog-truly-modal` [major · standard]
aria-modal=true is set only when code actually blocks interaction with the page behind the dialog and the page behind is visually obscured; otherwise the surface is built as a non-modal popover.
- Why: The APG says aria-modal can hide outside content from some assistive technology users, so a dialog marked modal that behaves non-modally seriously harms them.
- Check (manual): With the dialog open, try to Tab, click and screen-reader-navigate to background content. If any works, aria-modal must be absent. If aria-modal is present, confirm a dim or blur overlay covers the page. (tools: keyboard, screen reader)
- While designing: Make the background inert and dimmed whenever the dialog is modal; for popovers that leave the page usable, do not set aria-modal.
- Often conflicts with styles: glassmorphism
- Sources: apg-dialog-modal, apg-alertdialog

### `comp-landmarks-complete` [major · standard]
The page has exactly one main and one top-level banner (header) and one contentinfo (footer), uses nav, aside and search elements for those roles, and all perceivable content is inside some landmark.
- Why: APG landmarks best practice says all content belongs in a landmark; banner, main and contentinfo are one per page and top-level. header and footer only count as banner/contentinfo in the body context.
- Check (automated): Query landmarks with axe rules landmark-one-main, landmark-no-duplicate-banner, landmark-no-duplicate-contentinfo, region (content outside landmarks). (tools: axe-core, lighthouse)
- While designing: Wrap the page in header, nav, main and footer, and keep every text block inside one of them.
- Sources: apg-landmarks, apg-landmark-regions, wcag-22-quickref, axe-core-rule-descriptions

### `comp-listbox-select-semantics` [major · standard]
A custom listbox has role=listbox with an accessible name, role=option children each with aria-selected (or aria-checked, never both), aria-multiselectable=true when multi, short option names, and Up/Down, Home/End and type-ahead keys; options contain no interactive controls.
- Why: APG listbox: names are read as a flat string, long or repetitive names slow screen reader users, interactive content in options is unsupported. Where a native select would do, a11y-native-first applies.
- Check (hybrid): Inspect roles and states; keyboard test Up/Down/Home/End and typing a letter; scan options for nested a/button/input. (tools: axe-core, keyboard)
- While designing: Prefer a native select; build a custom listbox only with full APG keys and short option labels.
- Often conflicts with styles: experimental
- Sources: apg-listbox, wcag-22-quickref

### `comp-live-region-exists-before-content` [major · craft-consensus]
Live regions (role=status, role=alert or aria-live) exist in the DOM before their message is inserted, and messages that must be announced are injected after page load rather than rendered in the initial HTML.
- Why: APG says alerts already present at page load are not announced; Inclusive Components says do not add the region and its content at the same moment, leave a short gap.
- Check (hybrid): Inspect the initial DOM for an empty live-region container; trigger the message and confirm a screen reader announces it (NVDA, VoiceOver). Flag a region created together with its text. (tools: screen reader, devtools)
- While designing: Render an empty role=status container at load and fill it with text when something happens.
- Sources: apg-alert, ic-notifications, wcag-understanding-status-messages

### `comp-menu-button-action-menu` [major · standard]
A menu button that opens a list of actions is a button with aria-haspopup=menu and aria-expanded, opening role=menu with menuitem children; Enter/Space (and optionally Down/Up) open it and move focus to an item, arrows move between items, Escape closes it and returns focus to the button, and Tab leaves it.
- Why: APG menu-button and menu pages give this model; if you cannot implement all of it, use a plain button/list instead because role=menu promises these keys.
- Check (manual): Keyboard-test: open with Enter, Space, Down; move with arrows (Home/End); Escape returns focus to the button; Tab closes. Check aria-expanded flips. (tools: keyboard, devtools accessibility tree)
- While designing: Use role=menu only for action menus and implement every key the APG lists, or use a disclosure instead.
- Often conflicts with styles: floating-dock, command-palette
- Sources: apg-menu-button, apg-menubar, wcag-22-quickref, ic-menus-menu-buttons

### `comp-native-link-for-navigation` [major · standard]
Anything that navigates is an a element with an href; elements with role=link, onclick-only spans or buttons are not used for navigation, and buttons are used for in-page actions.
- Why: APG strongly encourages native link elements because role=link does not provide navigation or context-menu behavior; Inclusive Components uses a button, not a link, for in-page state changes.
- Check (automated): Query [role=link] and elements with click handlers that call location/navigation; assert none are non-anchor. Query a without href or with href='#'/javascript: used as buttons. (tools: axe-core, eslint-plugin-jsx-a11y)
- While designing: Use a[href] to go somewhere and button to do something.
- Sources: apg-link, ic-toggle-button, wcag-22-quickref

### `comp-radio-keyboard-model` [major · standard]
A radio group is one Tab stop (landing on the checked radio, else the first) with arrow keys moving and checking the next/previous radio with wrap; use native input type=radio with a shared name so the browser provides this.
- Why: APG radio keyboard model; the page notes some browsers differ on Shift+Tab landing when none is checked.
- Check (manual): Tab into the group, press arrows, confirm focus and checked state move together and the group is one tab stop. (tools: keyboard)
- While designing: Use native radio inputs with the same name attribute rather than custom divs.
- Sources: apg-radio, wcag-22-quickref

### `comp-site-nav-no-menu-role` [major · craft-consensus]
Site navigation is a nav landmark containing a list of links; dropdown groups are disclosure buttons with aria-expanded revealing a nested list; role=menu, menuitem and menubar are not used for site navigation.
- Why: Inclusive Components says ARIA menus are for application behavior and breaks link semantics in navigation. APG offers a Navigation Menubar example but recommends avoiding items that both navigate and open a submenu. Sources partly disagree (see disagreements).
- Check (automated): In header nav: assert no [role=menu|menubar|menuitem]; submenus triggered by button[aria-expanded]; first link of an opened list follows the button in focus order; nav has accessible name when more than one. (tools: axe-core, playwright)
- While designing: Build header menus as nav > ul with a button[aria-expanded] per dropdown and plain links inside.
- Often conflicts with styles: hamburger-only, unusual-nav, floating-dock
- Sources: ic-menus-menu-buttons, apg-menubar, aria-apg-disclosure-navigation

### `comp-slider-semantics` [major · standard]
A slider is a native input type=range or an element with role=slider carrying aria-valuenow, aria-valuemin, aria-valuemax and an accessible name, uses aria-valuetext when the number is not self-explanatory (a price, a time), and responds to arrow keys, Home and End.
- Why: APG slider requirements; it also warns touch-based assistive technology may not support slider gestures well, so test on touch screen readers.
- Check (hybrid): Inspect value attributes; keyboard test arrows/Home/End/PageUp/PageDown; check aria-valuetext shows units; test with VoiceOver on iOS or TalkBack. (tools: axe-core, keyboard, screen reader)
- While designing: Prefer input type=range; add output text next to it and aria-valuetext when units matter.
- Often conflicts with styles: drag-interaction, interactive-art
- Sources: apg-slider, wcag-22-quickref

### `comp-switch-label-stable` [major · craft-consensus]
An on/off control is a native checkbox, a button with aria-pressed, or role=switch with aria-checked, has a fixed accessible name, toggles with Space, and its name does not change when its state changes.
- Why: APG switch calls a stable label critical; Inclusive Components says never change the label and the state together (voice users say the visible label), and explicit aria-pressed true/false. Support for role=switch varied in 2017 (ChromeVox, NVDA) per Inclusive Components; check current support.
- Check (automated): Toggle each control and assert its accessible name is identical before and after, aria-checked/aria-pressed/checked is explicit 'true' or 'false', and Space toggles it. (tools: axe-core, playwright)
- While designing: Name toggles after the setting ('Dark mode') and flip only aria-pressed or aria-checked.
- Often conflicts with styles: mode-switching, micro-interactions
- Sources: apg-switch, ic-toggle-button, apg-checkbox

### `comp-tabs-keyboard` [major · standard]
In a tab list only the active tab is in the Tab order (others tabindex=-1), Left/Right arrows move focus between tabs with wrap, Home and End jump to first and last, and a tabpanel whose first content is not focusable has tabindex=0.
- Why: The APG gives this as the keyboard model; the single tab stop keeps long tab lists from trapping keyboard users, and the focusable panel lets Tab reach the content.
- Check (manual): Press Tab into the tablist: focus lands on the active tab. Press Right/Left/Home/End and verify focus moves; press Tab and verify focus lands in the panel (or its first focusable element). Check inactive tabs have tabindex=-1. (tools: keyboard)
- While designing: Implement tabs with roving tabindex and arrow, Home and End keys, and set tabindex=0 on a panel that starts with non-focusable content.
- Often conflicts with styles: hover-effects
- Sources: apg-tabs, ic-tabbed-interfaces, wcag-22-quickref

### `comp-tabs-semantics` [major · standard]
A tabbed interface uses role=tablist containing role=tab elements, each tab has aria-selected (true on exactly one) and aria-controls pointing at a role=tabpanel that has aria-labelledby pointing back to its tab, and the tablist has an accessible name.
- Why: The APG tabs pattern requires these roles and properties so assistive technology announces the set, the selected tab and the panel relationship.
- Check (hybrid): Query the DOM: every [role=tab] is a child of [role=tablist]; exactly one tab has aria-selected=true; each tab aria-controls resolves to a [role=tabpanel] whose aria-labelledby resolves to that tab; tablist has aria-label or aria-labelledby. Confirm with a screen reader that the selected state is announced. (tools: axe-core, screen reader, browser devtools accessibility tree)
- While designing: Give the tablist an aria-label, link every tab to its panel with aria-controls and aria-labelledby, and keep aria-selected in sync with the visible active state.
- Often conflicts with styles: minimal, brutalism
- Sources: apg-tabs, wcag-22-quickref

### `comp-toggle-visual-state-not-color` [major · craft-consensus]
A toggle's on/off state is visible through more than color (position of a knob, an icon, or text) and the visual style is driven by the ARIA state attribute so they cannot diverge.
- Why: Inclusive Components cites WCAG 1.4.1 and styling from [aria-pressed=true]; COGA 4.5.10 says toggles should expose state programmatically and every state change needs visual feedback.
- Check (hybrid): Grayscale screenshot of both states; confirm still distinguishable. Check CSS selectors key off aria-pressed/aria-checked/:checked. (tools: devtools)
- While designing: Style toggles from [aria-pressed=true] and add a knob position or check icon, not only a color change.
- Often conflicts with styles: minimal, neon
- Sources: ic-toggle-button, coga-usable, wcag-22-quickref

### `comp-tooltip-not-sole-label-no-interactive` [major · craft-consensus]
A tooltip appears on both hover and keyboard focus, closes with Escape, stays open while the pointer is over it, is linked to its trigger with aria-describedby, and contains no links, buttons or other interactive content; where space allows, a visible text label is used instead.
- Why: APG: Escape dismisses, focus stays on trigger, hover persistence, aria-describedby (the page says the pattern has no consensus yet). Inclusive Components: tooltips are a last resort and must not hold interactive content, which belongs in a dialog or menu. WCAG 1.4.13 covers dismiss, hover and persist.
- Check (hybrid): Hover and Tab to each tooltip trigger; press Escape; move the pointer onto the bubble; check aria-describedby; check the bubble DOM for a, button, input. (tools: keyboard, devtools)
- While designing: Prefer visible labels; if a tooltip is unavoidable, trigger on hover and focus, allow Escape, and keep it text only.
- Often conflicts with styles: hover-effects, cursor-effects, minimal
- Sources: apg-tooltip, ic-tooltips-toggletips, wcag-22-quickref

### `a11y-coga-action-feedback` [minor · craft-consensus]
Every user action produces immediate visible feedback (pressed or loading state, confirmation message after sending), and multi-step flows show completed, current and upcoming steps.
- Why: COGA 4.5.10 (provide feedback) and 4.2.4 (make each step clear): confirmation after sending a form, visible status per step, buttons with pressed state.
- Check (manual): Submit each form and click each state-changing control; confirm a visible confirmation or state change within about 1 second; in multi-step flows, check a step indicator exists.
- While designing: Show a visible confirmation after every submit and mark each step as done, current or next.
- Often conflicts with styles: minimal, micro-interactions
- Sources: coga-usable, wcag-22-quickref

### `a11y-coga-controls-recognizable` [minor · craft-consensus]
Links are visually distinguishable from body text (underline or equally strong cue), controls have a clear boundary or fill, non-interactive items do not look clickable, and nothing styled as a control is crowded against its neighbor.
- Why: COGA 4.2.5 asks for recognizable controls, underlined links, and for non-clickable items not to look like links; 4.2.6 asks that interactive elements are not crowded. Overlaps WCAG 1.4.1 and 1.4.11.
- Check (hybrid): Screenshot in grayscale: can every link and button be found? List elements with pointer-style hover or link color that are not links. (tools: grayscale emulation)
- While designing: Underline inline links and give every button a visible fill or border.
- Often conflicts with styles: minimal, brutalism, quiet-luxury, oversized-type
- Sources: coga-usable, wcag-22-quickref

### `a11y-coga-costs-up-front` [minor · craft-consensus]
On e-commerce and booking pages, price, fees, charges and key conditions are shown at the start of the task and the final total matches what was shown earlier; consequences and disadvantages of each option are stated next to it.
- Why: COGA 4.5.3 (fees at the start) and 4.8.3 (state results and disadvantages of options). Relevant to the EAA e-commerce scope.
- Check (manual): Walk product page to checkout: record each price shown; confirm no new fee appears at the last step; check options list their inclusions and exclusions.
- While designing: Show the full price with fees on the product page, not only at checkout.
- Sources: coga-usable, wcag-22-quickref

### `a11y-coga-hierarchy-visible-no-hover-reveal` [minor · craft-consensus]
Sub-menus and expandable content show a visible indicator that more exists and open on click or tap, not only on hover; heading levels form an outline of the page and same-level headings share a style.
- Why: COGA 4.3.2 (clear indicators for hidden or expandable text, no hover-only reveal), 4.3.3 (headings as an outline) and 4.2.3 (consistent visual design).
- Check (hybrid): Tab and click each menu: it opens without hover; indicator present. Extract heading outline and check levels do not skip and same-level headings have the same computed font-size/weight. (tools: HeadingsMap, playwright)
- While designing: Open menus on click, show a chevron on parents, and style each heading level once.
- Often conflicts with styles: hover-effects, unusual-nav
- Sources: coga-usable, wcag-22-quickref

### `a11y-coga-icons-with-text` [minor · craft-consensus]
Icons that carry meaning are paired with a visible text label, each icon has one consistent meaning across the site, and no section is crowded with decorative icons.
- Why: COGA 4.2.7: familiar icons next to content, one meaning per icon, no cluttered pages. Inclusive Components says tooltips are a last resort for icon-only controls.
- Check (manual): List every icon-only control on the homepage; each needs a visible text label or a proven universal meaning; verify the same icon is not reused for different things.
- While designing: Add a text label beside every icon except the universally understood few (search, close, menu).
- Often conflicts with styles: minimal, floating-dock, quiet-luxury
- Sources: coga-usable, ic-tooltips-toggletips, wcag-22-quickref

### `a11y-coga-key-tasks-prominent` [minor · craft-consensus]
The one to three key tasks of the site are visually distinct, placed near the top of the page, each under a descriptive heading, and reachable from the top level of the main navigation.
- Why: COGA patterns 4.3.1 and 4.3.4 ask for key tasks in visually distinct boxes near the top, in top-level navigation and early in the reading order, visible without scrolling or hovering. Overlaps ux-primary-cta-above-fold.
- Check (manual): At 1280x800 and 375x812 without scrolling, identify the key task controls; check each is in the nav and early in DOM order. (tools: browser)
- While designing: Surface the main task as a prominent labelled control in the first screen and in the top navigation.
- Often conflicts with styles: poster, long-scroll-narrative, hero-type-only
- Sources: coga-usable, nng-homepage-principles

### `a11y-coga-limit-interruptions` [minor · craft-consensus]
No pop-up, chat widget prompt, subscribe overlay or moving ad-like element interrupts the first task; moving content can be paused; notification settings, if any, are reachable from every screen.
- Why: COGA 4.6.1 (limit interruptions) says users should control reminders and changing content and that blocking pop-ups such as subscribe prompts should be avoided. Overlaps ux-no-popups and a11y-pause-stop-hide.
- Check (manual): Load the homepage fresh, wait 30 s, scroll to 50%, and record any overlay, auto-opened chat, or banner that takes attention or blocks controls. (tools: browser)
- While designing: Delay any prompt until after the user finishes a task and make it dismissible.
- Often conflicts with styles: cursor-effects, ambient-loop, marquee
- Sources: coga-usable, wcag-22-quickref

### `a11y-coga-no-surprise-changes` [minor · craft-consensus]
Content and controls do not move, open or change on load or without a user action: no layout shift after paint, no auto-opening windows or pop-ups, no auto-submitting forms; a loading indicator shows while content loads.
- Why: COGA 4.5.1 and 4.9.1 list these. WCAG 3.2.x and the Core Web Vitals CLS limit (0.1) already cover parts of this.
- Check (automated): Record page load; measure CLS (<= 0.1); open page with no input for 10 s and assert no new windows, dialogs or focus changes; check that selecting a control does not submit or navigate. (tools: lighthouse, playwright)
- While designing: Reserve space for late content and open dialogs only after a click.
- Often conflicts with styles: intro-preloader, page-transitions, scroll-triggered
- Sources: coga-usable, webdev-core-web-vitals, wcag-22-quickref

### `a11y-coga-plain-literal-language` [minor · craft-consensus]
Headings, labels, buttons and error messages use common words, literal wording, active voice and positive phrasing; acronyms and jargon are expanded or explained on first use; metaphors or idioms in navigation and calls to action are avoided.
- Why: COGA patterns 4.4.1 to 4.4.4 (clear words, simple tense and voice, no double negatives or nested clauses, literal language) apply to headings, labels, navigation, instructions and error messages.
- Check (manual): Read every nav label, heading, button and error string: list jargon, unexplained acronyms, idioms, double negatives; each must be replaced or explained.
- While designing: Name nav items and buttons with the literal thing the user gets, not a metaphor.
- Often conflicts with styles: quirky, playful, edgy, luxury
- Sources: coga-usable

### `a11y-coga-text-not-over-busy-background` [minor · craft-consensus]
Text is placed on solid or low-detail backgrounds (or a solid panel/overlay), not directly over photos, video, gradients or patterns with varying luminance.
- Why: COGA 4.4.11 says not to place words over busy backgrounds, to use solid backgrounds for text blocks and strong contrast. Overlaps WCAG 1.4.3 measurement, which varies across a photo.
- Check (hybrid): Screenshot hero and banner text; sample background luminance across the text box (min and max) and confirm the worst case still meets 4.5:1; flag text over video. (tools: contrast checker, screenshot)
- While designing: Put hero text on a solid or scrimmed panel, never straight onto moving or high-detail imagery.
- Often conflicts with styles: hero-full-bleed, hero-video, grain-noise, atmospheric, gradient-aurora, glassmorphism
- Sources: coga-usable, wcag-22-quickref

### `comp-accordion-region-limit` [minor · standard]
Accordion panels carry role=region with aria-labelledby only when the accordion has fewer than about six panels; larger accordions leave panels unlabeled as regions.
- Why: APG warns that region on many panels (it cites roughly six or more) creates landmark clutter. The number is approximate in the source.
- Check (automated): Count [role=region] / named section elements that are accordion panels on the page; flag if 6 or more per accordion. (tools: axe-core)
- While designing: Skip role=region on FAQ-style accordions with six or more items.
- Sources: apg-accordion, apg-landmark-regions

### `comp-breadcrumb-nav` [minor · standard]
A breadcrumb trail sits in a nav landmark with an accessible label (for example 'Breadcrumb'), is a list of links to parent pages in hierarchical order, and marks the current page link with aria-current=page.
- Why: The APG breadcrumb pattern requires the labeled navigation landmark and aria-current on the current-page link. COGA 4.2.1/4.2.4 also lists breadcrumbs as a way to show where the user is.
- Check (automated): Find the breadcrumb: assert nav[aria-label|aria-labelledby], ol/ul of links, last item aria-current=page. (tools: axe-core, playwright)
- While designing: On any page deeper than one level, add nav[aria-label=Breadcrumb] > ol with aria-current=page on the last item.
- Often conflicts with styles: minimal, anchor-only
- Sources: apg-breadcrumb, coga-usable, wcag-understanding-multiple-ways

### `comp-card-single-primary-link` [minor · our-take]
Each card is one list item with a heading at the same level across the set; the heading text is the only primary link (not a link wrapping the whole card); a whole-card click area, if wanted, is made with a stretched ::after on that link; images that are decorative have alt="".
- Why: Inclusive Components: whole-card links make screen reader announcements verbose and break with nested links; list markup gives item counts; the heading link has a unique descriptive name. Trade-off: the stretched-link technique prevents text selection, mitigated by a click-duration check.
- Check (automated): For each card: parent is li inside ul/ol; one heading; exactly one a whose text matches the heading; no a ancestor wrapping heading+image+text; images have alt (empty if decorative). (tools: playwright, axe-core)
- While designing: Mark cards up as li > heading > a with a stretched pseudo-element for the click area, not a wrapper anchor.
- Often conflicts with styles: bento-grid, gallery-wall, maximalist
- Sources: ic-cards

### `comp-data-table-sortable-headers` [minor · our-take]
Sortable column headers contain a button labelled with the column name, and the th carries aria-sort (ascending, descending or none); sort arrows use currentColor.
- Why: Inclusive Components: button in each sortable header, aria-sort for state, and clear labels; icons that show current state can mislead about what pressing does, so the button text must say what happens.
- Check (automated): For each sortable column: th[aria-sort] contains button with name; activating it changes aria-sort and row order. (tools: playwright)
- While designing: Render sortable headers as th[aria-sort] > button and update aria-sort on click.
- Sources: ic-data-tables

### `comp-disclosure-state-not-color-only` [minor · craft-consensus]
The open or closed state of a disclosure control is shown by a shape or icon change (such as plus to minus or a rotating chevron) that is hidden from assistive technology, never by color alone, and the icon uses currentColor.
- Why: Inclusive Components hides the decorative icon with aria-hidden because state is carried by aria-expanded, and uses currentColor so high-contrast modes recolor it. COGA 4.3.2 asks for consistent, clear indicators for expandable content. Primarily one practitioner plus COGA Note.
- Check (hybrid): Toggle each control and compare screenshots: the indicator shape changes. Inspect the icon SVG for aria-hidden=true and fill/stroke currentColor. Emulate forced-colors and confirm it stays visible. (tools: browser devtools, forced-colors emulation)
- While designing: Pair every expandable header with a plus/minus or chevron SVG marked aria-hidden that changes shape when aria-expanded flips.
- Often conflicts with styles: minimal, glassmorphism
- Sources: ic-collapsible-sections, coga-usable, wcag-22-quickref

### `comp-icon-currentcolor-aria-hidden` [minor · our-take]
Decorative inline SVG icons inside controls have aria-hidden=true and focusable=false, informative icons have a text alternative (visually hidden text), and icon fills and strokes use currentColor so forced-colors and high-contrast modes recolor them.
- Why: Inclusive Components repeats this in collapsible sections, notifications and theme switcher; the same author wrote all three, so this is one source. MDN forced-colors (existing source) is the independent place to confirm.
- Check (automated): Query svg inside buttons and links: aria-hidden=true when the control has text; fill/stroke not hard-coded hex; emulate forced-colors: active and verify icons remain visible. (tools: devtools)
- While designing: Draw icons with fill=currentColor and hide them from assistive tech when text is next to them.
- Sources: ic-collapsible-sections, ic-notifications, ic-theme-switcher, mdn-forced-colors

### `comp-landmarks-labels` [minor · standard]
Landmarks of the same role each have a unique accessible name (except identical-content pairs), section and form elements become landmarks only when named, labels do not repeat the role word, and the page has about seven or fewer landmark regions.
- Why: APG landmark regions: unique labels, name required for region and form, 'Site' not 'Site navigation'; the landmarks page gives a seven-or-fewer rule of thumb because value drops as the count grows.
- Check (automated): List landmarks with names; flag duplicates of the same role with the same or missing name; flag labels containing their own role word; count landmarks. (tools: axe-core, browser devtools accessibility tree)
- While designing: Give header and footer navs distinct aria-labels such as 'Main' and 'Footer'.
- Sources: apg-landmark-regions, apg-landmarks

### `comp-no-title-attribute-reliance` [minor · craft-consensus]
The title attribute is not the only source of an accessible name, instruction or tooltip text; essential information is also available as visible text or a labelled control.
- Why: Inclusive Components says title fails for keyboard and touch users and has inconsistent screen reader support; COGA 4.5.6 says labels should not depend only on title or ARIA attributes.
- Check (automated): Search for [title] on interactive elements; for each, assert there is also visible text or aria-label/labelledby and that no instruction exists only in title. (tools: axe-core, playwright)
- While designing: Never put meaning in title; show it as text or a labelled control.
- Sources: ic-tooltips-toggletips, coga-usable

### `comp-notification-recoverable` [minor · our-take]
Any transient notification (toast, snackbar) refers to something the user can find again elsewhere (list, history, page state), and notifications are not used for information needed to complete a task.
- Why: Inclusive Components advises that each notification points to something discoverable elsewhere so people who missed it are not stranded. Sources disagree on dismiss buttons and auto-dismiss (see disagreements); this rule takes the safe common ground. Single practitioner source.
- Check (manual): For each toast: after it disappears, can the same information be found on the page (cart count, order list, inline status)? If not, flag.
- While designing: Mirror every toast in persistent on-page state so missing it loses nothing.
- Often conflicts with styles: micro-interactions
- Sources: ic-notifications, apg-alert

### `comp-toggletip-click-live-region` [minor · our-take]
Help bubbles that must work on touch (info icons) are click-activated 'toggletips': a button with type=button and a visible or visually hidden name, an adjacent role=status region filled on click, no aria-describedby on the button, and dismissal by Escape, outside click or blur.
- Why: Inclusive Components: hover and focus tooltips do not work reliably on touch; describedby would read the content before the user asks. This differs from the APG tooltip, which has no click variant (single practitioner source, so hypothesis).
- Check (manual): Tap and keyboard-activate each info button: bubble appears, screen reader announces it, Escape closes. Check the button is a real button with an accessible name and that the bubble text is not exposed before activation. (tools: keyboard, touch device, screen reader)
- While designing: For info icons, render a button plus an empty role=status span and write the help text into it on click.
- Often conflicts with styles: hover-effects
- Sources: ic-tooltips-toggletips

### `comp-toolbar-threshold` [minor · standard]
role=toolbar is used only for a group of 3 or more controls, has an accessible name, exposes a single tab stop with arrow-key navigation among controls, and contains at most one control that needs the same arrow keys (placed last).
- Why: APG toolbar states the 3-control threshold and the single-tab-stop roving model; otherwise a plain group of buttons with normal Tab order is simpler.
- Check (hybrid): Find [role=toolbar]; count controls (3 or more); Tab once into it and use arrows; check name. (tools: keyboard, axe-core)
- While designing: Do not add role=toolbar to two buttons; use it for three or more and implement roving tabindex.
- Often conflicts with styles: floating-dock
- Sources: apg-toolbar, wcag-22-quickref

### `a11y-coga-limit-choices-per-screen` [advisory · craft-consensus]
Each screen or section offers about five or fewer main choices, secondary links sit in the footer or under a titled 'more' link, and one feature is visually dominant.
- Why: COGA 4.6.3 (avoid too much content) gives five or fewer main choices; also suggests one or two relevant images per page. This conflicts with ux-visible-navigation on desktop if read literally (see disagreements).
- Check (manual): Count primary actions/links competing in each viewport-height section of the homepage; flag more than about 5 equal-weight choices.
- While designing: Limit each section to one main action plus at most four alternatives. Tension: a list of situations or services that is the content is one choice, not many; keep it as one labelled list that is the dominant feature, group a long one under headings, keep other actions visibly secondary and record the call.
- Often conflicts with styles: maximalist, bento-grid, catalog-grid, gallery-wall
- Sources: coga-usable, nng-homepage-principles

### `a11y-coga-media-chunks-transcripts` [advisory · craft-consensus]
Long video or audio is split into labelled segments of about six minutes or less where there are natural breaks, and a transcript or summary is easy to find next to it.
- Why: COGA 4.3.5 (break media into chunks: segments generally six minutes or less, unique descriptive labels, transcripts easy to find) and 4.4.8 (summaries).
- Check (manual): For each media item over 6 minutes, check for chapter links or segmentation and a transcript or summary link adjacent.
- While designing: Add chapter labels and a transcript link under every video longer than six minutes.
- Often conflicts with styles: hero-video
- Sources: coga-usable, wcag-22-quickref

### `a11y-coga-short-paragraphs` [advisory · craft-consensus]
Body paragraphs carry one topic each and are about 50 words or fewer (English), with the point stated first; sequences of three or more items use bulleted lists and steps use numbered lists.
- Why: COGA 4.4.5 gives about 50 words per paragraph as a guide for English, one point per sentence, lists for three or more items. It is a guideline, not a hard limit.
- Check (automated): Count words per p in main content; report paragraphs over about 60; flag long comma-chained runs of 3+ items that should be lists. (tools: script, playwright)
- While designing: Break copy into short single-topic paragraphs and use lists for three or more items.
- Often conflicts with styles: editorial, serif-editorial, long-scroll-narrative
- Sources: coga-usable, nng-how-users-read

### `a11y-coga-visible-help-contact` [advisory · craft-consensus]
A way to reach a person (contact page, email or phone) is available from every page within one click, and a contact form has at most three required fields.
- Why: COGA 4.8.1 and 4.8.5: human help easy to find on every page, few steps, not behind complex menus; feedback forms simple with no more than three required fields; chatbots not the only route.
- Check (automated): On five different pages assert a link to contact/help exists in header or footer; open the contact form and count required fields. (tools: playwright)
- While designing: Put a Contact link in the footer of every page and keep its form to three required fields.
- Often conflicts with styles: minimal, anchor-only
- Sources: coga-usable

### `a11y-reading-level-support` [advisory · standard]
Where text needs more than lower-secondary reading ability (roughly school years 7 to 9), a plain summary, illustrations or a simpler version is offered.
- Why: WCAG 3.1.5 is Level AAA (not required for AA conformance); the Understanding page lists a text summary, illustrations, spoken version and simplified text as techniques. The EAA Annex I sets B2 (CEFR) for consumer banking information specifically.
- Check (hybrid): Run a readability score (for example Flesch-Kincaid) on main content, ignoring proper names; if above grade 9, check for a summary or simpler version. (tools: readability scorer)
- While designing: Write at roughly grade 8 and add a short summary above long or technical sections.
- Often conflicts with styles: editorial, serif-editorial, luxury
- Sources: wcag-understanding-reading-level, eaa-directive-2019-882, coga-usable

### `comp-card-limited-tab-stops` [advisory · our-take]
A card has one tab stop, or two only when a secondary link is genuinely useful, and 'read more' cues are non-interactive text hidden from assistive technology (aria-hidden) and tied to the link with aria-describedby rather than being a second link.
- Why: Inclusive Components: extra tab stops slow keyboard users and cards should not be miniature web pages; a visual 'read more' cue helps people recognize interactivity.
- Check (automated): Count focusable elements per card (max 2); flag 'read more' / 'learn more' links duplicated per card. (tools: playwright)
- While designing: Give each card one link on its heading and a decorative 'Read more' cue, nothing else focusable.
- Often conflicts with styles: bento-grid
- Sources: ic-cards

### `comp-tabs-not-for-navigation` [advisory · our-take]
Tabs are not used for site-wide navigation or for an unknown or large number of sections; links that go to other pages are not styled or marked up as tabs.
- Why: Inclusive Components says users who see tabs expect in-page panel switching, not page navigation, and recommends an accordion when the number of tabs is large or unknown. Single practitioner source for this point.
- Check (manual): Find every tab-looking control. If activating it loads another URL or it is part of the primary nav, flag it. Count tabs: more than about five on mobile widths, or generated from data, should be an accordion or a list of links.
- While designing: Use a plain nav list for pages and a table of contents for page sections; reach for tabs only for a few peer panels of one topic.
- Often conflicts with styles: unusual-nav, unconventional-layout
- Sources: ic-tabbed-interfaces

### `comp-theme-switcher-control` [advisory · our-take]
If the site offers a light/dark theme control, it is a labelled toggle (button with aria-pressed, or radio group in a fieldset with legend), lives in a landmark (header or footer) in the same place on every page, and the choice persists across visits.
- Why: Inclusive Components (2017) describes a toggle button, placement in a landmark, same location everywhere and localStorage persistence; it does not cover prefers-color-scheme, so default to the user's OS setting is not from this source. Single practitioner source.
- Check (manual): Toggle, reload, confirm persistence; confirm control is within header/footer landmark and identical on two pages; check name and state announced. (tools: devtools)
- While designing: Put one labelled theme toggle in the header, store the choice, and honor prefers-color-scheme as the default.
- Often conflicts with styles: mode-switching, dark-cyber
- Sources: ic-theme-switcher, ic-toggle-button, mdn-prefers-color-scheme
