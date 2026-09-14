---
name: Cloudflare MCP vs CLI
description: >-
  Use this when choosing between Cloudflare MCP connectors and the wrangler CLI
  for a development task — docs, builds, observability, bindings, deploy, local
  dev, secrets, types, KV/D1/R2/Queues, Pages, or incident debug.
---
# Cloudflare: MCP vs CLI

Use this skill **before** picking a path. Goal: choose the fastest correct tool for the task.

## Quick rule

| Need | Prefer | Why |
|------|--------|-----|
| Consultar docs / API / exemplos oficiais | **MCP** `Cloudflare-docs` | Resposta rápida no chat |
| Status de build / deploy recente / histórico | **MCP** `Cloudflare-builds` | Estado ao vivo sem dashboard |
| Métricas, logs, erros, saúde do Worker | **MCP** `Cloudflare-observability` | Observabilidade sem query manual |
| Listar / inspecionar bindings e recursos da conta | **MCP** `Cloudflare-bindings` | Inventário via conector (precisa auth) |
| “O que é X na Cloudflare?” / comparar produtos | **MCP** `Cloudflare-docs` (+ skill `cloudflare`) | Decisão de produto antes de codar |
| Init, scaffold, `dev`, `deploy`, environments | **CLI** `wrangler` | Mutação real no código e na conta |
| Secrets, `types`, `check`, config local | **CLI** `wrangler` | Comandos canônicos no projeto |
| KV / D1 / R2 / Queues / Vectorize no projeto | **CLI** `wrangler` | Criar, migrar, seed, binding no `wrangler.jsonc` |
| Pages / preview URL / publish | **CLI** (wrangler / C3) | Deploy e preview locais |
| Túnel / subdomínio HTTPS público | Skill **ip-com-subdominio-https** | Padrão de URL pública, não MCP vs CLI |

## Mais casos — preferir MCP

1. Confirmar sintaxe de API, limites, headers, pricing de produto → `Cloudflare-docs`.
2. “Esse build falhou? Qual commit? Quanto tempo levou?” → `Cloudflare-builds`.
3. “Tem spike de 5xx / CPU / request?” ou pegar stack de erro recente → `Cloudflare-observability`.
4. “Quais Workers / KV / D1 existem na conta?” (leitura) → `Cloudflare-bindings` se autenticado.
5. Tirar dúvida **sem** abrir o dashboard e **sem** editar repo.
6. Validar pós-deploy: build verde + métrica ok, ainda no chat.
7. Comparar opções (Workers vs Pages vs DO) antes de escolher stack → docs (+ skill `cloudflare`).

## Mais casos — preferir CLI (`wrangler`)

1. `wrangler init` / `create-cloudflare` / novo Worker ou app.
2. `wrangler dev` (local, hot reload, bindings locais vs `remote: true`).
3. `wrangler deploy` / environments (`staging`, `production`).
4. `wrangler secret put|list|delete` e Secrets Store.
5. `wrangler types` após mudar bindings; `wrangler check` antes de deploy.
6. Editar `wrangler.jsonc` (routes, compatibility_date, vars, triggers).
7. Recursos de dados no ciclo de vida do projeto:
   - KV: namespaces, put/get de teste
   - D1: create, migrations, execute SQL
   - R2: buckets, upload de teste
   - Queues / Vectorize / Hyperdrive: create + binding
8. Cron triggers, custom domains no Worker, tail de log **durante** debug local (`wrangler tail` quando MCP não basta).
9. Pages: build local, preview, publish.
10. Qualquer ação que **precise persistir no git** (config, migrations, scripts).

## Use os dois (sequências típicas)

**Feature nova**
1. MCP docs → confirmar API / produto
2. CLI → implementar, types, check, deploy
3. MCP builds + observability → validar

**Incidente / bug em prod**
1. MCP observability → achar erro / métrica
2. MCP docs → confirmar comportamento esperado
3. CLI → corrigir, `check`, redeploy
4. MCP builds + observability → confirmar recuperação

**Onboarding de recurso (ex.: D1)**
1. MCP docs → modelo e limites
2. CLI → create, migration, binding, types
3. MCP bindings (se auth) → conferir que o recurso apareceu na conta

## Checklist de decisão (1 minuto)

1. Só leitura no chat? → MCP.
2. Altera projeto, config ou conta via comando? → CLI.
3. Deploy / preview / secret / types / check / migration? → CLI.
4. Doc, build status, métrica, inventário de conta? → MCP correspondente.
5. Expor app por IP/porta? → skill de subdomínio HTTPS.
6. MCP sem auth ou sem cobertura? → CLI (ou autenticar o conector, sem improvisar no browser).

## Anti-padrões

- Usar CLI só para “ver uma métrica” se observability MCP está ok.
- Usar MCP quando a ação é deploy/config — MCP não substitui `wrangler deploy`.
- Criar recurso só no dashboard e esquecer binding/local no CLI.
- Misturar tunnel/DNS de domínio com “qual MCP usar”; isso é outra skill.

## Depois de escolher

- **MCP:** conector certo; se `needsAuth`, autenticar antes de improvisar no browser.
- **CLI:** skill `wrangler` (v4+, `wrangler.jsonc`, `compatibility_date`, `wrangler check` antes de deploy).
