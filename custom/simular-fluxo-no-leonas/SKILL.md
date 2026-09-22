---
name: Simular fluxo no Leonas
description: >-
  Use this when testing or validating a Leonas flow in the built-in Simulador
  (local, no WhatsApp): always reset first, start with oi, walk the full path,
  and document stuck phases for Manutenção.
---
# Simular fluxo no Leonas

Assumes signed-in Chrome on `app.leonasolutions.io`. Use the browser only for the Simulador UI (no WhatsApp send).

## Inputs
- `{flow_url}` — editor URL, e.g. `https://app.leonasolutions.io/flows/{id}/edit`
- `{start_message}` — first client message; default `oi`
- `{branches_to_cover}` — paths to walk (e.g. Disponible, No disponible, plegable, negociar, USDT)
- `{expected_copy}` — optional checklist of Spanish texts / nodes that must appear

## Every run (mandatory)
1. Open `{flow_url}` and confirm the canvas loaded.
2. **Reset the Simulador before every simulation** (including routine runs and re-runs after a branch):
   - If a previous test is open, close the Simulador pane (X) or clear the run so the pane shows "Envie uma mensagem para começar o teste" / "Digite para começar...".
   - Reopen with **▶ Simular** if needed.
   - Do not continue an old conversation; always start from a clean Simulador.
3. Type `{start_message}` (default `oi`) and send. Confirm "Fluxo iniciado." and the first bot message. Canvas nodes highlight green as the flow advances.
4. If the Simulador closes unexpectedly, click **▶ Simular** again, reset if needed, and restart from `oi`.
5. Walk the **full** intended path(s) in `{branches_to_cover}` as the customer until each path ends or hits a clear dead end. Prefer menu button labels; otherwise type free text. After each reply check language, product name, active node, and fluidity (no stuck wait with no next step).
6. For a new branch, **reset again** and start from `oi` — never mix branches in one dirty run.
7. Also validate: if the client would send image or audio, the bot must answer in **text** (flag if the flow has no textual reply path for media).
8. Optional: **Simular timeout (sem resposta)** only when checking timeout behavior.

## Report (document for Manutenção)
Post a clear analysis the Manutenção agent can act on:
- Branches run (each from a fresh reset + `oi`) and pass/fail
- Where it is **not fluid** — phase/node where the dialogue stalls or confuses
- Exact bot messages that are wrong, missing, or mismatched vs `{expected_copy}`
- Media case: image/audio → text reply present or missing
- Concrete suggestion of what to change (node / copy / conditional)
- Tag Manutenção when reporting gaps; stay quiet on routine runs only if everything stayed fluid and complete
- Do **not** send WhatsApp or publish the flow

## Notes
- Prefer stable UI targets: **▶ Simular**, Simulador input, menu labels, node titles — not coordinates.
- Do not embed credentials; login lives in the browser profile.
