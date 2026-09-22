---
name: Atualizar Leonas com uma aba
description: >-
  Use this when opening or revisiting a Leonas flow editor page — refresh the
  page and keep only one browser tab so the canvas is current and not confusing.
---
# Atualizar Leonas com uma aba

When working in the Leonas Solutions flow editor (`app.leonasolutions.io/flows/{flowId}/edit`), always prepare the browser like this before inspecting or editing.

## Steps

1. Open (or focus) the target flow URL: `https://app.leonasolutions.io/flows/{flowId}/edit`. Assumes the browser is already signed in to Leonas.
2. Refresh the page with the browser reload control so the canvas shows the latest saved flow (Leonas can look stale if left open).
3. If more than one Leona/tab is open, close the extras and leave **only one** tab — the refreshed flow editor — so you do not edit or simulate the wrong tab.
4. Confirm the remaining tab URL matches the intended `{flowId}` and the flow title on screen, then continue the real task (edit, simulate, report).

## Inputs

- `{flowId}` — the numeric flow id (example: `126172` for the Iphone flow).

## Notes

- Do not invent a second tab; close duplicates.
- Ignore incidental UI like a Google Translate popup after reload unless it blocks the canvas.
- This is prep only: it does not change the flow graph.
