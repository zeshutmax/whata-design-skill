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
