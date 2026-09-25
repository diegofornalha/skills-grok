---
name: Finalizar cadastro WhatsApp no ProdHub
description: >-
  Use this when completing ProdHub registration that asks for WhatsApp on
  Configurações, or when the “Finalize seu cadastro” modal is open and needs a
  Brazilian mobile number in the app’s format.
---
# Finalizar cadastro WhatsApp no ProdHub

Assumes signed in to ProdHub in Chrome (`app.prodhub.com.br`).

## Goal
Submit the WhatsApp number on the **Finalize seu cadastro** modal so registration completes.

## Input
- `{whatsapp}` — Brazilian mobile with DDD (example raw: `+5521923670743` or `21923670743`)

## Format (required by the UI)
Convert `{whatsapp}` to: `(DD) XXXXX-XXXX`

Rules:
- Drop `+55` / leading `55` country code if present
- First 2 digits after country code = DDD
- Remaining 9 digits = mobile (5 + 4 with hyphen)
- Example: `+5521923670743` → `(21) 92367-0743`
- Placeholder on the field: `(11) 98765-4321`

Do **not** submit a partial value (e.g. only `21`). That yields the toast: `WhatsApp inválido. Formato esperado: (11) 98765-4321`.

## Steps
1. Open `https://app.prodhub.com.br/configuracoes` (or stay there if already open).
2. If the modal **Finalize seu cadastro** is visible (text about informing WhatsApp to conclude cadastro):
   - Focus the **WhatsApp** field
   - Clear any partial/wrong value
   - Type the formatted number `(DD) XXXXX-XXXX`
   - Click **Finalizar cadastro**
3. Success: modal closes; no error toast; no OTP expected in the demonstrated flow.
4. Failure: if the invalid-format toast appears, re-enter using the format above and submit again.
5. If the modal is **not** present, registration is already finished — report that and do not invent another place to edit WhatsApp unless the user points to one.

## Report
URL, formatted number submitted (not raw secrets beyond the phone), whether the modal closed, and any toast text.

## Out of scope
- Google SSO / login (assumes already signed in)
- Changing other Configurações fields
