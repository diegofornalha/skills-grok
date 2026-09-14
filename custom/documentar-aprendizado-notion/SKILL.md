---
name: documentar-aprendizado-notion
description: >-
  Use this when documenting learnings in Notion: decide dedicated page vs
  consolidate (unique + substantial → dedicated; otherwise section in a parent);
  create dedicated without asking when it qualifies; never update an existing
  page without approval.
---
# Documentar aprendizado no Notion

## When to apply
When the user wants to document learnings, decisions, glossaries, or runbooks in Notion.

## Dedicated page vs consolidate (Diego’s rule)
Decide **before** writing:

**Dedicated page** only when **both** are true:
1. **Unique** — topic has its own identity (not just a bullet inside Plugin/Auth/etc.)
2. **Substantial** — needs more than a short section (rules, checklist, anti-patterns, multiple paths)

**Otherwise → consolidate** into the best existing parent page (curso, glossário, hub) as a clear section. Do **not** invent a thin second page.

Examples:
- “GitHub no Grok” (MCP + `gh` + skills, regras) → dedicated OK
- “PAT Classic” alone → section inside the GitHub hub, not a separate page
- One-line glossary tweak → edit the glossário page (with approval if updating existing)

## Policy
1. **Always search Notion first** for related/overlapping pages.
2. Apply **Dedicated vs consolidate** above.
3. **If dedicated** → create the new page (do not ask “create new page?” when the user already asked to document). Prefer `creation_mode: draft` unless a parent was named.
4. **If consolidate** → do **not** create a thin page. Ask which parent to update (or propose the best one) and **only update after explicit approval**.
5. **After a dedicated page exists**, if search found related pages → **ask** whether to consolidate/link (merge into / cross-link). Never silently merge.
6. **Never consolidate or update an existing page** without explicit approval.
7. If search found nothing related and the learning is substantial → deliver the new dedicated page link; no consolidate prompt needed.

## Steps
1. Capture the learning in clear bullets (definitions, rules, anti-patterns, examples).
2. Search Notion (fetch `self`, then search).
3. Decide dedicated vs consolidate.
4. Dedicated → create page; return link. Consolidate → propose parent + section outline; wait for approval; then update.
5. If related pages overlap a new dedicated page, ask: consolidate into X / Y / keep separate / cancel.
6. Only after approval, update chosen existing page(s) and optionally add cross-links.

## Anti-patterns
- Asking permission to create when the user already asked to document **and** the topic qualifies as dedicated.
- Creating a second page for a sub-detail that fits as a section (e.g. PAT Classic beside an existing GitHub hub).
- Silently merging into an old page.
- Skipping the post-create consolidate question when clear overlaps exist.
- Using hookify for this Notion decision flow (this skill + memory are enough).

## Done when
Content is live in the right place (dedicated page **or** approved section in a parent); overlaps were decided by the user when relevant.
