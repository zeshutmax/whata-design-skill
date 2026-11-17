# Step: Audit the landscape (`need-landscape`, stage need)
**Goal:** Look at how comparable companies present themselves, and what is overused in the niche.
**Your role:** See how comparable companies present themselves, and what the niche has made generic.
**Inputs:** need-statement, audience-profile  
**Output artifact:** landscape-audit -> `design/01-need/landscape-audit.md`
## Procedure
1. Query the library: search_sites with the industry and site-type tags that fit the need; also one or two adjacent industries.
2. Review at least 6 sites. If the library has fewer than 6 that fit the industry, add sites found on the web (open and view each) and mark them `not in library`. For each note the art style, hero type, page skeleton, how the primary action is presented, and anything the audit says not to copy (get_site returns audit failures).
3. Name the niche's default look in one sentence ('white, blue gradient, three icon cards'). That is what to avoid being indistinguishable from, unless the brief says otherwise. [Our take]
4. Note what nobody does that the audience might want.
## Tools
- `search_sites`: allOf: [industry slug, site-type slug]; status any; limit 20
- `get_site`: for each reference: tags, palette roles, audit summary
- `list_tags`: to find the right industry and site-type slugs
## Output template
```markdown
# Landscape audit
| Site | Art style | Hero | Skeleton | How it asks for the primary action | Do not copy (audit) |
|---|---|---|---|---|---|
## The niche's default look
## Gaps nobody fills
```
## Gates
- [ ] At least 6 sites from at least 3 different art-style families.
- [ ] A one-sentence description of the default look exists.
## Done when
- The table has 6 or more sites and the default look is named.
## Pitfalls
- Only studying direct competitors.
- Copying a reference without reading its audit caveats.
