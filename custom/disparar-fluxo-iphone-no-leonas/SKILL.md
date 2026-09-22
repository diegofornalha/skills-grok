---
name: Disparar fluxo iPhone no Leonas
description: >-
  Use this when starting or accompanying a real iPhone seller conversation in
  Leonas chats — clear list filters, open a contact, and trigger the Iphone flow
  (not CCC).
---
# Disparar fluxo iPhone no Leonas

Assumes signed in to Leonas in the box browser as Empresa Agentes Grok.

## Goal

Open a seller chat on Live Chats and trigger the **Iphone** flow so the bot asks for the cash price of the iPhone 17. Then watch the real replies to compare price and behavior.

## Inputs

- `{contato}` — seller name or phone as shown in the list (examples: `Inverfin SAECA`, `Alemania Cell`, or a `+595…` number that later resolves to a name)
- `{fluxo}` — flow to trigger (default: `Iphone`)

## Steps

1. Open `https://app.leonasolutions.io/chats` (Chats ao vivo). Prefer a single Leonas tab.
2. In the middle list, stay on the status tab that holds the chat (**Aguardando**, **Atendendo**, or **Resolvidos** as needed).
3. **Always clear the unread filter.** If the chip **Não lidas** is active, click the x / switch so **Tudo** is selected. With **Não lidas** on, the list often shows “Nenhum chat encontrado” and hides the sellers you need.
4. Find `{contato}` in the list (name or phone preview; last message may be “Buen dia !” / “buen dia !”). Click it to open the thread on the right. The label may flip from `+595…` to the display name a few seconds after open.
5. In the chat header actions, click the rocket / flow icon (**Disparar fluxo**).
6. In the Disparar fluxo panel, open the flow picker. The list may include other flows such as **CCC - Renovação** and **Setup Inicial Grok Bot — Diagnóstico**. Select only **`{fluxo}`** (default **Iphone**) — click that named row; do not pick CCC or other flows.
7. Click purple **Ativar** without asking for confirmation when Diego has already approved a batch run / “só rode”.
8. Success checks:
   - Green toast: **Fluxo disparado com sucesso!**
   - Bot message appears in the thread asking for the precio al contado del iPhone 17.
   - Contact may jump in the list and the name may resolve if it was only a phone number.
9. Stay on the chat and report incoming seller replies (price, availability, negotiation, USDT, etc.) without inventing content.

## Batch (when Diego says run for all sellers)

Repeat steps 4–8 for each seller chat in the list. Skip system chats (e.g. **Avisos Leona Flow**). If the iPhone price question is already in the thread, skip that contact.

## Do not

- Leave **Não lidas** on when hunting for chats.
- Select **CCC - Renovação** or any flow other than **Iphone** for this campaign.
- Edit the flow graph from this skill (that is the Criar Fluxo Iphone / simulator lane).
- Send free-typed messages unless Diego asked for a specific reply.

## Notes

- Contact labels can flip between phone and display name after open or after Ativar.
- Flow editor URL for the iPhone flow is separate (`/flows/126172/edit`); this skill only uses **Chats ao vivo**.
