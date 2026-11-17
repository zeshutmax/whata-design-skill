# Quality Bar: Visual craft
Severity: blocker (never traded for style), major, minor, advisory. Labels: standard, evidence, craft-consensus, our-take.

### `craft-body-size-min` [major · craft-consensus]
Running text (paragraphs, list items, form text, table cells) computes to at least 16px at every viewport width; only captions, footnotes and legal text may be smaller.
- Why: USWDS asks for an effective size of at least 16px for most text and reserves smaller sizes for captions and footnotes; GOV.UK sets body at 19px with its smallest style at 16px, to be used sparingly; Butterick gives 15-25 px as the web range for body text. Sources differ on the floor (15 vs 16), so the rule takes 16.
- Check (automated): At the audit's desktop (1440 px) and mobile (390 px) viewports, collect computed font-size of every visible text node inside p, li, td, th, label, button, and of every visible input, textarea and select (invisible and screen-reader-only text is ignored). Fail when any is under 16px, unless the node is inside figcaption, small, footer or a caption. List every such exempt text under 14px for manual review (14px is our review threshold, not from a source). (tools: playwright, getComputedStyle)
- While designing: Set the body size to 1rem (16px) or larger, sized up (17-20px) for long reading, and use smaller sizes only for captions and legal lines.
- Often conflicts with styles: minimal, editorial, quiet-luxury
- Sources: uswds-typography, govuk-paragraphs, govuk-type-scale, butterick-point-size

### `craft-breakpoints-content-based` [major · craft-consensus]
Layout breakpoints are written in em/rem at the widths where the content breaks, not at named device widths, and the page has no overflow, clipped content or line-length violation at any viewport width between 320px and 1920px.
- Why: web.dev: set breakpoints from your content rather than popular device sizes, use em/ch for text-based content, and prefer intrinsic grid rules (auto-fill/minmax(15em, 1fr)) and container queries over a ladder of media queries; GOV.UK says to design for a range of screen sizes rather than specific devices and to start with one column on small screens.
- Check (hybrid): Automated: resize one loaded page from 320 to 1920 px in 40px steps and fail at any width where the document scrolls sideways (scrollWidth > clientWidth); list the px media-query breakpoints of the readable stylesheets and flag any matching device presets (375, 414, 768 and 1024 px) for review. A person checks what the audit does not: no element overlapping its sibling's box, the measure rule at each width, and that breakpoints are written in em or rem where the content breaks. (tools: playwright)
- While designing: Build the layout with fluid grid rules first and add a breakpoint in em only where you can see the content break.
- Often conflicts with styles: horizontal-scroll, split-screen, poster, unconventional-layout
- Sources: webdev-design-media-queries, webdev-design-macro-layouts, webdev-design-micro-layouts, govuk-layout

### `craft-contrast-text-on-media` [major · standard]
Text placed over photos, video or gradients keeps 4.5:1 (3:1 for large text) against the worst-case backdrop beneath each line of text, using an overlay or scrim where needed.
- Why: WCAG 1.4.3 Understanding says background images that fail to give sufficient contrast with text are a failure, and contrast is judged on the color pairs actually adjacent; no gradient-specific method is given, so sampling the lightest/darkest backdrop pixel is our reading of it. This refines the existing a11y-contrast-text for hero imagery.
- Check (hybrid): Screenshot each section with text on imagery at 375, 768 and 1440 px (and at the video's brightest frame). Sample the backdrop under each text line's bounding box, take the pixel closest to the text color, compute the WCAG ratio. Fail below 4.5:1 (3:1 for 24px+ or 18.66px+ bold). (tools: playwright screenshots, colorjs.io)
- While designing: Put a solid or gradient scrim behind any text that sits on a photo or video and verify the contrast on the brightest area.
- Often conflicts with styles: hero-full-bleed, hero-video, photography, glassmorphism, gradient-aurora, atmospheric
- Sources: wcag-contrast-minimum

### `craft-contrast-wcag2-authoritative` [major · standard]
Contrast pass/fail is decided with the WCAG 2.x ratio (4.5:1 text, 3:1 large text and UI); APCA Lc values may be reported as extra information but never override a failing WCAG 2 ratio.
- Why: The W3C status page calls WCAG 3 an incomplete draft that is not expected to be a standard for a few more years and says meeting WCAG 2.2 is the best preparation; the Working Draft dated 10 Sep 2026 leaves the contrast algorithm as a placeholder ('yet to be determined') and does not name APCA in the part read. Myndex's own docs describe APCA as a candidate (author's opinion, not W3C's), with Lc 75 as a body-text minimum and Lc 90 as preferred on that page.
- Check (automated): Contrast reports must be computed with the WCAG 2.x relative-luminance ratio; if an APCA value is also shown, check the pass/fail column is still WCAG 2. Fail if a pair below 4.5:1 is marked as passing because of an APCA score. (tools: axe-core, colorjs.io)
- While designing: Validate colors with the WCAG 2.x ratio and treat APCA only as a second opinion for borderline thin or small text.
- Sources: wcag3-intro, wcag3-draft, apca-why, wcag-contrast-minimum

### `craft-dark-mode-reverify` [major · craft-consensus]
In the dark theme every text and UI color pair is re-checked against the same contrast thresholds (4.5:1 text, 3:1 large text and UI components), and the palette is not made by inverting or filtering the light one.
- Why: Apple HIG: dark colors are not simple inversions, keep 4.5:1 in every appearance and test with Increase Contrast; web.dev's theming module redefines each token for dark and darkens photos with `brightness(.8) contrast(1.2)` rather than inverting; WCAG 1.4.3 thresholds apply to the page as rendered. White-background images should be dimmed so they do not glow (Apple).
- Check (automated): Run the contrast audit (text 4.5:1, large 3:1, UI components 3:1) twice, once per emulated color scheme, over all pages and states (hover, focus, disabled excluded). Fail any pair that passes light but fails dark. Flag use of `filter: invert()` on the page root. (tools: axe-core, playwright)
- While designing: Author the dark palette as its own set of tokens, check contrast in both themes, and dim bright images instead of inverting anything.
- Often conflicts with styles: dark, dark-cyber, neon, glassmorphism
- Sources: apple-hig-dark-mode, webdev-design-theming, wcag-contrast-minimum

### `craft-fluid-type-rem-clamp` [major · craft-consensus]
No font-size is set in vw, vh or vi alone. Text that must reach 200% on zoom (body, UI, and headings you cannot afford to clip) uses rem sizes stepped at em or rem breakpoints, with the smallest step at least 40% of the largest. A clamp() with a vw term is allowed only for decorative display type, and only after you measured that it still grows at 200% zoom.
- Why: web.dev says never to use vw alone and to combine it with rem/em/ch in calc(), clamping with rem bounds; MDN says the maximum should be a relative unit at least twice the minimum so text can reach 200% (WCAG 1.4.4); Roselli shows `clamp(1.5rem, 5vw, 3rem)` growing from 64px only to about 68px at 200% zoom in a 1024px window, so the vw term can still fail 1.4.4 even when max = 2x min; Utopia cites the same warning and says to test before production. Our own measurement (content/learn/measurements/type-zoom-2026-11-05.json, Chrome): viewport-unit and clamp(rem + vw) sizes did not reach 200% at 200% zoom, because the vw term shrinks as the viewport in CSS px shrinks; stepped rem sizes with a small size of at least 40% of the large size did. The rule therefore prefers stepped rem and no longer recommends clamp(rem + vw) for text that must scale.
- Check (hybrid): Static: reject any font-size value that is a bare vw/vh/vi length or a clamp() with px bounds. Dynamic: at a 1024px-wide window measure the computed size of fluid headings, then emulate 200% and 300% browser zoom (viewport halves/thirds) and confirm the on-screen size at 200% is close to double; flag headings whose size grows by far less (Roselli's example: 6.25%) for manual review. Mark a clamp() with a vw term as failing for any text larger than 24px unless the measured size at 200% zoom is at least 1.5 times the 100% size. (tools: playwright, chrome devtools zoom)
- While designing: Set headline sizes in rem and step them at em/rem media queries (for example 3rem, 4rem, 7rem), keeping the smallest at least 40% of the largest; do not use clamp(rem + vw) for text that must scale; test at 200% zoom and 320 px.
- Often conflicts with styles: oversized-type, expressive-type, poster
- Sources: webdev-typography, mdn-clamp, roselli-responsive-type-zoom, utopia-clamp

### `craft-image-dimensions-reserved` [major · craft-consensus]
Every img and video element has width and height attributes or a CSS aspect-ratio, so its box is reserved before the file loads.
- Why: web.dev: always include width and height so the browser reserves the right space and avoids layout shift even when CSS scales the image; MDN: `aspect-ratio: auto 3/2` keeps the ratio before load and the natural one after (Baseline Widely available since Sept 2021). This is the cause-level rule behind the existing perf-cls metric.
- Check (automated): For every img, video, iframe: fail if it lacks both (width and height attributes) and a computed aspect-ratio other than auto. Run with images blocked and check CLS stays at or below 0.1. (tools: playwright, lighthouse, html validator)
- While designing: Put the intrinsic width and height on every image tag and keep height: auto in CSS.
- Sources: webdev-design-responsive-images, mdn-aspect-ratio

### `craft-measure-body` [major · craft-consensus]
Running-text paragraphs are never wider than 75 characters per line at any viewport width from 320px to 1920px (the target is about 66 characters; in CSS that is about 50ch to 55ch for proportional fonts, because ch is the width of the digit 0).
- Why: web.dev (citing Bringhurst) calls 45-75 characters satisfactory and about 66 ideal for single-column text; USWDS says 45-90 with a long-text target of 66; Butterick says 45-90; GOV.UK keeps main content in a two-thirds column for no more than about 75; WCAG 1.4.8 (AAA) caps at about 80. The upper edge differs between sources (75, 80, 90), so the rule uses the strictest common figure. Butterick calls missing line-length checks the main flaw of many responsive designs. Our own measurement (Chrome 156, macOS, 2026-11-06): max-inline-size 66ch produced 87 to 96 characters per line with system-ui, Georgia, Arial and Helvetica Neue; 50ch gave 67 to 74. So set the container to about 50ch to 55ch, not 66ch, and count real characters per line.
- Check (hybrid): At widths 320, 768, 1280 and 1920 px, find every paragraph/list-item/blockquote with more than two lines of text. Compute characters per line (text length divided by rendered line count, or compute container inline-size divided by the width of one '0' glyph, i.e. in ch). Fail if any exceeds 75. For the lower bound, where the viewport allows it (>= 768px), flag single-column text below 45 characters per line for manual review. (tools: playwright, getComputedStyle, Range.getClientRects)
- While designing: Wrap every block of running text in a container with max-inline-size of about 50ch to 55ch (ch is the width of the digit 0, wider than the average letter), never above 60ch, and count characters per line in the browser: it must not exceed 75.
- Often conflicts with styles: oversized-type, poster, hero-type-only, maximalist
- Sources: webdev-typography, uswds-typography, butterick-line-length, govuk-layout, wcag-understanding-visual-presentation

### `craft-relative-units-text` [major · craft-consensus]
Font sizes are declared in rem or em (not px), the root font-size is not fixed in px, and text containers are width-limited in ch, rem or em.
- Why: web.dev says to use relative units for line length (66ch rather than 700px) so it scales with user font settings, and for font size so text follows user preferences; Roselli advises not to set the base font size in px but to start from the browser default; MDN defines rem as the root font size, which users can change in preferences.
- Check (automated): Scan CSS for font-size declarations with px units (allow px only in fallback lines inside clamp() bounds that also use rem), for `html { font-size: <n>px }`, and for max-width/max-inline-size on text containers in px. (tools: stylelint, grep, playwright)
- While designing: Write every font-size and text max-width in rem, em or ch, leave html font-size at 100%, and treat any px font-size as a bug.
- Sources: webdev-typography, webdev-design-accessibility, roselli-responsive-type-zoom, mdn-length

### `craft-align-left-body` [minor · craft-consensus]
Multi-line body paragraphs are start-aligned (left in LTR); none is center-aligned or justified, except justified text that also has hyphens: auto and a declared lang.
- Why: Butterick left-aligns web text because browser justification is crude, says justified text must be hyphenated, and says to use centered text sparingly; WCAG 1.4.8 (AAA) asks that users can avoid full justification because it can make reading harder for some people. Butterick's remark that CSS hyphenation support is inconsistent is undated and may be stale.
- Check (automated): For paragraphs with 3 or more rendered lines, fail if computed text-align is center or justify (for justify, pass only if hyphens is auto and html has lang). (tools: playwright, getComputedStyle)
- While designing: Left-align paragraphs of three lines or more and center only short headlines, taglines and single-line captions.
- Often conflicts with styles: hero-centered, newspaper, serif-editorial, quiet-luxury
- Sources: butterick-justified-text, butterick-hyphenation, butterick-summary-of-key-rules, wcag-understanding-visual-presentation

### `craft-caps-letterspacing` [minor · craft-consensus]
Text set in uppercase or small caps has letter-spacing between 0.05em and 0.12em.
- Why: Butterick: capitals are designed to sit next to lowercase and look too tight set together, so add 5-12% letterspacing (CSS 0.05-0.12em), always for all caps; the 12% upper end also matches the WCAG 1.4.12 override value of 0.12 x font size that layouts must survive.
- Check (automated): Select elements with computed text-transform: uppercase or font-variant-caps small-caps (or text that is all uppercase); fail when letter-spacing / font-size is below 0.05 or above 0.12. (tools: playwright, getComputedStyle)
- While designing: Whenever you uppercase a label, eyebrow or button, add letter-spacing of about 0.06-0.1em.
- Often conflicts with styles: oversized-type, condensed, brutalism
- Sources: butterick-letterspacing, butterick-all-caps, butterick-summary-of-key-rules, wcag-understanding-text-spacing

### `craft-caps-short-only` [minor · craft-consensus]
Uppercase text is limited to strings shorter than one line (labels, eyebrows, buttons, short headings); no paragraph or multi-line block is uppercase.
- Why: Butterick: all caps is harder to read at body sizes because readers recognize lowercase word shapes, suits text shorter than one line, and whole paragraphs set in caps get skimmed; emphasize with rules, a label-style heading or a larger size instead.
- Check (automated): Find elements with text-transform: uppercase (or uppercase source text) and compute rendered line count; fail when any has two or more lines or more than about 40 characters (40 is our review threshold). (tools: playwright)
- While designing: Use uppercase only for short labels and set anything longer than a line in sentence case.
- Often conflicts with styles: brutalism, oversized-type, poster, condensed
- Sources: butterick-all-caps, butterick-summary-of-key-rules

### `craft-color-meaning-reserved` [minor · craft-consensus]
A color that signals interactivity or a state (link/accent, focus, error, success, warning) is not reused for non-interactive decoration or for a different state.
- Why: GOV.UK says to use functional colours only in their intended context, to reserve the focus yellow for keyboard focus and to use the error colour only for errors; Apple HIG says not to use the same color for different meanings, for example a brand color that marks a button as interactive should not style non-interactive text.
- Check (hybrid): List the computed colors of links, buttons, focus rings, error and success messages. Fail if any of those exact colors also appears as text or fill on non-interactive elements, or if error and success use the same hue. Confirm by reading the token definitions. (tools: playwright, getComputedStyle)
- While designing: Give links and primary buttons one accent color and never use that accent, or the error or success colors, as pure decoration.
- Often conflicts with styles: maximalist, memphis-playful, neon, monochrome
- Sources: govuk-colour, apple-hig-color

### `craft-color-role-tokens` [minor · craft-consensus]
Colors are defined once as named role tokens (text, secondary text, background, surface, border, accent/link, focus, error, success) and components reference the tokens; literal color values appear only in the token definitions.
- Why: GOV.UK says to reference functional colours by name, not hex, so palette updates propagate, and lists role colours such as text, secondary text, border, focus, error and success; web.dev's theming module stores colors in custom properties redefined for dark mode; Apple HIG prefers semantic colors over hard-coded values.
- Check (automated): Parse the CSS: collect hex/rgb/hsl/oklch literals outside :root, [data-theme] and @media (prefers-color-scheme) token blocks. Fail if components contain literals; confirm the token set includes at least text, background, border, accent, focus, error and success. (tools: stylelint (color-no-hex outside tokens), grep)
- While designing: Declare role-named color custom properties first and write every component color as var(--role).
- Sources: govuk-colour, webdev-design-theming, apple-hig-color

### `craft-contrast-preferences` [minor · craft-consensus]
Custom components stay legible under prefers-contrast: more and forced-colors: active (visible borders, focus and state) and the site strengthens borders or text colors when prefers-contrast: more is set.
- Why: web.dev's media-features module: prefers-contrast: more lets you strengthen colors and borders, Windows contrast themes replace page colors so custom components need fixing under forced-colors, and forced-color-adjust: none is for elements where color carries meaning; its accessibility module says to test with the OS increased-contrast setting. Apple HIG: custom colors need an increased-contrast variant with significantly more differentiation.
- Check (hybrid): Emulate forcedColors: active and contrast: more. Screenshot key pages; confirm buttons, inputs, cards, tabs and focus rings keep a visible boundary and no text disappears. Confirm a @media (prefers-contrast: more) block exists that raises border/text contrast. (tools: playwright (emulateMedia forcedColors, contrast), chrome devtools rendering)
- While designing: Give borders and focus rings a token that increases contrast under prefers-contrast: more and test the page with forced colors on.
- Often conflicts with styles: glassmorphism, minimal, pastel, neo-brutalist
- Sources: webdev-design-media-features, webdev-design-accessibility, apple-hig-color

### `craft-dark-mode-scheme` [minor · craft-consensus]
If the site has a dark theme, it declares color-scheme (meta tag before stylesheets and CSS) and follows prefers-color-scheme by default, so scrollbars, form controls and canvas render in the matching scheme.
- Why: MDN: color-scheme makes the browser adjust canvas, scrollbar and form control colors, the meta tag placed before stylesheets avoids a flash of wrong colors, and prefers-color-scheme (Baseline widely available since Jan 2020) is what styles the rest; light-dark() (Baseline 2024) only works when color-scheme is set. web.dev's theming module redefines custom properties in the dark media query. Apple HIG says to avoid an app-specific appearance setting that overrides the system choice.
- Check (automated): Emulate colorScheme 'dark' and 'light'. Confirm getComputedStyle(html).colorScheme includes the scheme, a <meta name='color-scheme'> exists in head before stylesheets, native inputs/scrollbars are dark in dark, and no first-paint flash of the light theme occurs (screenshot at DOMContentLoaded). (tools: playwright (emulateMedia colorScheme))
- While designing: Set color-scheme and the matching meta tag, define theme tokens for light and dark, and let prefers-color-scheme pick the default unless the brand is deliberately single-theme.
- Often conflicts with styles: dark, light, dark-cyber, mixed-theme
- Sources: mdn-color-scheme, mdn-prefers-color-scheme, mdn-light-dark, webdev-design-theming, apple-hig-dark-mode

### `craft-group-by-proximity` [minor · our-take]
Space between items inside a group (label and field, heading and its paragraph, card contents) is smaller than the space between groups or sections.
- Why: Apple HIG: group related items with negative space, container shapes or separators and keep unrelated items visually distinct; alignment and indentation tell people what is related. Only this one source was read for this claim (the sources.json gestalt-secondary page was not re-read), so it is labeled our-take.
- Check (hybrid): For each heading, compare its margin/padding above with below; for each card or form group, compare the internal gap with the gap to the neighbouring group. Fail where the internal gap is greater than or equal to the external gap. Visual review of screenshots for ambiguous groupings. (tools: playwright, getBoundingClientRect)
- While designing: Keep items in a group close together and put clearly larger gaps between groups, with each heading nearer to its own content than to the previous block.
- Often conflicts with styles: maximalist, collage
- Sources: apple-hig-layout, butterick-headings

### `craft-heading-line-height` [minor · craft-consensus]
Headings that wrap to two or more lines use a unitless line-height of 1.35 or less, and lower than the body line-height.
- Why: USWDS says headings can use line-height 1 to 1.35 and body reading text at least 1.5; GOV.UK heading styles pair 48/50, 36/40 and 24/30 px (ratios about 1.04-1.25) against 19/25 for body.
- Check (automated): For h1-h3 and display text, read computed line-height / font-size; fail if > 1.35 or if it is >= the body ratio. Skip single-line headings. (tools: playwright, getComputedStyle)
- While designing: Give large headings a tight unitless line-height (about 1.1-1.25) so wrapped lines read as one unit.
- Often conflicts with styles: expressive-type
- Sources: uswds-typography, govuk-type-scale

### `craft-icons-one-family` [minor · craft-consensus]
All UI icons come from one family with a single stroke weight, corner style and fill treatment, are drawn on a shared size grid, and their stroke weight visually matches adjacent text.
- Why: Apple HIG: use the same size, level of detail, stroke weight and perspective across all interface icons, and match icon weight to adjacent text weight; web.dev: icons are part of the brand identity so their style should match the rest of the site.
- Check (hybrid): Extract all inline SVG icons; collect distinct stroke-width, stroke-linecap/linejoin, fill-vs-outline treatment and viewBox sizes. Fail if more than one stroke-width or more than one outline/filled style is mixed in the same context. Manual: confirm icons beside text look the same weight. (tools: playwright, SVG parsing)
- While designing: Pick one icon library and one stroke weight and draw or import every icon from it, sized from a small set of steps.
- Often conflicts with styles: maximalist, collage, memphis-playful, illustrative
- Sources: apple-hig-icons, webdev-design-icons

### `craft-icons-svg-currentcolor` [minor · craft-consensus]
UI icons are vector (inline SVG or SVG sprite) that take their color from currentColor or theme tokens, so hover, focus and dark-theme changes apply to them; no raster icons are used for UI controls.
- Why: web.dev: inline SVG can be styled with CSS (fill set to match button text, hover and focus changes applying to icon and text together) while SVG background images are harder to recolor, and SVG fill/stroke can follow the theme custom properties; Apple HIG: use vector formats so icons scale and adapt, with dark-mode variants when needed.
- Check (automated): List all icon elements: fail any PNG/JPG/GIF used as a control icon; for inline SVG, fail hard-coded fill/stroke hex values instead of currentColor or var(--token). Toggle dark theme and hover state and confirm icon color changes with the text. (tools: playwright, SVG parsing)
- While designing: Inline the SVG icons with fill or stroke set to currentColor and size them with em or rem so they follow the text.
- Often conflicts with styles: skeuomorphic, illustrative, dimensional
- Sources: webdev-design-icons, webdev-design-theming, apple-hig-icons, apple-hig-dark-mode

### `craft-image-no-distortion` [minor · craft-consensus]
No image is shown stretched or squashed: its rendered aspect ratio matches its natural ratio unless object-fit: cover or contain crops or letterboxes it, and crops that lose the subject on small screens use object-position or a different crop via picture.
- Why: web.dev: block-size: auto keeps the ratio, forcing another ratio with aspect-ratio can squash or stretch, and object-fit avoids distortion; MDN: the default fill stretches content while cover crops and contain letterboxes; web.dev's picture module says to serve a different crop, not a smaller copy, when an image loses impact at small sizes.
- Check (automated): For every img/video compute renderedW/renderedH and naturalWidth/naturalHeight. If computed object-fit is fill (or none specified) and the ratios differ by more than 2%, fail. For object-fit: cover images in hero/portrait slots, screenshot at 375 px and confirm the subject (face, product) is inside the visible area. (tools: playwright)
- While designing: Fit images with object-fit: cover and an object-position that keeps the subject in view, and never set both width and height that change the ratio.
- Often conflicts with styles: collage, brutalism, memphis-playful
- Sources: webdev-design-responsive-images, mdn-object-fit, webdev-design-picture-element

### `craft-layout-balance` [minor · our-take]
At desktop widths no section keeps all its content to one side and leaves a wide empty region next to it, unless the space is meant (a deliberate margin, a sticky rail, a pause between sections).
- Why: Found when reviewing a real redesign: an accordion sat in a narrow left column at 1440 px and left the right side blank, which read as unfinished next to full-width sections. No source gives a number; the 40% content width and the 25%-of-width asymmetry limits are our own working thresholds, and the result is for a person to judge, not a fail.
- Check (hybrid): At the 1440 px viewport, for each top-level section at least 240 px tall, take the left and right edges of its text (measured with a text range, not the block width) and of its images, controls and media. Flag when the content covers less than 40% of the width and the empty gaps on the two sides differ by 25% of the width or more. A person decides whether the space is meant. (tools: playwright, getBoundingClientRect)
- While designing: Give a section that is narrower than the page a reason: center it, balance it with a second column or an image, or let it span the grid.
- Sources: dailey-design-with-ai-2

### `craft-lead-image-visible` [minor · our-take]
Images in the first screen are at least 40% visible at desktop and mobile widths: not covered by another element and not cut off by the screen edge, unless the layering is the design and enough of each image still shows to read it.
- Why: Found when reviewing a real redesign: on a phone the hero's scatter of frames sat mostly behind the text plate, so the mobile page lost the personality the desktop page had. No source gives a number; the 40% visible limit is our own working threshold, and the result is for a person to judge, not a fail.
- Check (hybrid): At 1440x900 and 390x844 take each img, video and canvas of 80 px or more that starts in the first screen. Sample a 5 by 5 grid of points over its box and count the points where the element itself is on top (elementFromPoint) and inside the screen. Flag when fewer than 40% show. A person decides whether the cover is meant. (tools: playwright, elementFromPoint)
- While designing: At mobile width show fewer, larger frames or move the text off them; do not let the lead images hide behind the headline plate.
- Sources: dailey-design-with-ai-2

### `craft-line-height-body` [minor · craft-consensus]
Body text uses a unitless line-height between 1.3 and 1.7, and long-form reading text uses 1.5 or more.
- Why: Butterick recommends 120-145% of point size and unitless CSS; web.dev gives 1.65 at a 66ch measure and says shorter lines can take more; USWDS says longer texts need at least 1.5 and gives tokens up to 1.75 for extended reading; GOV.UK body is 19px on 25px (about 1.32); WCAG 1.4.8 (AAA) asks that users can get 1.5. Sources overlap only loosely (1.2 to 1.65+), so the band is wide and the 1.5 floor applies to long-form only.
- Check (automated): For p, li, blockquote read the computed line-height and the authored value. Fail if the authored value has a unit (px, rem) rather than a unitless number, or if the computed ratio to font-size is outside 1.3-1.7. For article/long-form containers (more than about 300 words) require >= 1.5. (tools: playwright, getComputedStyle, stylelint)
- While designing: Set line-height as a unitless number (about 1.5 for body, higher for short lines, never a px value) on the root text style.
- Sources: butterick-line-spacing, webdev-typography, uswds-typography, govuk-type-scale, wcag-understanding-visual-presentation

### `craft-motion-duration-range` [minor · craft-consensus]
Functional UI transitions (hover, press, toggle, dropdown, tooltip, modal, drawer) last between 100ms and 400ms and none exceeds 500ms.
- Why: NN/g: about 100 ms for simple feedback, 200-300 ms for large screen changes, 100-400 ms as the general range, 400 ms only for big movements, and over 500 ms starts to feel like a drag; Material 3 tokens run from 50 ms (short1) to 1000 ms (extra-long4) with duration growing with the area or distance covered, so longer values exist for large transitions. Sources differ at the top end; the rule follows the stricter NN/g figure for functional UI and leaves narrative or hero motion to its own review.
- Check (automated): Collect computed transition-duration (+ delay) and animation-duration of interactive elements and overlays (button, a, input, nav, dialog, menu, tooltip, accordion). Fail durations under 100 ms (except color changes under 100 ms, review) or over 500 ms; flag 401-500 ms for review. (tools: playwright, getComputedStyle)
- While designing: Set interface transitions to 150-300ms (100ms for tiny state changes) and keep anything over 400ms for rare, large movements.
- Often conflicts with styles: page-transitions, intro-preloader, chaptered-story, scroll-triggered, parallax, micro-interactions
- Sources: nng-animation-duration, material-android-motion, apple-hig-motion

### `craft-motion-easing-direction` [minor · craft-consensus]
Elements entering the screen use a decelerating curve (ease-out or equivalent), elements leaving use an accelerating curve (ease-in), and linear easing is limited to non-spatial changes (opacity, color) and continuous or looping motion.
- Why: NN/g: linear motion looks unnatural, ease-out is the usual default for entrances, ease-in suits exits, and exits should be slightly shorter than entrances (for example about 300 ms in, 200-250 ms out); Material 3 tokens pair standard-decelerate cubic-bezier(0, 0, 0, 1) with entering and standard-accelerate cubic-bezier(0.3, 0, 1, 1) with exiting motion, and keep a linear token for simple non-stylized motion.
- Check (automated): For transitions that animate transform, top/left or height, read transition-timing-function: fail 'linear' on those properties. For overlays, menus and drawers, check the open state uses ease-out/decelerate and the close state ease-in/accelerate and has a duration no longer than the open duration. (tools: playwright, getComputedStyle)
- While designing: Use cubic-bezier(0, 0, 0.2, 1) style ease-out for things appearing, an ease-in for things leaving, and keep exits a bit faster than entrances.
- Often conflicts with styles: marquee, ambient-loop, brutalism, retro-computing
- Sources: nng-animation-duration, material-android-motion

### `craft-motion-frequent-quick` [minor · craft-consensus]
Animations on frequently repeated interactions (hover, press, toggle, menu open, tab change) are 200ms or shorter and never block input: the next click, key press or scroll works while the animation is running.
- Why: NN/g: the more often users see an animation, the shorter and subtler it should be, with about 100 ms for simple feedback; Apple HIG: avoid adding motion to frequently used interactions, keep feedback brief, and let people cancel motion so they do not wait for it to finish. The 200 ms ceiling combines NN/g's 100 ms feedback and 200-300 ms large-change figures.
- Check (hybrid): Automated: collect durations of hover/active/focus/toggle transitions and fail above 200 ms. Manual/scripted: trigger an animation (open menu) and immediately click the next target, press Escape or scroll; fail if the input is ignored or delayed until the animation ends. (tools: playwright)
- While designing: Make hover and press feedback about 100-200 ms and keep every control interactive while its animation plays.
- Often conflicts with styles: micro-interactions, hover-effects, cursor-effects, text-effects
- Sources: nng-animation-duration, apple-hig-motion

### `craft-reduced-motion-replace` [minor · craft-consensus]
Under prefers-reduced-motion: reduce, large spatial motion (parallax, scroll-linked movement, large translate or scale, autoplaying loops) is removed or replaced with opacity or color changes, while essential and feedback animations remain in a gentler form.
- Why: web.dev's accessibility module: limit scaling and movement, color changes and opacity or cross-fades are generally acceptable; its media-features module: keep reduced-motion alternatives free of the problematic movement and do not remove meaningful feedback entirely; web.dev's reduced-motion article lists parallax, autoplaying video, animated images and attention-grabbing motion as things to reduce and says essential movement is outside the preference; NN/g says to remove or minimize animations; Apple HIG says custom motion should respect accessibility settings. This refines the existing a11y-reduced-motion by saying what to do under the preference.
- Check (hybrid): Emulate reducedMotion: reduce. List computed transform/animation on elements that move more than about 20px or scale more than 5% (our review thresholds); fail if any remains. Confirm state changes (open, selected, error) still show a visible, non-spatial cue such as opacity or color. Confirm autoplay media and GIF/WebP loops are stopped or static. (tools: playwright (emulateMedia reducedMotion))
- While designing: Wrap movement in a no-preference media query and give reduce users opacity or color feedback instead of travel and scale.
- Often conflicts with styles: parallax, scroll-triggered, ambient-loop, realtime-3d, text-effects, hero-video
- Sources: webdev-design-accessibility, webdev-design-media-features, webdev-prefers-reduced-motion, nng-animation-duration, apple-hig-motion

### `craft-spacing-scale-tokens` [minor · craft-consensus]
All margin, padding and gap values come from one spacing scale defined as tokens on a single base unit, with at most 12 distinct non-zero spacing values in use on a page.
- Why: web.dev: pick a spacing system (a fixed gutter or a multiple of em) and store values as custom properties; GOV.UK defines units 0-9 in 5px steps up to 15px then larger; USWDS tokens are multiples of 8px with 4px half-steps; Utopia builds a named space palette and prefers as few sizes as possible. Base units differ (5px, 8px, em multiples), so any consistent base is acceptable. The cap of 12 is our threshold (GOV.UK has 9 non-zero units).
- Check (automated): At 1280px collect computed margin, padding, row-gap and column-gap (block/inline) of all elements, round to 0.5px, ignore 0 and 1-2px borders, and count distinct values; fail above 12 or when a value is not a multiple of the base unit (4 or 8, or the project's token base). Confirm values come from spacing custom properties. (tools: playwright, getComputedStyle)
- While designing: Define a spacing token scale (for example 4, 8, 12, 16, 24, 32, 48, 64, 96) first and use only those values for padding, margin and gap.
- Often conflicts with styles: maximalist, collage, unconventional-layout, asymmetric
- Sources: webdev-css-spacing, govuk-spacing, uswds-spacing-units, utopia-space-palette

### `craft-type-scale-tokens` [minor · craft-consensus]
All text sizes come from a defined scale of named tokens with at most 8 distinct sizes in use on a page (a fluid token counts once, not per viewport).
- Why: web.dev tells designers to build a typography scale into the design system; GOV.UK defines 7 scale points with line heights that are multiples of 5px and says to align any new style to an existing point; Utopia generates a named scale (the example in its post uses 5 steps up and 2 down). The count 8 is derived from those two (7 and 8 steps) and is our threshold.
- Check (hybrid): Collect computed font-size of all rendered text nodes at 1280px, round to 0.5px, and count distinct values. Fail above 8. Then confirm the sizes map to named tokens (custom properties) in the CSS. (tools: playwright, getComputedStyle)
- While designing: Define 6-8 type-size tokens up front, give each a role (caption, body, lead, h3, h2, h1, display), and use only those.
- Often conflicts with styles: expressive-type, oversized-type, maximalist, experimental
- Sources: webdev-typography, govuk-type-scale, utopia-typography

### `craft-weight-thin-limited` [minor · craft-consensus]
Body text and any text under 24px uses font-weight 400 or heavier; weights of 300 or lighter appear only at display sizes (24px and above).
- Why: Apple HIG says to avoid Ultralight, Thin and Light because they are hard to see at small sizes; WCAG 1.4.6 notes thin fonts render fainter due to anti-aliasing so a thicker font or a stronger color pair is advised; Butterick says heavier black/ultra weights are for display, not body. The 24px cut-off is WCAG's large-text size and our threshold.
- Check (automated): Collect computed font-weight and font-size of every text node. Fail where weight <= 300 and size < 24px. Variable fonts: check the computed value, not the file. (tools: playwright, getComputedStyle)
- While designing: Use weight 400-600 for text below 24px and reserve light and thin weights for large display lines.
- Often conflicts with styles: minimal, quiet-luxury, luxury, serif-display
- Sources: apple-hig-typography, wcag-understanding-contrast-enhanced, butterick-bold-or-italic

### `craft-body-tracking-normal` [advisory · craft-consensus]
Body paragraphs in lowercase text keep letter-spacing at normal (0); added tracking on body text is limited to small text, and large display headlines may be tightened but not widened.
- Why: Butterick: lowercase usually needs no letterspacing, text smaller than about 9pt may benefit from slight added spacing, and large lowercase headlines are often tightened.
- Check (automated): For p, li and td at 16px or more, fail if computed letter-spacing is not 'normal' or 0 (allow within +-0.01em). For text 24px and above, flag positive letter-spacing on lowercase headlines for review. (tools: playwright, getComputedStyle)
- While designing: Leave letter-spacing at normal on body text and use small negative tracking, if any, only on large headlines.
- Often conflicts with styles: expressive-type, luxury, quiet-luxury
- Sources: butterick-letterspacing, butterick-summary-of-key-rules

### `craft-container-max-width` [advisory · craft-consensus]
Page content sits in a centered container with a maximum width of 1400px or less; only backgrounds and full-bleed media may exceed it.
- Why: GOV.UK's default maximum page width is 1020px (wider only when content needs it) and USWDS names widths up to desktop 1200px and widescreen 1400px. These are the two design systems' own choices; neither states the number as a universal rule, so the rule is advisory.
- Check (automated): At a 1920px viewport, measure the bounding box of the main content wrapper(s): fail when text, cards or controls span wider than 1400px or touch both viewport edges; allow elements flagged full-bleed (backgrounds, images, video). (tools: playwright, getBoundingClientRect)
- While designing: Wrap content in a centered container with max-inline-size of 1200-1400px and let only backgrounds and media run edge to edge.
- Often conflicts with styles: hero-full-bleed, gallery-wall, bento-grid, poster, maximalist, oversized-type
- Sources: govuk-layout, uswds-spacing-units

### `craft-contrast-body-enhanced` [advisory · standard]
Primary body text reaches at least 7:1 contrast against its background, and secondary or muted text at least 4.5:1.
- Why: WCAG 1.4.6 (AAA) sets 7:1 (4.5:1 for large text); Apple HIG says 4.5:1 minimum and 7:1 for custom foreground/background colors, especially small text. The 4.5:1 floor for secondary text is WCAG 1.4.3 AA (already covered by a11y-contrast-text); this rule only adds the 7:1 target for primary text, which is AAA and so advisory.
- Check (automated): Compute the WCAG 2.x contrast ratio of the main body text color against its actual background in both light and dark themes; fail the target if under 7:1, and list muted text under 4.5:1 as a failure of a11y-contrast-text. (tools: axe-core, colorjs.io, playwright)
- While designing: Choose a near-black (or near-white in dark mode) body color that reaches 7:1 and keep muted text at 4.5:1 or better.
- Often conflicts with styles: pastel, quiet-luxury, minimal, gradient-aurora, atmospheric
- Sources: wcag-understanding-contrast-enhanced, wcag-contrast-minimum, apple-hig-dark-mode

### `craft-emphasis-single` [advisory · craft-consensus]
Inline emphasis uses either bold or italic on a run of text, never both, and is limited to short phrases; underline is reserved for links.
- Why: Butterick: use bold or italic, not both, only sparingly, because both are harder to read than regular text and stacking leaves no room for further emphasis; do not underline text except possibly web links.
- Check (automated): Find inline em/strong/b/i/span runs with both font-weight >= 600 and font-style italic; find text-decoration: underline on non-link elements; flag emphasized runs over about 12 words for review (12 is our threshold). (tools: playwright)
- While designing: Emphasize a phrase with bold or italic, not both, and never underline anything that is not a link.
- Often conflicts with styles: expressive-type, text-effects
- Sources: butterick-bold-or-italic, butterick-summary-of-key-rules

### `craft-font-families-few` [advisory · our-take]
The page uses at most two font families (plus an optional monospace for code), with hierarchy built from size, weight and color within them.
- Why: Apple HIG says to minimize the number of typefaces because many faces obscure hierarchy and hurt readability; web.dev notes each added font file increases load time. The figure of two is our own threshold: neither source states a number.
- Check (automated): Collect distinct computed font-family first entries across all rendered text, ignoring generic fallbacks and monospace on code/pre. Fail above two. (tools: playwright, document.fonts)
- While designing: Pick one family (or one pair) and create hierarchy with size, weight and color instead of adding another typeface.
- Often conflicts with styles: maximalist, mixed-pairing, experimental, memphis-playful, collage
- Sources: apple-hig-typography, webdev-typography

### `craft-heading-levels-limit` [advisory · craft-consensus]
Long-form content shows at most three visually distinct heading levels, and the size step between adjacent levels is small enough that a heading is not mistaken for display text.
- Why: Butterick says to use no more than three heading levels (two is better), to raise size only slightly and to emphasize with space; GOV.UK's default pairing uses just three heading styles (l, m, s) for h1-h3, with a larger fourth only for long-form pages.
- Check (hybrid): In article/long-form containers, list the distinct computed (font-size, font-weight) pairs of h1-h6. Fail if more than three look distinct. Manual: confirm each level is distinguishable from the next by size, weight or space. (tools: playwright)
- While designing: Style at most three heading levels in articles and separate them mainly with space above and below.
- Often conflicts with styles: expressive-type, editorial
- Sources: butterick-headings, govuk-headings

### `craft-heading-sentence-case` [advisory · craft-consensus]
Headings and button labels are written in sentence case and are not set in all caps when longer than one short line.
- Why: GOV.UK says to write headings in sentence case; Butterick advises against title case and against all-caps headings that are full sentences, allowing caps only for text shorter than one line.
- Check (hybrid): Extract heading text; flag headings where most words are capitalized (title case) for manual review. Flag any heading with computed text-transform: uppercase that wraps to more than one line. (tools: playwright)
- While designing: Write headings as sentences in sentence case and reserve uppercase for short labels and eyebrows.
- Often conflicts with styles: serif-editorial, newspaper, luxury
- Sources: govuk-headings, butterick-headings, butterick-all-caps

### `craft-palette-oklch-ramps` [advisory · craft-consensus]
Tints, shades and state variants (hover, active, disabled) of a brand color are generated from one base by changing lightness with hue and chroma held fixed (OKLCH, color-mix() or relative color syntax) instead of hand-picked unrelated hex values.
- Why: web.dev: in OkLCh changing hue does not change perceived lightness or saturation, which makes adjustments predictable; MDN lists lightness ramps and theming variants from one base as use cases and gives oklch() Baseline Widely available since May 2023; USWDS shows the payoff of lightness-ordered grades, where a grade gap of 40/50/70 predicts WCAG AA large/AA/AAA (written for WCAG 2.0). Contrast must still be computed with the WCAG 2.x formula; OKLCH lightness is not a contrast guarantee.
- Check (hybrid): Inspect the color tokens: for each ramp, confirm hover/active/tint values are derived with oklch()/color-mix()/relative color from one source token, or that their OKLCH hue differs by less than about 5 degrees and chroma follows a smooth curve (our tolerance). Still run the WCAG ratio on each text pairing. (tools: colorjs.io)
- While designing: Derive every tint and state color from the base token by changing OKLCH lightness only, then verify contrast numerically.
- Often conflicts with styles: pastel, neon
- Sources: webdev-css-color, mdn-oklch, uswds-color-overview

### `craft-space-responsive-large` [advisory · craft-consensus]
Section-level spacing (section padding, page gutters, large gaps) is smaller on a 360px viewport than on a 1280px viewport, while the smallest steps stay constant.
- Why: GOV.UK's responsive scale keeps units 0-3 the same at every size and lets units 4-9 grow above 640px (unit 9 is 40px on small screens and 60px on large); Utopia interpolates its named space steps between a small and large viewport so layouts breathe without per-breakpoint rules.
- Check (automated): Measure the computed vertical padding/margin of the main section containers at 360 and 1280 px; require the 1280 value to be greater. Measure small component gaps (4-16px) and require them to be unchanged within 2px. (tools: playwright, getComputedStyle)
- While designing: Scale section padding with clamp() or a breakpoint step so it grows with the viewport while small gaps stay fixed.
- Sources: govuk-spacing, utopia-space-palette

### `craft-text-wrap-balance-pretty` [advisory · our-take]
Headings, captions and short display text set text-wrap: balance, and long paragraphs set text-wrap: pretty, with no layout depending on either.
- Why: MDN says balance evens line lengths but browsers apply it only to blocks of six lines or fewer in Chromium and ten or fewer in Firefox (so it suits headings, captions, blockquotes), and pretty uses a slower algorithm to reduce orphans for body copy. MDN's text-wrap page lists Baseline Widely available (March 2024) while the text-wrap-style page lists Baseline 2024 newly available (October 2024), so treat it as progressive enhancement. Only MDN was read, so this is labeled our-take.
- Check (automated): Check computed text-wrap-style on h1-h3, figcaption, blockquote (expect balance) and on long p (expect pretty). Confirm nothing breaks when the declaration is removed. (tools: playwright, getComputedStyle)
- While designing: Add text-wrap: balance to headings and captions and text-wrap: pretty to long paragraphs as a progressive enhancement.
- Sources: mdn-text-wrap-style, mdn-text-wrap
