---
name: Sync skill → skills-grok
description: >-
  Use this when creating, updating, or deleting a user-created Grok skill —
  after the local skill change, sync that skill folder to the public GitHub repo
  diegofornalha/skills-grok.
---
# Sync skill → skills-grok

Whenever a **user-created** Grok skill is created, updated, or deleted, mirror that change to the public repo [`diegofornalha/skills-grok`](https://github.com/diegofornalha/skills-grok).

## When this applies
- After `update_state` (target `skill`, action `write` or `delete`) for a skill under `/home/box/agent-data/workflows/`
- When the user asks to publish/sync skills to GitHub
- **Not** for Cursor-managed skills or plugin skills (those are not owned by the user)

## Target layout in the repo
- User skills live at: `custom/<skill-id>/` (same folder name as the local workflow id)
- Keep `SKILL.md` and any sibling files in that folder
- Do **not** put plugin/Cloudflare skills under `custom/`; those stay under `cloudflare/` if present

## How to sync (no git clone)
Prefer the GitHub Contents API via `gh` (already authenticated as the repo owner). Do not clone the repo onto the box or a user machine.

### Create or update a skill
1. Confirm the local folder: `/home/box/agent-data/workflows/<skill-id>/`
2. For each file in that folder (at least `SKILL.md`):
   - Read file bytes, base64-encode (no newlines in the payload)
   - If the remote file already exists, GET it first to obtain `sha`
   - `PUT /repos/diegofornalha/skills-grok/contents/custom/<skill-id>/<relative-path>` with `message`, `content` (base64), and `sha` when updating
3. Commit message style: `Add skill <skill-id>` / `Update skill <skill-id>`

Example for a new or updated `SKILL.md`:

```bash
SKILL_ID="<skill-id>"
PATH_IN_REPO="custom/${SKILL_ID}/SKILL.md"
CONTENT_B64=$(base64 -w0 "/home/box/agent-data/workflows/${SKILL_ID}/SKILL.md")
SHA=$(gh api "repos/diegofornalha/skills-grok/contents/${PATH_IN_REPO}" --jq .sha 2>/dev/null || true)
if [ -n "$SHA" ]; then
  gh api --method PUT "repos/diegofornalha/skills-grok/contents/${PATH_IN_REPO}" \
    -f message="Update skill ${SKILL_ID}" -f content="$CONTENT_B64" -f sha="$SHA"
else
  gh api --method PUT "repos/diegofornalha/skills-grok/contents/${PATH_IN_REPO}" \
    -f message="Add skill ${SKILL_ID}" -f content="$CONTENT_B64"
fi
```

Repeat for any other files in the skill folder (preserve relative paths under `custom/<skill-id>/`).

### Delete a skill
1. List remote files under `custom/<skill-id>/` via the Contents API
2. DELETE each file with its `sha` and message `Remove skill <skill-id>`

### README index (optional but preferred)
If `README.md` at the repo root has a custom-skills list, add/update/remove the row for `<skill-id>` in the same sync (fetch → edit → PUT with sha). If editing the README is ambiguous, skip it and still sync the skill folder.

## After sync
- Tell the user the skill pill `[name](sand-workflow:<id>)` and the GitHub path/URL, e.g. `https://github.com/diegofornalha/skills-grok/tree/main/custom/<skill-id>`
- If the repo is missing or `gh` auth fails, say so plainly and do not pretend the sync succeeded

## Anti-patterns
- Do not sync plugin or managed skills into `custom/`
- Do not clone `skills-grok` just to copy files
- Do not force-push or rewrite history
- Do not put secrets, tokens, or machine-specific paths in skill files before publishing
