---
name: Status e alívio RAM
description: >-
  Use this when checking machine health as percentages (RAM, Swap, disk, load,
  CPU), reporting a status panel, or auto-relieving memory by closing extra
  browser/Claude processes when RAM or Swap exceeds agreed limits.
---
# Status e alívio de RAM

## Quando usar
- Pedido de status / “como está a máquina”
- Rotina diária de monitoramento
- Alívio de memória quando RAM ou Swap estão altos

## Sempre medir e reportar em %
Colete e mostre (nunca só Gi):
- **RAM %** usada (+ disponível)
- **Swap %** usada
- **Disco /** % usada
- **Load** 1m vs número de núcleos (~% de pressão = load/núcleos×100)
- **CPU** idle ou uso aproximado
- Serviços críticos do ambiente (ex.: PM2/Hermes): up/down curto

Tom: direto, curto, em português se o usuário falar português.

## Limites padrão de alívio
Disparar alívio automático se:
- **RAM > 75%** OU
- **Swap > 40%**

(Se o usuário pedir só relatório, não alivie.)

## Como aliviar (seguro)
1. Medir % **antes**
2. Encerrar **browsers extras** (Chrome/forks de agentes ociosos)
3. Encerrar sessões **Claude** CLI abertas, se existirem
4. **Nunca** matar: Hermes/PM2, sand-host, exec-daemon, supervisor, nem infra do sandbox
5. Medir % **depois**
6. Reportar tabela **Antes → Agora** em %

## Alertas extras (só se relevante)
- Disco > 80%
- Load perto ou acima do número de núcleos

## Não fazer
- Não ajustar tamanho de swap / swappiness neste fluxo (é outro assunto)
- Não inventar métricas — medir de verdade
- Não fechar serviços que o usuário depende no dia a dia (Hermes etc.)
