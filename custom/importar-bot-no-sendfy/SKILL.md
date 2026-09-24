---
name: Importar bot no Sendfy
description: >-
  Use this when importing a WhatsApp bot/funnel JSON into Sendfy
  (app.sendfy.app) via Importar Bot on the Bots list — pick a .json funnel file
  and confirm before committing.
---
# Importar bot no Sendfy

Assumes signed in to [Sendfy](https://app.sendfy.app/) as the account owner (Google OAuth or email). Prefer `?locale=pt-BR` URLs.

There is no Sendfy connector in Cursor for this step; use the signed-in browser. Login is out of scope — if redirected to `/users/sign_in`, stop and report that sign-in is required.

## Inputs
- `{funnel_json_path}` — path to a Sendfy bot/funnel JSON export (nodes + connections), e.g. a fixture like the Atendimento menu funnel
- Stop after opening the file picker if the user only asked to open import; select a file and confirm only when they asked to import

## Steps
1. Open `https://app.sendfy.app/bots?locale=pt-BR` (or from the dashboard: expand the left sidebar, click **Bot/Funil**).
2. Confirm the **Bots WhatsApp** page loaded (empty state shows "Nenhum bot cadastrado." when none exist).
3. Click **Importar Bot**.
4. The UI opens a **native file picker** (no in-page modal, paste area, or labeled fields). Choose `{funnel_json_path}`.
5. After the file is selected, observe what the app does next (reload of the list, toast, editor open, or error). **Confirm with the user before any final Importar/Salvar/Confirm control if one appears.** Do not import unprompted.
6. Report: whether the bot appeared in the list (name, WhatsApp, status), final URL, and any error (including Cloudflare 502 on related pages).

## Notes
- Prefer labeled UI and these URLs over coordinates.
- **+ Criar Novo Bot** is a different flow (`/bots/new`) — use [Criar bot no Sendfy](sand-workflow:criar-bot-no-sendfy) for that.
- Accepted file extensions may not be shown in the picker; use a Sendfy funnel JSON with `nodes` and `connections`.
- Do not send real WhatsApp messages as part of import.
