---
name: ip-com-subdominio-https
description: >-
  Use this when exposing an app via IP, localhost, or a raw port — always pair
  it with an HTTPS subdomain (Cloudflare tunnel + DNS) as the default public
  URL.
---
# IP / localhost always with HTTPS subdomain

## When to apply
Whenever an app, preview, or server is exposed by **IP**, **localhost**, or a **raw port** (e.g. `http://127.0.0.1:8765`), treat the local address as internal origin only. The default public URL must be an **HTTPS subdomain** on the user's domain (Cloudflare tunnel + DNS), same pattern as `crud.example.com` → local app.

## Goals
- User opens HTTPS on their domain, not IP/port.
- Apex/main site stays intact (use a **subdomain**; never replace the root domain without explicit ask).
- When deleting a published app, also ask whether to remove DNS / tunnel / subdomain.

## Steps

1. **Confirm the local app**
   - Service healthy on origin (e.g. `http://127.0.0.1:<port>`).
   - Note project folder, port, and process.

2. **Pick the hostname**
   - Ask or propose a short descriptive subdomain (e.g. `crud.`, `app.`, `preview.`).
   - Confirm the base domain (user's Cloudflare zone).
   - Do not use the apex for the app without explicit confirmation.

3. **Authenticate Cloudflare (if tunnel cert missing)**
   - Prefer `cloudflared tunnel login` on the assistant computer (user signs in via browser).
   - Alternative: API token with DNS + tunnel permissions, if the user prefers.

4. **Create named tunnel + DNS**
   - Create a stably named tunnel (e.g. `items-crud`).
   - Route DNS: `tunnel route dns <tunnel> <sub.domain>` (CNAME to the tunnel).
   - Ingress config: hostname → `http://127.0.0.1:<port>`; fallback `http_status:404`.
   - Run the tunnel; verify `Registered tunnel connection`.

5. **Validate public HTTPS**
   - `GET https://<subdomain>` returns 200 (or expected app response).
   - Confirm Cloudflare / TLS headers.
   - Deliver the **HTTPS link** as the primary URL; localhost is internal detail only.

6. **Persist and clean up safely**
   - Remember public URL, tunnel name, port, and folder.
   - If the user deletes the app folder, **ask** whether to also remove subdomain / DNS / tunnel (never assume).

## Anti-patterns
- Shipping only `http://IP:port` or `http://127.0.0.1` as the official link.
- Using `*.trycloudflare.com` as a permanent stand-in for the user's subdomain (ok only as a temporary quick test).
- Deleting DNS/tunnel without explicit hostname confirmation.
- Taking down the apex site to publish an app.

## Done when
User has working `https://<sub>.<domain>`, stable tunnel, and delete/cleanup confirmation covers both app and domain resources.
