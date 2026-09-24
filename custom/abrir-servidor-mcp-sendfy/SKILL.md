---
name: Abrir Servidor MCP Sendfy
description: >-
  Use this when finding or connecting the Sendfy native MCP (Cursor/Claude/n8n)
  — open /mcp, copy SSE URL and API token, optionally add the remote MCP to
  Cursor.
---
# Abrir Servidor MCP Sendfy

Assumes signed in to [Sendfy](https://app.sendfy.app/) as the account owner. Prefer `?locale=pt-BR` when the UI supports it. There is **no** Sendfy plugin in the Cursor catalog; the MCP is served by Sendfy itself.

## Inputs
- `{connect_to_cursor}` — whether to also add the remote MCP to the user's Cursor account after copying credentials (`true` / `false`; default `false`)
- Stop after documenting the page if the user only asked where the MCP lives

## Steps
1. Open `https://app.sendfy.app/mcp` (or from the dashboard: expand the left sidebar, click **Servidor MCP**).
2. Confirm the page **Servidor MCP (Model Context Protocol)** loaded with badge **SERVIDOR ONLINE** (version shown in UI, e.g. V1.0.0).
3. Read and report (never store secrets in chat, memory, or this skill):
   - **URL do Servidor MCP (SSE):** `https://app.sendfy.app/mcp/sse` (button **Copiar URL**)
   - **Seu Token de Acesso** — header `x-api-key` (masked by default; eye icon reveals; **Copiar Token** shows alert "Token copiado com sucesso!")
   - Optional expand **URL Completa (One-Click com Token Embutido)** — **Copiar Conexão Rápida** embeds the token in the URL; treat as secret
   - **Limites & Capacidade:** subscription status, instances in use, total MCP tools count (UI shows ~33 tools)
4. **Never** paste the API token, one-click URL, or `api_key=` query into chat, skills, memory, or GitHub. If a secret must leave the browser, use a masked secret request / credential flow, not plaintext.
5. If `{connect_to_cursor}` is true:
   - Confirm with the user first (changes their Cursor account)
   - Add a remote MCP named e.g. `sendfy` with URL `https://app.sendfy.app/mcp/sse` and header `x-api-key: <token from the page>` (user provides the token via secure input; you never invent or reuse a token from a demo)
   - After add, tools appear on the next turn; verify with MCP status
6. If redirected to `/users/sign_in`, stop and report that sign-in is required.

## Report
- Final URL and whether the server badge is online
- SSE URL (safe to share)
- Whether the token was copied (yes/no) — **never** the token value
- Tool count / plan limits shown on the page
- Whether Cursor MCP was added (if requested)

## Notes
- Prefer labeled UI and the `/mcp` URL over coordinates
- Prefer the native Sendfy MCP over inventing a catalog plugin
- Do not encode CDP/Playwright harness details
- Login is out of scope — session lives in the signed-in browser profile
