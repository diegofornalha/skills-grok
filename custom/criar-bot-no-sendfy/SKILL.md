---
name: Criar bot no Sendfy
description: >-
  Use this when opening or creating a WhatsApp bot in Sendfy (app.sendfy.app) —
  navigate to Bots, open Criar Novo Bot, optionally fill name and WhatsApp
  instance, and confirm before saving.
---
# Criar bot no Sendfy

Assumes signed in to [Sendfy](https://app.sendfy.app/) as the account owner (Google OAuth or email). Prefer `?locale=pt-BR` URLs.

## Inputs
- `{bot_name}` — text for **Nome do Bot** (example placeholder in UI: "Ex: Atendimento Comercial")
- `{whatsapp_instance}` — which WhatsApp to attach (dropdown **WhatsApp para o Bot**; only instances with Não oficial or Evolution API Business appear)
- `{active}` — **Ativo** toggle (default: on, as in the demo)
- Stop after opening the form if the user only asked to open create-bot; fill and save only when they asked to create/save a bot

## Steps
1. Open `https://app.sendfy.app/bots?locale=pt-BR` (or from the dashboard: expand the left sidebar via the hamburger, click **Bot/Funil**).
2. Confirm the **Bots WhatsApp** page loaded. Empty state shows "Nenhum bot cadastrado."
3. Click **+ Criar Novo Bot**.
4. Land on `https://app.sendfy.app/bots/new?locale=pt-BR` with the **Configurações Iniciais** panel:
   - **Nome do Bot** (text)
   - **WhatsApp para o Bot** (dropdown)
   - **Ativo** (toggle)
5. If creating (not just opening):
   - Type `{bot_name}` into **Nome do Bot**
   - Choose `{whatsapp_instance}` in **WhatsApp para o Bot**
   - Set **Ativo** to `{active}`
6. **Confirm with the user before clicking Salvar.** Do not click **Salvar** unprompted. **Voltar** cancels back to the bots list.

## Report
- Final URL and whether the form was only opened or a bot was saved
- Bot name and WhatsApp instance chosen (never log credentials)
- Any blocker (not signed in, empty WhatsApp dropdown, save error)

## Notes
- Prefer labeled UI and these URLs over coordinates
- There is no Sendfy connector; use the signed-in browser
- Login (Google or email/password) is out of scope for this skill — if redirected to `/users/sign_in`, stop and report that sign-in is required
