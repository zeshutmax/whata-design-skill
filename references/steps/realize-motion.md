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
