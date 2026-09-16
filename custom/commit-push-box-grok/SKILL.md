---
name: Commit + push box-grok
description: >-
  Use this when a publishable Grok box folder is updated — commit and push to
  the matching public diegofornalha/box-grok-* GitHub repo (no clone; scrub
  secrets). Also when the user asks to sync/publish box-grok updates.
---
# Commit + push box-grok

Whenever a **publishable folder on the Grok Bot box** is created or updated, mirror it to its matching **public** `diegofornalha/box-grok-*` GitHub repo (commit + push). Keep secrets out.

## When this applies
- After editing any mapped local folder/file below
- When the user asks to publish/sync/update box-grok repos
- After open-sourcing new box content into a new `box-grok-*` repo (add the mapping)

## Folder → repo map
| Local path | GitHub repo |
| --- | --- |
| `/workspace/grok-bot/` | `diegofornalha/box-grok-grok-bot` |
| `/workspace/hookify-demo/` | `diegofornalha/box-grok-hookify-demo` |
| `/home/box/guias-hermes/` | `diegofornalha/box-grok-guias-hermes` |
| `/home/box/reference/` | `diegofornalha/box-grok-reference` |
| `/home/box/start-ssh.sh` | `diegofornalha/box-grok-scripts` (file as `start-ssh.sh`) |
| `/workspace/plugins-catalogo.txt`, `/workspace/claude-catalog-basico2.txt` | `diegofornalha/box-grok-workspace-notes` |
| `/workspace/guimoo-mcp/` | `diegofornalha/box-grok-guimoo-mcp` (exclude `node_modules`, `.env`, battery dumps / live CRM validation with PII) |
| `/home/box/agent-data/workflows/` (user skills) | **not this skill** — use Sync skill → skills-grok |

Sibling (already separate): `diegofornalha/skills-grok`.

## Never publish here
`sand-host`, `deps`, `sand-data`/`agent-data` secrets, `.ssh`, `.hermes`, `.claude`, `.config`, `.garmin-tokens`, `.cloudflared`, `chrome-profile`, `.env*`, media/binaries, backups, transcripts, third-party exports, live CRM validation dumps with real contact data.

## How to push (no git clone)
Prefer GitHub Contents API via `gh` (owner auth). Do **not** clone repos onto the box.

### Per file (create/update)
1. Scrub secrets in a temp copy under `/workspace/` if needed (phones, tokens, personal names) before upload.
2. `CONTENT_B64=$(base64 -w0 "<local-file>")`
3. `SHA=$(gh api repos/<owner>/<repo>/contents/<path> --jq .sha 2>/dev/null || true)`
4. `PUT` with `message`, `content`, and `sha` when updating.

Commit messages: `Update <path>` / `Add <path>` — short, present tense.

### Deletes
If a tracked file was removed locally, DELETE remote via Contents API with its `sha`.

### New folder not in the map
1. Create public repo `diegofornalha/box-grok-<slug>` (`gh repo create … --public`)
2. Push full folder (minus secrets) with README noting box VM origin
3. Update this skill’s map (and sync this skill to skills-grok)

## Safety
- Never force-push or rewrite history
- Never commit `.env`, PEMs, credentials, tokens, private Notion links, WhatsApp numbers (redact)
- Keep/refresh `.gitignore` on each repo (`.env*`, `*.pem`, `*credentials*`, `*secret*`, `.ssh/`, `node_modules/`, `.venv*/`, `*.mp4`)
- Don’t touch global git config

## After push
Tell the user which repos/paths updated and the GitHub URLs. If `gh` auth fails or the remote is missing, say so plainly.

## Anti-patterns
- Monorepo dump of the whole box
- Cloning `box-grok-*` just to copy files
- Publishing hermes/claude/config home as “updates”
- Skipping scrub because “it’s already public”
