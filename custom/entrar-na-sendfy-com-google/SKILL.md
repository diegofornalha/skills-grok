---
name: Entrar na Sendfy com Google
description: >-
  Use when the box Chrome is on Sendfy sign-in (or redirected there) and you
  need a logged-in session — Google OAuth with Diego's saved Chrome account, no
  password typed.
---
# Entrar na Sendfy com Google

Assumes the box Chrome profile already has Diego Fornalha's Google session (`diegofornalha@gmail.com`). Prefer `?locale=pt-BR` URLs. Never ask Diego to type a password when this chooser path is available.

## Inputs
- `{destination}` — path to open after login (default: `/webhooks?locale=pt-BR`). Examples: `/`, `/webhooks?locale=pt-BR`, `/bots?locale=pt-BR`
- `{google_account_label}` — account to pick on Google accountchooser (default: **Diego Fornalha** / `diegofornalha@gmail.com`). Do **not** pick Lucas dos Santos unless Diego asks.

## Steps
1. Open `https://app.sendfy.app{destination}` (or `https://app.sendfy.app/users/sign_in` if already on the login wall).
2. If the app loads without a login wall, stop — already signed in. Report the final URL.
3. On **Realize seu login** (`/users/sign_in`):
   - Click the **Google** button (do not fill Email/Password).
4. On Google **accountchooser** (`accounts.google.com/.../accountchooser`, prompt like "Escolha uma conta para continuar no Sendfy"):
   - Click **Diego Fornalha** (`diegofornalha@gmail.com`).
   - Do not click Lucas dos Santos or "Usar outra conta".
5. Wait for redirect back to Sendfy. Success signals:
   - Toast/banner: **Autenticado com sucesso via conta Google** (or equivalent)
   - URL under `https://app.sendfy.app/...` (often the `{destination}` or dashboard)
6. If Google asks for password, 2FA, captcha, or passkey: stop and hand the box to Diego (`request_box_help`). Do not invent credentials.
7. If Email/Password is the only path and Google is missing: stop and report — this skill does not cover password login.

## Report
- Final URL and whether login was needed
- Which Google account was selected (name/email labels only)
- Any blocker (chooser missing Diego's account, extra Google challenge, still on `/users/sign_in`)

## Notes
- Prefer labeled UI and URLs over coordinates
- No Sendfy connector; use the signed-in box browser
- Session lives in this agent's Chrome profile (desktops are not shared across agents)
- Demonstrated ~2026-09-23: Google button → Diego Fornalha → landed on `/webhooks?locale=pt-BR` with success toast; empty webhooks table; no password typed
