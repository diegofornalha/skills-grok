---
name: Disparar fluxo iPhone no Leonas
description: >-
  Use this when working Leonas live chats for the iPhone campaign — scan the
  full list (do not stop at first), trigger Iphone on sellers still without the
  flow, mark off-topic Resolvido, evaluate replies.
---
# Disparar fluxo iPhone no Leonas

Assumes signed in to Leonas in the box browser as Empresa Agentes Grok.

## Goal

Open seller chats on Live Chats, trigger the **Iphone** flow for phone/iPhone sellers, archive off-topic chats as **Resolvido**, and watch real replies to compare price and behavior.

## Inputs

- `{contato}` — seller name or phone as shown in the list
- `{fluxo}` — flow to trigger (default: `Iphone`)

## Steps

1. Open `https://app.leonasolutions.io/chats` (Chats ao vivo). Prefer a single Leonas tab.
2. Work under **Aguardando** / **Atendendo**. Clear **Não lidas** so **Tudo** is selected.
3. **Scan the list — do not stop at the first contact.** Open chats one by one and classify each (below). Keep going until every visible candidate is handled (triggered, skipped as already-triggered, or Resolvido). Quitting after one open is wrong.
4. For each open contact:
   - **Already has the Iphone bot question** (or follow-up like “¿Qué te gustaría hacer con el precio del iPhone 17?”) → skip trigger; optionally note replies for evaluation; move to the **next** list item.
   - **iPhone / celular seller without that question yet** → Disparar fluxo → select **Iphone** only (never CCC - Renovação) → **Ativar**. Confirm toast + bot message, then continue to the next undtriggered seller.
   - **Off-topic** (tráfego, marketing genérico, sem celular/iPhone) → checkmark **Resolvido** → toast “Chat resolvido com sucesso” → continue scanning.
5. Success for a new trigger: toast **Fluxo disparado com sucesso!** and bot asks precio al contado del iPhone 17.
6. After the pass, evaluate new seller replies (price in guarani, availability, USDT, audio if possible). Report without inventing.

## How to tell “already triggered”

Look in the thread for the bot opener about iPhone 17 cash price, or later bot steps about that price (e.g. “Elegir una opción”). Preview snippets in the list like “Hola 👋 ¿Te gustaría conocer el prec…” often mean already triggered — still open to confirm if unsure, then move on.

## Archive off-topic (Resolvido)

Header → checkmark in a circle → toast **Chat resolvido com sucesso**. Do not trigger Iphone on that contact.

## Batch / continuous pass (required pattern)

Diego’s rule from teaching: **não desista na primeira tentativa**. Walk Aguardando top to bottom (scroll if needed). Skip already-fired. Fire the next without the flow. Repeat until no undtriggered iPhone sellers remain in the current list.

Then: evaluate replies on already-triggered threads; tell Diego / the Missão group only when useful (new triggers, Resolvidos, price sample for A/B); stay quiet if nothing new.

## Do not

- Stop after opening one chat that already had the flow.
- Leave **Não lidas** on when hunting.
- Select **CCC - Renovação** or any non-Iphone flow.
- Trigger Iphone on off-topic instead of Resolvido.
- Edit the flow graph (Manutenção Fluxo principal Iphone / simulador).
- Send free-typed messages unless Diego asked.

## Notes

- Labels may flip phone ↔ name after open or Ativar.
- After Resolvido, Aguardando may briefly look empty for that filter — continue with remaining chats.
- Flow editor (separate): `https://app.leonasolutions.io/flows/126172/edit`.
