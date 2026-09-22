---
name: Simular fluxo no Leonas
description: >-
  Use this when testing or validating a Leonas flow in the built-in Simulador
  (local test without WhatsApp) — open the flow editor, run the dialogue as the
  customer, cover branches, and report gaps.
---
# Simular fluxo no Leonas

Assumes signed-in Chrome on `app.leonasolutions.io`. Use the browser only for the Simulador UI (no WhatsApp send).

## Inputs
- `{flow_url}` — editor URL, e.g. `https://app.leonasolutions.io/flows/{id}/edit` (or open from Fluxos)
- `{start_message}` — optional first client message to type (demo used `oi`; empty + Enter also starts some flows)
- `{branches_to_cover}` — list of paths to walk (e.g. Disponible, No disponible, negociar, USDT, plegable)
- `{expected_copy}` — optional checklist of Spanish texts / nodes that must appear

## Steps
1. Open `{flow_url}` in the flow editor. Confirm the flow name and that the canvas loaded.
2. If the Simulador pane is closed, click **▶ Simular** (top-left of the canvas). The pane title is like "Simulador: Teste local, sem WhatsApp…".
3. Click the bottom input (`Digite para começar...` or later `Digite a resposta do cliente...`).
4. Start the run: type `{start_message}` and press Enter, or press Enter empty if that starts the flow. Confirm "Fluxo iniciado." and the first bot message. On the canvas, active nodes highlight green and the view may pan to follow them.
5. If the Simulador closes unexpectedly after a keypress, click **▶ Simular** again and continue from the input.
6. Reply as the customer for each wait state. Prefer labeled menu buttons when the flow offers them; otherwise type free-text answers. After each reply, check:
   - bot copy (language, product name, tone)
   - which canvas node is active (green)
   - that the conversation does not dead-end early
7. Walk every path in `{branches_to_cover}`. Restart the Simulador (close/reopen **▶ Simular** or restart the test) when you need a clean run for another branch.
8. Optional: use **Simular timeout (sem resposta)** only when validating timeout behavior.
9. Stop when all requested branches are covered or a blocker appears (login wall, missing node, wrong product, dead end).

## Report back
- Branches tested and pass/fail
- Exact bot messages that mismatched `{expected_copy}` (or surprising text)
- Dead ends, missing questions, wrong product/model, or broken conditionals
- Whether USDT / negotiation / unavailable paths behaved as specified
- Do **not** send WhatsApp messages or publish the flow; this is local Simulador only

## Notes
- Prefer stable UI targets: **▶ Simular**, Simulador input, menu option labels, canvas node titles — not coordinates.
- Do not embed credentials; login state lives in the browser profile.
