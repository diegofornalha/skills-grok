---
name: Disparar fluxo iPhone no Leonas
description: >-
  Use this when working Leonas live chats for the iPhone price campaign — clear
  filters, trigger Iphone on sellers, mark off-topic chats Resolvido, evaluate
  replies.
---
# Disparar fluxo iPhone no Leonas

Assumes signed in to Leonas in the box browser as Empresa Agentes Grok.

## Goal

Open seller chats on Live Chats, trigger the **Iphone** flow for phone/iPhone sellers, archive off-topic chats as **Resolvido**, and watch real replies to compare price and behavior.

## Inputs

- `{contato}` — seller name or phone as shown in the list (examples: `Alemania Cell`, `Rodriphone`, or a `+595…` number that later resolves to a name)
- `{fluxo}` — flow to trigger (default: `Iphone`)

## Steps

1. Open `https://app.leonasolutions.io/chats` (Chats ao vivo). Prefer a single Leonas tab.
2. In the middle list, work mainly under **Aguardando** / **Atendendo**.
3. **Always clear the unread filter.** If **Não lidas** is active, clear it so **Tudo** is selected.
4. Open a contact. Classify the thread:
   - **iPhone / celular seller** → keep and (if needed) trigger the flow below.
   - **Not about iPhone** (e.g. tráfego pago, marketing, unrelated pitch) → **archive as Resolvido** (see Archive) and do not trigger Iphone.
5. For iPhone sellers without the bot price question yet: click the rocket / flow icon (**Disparar fluxo**).
6. In the panel, select only **`{fluxo}`** (default **Iphone**). The list may also show **CCC - Renovação** and **Setup Inicial Grok Bot — Diagnóstico** — never pick those for this campaign. Typing `iphone` in the search is optional.
7. Click purple **Ativar** without asking when Diego already approved a batch / “só rode”.
8. Success checks for trigger:
   - Toast **Fluxo disparado com sucesso!**
   - Bot asks for precio al contado del iPhone 17.
9. Watch replies (price in guarani, availability, negotiation, USDT, voice notes if transcribable). Report without inventing.

## Archive off-topic (Resolvido)

When the open chat is clearly **not** about iPhone/celular:

1. In the chat header actions, click the **checkmark in a circle** (resolve).
2. Success: toast **Chat resolvido com sucesso**; status becomes **Resolvido por Agentes Grok**; the chat leaves **Aguardando**.
3. Do not send free messages; do not trigger Iphone on that contact.

Example from teaching: **Junior Rezende Trafego** (paid traffic / Instagram) → Resolvido.

## Batch round

1. List who already has the Iphone bot question.
2. Identify new iPhone sellers → Disparar Iphone.
3. Off-topic chats → Resolvido.
4. Evaluate replies on already-triggered threads.
5. Tell Diego only when something useful happened; stay quiet if nothing new.

## Do not

- Leave **Não lidas** on when hunting for chats.
- Select **CCC - Renovação** or any non-Iphone flow for this campaign.
- Trigger Iphone on off-topic chats instead of Resolvido.
- Edit the flow graph from this skill (that is manutenção Fluxo Iphone / simulador).
- Send free-typed messages unless Diego asked.

## Notes

- Contact labels can flip between phone and display name after open or after Ativar.
- After Resolvido, the **Aguardando** list may look empty for that filter — switch tabs or clear filters to continue.
- Flow editor: `https://app.leonasolutions.io/flows/126172/edit` (separate from this chats skill).
