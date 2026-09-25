---
name: Conectar LinkedIn no ProdHub
description: >-
  Use this when connecting or reconnecting LinkedIn on ProdHub Outbound (Unipile
  auth), or when the UI shows LinkedIn desconectado / Conectar LinkedIn.
---
# Conectar LinkedIn no ProdHub

Assumes signed in to ProdHub in Chrome (`app.prodhub.com.br`).

## Goal
Connect a LinkedIn account to ProdHub Outbound via Unipile so the UI shows **LinkedIn conectado**.

## When to use
- Outbound shows **LinkedIn desconectado** / button **Conectar LinkedIn**
- User asks to connect or reconnect LinkedIn on ProdHub

## Steps
1. Open `https://app.prodhub.com.br/linkedin/outbound`.
2. If status already shows **LinkedIn conectado** with a profile name, report connected and stop (optional: **Reconectar LinkedIn** only if the user asked to reconnect).
3. If disconnected, click **Conectar LinkedIn**. This opens Unipile at `auth.unipile.com` (“Sign in to LinkedIn to connect an account with Prod Hub”).
4. **Credentials (user only):** complete LinkedIn email/password on the Unipile form. Never store or embed passwords in this skill. Prefer in-chat form or box handoff for that step; do not screenshot password fields.
5. After LinkedIn sign-in, Unipile may show **Select your products**. Leave **Personal** and **Company Pages** checked (as demonstrated), then click **Next**.
6. Expect redirect to `https://app.prodhub.com.br/linkedin/outbound?connection=success` (query may clear after load).

## Success criteria
- Green toast: **Conta do LinkedIn conectada e sincronizada com sucesso.**
- Left status: **LinkedIn conectado** with the LinkedIn profile name (demo showed Diego Alcantara)
- Header actions may include **Reconectar LinkedIn** and **Sincronizar Aceites**
- Failure: status stays **LinkedIn desconectado** or Unipile never returns with `connection=success` — report URL and UI text; do not invent a connected state

## Related routes (context, not required for connect)
- Inbound: `https://app.prodhub.com.br/linkedin/inbound`
- Inbound strategy: `https://app.prodhub.com.br/linkedin/inbound/strategy`

## Out of scope
- Creating outbound campaigns, sending invites, or changing Segurança e limites
- Storing LinkedIn passwords
