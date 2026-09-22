---
name: Disparar fluxo iPhone no Leonas
description: >-
  Use this when starting or accompanying a real iPhone seller conversation in
  Leonas chats — open a contact, clear list filters, and trigger the Iphone
  flow.
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
2. In the middle list, stay on the status tab that holds the chat (usually **Aguardando** or **Atendendo**).
3. **Always clear the unread filter.** If the chip **Não lidas** is active, click it so **Tudo** is selected. With **Não lidas** on, the list often shows “Nenhum chat encontrado” and hides the sellers you need.
4. Find `{contato}` in the list (name or phone preview; last message may be “Buen dia !” / “buen dia !”). Click it to open the thread on the right.
5. In the chat header actions, click the rocket / flow icon (**Disparar fluxo**).
6. In the Disparar fluxo panel, open the flow picker (“Digite o nome do fluxo…”). Select **`{fluxo}`** (default **Iphone**) from the list — click the named row; typing is optional.
7. **Confirm with Diego before clicking Ativar** — this sends a real WhatsApp message to the seller.
8. After approval, click purple **Ativar**.
9. Success checks:
   - Green toast: **Fluxo disparado com sucesso!**
   - Bot message appears in the thread, e.g. asking for the precio al contado del iPhone 17.
10. Stay on the chat and report incoming seller replies (price, availability, negotiation, USDT, etc.) without inventing content.

## Do not

- Leave **Não lidas** on when hunting for chats.
- Trigger **Ativar** without Diego’s OK for that contact.
- Edit the flow graph from this skill (that is the Criar Fluxo Iphone / simulator lane).
- Send free-typed messages unless Diego asked for a specific reply.

## Notes

- Contact labels can flip between phone and display name after open.
- Flow editor URL for the iPhone flow is separate (`/flows/126172/edit`); this skill only uses **Chats ao vivo**.
